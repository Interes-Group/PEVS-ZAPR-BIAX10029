---
date: '2025-10-23T14:13:25+02:00'
title: 'Práca s prepínačami programu pomocou getopt()'
---

Funkcia `getopt()` a jej rozšírená verzia `getopt_long()` umožňujú jednoduché a štandardizované spracovanie argumentov
príkazového riadku v jazyku C. Tieto funkcie sú súčasťou POSIX štandardu a sú dostupné na Unix/Linux systémoch.

## Základy: `getopt()`

### Čo je getopt?

`getopt()` je funkcia na spracovanie **krátkych prepínačov** (napr. `-h`, `-v`, `-o file.txt`). Automaticky kontroluje:

- Či prepínač existuje
- Či prepínač vyžaduje argument
- Či sú všetky argumenty správne

### Syntax

```c
#include <unistd.h>

int getopt(int argc, char *const argv[], const char *optstring);

```

**Globálne premenné:**

- `optarg` - ukazovateľ na argument aktuálneho prepínača
- `optind` - index ďalšieho argumentu v `argv[]`
- `optopt` - neznámy prepínač (pri chybe)
- `opterr` - ak je 0, vypne automatické chybové hlášky

### Formát optstring

Reťazec definuje povolené prepínače:

```c
"hvo:n:"
```

- `h` - prepínač `-h` bez argumentu
- `v` - prepínač `-v` bez argumentu
- `o:` - prepínač `-o` **s povinným** argumentom
- `n:` - prepínač `-n` **s povinným** argumentom

**Pravidlá:**

- Písmeno bez `:` = prepínač bez argumentu
- Písmeno s `:` = prepínač s povinným argumentom
- Písmeno s `::` = prepínač s voliteľným argumentom (GNU rozšírenie)

## Príklad 1: Základné použitie getopt()

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    int opt;
    int verbose = 0;
    char *output_file = NULL;

    // Spracovanie argumentov
    while ((opt = getopt(argc, argv, "hvo:")) != -1) {
        switch (opt) {
            case 'h':
                printf("Použitie: %s [-h] [-v] [-o súbor]\n", argv[0]);
                printf("  -h        Zobrazí nápovedu\n");
                printf("  -v        Verbose režim\n");
                printf("  -o súbor  Výstupný súbor\n");
                return 0;
                
            case 'v':
                verbose = 1;
                printf("Verbose režim zapnutý\n");
                break;
                
            case 'o':
                output_file = optarg;
                printf("Výstupný súbor: %s\n", output_file);
                break;
                
            case '?':
                // Neznámy prepínač alebo chýbajúci argument
                fprintf(stderr, "Neznámy prepínač alebo chýbajúci argument\n");
                fprintf(stderr, "Použite -h pre nápovedu\n");
                return 1;
                
            default:
                return 1;
        }
    }
    
    // Spracovanie zvyšných argumentov (nie prepínače)
    for (int i = optind; i < argc; i++) {
        printf("Argument: %s\n", argv[i]);
    }
    
    return 0;
}
```

**Príklady spustenia:**

```bash
./program -h
./program -v
./program -o output.txt
./program -v -o output.txt argument1 argument2
./program -vo output.txt # Skrátený zápis
```

## Príklad 2: Program s viacerými prepínačmi

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(int argc, char *argv[]) {
    int opt;
    int verbose = 0;
    int count = 1;
    char *input_file = NULL;
    char *output_file = NULL;

    while ((opt = getopt(argc, argv, "vn:i:o:h")) != -1) {
        switch (opt) {
            case 'v':
                verbose = 1;
                break;
                
            case 'n':
                count = atoi(optarg);
                if (count <= 0) {
                    fprintf(stderr, "Chyba: -n musí byť kladné číslo\n");
                    return 1;
                }
                break;
                
            case 'i':
                input_file = optarg;
                break;
                
            case 'o':
                output_file = optarg;
                break;
                
            case 'h':
                printf("Použitie: %s [PREPÍNAČE]\n", argv[0]);
                printf("  -v          Verbose režim\n");
                printf("  -n POČET    Počet iterácií\n");
                printf("  -i SÚBOR    Vstupný súbor\n");
                printf("  -o SÚBOR    Výstupný súbor\n");
                printf("  -h          Nápoveda\n");
                return 0;
                
            case '?':
                return 1;
                
            default:
                return 1;
        }
    }
    
    // Validácia
    if (input_file == NULL) {
        fprintf(stderr, "Chyba: Vstupný súbor je povinný (-i)\n");
        return 1;
    }
    
    // Spracovanie
    if (verbose) {
        printf("Vstup: %s\n", input_file);
        printf("Výstup: %s\n", output_file ? output_file : "stdout");
        printf("Počet: %d\n", count);
    }
    
    printf("Program beží...\n");
    
    return 0;
}
```

