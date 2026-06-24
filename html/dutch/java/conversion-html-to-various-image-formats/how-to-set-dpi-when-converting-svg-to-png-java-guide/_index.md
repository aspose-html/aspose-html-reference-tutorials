---
category: general
date: 2026-05-06
description: Hoe DPI in te stellen voor high‑resolution SVG‑naar‑PNG conversie in
  Java met Aspose.HTML. Leer hoe je SVG naar PNG converteert, SVG exporteert als PNG,
  en vector naar raster converteert.
draft: false
keywords:
- how to set dpi
- convert svg to png
- how to convert svg
- export svg as png
- convert vector to raster
language: nl
og_description: Hoe DPI in te stellen voor hoge‑resolutie SVG‑naar‑PNG‑conversie in
  Java met Aspose.HTML. Ontvang stap‑voor‑stap code en deskundige tips.
og_title: Hoe DPI in te stellen bij het converteren van SVG naar PNG – Java-gids
tags:
- Java
- Aspose.HTML
- Image Conversion
title: Hoe DPI in te stellen bij het converteren van SVG naar PNG – Java-gids
url: /nl/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe DPI in te stellen bij het converteren van SVG naar PNG – Java-gids

Heb je je ooit afgevraagd **hoe je DPI moet instellen** voor een SVG‑naar‑PNG‑conversie en een scherp, afdrukklare afbeelding wilt krijgen? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur aan wanneer hun geëxporteerde PNG er wazig uitziet omdat de standaard DPI (meestal 96) gewoon niet genoeg is voor professioneel gebruik.

In deze tutorial lopen we een compleet, kant‑klaar voorbeeld door dat laat zien **hoe je DPI moet instellen** met Aspose.HTML voor Java. Aan het einde kun je **SVG naar PNG converteren**, **SVG exporteren als PNG**, en zelfs **vector naar raster converteren** met elke DPI die je nodig hebt—geen mysterie, gewoon duidelijke code.

## Wat je zult leren

- De exacte stappen om DPI te configureren vóór de conversie.
- Waarom DPI belangrijk is wanneer je **vector naar raster converteert**.
- Hoe je **SVG naar PNG kunt converteren** in één regel code.
- Tips voor het omgaan met grote SVG's en batchverwerking.
- Een volledig, compileerbaar programma dat je direct in je project kunt plaatsen.

## Vereisten

Voordat we beginnen, zorg ervoor dat je het volgende hebt:

- Java 17 of nieuwer (de nieuwste LTS‑versie werkt het beste).
- Maven of Gradle om de Aspose.HTML‑bibliotheek binnen te halen.
- Een eenvoudig SVG‑bestand dat je wilt rasteren (bijv. `logo.svg`).
- Een IDE of teksteditor—IntelliJ IDEA, VS Code, of zelfs een ouder Notepad volstaat.

Er zijn geen andere externe tools nodig; de bibliotheek doet al het zware werk.

## Stap 1: Voeg Aspose.HTML toe aan je project

Eerst en vooral heb je de Aspose.HTML JAR nodig. Als je Maven gebruikt, voeg dan dit fragment toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Voor Gradle ziet het er zo uit:

```groovy
implementation 'com.aspose:aspose-html:23.10'
```

> **Pro tip:** Gebruik altijd de nieuwste stabiele versie; nieuwere releases bevatten prestatie‑verbeteringen voor high‑DPI rendering.

## Stap 2: Hoe DPI in te stellen voor de conversie

Nu komen we bij het kernpunt—**hoe je DPI moet instellen**. Aspose.HTML biedt `ImageConversionOptions`, waarin je zowel de horizontale (`dpiX`) als verticale (`dpiY`) resolutie kunt opgeven. Beide op `300` instellen geeft je die klassieke afdruk‑kwaliteit dichtheid.

```java
import com.aspose.html.converters.ImageConversionOptions;
import com.aspose.html.rendering.Converter;

public class SvgHighRes {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create conversion options
        ImageConversionOptions conversionOptions = new ImageConversionOptions();

        // 2️⃣ Set target DPI for high‑resolution output (300 dpi → crisp print quality)
        conversionOptions.setDpiX(300);
        conversionOptions.setDpiY(300);

        // 3️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convertSvgToPng(
                "YOUR_DIRECTORY/logo.svg",        // source SVG
                "YOUR_DIRECTORY/logo_300dpi.png", // destination PNG
                conversionOptions);
    }
}
```

> **Waarom 300 dpi?** Het is de de‑facto standaard voor professioneel drukken. Als je een web‑klare afbeelding nodig hebt, is 72 dpi voldoende, maar voor flyers of brochures wil je minstens 300 dpi.

### Voorbeeldafbeelding

