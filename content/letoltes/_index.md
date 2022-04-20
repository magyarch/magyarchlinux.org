---
title: "Letöltés"
date: 2022-03-14T13:37:56+01:00
draft: false
layout: default
---
A legfrissebb, **2022.03** verziójú MagyArch Linux ISO-t innen töltheted le.

<a href="https://drive.google.com/file/d/1v6XKDjCHTF-ffWx_vhPAUvvHbCmVIHGk/view?usp=sharing" class="btn btn-main mt-20">Letöltés</a>

Az egyes verziók újdonságai a [Hírek](/hirek) menüpontban érhetőek el.

### Ellenőrzés
A letöltött ISO fájl ellenőrző összegei:

MD5: `0791d9a0f14a05fa370a3d48fbfb0360`

SHA1: `c368b493f96272d08b0bef034857cc300587d269`

SHA256: `f46171f2b090d135a84b7c1e7602662ad89745a05bcd229a0179a50ab6be3e4a`

A letöltött ISO fájl ellenőrizhető a Linux/Mac terminálban. Először belépünk a mappába ahova letöltöttük a fájlt. Például így:
```bash
cd ~/Letöltések
```
Ezután elindítjuk a következő parancsok egyikét attól függően melyik ellenőrző összeget szeretnénk ellenőrizni. Javasoljuk legalább 2 ellenőrzését.
```bash
echo "0791d9a0f14a05fa370a3d48fbfb0360 MagyArchLinux-2022.03-x86_64.iso" | md5sum -c

echo "c368b493f96272d08b0bef034857cc300587d269 MagyArchLinux-2022.03-x86_64.iso" | sha1sum -c

echo "f46171f2b090d135a84b7c1e7602662ad89745a05bcd229a0179a50ab6be3e4a MagyArchLinux-2022.03-x86_64.iso" | sha256sum -c
```
Kellemes használatot kíván a MagyArchLinux csapata! Ha bármilyen kérdésed van, nyugodtan [lépj velünk kapcsolatba](/kapcsolatba).
