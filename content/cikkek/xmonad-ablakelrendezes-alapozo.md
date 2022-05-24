---
title: "Xmonad ablakelrendezés alapozó"
date: 2021-01-01T20:46:37+02:00
draft: false
tags: [ "Konfiguráció", "Xmonad" ]
image: images/xmonad.png
---

## "Magas" elrendezés

A Tall(Magas) elrendezésben bal oldalon van a fő ablaktábla, a Master ablak és a képernyő felét elfoglalja. Az összes többi ablak megosztja a képernyő jobb felét, és függőlegesen, felülről lefelé halmozódik.

A Tall(Magas) ablakelrendezésnek három opcionális paramétere van. Az első meghatározza a kezdő ablakok számát a fő ablaktáblán (ami alapértelmezés szerint 1), ez használat közben a `mod + ,`/`.`gombokkal módosítható. Mivel a Tall a beépített elrendezések egyike, az `xmonad.hs` konfigurációs fájlban nem kell külön importálni.

`myLayout = Tall 1 (3/100) (1/2)`

Ez a go-to elrendezés, és ez az első, amelyet kap, amikor az xmonad-ot futtatja a dobozból. Gyakori, hogy egy ablak fókuszban van, miközben néhány másodlagos ablak látható, így a Tall elrendezés remekül működik. Nagyon hasznos sok helyzetben, de a jobb oldali ablakok kissé zsúfoltnak tűnnek öt ablakon túl.

## "Spirál" elrendezés

A spirális elrendezés úgy kezdődik, hogy egy ablak veszi a bal oldali képernyő többségét, majd egy másik ablak foglalja el a fennmaradó rész tetejét, majd egy másik a maradék jobb oldalán, majd a maradék alján, majd a maradék bal oldalán , stb.

Az ablak által elfoglalt hely nagyságának és a fennmaradó részének népszerű aránya az Aranymetszés (kb. 0,856), amely az ablakokat egy Fibonacci-spirál szimulálására késztetné. Ez azonban nem szükséges, és tetszőleges frakciót tehet.

```haskell
import XMonad.Layout.Spiral

myLayout = spiral (6/7)
```

Őszintén szólva úgy gondolom, hogy ennek az elrendezésnek a felhasználása szűk. Előfordult már, hogy hasznos volt egy olyan elrendezés, amelyben az egyes ablakok egymás után kisebbek voltak, és spirálszerűen helyezkedtek el, de a leggyakoribb alkalmazás számomra az volt, hogy megmutassam a barátaimnak, hogy mire képes az xmonad.

## "Három oszlop" elrendezés

Ahogy a neve is sugallja, a `ThreeCol` elrendezés három oszlopra osztja a képernyőt: egy elsődleges és két másodlagos. Eredeti formában az elsődleges oszlop a bal oldalon található, és a képernyő felét lefedi. Ezután a következő két ablak vízszintesen osztja meg a képernyő másik felét. Ha van negyedik ablak, akkor a harmadik ablak középre tolódik, és a középső oszlop függőlegesen oszt meg két ablakot. Az ötödik ablak megosztja a jobb oldali oszlopot a negyedik ablakkal. Az összes következő ablak ugyanúgy kerül a két jobb oszlopba.

A `ThreeCol` konfigurációja megegyezik a `Tall` konfigurációjával, az első paraméter az elsődleges ablaktáblában szereplő ablakok kezdő száma, a második paraméter az átméretezés mennyisége, a harmadik pedig a fő oszlop kezdeti aránya.

```haskell
import XMonad.Layout.ThreeColumns

myLayout = ThreeCol 1 (3/100) (1/2)
```

Ez az elrendezés különösen hasznos programozáskor, különösen, ha csak egy képernyője van. Az elsődleges ablaktábla tartalmazza a kódot. A másik kettő tartalmaz egy böngészőt dokumentációval (vagy a google kereséseket és a Stack Overflow!), Valamint egy ablakot fordítással és tesztkészlet kimenettel - mindkettő általában jobb, ha függőlegesen helyezzük el.

Van még egy változat (sok elrendezésnél vannak olyan változatok, amelyek az eredetihez csavart kínálnak) a ThreeColMid nevű, amely ugyanúgy van konfigurálva, mint a ThreeCol, de az elsődleges ablaktáblát középre helyezi, a másik két oszlop mindkét oldalán. Ez különösen nagy a széles képernyőknél, mivel a fontos dolgokat közvetlenül a látókörébe helyezi, a másodlagosakat pedig a perifériára.

