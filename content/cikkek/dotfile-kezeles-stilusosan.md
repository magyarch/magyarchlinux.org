---
title: "Dotfile kezelés stílusosan, avagy mire való a Git Bare Repository"
date: 2020-09-26T11:28:57+02:00
draft: false
tags: [ "Konfiguráció" ]
image: images/Git-Bare-Repository-Banner.png
---
Ha hosszú ideje használjuk a Linux rendszerünket, valószínűleg elég sokat módosítottunk már az egyes programok dotfile-jain (A dotfile-ok olyan konfigurációs fájlok, melyeknek neve előtt pont van.) Mivel eléggé fárasztó dolog minden egyes újratelepítéskor megint  személyre szabni a konfigurációs fájljainkat, célszerű őket egy könnyen kezelhető helyen tárolni. Legtöbben a Git verziókezelő-rendszert szokták erre használni olyan módon, hogy minden egyes módosítás után átmásolják a konfigurációs fájlt egy külön mappába, majd feltöltik GitHub-ra vagy Gitlab-re. Viszont ez a módszer egy idő után fárasztóvá tud válni. Ezt a módszert hivatott kiváltani a Git Bare Repository, aminek a használatával sokkal könnyebbé tehető a konfigurációs fájlok kezelése.
<!--more-->
A Git Bare Repository egy olyan Git-tároló, aminél nem kell bemásolni a Git-tároló helyi mappájába azokat a fájlokat, amiket menteni szeretnénk, hanem megadhatjuk azt az alapmappát, ahonnan fel szeretnénk tölteni a fájlokat. Git Bare Repository létrehozásához először csinálnunk kell egy tárolót GitLab-en vagy GitHub-on (ne hozzunk létre Readme fájt), majd készítsünk a következő paranccsal egy Bare Git Repository-t:
```bash
mkdir dotfiles && cd dotfiles && git init --bare
```

Ezek után nyissuk meg a `.bashrc` fájlt és írjuk bele a következő sort, majd újraindítjuk a terminálunkat, ezzel létrehozva egy aliast:
```bash
alias dot='/usr/bin/git --git-dir=$HOME/dotfiles/ --work-tree=$HOME'
```

Most már nincs más dolgunk, mint futtatni a GitLab/GitHub által javasolt parancsokat, azzal a különbséggel, hogy a `git` szót minden parancsban cseréljük le `dot`-ra. Mivel sok olyan fájl lesz, amit soha sem szeretnénk hozzáadni a tárolónkhoz, célszerű kiadnunk a `dot config --local status.showUntrackedFiles no`, hogy a git commitok kiadásánál ne lássuk a nem követett fájlokat. 
