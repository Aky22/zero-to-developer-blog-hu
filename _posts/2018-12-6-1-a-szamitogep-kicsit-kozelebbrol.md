---
title: "1. A számítógép, kicsit közelebbről"
author: Botond János Kovács <botondjanoskovacs@gmail.com>
---

# Bevezetés

Ebben a modulban kicsit közelebbről ismerkedünk meg a számítógéppel. Megtanulod, hogy nagyvonalakban
hogyan tárolja a számítógép a fájlokat, mit csinál a processzor, és pontosan mi is történik, amikor
bekapcsolod a számítógépet.

# A számítógép felépítése

Minden számítógép, beleértve a laptopokat, PC-ket, telefonokat különböző komponensekből áll. Ha ezeket
a komponenseket megfelelő módon összekötjük, akkor egy igazi számítógépet kapunk. Ezek a komponensek
általánosságban a következőek:

* `CPU`: Másnéven `processzor`, ez a számítógép "agya". Legalábbis ezt a megfogalmazást szokták használni
a legtöbb számítógépes szakirodalomban. Míg ez a megfogalmazás nem teljesen valótlan, egy kicsit 
pontatlan; gondolhatnánk azt is, hogy minden számítógépben pontosan 1 darab processzor van, de ez
egyáltalán nem igaz. Vannak többprocesszoros rendszerek (főleg nagy teljesítményű szerverek), de
ami ennél is fontosabb, hogy minden különálló komponens, amit a számítógépbe rakunk **is** rendelkezik
egy saját processzorral. A processzor feladata az, hogy a felhasználó által készített, vagy telepített
programok kódját végrehajtsa.
* `Operatív tár`: Másnéven `memória`, vagy `RAM` (Random Access Memory). A számítógép programjainak
szüksége van az ún. memóriára, ha nagyon nagy adattömegekkel dolgoznak. Ha például egy bérszámfejtőszoftverben 
szeretnénk egyszerre 100 ember adatait kezelni, akkor ezeket az adatokat az operatív 
tárban tároljuk. Az operatív tár tartalma **megsemmisül**, ha kikapcsoljuk a számítógépet.
* `Háttértár`: Másnéven `tárhely`, `merevlemez`, stb. A háttértár is memória abból a szempontból, hogy
adatokat tárolunk benne, ám 3 nagyon fontos különbség van az operatív tár és a háttértár között:
    * Az operatív tár tartalma megsemmisül, amikor kikapcsoljuk a számítógépet, a háttértár tartalma
    azonban megmarad.
    * A háttértár **lényegesen** lassabb, mint az operatív tár. Több nagyságrendű lassulásról beszélünk
    * A háttértár mérete általában sokkal nagyobb, mint az operatív táré. Ennek az (egyik) oka az, hogy a 
    háttértár ára gigabájtonként sokkal olcsóbb, mint az operatív táré
* `Bővítő kártyák`: Ezek sokrétű eszközök, a legtöbb ilyen "kártya" speciális célokra készült, és
csak speciális számítógépekben elérhető. Akad néhány, ami ma már minden számítógép részét alkotja,
például a hálózati kártya, USB controller, videókártya, és ezek közül több is a számítógép egy
másik komponensén, az `alaplapon` integráltan elérhető. A leggyakoribb ilyen bővítőkártyák:
    * `Videókártya`: A számítógép által készített, a monitoron megjelenő kép elkészítésének gyorsításáért
    felel, illetve a számítógép ennek a kártyának a speciális memória chip-jein, a `videómemóriában`
    tárolja a képernyőn megjelenő képet.
    * `Hálózati kártya`: Ahhoz, hogy a számítógépeket hálózatokhoz tudjuk csatlakoztatni, szükség
    van egy hálózati kártyára.
    * `Hangkártya`: A számítógép hangkimenetének vezérléséért felelős.
    * `USB controller kártya`: A számítógéphez csatlakoztatható USB (universal serial bus) perifériák
    vezérléséért felelős

A továbbiakban kicsit részletesebben ismertetem az operatív tárat (amelyet ettől a ponttól fogva 
`memóriának` fogok nevezni), a háttértárat, illetve a processzort.

# Háttértár

