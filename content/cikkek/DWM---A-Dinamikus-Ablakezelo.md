---
title: "DWM - A Dinamikus Ablakezelő"
date: 2021-03-13T01:42:17+02:00
draft: false
tags: [ "DWM" ]
image: images/dwm-1.png
---

A Dwm a Dynamic Window Manager (Dinamikus Ablak kezelő) rövidítést jelenti.Amit tudnunk kell hogy C program nyelven íródott és ez egy minimalista csempéző ablak kezelő, amelyet kifejezetten az X11-hez terveztek. Úgy tervezték, hogy sokkal kisebb, gyorsabb és egyszerűbb legyen, mint az alternatívái. A Suckless közösség azt állítja, hogy a dwm kódjának soha nem szabad meghaladnia a 2000 SLOC-ot (forráskódsor-t),csakúgy, mint a többi Suckless eszköz, ez is az elitistának szól, és a suckless erről gondoskodik is. A dwm-nek nincs bináris eloszlása. Ez csak egy forrásfájl, amelyet kézzel kell lefordítania a kezdéshez. A testreszabáshoz szükség van a forrás közvetlen szerkesztésére és a semmiből való felépítésre (ami egyszerűbb, mint amilyennek látszik).

## Jellemzők

A Dwm csak egyetlen bináris fájl, és forráskódja soha nem haladja meg a 2000 SLOC értéket. A testreszabás a forráskód szerkesztésével történik, ami nagyon könnyen érthető. Csempézett elrendezésben az ablakok kezelése egy fő és egymásra rakható területen történik. A főterület tartalmazza azt az ablakot, amelyre jelenleg a legnagyobb figyelmet kell fordítani, míg a halmozási terület az összes többi ablakot tartalmazza. Monocle elrendezésben az összes ablak a képernyő méretére maximalizálódik. A lebegő (floating) elrendezésben az ablakok átméretezhetők és szabadon mozgathatók. A párbeszédablakokat mindig lebegve kezelik, függetlenül az alkalmazott elrendezéstől.További elrendezések és funkcionalitások adhatók hozzá patchelésel(foltozással) mint az összes Suckless feljesztésnél ez úgymond a filozófiajuk.

## Telepítés

Több lehetőség adott de én a suckless repót fogom használni a dwm telepítéséhez:

```bash
# klónozd a forrás dwm repót
git clone git://git.suckless.org/dwm

# lépj a leklónozott mappába
cd dwm

# futtasd a tiszta telepítést
make clean install
```

Most egyszerűen írja be a következő sort a `~/.xinitrc` fájlba:

`exec dwm`

Ha a fájl nem létezik hozza létre a touch `.xinitrc` parancsal.

**További információért olvasd el a githubon található [pdf fájlunkat](https://github.com/bazeeel/magyarch-dwm/blob/main/.local/share/Magyarch-dwm.pdf).**

Egyre több felhasználó inkább a grafikus bejelentkezést preferálja, mint például a LightDM.

A LightDM egy asztali bejelentkezés kezelő.

## Főbb jellemzői

- Támogatja a különféle asztali felületeket.
- Támogatja a különböző megjelenítési technológiákat (X, Mir, Wayland ...).
- Egyszerű, alacsony memóriafelhasználás és nagy teljesítmény.
- Támogatja a vendég bejelentkezéseket.
- Támogatja a távoli bejelentkezést (bejövő - XDMCP , VNC , kimenő - XDMCP).
- Átfogó tesztcsomag.
- Minimális kódösszetétel.

## Telepítés és szolgáltatás indítása

```bash
sudo pacman -S --noconfirm --needed lightdm lightdm-gtk-greeter-settings lightdm-gtk-greeter
```

Ezután elindítjuk a lightdm szolgáltatást:

```bash
sudo systemctl enable lightdm.service
```

## Bejelentkezés grafikusan

Ahhoz hogy müködjön a bejelentkezés az ablak kezelő felületen el kell végeznünk néhány módosítást.

Hozzunk létre egy dwm asztal bejegyzést így: `sudo nvim /usr/share/xsessions/dwm.desktop` az ablakkezelőnek, a következő adatokkal:

```bash
[Desktop Entry]
Encoding=UTF-8
Name=DWM
Comment=DWM Session
Exec=/usr/local/bin/dwm
Type=Application
Keywords=wm;tiling
```

Már kész is vagyunk. Jelenkezzen ki vagy indítsa újra számitógépét.
