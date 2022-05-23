---
title: "Hogyan lehet kernelt váltani Arch Linuxon"
date: 2021-03-11T02:07:06+02:00
draft: false
tags: [ "Konfiguráció", "Kernel" ]
image: images/arch.svg
---

Elsőként beszéljünk arról milyen kernel változatok léteznek, amelyek Arch felhasználóként elérhetők.

## Kernel

### Mainline kernel:

Ez a legújabb legfrissebb stabil Linux kernel.Ezt használják legtöbben. Miért? - mert támogatja a legfrissebb hardvereket.

### Lts kernel:

Ez a legújabb, hosszú távon támogatott Linux kernel. Nincs előre meghatározott életciklusa, de biztos lehet benne, hogy sokkal hosszabb ideig élvezheti ugyanazt a kernel verziót.

### Linux hardened:

A legújabb stabil kernel edzett verziója, amit tudni kell nem biztos, hogy minden program megfelelően fog futni használatakor.

### Zen kernel:

Ez a kernel ami a legtöbbet hozza ki rendszeréből, alapvetően a legújabb kernel optimalizált, tweakelt verziója.

## Folyamat:

1. Telepítse a választott Linux kernelt (a `pacman` paranccsal telepítheti)
2. Grub konfigurációs fájl szerkesztése.

Többféle Linux kernelt is telepíthet a rendszerbe, és a grub menüből kiválaszthatja, melyik kernelt használja.

## Példák:

```bash
sudo pacman -S linux #(mainline kernel)
sudo pacman -S linux-lts #(hosszú távon támogatott)
sudo pacman -S linux-hardened #(edzett kernel)
sudo pacman -S linux-zen #(zen kernel)
```
Az Arch Linux alapértelmezés szerint a legújabb kernelváltozatot használja. További verziók a speciális beállítások alatt érhetők el.

## Szerkesztés

1. Tiltsa le a grub almenüt, hogy az összes elérhető kernelváltozat megjelenjen a főképernyőn (a speciális beállítások helyett).

2. Konfigurálja a grub-ot, hogy visszahívja az utolsó kernelbejegyzést, és alapértelmezett bejegyzésként használja a következő alkalommal történő indításhoz.

Nyissa meg a terminált, és szerkessze a konfigurációs fájlt a kedvenc terminálalapú szövegszerkesztőben. Én a neovimet ajánlom.

`sudo nvim /etc/default/grub`

![grub config](/images/grub.png)

Meg változtattam két alap értéket és egy új sort adtam hozzá:

```bash
GRUB_DISABLE_SUBMENU=y # (almenü letiltása)
GRUB_DEFAULT=saved     # (utolsó kernelbejegyzés mentése)
GRUB_SAVEDEFAULT=true  # (mentett bejegyzés használata)
```

Mentse el a konfigurációs fájlt, és lépjen ki

**FONTOS!! Útolsó lépésként generáljuk újra a grub konfigurációs fájlt!**

Nyisson egy terminalt és írja be a következő parancsot:

`sudo grub-mkconfig -o /boot/grub/grub.cfg`