A számítógép rengeteg adatot tárol; a letöltött programoktól kezdve a filmekig megszámlálhatatlanul
sok fájl található a számítógépeinken. Minden olyan adat, ami a számítógép újraindítását követően
is elérhető kell, hogy legyen az ún. `háttértáron` van tárolva. Ma a leggyakrabban használt háttértár
típusok a `merevlemezek (HDD)`, az `SSD-k`, illetve az `optikai lemezek (CD, DVD, BlueRay)`. 

Ezeken az eszközökön minden létező adat `bináris formátumban` van tárolva, azaz **egyesek** és 
**nullák** formájában. A mágneslemezek esetén (HDD) egy író-olvasó fej halad végig a forgó lemezen,
és a mágneses tér változásából tudja kikövetkeztetni, hogy pontosan az író-olvasó fej alatti részen
egy egyes, vagy egy nullás szerepel-e. 

Ezt azért írtam le, mert elengedhetetlen annak a megértése, hogy a HDD, az SSD, vagy a CD/DVD/BlueRay
**nem tudja**, hogy azok az adatok, amiket ír, vagy olvas magára / magáról éppen milyen fájlhoz, 
könyvtárhoz, vagy bármi máshoz tartoznak. Ahhoz, hogy ezt az információt is meg tudjuk határozni 
(azaz tudjunk létrehozni, módosítani, olvasni és törölni konkrét fájlokat és mappákat), be kell vezetni
egy új fogalmat, a `fájlrendszer` fogalmát. A fájlrendszert az operációs rendszer kezeli, a mögöttes
háttértárnak általában nincsen fogalma arról, hogy rajta most éppen milyen fájlrendszer szerint 
van az adat rendezve. A fájlrendszer felelős azért, hogy a fájljaink név és elérési útvonal szerint
legyenek elérhetőek, hogy meghatározhassuk azt, hogy a fájlokat mikor módosították utoljára, hogy
korlátozhassuk a felhasználók fájl elérését (azaz, hogy egyes felhasználók ne férhessenek hozzá egyes
fájlokhoz, másokhoz viszont igen).

A fájlrendszerhez is értelemszerűen tartoznak tárolandó adatok: milyen könyvtáraink, illetve fájljaink
léteznek, ki hozta őket létre, mikor, stb. Éppen ezért magát a `fájlrendszert leíró állományt` is
a háttértáron tároljuk. 

Egy fizikai háttértár eszközön azonban nem csak egy fájlrendszer létrehozása lehetséges; amikor egy
háttértáron több, különálló fájlrendszert hozunk létre, akkor `particionáljuk` a háttértárat. 
Windows-ban az egyes partíciókat az operációs rendszer egy betűjellel azonosítja (például `C`, vagy `D`).

Fontos megemlíteni még a `formázás` nevű műveletet is; amikor egy partíciót `formázunk`, az annyit
jelent, hogy a partícióhoz tartozó `fájlrendszer leíró állományt` alapállapotba rakjuk. Ezzel logikailag
töröljük az összes fájlt, és könyvtárat ami a fájlrendszeren megtalálható volt, viszont fizikailag
ezek az adatok elérhetőek maradnak. Létezik a formázásnak egy olyan módja is, az ún. `teljes formázás`,
amikor a régi adatokat felülírjuk nullákkal, vagy bármilyen más generált adattal. A teljes formázás
után a régi adatok nem visszaállíthatóak.

A fájlrendszereknek rengeteg típusa van: FAT, NTFS, ext4, stb. Léteznek open-source fájlrendszerek, 
és closed-source fájlrendszerek is. A fájlrendszereket a következő adatok jellemzik:

* Maximális fájlméret
* Maximális fájlszám
* Fájlnév maximális hossza
* Maximális partíció méret

(Megjegyzés: A fentieken kívül még számos jellemző tulajdonsága van a fájlrendszereknek, de ezek közül
sok bonyolultabban megérthető van, ezek a legtipikusabbak, és a legfontosabbak)

Néhány példa fájlrendszerekre:

