---
title: "BSPWM"
date: 2021-02-09T04:34:24+02:00
draft: false
tags: [ "BSPWM" ]
image: images/bspwm.svg
---

A Bspwm a `Binary Space Partitioning Window Manager` rövidítése.

A Bspwm nem `DE`, de kezeli a rendszerablak(ok) kinézetét és viselkedését, amelyet mozaikablak-kezelőnek is neveznek.

Az ablakkezelő kizárólag a hozzárendelt billentyűzet gombfunkciókon vagy billentyűkombinációkon működik.

A billentyűkapcsolatokhoz szükségünk van egy másik programra, például az `SXHKD`-re, amely a `Simple X Hot Key Daemon` rövidítése.
A bspwm és az `sxhkd` kombinációja kiválóan működik együtt, mindkét csomagot ugyanaz a `Baskerville` nevű alkotó írta.

Ebben az oktatóanyagban a Bspwm és az sxhkd fájlokat állítom össze forrásból, de telepítheti az AUR-ból, ha úgy tetszik, mind a git, mind a legújabb stabil verzió elérhető.

## Útmutató

Ezt az útmutatót követve kb. 20 perc, hogy működőképes legyen a bspwm (ablakkezelő).

Néhány függőségre van szükség, amit telepítenünk kell:

`sudo pacman -S libxcb xcb-util xcb-util-wm xcb-util-keysyms`

## Kezdetek

Először a bspwm és az sxhkd repók klónozásával kezdünk, ezt megteheti a következő sorok beírásával a terminálba:

```bash
git clone https://github.com/baskerville/bspwm.git
git clone https://github.com/baskerville/sxhkd.git
```

Most a cd parancsal a klónozott bspwm mappába lépünk:

`cd bspwm`

majd futassuk le a következőket:

```bash
make
sudo make install
```

Most ugyanezt tesszük a klónozott sxhkd mappával is:

```bash
cd sxhkd
make
sudo make install
```

Most átmásoljuk a példa fájlokat, hogy legyen egy alap konfigurációnk. Először azonban létre kell hoznunk egy könyvtárat, ahová átmásoljuk őket:

`mkdir -p ~/.config/{bspwm,sxhkd}`

Másoljuk ide példa konfigurációs fájlokat:

`cp /usr/local/share/doc/bspwm/examples/bspwmrc ~/.config/bspwm/bspwmrc`

és

`cp /usr/local/share/doc/bspwm/examples/sxhkdrc ~/.config/sxhkd/sxhkdrc`

Ezután a Bspwm konfigurációs fájlt egy shell parancsal futtathatóvá kell tennünk:

`chmod u+x ~/.config/bspwm/bspwmrc`

Ha nem akarunk display manager-t de mégis szeretnénk elindítani Bspwm-t bejelentkezéskor. Létre kell hoznunk egy `~/.xinitrc` fájlt és abba gépeljük be hogy:

`exec bspwm`

Még nem vagyunk kész, de most már rendelkeznünk kell egy működő Bspwm beállítással.

Mivel a példafájlok célzottan bizonyos programokat használnak, a használat megkönnyítése érdekében egy speciális terminált telepítünk, csak a kezdéshez:

`sudo pacman -S rxvt-unicode`

Indítsa újra a számítógépet, írja be felhasználónevét és jelszavát, majd `startx`.

Most fekete képernyőt kell látnia.

A `mod + return` billentyűkombinációra megnyílik egy terminál aminek a neve `urxvt`.

Ez kitölti az egész képernyőt - most nyisson meg egy új terminált, és láthatja, hogyan működik az elosztás. Most 2 terminálja lesz a képernyőt ketté osztva. Nyisson további, terminal ablakot és nézze meg, hogy az automatikus séma hogyan helyezi el a terminálokat a képernyőn. Különböző sémákat lehet választani de én inkább a spirált szeretem, de többnyire az előválasztást használom.

Ablak bezárása:

`mod + w` ezt célszerü azonnal megváltoztatni például:

`mod + q` a MagyArch Linux-on ez az alap billentyűkombináció.

Az előválasztás használatával eldöntheti, hová akarja eljuttatni a következő terminált, ahelyett hogy a Bspwm döntene ön helyett.

`mod + ctrl + h, j, k, l (balra, lefelé, felfelé, jobbra)`

Most megfigyelhető egy előre kiválasztott terület, ahol megnyílik a következő ablak. Rajta próbáld ki.

