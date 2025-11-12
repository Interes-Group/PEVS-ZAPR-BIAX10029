---
date: '2025-11-13T00:02:13+01:00'
title: 'Uhádni číslo'
weight: 101
---

Úlohou je naprogramovať jednoduchú hru pomocou jazyka C, štandard C17, v ktorej sa hráč snaží uhádnuť náhodné
číslo generované hrou tzv. tajomné číslo.
Používateľ interaguje s hrou pomocou príkazového riadku / termínálu, t.j. štandardným vstupom a výstupom.

## Priebeh

Na začiatku, hra vypýta od hráča interval v ktorom vygeneruje náhodné číslo. Rozdiel hraníc intervalu musí byť minimálne

10.

Hráč následne môže napísať číslo, ktoré si myslí, že je tajomné číslo. Po zadaní čísla hra pokračuje nasledovne:

* Ak hráč zadal číslo mimo stanoveného intervalu na začiatku hry, hra vypíše hráčovi "Zadané číslo je mimo stanoveného
  intervalu",
  následne hra vypíše v akom intervale sa môže tajomné číslo nachádza a dá hráčovi možnosť hádať znovu.
* Ak hráč zadal číslo, ktoré je väčšie ako tajomné číslo, hra vypíše hráčovi “Tajomné číslo je menšie ako tvoj odhad”
  a dá hráčovi možnosť hádať znovu.
* Ak hráč zadal číslo, ktoré je menšie ako tajomné číslo, hra vypíše hráčovi “Tajomné číslo je väčšie ako tvoj odhad”
  a dá hráčovi možnosť hádať znovu.
* Ak hráč uhádol číslo, hra mu pogratuluje a skončí.

Hra končí ak hráč uhádne tajomné číslo ale sa dobrovoľne vzdá a ukončí hru tím, že napíše znak 'Q' do vstupu pre odhad.
Hra počíta koľko pokusov hráč zadal a pri ukončení hry ich vypíše hráčovi.

Ešte pred ukončením programu zapíšte záznam o hádaní do súboru _hadaj_cislo.log_. Záznam o hre má nasledujúci tvar:

**tajomné_číslo počet_pokusov uhadol/neuhadol**

Napríklad ak tajomné číslo bolo 8 a používateľ ho uhádol na 3 pokusy záznam v súbore by mal vyzerať nasledovne:
`8 3 uhadol`.

Program do súboru iba pridáva záznamy o hre nikdy nepremazáva existujúce dáta. Ak súbor neexistuje vytvorí ho.
Súbor sa môže nachádzať v rovnakom priečinku ako zdrojový súbor `main.c`.

Dbajte na dodatočnú komunikáciu/výpisy hráčovi o priebehu hry, prípadne aký vstup očakávate od hráča.

## Implementácia

Pri implementácii zadania musíte vytvoriť aspoň jednu vlastnú funkciu, ktorú následne použijete v inej časti programu.
Pri implementácii môžte použiť všetky výrazy, techniky a funkcie, ktoré sme doteraz prebrali a samozrejme aj nejaká
tvorivá
práca navyše môže byť ocenená bonusovými bodmi.

> [!TIP]
> Náhodné číslo je možné vygenerovať pomocou funkcie `rand()`, ktorá vráti náhodné číslo medzi 0 a konštantou
`RAND_MAX`.
> `rand()` je funkcia z knižnice `stdlib.h`. Pre použitie je potrebné túto knižnicu najprv zahrnúť do zdrojového kódu na
> začiatku súboru `main.c` - `#include <stdlib.h>`
>
> Ak chceme vygenerovať náhodné číslo medzi dvomi hranicami napr. medzi číslom A a číslom B tak vieme použiť vzorec:
> `rand() % (B - A + 1) + A`