| Fájlrendszer neve | Leírás | Maximális fájlméret | Maximális fájlszám | Fájlnév maximális hossza | Maximális partíció méret |
| FAT32 | A DOS-ból is ismert, ma is gyakran használatos fájlrendszer. A teljes neve: `File Allocation Table` | 4 GiB - 1 byte | 268 173 300 | 255 karakter | 2 TiB |
| NTFS | Ma szinte minden Windows alapú számítógép ezt a fájlrendszert használja. A teljes neve: `New Technology File System` | 16 TB | 2^32 - 1 | 255 karakter | 256 TB |
| ext4 | Egy open-source "naplózó" fájlrendszer, legfőképp a linux alapú rendszerek használják. | 16 TiB | 4 000 000 000 | 255 byte | 1 EiB (1 048 576 TB) |

# Processzor

A számítógép folyamatosan azt csinálja, ami a nevében is benne van: számol. Egészen konkrétan az a 
komponens, ami ezeket a számításokat végzi az ún. `processzor`. Ez az áramkör képes bekérni a 
felhasználótól a futtatandó parancsokat, majd szekvenciálisan (szigorúan sorrendben) végrehajtja
azokat. Ezek a parancsok sokrétűek, akad olyan, ami két számot az össze, mások pedig a monitoron
egy adott pixelt piros színűre váltanak. 

A mai processzorok ezeknek a parancsoknak a végrehajtását annyira gyorsan csinálják, hogy azt még
elképzelni is nehéz: egy átlagos 1 magos, 2 GHz órajelű processzor másodpercenként 2 000 000 000
darab utasítást képest feldolgozni, és végrehajtani. Ez lehet ennyi összeadás, ennyi darab karakter
kiírása a képernyőre, vagy bármi más, amire az adott processzor képes.

Amikor programozunk, akkor gyakorlatilag nem is csinálunk mást, mint a processzornak megmondjuk,
hogy mit csináljon. Ahhoz, hogy ezt megtehessük, szükségünk van egy közös nyelvre, amit mi is 
beszélünk, és a processzor is: ez a programozási nyelv. Nos, hát igazából mégsem, mert az a 
programozási nyelv, amit a processzor beszél elég primitív, ennek a nyelvnek a neve `gépi kód`,
vagy angolul `assembly`. Ez egy annyira egyszerű és primitív nyelv, hogy csak ahhoz, hogy mondjuk
egy darab 'a' betűt ki tudjunk rajzolni a képernyő bal felső sarkába, szükségünk van többtízezer
sor kódra. Az életben viszont láthatjuk, hogy nagyon sok olyan alkalmazás létezik, ami sokkal többet
tud, mint a képernyő bal felső sarkába rajzolt 'a' betű. Szóval hogyan is van ez? Nos erre a kérdésre
konkrétan egy későbbi modulban kapsz választ, egyellőre most maradunk a processzornál.

A processzor (nagyvonalakban) a következő egységekből áll:

* `regiszterek`: Ilyenből általában 8-32 darab van egy processzorban. Ezek fix hosszúságú (például 32 bit)
bináris számok tárolására alkalmas, memória szerű valamik.
* `APU`: Az `APU`, másnéven `Arithmetic Processing Unit`, magyarul `Aritmetikai feldolgozó egység` felelős
azért, hogy az alapvető matematikai műveleteket elvégezhessük (összeadás, kivonás, maradékos osztás, szorzás).
* `FPU`: A `FPU`, másnéven `Floating Point Unit`, magyarul `Lebegőpontos egység` a lebegőpontos (ezekről később),
azaz "nem túl pontos törtszámokon" végzett műveletek végrehajtásáért felel

A processzor ezen kívül áramköri összeköttetéseken keresztül hozzáfér az operatív tárhoz, illetve
minden, a számítógéphez csatlakoztatott komponenshez és perifériákhoz.

A processzor csak nagyon egyszerű parancsokat tud végrehajtani. A legfontosabb típusú parancsok a 
következők:

