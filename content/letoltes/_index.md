---
title: "Letöltés"
date: 2022-03-14T13:37:56+01:00
draft: false
layout: default
---
A legfrissebb, **2023.01** verziójú MagyArch Linux ISO-t innen töltheted le.

<a href="https://drive.google.com/file/d/1xcsjvdypyGpCSD5ia6z9NkFoUmvxPpHt/view" class="btn btn-main mt-20">Letöltés</a>

Az egyes verziók újdonságai a [Hírek](/hirek) menüpontban érhetőek el.

### Ellenőrzés
Az ISO fájl ellenőrző összegei:

MD5: `7e4476d90f1c4868f45436738b02cc2a`

SHA1: `02873419c518b50d26f783c8a3169d3fdd0b90a1`

SHA256: `f25de9d5228b6280f0c498b30c8665db62309f20542723bf071da439dae6a696`

A letöltött ISO fájl ellenőrizhető a Linux/Mac terminálban. Először belépünk a mappába ahova letöltöttük a fájlt. Például így:
```bash
cd ~/Letöltések
```
Ezután elindítjuk a következő parancsok egyikét attól függően melyik ellenőrző összeget szeretnénk ellenőrizni. Javasoljuk legalább 2 ellenőrzését.
```bash
echo "7e4476d90f1c4868f45436738b02cc2a MagyArchLinux-2023.01-x86_64.iso" | md5sum -c

echo "02873419c518b50d26f783c8a3169d3fdd0b90a1 MagyArchLinux-2023.01-x86_64.iso" | sha1sum -c

echo "f25de9d5228b6280f0c498b30c8665db62309f20542723bf071da439dae6a696 MagyArchLinux-2023.01-x86_64.iso" | sha256sum -c
```
Kellemes használatot kíván a MagyArchLinux csapata! Ha bármilyen kérdésed van, nyugodtan [lépj velünk kapcsolatba](/kapcsolat).
