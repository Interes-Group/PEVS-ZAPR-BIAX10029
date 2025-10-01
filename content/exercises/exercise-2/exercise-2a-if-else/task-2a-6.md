---
date: '2025-10-01T23:16:49+02:00'
title: 'Úloha 2a.6'
weight: 6
---

Napíšte program, zdrojový kód, v jazyku C použitím štandardu C17, ktorý vypočíta účet za elektrinu používateľa
na základe zadanej spotreby. Spotreba elektriny je zadaná používateľ štandardným vstupom v abstraktných jednotkách.

Účet za elektrinu vypočítajte podľa graduálneho cenníka:

- **Prvých 50 jednotiek** je účtovaných cenou **0.5€/jednotku**.
- **Ďalších 100 jednotiek** je účtovaných cenou **0.75€/jednotku**.
- **Ďalších 100 jednotiek** je účtovaných cenou **1.20€/jednotku**.
- **Nad 250 jednotiek** je účtovaná cena **1.50€/jednotku**.

Pre finálnu sumu **sa vzťahuje daň 20%**, ktorá je pridaná k finálnej sume.

### Príklady vstupov / výstupov programu

Ak používateľ zadá spotrebu elektrickej energie **300 jednotiek** tak finálna cena po zdanení bude **354€**.

Rozpad výpočtu by bol takto:

- 50 * 0.5 = 25 (ostáva ešte 250)
- 100 * 0.75 = 75 = spolu 100 (ostáva ešte 150)
- 100 * 1.2 = 120 = spolu 220 (ostáva ešte 50)
- 50 * 1.5 = 75 = spolu 295
- 20% daň = **354€**

---

{{< details title="Rozbaľ pre ukážku riešenia" closed="true" >}}

Musím si počkať kým sa tu objaví príklad riešenia.

Nezabudni, že najviac sa naučíš ak to vypracuješ sám. 😉

{{< /details >}}
