---
category: general
date: 2026-10-02
description: Maak pdf van html in Java met één enkele oproep. Deze tutorial laat zien
  hoe je html naar pdf converteert, opties configureert en veelvoorkomende problemen
  afhandelt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- how to convert html to pdf
- html to pdf conversion java
- convert html file to pdf
language: nl
lastmod: 2026-10-02
og_description: Maak pdf van html in Java met HtmlConverter. Volg deze volledige gids
  om html naar pdf te converteren, opties in te stellen en valkuilen te vermijden.
og_image_alt: Diagram showing create pdf from html process in Java
og_title: PDF maken van HTML in Java – snelle, betrouwbare conversie
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Create pdf from html in Java with a single call. This tutorial shows
    how to convert html to pdf, configure options, and handle common issues.
  headline: How to create pdf from html in Java – step‑by‑step guide
  type: TechArticle
- description: Create pdf from html in Java with a single call. This tutorial shows
    how to convert html to pdf, configure options, and handle common issues.
  name: How to create pdf from html in Java – step‑by‑step guide
  steps:
  - name: Why this approach works
    text: '* **Single responsibility** – the `convertHtmlToPdf` method isolates the
      conversion logic, making the code easy to test. * **Resource safety** – `try‑with‑resources`
      guarantees that the `PDDocument` is closed, preventing file‑handle leaks. *
      **Flexibility** – you can swap `HtmlRenderer` for another '
  - name: 1️⃣ Specify the source HTML file and the target PDF file
    text: '```java private static final String INPUT_PATH = "YOUR_DIRECTORY/input.html";
      private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf"; ``` *Replace
      `YOUR_DIRECTORY` with an absolute or relative path that your Java process can
      read/write.*'
  - name: 2️⃣ Load the HTML content
    text: '```java String html = Files.readString(Path.of(INPUT_PATH)); ``` Reading
      the file as a `String` preserves the original markup and makes it easy to feed
      the converter. The method assumes UTF‑8; if your HTML uses a different charset,
      use `Files.readAllBytes` and decode accordingly.'
  - name: 3️⃣ Convert the HTML document to PDF
    text: '```java byte[] pdfBytes = convertHtmlToPdf(html); ``` `convertHtmlToPdf`
      encapsulates **how to convert html to pdf**. Inside, `HtmlRenderer` parses the
      markup, applies CSS, and draws the result onto a PDF page. This is the heart
      of the **html to pdf conversion java** process.'
  - name: 4️⃣ Write the PDF file
    text: '```java Files.write(Path.of(OUTPUT_PATH), pdfBytes, StandardOpenOption.CREATE,
      StandardOpenOption.TRUNCATE_EXISTING); ``` The `Files.write` call creates the
      output file if it does not exist, or overwrites it otherwise. The method throws
      `IOException` if the directory is missing or the process lacks '
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: Hoe maak je een PDF van HTML in Java – stapsgewijze handleiding
url: /nl/java/conversion-html-to-other-formats/how-to-create-pdf-from-html-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe pdf van html te maken in Java – stapsgewijze gids

Als je **pdf van html moet maken** in een Java‑applicatie, laat deze gids je een complete, kant‑klaar oplossing zien. Je ziet hoe je **html naar pdf kunt converteren** met één methode‑aanroep, de conversie kunt configureren en typische randgevallen kunt afhandelen.

We behandelen alles wat je moet weten: vereiste afhankelijkheden, een volledig bronbestand en tips voor probleemoplossing. Aan het einde kun je **html‑bestand naar pdf converteren** betrouwbaar in elk Java‑project.

## Vereisten

* JDK 17 of nieuwer geïnstalleerd  
* Maven 3.8+ (of Gradle) om afhankelijkheden te beheren  
* Basiskennis van Java I/O  

Het voorbeeld gebruikt de open‑source **HtmlConverter**‑klasse uit de *pdfbox‑layout*‑bibliotheek, die Apache PDFBox omsluit voor HTML‑rendering. Als je een andere bibliotheek verkiest, zijn dezelfde stappen van toepassing — pas gewoon de import‑verklaringen aan.

## Voeg de vereiste afhankelijkheid toe

Voeg de volgende Maven‑coördinaten toe aan je `pom.xml`. Hiermee worden PDFBox en de HTML‑naar‑PDF‑helper opgehaald.

```xml
<dependency>
    <groupId>org.apache.pdfbox</groupId>
    <artifactId>pdfbox</artifactId>
    <version>3.0.2</version>
</dependency>
<dependency>
    <groupId>com.github.jhonnymertz</groupId>
    <artifactId>pdfbox-layout</artifactId>
    <version>1.0.0</version>
