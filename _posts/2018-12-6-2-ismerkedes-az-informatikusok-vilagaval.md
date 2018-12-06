---
layout: post
title: "2. Ismerkedés az informatikusok világával"
author: Botond János Kovács <botondjanoskovacs@gmail.com>
---

# Bevezető

Ebben a modulban az informatikusok világával fogunk ismerkedni: gyakori jelölések,
egy kis gyakran használt matematika, mértékegységek, ilyesmi. Ezek a dolgok nagyon fontosak
lesznek a későbbi modulokban, ugyanis a programozásban mindenhol előfordulnak, és
alapvető fontosságú a megértésük, és tudásuk.

# Boole-algebra

A programozásban szinte minden problémát eldöntendő kérdésekre vetítünk le, azaz 
két állapotú változókra bontjuk. Ezeket a változókat összevonva használhatunk bináris
számokat is, amikben minden helyiértéken szerepelhet `1`, vagy `0`. Logikailag az 
`1` és `0` helyett szoktuk azt is mondani, hogy `IGAZ`, vagy `HAMIS`. 

Az olyan eldöntendő kérdéseket, amiket programozásban használunk, általában 
`logikai feltételnek` nevezzük. A logikai feltételek `kiértékelhetőek`, kiértékelés
után kapjuk meg az eredményüket (ami `IGAZ`, vagy `HAMIS`). Logikai feltétel lehet az
`a < b` (azaz `a kisebb mint b`), vagy az, hogy `piros-e a nadrág`. Ezen kívül két vagy
több logikai feltétel között értelmezünk bizonyos műveleteket. Ezek a `logikai műveletek`
a következőek lehetnek:

* `ÉS`: Az `ÉS` művelet kettő, vagy több logikai feltétel között értelmezett. Az olyan
logikai feltételek eredménye, amelyek kettő, vagy több logikai feltétel `ÉS`-ezésének 
kompozíciója akkor `IGAZ`, ha a kompozícióban szereplő **összes** logikai feltétel
eredménye `IGAZ`. Jelölései (`a` és `b` logikai feltételek):
    * `a ∧ b`
    * `a · b`
    * `a & b`
    * Programkódban: `a && b`
* `VAGY`: A `VAGY` művelet is kettő, vagy több logikai feltétel között értelmezett. 
Eredménye akkor `IGAZ`, ha a kompozíciót alkotó logikai feltételek **legalább egyike**
`IGAZ`. Jelölései (`a` és `b` logikai feltételek): 
    * `a ∨ b`
    * `a + b`
    * `a | b`
    * Programkódban: `a || b`
* `NEM`: A `NEM` művelet egy darab logikai feltétellel használható. Az eredménye `IGAZ`,
ha a `NEM`-ezett logikai feltétel értéke `HAMIS`, és `HAMIS`, ha a `NEM`-ezett logikai
feltétel értéke `IGAZ`. Jelölése (`a` logikai feltétel):
    * `¬a`
    * `~a`
    * Programkódban: `!a`
* Zárójel: Úgy, mint a számokkal történő számolásban, a logikai feltételeknél is használhatóak
zárójelek, hogy a logikai feltétel egyes részeit csoportosítsuk, és előbb kelljen kiértékelnünk,
mint a többit. A zárójelek műveleti sorrendje ugyanúgy működik, mint az aritmetikában (a 
legbelső zárójellel kezdünk).

Példák logikai feltételekre:

* `az alma piros ÉS több, mint kétszáz forintom van`: Akkor `IGAZ`, ha az alma piros, és több,
mint kétszáz forintom van. Ha az alma nem piros, akkor mindenképp `HAMIS`, ugyanúgy, mint
amikor kevesebb, mint kétszáz forintom van.
* `NEM (elindul a kocsi) ÉS tudom az autószerelő telefonszámát`: Akkor `IGAZ`, ha nem indul
az autó, és tudom az autószerelő telefonszámát. Ha elindul az autó, vagy nem tudom az autószerelő
telefonszámát, akkor már `HAMIS`.

Megjegyzés: A logikai feltételek az halmazokhoz nagyon hasonló módon működnek. Gyakorlatilag az
`ÉS` művelet megfeleltethető a metszetképzésnek, a `VAGY` művelet az unióképzésnek, a `NEM` 
művelet pedig a komplementerképzésnek.

Ezeknek a logikai feltételeknek azért van kiemelt fontossága az informatikában, mert amikor
egy kétállapotú változót alakítunk át elektromos áramkörré, tökéletesen megvalósíthatjuk a 
műveleteket, lévén, hogy az `IGAZ` állapotot realizálhatjuk úgy, hogy `VAN FESZÜLTSÉG A VONALON`,
a `HAMIS` állapotot pedig úgy, hogy `NINCS FESZÜLTSÉG A VONALON`. A mai informatika, és a ma
használt összes számítógép (a kvantumszámítógépeket kivéve) ezen az alapon működik.

