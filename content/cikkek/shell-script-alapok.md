---
title: "Shell Script alapok"
date: 2022-04-17T11:46:59+02:00
draft: false
tags: [ "Konfiguráció" ]
image: images/bash-logo.jpg
---
A Shell script egy olyan programozási nyelv, ami arra lett tervezve, hogy Unix alapú rendszerek futtassák. A használata egyszerű és gyorsan megírható. Emellett ez egy scripting language, ez azt takarja, hogy nincs szükségünk külön fordítóra. A megalkotásánál az volt a cél, hogy más, Unix programokkal kompatibilis legyen. Ez később szemléltetve is lesz.
<!--more-->
## Felépítése
Minden shell script kódra jellemző, hogy ugyan úgy kezdődnek. Az első sor mindig az kódot futtató program megadása, így a rendszer tudni fogja, hogy melyik programmal kell futtatnia. Ez a következő módon néz ki:

```bash
#!/bin/bash
```
Ez után kezdődik maga a kód megírása. Itt a megszokott programozási nyelvektől eltérően soha nem történik modul importálása (lásd, python: `import time`), mivel itt modulok helyett Unix alapú rendszerek által futtatható programokat használ a kód. A shell script kódok `.sh` végződésűek. Fontos viszont, hogy a kód futtatása előtt jogot kell neki adni erre:

```bash
chmod +x elso_program.sh
```

## Változók deklarálása
Itt a változók deklarálása egyszerűen történik. Először a már említett módon az első sorba a program megadása kerül, amivel futtatni fogja a rendszer.

Egy hello world programban először deklarálni kell a változót: `VALTOZO_NEVE=valtozo_erteke`, fontos, hogy a változó neve ne használjon ékezetes karaktereket illetve helykihagyást. Következő a változó kiíratása. Ezt `echo` paranccsal történik: `echo $változó neve`. Az echo az utána következő argumentumok kiírásáért felel. Ha a változónak nem értéket adunk, hanem az értékét kérjük le, akkor mindig rakunk egy `$`-et a változó neve elé ügyelve arra, hogy ne legyen közte szóköz.

```bash
#!/bin/bash
VAR="Hello World"
echo $VAR
```
Mivel ez egy scripting language így a változók deklarálása nincs túlbonyolítva, nem szükséges a típus megadása. Erre jó példa a következő kódrészlet:

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
Argumentumokkal már találkozhattunk. Ezek a parancs után találhatóak általában egy kötőjellel kezdődnek(például: *irssi -n <username>*). Viszont a shell scriptingben nem kell kötőjellel megadni, hogy az argumentum miért felel.

Az argumentumok számozva vannak és a számozás 0-tól indul. A 0. argumentum mindig a fájlnév és utána következnek a változók.

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
Ezt a programot miután elmentjük a következő képpen kell használni:

```bash
./args.sh elso masodik
```
Ez vissza fogja adni nekünk az fájlnév után következő első illetve második argumentumot.


# If használata
At if statement egy feltételből és egy állításból áll. Erre egy egyszerű példa:

```bash
if 5 -gt 4
then
    echo “5 nagyobb mint 4”
fi
```
Itt felmerülhet a kérdés, hogy mit jelent a `-gt`, ez a "nagyobb mint"-nek felel meg, shell scriptben az operátorok mid hasonló képpen kell megadni. Ezek magyarázata:

```bash
-eq: equal to = egyenlő vele, ==
-ne: not equal to = nem egyenlő vele, !=
-lt: less than = kisebb mint, <
-le: less than or equal to = kisebb mint vagy egyenlő, <=
-gt: greater than = nagyobb mint, >
-ge: greater than or equal to = nagyobb mint vagy egyenlő, >=
```
Ez számokra vonatkozik, viszont fájlokkal is vannak operátorok. Ezek közül a fontosabbak:

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
A while loop addig futtatja a tartalmát újra és újra, amíg az állítása igaz. Ezt legtöbbször egy boolean változóval teszik, viszont egy változó értékének ellenőrzését is szokták while loop állításba tenni, viszont erre legtöbb esetben a for loop sokkal előnyösebb. A while loopra egy példa:

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
Ez a ciklus minden alkalommal lefut, amíg a num változó nem éri el a 10 értéket. A num változó alapértéke 1 és minden lefutás során az értéke növekszik 1-el. Ez megoldható, hogy ne 1-et lépjen ciklusonként, hanem például 10-et.

