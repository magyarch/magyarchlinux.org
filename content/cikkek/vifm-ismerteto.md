---
title: "Vifm ismertető"
date: 2021-02-09T04:14:03+02:00
draft: false
tags: [ "Eszközök" ]
image: images/vifm.png
---

## Jellemzők

A vifm fájlkezelő segítségével mozgathatja a fájlrendszerhierarchiát: Pl: fájlok másolása, fájlok törlése,  beillesztése, keresése .... mindezt gyorsan és hatékonyan. Mi többre van szüksége egy fájlkezelőben?

## Telepítés

Természetesen a parancssorból telepítjük. Ezt egy Arch alapú disztribúcióban (például MagyArch vagy Manjaro) a következő módon teheti meg:

1. Nyisson meg egy terminál ablakot.
2. Adja ki a parancsot `sudo pacman -S vifm`.
3. Írja be a sudo jelszavát, és nyomja meg az `Enter` billentyűt.
4. Az `y` gomb lenyomásával fogadja el az esetleges függőségeket.
5. A telepítés végeztével készen áll a vifm fájlkezelő használatára.

## Használat

![A vifm felülete](/images/vifm.png)

A vifm megnyitásához írja be a `vifm` parancsot egy nyított terminál ablakba. A fájlkezelő megnyitásakor egy kétoldalas ablak jelenik meg (lásd 1. ábra). Amit kiemelve lát, az jelenleg aktív oldal.

A fejléc alatt lásd 1.ábra `../` karakterlánc azt jelenti, hogy felmegy a szülő könyvtárba. Tehát ha megnyomja az `enter` billentyűt, miközben ez be van jelölve, akkor az aktuális könyvtár szülő könyvtárába lép (az 1. ábra esetében ez lenne a `home`).A könyvtár-hierarchia fel és le mozgatásához használja a fel és le nyilakat vagy a `j` és `k` billentyűt. A két oldal között az oda-vissza mozgatáshoz használja a `Tab` billentyűt.

A vifm fájlkezelő hasonlóan működik, mint a vi szerkesztő - billentyűkombinációkkal rendelkezik a feladatok elvégzéséhez.

### A leghasznosabbak:

`yy` - a yank rövidítése egy fájlt (vagy "másolatot" jelent).

`p` - jelentése helyezzen be egy fájlt (vagy "illessze be" ).

`dd` - fájl törlése.

`Enter` - fájl megtekintése (nem jelenít meg bináris fájlokat).

`/` - fájl keresés (a / karaktert a keresési karakterlánc követi).

`za` - rejtett másnéven .(dot fájlok).

`s` - a beállított terminál ablakba lép.

`bg` - a kijelölt kép beállitása háttérképnek.

`mkd` - mappa létrehozása.

`w` - fájlok mappák tartalmának előnézete.

`X` - (shift + x) tömörített fájlok kicsomagolása (szükséges hozzá unzip és unrar csomag)

`A` - (shift + a) fájlok átnevezése.

`E` - (shift + e) kiválasztott `$EDITOR` használata a kijelölt fájl-on.

`q` - kilépés.

`:q` - kilpés megszokott vi módban

Tegyük fel, hogy másolni szeretne egy fájlt az egyik könyvtárból, és beilleszteni a másikba. A folyamat lépései a következők:

1. Vigye a kiválasztó sávot a másolni kívánt fájlra és
2. Nyomjon `yy`-t.

3. Vigye a kiválasztó sávot a könyvtárba, ahová a fájlt lemásolja, és nyomja meg a a `jobbra nyílat` az `Enter`-t vagy az `l` billentyűt (ezután a könyvtár belsejébe lép).

4. Nyomja meg a `p` gombot, és a fájl lemásolódik.

## Végszó

Ha szöveges fájlkezelőre van szüksége, akkor egy jó alternatíva lehet a vifm (én ezt használom). Nyilvánvaló, hogy meg kell tanulnia új billentyűkombinációkat (kivéve, ha már hozzászoktál a vi-hez), de a vifm sebessége és hatékonysága mindent elárul.
