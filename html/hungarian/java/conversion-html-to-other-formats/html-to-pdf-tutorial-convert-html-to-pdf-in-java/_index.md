---
category: general
date: 2026-06-19
description: Tanulja meg, hogyan generáljon PDF-et HTML-ből egy egyszerű Java példával.
  Ez az HTML‑PDF oktató bemutatja, hogyan konvertálhat HTML fájlt PDF‑be az OpenHTMLtoPDF
  segítségével.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: hu
og_description: Az html to pdf útmutató megmutatja, hogyan lehet PDF-et generálni
  HTML-ből Java használatával. Kövesd a lépéseket, hogy gyorsan konvertáld az HTML
  fájlt PDF-be.
og_title: 'HTML‑PDF útmutató: Java konverziós útmutató'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'HTML to PDF útmutató: HTML konvertálása PDF‑be Java‑ban'
url: /hu/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf tutorial – HTML oldal PDF‑vé alakítása Java‑val

Gondolkodtál már azon, hogyan lehet egy statikus HTML oldalt egy elegáns PDF dokumentummá alakítani anélkül, hogy elhagynád az IDE‑det? Nem vagy egyedül. Ebben a **html to pdf tutorial**‑ban végigvezetünk egy teljes, azonnal futtatható Java példán, amely **generate pdf from html** néhány perc alatt.

Mindent lefedünk, amire szükséged van – projekt beállítása, a megfelelő könyvtár hozzáadása, a konverziós kód írása, és még egy gyors tippet is a élő weboldal PDF‑vé alakításához. A végére képes leszel **convert html file pdf** a saját gépeden, és megérted, hogyan **create pdf from html** bármely jövőbeli projekthez.

## Amire szükséged lesz

- Java 17 vagy újabb (a kód bármely friss JDK‑val működik)
- Maven vagy Gradle (a Maven példát mutatjuk)
- Egy apró HTML fájl, amelyet PDF‑vé szeretnél alakítani (a futás közben létrehozzuk)
- Egy IDE vagy egyszerű szövegszerkesztő – a döntés a tiéd

Ennyi. Nincs nehéz szerver, nincs fizetős SDK, csak tiszta Java és egy ingyenes nyílt forráskódú könyvtár.

## 1. lépés: html to pdf tutorial – Maven projekt beállítása

Először is. Hozz létre egy új Maven projektet (vagy adj hozzá egy meglévőhöz). Az egyetlen függőség, amire valóban szükséged van, a **OpenHTMLtoPDF**, amely elvégzi a HTML és CSS PDF‑be renderelésének nehéz munkáját.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Ha Gradlet használsz, ugyanazok a függőségek hozzáadhatók a `implementation` alatt a `build.gradle`‑ban.  

Miért fontos ez a lépés: a könyvtár nélkül a JVM-nek fogalma sincs, hogyan fordítsa le a HTML címkéket PDF rajzolási parancsokká. Az OpenHTMLtoPDF könnyű, aktívan karbantartott, és a CSS‑2.1‑et támogatja, így a stílusod változatlan marad.

## 2. lépés: generate pdf from html – Minta HTML fájl előkészítése

Hozzunk létre egy apró `input.html` fájlt közvetlenül a Java forrásunk mellett. Ez önálló példát biztosít, és bemutatja a **create pdf from html** munkafolyamatot.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

A tartalmat bármi mással helyettesítheted – táblázatok, képek, akár JavaScript (bár a renderelő figyelmen kívül hagyja a szkripteket). A lényeg, hogy a fájl a classpath‑on legyen, hogy a konverter megtalálja.

## 3. lépés: convert html file pdf – Konverziós segédprogram írása

Most jön a **html to pdf tutorial** szíve: egy apró `HtmlToPdfConverter` osztály, amely beolvassa a HTML‑t és PDF‑et ír ki. Az alábbi kód egy teljes, futtatható példa; másold be a `src/main/java/com/example/HtmlToPdfConverter.java` fájlba.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Miért működik ez a kód

1. **Resource flexibility** – a metódus először ellenőrzi, hogy a megadott útvonal valódi fájlra mutat-e; ha nem, visszaesik egy classpath erőforrásra. Ez azt jelenti, hogy később **convert webpage to pdf** is elvégezhető egy URL karakterlánc megadásával (csak cseréld le a `withHtmlContent` hívást `withUri`‑ra).

2. **Automatic directory creation** – a `Files.createDirectories` garantálja, hogy a `target/` mappa létezik, így nem kapsz „No such file or directory” hibát.

3. **Single‑line conversion** – a `PdfRendererBuilder` belsőleg kezeli a CSS‑t, betűtípusokat és az oldalelrendezést. Nincs szükség a PDF oldalak kézi kezelésére; a könyvtár megteszi helyetted, így a példa rövid és a **convert html file pdf** koncepcióra fókuszál.

## 4. lépés: create pdf from html – Program futtatása és ellenőrzés

Nyiss egy terminált a projekt gyökerében és futtasd:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Ha minden helyesen van beállítva, a következőt fogod látni:

```
✅ PDF successfully created at target/output.pdf
```

Nyisd meg a `target/output.pdf` fájlt bármely PDF‑nézővel. Látnod kell a stílusos „Monthly Sales Report” fejlécet, a bekezdés szövegét, és ugyanazokat a margókat, amelyeket az HTML `<style>` blokkban definiáltál.

> **Mi van, ha nem látod a stílusokat?**  
> Győződj meg arról, hogy a CSS inline vagy ugyanabban a mappában van, mint az HTML. Az OpenHTMLtoPDF a relatív URL‑eket a `withHtmlContent`‑nek átadott alap‑URI alapján oldja fel. A fenti példában `null`‑t adtunk meg, ami egyszerű inline CSS‑hez működik. Külső stíluslapok esetén add meg a könyvtár útvonalát második argumentumként.

## 5. lépés: convert webpage to pdf – Távoli URL‑ek kezelése (opcionális)

Néha közvetlenül az internetről kell **convert webpage to pdf** – például egy online nyugta archiválásához. A könyvtár ezt a `withUri`‑val támogatja. Íme egy gyors adaptáció:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Call it like:



## Mit tanulj meg legközelebb?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan konvertáljunk HTML‑t PDF‑vé Java‑ban – Aspose.HTML for Java használata](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [HTML PDF‑vé konvertálása Java‑ban – Környezet beállítása az Aspose.HTML‑ben](/html/english/java/configuring-environment/)
- [HTML PDF‑vé konvertálása Java‑ban – Lépésről‑lépésre útmutató oldalméret beállításokkal](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}