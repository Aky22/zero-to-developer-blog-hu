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

![A "run" ablak]({{site.url}}{{site.baseurl}}/assets/images/module-3/figure-1-run-dialog.png)

A megjelenő, valószínüleg fekete hátterű és fehér betűket tartalmazó ablak maga a parancssor.
Parancsokat úgy tudunk futtatni, hogy az ablakba begépeljük a futtatandó parancsot, majd
entert nyomunk. A futtatott parancs írhat különböző üzeneteket ugyanebbe az ablakba, de futtatás
után ugyanaz a sor jelenik meg, mint amikor elindítottuk az alkalmazást.

![Így néz ki a parancssor]({{site.url}}{{site.baseurl}}/assets/images/module-3/figure-2-cmd-window.png)

A következő ábrán láthatjuk azt, mi történik, amikor begépelünk, és futtatunk egy parancsot:

![Ez történik, ha futtatunk egy parancsot]({{site.url}}{{site.baseurl}}/assets/images/module-3/figure-3-cmd-after-running-a-command.png)

A parancssor tehát így működik:

* Látjuk azt, hogy melyik könyvtárban tartózkodunk éppen. A könyvtár utáni `>` karakter jelzi, hogy
  oda írhatjuk a következő parancsot
* Begépeljük a futtatandó parancsot, majd entert nyomunk
* A parancssorban ekkor új sor kezdődik, majd a futtatott parancs szöveget ír(hat) a következő
sorokba
* Új sor kezdése után ismét látjuk a jelenlegi könyvtárat, és újra adhatunk meg parancsot

A Windows-ban használható sok, még a DOS-ból maradt parancs. Ezek közül a leghasznosabbak:

* `cd KÖNYVTÁR`: Másik könyvtárba lehet navigálni ezzel a paranccsal. A `KÖNYVTÁR` helyére 
  be kell illeszteni a célkönyvtárat.
* `mkdir KÖNYVTÁR_NEVE`: Új könyvtárat lehet segítségével létrehozni. A `KÖNYVTÁR_NEVE` helyére
  be kell illeszteni az új könyvtár nevét.
* `echo SZÖVEG`: Kiírja pontosan ugyanazt a szöveget, amit beírtunk a `SZÖVEG` helyére
* `type FÁJL_NEVE`: Beolvas egy szöveges fájlt (azt, aminek a `FÁJL_NEVE` a neve), és a tartalmát
  kiírja a parancssorba
* `rmdir KÖNYVTÁR_NEVE`: Törli a `KÖNYVTÁR_NEVE` nevű könyvtárat
* `del FÁJL_NEVE`: Törli a `FÁJL_NEVE` nevű fájlt

Láthatjuk, hogy az összes felsorolt parancsnál van valami behelyettesítendő szöveg. Ezt a szöveget
a parancsok megkapják, és aszerint módosul a viselkedésük, hogy mit írtunk oda. Ezeknek a szövegeknek
a gyűjtő neve: `parancssori argumentum`.

A két parancs között megjelenő szöveg, amit az egyik parancs "kiír" a parancssorban a parancs `kimenete`.

Léteznek olyan parancsok, melyeket elindítunk, ám futásuk során kiegészítő felhasználói interakcióra
van szükségük. Ilyenkor feltehetnek kérdéseket (például `Írja be a nevét: `), és a felhasználónak
be kell gépelnie valamit. Azt, amit a felhasználó ilyenkor begépel a parancs `bemenetének` nevezzük.
A következő ábrán láthatunk olyan parancsot, aminek szükséges a parancs futtatása közben is bemenetet
adnunk:

![A date parancs bekéri a dátumot a felhasználótól]({{site.url}}{{site.baseurl}}/assets/images/module-3/figure-4-date-command.png)

Felmerülhet a kérdés ezek után: Nagyon jó, hogy vannak ezek a parancsok, de tudok saját parancsot is 
csinálni? A válasz az, hogy **IGEN**. Ezek a parancsok ugyanis egytől egyig ugyanolyan futtatható
`.exe` fájlok a számítógépen, mint a játékok, a Google Chrome, és minden egyéb futtatható alkalmazás.
Egészen pontosan a parancsokhoz tartozó `.exe` fájlok a `C:\Windows\System32` mappában találhatóak.
Létezik ebben a könyvtárban `cd.exe`, `mkdir.exe`, stb. Így elméletileg ha készítünk egy futtatható
programot, és ebbe a könyvtárba helyezzük, akkor a parancssorban használhatjuk a fájl `.exe` nélküli
nevét, és így futtathatjuk a saját programunkat! És hogy hogyan lehet ezt még egyszerűbbé tenni, a
következő fejezetből kiderül.

