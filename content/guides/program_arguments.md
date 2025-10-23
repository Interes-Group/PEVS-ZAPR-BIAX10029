---
date: '2025-10-23T12:14:12+02:00'
draft: true
title: 'Argumenty programu'
---

# Návod: Práca s argumentami programu v jazyku C

Argumenty programu umožňujú používateľovi odovzdať programu hodnoty pri jeho spustení z príkazového riadka. Táto
funkčnosť je kľúčová pre vytváranie flexibilných a interaktívnych aplikácií.

## Úvod

Argumenty programu (command-line arguments) umožňujú predať programu hodnoty pri jeho spustení z príkazového riadka. V
jazyku C sa tieto argumenty spracúvajú pomocou parametrov funkcie `main()`.

## Základná syntax

Funkcia `main()` môže mať dva parametre:

```c
int main(int argc, char *argv[])
```

**Parametre:**

- `argc` (argument count) - počet argumentov vrátane názvu programu
- `argv` (argument array) - pole pointerov na reťazce obsahujúce jednotlivé argumenty

### Alternatívne zápisy

```c
int main(int argc, char **argv)  // Ekvivalentný zápis
```

## Ako fungujú argumenty

### Indexovanie

- `argv[0]` - názov programu (cesta k spustiteľnému súboru)
- `argv[1]` - prvý argument
- `argv[2]` - druhý argument
- ...
- `argv[argc-1]` - posledný argument
- `argv[argc]` - vždy `NULL`

### Príklad spustenia

```bash
./program argument1 argument2 argument3
```

V tomto prípade:

- `argc` = 4
- `argv[0]` = `"./program"`
- `argv[1]` = `"argument1"`
- `argv[2]` = `"argument2"`
- `argv[3]` = `"argument3"`

## Základné príklady

### Príklad 1: Výpis všetkých argumentov

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    printf("Počet argumentov: %d\n", argc);

    for (int i = 0; i < argc; i++) {
        printf("argv[%d]: %s\n", i, argv[i]);
    }
    
    return 0;
}
```

**Výstup pri spustení** `./program hello world`:

```
Počet argumentov: 3
argv[0]: ./program
argv[1]: hello
argv[2]: world
```

### Príklad 2: Jednoduchá kalkulačka

```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    if (argc != 4) {
        printf("Použitie: %s <číslo1> <operátor> <číslo2>\n", argv[0]);
        printf("Operátory: +, -, *, /\n");
        return 1;
    }

    double num1 = atof(argv[1]);
    char operator = argv[2][0];
    double num2 = atof(argv[3]);
    double result;
    
    switch (operator) {
        case '+':
            result = num1 + num2;
            break;
        case '-':
            result = num1 - num2;
            break;
        case '*':
            result = num1 * num2;
            break;
        case '/':
            if (num2 == 0) {
                printf("Chyba: Delenie nulou!\n");
                return 1;
            }
            result = num1 / num2;
            break;
        default:
            printf("Neznámy operátor: %c\n", operator);
            return 1;
    }
    
    printf("%.2f %c %.2f = %.2f\n", num1, operator, num2, result);
    return 0;
}
```

**Použitie:**

```bash
./calculator 10 + 5    # Výsledok: 15.00
./calculator 20 / 4    # Výsledok: 5.00
```

### Príklad 3: Práca so súbormi

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    if (argc != 2) {
        printf("Použitie: %s <názov_súboru>\n", argv[0]);
        return 1;
    }

    FILE *file = fopen(argv[1], "r");
    if (file == NULL) {
        printf("Chyba: Nemožno otvoriť súbor '%s'\n", argv[1]);
        return 1;
    }
    
    char line[256];
    int line_number = 1;
    
    while (fgets(line, sizeof(line), file)) {
        printf("%3d: %s", line_number++, line);
    }
    
    fclose(file);
    return 0;
}
```

## Konverzia argumentov

Argumenty sú vždy reťazce (typu `char*`). Na konverziu na iné typy použite:

### Konverzia na celé číslo

```c
#include <stdlib.h>

int number = atoi(argv[1]);        // ASCII to Integer
long lnumber = atol(argv[1]);      // ASCII to Long
```

### Konverzia na desatinné číslo

```c
#include <stdlib.h>

double dnumber = atof(argv[1]);    // ASCII to Float/Double
```

### Bezpečnejšia konverzia s kontrolou chýb

```c
#include <stdlib.h>
#include <errno.h>

int main(int argc, char* argv[]){
    char *endptr;
    errno = 0;
    long number = strtol(argv[1], &endptr, 10);
    
    if (errno != 0 || *endptr != '\0') {
        printf("Chyba: '%s' nie je platné číslo\n", argv[1]);
        return 1;
    }
}
```

## Spracovanie prepínačov (flags)

