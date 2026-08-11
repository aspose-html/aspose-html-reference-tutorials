---
category: general
date: 2026-02-14
description: Hoe DPI in te stellen voor SVG-naar-PNG-conversie met Java. Exporteer
  PNG met hoge resolutie, leer SVG naar PNG te converteren en gebruik een Java-afbeeldingsconversiebibliotheek.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: nl
og_description: Hoe DPI in te stellen voor SVG‑naar‑PNG-conversie met Java. Deze gids
  laat zien hoe je een PNG met hoge resolutie exporteert en een Java‑afbeeldingsconversiebibliotheek
  gebruikt.
og_title: Hoe DPI in te stellen bij het converteren van SVG naar PNG met Java
tags:
- java
- image-conversion
- svg
- png
title: Hoe DPI in te stellen bij het converteren van SVG naar PNG met Java
url: /nl/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

PNG with Java" translated.

Make sure we didn't translate code block placeholders.

Check for any URLs inside text: none.

Check for any variable names: we kept them.

Check for any markdown links: none.

All good.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe DPI in te stellen bij het converteren van SVG naar PNG met Java

Heb je je ooit afgevraagd **hoe je DPI moet instellen** voor een SVG‑naar‑PNG‑conversie zodat het resultaat scherp is op een print‑klaar poster? Je bent niet de enige. In veel projecten—denk aan marketingflyers, UI‑mock‑ups of technische diagrammen—het verkrijgen van een high‑resolution PNG uit een SVG is niet onderhandelbaar.  

In deze tutorial lopen we de exacte stappen door om **SVG naar PNG te converteren**, **high resolution PNG te exporteren**, en, vooral, de DPI te regelen met behulp van de Aspose.HTML for Java bibliotheek. Aan het einde heb je een herbruikbare code‑snippet die je in elke Java‑applicatie kunt plaatsen, ongeacht of je een desktop‑tool of een backend‑service bouwt.

## Wat je nodig hebt

- **Java 8+** (de code compileert met elke recente JDK)
- **Aspose.HTML for Java** JAR‑s (beschikbaar via Maven Central of de Aspose‑website)
- Een SVG‑bestand dat je wilt rasteren  
- Een klein beetje nieuwsgierigheid—niets anders.

Als je vertrouwd bent met Maven, voeg dan gewoon de afhankelijkheid toe zoals weergegeven in de volgende sectie; anders download je de JAR‑s handmatig en voeg je ze toe aan je classpath.

## Stap 1: Voeg de Java‑afbeeldingsconversiebibliotheek toe

Allereerst—je project heeft de **java image conversion library** nodig die daadwerkelijk SVG kan lezen en PNG kan schrijven. Aspose.HTML is een solide keuze omdat het CSS, fonts en complexe vectorfuncties direct ondersteunt.

**Maven‑gebruikers** kunnen dit in je `pom.xml` plakken:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Gradle‑liefhebbers** kunnen toevoegen:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Als je de handmatige route verkiest, download dan de JAR van de Aspose‑downloadpagina en plaats deze in `libs/`, voeg hem vervolgens toe aan het build‑pad van je IDE.

> **Pro tip:** Houd het versienummer in de gaten; nieuwere releases verbeteren vaak de DPI‑afhandeling en lossen edge‑case‑bugs op.

## Stap 2: Maak conversie‑opties aan en stel de gewenste DPI in

Nu de bibliotheek aan boord is, moeten we hem vertellen *hoe* we de uitvoer‑PNG eruit willen laten zien. Hier komt het belangrijkste trefwoord—**how to set DPI**—in beeld. De `ImageConversionOptions`‑klasse geeft je gedetailleerde controle over zowel horizontale (`dpiX`) als verticale (`dpiY`) resolutie.

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Waarom 300 DPI? Voor de meeste print‑workflows wordt 300 dots‑per‑inch beschouwd als “printkwaliteit”. Als je alleen web‑assets target, kun je dit verlagen naar 72 of 96 DPI om de bestandsgrootte klein te houden.

> **Wat als ik een andere DPI voor breedte en hoogte nodig heb?**  
> Verander gewoon `setDpiX` en `setDpiY` onafhankelijk van elkaar. De bibliotheek respecteert niet‑uniforme waarden, wat handig is voor anamorfische afbeeldingen.

## Stap 3: Voer de SVG‑naar‑PNG-conversie uit

Met de opties klaar, is de daadwerkelijke conversie een enkele statische aanroep. We gebruiken `java.nio.file.Paths` om platform‑onafhankelijk te blijven.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

