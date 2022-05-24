---
title: "Bootolható pendrive készítés dd-vel"
date: 2020-12-07T21:10:20+02:00
draft: false
tags: [ "Eszközök" ]
---

[Wiki](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_basic_command_line_utilities)-n és egyéb helyeken a pontos doksi és leírás megtalálható. Egyszerű, hatásos, és egyben veszélyes a dd, ha nem figyelsz oda.

Rengeteg felhasználási formája lehet, most csak a [telepítő ISO](https://magyarchlinux.org/letoltes/)-k pendrájvra kiírását vázolom, ahogy én szoktam. Régóta és sokszor használtam, használom. Bajt még nem csináltam, mert be tartok egy-két ökölszabályt.

1. Minden ISO-mat külön könyvtárban tartok, mellette csak a checksum-ja van szöveges fájlban.
2. Mindig abban a könyvtárban nyitok terminált, amelyik ISO-t ki akarom írni.
3. **Mindig lecsekkolom az eszközök neveit.** (`sudo fdisk -l`)
4. Használom a `TAB`-ot a fájlnév kiegészítésére.
5. Mielőtt entert nyomok az írásra, kétszer minimum átnézem a céleszköz nevét.

`sudo dd if=valami.iso of=/dev/sdx bs=4M status=progress && sync`

**if=valami.iso** - kezd el gépelni az ISO nevét, majd TAB-al egészítsd ki
**of=/dev/sdx** - a céllemez, ott van előtted a sudo fdisk -l kimenet, annak megfelelően írd be
**status=progress** - ez mutatja az írás folyamatát, sebességét, kiírt adat mennyiségét
**&& sync** - szabályosan leválasztja és kiadja a pendrájvot

Várj addig ameddig a promptod vissza nem kapod. Ha előtte húzod ki a pendrájvot hiányos lehet a kiírás. A pendrájvod nem fog bootolni vagy hibás telepítés lesz a vége.

A témában Xeoncpu készített egy videót is, amelyben további ezközöket mutat be.
