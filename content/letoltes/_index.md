---
title: "Letöltés"
date: 2022-03-14T13:37:56+01:00
draft: false
layout: default
---
A legfrissebb, **2023.01** verziójú MagyArch Linux ISO-t innen töltheted le.

<a href="https://drive.google.com/file/d/1WVHxvKmIkzmuOhV8SkRKq-8BG_siQq5k/view" class="btn btn-main mt-20">Letöltés</a>

Az egyes verziók újdonságai a [Hírek](/hirek) menüpontban érhetőek el.

### Ellenőrzés
Az ISO fájl ellenőrző összegei:

MD5: `3cdd747c64e817d5836098cc9b4880ac`

SHA1: `f462fed0133885eb2590808916d6c2128af28ef4`

SHA256: `63474afdcd74ef46172d4503b5afde452d90fe8e3abec18dd42b4583e1a7ea31`

A letöltött ISO fájl ellenőrizhető a Linux/Mac terminálban. Először belépünk a mappába ahova letöltöttük a fájlt. Például így:
```bash
cd ~/Letöltések
```
Ezután elindítjuk a következő parancsok egyikét attól függően melyik ellenőrző összeget szeretnénk ellenőrizni. Javasoljuk legalább 2 ellenőrzését.
```bash
echo "3cdd747c64e817d5836098cc9b4880ac MagyArchLinux-2022.12-x86_64.iso" | md5sum -c

echo "f462fed0133885eb2590808916d6c2128af28ef4 MagyArchLinux-2022.12-x86_64.iso" | sha1sum -c

echo "63474afdcd74ef46172d4503b5afde452d90fe8e3abec18dd42b4583e1a7ea31 MagyArchLinux-2022.12-x86_64.iso" | sha256sum -c
```
Kellemes használatot kíván a MagyArchLinux csapata! Ha bármilyen kérdésed van, nyugodtan [lépj velünk kapcsolatba](/kapcsolat).
