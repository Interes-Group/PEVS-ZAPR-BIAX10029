---
date: '2025-11-13T00:01:53+01:00'
title: 'Kalkulačka'
---

Vytvorte program v jazyku C v štandarde C17, ktorý bude slúžiť ako jednoduchá kalkulačka.

Program po svojom spustení vypíše používateľovi ponuku funkcií, ktoré ponúka a čaká na voľbu používateľa.
Ku každej ponúkanej funkcii je priradené poradové číslo. Keď používateľ zadá poradové číslo funkcie, spustí zvolenú
funkciu v rámci programu.
Každá funkcia sa vypýta od používateľa požadované vstupy aby vedela vykonať svoju logiku.
Program má poskytovať nasledovné funkcie:

- súčet dvoch čísel
- rozdiel dvoch čísel
- násobok dvoch čísel
- podiel dvoch čísel
- faktoriál čísla

Ponuka funkcií programu môže vyzerať nasledovne:

```text
1 Súčet
2 Rozdiel
3 Násobok
4 Podiel
5 Faktoriál
```

Ponuka je používateľovi vypísaná vždy keď za vykonanie zvolenej funkcií skončí, t.j. program beží v cykle:
_ponuka -> voľba funkcie -> spustenie funkcie -> ponuka_

Ak používateľ v ponuke namiesto čísla zadá písmeno '_q_' program skončí.
Dbajte na dodržanie prebratých praktík a programovacích techník pri implementácii. Snažte sa používateľa vhodne
informovať o priebehu programu,
či o potrebných vstupoch pre jednotlivých funkciách.

### Súčet

Po voľbe funkcie súčet program od používateľa vypýta na štandardnom vstupe dve čísla. Po zadaní druhého čísla program
vypíše výsledok
súčtu zadaných dvoch čísel.

### Rozdiel

Po voľbe funkcie rozdiel program od používateľa vypýta na štandardnom vstupe dve čísla. Po zadaní druhého čísla program
vypíše výsledok
rozdielu prvého čísla od druhého.

### Násobok

Po voľbe funkcie násobok program od používateľa vypýta na štandardnom vstupe dve čísla. Po zadaní druhého čísla program
vypíše výsledok
násobenia zadaných dvoch čísel.

### Podiel

Po voľbe funkcie podiel program od používateľa vypýta na štandardnom vstupe dve čísla. Po zadaní druhého čísla program
vypíše výsledok
podielu prvého čísla druhým číslom.

### Faktoriál

Po voľbe funkcie faktoriál program od používateľa vypýta na štandardnom vstupe číslo. Po zadaní čísla program vypíše
výsledok
výpočtu faktoriálu zadaného čísla.

## Vypracovanie

Pre vypracovanie tohto projektu môžte použiť ľubovolné vývojové prostredie, ktoré podporuje programovanie v jazyku C
štandardom C11.
Môžte napríklad použiť IDE:

- [CLion](https://www.jetbrains.com/clion/)
- [VS Code](https://code.visualstudio.com/) (s
  [rozšírením pre C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools))
- online kompilátor [OneCompiler for C](https://onecompiler.com/c)

> [!IMPORTANT]
> Ak používate ako vývojové prostredie lokálny a editor a následnú kompiláciu cez terminál. Použite príkaz:
> ```shell
> gcc -std=c17 -o program -Wall -Wextra main.c
> ```

Program môže byť implementovaný ako jeden súbor. Pre implementáciu nie je potrebná žiadna externá knižnica, len
štandardné funkcie poskytovanie jazykom C ako `<stdio.h>` a `<stdlib.h>`.