```bash
for num in {0..100..10}
do
    echo "$num"
done
```
Ez hasonló képpen fog lefutni mint az előző példa, viszont ez esetben 1-től 100-ig 10-esével növeli a num változó értékét. A for loopot lehet többféle képpen is használni, viszont van egy mód, amit más nyelvekben is előszeretettel használnak az átláthatósága miatt.

```bash
for (( i=1; i -et 10; i++))
do
    echo "$i"
done
```

## Tömbök használata
Ez idáig véges számú változókat deklaráltunk az értékeink tárolására. Mi történik abban az esetben, ha nekünk ennél többre van szükségünk? Tételezzük fel, hogy a felhasználótól 20 értéket kérünk be. Ehhez 20 változót kellene deklarálnunk? Korántsem. A tömbök használatával dinamikusan tárolhatjuk értékeinket anélkül, hogy minden egyes értékhez egy új változót hoznánk létre. Első lépésben hozzunk létre egy új tömböt.

```bash
declare -a SZAM;
declare -A NAME;
```

A `declare` kulcsszó létrehozza a tömböt, melyet az `-a` és `-A` kapcsolókkal láthatunk el. Az `-a` kapcsoló egy index-alapú tömböt hoz létre. A tömb első elemének indexe minden esetben `0` és elemenként 1-el növekszik. A tömb `-1` indexe mindig az utolsó elemet adja vissza. 

Ezzel ellentétben az `-A` kapcsoló egy asszociatív tömböt hoz létre, ahol a tömbelemek kulcsszavak alapján kerülnek indexelésre:

```bash
declare -a SZAM;
SZAM=(1 2 3 4 5 6)
#általános alak: TÖMB[index]=érték
SZAM[0]=1
SZAM[1]=2
SZAM[2]=3
SZAM[3]=4
SZAM[4]=5
SZAM[5]=6

declare -A NAME;
#általános alak: TÖMB[kulcs]=érték
NAME[manager]=Attila
NAME[dev]=Béla
NAME[devOps]=Károly
NAME[finOps]="Gipsz Jakab"
```

Az előbb említett asszociatív tömböt alternatív módon is létrehozhatjuk, egy sorban:

```bash
#általános alak: TÖMB=([kulcs1]=érték1 [kulcs2]=érték2...)
declare -A NAME
NAME=([manager]=Attila [dev]=Béla [devOps]=Károly [finOps]="Gipsz Jakab")

#vagy
NAME=(
    [manager]=Attila 
    [dev]=Béla 
    [devOps]=Károly 
    [finOps]="Gipsz Jakab"
)
```

Fontos észrevennünk, hogy ha a tömbelemeket egy kifejezésként szeretnénk definiálni (egysoros definíció), akkor szóközökkel kell elválasztanunk őket egymástól. Ha tömbben olyan elemünk van, amely szóközöket tartalmaz, akkor idézőjelek használatával tehetjük egyértelművé, hogy az érték egy elemet alkot. 

### Hozzáférés a tömbelemekhez

Amennyiben a tömböt szimplán megpróbáljuk kiíratni, akkor mindig az első tömbelemet kapjuk:

```bash
SZAM=(1 2 3 4 5 6)
echo $SZAM
1
```

A tömbelemeket a "bash expansion" szintaktikával érhetjük el explicit módon:

```bash
SZAM=(1 2 3 4 5 6)
echo ${SZAM[0]}
1

echo ${SZAM[2]}
3

echo ${SZAM[-1]}
6

echo ${SZAM[1+1]}
3
```