## Hasznos alapbeálliltások:

A szövegszerkesztő számomra az egyik legfontosabb csomag, ezért mindig először ezt telepítem, de kiválaszthatja, amit csak szeretne. Ezután a preferált szerkesztőnket használjuk a szerkesztéshez

`sudo nvim /.config/sxhkd/sxhkdrc`

Most keresse meg a sort a terminálemulátorral (az első sorok egyike), és szerkessze a telepítettre - esetemben az `urxvt` és hozzáadom. Könnyű, igaz?

Javaslom, hogy nézze át az `sxhkdrc` fájlt, hogy megértse, mely billentyűkötéseket használják, és szerkessze az ön személyes preferenciái szerint.

A terminálokon kívül a BSPWM kissé hervasztónak tűnhet - a fekete terminálban nincs semmi pompa. De ezt könnyű orvosolni - csak a bspc-t kell használnia a konfiguráláshoz.

Például, ha fehér ablakszegélyeket szeretne, akkor:

`bspc config normal_border_color "ffffff"`

Ha azt szeretné, hogy a fókuszált ablak piros szegéllyel rendelkezzen

`bspc config focused_border_color #900900"`

Ha a vastag keretet szereti:

`bspc config border_width 6`

A lehetőségek szinte végtelenek.

Megváltoztathatjuk az automatikus osztási sémákat - osztási arányokat - hozzáadhatunk/eltávolíthatunk hiányosságokat stb

Ha egeret használ, akkor ez a beállitás megfontolandó:

`bspc config focus_follows_pointer true`

Tehát bármelyik ablak felett a kurzor lebeg - fókuszban van

Néhány személyes "kötelező beállítás"

```bash
bspc config split_ratio          0.50

bspc config single_monocle       true

bspc config borderless_monocle   true

bspc config gapless_monocle      true

bspc config pointer_follows_focus true

bspc config center_pseudo_tiled true
```

Ahhoz, hogy ezek a konfigurációk állandóak maradjanak, hozzá kell adnia a `bspwmrc` fájlhoz.

Javaslom a `bash` vagy `zsh` automatikus kiegészítéssel történő használatát, ez egyszerű módja annak, hogy megtalálja a bspwm által kínált összes lehetőséget.

Csak írja be a `bspc` parancsot, és nyomja meg a tab billentyűt. Ha konfigurációs opciókat keres, akkor beírhatja:

`bspc config`

Ezután nyomja meg a `TAB` billentyűt, és megmutatja az összes konfigurációs lehetőséget.

A `man bspc` is egy jó módja annak, hogy többet tudjon meg.

Mint említettük, a `bspwmrc` egy shell szkript, így saját külső szabályokat írhat a bspwm viselkedésének hozzáadásához/megváltoztatásához. Ha nem tudja, hogyan kell szkripteket írni, a GitHubon sok konfiguráció található, ahová átmásolhatja/beillesztheti a megvalósítani kívánt dolgokat.

## Végszó

Oké, szóval most van egy működő bspwm alapbeállításod, de jó lenne, ha rendelkeznél egy divatos sávval és egy programindítóval, esetleg valamiféle értesítésel?

A [polybar](http://magyarchlinux.org/cikkek/polybar-alapozo/)-t, a `rofi`-t, és a `Dunst`-ot ajánlom.

Mindegyik alap konfigurációja elegendő és egyszerűen konfigurálhatóak a szkriptek ismerete nélkül.

Csak nézze meg az adott program konfigurációs fájljait, és meglátja, mit kell szerkeszteni és/vagy megjegyzéseket fűzni. Ezek mind nagyon könnyű programok.

Vannak más lehetőségek is, többek között, de egy kezdő számára szerintem a polybar, rofi, és a Dunst a legjobb kiindulópont, mert a konfigurációs fájlok ember által olvashatók.

Most kezdje el elkészíteni saját csodálatos Bspwm-jét, és ne féljen elrontani a konfigurációs fájlokat. Ne feledje, hogy van bspc fájlunk, így változtathat a dolgokon, mielőtt valóban módosítaná a konfigurációt.

Próbálja ki, mielőtt eldönti, hogy valóban szeretné-e szerkeszteni a fájlban. Elrontani igazán nem lehet ha mégis, ne feledje hogy mindig újrakezdheti a példafájlok másolásával, ahogy az elején tette.
