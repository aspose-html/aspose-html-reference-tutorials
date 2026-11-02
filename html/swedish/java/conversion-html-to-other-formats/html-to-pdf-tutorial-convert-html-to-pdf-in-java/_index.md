---
category: general
date: 2026-06-19
description: Lär dig hur du genererar PDF från HTML med ett enkelt Java‑exempel. Denna
  HTML‑till‑PDF‑handledning visar hur du konverterar en HTML‑fil till PDF med OpenHTMLtoPDF.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: sv
og_description: html till pdf-handledning visar dig hur du genererar PDF från HTML
  med Java. Följ stegen för att snabbt konvertera en HTML‑fil till PDF.
og_title: 'HTML till PDF-handledning: Java‑konverteringsguide'
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
title: 'html till pdf handledning: Konvertera HTML till PDF i Java'
url: /sv/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf tutorial – Gör om en HTML‑sida till en PDF med Java

Har du någonsin undrat hur man gör om en statisk HTML‑sida till ett elegant PDF‑dokument utan att lämna din IDE? Du är inte ensam. I den här **html to pdf tutorial** går vi igenom ett komplett, färdigt‑att‑köra Java‑exempel som **generate pdf from html** på bara några minuter.

Vi kommer att gå igenom allt du behöver—projektuppsättning, lägga till rätt bibliotek, skriva konverteringskoden, och till och med ett snabbt tips för att konvertera en live‑webbsida till PDF. I slutet kommer du att kunna **convert html file pdf** på din egen maskin, och du kommer att förstå hur man **create pdf from html** för alla framtida projekt.

## Vad du behöver

- Java 17 eller nyare (koden fungerar med vilken recent JDK som helst)
- Maven eller Gradle (vi visar Maven‑exemplet)
- En liten HTML‑fil som du vill göra om till en PDF (vi skapar en på flygande fot)
- En IDE eller en enkel textredigerare—du bestämmer

Det är allt. Inga tunga servrar, inga betalda SDK:er, bara ren Java och ett gratis open‑source‑bibliotek.

## Steg 1: html to pdf tutorial – Ställ in ett Maven‑projekt

Först och främst. Skapa ett nytt Maven‑projekt (eller lägg till i ett befintligt). Det enda beroendet du verkligen behöver är **OpenHTMLtoPDF**, som sköter det tunga arbetet med att rendera HTML och CSS till en PDF.

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

> **Pro tip:** Om du använder Gradle kan samma beroenden läggas till under `implementation` i `build.gradle`.  

Varför detta steg är viktigt: utan biblioteket har JVM:n ingen aning om hur man översätter HTML‑taggar till PDF‑ritkommandon. OpenHTMLtoPDF är lättviktigt, aktivt underhållet och fungerar med CSS‑2.1, så din styling förblir intakt.

## Steg 2: generate pdf from html – Förbered en exempel‑HTML‑fil

Låt oss skapa en liten `input.html` precis bredvid vår Java‑källa. Detta håller exemplet självständigt och demonstrerar **create pdf from html**‑arbetsflödet.

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

Du kan ersätta innehållet med vad som helst—tabeller, bilder, till och med JavaScript (även om renderaren ignorerar skript). Det viktiga är att filen finns på classpath så att konverteraren kan hitta den.

## Steg 3: convert html file pdf – Skriv konverteringsverktyget

Nu hjärtat i **html to pdf tutorial**: en liten `HtmlToPdfConverter`‑klass som läser HTML och skriver en PDF. Koden nedan är ett komplett, körbart exempel; kopiera‑klistra in den i `src/main/java/com/example/HtmlToPdfConverter.java`.

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

### Varför den här koden fungerar

1. **Resource flexibility** – metoden kontrollerar först om den angivna sökvägen pekar på en riktig fil; om inte, faller den tillbaka på en classpath‑resurs. Det betyder att du kan **convert webpage to pdf** senare genom att mata in en URL‑sträng (byt bara `withHtmlContent`‑anropet mot `withUri`).
2. **Automatic directory creation** – `Files.createDirectories` garanterar att `target/`‑mappen finns, så du får inte ett “No such file or directory”-fel.
3. **Single‑line conversion** – `PdfRendererBuilder` hanterar CSS, typsnitt och sidlayout internt. Ingen behov av att manuellt hantera PDF‑sidor; biblioteket gör det åt dig, vilket håller exemplet kort och fokuserat på konceptet **convert html file pdf**.

## Steg 4: create pdf from html – Kör programmet och verifiera

Öppna en terminal i projektets rot och kör:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Om allt är korrekt konfigurerat kommer du att se:

```
✅ PDF successfully created at target/output.pdf
```

Öppna `target/output.pdf` med någon PDF‑visare. Du bör se den stylade “Monthly Sales Report”-rubriken, paragraftexten, och samma marginaler som du definierade i HTML‑`<style>`‑blocket.

> **Vad händer om du inte ser stilen?**  
> Se till att CSS är inline eller ligger i samma mapp som HTML‑filen. OpenHTMLtoPDF löser relativa URL:er baserat på den bas‑URI du skickar till `withHtmlContent`. I snippet‑exemplet ovan skickade vi `null`, vilket fungerar för enkel inline‑CSS. För externa stilmallar, ange katalogsökvägen som det andra argumentet.

## Steg 5: convert webpage to pdf – Hantera fjärr‑URL:er (valfritt)

Ibland behöver du **convert webpage to pdf** direkt från internet—tänk på att arkivera ett online‑kvitto. Biblioteket stödjer detta via `withUri`. Här är en snabb anpassning:

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



## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man konverterar HTML till PDF Java – med Aspose.HTML för Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Konvertera HTML till PDF Java – Konfigurera miljö i Aspose.HTML](/html/english/java/configuring-environment/)
- [Konvertera HTML till PDF i Java – Steg‑för‑steg‑guide med sidstorleksinställningar](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}