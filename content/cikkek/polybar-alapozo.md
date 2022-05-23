---
title: "Polybar alapozó"
date: 2021-02-10T03:36:53+02:00
draft: false
tags: [ "Konfiguráció" ]
image: images/polybar.svg
---

A Polybar teljesen független, de kifejezetten az i3 és a BSPWM kompatibilitásra tervezték.Használhatja más ablakkezelőkel is.Csak további konfigurációt igényel a testreszabásuk.A bar ugalmas és egyszerű ,könnyen témázható nem igényel bonyolult parancsfájlokat, de ha úgy dönt, létrehozhat egyedi modulokat szkriptekkel.Célja hogy segítse a felhasználókat abban, hogy szép és jól testreszabható állapotsorokat építsenek az asztali környezetükhöz.

## Telepítés

Arch felhasználok számára elérhető az AUR-on keresztül, ha nem különösebben kedveli vagy nem bízik ezekben a forrásokban, akkor maga is elkészítheti. A polybar-t a projekt Github oldalán találja meg.

## Polybar beállítása

A Polybar-t telepítés után konfigurálnia kell. Az egyik nagy erőssége a rugalmasság, amelyet a konfiguráció viszonylag minimális erőfeszítéssel nyújt önnek. Az alapértelmezett konfigurációt letöltve másolhatja, és módosíthatja a konfigurációt, vagy a github-on található kész konfigurációt, és átmásolhatja annak darabjait egy új fájlba, amely az ön konfigurációjává válik. Bármelyik működik, úgyhogy válassza ki a stílusának megfelelőt. Nem számít, melyiket választja, először hozza létre a konfigurációs könyvtárat.

`mkdir ~/.config/polybar/`

Ezután csomagolja ki az alap konfigurációt ebbe a mappába.

```bash
cd ~/.config/polybar
sudo cp -iv /usr/share/doc/polybar/config ~ /.config/polybar/config
```

## Indítás

A Polybar indítása nagyon egyszerű. Szükségünk van egy indító szkriptre vagy egyszerűen hívatkozzunk a kivánt sáv: `polybar example` nevére, attól függ alap vagy már előre konfigolt fájlt használ. Választható (egyéni preferencia) hogy a `.xinitrc`-ből, `.xprofile`-ból vagy az ablakkezelő konfigurációs fájlból induljon a panel. Ha például szkriptel szeretné elíndítani a bar-t, keresse fel az [Arch-wiki](https://wiki.archlinux.org/index.php/Polybar) oldalát.

Hozzon létre egy futtatható fájlt például `$HOME/.config/polybar/launch.sh`, amely tartalmazza az indításhoz szűkséges szkriptet:

```bash
#!/bin/bash

# Terminate already running bar instances
killall -q polybar

# Wait until the processes have been shut down
while pgrep -u $UID -x polybar >/dev/null; do sleep 1; done

# Launch Polybar, using default config location ~/.config/polybar/config
polybar example &

echo "Polybar launched..."
```

Ez a szkript azt jelenti, hogy az ablakkezelő újraindítása a Polybar-t is újraindítja.

Bspwm használata esetén adja hozzá a következőt a bspwmrc fájlhoz:

`$HOME/.config/polybar/launch.sh`

i3 használata esetén adja hozzá a következőket a konfigurációhoz:

`exec_always --no-startup-id $ HOME/.config/polybar/launch.sh`

## Témázás

A színek nyilvánvaló első dolgok, amelyeket módosítani akar.
Sokféleképpen kezelhetjük a színeket. Vessen egy pillantást az alapértelmezett konfigurációra. A `[colors]` szakasznak az alábbi példának kell lennie.

### Színek

```bash
[colors]
;background = ${xrdb:color0:#222} - #.Xresources mód
background = #222
background-alt = #444 - normal mód (hexkód)
;foreground = ${xrdb:color7:#222}
foreground = #dfdfdf
foreground-alt = #555
primary = #ffb52a
secondary = #e60053
alert = #bd2c40
```
Figyelje meg a színek beállításának két különböző módját. Az egyik csak sima hex kódokat használ, ellenben a másik színeket importál a `.Xresources`-ból. Valószínűleg ez a leghatékonyabb, és garantálja, hogy a Polybar mindig illeszkedik a rendszer színvilágához.

**Fontos megjegyezni azt is, hogy ezeket az értékeket a változókhoz rendelik. Ezeket a változókat a konfiguráció során újra felhasználhatja, hogy megkönnyítse az életét, és a színsémáját egységesen tartsa. Elméletileg ezt beállíthatja úgy, hogy egyszer megváltoztathatja a színét `.Xresources`-ben, és az összes X alkalmazásán, és ez a Polybar konfigurációjának minden modulján keresztül érvényesül.**

### Bar

Több sávot definiálhat ugyanabban a konfigurációs fájlban. Ezek definiálásához hozzon létre egy blokkot, hasonlót mint a `[colors]`. Az alapértelmezett sáv a konfigurációban `[bar/example]`. Vessen egy pillantást rá.

```bash
# bar beállitás ( méretek elhelyezkedés stb..)
[bar/example]
;monitor = ${env:MONITOR:HDMI-1}
width = 100%
height = 27
;offset-x = 1%
;offset-y = 1%
radius = 6.0
fixed-center = false

# háttér és szöveg szín
background = ${colors.background}
foreground = ${colors.foreground}

# sor méret és szín
line-size = 3
line-color = #f00

# szegély/bar körüli keret
border-size = 4
border-color = #00000000

# távolság modulok szövegek-nél
padding-left = 0
padding-right = 2

# margók
module-margin-left = 1
module-margin-right = 2

# betűtípus(ok) meghatározása
font-0 = fixed:pixelsize=10;1
font-1 = unifont:fontformat=truetype:size=8:antialias=false;0
font-2 = siji:pixelsize=10;1

# modulok elhelyezkedése a bar-on (bal.közép,jobb)
modules-left = bspwm i3
modules-center = xwindow
modules-right = filesystem xbacklight volume xkeyboard memory cpu wlan eth battery temperature date powermenu

# a tálca meghatározása
tray-position = right
tray-padding = 2
;tray-transparent = true
;tray-background = #0063ff

# eredeti helyzetére áll vissza (nem takarja a bar-t)
;wm-restack = bspwm               # bspwm
;wm-restack = i3                  # i3 

# felülbírál
;override-redirect = true

# görgetés fel-le
;scroll-up = bspwm-desknext       # bspwm esetén
;scroll-down = bspwm-deskprev

#görgetés fel-le
;scroll-up = i3wm-wsnext          # i3 esetén
;scroll-down = i3wm-wsprev
```

## Végszó

Most már rendelkeznie kell egy alap ismerettel ahhoz, hogy elkészíthesse saját konfigurációját, és önállóan elmélyülhessen azokban a fantasztikus dolgokban, amelyeket a Polybar-ral tehet.