![Hoe DPI in te stellen bij het converteren van SVG naar PNG](https://example.com/placeholder.png "Hoe DPI in te stellen bij het converteren van SVG naar PNG")

*De bovenstaande afbeelding toont het verschil tussen een low‑DPI PNG (links) en een 300 dpi output (rechts).*

## Stap 3: Converteer SVG naar PNG – Een één‑regel code

Als je alleen een snelle **convert svg to png** wilt zonder te rommelen met DPI, kun je het opties‑object volledig overslaan:

```java
Converter.convertSvgToPng("logo.svg", "logo_default.png", null);
```

`null` doorgeven vertelt Aspose.HTML om de standaard DPI te gebruiken (meestal 96). Dit is handig voor miniaturen of wanneer je geen belang hecht aan afdrukkwaliteit.

## Stap 4: Verifieer het resultaat – Export SVG als PNG

Nadat de conversie is voltooid, open je de gegenereerde PNG in een willekeurige afbeeldingsviewer. Je zou een rasterafbeelding moeten zien die overeenkomt met de afmetingen van de oorspronkelijke vector, maar nu de DPI heeft die je hebt ingesteld. De meeste viewers tonen DPI in de afbeeldings‑eigenschappen; op Windows, rechts‑klikken → Eigenschappen → Details.

Als je de DPI programmatisch wilt verifiëren, kan Java’s `ImageIO` deze lezen:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File("logo_300dpi.png"));
int dpi = (int) img.getProperty("dpi");
System.out.println("Exported PNG DPI: " + dpi);
```

> **Opmerking:** Niet alle afbeeldingsformaten slaan DPI‑metadata op; PNG wel, maar JPEG kan extra verwerking vereisen.

## Randgevallen & Variaties

### 1️⃣ Verschillende DPI‑waarden

Je vraagt je misschien af: “Wat als ik 600 dpi nodig heb voor een grote poster?” Verander gewoon de getallen:

```java
conversionOptions.setDpiX(600);
conversionOptions.setDpiY(600);
```

Hogere DPI betekent een grotere bestandsgrootte, dus houd rekening met geheugenlimieten bij het verwerken van veel bestanden.

### 2️⃣ Batch‑conversie van een map

Als je tientallen SVG's hebt, wikkel je de conversie in een eenvoudige lus:

```java
File dir = new File("YOUR_DIRECTORY");
for (File svg : dir.listFiles((d, name) -> name.endsWith(".svg"))) {
    String pngName = svg.getName().replace(".svg", "_300dpi.png");
    Converter.convertSvgToPng(svg.getAbsolutePath(),
                              new File(dir, pngName).getAbsolutePath(),
                              conversionOptions);
}
```

Dit patroon **converteert vector naar raster** in massa, waardoor je uren handmatig werk bespaart.

### 3️⃣ Transparante achtergronden verwerken

Als je SVG transparantie bevat en je wilt een witte achtergrond, render dan eerst naar een `BufferedImage` en vul daarna de achtergrond:

```java
// Render SVG to BufferedImage with DPI
BufferedImage raster = Converter.convertSvgToImage(
        "logo.svg", conversionOptions);

// Fill background (optional)
Graphics2D g = raster.createGraphics();
g.setComposite(AlphaComposite.SrcOver);
g.setColor(Color.WHITE);
g.fillRect(0, 0, raster.getWidth(), raster.getHeight());
g.dispose();

// Write out PNG
ImageIO.write(raster, "png", new File("logo_whitebg.png"));
```

## Veelgestelde vragen

**V: Werkt dit op Linux?**  
A: Absoluut. Aspose.HTML is platform‑onafhankelijk; zorg er alleen voor dat je de juiste Java‑runtime hebt.

**V: Wat als mijn SVG externe afbeeldingen referereert?**  
A: Zorg ervoor dat die bronnen bereikbaar zijn via absolute paden of URL's; anders zal de renderer ze overslaan.

**V: Kan ik SVG naar andere rasterformaten zoals JPEG of BMP converteren?**  
A: Ja. Gebruik `Converter.convertSvgToJpeg` of `Converter.convertSvgToBmp` met dezelfde `ImageConversionOptions`.

## Pro‑tips voor rasterisatie van hoge kwaliteit

- **Stem DPI af op de uiteindelijke afmeting.** Een logo van 2 inch gedrukt op 300 dpi heeft een breedte van 600 px (2 in × 300 dpi). Schaal de SVG dienovereenkomstig vóór de conversie als je een specifieke pixelafmeting nodig hebt.
- **Let op het kleurprofiel.** PNG's embedden standaard geen ICC‑profielen; als kleurnauwkeurigheid belangrijk is, converteer dan naar TIFF of gebruik een bibliotheek die profiel‑embed ondersteunt.
- **Hergebruik het `ImageConversionOptions`‑object** bij het converteren van veel bestanden—dit voorkomt onnodige objectcreatie en kan de prestaties verbeteren.

## Conclusie

Je weet nu **hoe je DPI moet instellen** voor een SVG‑naar‑PNG‑conversie in Java, en je hebt gezien hoe dezelfde aanpak je **svg naar png kunt converteren**, **svg als png kunt exporteren**, en over het algemeen **vector naar raster kunt converteren** met volledige controle over de resolutie. Het volledige voorbeeld hierboven werkt direct, en de extra tips geven je een routekaart om de oplossing op te schalen naar projecten in de echte wereld.

Wat nu? Probeer de 300 dpi‑waarde te vervangen door 600 dpi, experimenteer met batchverwerking, of verken andere rasterformaten. Dezelfde principes gelden—verander gewoon de output‑methode en je bent klaar.

Heb je een lastige SVG of een prestatie‑vraag? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}