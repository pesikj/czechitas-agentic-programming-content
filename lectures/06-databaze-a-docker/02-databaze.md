---
id: databaze
title: Databáze v Djangu
---

# Databáze v Djangu

Tvoje CRM si pamatuje firmy i po restartu serveru. Kam je ale ukládá? A co se stane s daty, když agenta požádáš, aby k firmě přidal nový údaj? Abys mohl(a) agentovu práci s daty zkontrolovat, potřebuješ rozumět tomu, jak Django s databází pracuje.

## Co je databáze

> **Kdy se to hodí:** Obchodnice ti napíše, že firma "Pekárna U Lípy" z CRM zmizela. Než požádáš agenta o opravu, chceš sám(a) zjistit, jestli firma v datech opravdu chybí, nebo ji jen nevidíš v seznamu.

*Databáze* je místo, kam aplikace ukládá data tak, aby v nich mohla rychle hledat, měnit je a aby nezmizela po vypnutí. Představ si ji jako sešit v Excelu:

- **Tabulka** je jeden list sešitu. CRM má tabulku pro firmy a tabulku pro obchodní případy.
- **Sloupec** je jeden údaj: název, IČO, stav.
- **Řádek** je jeden záznam: jedna konkrétní firma.

Rozdíl proti Excelu je v tom, že databáze hlídá pravidla. Do sloupce s hodnotou obchodu nepustí text a obchodní případ nedovolí přiřadit k firmě, která neexistuje.

Django ve výchozím nastavení používá databázi *SQLite*. Celá databáze je jeden soubor, `db.sqlite3` ve složce projektu. Nepotřebuje žádný server ani instalaci, proto je ideální na začátek. Najdeš ho v Exploreru ve VS Code.

## Od modelu k tabulce

Tabulky jsi nikdy nevytvářel(a) ručně. Agent napsal v souboru `obchod/models.py` *modely* a Django z nich tabulky vytvořilo. Model firmy může vypadat třeba takhle (tvůj se může v detailech lišit):

```python
class Firma(models.Model):
    nazev = models.CharField(max_length=200)
    ico = models.CharField(max_length=8)
    email = models.EmailField(blank=True)
    telefon = models.CharField(max_length=20, blank=True)
    stav = models.CharField(max_length=20, choices=STAVY, default="nova")
```

- Třída `Firma` je jedna tabulka, Django ji pojmenuje `obchod_firma` (název aplikace a modelu).
- Každý řádek s `models....` je jeden sloupec. `CharField` je text s nejvyšší délkou, `EmailField` text, který musí vypadat jako e-mail, `DecimalField` (u obchodního případu) přesné desetinné číslo pro peníze.
- `blank=True` znamená, že údaj je nepovinný. `default="nova"` je výchozí hodnota.
- Sloupec `id` v modelu nevidíš, ale Django ho přidá samo. Každá firma tak dostane jedinečné číslo.

Obchodní případ má pole `firma = models.ForeignKey(Firma, ...)`. *Cizí klíč* (anglicky *foreign key*) je sloupec, ve kterém je uložené `id` firmy. Tak databáze ví, ke které firmě případ patří.

## Migrace: jak se model dostane do databáze

Model je jen popis v Pythonu. Aby z něj vznikla tabulka, potřebuješ dva příkazy, které už znáš z plánu:

```bash
uv run python manage.py makemigrations
uv run python manage.py migrate
```

- `makemigrations` porovná modely se stavem databáze a změny zapíše do souboru *migrace*, třeba `obchod/migrations/0001_initial.py`. Migrace je recept: "vytvoř tabulku firem s těmito sloupci".
- `migrate` recept provede a databázi upraví.

Migrace mají pořadová čísla a ukládají se do Gitu. Kdokoli si projekt stáhne, spustí `migrate` a dostane stejné tabulky. Které migrace už jsou v databázi provedené, ti ukáže:

```bash
uv run python manage.py showmigrations obchod
```

Výstup:

```text
obchod
 [X] 0001_initial
```

Databáze ve skutečnosti nemluví Pythonem, ale jazykem *SQL*. Django ti ukáže, co z migrace přeloží:

```bash
uv run python manage.py sqlmigrate obchod 0001
```

Výstup (zkrácený):

```text
CREATE TABLE "obchod_firma" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT,
"nazev" varchar(200) NOT NULL, "ico" varchar(8) NOT NULL, ...);
```

