---
date: '2025-10-09T10:02:09+02:00'
title: '✨ Úloha 3.8'
weight: 8
---

Napíšte program, zdrojový kód, v jazyku C použitím štandardu C17, ktorý realizuje nasledovnú činnosť.
Definujte všeobecnejšiu verziu funkciu z úlohy 3.5, **_int pocet_delitelnych(int n, int k)_**. Funkcia má 2
vstupné parametre, nezáporné celé číslo _n_ a kladné číslo _k_. Ošetrite situáciu, že by vstupný
argument pre parameter _n_ bolo záporné číslo alebo že by vstupný argument pre parameter _k_ bolo
záporné číslo alebo nula – vždy vypíšte príslušnú chybovú hlášku a funkcia vráti hodnotu -1. V
prípade, že sú vstupné argumenty v poriadku, funkcia načíta n čísiel a vráti počet načítaných čísiel,
ktoré boli deliteľné číslom k.

### Príklady vstupov / výstupov programu

- Volanie `pocet_delitelnych(5,2)` načíta 5 čísiel z klávesnice a vráti koľko z nich je deliteľných 2. Ak
  čísla sú napríklad 5,10,3,4,0 funkcia vráti číslo 3 (pretože 10, 4 a 0 sú deliteľné 2).
- Volanie `pocet_delitelnych(4,0)` vypíše chybovú správu, že hodnota k nie je kladná a vráti -1.
- Volanie `pocet_delitelnych(-1,2)` vypíše chybovú správu, že hodnota n je záporná a vráti -1.
- Volanie `pocet_delitelnych(-1,-2)` vypíše chybovú správu, že hodnota n je záporná a že hodnota k nie
  je kladná a vráti -1.

---

{{< details title="Rozbaľ pre ukážku riešenia" closed="true" >}}

Musím si počkať kým sa tu objaví príklad riešenia.

Nezabudni, že najviac sa naučíš ak to vypracuješ sám. 😉

{{< /details >}}
