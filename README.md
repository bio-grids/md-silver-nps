# Procedures

## Cleaning protein

```shell
grep -v HOH FimH.pdb > FimH_clean.pdb
```

## Creating topology

```shell
gmx pdb2gmx -f FimH_clean.pdb -o FimH_processed.gro -water spce
```