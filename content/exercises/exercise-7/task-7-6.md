---
date: '2025-11-12T23:19:15+01:00'
title: 'Úloha 7.6'
weight: 6
---

Majme nasledujúci program:

```C
void runMe(){
    int* leakingPtr = (int*) malloc(sizeof(int) * 1024);
    for(int i=0; i < 1024; i++){
        leakingPtr[i] = i + 1000;
    }
}

int main(){
    runMe();
    return 0;
}
```

1. Ako vyzerá alokovaná pamäť program pred a po volaní funkcie `runMe`?
2. Čo je zlé s funkciou `runMe`? (minimálne 2 veci)
3. Prepíšte program tak aby bol korektný.

---

{{< details title="Rozbaľ pre ukážku riešenia" closed="true" >}}

Musím si počkať kým sa tu objaví príklad riešenia.

Nezabudni, že najviac sa naučíš ak to vypracuješ sám. 😉

{{< /details >}}
