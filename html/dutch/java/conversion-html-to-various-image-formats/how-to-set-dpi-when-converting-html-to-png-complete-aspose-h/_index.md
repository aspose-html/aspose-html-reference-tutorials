---
category: general
date: 2026-06-29
description: Leer hoe u DPI en beeldresolutie instelt bij het converteren van HTML
  naar PNG met Aspose HTML Converter. Stap‑voor‑stap Java‑voorbeeld inbegrepen.
draft: false
keywords:
- how to set dpi
- convert html to png
- set image resolution
- convert html page
- aspose html converter
language: nl
og_description: Hoe DPI in Aspose HTML-conversie in te stellen. Deze gids laat zien
  hoe u een HTML-pagina naar een hoge‑resolutie PNG-afbeelding converteert in Java.
og_title: Hoe DPI in te stellen bij het converteren van HTML naar PNG – Aspose HTML
  Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  headline: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  type: TechArticle
- description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  name: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  steps:
  - name: 1. Different Output Formats
    text: Aspose.HTML isn’t limited to PNG. Swap the file extension and use a matching
      options class, e.g., `JpegConversionOptions` for JPEGs. The DPI logic stays
      identical.
  - name: 2. Dynamically Determining Screen Size
    text: 'If you need the sandbox to mimic a mobile device, read the dimensions from
      a config file:'
  - name: 3. Batch Conversion
    text: Wrap the conversion call inside a loop that iterates over a directory of
      HTML files. Remember to reuse the same `Sandbox` and `ImageConversionOptions`
      objects to avoid unnecessary allocations.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Image Processing
title: Hoe DPI in te stellen bij het converteren van HTML naar PNG – Complete Aspose
  HTML-gids
url: /nl/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png-complete-aspose-h/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe DPI in te stellen bij het converteren van HTML naar PNG – Complete Aspose HTML-gids

Heb je je ooit afgevraagd **hoe je DPI** kunt instellen voor een PNG die je genereert vanuit een HTML‑pagina? In veel rapportage‑ of screenshot‑automatiseringsscenario’s is de standaard 96 dpi simpelweg niet scherp genoeg. Het goede nieuws is dat Aspose.HTML voor Java je volledige controle geeft over schermsimulatie en afbeeldingsresolutie, zodat je de DPI kunt opschroeven naar 300 of zelfs 600 met slechts een paar regels code.

In deze tutorial lopen we een praktisch Java‑voorbeeld door dat **een HTML‑pagina naar PNG converteert** terwijl het expliciet **de DPI** en **beeldresolutie** instelt. Aan het einde heb je een kant‑klaar klasse, begrijp je waarom elke instelling belangrijk is, en weet je hoe je deze kunt aanpassen voor verschillende use‑cases zoals hoge‑resolutie afdrukken of web‑thumbnails.

> **Korte preview:** De kernstappen zijn (1) een `Sandbox` maken die een scherm nabootst, (2) de DPI instellen, (3) `ImageConversionOptions` configureren met de gewenste resolutie, en (4) `Converter.convert` aanroepen. Geen externe tools, geen command‑line toeren—alleen pure Java.

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

