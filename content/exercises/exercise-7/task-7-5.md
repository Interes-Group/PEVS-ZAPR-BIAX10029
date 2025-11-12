---
date: '2025-11-12T23:19:13+01:00'
title: 'Úloha 7.5'
weight: 5
---

Napíšte program, zdrojový kód, v jazyku C použitím štandardu C17, ktorý na začiatku alokuje pamäť o veľkosti 5 čísel
(t.j. pole veľkosti `5 * sizeof(int)`). Následne umožní používateľovi pridávať hodnoty to poľa zo štandardného vstupu.
Ak sa pole naplní, zmeňte jeho alokovanú veľkosť na dvojnásobnú aktuálnej veľkosti a umožnite používateľa ďalej zadávať
čísla. Pokračujte načítanie hodnôt pokým používateľ nezadá hodnotu **-1**, ktorý ukonči zadávanie čísel.

Na záver, program vypíše všetky načítané čísla, veľkosť a adresu alokovanej pamäte.

Nezabudnite patrične uvoľniť alokovanú pamäť a ošetriť prípady keď alokácia pamäte zlyhá.

### Príklady vstupov / výstupov programu

Priebeh programu môže byť nasledovný:

```text
Zadajte hodnoty (zadaním -1 ukončíte): 
10
20
30
40
50
60
70
-1
---
Zadané hodnoty: 10 20 30 40 50 60 70
Konečná veľkosť poľa: 10 prvkov
Adresa poľa: 0x000044781dcc
```

---

{{< details title="Rozbaľ pre ukážku riešenia" closed="true" >}}

Musím si počkať kým sa tu objaví príklad riešenia.

Nezabudni, že najviac sa naučíš ak to vypracuješ sám. 😉

{{< /details >}}
