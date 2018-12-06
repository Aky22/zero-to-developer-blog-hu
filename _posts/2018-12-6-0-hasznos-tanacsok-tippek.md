---
title: "0. Hasznos tanácsok, tippek"
---

A tananyag során előfordul majd, hogy bizonyos fejlesztőeszközöket le kell tölteni. Feltételezem,
hogy a tutorial-t Windows operációs rendszeren szeretnéd végigcsinálni, így itt egy pár hasznos
jótanács, hogy elkerüld a szélütést:

* A Windows nagyon szereti a `C:\Program Files (x86)` mappába telepíteni a letöltött alkalmazásokat.
Ez **nagyon rossz**, ugyanis a legtöbb multiplatform szoftver (ami fut több operációs rendszeren is)
nem szereti, ha az elérési útvonalában speciális karakterek, vagy szóközök találhatóak. Így azt
javaslom, hogy minden, a programozáshoz használatos eszközt a `C:\` gyökérkönyvtárba, esetleg azon
belül egy `DEVTOOLS` (azaz `C:\DEVTOOLS`) könyvtárba telepíts. Minden program a saját könyvtárába
megy ezen belül, aminek olyan a neve, hogy csak nagybetűket tartalmaz, és az aláhúzáson kívül ("_" 
karakter) nem tartalmaz speciális karaktereket (például a Python nevű programozási nyelv környezetét
a `C:\DEVTOOLS\PYTHON` mappába érdemes telepíteni)