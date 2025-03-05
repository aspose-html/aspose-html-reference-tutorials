---
title: Alkalmazzon külső CSS-t a HTML-dokumentumokra az Aspose.HTML for Java-ban
linktitle: Alkalmazzon külső CSS-t a HTML-dokumentumokra az Aspose.HTML for Java-ban
second_title: Java HTML feldolgozás Aspose.HTML-lel
description: Fedezze fel, hogyan alkalmazhat külső CSS-t HTML-dokumentumokra az Aspose.HTML for Java használatával! Kövesse ezt a lépésről lépésre szóló útmutatót a teljes oktatóanyaghoz.
type: docs
weight: 12
url: /hu/java/editing-html-documents/apply-external-css-html-documents/
---
## Bevezetés
Amikor HTML-dokumentumokkal dolgozik, a stílusok alkalmazása jelentősen megváltoztathatja a megjelenítést és a felhasználói élményt. Ha belemerül a Java-ba, és szeretné megtanulni, hogyan alkalmazhat külső CSS-stílusokat HTML-dokumentumaira az Aspose.HTML könyvtár segítségével, akkor jó helyen jár! Ennek az útmutatónak a célja, hogy lépésről lépésre megvilágítsa a folyamatot, megkönnyítve ezzel még azok számára is, akik még nem ismerik a Java-t vagy a CSS-t.
## Előfeltételek
Mielőtt belemerülne a kódba, néhány dolgot meg kell határoznia:
### 1. Java fejlesztőkészlet (JDK)
 Győződjön meg arról, hogy a JDK telepítve van a gépen. A legújabb verziót innen töltheti le[Az Oracle Java webhelye](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML for Java
Be kell állítania az Aspose.HTML for Java fájlt. Ha még nem tetted meg, menj a[Aspose letöltési oldal](https://releases.aspose.com/html/java/) és megragad a könyvtárat.
### 3. IDE vagy szövegszerkesztő
Java kódjának megírásához válasszon integrált fejlesztőkörnyezetet (IDE), például IntelliJ IDEA-t, Eclipse-t, vagy akár egy egyszerű szövegszerkesztőt.
### 4. Java alapismeretek
A Java programozás és a CSS alapjainak ismerete minden bizonnyal segít a kényelmesebb követésben.
## Csomagok importálása
Miután mindent beállított, a következő lépés a szükséges csomagok importálása a Java projektbe. Íme, amire szüksége van:
```java
import com.aspose.html.HTMLDocument;
```
Ezekkel az importálásokkal kezelheti a HTML-dokumentumokat, és különböző formátumokba, például PDF-be renderelheti őket.

Az oktatóanyagot kezelhető lépésekre bontjuk. Minden lépés végigvezeti Önt a külső CSS-stílusok HTML-dokumentumra történő alkalmazásán az Aspose.HTML for Java használatával.
## 1. lépés: Hozzon létre egy HTML-dokumentumot
Először is létre kell hoznunk a HTML dokumentumunkat. Kezdjük azzal, hogy meghatározzuk a tartalmat egy egyszerű HTML-struktúra segítségével.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Itt egy alapvető HTML-struktúrát határoztunk meg, beleértve a`<div>` két bekezdéssel. A`HTMLDocument` osztályt használjuk HTML-tartalmunk dokumentumábrázolásának létrehozására.
## 2. lépés: Hozzon létre egy stíluselemet
 Ezután létrehozzuk a`style` elemet a CSS-szabályaink megtartásához.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 A`createElement` módszere`HTMLDocument` , létrehozunk egy új`<style>` elemet, és állítsa be a tartalmát úgy, hogy tartalmazza a CSS-definícióinkat két osztályhoz:`frame1` és`frame2`. Ezek az osztályok határozzák meg a margókat, a kitöltést, a méreteket, a háttérszíneket, a betűtípuscsaládokat és a szövegszíneket.
## 3. lépés: Adja hozzá a stílust a dokumentum fejlécéhez
Most, hogy a CSS a helyén van, hozzá kell fűznünk a stíluselemünket a dokumentum fejéhez.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Lekérjük a dokumentum fejét, és hozzáfűzzük az újonnan létrehozott fájlunkat`style` elem. Ez a művelet hatékonyan integrálja a CSS-t a HTML-dokumentumba, lehetővé téve a HTML-tartalom stílusának kialakítását.
## 4. lépés: Osztályok alkalmazása HTML-elemekre
Ezután a korábban meghatározott CSS-osztályokat alkalmazzuk bekezdéselemeinkre.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Itt elérjük a dokumentum első és utolsó bekezdésének elemeit, és hozzárendeljük az általunk létrehozott CSS-osztályokat. Ez a hozzárendelés biztosítja, hogy megfeleljenek a CSS-ben meghatározott stílusoknak.
## 5. lépés: Állítsa be a további stílustulajdonságokat
A megjelenés további javítása érdekében további stílustulajdonságokat állítunk be bekezdéseinkhez.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

Ebben a lépésben stílusainkat finomhangoljuk. Az első bekezdés betűmérete meg van növelve és középre igazítva, míg az utolsó bekezdés színe, betűmérete és betűcsaládja meg van határozva. Ez a finomítás döntő fontosságú az olvashatóság és az esztétikai vonzerő szempontjából.
## 6. lépés: Mentse el a HTML-dokumentumot
Miután alkalmaztuk a stílusainkat, ideje elmenteni a HTML-dokumentumot.
```java
document.save("edit-internal-css.html");
```

 Itt használjuk a`save` módszere a`HTMLDocument` osztályt, hogy a módosított HTML tartalmat fájlba írjuk, így megőrizzük stílusainkat és változtatásainkat.
## 7. lépés: Rendelje le a dokumentumot PDF formátumban
Végül rendereljük a dokumentumot PDF formátumba a kimenethez.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 A`PdfDevice` osztályban beállítjuk HTML-dokumentumunk PDF-be való megjelenítését. Ez a lépés kulcsfontosságú, ha a stílusos dokumentumot univerzálisan elérhető formátumban szeretné megosztani.
## Következtetés
És kész – a külső CSS alkalmazása HTML-dokumentumokra az Aspose.HTML for Java használatával egyszerű és kifizetődő! Néhány sornyi kóddal az egyszerű szöveget tetszetős és professzionális stílusú dokumentumokká alakíthatja. Tehát akár személyes használatra tervez, akár jelentéseket készít, akár webes tartalmat fejleszt, a HTML és a CSS Java nyelven történő kezelésének megértése hatalmas készség az eszköztárban.
## GYIK
### Mi az Aspose.HTML for Java?
Az Aspose.HTML for Java egy hatékony könyvtár, amely lehetővé teszi a fejlesztők számára, hogy HTML-dokumentumokkal dolgozzanak Java-alkalmazásokban, és a szolgáltatások széles skáláját kínálja a HTML-kezeléstől a renderelésig.
### Szükségem van internetkapcsolatra az Aspose.HTML használatához?
Nem, miután letöltötte a szükséges könyvtárfájlokat, offline is használhatja az Aspose.HTML-t.
### Alkalmazhatok több CSS-fájlt egy HTML-dokumentumra?
 Igen, létrehozhat többször is`<link>` elemeket, és fűzze őket a dokumentum fejéhez különböző CSS-fájlokhoz.
### Van különbség a belső és a külső CSS között?
Igen! A belső CSS-t egy HTML-dokumentumban határozzák meg, míg a külső CSS-t egy külön fájlba helyezik, és a dokumentumhoz kapcsolják.
### Hogyan kaphatok támogatást az Aspose.HTML for Java számára?
 A közösségi támogatást a következőn keresztül érheti el[Aspose fórum](https://forum.aspose.com/c/html/29) bármilyen kérdéssel vagy problémával kapcsolatban.