---
title: "Shell Script alapok"
date: 2022-04-17T11:46:59+02:00
draft: false
tags: [ "Konfiguráció" ]
image: images/bash-logo.jpg
---
A Shell script egy olyan programozási nyelv, ami arra lett tervezve, hogy Unix alapú rendszerek futtassák. A használata egyszerű és gyorsan megírható. Emellett ez egy scripting language, ez azt takarja, hogy a megalkotásánál az volt a cél, hogy más programokkal kompatibilis legyen. Ez később szemléltetve is lesz.
<!--more-->
## Felépítése
Minden shell script kódra jellemző, hogy ugyan úgy kezdődnek. Az első sor mindig az kódot futtató program megadása, így a rendszer tudni fogja, hogy melyik programmal kell futtatnia. Ez a következő módon néz ki:

```bash
#!/bin/bash
```
Ez után kezdődik maga a kód megírása. Itt a megszokott programozási nyelvektől eltérően soha nem történik modul importálása (lásd, python: `import time`), mivel itt modulok helyett Unix alapú rendszerek által futtatható programokat használ a kód. A shell scritpt kódok `.sh` végződésűek. Fontos viszont, hogy a kód futtatása előtt jogot kell neki adni erre. Ez a `chmod +x elso_program.sh`.

## Változók deklarálása
Itt a változók deklarálása egyszerűen történik. Először a már említett módon az első sorba a program megadása kerül, amivel futtatni fogja a rendszer.

Egy hello world programban először deklarálni kell a változót: `változó neve=változó értéke`, fontos, hogy a változó neve ne használjon ékezetes karaktereket illetve helykihagyást. Következő a változó kiíratása. Ezt `echo` parancsal történik: `echo $változó neve`. Az echo az utána következő argumentumok kiírásáért felel. Ha a változónak nem értéket adunk, hanem az értékét kérjük le, akkor mindig rakunk egy `$`-et a változó neve elé ügyelve arra, hogy ne legyen közte szóköz.

```bash
#!/bin/bash
VAR="Hello World"
echo $VAR
```
Mivel ez egy scripting language így a változók deklarálása nincs túlbonyolítva. Erre jó példa a következő kódrészlet:

```bash
string="Hello World"
number=1
float=3.142
mixed=abc123
```

## Nem előre deklarált változók
### Read
A `read` parancs lehetővé teszi, hogy változóknak bemeneti értéket adjunk meg értékként. Erre egy jó példa:

```bash
echo "Mi a neved?"
read nev
echo "Helló $nev"
```

Itt a program kiírja, hogy `Mi a neved?`, majd beolvassa a `nev` változó értékét, ez után az `echo` parancs segítségével pedig kiírja.

## Argumentumok
Argumentumokkal már találkozhattunk. Ezek a parancs után találhatóak általában egy kötőjellel kezdődnek(pl: *irssi -n <username>*). Viszont a shell scriptingben nem kell kötőjellel megadni, hogy az argumentum miért felel.

Az argumentumok számozva vannak és a számozás 0-tól indul. A 0. argumnetum mindig a fájlnév és utánna következnek a váltzók.

```bash
script.sh arg1 arg2 arg3
```
Ezekre az argumentumokra $-el lehet hivatkozni. $, majd pedig az argumentum száma.

```bash
#!/bin/bash
echo "Fájlnév $0"
echo "1. argumentum $1"
echo "2. argumentum $2"
```
Ezt a programot miután elmentjük a következő képpen kell haználni:

```bash
./args.sh elso masodik
```
Ez vissza fogja adni nekünk az fájlnév után következő első illetve második argumentumot.

## Array vagyis tömb használata
Egy változó egyszerre 1 értéket tárolhat. Ezzel szemben egy array többet is tud, ez azt jelenti, hogy új változók létrehozása helyett a már meglévő tömbhöz kell hozzáadnunk még 1 elemet. Az elemekre index számmal tudunk hivatkozni, a legelső index szám a 0. Az array használatára jó példa egy névsor létrehozása.

``` bash
NAME01="Attila"
NAME02="Béla"
NAME03="Károly"
```
A változók egyenkénti ledekralásáa helyett ezeket egy tömbbe rendeljük. Így elég a név index számát tudnunk és nemkell egy új változóra hivatkoznunk.