- **Java 17** (of een recente JDK) geïnstalleerd en geconfigureerd in je IDE.
- **Aspose.HTML voor Java**‑bibliotheek (het Maven‑artifact `com.aspose:aspose-html`). Je kunt de nieuwste versie halen van de [Aspose Maven‑repository](https://repo.aspose.com/repo) of de JAR direct downloaden.
- Een eenvoudige HTML‑file (`page.html`) die je wilt omzetten naar een PNG. Plaats deze ergens toegankelijk, bv. `C:/temp/page.html`.
- Basiskennis van Java‑exception handling—niets ingewikkeld.

Als een van deze onderdelen onbekend is, pauzeer even en installeer het ontbrekende onderdeel. De rest van de gids gaat ervan uit dat je comfortabel een Java‑project kunt openen en externe JAR‑bestanden kunt toevoegen.

## Stap 1: Stel je Maven‑project in (of voeg JAR handmatig toe)

Als je Maven gebruikt, voeg dan de afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.11</version> <!-- Check for the newest version -->
</dependency>
```

Anders, plaats de `aspose-html-*.jar` in de `libs`‑map van je project en voeg deze toe aan het build‑pad. Deze stap gaat niet direct over **hoe DPI in te stellen**, maar zonder de bibliotheek kun je de `Sandbox`‑klasse die DPI‑controle mogelijk maakt niet gebruiken.

## Stap 2: Maak een Sandbox die een echt scherm simuleert

Een *sandbox* is Aspose‑manier om een browseromgeving te reproduceren. Beschouw het als een virtueel scherm waarbij je de breedte, hoogte en vooral de **DPI** bepaalt. Hieronder staat de code‑snippet die een scherm van 1024 × 768 bij 96 dpi maakt—een basis voordat we de resolutie verhogen:

```java
// Step 2.1: Initialise the sandbox
Sandbox sandbox = new Sandbox();

// Step 2.2: Define virtual screen dimensions (pixels)
sandbox.setScreenWidth(1024);
sandbox.setScreenHeight(768);

// Step 2.3: Set the DPI – this is the key to controlling image sharpness
sandbox.setDpi(96); // Change this value to 300, 600, etc., later
```

> **Waarom een sandbox?** Zonder sandbox zou Aspose terugvallen op de scherminstellingen van de host‑machine, wat leidt tot inconsistente resultaten op verschillende ontwikkelmachines. Door de DPI vast te zetten, garandeer je dat elke conversie er hetzelfde uitziet, of je nu op een laptop of een CI‑server draait.

## Stap 3: Configureer Image Conversion Options – Stel beeldresolutie in

Nu de sandbox klaar is, vertellen we de converter welke **beeldresolutie** we willen. De `ImageConversionOptions`‑klasse laat je de DPI van de output‑PNG onafhankelijk van de sandbox‑DPI instellen, waardoor je twee hefbomen hebt om mee te spelen.

```java
// Step 3.1: Prepare conversion options
ImageConversionOptions conversionOptions = new ImageConversionOptions();

// Step 3.2: Desired output DPI – this directly influences PNG quality
conversionOptions.setResolution(300); // 300 dpi is print‑quality; increase for sharper prints

// Step 3.3: Bind the sandbox to the options so the layout engine respects our virtual screen
conversionOptions.setSandbox(sandbox);
```

**Tip:** Als je een PNG van 600 dpi wilt voor hoogwaardige brochures, wijzig dan `setResolution(300)` naar `setResolution(600)`. Houd er rekening mee dat hogere DPI‑waarden meer geheugen verbruiken en de verwerkingstijd verlengen, dus test eerst met een kleine pagina.

## Stap 4: Converteer de HTML‑pagina naar PNG

Met de sandbox en opties in place, is de feitelijke **convert html to png**‑stap een één‑regelige oproep:

```java
// Step 4: Perform the conversion
Converter.convert(
        "C:/temp/page.html",   // Source HTML file (convert html page)
        "C:/temp/page.png",    // Destination PNG file
        conversionOptions);    // Options that include DPI and sandbox
```

Als alles soepel verloopt zie je het console‑bericht van de volgende stap.

## Stap 5: Verifieer het resultaat en druk bevestiging af

Een snelle `System.out.println` vertelt je dat de taak voltooid is. In een echt project wil je misschien de bestandsgrootte, afmetingen, of zelfs de PNG programmatisch openen om de DPI te valideren.

```java
System.out.println("PNG generated with sandboxed layout at 300 dpi.");
```

Het uitvoeren van de klasse moet `page.png` aanmaken in dezelfde map als je HTML‑bestand. Open het in een afbeeldingsviewer die DPI weergeeft (bijv. Windows Photo Viewer → Eigenschappen → Details) en controleer dat het **300 dpi** aangeeft.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is een zelfstandige Java‑klasse die je kunt kopiëren‑plakken in je IDE:

```java
import com.aspose.html.conversions.Converter;
import com.aspose.html.conversions.options.ImageConversionOptions;
import com.aspose.html.sandbox.Sandbox;

public class HtmlToPngWithSandbox {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that simulates a 1024×768 screen with 96 dpi.
        Sandbox sandbox = new Sandbox();
        sandbox.setScreenWidth(1024);
        sandbox.setScreenHeight(768);
        sandbox.setDpi(96); // <-- This is where you learn how to set dpi

        // Step 2: Configure image conversion options – 300 dpi PNG using the sandbox.
        ImageConversionOptions conversionOptions = new ImageConversionOptions();
        conversionOptions.setResolution(300); // Set image resolution (dpi)
        conversionOptions.setSandbox(sandbox);

        // Step 3: Convert the HTML page to a PNG image using the defined options.
        Converter.convert(
                "C:/temp/page.html",   // convert html page
                "C:/temp/page.png",    // output PNG
                conversionOptions);    // includes dpi and resolution settings

        // Step 4: Indicate that the conversion has completed.
        System.out.println("PNG generated with sandboxed layout at 300 dpi.");
    }
}
```

> **Onthoud:** De regel `sandbox.setDpi(96);` is het *hoe DPI in te stellen*‑deel. Pas deze aan naar de schermdichtheid die je nodig hebt; `conversionOptions.setResolution(300);` bepaalt de DPI van de uiteindelijke afbeelding.

## Veelvoorkomende valkuilen behandelen

| Situatie | Waar je op moet letten | Aanbevolen oplossing |
|-----------|------------------------|----------------------|
| **Out‑of‑Memory‑fouten** bij gebruik van 600 dpi | Hoge DPI vergroot de rastergrootte drastisch (bijv. 1024 × 768 @ 600 dpi ≈ 4 MP). | Verklein de schermafmetingen, of stream de conversie met `ConversionProgress`‑callbacks. |
| **HTML gebruikt externe CSS/JS die niet wordt geladen** | De sandbox draait geïsoleerd; externe bronnen moeten bereikbaar zijn. | Geef absolute URL’s op of embed CSS direct in de HTML. |
| **Onjuiste DPI in de output** | Je hebt `sandbox.setDpi` aangepast maar `conversionOptions.setResolution` niet. | Zorg dat beide waarden overeenkomen met je gewenste output. |
| **FileNotFoundException** | Pad‑typefout of ontbrekende bestandsrechten. | Gebruik `Paths.get(...).toAbsolutePath()` en controleer lees‑/schrijfrechten. |

## Geavanceerde variaties

### 1. Verschillende outputformaten

Aspose.HTML is niet beperkt tot PNG. Vervang de bestandsextensie en gebruik een bijpassende options‑klasse, bv. `JpegConversionOptions` voor JPEG’s. De DPI‑logica blijft identiek.

```java
import com.aspose.html.conversions.options.JpegConversionOptions;