# Környezeti változók

Azt már tudjuk, hogy ha a parancssorba begépelünk egy parancsot, akkor a `C:\Windows\System32` mappában
próbálja megkeresni az operációs rendszer a futtatandó programot. Ez az állítás viszont nem teljesen igaz.
Konfigurálható ugyanis a Windows-ban (és egyébként minden más operációs rendszerben is), hogy pontosan
melyik könyvtárakban próbáljon meg keresni a begépelttel egyező nevű programot az operációs rendszer.
Ezt a beállítást az operációs rendszer egy ún. `környezeti változóban` tárolja.

A környezeti változók olyan rendszerszintű beállítások, amiknek van egy egyszerű szöveges neve, és egy
szöveges értéke. Ha megváltoztatunk egy környezeti változót, az operációs rendszer szinten megváltozik,
és minden új program futtatásakor már a módosított környezeti beállítások lesznek érvényesek. Ezekhez
a környezeti változókhoz **minden** futtatott program hozzáfér. Segítségükkel könnyen lehet konfigurálni
egyes alkalmazások viselkedését, többet között a parancssorét.

Szóval hogyan is találja meg a parancssor, hogy melyik programot kell futtatni, amikor beírunk egy 
parancsot? A következő algoritmus segítségével:

1. Legyen a futtatott parancs neve `X`. A program fájlneve, amit keresünk így `X.exe`, vagy amennyiben
   `X` már eredetileg `.exe`-re végződik, simán `X`. Ezt a fájlnevet tároljuk az `Y` változóban.
2. Először megnézzük, hogy van-e `Y` nevű fájl a jelenlegi mappában. Ha van, végeztünk, lefuttatjuk.
3. Nézzük a `PATH` elnevezésű környezeti változó értékét. Ennek a környezeti változónak az értéke úgy
   van definiálva, hogy minden egyes elem a könyvtárlistában egy `;` karakterrel van elválasztva. Így
   megyünk végig az összes felsorolt `Z` mappán, a könyvtárlista eredeti sorrendjében.
4. Megnézzük, hogy létezik-e `Y` nevű futtatható fájl a `Z` mappában. Ha igen, végeztünk, és lefuttatjuk.
5. Amennyiben egyik mappában sem találtunk megfelelő fájlt, kiírunk egy hibát a felhasználónak.

A környezeti változók értékét parancssorban könnyen lekérhetjük. Az `echo %VÁLTOZÓ_NEVE%` parancs ki
fogja írni a `VÁLTOZÓ_NEVE` nevű környezeti változó értékét. Például az `echo %PATH%` parancs segítségével
megnézhetjük, hogy a parancsok futtatásakor a Windows melyik mappákban keresi a megadott parancsot.

A környezeti változók értékét kétféleképpen szerkeszthetjük:

* Nyitunk egy fájlböngészőt, majd a "This PC"-re kattintunk a jobb egér gombbal. Ezután kiválasztjuk a 
  "Properties" opciót. A felugró ablakban, a bal oldali sávban látunk egy "Advanced System Settings" 
  feliratú linket, arra kattintsunk. A felugró ablak jobb alsó sarkában látunk egy "Environment Variables ..."
  feliratú gombot, arra kattintva válik elérhetővé a környezeti változók szerkesztését biztosító eszköz
* Nyomunk egy `WINDOWS + R` kombinációt, a felugró ablakba a következőt írjuk: `rundll32 sysdm.cpl,EditEnvironmentVariables`,
  majd entert nyomunk, vagy a "Run" gombra kattintunk.

# A modul fogalmai

* parancssor
* fontosabb parancsok: cd, mkdir, echo, type, rmdir, del
* parancssori argumentum, futtatási argumentum
* parancs kimenete, program kimenete
* parancs bemenete, program bemenete
* környezeti változó
* környezeti változó vizsgálata, módosítása