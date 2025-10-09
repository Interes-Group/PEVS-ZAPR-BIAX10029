---
date: '2025-10-09T10:02:06+02:00'
title: 'Úloha 3.7'
weight: 7
---

Napíšte program, zdrojový kód, v jazyku C použitím štandardu C17, ktorý realizuje nasledovnú činnosť.
Definujte funkciu **_int druhe_najvacsie(int n)_** s parametrom celé číslo _n_. Funkcia načíta n čísiel z
klávesnice a vráti druhé najväčšie načítané číslo (druhé maximum). V prípade, že má parameter _n_
hodnotu menšiu ako 2, funkcia vypíše chybovú hlášku, že hodnota vstupného argumentu funkcie
musí byť aspoň 2 a ukončí program.

### Príklady vstupov / výstupov programu

- Volanie `druhe_najvacsie(1)` vypíše chybu a skončí.
- Volanie `druhe_najvacsie(5)` načíta 5 čísiel z klávesnice. Ak sú tieto čísla napríklad 5,-2,1,2,3
  funkcia vráti číslo 3, pretože -2 ≤ 1 ≤ 2 ≤ 3 ≤ 5
- Volanie `druhe_najvacsie(3)` načíta 3 čísla z klávesnice. Ak sú tieto čísla napríklad -10, -5, 0 funkcia
  vráti číslo -5, pretože -10 ≤ -5 ≤ 0

> [!TIP]
> Pri implementácia môžte použiť knižnicu limits.h. `#include <limits.h>`, ktorá obsahuje konštanty pre maximálne
> a minimálne hodnoty dátových typov.

---

{{< details title="Rozbaľ pre ukážku riešenia" closed="true" >}}

Musím si počkať kým sa tu objaví príklad riešenia.

Nezabudni, že najviac sa naučíš ak to vypracuješ sám. 😉

{{< /details >}}
