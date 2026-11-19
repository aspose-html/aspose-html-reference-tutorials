---
date: 2026-08-28
description: Az XPS oldalméretének módosítása HTML XPS-re konvertálásakor Java-ban
  az Aspose.HTML használatával. Render HTML to XPS with precise dimensions.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: Az XPS Page Size módosítása
og_description: Az XPS oldalméretének módosítása HTML XPS-re konvertálásakor Java-ban
  az Aspose.HTML használatával. Learn to render HTML to XPS with precise dimensions
  in seconds.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Az XPS oldalméretének módosítása HTML XPS-re konvertálásakor Java-ban
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Az XPS oldalméretének módosítása HTML XPS-re konvertálásakor Java-ban
url: /hu/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Állítsa be az XPS oldal méretét HTML‑ről XPS‑re konvertáláskor Java‑ban

Ebben a tutorialban megtanulja, **hogyan állítsa be az XPS oldal méretét** HTML‑ről XPS‑re konvertálás közben az Aspose.HTML for Java segítségével. Akár nyomtatható számlákat, archiválási jelentéseket vagy egyedi méretű címkéket kell készítenie, az oldal méretének szabályozása garantálja, hogy a végső XPS pontosan úgy nézzen ki, ahogy szeretné. Végigvezetjük a környezet beállításán, a renderelési opciókon és a végső XPS generáláson, hogy ezt a képességet közvetlenül beépíthesse Java alkalmazásaiba.

## Gyors válaszok
- **Mi jelent a „convert HTML to XPS”?** HTML dokumentumot renderel XPS fájlba, megőrizve a elrendezést és a stílusokat.  
- **Szükségem van licencre?** A ingyenes próba verzió fejlesztéshez működik; a gyártási környezethez kereskedelmi licenc szükséges.  
- **Mely Java verzió támogatott?** Java 8 vagy újabb (JDK 11+ ajánlott).  
- **Módosíthatom az oldal méretét?** Igen – az Aspose.HTML lehetővé teszi egyedi méretek megadását a renderelés előtt.  
- **Mennyi időt vesz igénybe a konvertálás?** Általában egy másodperc alatt megy a szokásos oldalak esetén; nagyobb dokumentumok hosszabb időt vehetnek igénybe.

## Mi a HTML‑ről XPS‑re konvertálás?
A HTML‑ről XPS‑re konvertálás azt jelenti, hogy egy web‑orientált jelölőfájlt XPS (XML Paper Specification) dokumentummá alakítunk – egy rögzített elrendezésű, nyomtatásra kész formátummá, amely hasonló a PDF‑hez. Ez akkor hasznos, ha magas hűségű, eszközfüggetlen dokumentumokra van szükség archiváláshoz vagy nyomtatáshoz Java alkalmazásokból.

## Miért kell beállítani az XPS oldal méretét?
Az XPS oldal méretének beállítása lehetővé teszi a végső dokumentum fizikai méretének (pl. A4, Letter, egyedi címkék) szabályozását. Megakadályozza a nem kívánt méretezést, biztosítja, hogy a tartalom tökéletesen illeszkedjen, és csökkentheti a fájlméretet a felesleges fehér tér eltávolításával.

## Hogyan rendereljük a HTML‑t XPS‑re egyedi oldalmérettel?
Töltse be a HTML‑t, konfigurálja a `XpsRenderingOptions`‑t egy `PageSetup`‑mal, amely meghatározza a pontos szélességet és magasságot, majd rendereljen egy `XpsDevice`‑re. Ez a kétlépéses folyamat lehetővé teszi a layout megőrzését, miközben a megadott méreteket kényszeríti, mindezt egyetlen API‑hívásban.

## Előfeltételek

Mielőtt elkezdenénk, győződjön meg róla, hogy a következő előfeltételek teljesülnek:

