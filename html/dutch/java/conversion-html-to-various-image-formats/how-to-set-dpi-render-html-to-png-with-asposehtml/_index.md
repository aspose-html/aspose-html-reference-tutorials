---
category: general
date: 2026-01-14
description: hoe DPI in te stellen bij het converteren van een URL naar PNG. Leer
  HTML naar PNG te renderen, de viewportgrootte in te stellen en HTML op te slaan
  als PNG met Aspose.HTML in Java.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: nl
og_description: hoe DPI in te stellen bij het converteren van een URL naar PNG. Stapsgewijze
  handleiding om HTML naar PNG te renderen, de viewportgrootte te regelen en HTML
  op te slaan als PNG met Aspose.HTML.
og_title: Hoe DPI in te stellen – HTML renderen naar PNG met AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: hoe DPI in te stellen – HTML renderen naar PNG met AsposeHTML
url: /nl/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe DPI in te stellen – HTML renderen naar PNG met AsposeHTML

Heb je je ooit afgevraagd **hoe je DPI instelt** voor een screenshot‑achtig beeld dat van een webpagina wordt gegenereerd? Misschien heb je een 300 DPI PNG nodig voor afdrukken, of een lage‑res thumbnail voor een mobiele app. In beide gevallen is de truc om de renderengine te vertellen welke logische DPI je wilt, en het vervolgens het zware werk te laten doen.  

In deze tutorial nemen we een live URL, renderen we deze naar een PNG‑bestand, **stellen we de viewport‑grootte in**, passen we de DPI aan, en slaan we tenslotte **HTML op als PNG**—alles met Aspose.HTML voor Java. Geen externe browsers, geen rommelige command‑line tools—gewoon nette Java‑code die je in elk Maven‑ of Gradle‑project kunt gebruiken.

> **Pro tip:** Als je alleen een snelle thumbnail wilt, kun je de DPI op 96 DPI houden (de standaard voor de meeste schermen). Voor print‑klare assets, verhoog je deze naar 300 DPI of hoger.