// ...

JpegConversionOptions jpegOpts = new JpegConversionOptions();
jpegOpts.setResolution(300);
jpegOpts.setSandbox(sandbox);

Converter.convert("page.html", "page.jpg", jpegOpts);
```

### 2. Dynamisch de schermgrootte bepalen

Als je wilt dat de sandbox een mobiel apparaat nabootst, lees je de afmetingen uit een configuratie‑bestand:

```java
sandbox.setScreenWidth(Integer.parseInt(System.getProperty("screen.width", "375")));
sandbox.setScreenHeight(Integer.parseInt(System.getProperty("screen.height", "667")));
sandbox.setDpi(Integer.parseInt(System.getProperty("screen.dpi", "96")));
```

Voer uit met `-Dscreen.width=375 -Dscreen.height=667 -Dscreen.dpi=326` om een iPhone Retina‑display te emuleren.

### 3. Batch‑conversie

Plaats de conversie‑aanroep in een lus die over een map met HTML‑bestanden itereren. Hergebruik dezelfde `Sandbox`‑ en `ImageConversionOptions`‑objecten om onnodige allocaties te vermijden.

```java
Files.list(Paths.get("C:/temp/html"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(htmlPath -> {
         String pngPath = htmlPath.toString().replace(".html", ".png");
         Converter.convert(htmlPath.toString(), pngPath, conversionOptions);
     });
```

## Verwachte output

Het uitvoeren van de klasse met de standaardinstellingen levert een PNG‑bestand van ongeveer **1024 × 768 pixels** bij **300 dpi** op. In de meeste beeldbewerkers verschijnen de afmetingen als 1024 × 768, terwijl de DPI‑metadata 300 aangeeft. Als je de afbeelding afdrukt op een breedte van 1 inch, krijg je een scherpe lijn van 300 pixel—perfect voor hoogwaardige flyers.

## Visuele samenvatting

![hoe DPI in te stellen in Aspose HTML-conversie](/images/aspose-dpi-example.png "hoe DPI in te stellen – Aspose HTML sandbox‑voorbeeld")

*De screenshot toont de DPI‑metadata van de gegenereerde PNG (300 dpi).*

## Conclusie

We hebben behandeld **hoe DPI in te stellen** wanneer je **HTML naar PNG converteert** met de **Aspose HTML Converter** in Java. Door een sandbox te maken, `ImageConversionOptions` te configureren en `Converter.convert` aan te roepen, krijg je pixel‑perfecte controle over zowel schermsimulatie als de uiteindelijke beeldresolutie. Of je nu afdrukbare facturen, hoge‑resolutie web‑assets of geautomatiseerde thumbnails genereert, hetzelfde patroon geldt—pas simpelweg de DPI en schermgrootte aan voor jouw situatie.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Aspose te gebruiken om HTML naar PNG te renderen – Stapsgewijze gids](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Hoe HTML naar JPEG te converteren met Aspose.HTML voor Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)
- [Hoe HTML naar BMP te converteren met Aspose.HTML voor Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-bmp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}