**Spustenie:**

```bash
./program -i input.txt -o output.txt -n 5 -v
./program -vi input.txt -n 10 # Kombinované prepínače
```

## Rozšírené: `getopt_long()`

### Čo je getopt_long?

`getopt_long()` podporuje **dlhé prepínače** (napr. `--help`, `--verbose`, `--output file.txt`) aj krátke.

### Syntax

```c
#include <getopt.h>

int getopt_long(int argc, char *const argv[],
const char *optstring,
const struct option *longopts,
int *longindex);
```

### Štruktúra option

```c
struct option {
    const char *name; // Názov dlhého prepínača (bez --)
    int has_arg; // no_argument, required_argument, optional_argument
    int *flag; // Ak NULL, getopt_long vracia 'val'
    int val; // Hodnota na vrátenie (zvyčajne krátky prepínač)
};
```

**Hodnoty pre has_arg:**

- `no_argument` (0) - prepínač bez argumentu
- `required_argument` (1) - prepínač s povinným argumentom
- `optional_argument` (2) - prepínač s voliteľným argumentom

## Príklad 3: Kompletný príklad s getopt_long()

```c
#include <stdio.h>
#include <stdlib.h>
#include <getopt.h>

int main(int argc, char *argv[]) {
    int opt;
    int verbose = 0;
    int help = 0;
    char *output_file = NULL;
    int count = 1;

    // Definícia dlhých prepínačov
    static struct option long_options[] = {
        {"help",     no_argument,       0, 'h'},
        {"verbose",  no_argument,       0, 'v'},
        {"output",   required_argument, 0, 'o'},
        {"count",    required_argument, 0, 'n'},
        {"version",  no_argument,       0, 'V'},
        {0, 0, 0, 0}  // Ukončovací prvok
    };
    
    int option_index = 0;
    
    // Spracovanie argumentov
    while ((opt = getopt_long(argc, argv, "hvo:n:V",
                              long_options, &option_index)) != -1) {
        switch (opt) {
            case 'h':
                printf("Použitie: %s [PREPÍNAČE]\n\n", argv[0]);
                printf("Krátke prepínače:\n");
                printf("  -h          Zobrazí nápovedu\n");
                printf("  -v          Verbose režim\n");
                printf("  -o SÚBOR    Výstupný súbor\n");
                printf("  -n POČET    Počet iterácií\n");
                printf("  -V          Verzia programu\n\n");
                printf("Dlhé prepínače:\n");
                printf("  --help\n");
                printf("  --verbose\n");
                printf("  --output SÚBOR\n");
                printf("  --count POČET\n");
                printf("  --version\n");
                return 0;
                
            case 'v':
                verbose = 1;
                printf("Verbose režim zapnutý\n");
                break;
                
            case 'o':
                output_file = optarg;
                if (verbose) {
                    printf("Výstupný súbor: %s\n", output_file);
                }
                break;
                
            case 'n':
                count = atoi(optarg);
                if (count <= 0) {
                    fprintf(stderr, "Chyba: počet musí byť kladné číslo\n");
                    return 1;
                }
                if (verbose) {
                    printf("Počet iterácií: %d\n", count);
                }
                break;
                
            case 'V':
                printf("Program verzia 1.0.0\n");
                return 0;
                
            case '?':
                fprintf(stderr, "Použite --help pre nápovedu\n");
                return 1;
                
            default:
                return 1;
        }
    }
    
    // Spracovanie zvyšných argumentov
    if (optind < argc) {
        printf("Zvyšné argumenty: ");
        while (optind < argc) {
            printf("%s ", argv[optind++]);
        }
        printf("\n");
    }
    
    printf("Program dokončený.\n");
    return 0;
}
```

