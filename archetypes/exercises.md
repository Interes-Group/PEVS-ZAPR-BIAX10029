---
date: '{{ .Date }}'
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
type: 'exercise'
---

// TODO popis

{{< pdf "./pevs-zapr-XXX.pdf" >}}

### Náplň

- // TODO čo sú tu za cvičenia

> [!IMPORTANT]
> Ak používate ako vývojové prostredie lokálny a editor a následnú kompiláciu cez terminál. Použite príkaz:
> ```shell
> gcc -std=c17 -o program -Wall -Wextra main.c
> ```

Pre vypracovanie týchto úloh úplne postačuje použitie online kompilátora jazyku C. Napríklad
stránku [OneCompiler for C](https://onecompiler.com/c)

Riešenia na jednotlivé úlohy budú uverejnené neskôr.

## Úlohy

{{< cards cols="2" >}}
{{< card link="./task-X-X" title="Úloha X.X" subtitle="" icon="document" >}}
{{< card link="./task-X-Y" title="Úloha X.Y" subtitle="" icon="document" tag="Komplexné" tagType="info" >}}
{{< /cards >}}
