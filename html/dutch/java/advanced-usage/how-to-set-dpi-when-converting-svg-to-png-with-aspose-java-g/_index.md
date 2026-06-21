---
category: general
date: 2026-04-23
description: Leer hoe je DPI instelt voor ultra‑hoog‑kwaliteits SVG‑naar‑PNG-conversie
  in Java met Aspose. Inclusief stapsgewijze code, tips en afhandeling van randgevallen.
draft: false
keywords:
- how to set dpi
- convert svg to png
- svg to png java
- how to convert svg
- aspose svg to png
language: nl
og_description: Beheers hoe je DPI instelt voor SVG‑naar‑PNG-conversie met Aspose
  HTML in Java. Complete code, uitleg en best‑practice‑tips.
og_title: Hoe DPI in te stellen bij het converteren van SVG naar PNG – Java‑tutorial
tags:
- Aspose
- Java
- SVG
- PNG
- Image Conversion
title: Hoe DPI in te stellen bij het converteren van SVG naar PNG met Aspose – Java‑gids
url: /nl/java/advanced-usage/how-to-set-dpi-when-converting-svg-to-png-with-aspose-java-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe DPI in te stellen bij het converteren van SVG naar PNG met Aspose – Java‑gids

Heb je je ooit afgevraagd **hoe je DPI instelt** voor een kristalheldere PNG die afkomstig is van een SVG? Misschien bouw je een branding‑pipeline en heb je het logo nodig op 600 dpi voor drukwerk, of wil je gewoon dat de rasterafbeelding er scherp uitziet op hoge‑resolutie schermen. Het goede nieuws is dat je niet hoeft te gokken—Aspose HTML for Java maakt het een fluitje van een cent.

In deze tutorial lopen we **uit hoe je DPI instelt** terwijl je **SVG naar PNG converteert** met de Aspose‑bibliotheek. Je krijgt een volledige, kant‑klaar code‑voorbeeld, een uitleg van elke configuratie‑optie, en een reeks praktische tips voor projecten in de echte wereld. Geen externe referenties nodig—alles wat je nodig hebt staat hier.

## Voorvereisten

Voordat we beginnen, zorg dat je het volgende hebt:

- Java 17 (of een recente JDK) geïnstalleerd.
- Maven of Gradle om afhankelijkheden te beheren (we laten het Maven‑fragment zien).
- Een SVG‑bestand dat je wilt rasteren (bijv. `logo.svg`).
- Een basisbegrip van Java‑syntaxis—niets speciaals, gewoon de gebruikelijke `public static void main`.

Als een van deze ontbreekt, haal het eerst op; de rest van de gids gaat ervan uit dat ze al aanwezig zijn.

## Maven‑afhankelijkheid

Voeg de Aspose HTML for Java‑afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle‑gebruikers kunnen het fragment vervangen door de equivalente regel `implementation "com.aspose:aspose-html:23.12"`.

## Stap 1: Maak het Conversie‑optiesobject

Het eerste wat je moet doen is een `SvgConversionOptions`‑instantie maken. Dit object bevat elke aanpassing die je wilt—DPI, achtergrondkleur, schaling, enzovoort.

```java
// Step 1: Build conversion options for SVG → PNG
SvgConversionOptions conversionOptions = new SvgConversionOptions();
```

Waarom dit belangrijk is: zonder expliciet de DPI in te stellen, gebruikt Aspose standaard 96 dpi, wat prima is voor web maar verre van print‑klaar. Door het optiesobject te maken, krijg je volledige controle over het rasterisatie‑proces.

## Stap 2: Stel de gewenste DPI in

Nu beantwoorden we de kernvraag: **hoe je DPI instelt**. De methode `setDpi(int)` verwacht een geheel getal; typische waarden liggen tussen 72 dpi (laag‑res) en 1200 dpi (ultra‑hoog‑res). Voor de meeste printopdrachten is 300 dpi de ideale waarde; voor logo’s die moeten schalen, is 600 dpi een veilige keuze.

```java
// Step 2: Define the resolution (DPI) – 600 DPI for ultra‑high‑quality output
conversionOptions.setDpi(600);
```

