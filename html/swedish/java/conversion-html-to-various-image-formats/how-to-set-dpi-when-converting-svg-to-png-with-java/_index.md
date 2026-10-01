---
category: general
date: 2026-02-14
description: Hur man ställer in DPI för konvertering från SVG till PNG med Java. Exportera
  högupplöst PNG, lär dig konvertera SVG till PNG och använda ett Java‑bildkonverteringsbibliotek.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: sv
og_description: Hur man ställer in DPI för konvertering från SVG till PNG med Java.
  Den här guiden visar hur du exporterar PNG med hög upplösning och använder ett Java‑bildkonverteringsbibliotek.
og_title: Hur man ställer in DPI när man konverterar SVG till PNG med Java
tags:
- java
- image-conversion
- svg
- png
title: Hur man ställer in DPI när man konverterar SVG till PNG med Java
url: /sv/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man ställer in DPI vid konvertering av SVG till PNG med Java

Har du någonsin undrat **how to set DPI** för en SVG‑till‑PNG‑konvertering så att resultatet ser skarpt ut på en utskriftsklar affisch? Du är inte ensam. I många projekt—tänk marknadsföringsflygblad, UI‑mock‑ups eller tekniska diagram—är det icke‑förhandlingsbart att få en högupplöst PNG från en SVG.  

I den här handledningen går vi igenom de exakta stegen för att **convert SVG to PNG**, **export high resolution PNG**, och, viktigast av allt, kontrollera DPI med Aspose.HTML for Java‑biblioteket. I slutet har du ett återanvändbart kodsnutt som du kan släppa in i vilken Java‑applikation som helst, oavsett om du bygger ett skrivbordsverktyg eller en backend‑tjänst.

## Vad du behöver

- **Java 8+** (koden kompileras med vilken recent JDK som helst)
- **Aspose.HTML for Java** JARs (tillgängliga från Maven Central eller Aspose‑webbplatsen)
- En SVG‑fil som du vill rasterisera  
- En liten dos nyfikenhet—inget annat.

Om du är bekväm med Maven, lägg bara till beroendet som visas i nästa avsnitt; annars, ladda ner JAR‑filerna manuellt och lägg till dem i din classpath.

## Steg 1: Lägg till Java‑bildkonverteringsbiblioteket

Först och främst—ditt projekt behöver **java image conversion library** som faktiskt kan läsa SVG och skriva PNG. Aspose.HTML är ett solidt val eftersom det hanterar CSS, typsnitt och komplexa vektorfunktioner direkt ur lådan.

**Maven‑användare** kan klistra in detta i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Gradle‑entusiaster** kan lägga till:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Om du föredrar den manuella vägen, ladda ner JAR‑filen från Aspose‑nedladdningssidan och lägg den i `libs/`, lägg sedan till den i ditt IDE:s byggsökväg.

> **Pro tip:** Håll ett öga på versionsnumret; nyare versioner förbättrar ofta DPI‑hantering och åtgärdar edge‑case‑buggar.

## Steg 2: Skapa konverteringsalternativ och ange önskad DPI

Nu när biblioteket är på plats måste vi berätta för det *hur* vi vill att den resulterande PNG‑filen ska se ut. Här kommer huvudnyckelordet—**how to set DPI**—in i bilden. Klassen `ImageConversionOptions` ger dig fin kontroll över både horisontell (`dpiX`) och vertikal (`dpiY`) upplösning.

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Varför 300 DPI? För de flesta utskriftsarbetsflöden anses 300 dots‑per‑inch vara “print quality”. Om du riktar dig mot enbart web‑tillgångar kan du sänka det till 72 eller 96 DPI för att hålla filstorlekarna små.

> **What if I need a different DPI for width and height?**  
> Ändra bara `setDpiX` och `setDpiY` oberoende av varandra. Biblioteket respekterar icke‑uniforma värden, vilket är praktiskt för anamorfiska bilder.

## Steg 3: Utför SVG‑till‑PNG‑konverteringen

Med alternativen klara är den faktiska konverteringen ett enda statiskt anrop. Vi kommer att använda `java.nio.file.Paths` för att hålla saker plattformsoberoende.

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