Mint láthatjuk, a tömbelem hivatkozás lehet akár egy kifejezés is, a szabály mindösszesen annyi a szabály, hogy kifejezésnek számra kell kiértékelődnie.

Az összes tömbelemet az alábbi módokon tudjuk kiíratni:

```bash
SZAM=(1 2 3 4 5 6)
echo ${SZAM[*]}
1 2 3 4 5 6

echo ${SZAM[@]}
1 2 3 4 5 6
```

Látszólag a két parancs egyenértékű, de a kettő között különbség van. Az `*` operátor a tömbelemet egy argumentumként írja ki, a `@` viszont külön argumentumonként írja ki az elemeket. A tömböt egy `for` looppal történő bejárás után a különbség nyilvánvalóvá válik:

```bash
for i in "${SZAM[*]}";do
    echo "$i"
done
1 2 3 4 5 6

for i in "${SZAM[@]}";do
    echo "$i"
done
1
2
3
4
5
6
```

A tömbelemek számát az alábbi módon írhatjuk ki:


```bash
echo ${#SZAM[@]}
6

#vagy
echo ${#SZAM[*]}
6
```

Asszociatív tömb kulcsainak a listázása:

```bash
echo ${!NAME[@]}
#vagy
echo ${!NAME[*]}
finOps dev manager devOps
```

### Tömbelemek hozzáadása és törlése

Indexelt tömbökben a törlés index alapján történik. Asszociatív tömbelemeket kulcs alapját törölhetünk:

```bash
declare -A NAME
NAME=([manager]=Attila [dev]=Béla [devOps]=Károly [finOps]="Gipsz Jakab")


unset NAME[manager]
echo ${NAME[@]}
Gipsz Jakab Béla Károly
```

Új asszociatív tömbelem hozzáadása:

```bash
NAME=([manager]=Attila [dev]=Béla [devOps]=Károly [finOps]="Gipsz Jakab")

NAME[cleaner]=Mária

NAME+=([scrumMaster]=Ivó)

echo ${NAME[@]}
Gipsz Jakab Béla Attila Ivó Károly Mária
```

Mivel az értékeket kulcs határozza meg, ezért az asszociatív tömb nem rendezett. Az új érték bárhová kerülhet. Ha fontos számunkra a rendezett sorozat (és amennyiben a feladat megengedi), használjunk indexelt tömböt. 


Új tömbelem beszúrása indexelt tömbökbe:


```bash
declare -a SZAM;
SZAM=(1 2 3 4 5 6)
```


Ha már egy létező index helyére hivatkozunk, akkor az elem felülíródik:

```bash
SZAM[3]=NaN

echo ${SZAM[@]}
1 2 3 NaN 5 6
```

A tömb végére pedig az alábbiképpen szórhatunk be egy új elemet:

```bash
SZAM+=Undefined

echo ${SZAM[@]}
1 2 3 NaN 5 6 Undefined
```

Kiírathatjuk a lista részét is, melynek általános alakja `${TOMB[@]:kezdo:elem}`. A visszatérési érték a tömbelem `kezdo` indexétől számított `elem` indexen át tartó altömb lesz.


```bash
echo ${SZAM[@]:3:1}
NaN

echo ${SZAM[@]:3:3}
NaN 5 6 

echo ${SZAM[@]:1:5}
2 3 NaN 5 6 
```

## Összefoglaló
A shell script nagyon hasznos tud lenni, ha unix alapú rendszereken akarunk műveleteket végezni, nem szeretnénk törődni modulok importálásával, valamint összetett szintaktikák alkalmazásával. Bármely Linux felhasználónak jó szolgálatot tesz egy minimális shell script tudás, mivel ezzel felgyorsíthatjuk, kényelmesebbé tehetjük a munkánkat, hosszú távon nagyon kifizetődő. A terjedelmes, gyakran használt parancsokat automatizálhatjuk, ehhez nem kell mást tennünk, mint parancsainkat egy úgynevezett shell script fájlba írni és ezt a fájlt futtathatóvá tenni.
