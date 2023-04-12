# Skripte
### Velikost slikovnih datotek
#

![velikost](velikost.png)

Skripta izpiše skupek prostora, ki ga porabijo slikovne datoteke.

```bash
#!/bin/bash

dir=$1 # V navodilu piše, da je prvi argument imenik v katerem bomo preštevali velikosti

jpg=0;png=0;gif=0; # Inicializiram spremenljivke, kjer bom shranjeval koliko prostora zapravljajo datoteke

for i in $(ls $dir); do # Loopam po seznamu datotek, ki sem jih dobil prek ukaza "ls" z argumentom "$dir" v podlupini

    size=$(stat -c %s "$dir/$i") # Z ukazom podanim v navodilu dobim velikost trenutne datoteke, ki jo gledam

    type=${i##*.} # Uporabim nekaj s ppt-ja "Skriptiranje", da odstranim vse znake do prve pojavitve "."

    case $type in # Switch, kjer mi odvisno od končnice ali prišteje k velikostim, ali pa ne naredi ničesar če ni nič od naštetega

        "jpg") jpg=$(( jpg + size )) ;; 
        "png") png=$(( png + size )) ;;
        "gif") gif=$(( gif + size )) ;;
        *) ;;
    esac;
done
 # Če ne zapravi nič prostora, reči ne bom izpisal, ker je tako prikazano tudi na papirju

    [ $jpg -ne 0 ] && echo "jpg" $jpg 
    [ $png -ne 0 ] && echo "png" $png
    [ $gif -ne 0 ] && echo "gif" $gif

exit 0;

# /home/lukawernig/Pictures/Wallpapers, path na katerem sem stestiral in je delovalo pravilno

```