Dat is alles—voer de `main`‑methode uit en je vindt een scherpe, 300 DPI PNG in `YOUR_DIRECTORY`. De bibliotheek schaalt de vectorafbeeldingen automatisch om te voldoen aan de opgegeven DPI, waarbij de beeldverhouding en teksthelderheid behouden blijven.

## Stap 4: Verifieer het resultaat (optioneel maar aanbevolen)

Een snelle sanity‑check kan je later hoofdpijn besparen. Open de gegenereerde PNG in een beeldviewer die DPI‑metadata toont (bijv. Photoshop, GIMP, of zelfs het “Details”‑tabblad van Windows Explorer). Je zou **300 DPI** moeten zien staan onder horizontale en verticale resolutie.

Als het bestand er wazig uitziet, controleer dan:

1. De originele SVG is niet al van lage resolutie (vectorbestanden zijn resolutie‑agnostisch, maar ingebedde rasterafbeeldingen erin kunnen de kwaliteit beperken).  
2. Je hebt het bestand echt opgeslagen na het instellen van de DPI—soms cachen IDE's oude builds.  
3. De conversie‑opties zijn niet elders in je code overschreven.

## Waarom DPI belangrijk is voor het exporteren van high resolution PNG

Je zou kunnen vragen: “Waarom zou je je überhaupt met DPI bemoeien? Is PNG niet gewoon pixels?” Het is waar dat DPI een *metadata*‑tag is die downstream‑applicaties (vooral print‑gerichte) vertelt hoeveel pixels overeenkomen met een inch fysieke ruimte. Als je een 1200 × 800 PNG aan een printer geeft zonder juiste DPI‑metadata, gaat de printer mogelijk uit van een standaardwaarde (vaak 72 DPI) en vergroot de afbeelding, wat leidt tot een wazig resultaat.

Het correct instellen van DPI is ook een prestatievoordeel: je vermijdt later het opschalen van rasterafbeeldingen, wat computationeel duur kan zijn en de kwaliteit kan verminderen.

## Randgevallen & Veelvoorkomende valkuilen

| Situation | What to Watch For | How to Fix |
|-----------|-------------------|------------|
| **SVG bevat ingesloten bitmap‑afbeeldingen** | De ingesloten bitmap kan een lage resolutie hebben, waardoor de uiteindelijke PNG er zelfs bij hoge DPI gepixeld uitziet. | Vervang de bitmap door een versie met hogere resolutie of bewerk de SVG zodat deze naar een externe afbeelding verwijst. |
| **Grote DPI‑waarden (bijv. 1200 DPI)** | Het geheugenverbruik stijgt sterk; je kunt een `OutOfMemoryError` krijgen. | Verhoog de JVM‑heap‑grootte (`-Xmx2g`) of beperk de DPI tot een redelijk maximum voor jouw gebruikssituatie. |
| **Niet‑vierkante pixels** | Sommige displays interpreteren DPI anders, wat leidt tot uitgerekte afbeeldingen. | Zorg ervoor dat `setDpiX` gelijk is aan `setDpiY`, tenzij je een specifieke reden hebt om ze te laten verschillen. |
| **Ontbrekende fonts** | Tekst in de SVG kan terugvallen op een standaardfont, waardoor de lay-out verandert. | Integreer fonts in de SVG of installeer de benodigde fonts op de runtime‑machine. |

## Korte samenvatting (in één zin)

Om **how to set DPI** voor een SVG‑naar‑PNG-conversie uit te voeren, maak je een `ImageConversionOptions`‑object aan, stel je `dpiX`/`dpiY` in, en roep je `Converter.convert` aan vanuit de Aspose.HTML Java‑bibliotheek.

## Volgende stappen & gerelateerde onderwerpen

- **Batchverwerking:** Loop over een map met SVG‑bestanden en pas dezelfde DPI‑instellingen toe.  
- **Dynamische DPI:** Lees een configuratie‑bestand of command‑line‑argument om DPI tijdens runtime in te stellen.  
- **Alternatieve bibliotheken:** Als je Aspose niet kunt gebruiken, overweeg dan **Batik** (Apache) of **SVG Salamander**, hoewel ze extra code kunnen vereisen om DPI te verwerken.  
- **Export high resolution PNG** voor Android‑assets: combineer deze techniek met Android’s `drawable‑hdpi`, `xhdpi`, etc., mappen.

Voel je vrij om te experimenteren—probeer 72 DPI voor web‑thumbnails, 600 DPI voor grootformaat‑prints, of zelfs 150 DPI als een middenweg. De code blijft hetzelfde; alleen de getallen veranderen.

---

![hoe DPI in te stellen](placeholder-image.png "Illustratie van DPI‑instelling in Java‑conversieworkflow")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}