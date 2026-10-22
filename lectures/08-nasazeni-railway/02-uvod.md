---
id: uvod
title: Úvod
---

# Nasazení na Railway

Minule jsi CRM pokryl(a) testy: jednotkovými, integračními i testy v prohlížeči. Aplikace funguje a víš to jistě. Zatím ale běží jen na tvém počítači a obchodníci Webovky ji nemají jak otevřít. Dnes to změníš:

1. **Co je nasazení** – co se stane, když aplikace "jde na internet", a proč k tomu použijeme Railway.
2. **Příprava aplikace** – co se musí v aplikaci změnit, aby mohla bezpečně běžet na internetu, včetně přihlašování.
3. **Nasazení na Railway** – jak z repozitáře na GitHubu vznikne běžící aplikace s databází a veřejnou adresou.
4. **Když se něco pokazí** – jak číst logy na Railway a jak se vrátit k verzi, která fungovala.
5. **Cena a úklid** – kolik nasazená aplikace stojí a jak ji po kurzu vypnout.

**Proč to potřebuješ:** Aplikace, kterou nikdo nemůže otevřít, nikomu nepomáhá. Metriku úspěchu z produktové analýzy, "obchodníci už nepoužívají tabulku v Excelu", nesplníš, dokud CRM běží jen u tebe. Nasazení je zároveň chvíle, kdy se z učebního projektu stává věc, kterou používají skuteční lidé, a s tím přichází nová odpovědnost: hesla, přihlášení a data, která nesmí uniknout. Docker z lekce 06 a testy z lekce 07 jsou přesně to, co nasazení usnadní.

**Po lekci budeš umět:**
- Víš, co je nasazení, server a PaaS a čím se liší vývojové a produkční nastavení aplikace.
- Umíš s agentem připravit aplikaci v Djangu na nasazení: tajný klíč a hesla v proměnných, vypnutý ladicí režim, přihlašování a migrace při nasazení.
- Umíš nasadit aplikaci z GitHubu na Railway s databází PostgreSQL a veřejnou adresou.
- Umíš najít chybu v logech na Railway a vrátit se k předchozímu nasazení.
- Víš, kolik nasazení stojí, kde hlídáš spotřebu a jak projekt po kurzu smazat.
