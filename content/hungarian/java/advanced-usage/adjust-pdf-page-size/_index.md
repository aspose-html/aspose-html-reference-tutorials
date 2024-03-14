---
title: Állítsa be a PDF oldalméretét az Aspose.HTML for Java segítségével
linktitle: A PDF oldalméretének beállítása
second_title: Java HTML feldolgozás Aspose.HTML-lel
description: Ismerje meg, hogyan állíthatja be a PDF oldalméretét az Aspose.HTML for Java segítségével. Hozzon létre könnyedén kiváló minőségű PDF-eket HTML-ből. Az oldalméretek hatékony szabályozása.
type: docs
weight: 15
url: /hu/java/advanced-usage/adjust-pdf-page-size/
---

mai digitális korban egyre nagyobb az igény a HTML-tartalomból kiváló minőségű PDF-ek előállítására. Az Aspose.HTML for Java egy hatékony Java-könyvtár, amely lehetővé teszi a HTML-dokumentumok könnyű konvertálását PDF formátumba. Ebben az oktatóanyagban az oldalméret beállítására összpontosítunk, amikor HTML-t PDF-be konvertálunk az Aspose.HTML for Java használatával.

## Előfeltételek

Mielőtt elkezdené, győződjön meg arról, hogy a következő előfeltételeket teljesítette:

- Java fejlesztői környezet: Győződjön meg arról, hogy a Java Development Kit (JDK) telepítve van a rendszerén.
-  Aspose.HTML for Java: Le kell töltenie és telepítenie kell az Aspose.HTML for Java programot a webhelyről[itt](https://releases.aspose.com/html/java/).
- HTML-dokumentum: Konverzióra készen kell lennie egy HTML-dokumentumnak. Ha nem, hozzon létre egyet, vagy használjon egy meglévő HTML-fájlt.

## Csomagok importálása

A kezdéshez importálnia kell a szükséges csomagokat az Aspose.HTML for Java használatához. A következő kódrészlet bemutatja, hogyan kell ezt megtenni:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Most, hogy megvannak az előfeltételek, és importálta a szükséges csomagokat, bontsuk le a PDF oldalméret beállításának folyamatát több lépésre:

## 1. lépés: HTML-tartalom olvasása

Először is el kell olvasnia a PDF-be konvertálni kívánt HTML-tartalmat. Ebben a példában a HTML-t egy "FirstFile.html" nevű fájlból fogjuk beolvasni.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## 2. lépés: HTML tartalom írása

Ezután a HTML-tartalmat egy "FirstFileOut.html" nevű fájlba írja.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Adjon hozzá egyéni HTML stílusokat vagy tartalmat itt
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## 3. lépés: HTML renderelés PDF-be

Most a HTML-tartalmat PDF-fájlként jeleníti meg. Két forgatókönyvvel foglalkozunk: az egyikben az oldalméret nincs a tartalom szélességéhez igazítva, a másikban pedig.

### Az oldal mérete nincs beállítva

Ebben a forgatókönyvben az oldal mérete rögzített szélességre és magasságra van beállítva, ami levághatja a tartalmat, ha az meghaladja ezeket a méreteket.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Hozzon létre egy HTMLDocument példányt a HTML-fájlból
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Állítsa be a PDF-megjelenítési beállításokat
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Renderje le a kimenetet
pdf_renderer.render(device, html_document);
```

### Az oldalméret a tartalom szélességéhez igazítva

Ebben az esetben az oldal mérete a tartalom szélességéhez igazodik.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Renderje le a kimenetet
pdf_renderer.render(device, html_document);
```

## Következtetés

Ebben az oktatóanyagban megvizsgáltuk, hogyan állíthatja be a PDF oldalméretét, amikor HTML-t PDF-be konvertál az Aspose.HTML for Java használatával. Megtanulta az előfeltételeket, importálta a szükséges csomagokat, és lépésről lépésre követte ezt a feladatot. Az Aspose.HTML for Java segítségével könnyedén szabályozhatja a létrehozott PDF-ek oldalméretét, így biztosítva, hogy tartalma a kívánt módon jelenjen meg.

 Nyugodtan kísérletezzen a különböző oldalméretekkel és beállításokkal, hogy megfeleljen egyedi igényeinek. Ha bármilyen problémába ütközik, vagy további kérdései vannak, ne habozzon kérni segítséget a[Aspose.HTML a Java dokumentációhoz](https://reference.aspose.com/html/java/) vagy a[Aspose támogatási fórum](https://forum.aspose.com/).

## GYIK

### 1. kérdés: Mi az Aspose.HTML for Java?

1. válasz: Az Aspose.HTML for Java egy Java-könyvtár, amely lehetővé teszi a HTML-dokumentumok kezelését, azok kezelését, konvertálását és különféle formátumokká, köztük PDF-ekké való megjelenítését.

### 2. kérdés: Hogyan állíthatom be a PDF oldalméretét, amikor HTML-t PDF-be konvertálok az Aspose.HTML for Java segítségével?

 2. válasz: A PDF-oldal méretét a gombbal állíthatja be`PageSetup` osztály és beállítás a`AdjustToWidestPage` tulajdonát`true` vagy `hamis, az Ön igényeitől függően.

### 3. kérdés: Testreszabhatom a HTML-tartalom stílusát, mielőtt PDF-be konvertálnám?

3. válasz: Igen, testreszabhatja a stílust úgy, hogy CSS- és HTML-elemeket ad hozzá a HTML-tartalomhoz, mielőtt PDF-be konvertálja, amint az az oktatóanyagban látható.

### 4. kérdés: Hol találom az Aspose.HTML for Java dokumentációját?

 V4: Olvassa el a dokumentációt[itt](https://reference.aspose.com/html/java/) átfogó információkért és példákért.

### 5. kérdés: Elérhető az Aspose.HTML for Java ingyenes próbaverziója?

 5. válasz: Igen, elérheti az Aspose.HTML for Java ingyenes próbaverzióját a webhelyről[ez a link](https://releases.aspose.com/).