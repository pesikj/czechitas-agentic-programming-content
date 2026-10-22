---
id: kam-dal
title: Kam dál
---

# Kam dál

- **Testy před nasazením.** Nech agenta nastavit GitHub Actions tak, aby se testy spustily při každém pull requestu, a v nastavení služby na Railway zapni čekání na úspěšné testy (*Wait for CI*). Rozbitá verze se pak na internet nedostane.
- **Vlastní doména.** Pokud máš vlastní doménu, připoj ji v **Settings → Networking** a nezapomeň ji přidat do `ALLOWED_HOSTS` a `CSRF_TRUSTED_ORIGINS`.
- **Záloha databáze.** Zeptej se agenta, jak udělat zálohu databáze PostgreSQL na Railway a jak ji obnovit. Vyzkoušej to na zkušebních datech.
- **Účty pro obchodníky.** Přihlas se do administrace na Railway a vytvoř účty pro tři obchodníky Webovky. Ověř, že se každý přihlásí a vidí stejná data.
- **Sleduj spotřebu.** Po týdnu otevři na Railway přehled spotřeby. Kolik stála aplikace a kolik databáze?

Chceš vědět víc? [Railway: nasazení Djanga](https://docs.railway.com/guides/django) · [Django: kontrolní seznam před nasazením](https://docs.djangoproject.com/en/stable/howto/deployment/checklist/)

Příště budeš v aplikaci CRM pokračovat.