> **Pro tip:** DPI‑waarden die geen veelvouden van 72 zijn, kunnen soms niet‑gehele pixelafmetingen opleveren. Als je een exacte pixelgrootte nodig hebt, bereken dan `pixel = inches * DPI` vooraf en pas de SVG‑viewBox dienovereenkomstig aan.

## Stap 3: Transparantie afhandelen met een achtergrondkleur

SVG‑bestanden bevatten vaak transparante gebieden. PNG ondersteunt transparantie, maar als je een print‑workflow hebt die een ondoorzichtige achtergrond verwacht, wil je die vervangen. De methode `setBackgroundColor(String)` accepteert elke CSS‑compatibele kleurstring.

```java
// Step 3: Replace transparent areas with white (or any color you prefer)
conversionOptions.setBackgroundColor("white");
```

Je kunt ook `#FFFFFF`, `rgb(255,255,255)` of zelfs `transparent` gebruiken als je *wel* het alfakanaal wilt behouden.

## Stap 4: Voer de conversie uit

Met de opties geconfigureerd, is de daadwerkelijke conversie één statische aanroep naar `Converter.convert`. Geef het invoer‑SVG‑pad, het gewenste PNG‑uitvoerpAd en het optiesobject op.

```java
// Step 4: Convert the SVG file to a PNG using the configured options
Converter.convert(
        "YOUR_DIRECTORY/logo.svg",   // Input SVG
        "YOUR_DIRECTORY/logo.png",   // Output PNG
        conversionOptions);          // Options we just set
```

Dat is alles—Aspose verwerkt het parsen van de SVG, past de DPI‑schaal toe, vult de achtergrond en schrijft het PNG‑bestand naar schijf.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat de complete Java‑klasse die je kunt kopiëren‑en‑plakken in een bestand met de naam `SvgToPngHighRes.java`. Vervang `YOUR_DIRECTORY` door het daadwerkelijke mappad op jouw machine.

```java
import com.aspose.html.converters.SvgConversionOptions;
import com.aspose.html.converters.Converter;

/**
 * Demonstrates how to set DPI when converting an SVG file to a high‑resolution PNG
 * using Aspose.HTML for Java.
 *
 * Prerequisites:
 *   - Aspose.HTML for Java library (Maven dependency shown earlier)
 *   - Java 17+ runtime
 *
 * Expected result:
 *   - logo.png created at 600 DPI with a white background.
 */
public class SvgToPngHighRes {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create conversion options for SVG → PNG
        SvgConversionOptions conversionOptions = new SvgConversionOptions();

        // 2️⃣ Set the desired resolution (DPI) – 600 DPI yields ultra‑high‑quality output
        conversionOptions.setDpi(600);

        // 3️⃣ Define a background color to replace any transparency (white works for most prints)
        conversionOptions.setBackgroundColor("white");

        // 4️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convert(
                "YOUR_DIRECTORY/logo.svg",   // <-- change this to your source file
                "YOUR_DIRECTORY/logo.png",   // <-- change this to your target file
                conversionOptions);

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/logo.png");
    }
}
```

### Verwachte output

Het uitvoeren van het programma genereert `logo.png` in dezelfde map. Open het bestand in een afbeeldingsviewer en inspecteer de **afbeeldingseigenschappen**—je zou moeten zien:

- **Resolutie:** 600 dpi (of welke waarde je ook hebt ingesteld)
- **Afmetingen:** Geschaald volgens de oorspronkelijke SVG‑viewBox vermenigvuldigd met de DPI‑factor
- **Achtergrond:** Solid wit (geen transparante pixels)

Als je de PNG opent in een tool zoals Photoshop, is de DPI‑metadata zichtbaar onder *Afbeelding → Afbeeldingsgrootte*.

## Veelvoorkomende randgevallen & hoe ze op te lossen