</dependency>
```

Als je Gradle gebruikt, is het equivalent:

```gradle
implementation "org.apache.pdfbox:pdfbox:3.0.2"
implementation "com.github.jhonnymertz:pdfbox-layout:1.0.0"
```

> **Pro tip:** Houd je afhankelijkheden up‑to‑date; nieuwere versies verhelpen render‑bugs en voegen CSS‑ondersteuning toe.

## Maak pdf van html – algemeen werkproces

De conversie bestaat uit drie logische stappen:

1. **Lees het bron‑HTML‑bestand** – zorg ervoor dat het pad correct is en het bestand UTF‑8 gecodeerd is.  
2. **Roep de converter aan** – de bibliotheek parseert de HTML, past CSS toe en genereert een PDF‑document.  
3. **Schrijf de PDF naar schijf** – behandel I/O‑exceptions en bevestig dat het bestand is aangemaakt.

Hieronder staat een volledige, zelfstandige Java‑klasse die dit werkproces implementeert.

```java
package com.example.pdfconverter;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

import org.apache.pdfbox.pdmodel.PDDocument;
import org.apache.pdfbox.pdmodel.PDPage;
import org.apache.pdfbox.pdmodel.PDPageContentStream;
import org.apache.pdfbox.pdmodel.common.PDRectangle;
import org.apache.pdfbox.layout.Document;
import org.apache.pdfbox.layout.element.Paragraph;
import org.apache.pdfbox.layout.renderer.HtmlRenderer;

/**
 * Simple utility that demonstrates how to create pdf from html in Java.
 *
 * The class reads an HTML file, converts it to PDF, and saves the result.
 * It uses Apache PDFBox together with the pdfbox‑layout HtmlRenderer.
 *
 * Adjust INPUT_PATH and OUTPUT_PATH to match your environment.
 */
public class HtmlToPdfConverter {

    // --------------------------------------------------------------------
    // 1️⃣  Define input and output locations
    // --------------------------------------------------------------------
    private static final String INPUT_PATH  = "YOUR_DIRECTORY/input.html";
    private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf";

    public static void main(String[] args) {
        try {
            // --------------------------------------------------------------
            // 2️⃣  Load the HTML content (UTF‑8 is assumed)
            // --------------------------------------------------------------
            String html = Files.readString(Path.of(INPUT_PATH));

            // --------------------------------------------------------------
            // 3️⃣  Perform the conversion
            // --------------------------------------------------------------
            byte[] pdfBytes = convertHtmlToPdf(html);

            // --------------------------------------------------------------
            // 4️⃣  Write the PDF file to disk
            // --------------------------------------------------------------
            Files.write(Path.of(OUTPUT_PATH), pdfBytes,
                    StandardOpenOption.CREATE,
                    StandardOpenOption.TRUNCATE_EXISTING);

            System.out.println("✅ PDF created successfully at " + OUTPUT_PATH);
        } catch (IOException e) {
            System.err.println("❌ Failed to convert HTML to PDF: " + e.getMessage());
            e.printStackTrace();
        }
    }

    /**
     * Core conversion logic.
     *
     * @param html the raw HTML string
     * @return a byte array containing the generated PDF
     * @throws IOException if PDF generation fails
     */
    private static byte[] convertHtmlToPdf(String html) throws IOException {
        // Create a new PDFBox document – this is the container for the output.
        try (PDDocument pdDocument = new PDDocument()) {

            // The HtmlRenderer parses the HTML and draws it onto a PDF page.
            HtmlRenderer renderer = new HtmlRenderer(pdDocument);
            renderer.renderHtml(html);

            // Save the document into a byte array so we can write it later.
            return toByteArray(pdDocument);
        }
    }

