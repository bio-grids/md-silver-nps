# Procedures

## Cleaning protein

```shell
grep -v HOH FimH.pdb > FimH_clean.pdb
```

## Creating topology

```shell
gmx pdb2gmx -f FimH_clean.pdb -o FimH_processed.gro -water spce
```

## Defining the Unit Cell & Adding Solvent

```shell
gmx editconf -f FimH_processed.gro -o FimH_newbox.gro -c -d 1.0 -bt cubic

gmx solvate -cp FimH_newbox.gro -cs spc216.gro -o FimH_solv.gro -p topol.top
```

## Adding ions

```shell
gmx grompp -f ions.mdp -c FimH_solv.gro -p topol.top -o ions.tpr

gmx genion -s ions.tpr -o FimH_solv_ions.gro -p topol.top -pname AG -nname CL -neutral
```