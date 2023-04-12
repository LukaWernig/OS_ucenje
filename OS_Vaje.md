# Ukazi prvega izziva
### Prvi predelek (Osnovno delo v lupini)
#
```bash
type logout ls cd pwd date echo printf alias fi esac # Napiše tip naših ukazov, če so notranji/zunanji ukazi, če so keywordi ...
echo $PATH | tr : "\n" | nl # Izpiše vsebino $PATH-a v obliki oštevilčenega seznama
```
Prednost pri izvajanju imajo notranji ukazi, zunanji ukaz izvedemo tako, da ob izvajanju napišemo celoten `path` do njega.
```bash
man echo # To je za zunanji ukaz
help echo # To je za notranji ukaz
history # Izpiše zgodovino
echo $HISTSIZE # Izpiše max število vnosov v zgodovini 
```
Če je torej vnosov več kot `$HISTSIZE` vemo, da je v našem historyu `$HISTSIZE` vnosov.
Drugače jih je toliko, kolikor je zadnji index vnosa.
Če bi jih pa želeli prešteti ...
```bash
touch history_log.txt && history > history_log.txt && wc -l history_log.txt
```
To bo kreiralo datoteko `history_log` v katero se bo shranil output ukaza `history`.
Nato pa z `wc -l` (word count, lines) preštejemo število vrstic v našem historyu.
```bash
!3 # To uporabi/prikliče 3. ukaz v dnevinku
sleep 1000 # Končamo ga s CTRL+C, zaustavimo ga s CTRL+Z
```
  
  
### Drugi predelek (Datoteke in imeniki)
#
```bash
cd /var && echo $PWD && cd $OLDPWD # Premaknemo se v /var, izpišemo trenutni delovni direktorij in se premaknemo v prejšnji delovni direktorij
mkdir t1 t1/{t2,t3,t4} t1/t3/{t5,t6} # Ustvari shemo direktorijev prikazanih na spletni ucilnici
head -n 5 /etc/fstab # Prvih 5 vrstic datoteke /etc/fstab
tail -n /etc/group # Zadnjih 6 vrstic datoteke /etc/group
cut -d ":" -f 7 /etc/passwd # Izpiše 7 stolpec, ki je določen prek delimiterja ":", datoteke /etc/passwd
cat /etc/protocols # Navodilo malce nejasno?
sort /etc/protocols # Uredi na nek čuden način, če je to mišljeno?
cat /etc/shells | nl # Izpiše vrstice /etc/shells v obliki oštevilčenega seznama
grep "udp" /etc/services #Izpiše vse vrstice v /etc/services kjer se pojavi "udp"
wc -l /etc/passwd # Prešteje število vrstic datoteke /etc/passwd
```
  
  
### Tretji predelek (Izpis in terminal)
#
```bash
echo -e "$a\t$b\t$c" # Izpiše vrednosti spremenljivk a, b in c ločene s tabulatorjem
printf "%d\t%d\t%d" $a $b $c # Enako kot prej le, da prek printf
clear # Sprazni terminal
tty # Izpiše ime trenutnega terminala
```
Ukaz `echo -e "\033[33;1mOS \x1b[35;3mje \e[36;4mzakon."?` izpiše OS je zakon, kjer je "OS" rjav, "je" je vijoličen, "zakon." pa moder in podčrtan.
  
  
  
# Ukazi drugega izziva
### Osnovno o skriptah
#
Skripta, ki izpiše sama sebe
```bash
#!/usr/bin/cat
```
Skripta, ki izbriše sama sebe 
```bash
#!/usr/bin/rm
```
Skripta, ki zaključi program ali s prvim podanim argumentom, čigar privzeta vrednost je 42.
```bash
#!/bin/bash
code=${1:-42}
exit code
```
  
  
### Substitucija vrednosti spremenljivk
#
Naj bo dana spremenljivka `a=1:2:3:4:5`
```bash
echo ${a#*:} # Spredaj odstrani vse do prvega ":"
echo ${a##*:} # Spredaj odstrani vse do zadnjega ":"
echo ${a%:*} # Zadaj odstrani vse do prvega ":"
echo ${a%%:*} # Zadaj odstrani vse do zadnjega ":"
```
  
  
### Pogojni izrazi
#
```bash
[[ -e /etc/passwd ]] && echo "OK" # Preveri če obstaja datoteka /etc/passwd, in če izpiše OK
mkdir naloga && cd naloga && echo $PWD && cd .. # Naredi imenik naloga, skoči vanj, izpiše trenutni delovni imenik in skoči v starševski imenik.
# Če pride med delom do napake, se program ne izvede do konca
[[ $smisel = 42 ]] && echo OK || echo ERR # Če je smisel enak 42 izpiše OK, drugače ERR
```
  
  
### Zankice
#
While zanka, ki izpiše vsa soda števila od 0 do 100.
```bash
i=0
while [ $i -le 100 ]; do
if [ $(( i%2 )) -eq 0 ]; then
echo $i;
fi;
i=$(( i+1 ))
```
For zanka, ki vsem `.jpg` datotekam v trenutnem imeniku spremeni končnico na `.jpeg`.
```bash
for i in $( ls ); do
if [ ${i##*.} = jpg ]; then
mv $i "${i%.*}.jpeg";
fi;
done
```
  
  
### Ujemanje vzorcev
#
```bash
echo *[0-9] # v /proc/ izpiše pid vseh procesov
echo * # v etc izpiše vse datoteke
```
  
### Izziv za oddati
#
Studentske stevilke. Ob vnosu na standardni vhod, ki je oblike
`vpisna_st a b c`, mi na standardni vhod vrne `vpisna_st sum(a,b,c)`.

```bash
#!/bin/bash

read line;

while [[ -n $line ]]; do
    vpisna_st=${line%% *};
    stevilke=${line#* };
    sum=0;
    for i in $stevilke; do
        sum=$(( sum+i ));
    done
    
    echo $vpisna_st $sum;
    read line;
done
exit 42

```

# Ukazi tretjega izziva



