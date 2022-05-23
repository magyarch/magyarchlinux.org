---
title: "QEMU és a virtualizáció"
date: 2021-02-28T03:03:22+02:00
draft: false
tags: [ "Virtualizáció" ]
image: images/qemu.jpg
---

A Qemu egy virtualizációs technológiai emulátor, amely lehetővé teszi az operációs rendszerek és a Linux disztribúciók egyszerű futtatását a jelenlegi rendszeren anélkül, hogy telepítenie kellene őket, vagy ki kellene írni az ISO fájlokat. Olyan, mint a VMware vagy a VirtualBox. Bármikor használhatja bármelyik operációs rendszer futtatását sok eszközön és architektúrán.

A QEMU ingyenes és nyílt forráskódú program, ami GPL 2. licenc alatt áll, és képes KVM, valamint XEN modelleken futni (ha először engedélyezte a virtualizációs technológiát a BIOS-ból), és rengeteg virtualizációs lehetőséget kínál. Ebben a cikkben elmagyarázzuk a QEMU használatát és telepítését.

Szerencsére a QEMU szinte az összes hivatalos Linux disztribúciós tárolóból elérhető. Ez jó dolog számunkra, mivel nem kell semmit letöltenünk vagy telepítenünk harmadik fél adattáraiból.

## A QEMU használata

Először létre kell hoznunk egy virtuális merevlemez-képet, ha valahova telepíteni akarjuk a virtuális operációs rendszerünket. Ez a képfájl a telepítés után az operációs rendszer összes adatait és fájljait tartalmazza. Ehhez használhatjuk a `qemu-img` eszközt.
Egy 30 GB méretű, és qcow2 formátumú képfájl létrehozásához (ez az alapértelmezett formátum a QEMU képekhez) futtassa ezt a parancsot:

`qemu-img create -f qcow2 testing-image.img 30G`

**Fontos! Ne feledje, hogy a `home` mappában (vagy azon a helyen, ahol a terminált futtatja) most létrejön egy új fájl `testing-image.img` néven. Vegye figyelembe azt is, hogy ennek a fájlnak a mérete nem 30 gigabájt, csak kb. 450 KB; A QEMU csak akkor használ helyet, ha a virtuális operációs rendszernek szüksége van rá, de a kép maximálisan megengedett területét csak 30 gigabájtra állítja be.**

Most, hogy létrehoztuk a képfájlunkat, ha van egy ISO fájlunk egy Linux disztribúcióhoz vagy bármely más operációs rendszerhez, és azt QEMU használatával szeretnénk tesztelni, és az általunk létrehozott új képfájlt merevlemezként használni, futtathatjuk a következő sort amit mi most (telepítési parancsnak nevezzünk el:

`qemu-system-x86_64 -m 2048 -boot d -enable-kvm -vga virtio -smp 4 -net nic -net user -hda testing-image.img -cdrom ~/Letöltések/MagyArchLinux-2021.02-x86_64.iso`

**Magyarázzuk el az előző parancsrészt:**

`-m 2048`: Itt választottuk ki azt a RAM mennyiséget,(tetszőlegesen változtatható) amelyet a QEMU számára biztosítanunk kell az ISO fájl futtatásakor.

`-boot -d`: A boot opció lehetővé teszi számunkra, hogy meghatározzuk a rendszerindítási sorrendet, melyik eszközt kell először elindítani. A `-d` azt jelenti, hogy a CD-ROM lesz az első, majd a QEMU rendszerint a merevlemez képére indul. A `-cdrom` opciót használtuk, amint az a parancs végén látható. Használhatja a `-c` parancsot, ha először a merevlemez-képet akarja betölteni.

`-enable-kvm`: Lehetővé teszi számunkra, hogy a KVM technológiát felhasználva a kívánt architektúrát utánozzuk. Enélkül a QEMU nagyon lassú szoftver-megjelenítést fog használni. Ezért kell használnunk ezt az opciót, csak győződjön meg arról, hogy a virtualizációs beállítások engedélyezve vannak a számítógép BIOS-ában.

`-vga virtio`: Azt jelenti: Szimulálni egy általános kényelmes virtuális gépet normál hardveres korlátozások nélkül.

`-smp 4`: Ha egynél több magot akarunk használni az emulált operációs rendszerhez. Úgy döntöttünk, hogy 4 magot használunk a virtuális kép futtatásához, ami gyorsabbá teszi. Célszerű megváltoztatni ezt a számot a számítógép CPU-jának megfelelően.

`-net nic -net <felhasználó>`: Ezeknek az opcióknak a használatával alapértelmezés szerint engedélyezzük, hogy egy Ethernet Internet kapcsolat elérhető legyen a futó virtuális gépben.

`-hda testing-image.img`: Itt adtuk meg a használt merevlemez elérési útját. Esetünkben a testing-image.img fájlt hoztuk létre korábban.

`-cdrom MagyArchLinux-2021.02-x86_64.iso`: Végül elmondtuk a QEMU-nak, hogy be akarjuk indítani az „MagyArchLinux-2021.02-x86_64” ISO fájlt.

`-show-cursor`: Egér emuláció(szükséges lehet ha nem jelenik meg)

**Vegye figyelembe, hogy ebben az oktatóanyagban az `x86_64` architektúrát használtuk a QEMU futtatásához.**

Az előző parancs futtatása után a QEMU önálló ablakként indul el:

Ha a képfájlból szeretne ISO-fájl nélkül elindulni (például, ha befejezte a telepítést, és most mindig a telepített rendszert szeretné indítani), akkor egyszerűen eltávolíthatja a `-cdrom` opciót:

`qemu-system-x86_64 -m 2048 -boot d -enable-kvm -smp 4 -net nic -net user -show-cursor -hda testing-image.img`

A cikk végére is értünk,láthatják nem volt olyan bonyolult.A qemu egy nagyszerü program,tessék kipróbálni!