Det är allt—kör `main`‑metoden så hittar du en skarp, 300 DPI PNG i `YOUR_DIRECTORY`. Biblioteket skalar automatiskt vektorgrafiken för att matcha den DPI du angav, och bevarar bildförhållande och textklarhet.

## Steg 4: Verifiera resultatet (valfritt men rekommenderat)

En snabb kontroll kan spara dig huvudvärk senare. Öppna den genererade PNG‑filen i någon bildvisare som visar DPI‑metadata (t.ex. Photoshop, GIMP eller till och med Windows Explorers “Details”-flik). Du bör se **300 DPI** listat under horisontell och vertikal upplösning.

Om filen ser suddig ut, dubbelkolla:

1. Den ursprungliga SVG‑filen är inte lågupplöst från början (vektorfiler är upplösningsagnostiska, men inbäddade rasterbilder i dem kan begränsa kvaliteten).  
2. Du sparade verkligen filen efter att ha ställt in DPI—ibland cachar IDE:er gamla byggen.  
3. Konverteringsalternativen överskreds inte någon annanstans i din kod.

## Varför DPI är viktigt för Export High Resolution PNG

Du kanske undrar, “Varför bry sig om DPI alls? Är inte PNG bara pixlar?” Sanningen är att DPI är en *metadata*-tagg som talar om för efterföljande applikationer (särskilt de som är inriktade på utskrift) hur många pixlar som motsvarar en tum av fysisk yta. Om du ger en 1200 × 800 PNG till en skrivare utan korrekt DPI‑metadata kan skrivaren anta ett standardvärde (ofta 72 DPI) och förstora bilden, vilket resulterar i ett suddigt resultat.

Att ställa in DPI korrekt är också en prestandafördel: du undviker behovet av att skala upp rasterbilder senare, vilket kan vara beräkningsmässigt dyrt och försämra kvaliteten.

## Edge Cases & Vanliga fallgropar

| Situation | What to Watch For | How to Fix |
|-----------|-------------------|------------|
| **SVG innehåller inbäddade bitmapbilder** | Den inbäddade bitmap kan vara lågupplöst, vilket får den slutliga PNG‑filen att se pixelerad ut även vid hög DPI. | Byt ut bitmapen mot en högre upplösning eller redigera SVG:n så att den refererar till en extern bild. |
| **Stora DPI‑värden (t.ex. 1200 DPI)** | Minnesanvändningen skjuter i höjden; du kan få ett `OutOfMemoryError`. | Öka JVM‑heap‑storleken (`-Xmx2g`) eller begränsa DPI till ett rimligt maximum för ditt användningsfall. |
| **Icke‑kvadratiska pixlar** | Vissa skärmar tolkar DPI annorlunda, vilket leder till utdragna bilder. | Se till att `setDpiX` är lika med `setDpiY` om du inte har ett specifikt skäl att skilja dem åt. |
| **Saknade typsnitt** | Text i SVG:n kan falla tillbaka på ett standardtypsnitt, vilket ändrar layouten. | Bädda in typsnitten i SVG:n eller installera de nödvändiga typsnitten på körmaskinen. |

## Snabb sammanfattning (i en mening)

För att **how to set DPI** för en SVG‑till‑PNG‑konvertering, skapa ett `ImageConversionOptions`‑objekt, sätt `dpiX`/`dpiY` och anropa `Converter.convert` från Aspose.HTML Java‑biblioteket.

## Nästa steg & relaterade ämnen

- **Batch processing:** Loopa över en katalog med SVG‑filer och tillämpa samma DPI‑inställningar.  
- **Dynamic DPI:** Läs en konfigurationsfil eller kommandoradsargument för att sätta DPI vid körning.  
- **Alternative libraries:** Om du inte kan använda Aspose, överväg **Batik** (Apache) eller **SVG Salamander**, även om de kan kräva extra kod för att hantera DPI.  
- **Export high resolution PNG** för Android‑tillgångar: kombinera denna teknik med Androids `drawable‑hdpi`, `xhdpi` osv. mappar.

Känn dig fri att experimentera—prova 72 DPI för web‑miniatyrer, 600 DPI för storformatsskrivningar, eller till och med 150 DPI som ett mellanting. Koden förblir densamma; bara siffrorna ändras.

![hur man ställer in dpi](placeholder-image.png "Illustration av DPI-inställning i Java‑konverteringsflöde")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}