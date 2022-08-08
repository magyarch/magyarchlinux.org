---
title: "Letöltés"
date: 2022-03-14T13:37:56+01:00
draft: false
layout: default
---
A legfrissebb, **2022.09** verziójú MagyArch Linux ISO-t innen töltheted le.

<a href="https://drive.google.com/file/d/1Ke4tKhkDiRYMULJgjMBKlCq5Z3IetTiS/view?usp=sharing" class="btn btn-main mt-20">Letöltés</a>

Az egyes verziók újdonságai a [Hírek](/hirek) menüpontban érhetőek el.

### Ellenőrzés
A letöltött ISO fájl ellenőrző összegei:

MD5: `775819a6a3cbba0e7286527e0b202022`

SHA1: `c1ff390d64130f6ccda6fae4c3e226516c356f5c`

SHA256: `ce9a60ee9941523f743d483d18d981354421dd2a370a85cd663af30a02779c99`

A letöltött ISO fájl ellenőrizhető a Linux/Mac terminálban. Először belépünk a mappába ahova letöltöttük a fájlt. Például így:
```bash
cd ~/Letöltések
```
Ezután elindítjuk a következő parancsok egyikét attól függően melyik ellenőrző összeget szeretnénk ellenőrizni. Javasoljuk legalább 2 ellenőrzését.
```bash
echo "775819a6a3cbba0e7286527e0b202022 MagyArchLinux-2022.09-x86_64.iso" | md5sum -c

echo "c1ff390d64130f6ccda6fae4c3e226516c356f5c MagyArchLinux-2022.09-x86_64.iso" | sha1sum -c

echo "ce9a60ee9941523f743d483d18d981354421dd2a370a85cd663af30a02779c99 MagyArchLinux-2022.09-x86_64.iso" | sha256sum -c
```
Kellemes használatot kíván a MagyArchLinux csapata! Ha bármilyen kérdésed van, nyugodtan [lépj velünk kapcsolatba](/kapcsolatba).
