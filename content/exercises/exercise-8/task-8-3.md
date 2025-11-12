---
date: '2025-11-12T23:39:41+01:00'
title: '🗓️ Úloha 8.3'
weight: 3
---

Napíšte program, zdrojový kód, v jazyku C použitím štandardu C17, ktorý definuje štruktúru na reprezentáciu dátumu s
položkami:

- _deň_ (celé číslo)
- _mesiac_ (celé číslo)
- _rok_ (celé číslo)

Program by mal umožniť používateľovi zadať dva dátumy kde jednotlivé hodnoty dátumov sú
definované v jednom riadku oddelené medzerou
a vypočítať rozdiel medzi nimi. Rozdieľ je vypísaný ako počet dní medzi dátumami.

V programe ošetrite vstup od používateľa aby bolo možné zadať iba správny dátum (napríklad nie je možné zadať 31.2.) a
zohľadňuje priestupné roky.

### Príklady vstupov / výstupov programu

Priebeh programu môže vyzerať nasledovne:

```text
Prvý dátum: 1 1 2023
Druhý dátum: 15 1 2024
---
Rozdiel dátumov: 376 dní
```

```text
Prvý dátum: 28 2 2020
Druhý dátum: 1 3 2020
---
Rozdiel dátumov: 2 dni
```

### Bonus

Skúste upraviť výpis rozdielu dátumov tak aby uviedol pre používateľa rozdiel aj koľko prípadných rokov, mesiacov, či
dní je medzi dátumami. Napríklad:

- vstup: 1.1.2023 a 15.1.2024 -> 1 rok a 15 dní
- vstup: 1.1.2022 a 5.3.2022 -> 2 mesiace a 5 dní

---

{{< details title="Rozbaľ pre ukážku riešenia" closed="true" >}}

Musím si počkať kým sa tu objaví príklad riešenia.

Nezabudni, že najviac sa naučíš ak to vypracuješ sám. 😉

{{< /details >}}
