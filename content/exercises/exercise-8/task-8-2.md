---
date: '2025-11-12T23:39:39+01:00'
title: 'Úloha 8.2'
weight: 2
---

Napíšte program, zdrojový kód, v jazyku C použitím štandardu C17, ktorý vytvorí štruktúru na reprezentáciu zamestnanca.

Štruktúra by mala obsahovať:

- _meno_ (pole znakov)
- _identifikačné číslo_ (celé číslo)
- _plat_ (desatinné číslo)

Program by mal načítať údaje pre niekoľko zamestnancov, zoradiť ich podľa platu zostupne a
vypísať zoznam zamestnancov spolu s ich platmi. Následne program vypíše priemerný plat zamestnancov.

Údaje o zamestnancoch načítajte zo súboru, kde na jednom riadku je definovaný jeden zamestnanec a hodnoty na riadku sú
oddelené medzerou: `ID Meno Plat`

Cestu k súboru načítajte od používateľa zo štandardného vstupu na začiatku programu.

### Príklady vstupov / výstupov programu

Program pre vstupný súbor:

```text
101 Anna 2500.50
102 Peter 3000.75
103 Lucia 2800.00
```

vypíše nasledovný text na výstupe:

```text
102 Peter 3000.75
103 Lucia 2800.00
101 Anna 2500.50
---
Priemerný plat: 2767.08
```

### Bonus

Skúste upraviť výpis tak aby mal formát tabuľky. Nezabudnite na správne zarovnanie stĺpcov. Takýto výstup by mohol
vyzerať nasledovne:

```text
|ID  |Meno  |Plat    |
|----|------|--------|
|102 |Peter |3000.75 |
|103 |Lucia |2800.00 |
|101 |Anna  |2500.50 |
---
Priemerný plat: 2767.08
```

---

{{< details title="Rozbaľ pre ukážku riešenia" closed="true" >}}

Musím si počkať kým sa tu objaví príklad riešenia.

Nezabudni, že najviac sa naučíš ak to vypracuješ sám. 😉

{{< /details >}}