SQL psát nemusíš, za tebe ho píše Django. Stačí poznat, že `CREATE TABLE` vytváří tabulku a v závorce jsou její sloupce.

## Jak se na data podíváš

**Administrace.** Nejpohodlnější cesta je administrace Djanga, kterou ti agent připravil v minulé lekci: spusť server a otevři http://127.0.0.1:8000/admin/. Uvidíš tabulky jako seznamy a každý řádek si můžeš otevřít.

**Django shell.** Když se chceš na data zeptat přesněji, použij *Django shell*: Python, který je rovnou připojený k databázi projektu. V terminálu ve VS Code spusť:

```bash
uv run python manage.py shell
```

A zkus:

```python
from obchod.models import Firma

Firma.objects.all()
Firma.objects.filter(stav="lead")
Firma.objects.count()
```

Výstup (s tvými firmami):

```text
<QuerySet [<Firma: Pekárna U Lípy>, <Firma: Autoservis Novák>]>
<QuerySet [<Firma: Pekárna U Lípy>]>
2
```

`Firma.objects` je přístup k tabulce firem. `all()` vrátí všechny řádky, `filter(stav="lead")` jen ty, které odpovídají podmínce, a `count()` jejich počet. Django každý dotaz přeloží do SQL a výsledek ti vrátí jako Python. Shell ukončíš příkazem `exit()`.

Pokud místo názvu firmy vidíš `<Firma: Firma object (1)>`, model nemá metodu `__str__`, která říká, jak firmu vypsat. Můžeš o ni požádat agenta.

## Změna modelu: nové pole

> **Kdy se to hodí:** Obchodníci chtějí mít u firmy odkaz na její web, aby si ho před schůzkou mohli rychle otevřít. Musíš přidat sloupec do tabulky, ve které už jsou data.

Změna modelu je místo, kde se data ztrácejí nejsnáz. Přidání nepovinného pole je bezpečné. Smazání nebo přejmenování pole ale může data smazat, protože Django sloupec odstraní i s obsahem.

Proto postupuj opatrně:

1. **Zazálohuj databázi.** Zkopíruj soubor `db.sqlite3` třeba na `db-zaloha.sqlite3`. Git ti tady nepomůže: `db.sqlite3` je v `.gitignore`, takže Git ukládá kód a migrace, ale ne data.
2. **Nech agenta připravit migraci, ale ne ji spustit.**

Prompt pro agenta:

```text
Přidej k firmě nepovinné pole web pro odkaz na webové stránky firmy.
Zobraz ho v seznamu firem i ve formuláři. Vytvoř migraci, ale nespouštěj ji.
Ukaž mi, co migrace změní v databázi.
```

3. **Přečti migraci.** Výstup `makemigrations` by měl vypadat takhle:

```text
Migrations for 'obchod':
  obchod/migrations/0002_firma_web.py
    + Add field web to firma
```

Znaménko `+` znamená, že se něco přidává. Kdybys uviděl(a) `- Remove field`, migrace by sloupec mazala i s daty. Takovou migraci nespouštěj, dokud nevíš proč.
4. **Spusť migraci** (`uv run python manage.py migrate`) a ověř v administraci, že firmy zůstaly a mají nové prázdné pole web.

## Cvičení: Nové pole u firmy

Přidej k obchodnímu případu nepovinné datum, do kdy se má obchodník zákazníkovi ozvat (třeba `pristi_krok`). Postupuj podle návodu výše: záloha, migrace bez spuštění, kontrola, spuštění. Pak v Django shellu zjisti, kolik obchodních případů nemá datum vyplněné. Pokud nevíš, jak dotaz napsat, požádej agenta a nech si ho vysvětlit.

```exercise
id: nove-pole-pripadu
revision: 1
title: Nové pole u obchodního případu
fields:
  - id: migrace
    label: Co migrace změnila
    guidance: Jak se migrace jmenuje? Které řádky výstupu makemigrations ukazují, co se v databázi změní?
  - id: data
    label: Zůstala data zachovaná?
    guidance: Jak jsi ověřil(a), že se po migraci neztratila žádná firma ani obchodní případ?
  - id: shell
    label: Dotaz v Django shellu
    guidance: Jaký dotaz jsi použil(a) a co vrátil?
```