# A byte és a számrendszerek

Az informatikában van egy rendkívül fontos mértékegység: a `byte`. Egy `byte` pontosan 8
darab `bit`, egy `bit` pedig pontosan 1 darab kétállapotú logikai változó. Ez azért is kifejezetten
fontos, mert ez azt jelenti, hogy több bit segítségével ábrázolhatunk számokat, kettes számrendszerben.

Ugyebár az összes számrendszer úgy működik, hogy van egy alapunk, legyen ez most a 10 (tízes 
számrendszer esetén), és helyiértékenként növeljük a számot leíró polinomban az alap hatványkitevőjét.
Pontosan ugyanígy működik a kettes számrendszer is, ami azt jelenti, hogy egy darab byte-on a
legnagyobb ábrázolható szám az, amiben 8 darab helyiérték van, és minden helyiértékre 1-est írtunk.
Ez a szám a 1 · 2<sup>0</sup> + 1 · 2<sup>1</sup> + 1 · 2<sup>2</sup> + 1 · 2<sup>3</sup> + 1 · 2<sup>4</sup> + 
1 · 2<sup>5</sup> + 1 · 2<sup>6</sup> + 1 · 2<sup>7</sup> összeadás eredménye, ami 255. Ha nem
szeretnénk ezt a hosszú összeget minden alkalommal kiírni, akkor használhatjuk az `11111111` formát is.

Az előző modulban szó volt a processzorban található regiszterekről. A kettes számrendszerbeli tudásunkat
felhasználva kiszámolhatjuk, hogy mi az a legnagyobb szám, amit egy átlagos processzor egy regiszterében
tárolni tudunk. Fun fact: Manapság a PC-kben és laptopokban használt processzorok 64-bites regisztereket
használnak. Ebből kiderül, hogy a legnagyobb szám, amit felírhatunk az az a szám, aminek 64 helyiértéke van,
és mindegyik helyiértéken 1-es áll. Ez a 2<sup>64</sup> - 1, ami `18 446 744 073 709 551 615`. Ez a 
legnagyobb szám, amivel a processzor egy parancsban dolgozni tud. Ez azért meglepő, mert ez egy viszonylag
véges szám. Ennek a korlátnak a feloldásában majd valamely későbbi leckében foglalkozunk.

A `byte`-ot szoktuk használni az egyes állományaink, illetve bármilyen más adat *méretének* meghatázorására
is. Egy byte-nyi adat meglepően kicsi: általában pontosan 1 darab karakter fér bele. Mivel ennél 
lényegesen nagyobb fájlok méretét is szeretnénk meghatározni, a `byte`-nál nagyobb mértékegységeket is
definiálunk:

* `b`: Ez a `bit`, a kétállapotú logikai változónk.
* `B`: Másnéven `Byte`. `1 B = 8 b`
* `KB`: Másnéven `Kilobyte`. A **mai** állás szerint `1 KB = 1000 B`
* `MB`: Másnéven `Megabyte`. A **mai** állás szerint `1 MB = 1000 KB = 1 000 000 B`
* `GB`: Másnéven `Gigabyte`. A **mai** állás szerint `1 GB = 1000 MB = 1 000 000 KB = 1 000 000 000 B`
* `TB`: Másnéven `Terabyte`. A **mai** állás szerint `1 TB = 1000 GB = 1 000 000 MB = 1 000 000 000 KB = 1 000 000 000 000 B`

Az ezres szorzó a Microsoft-nak köszönhető, mert úgy gondolták, hogy a hétköznapi ember számára könnyebben
felfogható, mint a kettő hatványos szorzó. Amit a programozók **igazából** használnak, az a következő:

* `KiB`: Másnéven `Kibibyte`. `1 KiB = 1024 B`
* `MiB`: Másnéven `Mibibyte`. `1 MiB = 1024 KiB = 1 048 576 B`
* `GiB`: Másnéven `Gibibyte`. `1 GiB = 1024 MiB = 1 048 576 KiB = 1 073 714 824 B`
* `TiB`: Másnéven `Tibibyte`. `1 TiB = 1024 GiB = 1 048 576 MiB = 1 073 714 824 KiB = 1 099 511 627 776 B`

**NAGYON FONTOS**: Oda kell figyelni a kis `i` betűre, illetve arra, hogy az adott mértékegység végén kis `b`,
vagy nagy `B` szerepel, mert egészen mást jelentenek! Hálózati sávszélesség mérésnél szokásos az egység idő alatt
áteresztett adat mennyiségét **bitekben** megadni, ahhoz, hogy levetítsük ezt az adatot byte-okra, az adott
mennyiséget el kell osztani 8-cal!