| Situatie | Waar op te letten | Aanbevolen oplossing |
|----------|-------------------|----------------------|
| **Ontbrekend SVG‑bestand** | `FileNotFoundException` gegooid door `Converter.convert` | Valideer het pad vóór conversie met `Files.exists(Paths.get(...))`. |
| **Niet‑ondersteunde SVG‑functies** (bijv. filters die nog niet geïmplementeerd zijn) | Aspose kan die functies stilletjes weglaten | Gebruik `SvgConversionOptions.setEnableSvgFilters(true)` als je filterondersteuning nodig hebt (beschikbaar in nieuwere versies). |
| **Zeer hoge DPI (≥1200)** | Uitvoerbestand kan enorm worden (honderden MB) | Overweeg streaming van het resultaat of verlaag de DPI voor grote afbeeldingen. |
| **Transparantie behouden** | Je stelt een achtergrondkleur in maar wilt eigenlijk alfa | Laat `setBackgroundColor` weg of geef `"transparent"` door om het originele alfakanaal te behouden. |
| **Batch‑conversie** | Het opnieuw maken van `SvgConversionOptions` voor elk bestand is inefficiënt | Maak één `SvgConversionOptions`‑instantie en hergebruik deze binnen een lus. |

## Veelgestelde vragen

**V: Werkt dit ook met andere rasterformaten zoals JPEG of BMP?**  
A: Ja. Vervang de extensie van het uitvoerbestand (`.png`) door `.jpg` of `.bmp`, en Aspose selecteert automatisch de juiste encoder. Je kunt de JPEG‑kwaliteit ook verfijnen via `JpegConversionOptions`.

**V: Kan ik SVG‑bestanden converteren die in een byte‑array zijn opgeslagen in plaats van in een bestand?**  
A: Absoluut. Gebruik de overloads `Converter.convert(InputStream, OutputStream, conversionOptions)` om met streams te werken, wat handig is voor webservices.

**V: Is de DPI‑instelling hetzelfde als het schalen van de afbeelding?**  
A: DPI is een metadata‑tag die printers vertelt hoeveel pixels een inch vertegenwoordigen. Intern schaalt Aspose de rasterafbeelding om overeen te komen met de DPI, dus de visuele grootte verandert als je de PNG bekijkt op 100 % zoom in een viewer die DPI respecteert.

## Pro‑tips voor productieklaar code

1. **Cache de opties** – Als je tientallen logo’s met dezelfde DPI en achtergrond converteert, instantiateer `SvgConversionOptions` één keer en hergebruik deze. Dit vermindert de overhead van objectcreatie.
2. **Valideer invoerafmetingen** – Voor extreem grote SVG‑bestanden, bereken de verwachte pixelgrootte (`width * DPI/96`) en annuleer als deze een veilig limiet (bijv. 20 000 px) overschrijdt om `OutOfMemoryError` te voorkomen.
3. **Log conversiemetadata** – Sla DPI, bestandsnaam en tijdstempel op in een logbestand; dit vereenvoudigt later debuggen.
4. **Thread‑veiligheid** – `Converter.convert` is thread‑safe, dus je kunt batch‑taken paralleliseren met een `ExecutorService`.

## Visuele samenvatting

![voorbeeld hoe DPI in te stellen](image.png){: .align-center alt="voorbeeld hoe DPI in te stellen"}

Het diagram hierboven illustreert de stroom: **SVG → DPI & achtergrond instellen → PNG**.

## Conclusie

Je weet nu **hoe je DPI instelt** wanneer je **SVG naar PNG converteert** met Aspose HTML for Java. Door `SvgConversionOptions` te configureren beheer je resolutie, achtergrondafhandeling en meer, waardoor een eenvoudig vectorbestand wordt omgezet in een print‑klaar rasterbeeld met slechts een paar regels code.

Ga nu een stap verder en experimenteer met:

- Het batch‑converteren van een hele map SVG‑bestanden.
- Het wijzigen van het uitvoerformaat naar JPEG voor web‑geoptimaliseerde assets.
- Het gebruik van andere Aspose‑conversie‑opties zoals `setScaleX/Y` voor aangepaste schaling naast DPI.

Happy coding, en moge je PNG‑bestanden altijd net zo scherp zijn als je ze nodig hebt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}