```bash
NAME[0]="Attila"
NAME[1]="Béla"
NAME[2]="Károly"
```
Így elérjük azt, hogy sok változó helyett egy tömbben gyűjtjük össze a neveket és ha komplexabb programot írunk, akkor sokkal egyszerűbb dolgunk lesz. Az arrayre való hivatkozásra egy egyszerű példa:

```bash
#!/bin/sh
NAME[0]="Attila"
NAME[1]="Béla"
NAME[2]="Károly"
echo "Első Index: ${NAME[0]}"
echo "Második Index: ${NAME[1]}"
echo "harmadik Index: ${NAME[2]}"
```
Itt a `NAME` tömbnek megadjuk az első 3 értékét, majd kiíratjuk. A tömbre való hivatkozáskor `${ }` közé rakjuk az array nevét, majd `[]` közé az indexét az elemnek, amire hivatkozni akarunk.

## If használata
At if statement egy feltételből és egy állításból áll. Erre egy egyszerű példa:

```bash
if 5 -gt 4
then
    echo “5 nagyobb mint 4”
fi
```
Itt felmerülhet a kérdés, hogy mit jelent a `-gt`, ez a nagyobb mintnek felel meg, shell scriptben az operátorok mid hasonló képpen kell megadni. Ezek magyarázata:

```bash
-eq: equal to = egyenlő vele
-ne: not equal to = nem egyenlő vele
-lt: less than = kisebb mint
-le: less than or equal to = kisebb mint vagy egyenlő
-gt: greater than = nagyobb mint
-ge: greater than or equal to = nagyobb mint vagy egyenlő
```
Ez számokra vonatkozik, viszont fájlokkal is vannak operátorok. Ekek közül a fontosabbak:

```bash
-e	a fájl létezik és
-d	a fájl létezik és egy mappa
-f	a fájl létezik és egy fájl
-r	a fájl létezik és olvasható
-w	a fájl létezik és írható
-x	a fájl létezik és futtatható
-s	a fájl létezik és a mérete nagyobb mint 0
```
Ezeket hasonló módon kell használni mint az előző példában.

```bash
if [ -e ".bash_profile" ]
then
    echo " The file exists "
else
    echo " File not found "
fi
```
## While loop
A while loop addig futtatja a tartalmát újra és újra, amég az állítása igaz. Ezt legtöbbször egy boolean változóval teszik, viszont egy változó értékének ellenörzését is szokták while loop állításába tenni, viszont erre legtöbb esetben a for loop sokkal előnyösebb. A while loopra egy példa:

```bash
n=1
while [ $n -le 3 ]
do
    echo "$n alkalommal lefutott"
    n=$(( n+1 ))
done
```
## For loop
A for loop hasonlít a while loopra, viszont ez arra lett kitalálva, hogy értéket növeljen és úgy hajtson végre utasításokat.
A for loopra egy jó példa:

```bash
for num in {1..10}
do
    echo "$num"
done
```
Ez a ciklus minden alkalommal lefut, amíg a num változó nem éri el a 10 értéket. A num változó alapértéke 1 és minden lefutás során az értéke növekszik 1-el. Ez megoldható, hogy ne 1-et lépjen ciklusonként, hanem példáúl 10-et.

```bash
for num in {0..100..10}
do
    echo "$num"
done
```
Ez hasonló képpen fog lefutni mint az előző példa, viszont ezesetben 1-től 100-ig 10-esével növeki a num változó értékét. A for loopot lehet több féle képpen is hasznánli, viszont van egy mód, amit más nyelvekben is előszeretettel használnak az átláthatósága miatt.

```bash
for (( i=1; i -et 10; i++))
do
    echo "$i"
done
```
## Összefoglaló
A shell script nagyon hasznos tud leni, ha unix alapú rendszeren akarunk gyorsan kódot írni valamire és nem akarunk törődni modulok importálásával és összetett szintaktikák alkalmázásával. Bármely linux felhasználónak jól jöhet néha egy minimális shell script tudás, mivel ezzel folgyorsíthatjuk a munkánkat és kényelmesebbé tehetjük, hosszú távon nagyon kifizetődő.Hosszú, gyakran használt parancsokat ha nem akarunk minden alkalommal begépelni, mikor szükségünk van rá, akkor a legjobb megoldás ezeket egy shell script fájlba beleírni és ezt a fájlt futtathatóvá tenni.
