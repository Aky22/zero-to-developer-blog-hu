---
layout: post
title: "3. Felhasználó++"
author: Botond János Kovács <botondjanoskovacs@gmail.com>
---

# Bevezető

Ebben a modulban az operációs rendszert vesszük górcső alá. Megtanuljuk, hogy mi az a 
parancssor, mit jelent az, hogy "futtatási argumentum", környezeti változó, és, hogy mi
az a szabványos be- és kimenet.

# A parancssor

Amikor az első személyi számítógépek piacra kerültek, nem voltak olyan kifinomult videó
technológiák, hogy ablakokat tudjon a számítógép a képernyőre rajzolni. Helyette a számítógépet
szöveges parancsokkal lehetett irányítani. Az ilyen szöveges parancsokkal lehetett mappákat
létrehozni, mappák között navigálni, fájlokat írni, olvasni, és gyakorlatilag a számítógépen
mindent csinálni. Ahogyan a számítógépbe kerülő hardver sebessége fejlődött, úgy elkezdtek
megjelenni a grafikus interfészek, később az "ablakos megoldást" alkalmazó operációs rendszerek
is. Ezután már a felhasználónak nem volt szüksége arra, hogy parancsokat adjon a számítógépnek,
mert ezeket a parancsokat az egér segítségével is ki tudta adni. Az informatikusoknak és a 
programozóknak azonban nagyon sokszor kell olyan szoftvereket használnia, amik nem rendelkeznek
grafikus felhasználói interfésszel, ezért az összes mai operációs rendszerben lehetőség adódik
a régi, azóta is az operációs rendszer részét képző szöveges interfészt használni. Windows-ban
ezt a szöveges interfészt `parancssornak` nevezzük. A parancssort úgy tudjuk elindítani, hogy
megnyomjuk a `WINDOWS + R` gombokat, majd beírjuk a megjelenő ablakba, hogy `cmd.exe`, végül
entert nyomunk, vagy a futtatás gombra kattintunk.

![A "run" ablak]({{site.url}}/assets/images/module-3/figure-1-run-dialog.png)

A megjelenő, valószínüleg fekete hátterű és fehér betűket tartalmazó ablak maga a parancssor.
Parancsokat úgy tudunk futtatni, hogy az ablakba begépeljük a futtatandó parancsot, majd
entert nyomunk. A futtatott parancs írhat különböző üzeneteket ugyanebbe az ablakba, de futtatás
után ugyanaz a sor jelenik meg, mint amikor elindítottuk az alkalmazást.

![Így néz ki a parancssor]({{site.url}}/assets/images/module-3/figure-2-cmd-window.png)

![Ez történik, ha futtatunk egy parancsot]({{site.url}}/assets/images/module-3/figure-3-cmd-after-running-a-command.png)