    /**
     * Helper that converts a PDDocument into a byte array.
     *
     * @param document the populated PDFBox document
     * @return PDF content as a byte array
     * @throws IOException if writing fails
     */
    private static byte[] toByteArray(PDDocument document) throws IOException {
        try (java.io.ByteArrayOutputStream out = new java.io.ByteArrayOutputStream()) {
            document.save(out);
            return out.toByteArray();
        }
    }
}
```

### Waarom deze aanpak werkt

* **Enkele verantwoordelijkheid** – de `convertHtmlToPdf`‑methode isoleert de conversielogica, waardoor de code makkelijk te testen is.  
* **Resource‑veiligheid** – `try‑with‑resources` garandeert dat de `PDDocument` wordt gesloten, waardoor lekken van bestands‑handles worden voorkomen.  
* **Flexibiliteit** – je kunt `HtmlRenderer` vervangen door een andere implementatie (bijv. *OpenHTMLtoPDF*) zonder de omliggende I/O‑code aan te passen, wat nuttig is wanneer je **html to pdf conversion java** nodig hebt die geavanceerde CSS ondersteunt.

## Stap‑voor‑stap uitleg

### 1️⃣ Specify the source HTML file and the target PDF file
```java
private static final String INPUT_PATH  = "YOUR_DIRECTORY/input.html";
private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf";
```
*Vervang `YOUR_DIRECTORY` door een absoluut of relatief pad dat je Java‑proces kan lezen/schrijven.*

### 2️⃣ Load the HTML content
```java
String html = Files.readString(Path.of(INPUT_PATH));
```
Het lezen van het bestand als een `String` behoudt de oorspronkelijke markup en maakt het eenvoudig om de converter te voeden. De methode gaat uit van UTF‑8; als je HTML een andere tekenset gebruikt, gebruik dan `Files.readAllBytes` en decodeer dienovereenkomstig.

### 3️⃣ Convert the HTML document to PDF
```java
byte[] pdfBytes = convertHtmlToPdf(html);
```
`convertHtmlToPdf` omvat **hoe html naar pdf te converteren**. Binnenin parseert `HtmlRenderer` de markup, past CSS toe en tekent het resultaat op een PDF‑pagina. Dit is het hart van het **html to pdf conversion java**‑proces.

### 4️⃣ Write the PDF file
```java
Files.write(Path.of(OUTPUT_PATH), pdfBytes,
        StandardOpenOption.CREATE,
        StandardOpenOption.TRUNCATE_EXISTING);
```
De `Files.write`‑aanroep maakt het uitvoerbestand aan als het niet bestaat, of overschrijft het anders. De methode gooit een `IOException` als de map ontbreekt of het proces geen schrijfrechten heeft.

## Veelvoorkomende valkuilen behandelen

| Issue | Symptomen | Oplossing |
|-------|-----------|----------|
| **Ontbrekend invoerbestand** | `java.nio.file.NoSuchFileException` | Controleer of `INPUT_PATH` naar een bestaand bestand wijst. Gebruik `Files.exists(Path)` voor een pre‑flight check. |
| **Niet‑ondersteunde CSS** | Layout ziet er eenvoudig of kapot uit | Gebruik een meer functionaliteit‑rijke engine zoals *OpenHTMLtoPDF* (voeg de Maven‑afhankelijkheid toe en vervang `HtmlRenderer` door `PdfRendererBuilder`). |
| **Grote HTML veroorzaakt geheugen‑druk** | `OutOfMemoryError` | Stream de HTML in delen of vergroot de JVM‑heap (`-Xmx2g`). |
| **Unicode‑tekens verschijnen als �** | Vervormde tekst in de PDF | Zorg ervoor dat het HTML‑bestand als UTF‑8 is opgeslagen en dat het lettertype van de renderer de benodigde glyphs ondersteunt (embed een lettertype via `renderer.setDefaultFont("Arial Unicode MS")`). |

## Volledig werkend voorbeeld

Sla de bovenstaande klasse op als `src/main/java/com/example/pdfconverter/HtmlToPdfConverter.java`, pas de paden aan en voer uit:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.pdfconverter.HtmlToPdfConverter"
```

Als alles correct is ingesteld, zie je:

```
✅ PDF created successfully at YOUR_DIRECTORY/output.pdf
```

Open `output.pdf` met een PDF‑viewer — je zou de gerenderde HTML‑pagina exact moeten zien zoals deze in een browser verschijnt.

## Conclusie

Je weet nu hoe je **pdf van html kunt maken** in Java met een beknopt, productie‑klaar patroon. De tutorial behandelde:

* Het toevoegen van de benodigde Maven‑afhankelijkheden  
* Het veilig lezen van een HTML‑bestand  
* Het uitvoeren van de **convert html file to pdf**‑operatie met `HtmlRenderer`  
* Het schrijven van de resulterende PDF en het afhandelen van I/O‑fouten  

Vanaf hier kun je geavanceerde onderwerpen verkennen, zoals **convert html to pdf** met aangepaste headers/footers, grote documenten streamen, of overschakelen naar een andere render‑engine voor rijkere CSS‑ondersteuning.

**Volgende stappen**

* Probeer **how to convert html to pdf** met *OpenHTMLtoPDF* voor betere CSS3‑afhandeling.  
* Experimenteer met het toevoegen van een omslagpagina of inhoudsopgave met PDFBox direct.  
* Kijk naar server‑side PDF‑generatie voor webservices, waarbij je de PDF‑bytes retourneert in een HTTP‑respons.

Veel plezier met coderen, en geniet van de soepele workflow van het omzetten van HTML naar hoogwaardige PDF’s!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe HTML naar PDF te converteren in Java – Met Aspose.HTML voor Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [PDF maken van HTML in Java – Complete stap‑voor‑stap gids](/html/english/java/conversion-html-to-other-formats/create-pdf-from-html-in-java-complete-step-by-step-guide/)
- [html to pdf tutorial: HTML naar PDF converteren in Java in één regel](/html/english/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java-in-one-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}