## "Rács" elrendezés
A Rács elrendezés az ablakokat vízszintesen és függőlegesen rendezi el, amennyire csak lehetséges. Ha négy ablak van, akkor azok derékszögű grafikonként vannak elrendezve. Ha kilenc ablak van, úgy vannak elrendezve, mint egy tic-tac-toe tábla.
Ehhez az elrendezéshez nincsenek paraméterek, bár van olyan változata, amely lehetővé teszi az oszlopok és sorok arányának beállítását.

```haskell
import XMonad.Layout.Grid

myLayout = Grid
```

Ez a legjobb elrendezés nagyszámú ablak egyidejű megjelenítéséhez, mivel mindegyik ablak nagyjából azonos méretű.

## "Multi-Cols" elrendezés

A `MultiColumns` elrendezés egymás mellé rendezi az ablakokat, mindegyik kitölti a teljes függőleges teret és megosztja a vízszintes teret.
A `mod + ,`/`.` billentyűk segítségével több ablak egyesíthető oszlopokká, megosztva a függőleges helyet. Az első és a második paraméter multiCol meghatározza az oszlopok megosztására képes ablakok maximális számát minden oszlopban. A másik két paraméter az egyes oszlopok relatív szélességét írja le, alapértelmezés szerint egyforma méretű oszlopok.

```haskell
import XMonad.Layout.MultiColumns

myLayout = multiCol [1] 1 0.01 (-0.5)
```

Ez az elrendezés optimális több terminál megjelenítésére streaming kimenettel. Ilyen módon nagyon geeknek és hűvösnek tűnik.

## "Teljes" elrendezés

Ez az elrendezés a legegyszerűbb - kitölti a teljes képernyőt egy ablakkal. Az összes többi ablak elrejtőzik mögötte, és a szokásos módon ( `alt + tab`, vagy `mod + j/k`) használva kerékpározva elölre viszi őket .
Ehhez az elrendezéshez nincsenek paraméterek.

```haskell
myLayout = Full
```

A teljes elrendezés ideális videók megtekintéséhez, vagy ha egyszerre csak egy dologra kíván koncentrálni. Akkor is jó, ha olyan alkalmazást vagy programot használ, amely már felosztja a képernyőt, és nem akarja elrontani annak belső elrendezését - például a VIM vagy a Tmux osztott képernyős munkamenetét.

# Módosítók

Az xmonad néhány módosítót is kínál, ezek olyan funkciók, amelyek elfogadják az elrendezést, és valamilyen módon módosítják azokat. A két modósítót így fogom említeni itt Mirror(tükör) és spacing(távolság).

A Tükör módosító elrendezést készít és 90 fokkal elforgatja. A legjobb példa erre az útmutató, a Mirror Tall(Magas tükör) végleges elrendezése.

## "Magas tükör" elrendezés

A Mirror Tall elrendezés a Tall elrendezés, de az oldalán elforgatva. A mesterablak a tetején, amely a képernyő teljes felső felét elfoglalja. Az összes többi ablak osztja az alsó felét, balról jobbra.

```haskell
myLayout = Mirror (Tall 1 (3/100) (3/5))
```

## Spacing/Gaps magyarul távolság/rés:

A másik gyakran használt módosító a spacing. A megadott paramétertől függően ez egy bizonyos szélességű rést ad az egyes ablakok (és a képernyő széle) között, felfedve az ablakok hátterét. Ha a képernyőn lévő területnek van tartaléka, az vizuálisan teret enged az ablakainak a lélegzéshez,ez segíthet megkülönböztetni a hasonló kinézetű ablakokat. Emellett nagyon klassznak tűnik.

Az xmonad különböző elrendezéseinek legegyszerűbb módja, ha kiválasztja a kedvenc elrendezését, és beírja az xmonad.hs konfigurációs fájlba. Ezután a használat közben nyomja meg a mod + space gombot az elrendezés végigpörgetéséhez (és a mod+ shift+ space-t pedig az első elrendezés visszaállításához).

Az érthetőség kedvéért azt javaslom, hogy az összes elrendezést határozza meg egy változóban, amely a fő funkción kívül esik, majd utaljon rá a hívásában xmonad. Használja a, háromcsöves kezelőt, ||| a kívánt elrendezések felsorolásához. Használja a haskell függvényalkalmazás-operátorát, a dollárjelet $, hogy módosítót alkalmazzon az egész listára.