### Príklad: Program s prepínačmi

```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) {
    int verbose = 0;
    int help = 0;

    // Spracovanie prepínačov
    for (int i = 1; i < argc; i++) {
        if (strcmp(argv[i], "-v") == 0 || strcmp(argv[i], "--verbose") == 0) {
            verbose = 1;
        } else if (strcmp(argv[i], "-h") == 0 || strcmp(argv[i], "--help") == 0) {
            help = 1;
        } else {
            printf("Neznámy prepínač: %s\n", argv[i]);
            return 1;
        }
    }
    
    if (help) {
        printf("Použitie: %s [PREPÍNAČE]\n", argv[0]);
        printf("  -v, --verbose    Podrobný výstup\n");
        printf("  -h, --help       Zobrazí túto nápovedu\n");
        return 0;
    }
    
    if (verbose) {
        printf("Verbose režim je zapnutý\n");
    }
    
    printf("Program beží...\n");
    return 0;
}
```

## Pokročilé techniky

### Spracovanie prepínačov s hodnotami

```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) {
    char *output_file = NULL;
    int count = 1;

    for (int i = 1; i < argc; i++) {
        if (strcmp(argv[i], "-o") == 0) {
            if (i + 1 < argc) {
                output_file = argv[++i];
            } else {
                printf("Chyba: -o vyžaduje názov súboru\n");
                return 1;
            }
        } else if (strcmp(argv[i], "-n") == 0) {
            if (i + 1 < argc) {
                count = atoi(argv[++i]);
            } else {
                printf("Chyba: -n vyžaduje číslo\n");
                return 1;
            }
        }
    }
    
    printf("Výstupný súbor: %s\n", output_file ? output_file : "stdout");
    printf("Počet iterácií: %d\n", count);
    
    return 0;
}
```

**Použitie:**

```bash
./program -o output.txt -n 10
```

## Dobre praktiká

### 1. Vždy kontrolujte počet argumentov

```c
if (argc < 2) {
    fprintf(stderr, "Chyba: Nedostatok argumentov\n");
    fprintf(stderr, "Použitie: %s <argument>\n", argv[0]);
    return 1;
}
```

### 2. Poskytujte užitočné chybové správy

```c
void print_usage(const char *program_name) {
    printf("Použitie: %s [PREPÍNAČE] <súbor>\n", program_name);
    printf("\nPrepínače:\n");
    printf("  -v, --verbose    Podrobný výstup\n");
    printf("  -h, --help       Zobrazí túto nápovedu\n");
    printf("  -o <súbor>       Výstupný súbor\n");
}
```

### 3. Validujte vstupy

```c
if (number < 0 || number > 100) {
    fprintf(stderr, "Chyba: Číslo musí byť v rozsahu 0-100\n");
    return 1;
}
```

### 4. Použite návratové kódy

```c
return 0;   // Úspech
return 1;   // Všeobecná chyba
return 2;   // Nesprávne argumenty
```

## Časté chyby a riešenia

### Chyba 1: Prístup mimo poľa

❌ **Nesprávne:**

```c
int number = atoi(argv[1]);  // Bez kontroly argc!
```

✅ **Správne:**

```c
if (argc < 2) {
    printf("Chyba: Chýba argument\n");
    return 1;
}
int number = atoi(argv[1]);
```

### Chyba 2: Neošetrenie medzier v argumentoch

Pri spustení s medzerami:

```bash
./program "hello world"  # Správne - jeden argument
./program hello world    # Dva samostatné argumenty
```

### Chyba 3: Zabudnutie na konverziu typov

```c
// ❌ Nesprávne - porovnávanie smerníkov
if (argv[1] == "hello") { ... }

// ✅ Správne - porovnávanie reťazcov
if (strcmp(argv[1], "hello") == 0) { ... }
```

## Cvičenia

### Cvičenie 1: Výpočet priemeru

Napíšte program, ktorý vypočíta priemer čísel zadaných ako argumenty.

### Cvičenie 2: Grep-like program

Vytvorte program, ktorý v súbore hľadá riadky obsahujúce zadaný reťazec.

**Použitie:** `./mygrep <vzor> <súbor>`

### Cvičenie 3: Konvertor jednotiek

Naprogramujte konvertor jednotiek s argumentmi: hodnota, jednotka_z, jednotka_na.

**Príklad:** `./convert 100 cm m` → `1.00 m`

## Zhrnutie

- Argumenty sa spracúvajú cez `argc` a `argv` v funkcii `main()`
- Všetky argumenty sú reťazce a vyžadujú konverziu
- Vždy kontrolujte počet argumentov pred ich použitím
- Používajte `strcmp()` na porovnávanie reťazcov
- Poskytujte užívateľovi jasné chybové hlásenia a nápovedu