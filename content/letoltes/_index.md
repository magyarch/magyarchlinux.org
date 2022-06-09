---
title: "Letöltés"
date: 2022-03-14T13:37:56+01:00
draft: false
layout: default
---
A legfrissebb, **2022.06** verziójú MagyArch Linux ISO-t innen töltheted le.

<a href="https://drive.google.com/file/d/18F-f3CIGBAtfzYSWfCWsSBMx98rSvgjv/view?usp=sharing" class="btn btn-main mt-20">Letöltés</a>

Az egyes verziók újdonságai a [Hírek](/hirek) menüpontban érhetőek el.

### Ellenőrzés
A letöltött ISO fájl ellenőrző összegei:

MD5: `f50966076f71d3be005ace7cc53663cd`

SHA1: `182e7d5dee2d75333f402865cb5faaf2078d0eeb`

SHA256: `e70eb6b69fb7c6cebc6ddfd54804d6f57d3d0b59b8fffbd9c740680a7ada4d17`

A letöltött ISO fájl ellenőrizhető a Linux/Mac terminálban. Először belépünk a mappába ahova letöltöttük a fájlt. Például így:
```bash
cd ~/Letöltések
```
Ezután elindítjuk a következő parancsok egyikét attól függően melyik ellenőrző összeget szeretnénk ellenőrizni. Javasoljuk legalább 2 ellenőrzését.
```bash
echo "f50966076f71d3be005ace7cc53663cd MagyArchLinux-2022.03-x86_64.iso" | md5sum -c

echo "182e7d5dee2d75333f402865cb5faaf2078d0eeb MagyArchLinux-2022.03-x86_64.iso" | sha1sum -c

echo "e70eb6b69fb7c6cebc6ddfd54804d6f57d3d0b59b8fffbd9c740680a7ada4d17 MagyArchLinux-2022.03-x86_64.iso" | sha256sum -c
```
Kellemes használatot kíván a MagyArchLinux csapata! Ha bármilyen kérdésed van, nyugodtan [lépj velünk kapcsolatba](/kapcsolatba).
