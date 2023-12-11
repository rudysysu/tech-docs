# xargs

[TOC]

## xargs
```
find . -name *gz  | xargs gzip -dc {}
find . -name *gz  | xargs -I {} gzip  -dc {}
find . -name *gz  | xargs -I {{{ gzip  -dc {{{
```