![voorbeeld hoe DPI in te stellen](https://example.com/images/how-to-set-dpi.png "voorbeeld hoe DPI in te stellen")

## Wat je nodig hebt

- **Java 17** (of een recente JDK).  
- **Aspose.HTML for Java** 24.10 of nieuwer. Je kunt het ophalen van Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Een internetverbinding om de doelpagina op te halen (het voorbeeld gebruikt `https://example.com/sample.html`).  
- Schrijfrechten voor de doelmap.

Dat is alles—geen Selenium, geen headless Chrome. Aspose.HTML doet de rendering in‑process, wat betekent dat je binnen de JVM blijft en de overhead van het starten van een browser vermijdt.

## Stap 1 – Laad het HTML‑document vanaf een URL

Eerst maken we een `HTMLDocument`‑instantie die naar de pagina wijst die we willen vastleggen. De constructor downloadt automatisch de HTML, parseert deze en bereidt de DOM voor.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Waarom dit belangrijk is:* Door het document direct te laden, hoef je geen aparte HTTP‑client te gebruiken. Aspose.HTML respecteert redirects, cookies, en zelfs basisauthenticatie als je inloggegevens in de URL opneemt.

## Stap 2 – Bouw een sandbox met gewenste DPI en viewport

Een **sandbox** is de manier waarop Aspose.HTML een browser‑omgeving nabootst. Hier laten we het doen alsof het een 1280 × 720 scherm is en, cruciaal, stellen we de **apparaat‑DPI** in. Het wijzigen van de DPI verandert de pixel‑dichtheid van de gerenderde afbeelding zonder de logische grootte aan te passen.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Waarom je deze waarden zou kunnen aanpassen:*
- **Viewport‑grootte** bepaalt hoe CSS‑media‑queries (`@media (max-width: …)`) zich gedragen.  
- **Apparaat‑DPI** beïnvloedt de fysieke grootte van de afbeelding bij afdrukken. Een 96 DPI afbeelding ziet er goed uit op schermen; een 300 DPI afbeelding behoudt scherpte op papier.  

Als je een vierkante thumbnail nodig hebt, wijzig je eenvoudig `setViewportSize(500, 500)` en houd je de DPI laag.

## Stap 3 – Kies PNG als uitvoerformaat

Aspose.HTML ondersteunt verschillende rasterformaten (PNG, JPEG, BMP, GIF). PNG is loss‑less, waardoor het perfect is voor screenshots waarbij je elke pixel wilt behouden.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Je kunt ook het compressieniveau aanpassen (`pngOptions.setCompressionLevel(9)`) als je je zorgen maakt over de bestandsgrootte.

## Stap 4 – Render en sla de afbeelding op

Nu laten we het document zichzelf **opslaan** als afbeelding. De `save`‑methode neemt een bestandspad en de eerder geconfigureerde opties.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Wanneer het programma klaar is, vind je een PNG‑bestand op `YOUR_DIRECTORY/sandboxed.png`. Open het—als je de DPI op 300 hebt ingesteld, zal de afbeeldingsmetadata dat weergeven, hoewel de pixelafmetingen 1280 × 720 blijven.

## Stap 5 – Verifieer de DPI (optioneel maar handig)

Als je wilt dubbel‑controleren of de DPI echt is toegepast, kun je de PNG‑metadata lezen met een lichte bibliotheek zoals **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Je zou `300` (of wat je ook hebt ingesteld) in de console moeten zien verschijnen. Deze stap is niet vereist voor het renderen, maar het is een snelle sanity‑check, vooral wanneer je assets genereert voor een print‑workflow.

## Veelgestelde vragen & randgevallen

### “Wat als de pagina JavaScript gebruikt om inhoud te laden?”

Aspose.HTML voert een **beperkte subset** van JavaScript uit. Voor de meeste statische sites werkt het direct. Als de pagina sterk afhankelijk is van client‑side frameworks (React, Angular, Vue), moet je de pagina mogelijk vooraf renderen of een headless browser gebruiken. Het instellen van DPI werkt echter op dezelfde manier zodra de DOM klaar is.

### “Kan ik een PDF renderen in plaats van PNG?”

Zeker. Vervang `ImageSaveOptions` door `PdfSaveOptions` en wijzig de uitvoerextensie naar `.pdf`. De DPI‑instelling beïnvloedt nog steeds het gerasterde uiterlijk van eventuele ingesloten afbeeldingen.

### “Wat betreft high‑resolution screenshots voor retina‑displays?”

Verdubbel simpelweg de viewport‑afmetingen terwijl je de DPI op 96 DPI houdt, of behoud de viewport en verhoog de DPI naar 192. De resulterende PNG bevat dan twee keer zoveel pixels, waardoor je dat scherpe retina‑gevoel krijgt.

### “Moet ik resources opruimen?”

`HTMLDocument` implementeert `AutoCloseable`. In een productie‑app, wikkel het in een try‑with‑resources‑blok:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

## Volledig werkend voorbeeld (klaar om te kopiëren‑plakken)

Hieronder staat het volledige, kant‑klaar programma. Vervang `YOUR_DIRECTORY` door een echte map op jouw machine.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Voer de klasse uit, en je krijgt een PNG die de **hoe DPI in te stellen**‑instelling die je hebt opgegeven respecteert.

## Conclusie

We hebben stap voor stap uitgelegd **hoe je DPI instelt** wanneer je **HTML rendert naar PNG**, de stap **viewport‑grootte instellen** behandeld, en laten zien hoe je **HTML opslaat als PNG** met Aspose.HTML voor Java. De belangrijkste punten zijn:

- Gebruik een **sandbox** om DPI en viewport te controleren.  
- Kies de juiste **ImageSaveOptions** voor lossless output.  
- Verifieer de DPI‑metadata als je printkwaliteit moet garanderen.  

Vanaf hier kun je experimenteren met verschillende DPI‑waarden, grotere viewports, of zelfs een batch‑verwerking van een lijst URL's. Wil je een hele website omzetten naar PNG‑thumbnails? Loop gewoon over een array van URL's en hergebruik dezelfde sandbox‑configuratie.

Veel renderplezier, en moge je screenshots altijd pixel‑perfect zijn!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}