1. **Java fejlesztői környezet** – Java Development Kit (JDK) telepítve a rendszerén.  
2. **Aspose.HTML for Java könyvtár** – Töltse le és vegye fel a projektjébe az Aspose.HTML for Java könyvtárat. A könyvtárat megtalálja a [Aspose.HTML for Java letöltési oldalon](https://releases.aspose.com/html/java/).  
3. **Bemeneti HTML fájl** – Készítsen egy HTML fájlt, amelyet renderelni és az XPS oldal méretét beállítani szeretne. A tutorialhoz saját HTML fájlt is használhat.

## Csomagok importálása

A `Page` osztály az XPS kimenet oldalméreteit és beállításait képviseli. A `HtmlRenderer` osztály végzi a HTML‑ről XPS‑re konvertálást.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Lépésről‑lépésre útmutató

Az alábbiakban egy tömör, számozott útmutatót talál, amely tükrözi az eredeti lépéseket, miközben további kontextust ad a tisztánlátáshoz.

### 1. lépés: a bemeneti fájl nevének beállítása

A `FileInputStream` osztály nyers bájtokat olvas be egy fájlból, és a HTML forrást biztosítja a renderelőnek.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### 2. lépés: HTML dokumentum létrehozása és stílusok beállítása

A `HTMLDocument` osztály egy memóriában lévő HTML DOM‑ot képvisel, amelyet az Aspose.HTML a rendereléshez használ.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### 3. lépés: XPS renderelési beállítások létrehozása

A `XpsRenderingOptions` osztály olyan beállításokat tartalmaz, amelyek szabályozzák, hogyan renderelődik a HTML XPS‑be, például oldalméret és képminőség.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### 4. lépés: az oldal méretének beállítása  

**Hogyan állítsuk be az XPS oldal méretét** – Definiáljon egy egyedi oldalméretet (szélesség × magasság pontban), és adja meg a renderelőnek, hogy automatikusan a legszélesebb oldalra bővüljön‑e. Az `adjustToWidestPage` `false` értékre állítása megőrzi a megadott pontos méreteket.

A `PageSetup` osztály határozza meg az oldal méretét, margókat és tájolást az XPS kimenethez.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### 5. lépés: a kimenet renderelése

A `XpsDevice` osztály a renderelés célpontja, amely a feldolgozott tartalmat XPS fájlba írja.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Gyakori problémák és megoldások

| Probléma | Miért fordul elő | Megoldás |
|----------|------------------|----------|
| **Üres XPS kimenet** | A bemeneti stream nincs lezárva, vagy a HTMLDocument rossz fájlra mutat. | Győződjön meg róla, hogy a `FileInputStream` megfelelően van try‑with‑resources blokkba ágyazva, és a fájl útvonala pontos. |
| **Az oldal mérete nem alkalmazódik** | `adjustToWidestPage` `true` értéken maradt. | Állítsa be a `pageSetup.setAdjustToWidestPage(false);` értéket, ahogy a 4. lépésben látható. |
| **Nem támogatott CSS** | Az Aspose.HTML csak egy részhalmazát támogatja a CSS‑nek. | Maradjon az alap elrendezésnél, betűtípusoknál és színeknél; kerülje a fejlett szelektorokat vagy a CSS Grid-et. |
| **LicenseException** | Érvényes licenc nélkül futtatás a termelésben. | Alkalmazza a temporális vagy megvásárolt licencet a renderelés előtt (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Gyakran ismételt kérdések

**Q: Mi az Aspose.HTML for Java?**  
A: Az Aspose.HTML for Java egy Java könyvtár, amely lehetővé teszi a fejlesztők számára HTML dokumentumok manipulálását és különböző formátumokba, például XPS, PDF és képek, konvertálását. A könyvtárat letöltheti a [Aspose.HTML for Java letöltési oldalról](https://releases.aspose.com/html/java/).

**Q: Hol tölthetem le az Aspose.HTML for Java‑t?**  
A: Az Aspose.HTML for Java könyvtárat a [Aspose termék kiadási oldalról](https://releases.aspose.com/) töltheti le.

**Q: Van ingyenes próba verzió az Aspose.HTML for Java‑hoz?**  
A: Igen, ingyenes próbaverziót kaphat az Aspose.HTML for Java‑hoz a [temporális licenc kérelem oldalról](https://purchase.aspose.com/temporary-license/).

**Q: Hogyan szerezhetek temporális licencet az Aspose.HTML for Java‑hoz?**  
A: Temporális licencet az Aspose.HTML for Java‑hoz a [temporális licenc kérelem oldalról](https://purchase.aspose.com/temporary-license/) szerezhet.

**Q: Kaphatok támogatást az Aspose.HTML for Java‑hoz?**  
A: Igen, segítséget és támogatást kaphat az Aspose közösségtől a [Aspose Fórumon](https://forum.aspose.com/).

**Q: Konvertálhatok HTML‑t XPS‑re fej nélküli szerveren?**  
A: Természetesen. Az Aspose.HTML működik GUI‑ nélküli környezetben; csak győződjön meg róla, hogy a Java futtatókörnyezet megfelelően van konfigurálva.

**Q: Támogatja a könyvtár az egyedi oldal margókat?**  
A: Igen. Használja a `PageSetup.setMarginTop()`, `setMarginBottom()` stb. metódusokat, mielőtt a `PageSetup`‑ot a renderelési beállításokhoz rendeli.

## Következtetés

Áttekintettük a **HTML‑ről XPS‑re konvertálás** és az **XPS oldal méretének beállítása** folyamatát az Aspose.HTML for Java segítségével. Ezeket a lépéseket követve nyomtatásra kész XPS dokumentumokat hozhat létre, amelyek pontosan megfelelnek az Ön által meghatározott elrendezési követelményeknek. Nyugodtan kísérletezzen különböző oldalméretekkel, stílusokkal, vagy akár fejlécekkel és láblécekkel, hogy a projekt igényeihez igazodjon.

Ha kérdése van vagy további segítségre van szüksége, tekintse meg az [Aspose.HTML for Java dokumentációt](https://reference.aspose.com/html/java/) vagy csatlakozzon a beszélgetéshez a [Aspose Fórumon](https://forum.aspose.com/).

---

**Legutóbb frissítve:** 2026-08-28  
**Tesztelt verzió:** Aspose.HTML for Java 24.11 (legújabb a megírás időpontjában)  
**Szerző:** Aspose

## Kapcsolódó tutorialok

- [HTML konvertálása XPS-re Aspose.HTML for Java használatával](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [PDF oldal méretének beállítása Aspose.HTML for Java használatával](/html/java/advanced-usage/adjust-pdf-page-size/)
- [EPUB konvertálása XPS-re Aspose.HTML for Java használatával](/html/java/converting-epub-to-xps/convert-epub-to-xps/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}