* Regiszter feltöltő parancsok: Ezeknek a parancsoknak a segítségével írhatunk be egy konstans számot,
vagy olvashatunk be a memóriában, vagy egy másik regiszterből értéket egy adott regiszterbe.
* Aritmetikai parancsok: Ezek a parancsok a regiszterekben, vagy a memóriában tárolt értékek között
végzendő matematikai műveleteket realizálnak.
* Memória parancsok: A memória parancsok segítségével írhatunk adatot a memóriába, vagy tölthetünk
be adatot a memóriából a regiszterekbe.
* Elágazó parancsok: Ezek a parancsok azt csinálják, hogy megadunk egy logikai feltételt (egy 
eldöntendő kérdést), amire ha "IGEN" a válasz, akkor a program egy másik, általunk megadott sorára
ugrik a végrehajtás, ha "NEM", akkor folytatódik a következő sorral. Ezek a "legfontosabb" parancsok,
ezek segítségével késztethetjük a számítógépet valós döntések meghozatalára.

De hogyan kerülnek be ezek a parancsok a processzorba? A következő fejezetben ismertetem.

# Hogyan indul el a számítógép?

Megnyomjuk a bekapcsológombot, mindenféle LED-ek elkezdenek világítani, egy pittyegést hallunk, majd
a monitoron megjelenik a "Windows betöltése folyamatban" felirat. Nagyon egyszerűnek hangzik, de igazából
több milliárd parancs hajtódott végre ez alatt a pár másodperc alatt a számítógép processzorán. Ez a 
fejezet megpróbálja dióhéjban szemléltetni, és elmagyarázni, hogy mi is történt pontosan.

Amikor a számítógép alaplapja áram alá kerül, az első dolog ami bekapcsol az ún. `BIOS ROM`. Ez egy
olyan `ROM` (Read Only Memory), amit az alaplap gyártója programozott, az ezen a chip-en tárolt
programkód betöltődik a processzorba, ami elkezdni végrehajtani a `BIOS` (Basic Input Output System) kódot.

A BIOS kód először végigszkenneli a csatlakoztatott komponenseket, és perifériákat: megnézi, milyen
háttértárak elérhetőek, mennyi operatív memória áll rendelkezésre, milyen típusú bővítőkártyákat
talál. Amikor ezt a szkennelést befejezte, beindul a `boot szekvencia`. 

A boot szekvencia során a BIOS program végigmegy a csatlakoztatott háttértár eszközökön abban a 
sorrendben, amit a felhasználó beállított, és kiolvassa a háttértáron található ún. `MBR`-t. Az
MBR (Master Boot Record) egy 4 KiB méretű blokk, ami mindig a háttértár legelső blokkja. Amennyiben
ebben a blokkban található a processzor által futtatható gépi kód, úgy a BIOS a boot szekvenciát
befejezi, és átadja a vezérlést ennek a 4 KiB-nyi kódnak. 

4 KiB nagyon kevés, nyilvánvalóan nem fér bele egy teljes operációs rendszer. Éppen ezért ebbe a 
4 KiB-ba a legtöbb operációs rendszer egy speciális kódrészletet, az ún. `boot loader`-t helyezi.
A boot loader feladata az, hogy beállítson néhány, az operációs rendszer futtatásához szükséges
dolgot, és betöltse a háttértárról az operációs rendszer valós kódját az operatív tárba. Amikor ezzel
végzett, a vezérlést tovább adja az operációs rendszer inicializációs részének, és innentől kezdve
az operációs rendszer gyakorlatilag fut.

Ettől a ponttól kezdve minden operációs rendszer másképp viselkedik, hiszen alapvető eltérések vannak
a fájlkezelésben, memória és periféria kezelésben minden operációs rendszer között. Ez a `boot szekvencia`
viszont majdnem minden operációs rendszerben ugyanúgy működik.

Általában a boot szekvenciából a felhasználó semmit sem lát, lévén, hogy az egész néhány ezredmásodperc
alatt végbemegy. A Windows töltőképernyő, bejelentkező ablak, majd utána az asztal, böngésző, és 
minden más, amit látunk a képernyőn már "felhasználói program".

# A modul fogalmai

* háttértár
* merevlemez (HDD), SSD, optikai lemez (CD, DVD, BlueRay)
* bináris formátum
* fájlrendszer
* particionálás, partíció
* formázás, teljes formázás
* FAT32, NTFS, ext4
* processzor
* regiszterek, APU, FPU
* gépi kód, assembly
* BIOS
* MBR
* boot szekvencia
* boot loader