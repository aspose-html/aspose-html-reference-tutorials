---
category: general
date: 2026-06-19
description: Leer hoe je PDF genereert vanuit HTML met een eenvoudig Java‑voorbeeld.
  Deze HTML‑naar‑PDF‑tutorial laat zien hoe je een HTML‑bestand naar PDF converteert
  met OpenHTMLtoPDF.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: nl
og_description: html-naar-pdf‑tutorial laat zien hoe je PDF genereert vanuit HTML
  met Java. Volg de stappen om een HTML‑bestand snel naar PDF te converteren.
og_title: 'HTML naar PDF tutorial: Java-conversiegids'
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
title: 'HTML naar PDF‑tutorial: Converteer HTML naar PDF in Java'
url: /nl/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf tutorial – Zet een HTML-pagina om in een PDF met Java

Heb je je ooit afgevraagd hoe je een statische HTML-pagina kunt omzetten naar een strak PDF-document zonder je IDE te verlaten? Je bent niet de enige. In deze **html to pdf tutorial** lopen we een compleet, kant‑klaar Java‑voorbeeld door dat **generate pdf from html** in slechts een paar minuten.

We behandelen alles wat je nodig hebt—projectopzet, het toevoegen van de juiste bibliotheek, het schrijven van de conversiecode, en zelfs een snelle tip voor het omzetten van een live webpagina naar PDF. Aan het einde kun je **convert html file pdf** op je eigen machine, en begrijp je hoe je **create pdf from html** voor elk toekomstig project kunt maken.

## Wat je nodig hebt

- Java 17 of nieuwer (de code werkt met elke recente JDK)
- Maven of Gradle (we laten het Maven‑fragment zien)
- Een klein HTML‑bestand dat je wilt omzetten naar een PDF (we maken er één ter plekke)
- Een IDE of een eenvoudige teksteditor—jouw keuze

Dat is alles. Geen zware servers, geen betaalde SDK's, alleen pure Java en een gratis open‑source bibliotheek.

## Stap 1: html to pdf tutorial – Een Maven‑project opzetten

Allereerst. Maak een nieuw Maven‑project aan (of voeg toe aan een bestaand project). De enige afhankelijkheid die je echt nodig hebt is **OpenHTMLtoPDF**, die het zware werk doet van het renderen van HTML en CSS naar een PDF.

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

> **Pro tip:** Als je Gradle gebruikt, kunnen dezelfde afhankelijkheden worden toegevoegd onder `implementation` in `build.gradle`.  

Waarom deze stap belangrijk is: zonder de bibliotheek heeft de JVM geen idee hoe HTML‑tags om te zetten naar PDF‑tekenopdrachten. OpenHTMLtoPDF is lichtgewicht, actief onderhouden, en werkt met CSS‑2.1, zodat je opmaak behouden blijft.

## Stap 2: generate pdf from html – Een voorbeeld‑HTML‑bestand voorbereiden

Laten we een klein `input.html` maken direct naast onze Java‑bron. Dit houdt het voorbeeld zelf‑voorzienend en demonstreert de **create pdf from html** workflow.

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

Je kunt de inhoud vervangen door alles—tabellen, afbeeldingen, zelfs JavaScript (hoewel de renderer scripts negeert). Het belangrijke is dat het bestand op de classpath staat zodat de converter het kan vinden.

## Stap 3: convert html file pdf – Schrijf de conversie‑utility

Nu het hart van de **html to pdf tutorial**: een kleine `HtmlToPdfConverter`‑klasse die de HTML leest en een PDF schrijft. De onderstaande code is een volledig, uitvoerbaar voorbeeld; kopieer‑en‑plak het naar `src/main/java/com/example/HtmlToPdfConverter.java`.

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

### Waarom deze code werkt

1. **Resource flexibility** – de methode controleert eerst of het opgegeven pad naar een echt bestand wijst; zo niet, dan valt hij terug op een classpath‑resource. Dat betekent dat je later **convert webpage to pdf** kunt doen door een URL‑string te gebruiken (vervang simpelweg de `withHtmlContent`‑aanroep door `withUri`).

2. **Automatic directory creation** – `Files.createDirectories` zorgt ervoor dat de map `target/` bestaat, zodat je geen “No such file or directory”‑fout krijgt.

3. **Single‑line conversion** – `PdfRendererBuilder` verwerkt CSS, lettertypen en paginalay-out intern. Geen noodzaak om PDF‑pagina's handmatig te beheren; de bibliotheek doet het voor je, waardoor het voorbeeld kort blijft en zich richt op het **convert html file pdf** concept.

## Stap 4: create pdf from html – Voer het programma uit en controleer

Open een terminal in de project‑root en voer uit:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Als alles correct is ingesteld zie je:

```
✅ PDF successfully created at target/output.pdf
```

Open `target/output.pdf` met een PDF‑viewer. Je zou de gestylede “Monthly Sales Report”‑kop, de alinea‑tekst, en dezelfde marges die je in het HTML `<style>`‑blok hebt gedefinieerd, moeten zien.

> **Wat als je de opmaak niet ziet?**  
> Zorg ervoor dat de CSS inline is of zich in dezelfde map als de HTML bevindt. OpenHTMLtoPDF lost relatieve URL's op op basis van de base‑URI die je doorgeeft aan `withHtmlContent`. In het bovenstaande fragment hebben we `null` doorgegeven, wat werkt voor eenvoudige inline CSS. Voor externe stylesheets, geef het map‑pad op als tweede argument.

## Stap 5: convert webpage to pdf – Afhandelen van externe URL's (optioneel)

Soms moet je **convert webpage to pdf** direct vanaf het internet—denk aan het archiveren van een online bon. De bibliotheek ondersteunt dit via `withUri`. Hier is een snelle aanpassing:

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

Roep het aan als:



## Wat je hierna moet leren

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe HTML naar PDF te converteren in Java – Met Aspose.HTML voor Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [HTML naar PDF converteren in Java – Omgeving configureren in Aspose.HTML](/html/english/java/configuring-environment/)
- [HTML naar PDF converteren in Java – Stapsgewijze gids met paginagrootte‑instellingen](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}