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
#!/usr/bin/bash
code=${1:-42}
exit code
```
  
  
### Substitucija vrednosti spremenljivk
#