**Príklady spustenia:**

```bash
./program --help
./program -v --output result.txt
./program --verbose --count 10 --output data.txt
./program -vo result.txt -n 5 # Mix krátkych a dlhých
./program --version
```

## Pokročilé techniky

### 1. Vypnutie automatických chybových hlášok

```c
opterr = 0; // Vypne automatické chybové hlášky

while ((opt = getopt(argc, argv, "hvo:")) != -1) {
    if (opt == '?') {
        fprintf(stderr, "Vlastná chybová hláška pre '%c'\n", optopt);
    }
}
```

### 2. Reset getopt pre opätovné použitie

```c
optind = 1; // Reset na začiatok argv
```

### 3. Voliteľné argumenty (GNU rozšírenie)

```c
while ((opt = getopt(argc, argv, "o::")) != -1) {
    switch (opt) {
        case 'o':
            if (optarg) {
                printf("Výstup: %s\n", optarg);
            } else {
                printf("Výstup: default.txt\n");
            }
        break;
    }
}
```

**Použitie:**

```bash
./program -o # optarg je NULL
./program -ofile.txt # Bez medzery!
```

## Časté chyby a riešenia

### ❌ Chyba 1: Zabudnutie na dvojbodku

```c
getopt(argc, argv, "o")  // CHYBA: -o nebude akceptovať argument
```

✅ **Správne:**

```c
getopt(argc, argv, "o:")  // -o vyžaduje argument
```

### ❌ Chyba 2: Nekontrolovanie povinných argumentov

```c
char *output = optarg; // Môže byť NULL!
```

✅ **Správne:**

```c
if (output == NULL) {
    fprintf(stderr, "Chyba: Výstupný súbor je povinný\n");
    return 1;
}
```

### ❌ Chyba 3: Neukončenie option poľa

```c
static struct option long_options[] = {
    {"help", no_argument, 0, 'h'}
    // CHYBA: Chýba ukončovací prvok!
};
```

✅ **Správne:**

```c
static struct option long_options[] = {
    {"help", no_argument, 0, 'h'},
    {0, 0, 0, 0} // Ukončovací prvok
};
```

## Kompatibilita

- **getopt()**: POSIX štandard, funguje na všetkých Unix/Linux systémoch
- **getopt_long()**: GNU rozšírenie, funguje na Linux, macOS, ale **NIE** na čistom Windows
- **Windows alternatíva**: Použite vlastnú implementáciu alebo knižnicu ako `getopt-win32`

## Zhrnutie

| Vlastnosť        | getopt()     | getopt_long() |
|------------------|--------------|---------------|
| Krátke prepínače | ✓            | ✓             |
| Dlhé prepínače   | ✗            | ✓             |
| Jednoduchosť     | Jednoduchšie | Komplexnejšie |
| Štandard         | POSIX        | GNU           |

**Odporúčanie:**

- Pre jednoduché programy: použite `getopt()`
- Pre profesionálne CLI nástroje: použite `getopt_long()`
- Pre študentské projekty: `getopt_long()` je dobrá voľba

## Ďalšie zdroje

- `man 3 getopt` - manuálová stránka
- `man 3 getopt_long` - rozšírená verzia
- [GNU libc dokumentácia](https://www.man7.org/linux/man-pages/man3/getopt.3.html)