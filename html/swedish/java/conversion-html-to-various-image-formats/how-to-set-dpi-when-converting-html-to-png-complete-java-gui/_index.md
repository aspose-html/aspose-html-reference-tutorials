---
category: general
date: 2026-03-14
description: Lär dig hur du ställer in DPI när du konverterar HTML till PNG med Aspose.HTML.
  Inkluderar export av HTML som PNG, spara HTML som PNG och ersätta transparent bakgrund.
draft: false
keywords:
- how to set dpi
- convert html to png
- export html as png
- save html as png
- replace transparent background
language: sv
og_description: Hur man ställer in DPI vid konvertering av HTML till PNG med Aspose.HTML.
  Steg‑för‑steg‑guide för att exportera HTML som PNG, spara HTML som PNG och ersätta
  transparent bakgrund.
og_title: Hur man ställer in DPI när man konverterar HTML till PNG – Java‑handledning
tags:
- Java
- Aspose.HTML
- Image Export
title: Hur man ställer in DPI vid konvertering av HTML till PNG – Komplett Java‑guide
url: /sv/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png-complete-java-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man ställer in DPI när man konverterar HTML till PNG – Komplett Java‑guide

Har du någonsin undrat **hur man ställer in DPI** för en bild som genereras från HTML? Kanske förbereder du en utskrivbar rapport och standard‑96 DPI ser bara suddig ut på papper. Den goda nyheten är att du inte behöver leta efter obskyra bibliotek—Aspose.HTML gör det tunga arbetet, och du kan kontrollera upplösningen med bara några rader kod. I den här handledningen visar vi också hur du **konverterar HTML till PNG**, **exporterar HTML som PNG**, och till och med **ersätter transparent bakgrund** med en solid färg.

Vi går igenom allt du behöver: den nödvändiga Maven‑beroendet, en fullt körbar Java‑klass och tips för vanliga fallgropar. När du är klar har du en skarp 300 DPI PNG redo för högkvalitativ utskrift eller inbäddning i PDF‑filer.

## Förutsättningar

- Java 17 (eller någon nyare JDK)  
- Maven eller Gradle byggverktyg  
- Aspose.HTML för Java (du kan få en gratis provversion från Asposes webbplats)  
- En HTML‑fil som du vill omvandla till en bild (valfri giltig HTML fungerar)

> **Proffstips:** Om du använder en IDE som IntelliJ IDEA, aktivera “Show whitespaces” – det hjälper dig att upptäcka lösa mellanslag som kan bryta filvägar.

## Steg 1: Lägg till Aspose.HTML‑beroende

Först, tala om för Maven var biblioteket ska hämtas. Klistra in följande kodsnutt i din `pom.xml` inom `<dependencies>`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Om du föredrar Gradle, är motsvarigheten:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

> **Varför detta är viktigt:** Utan rätt version får du kompileringsfel som `cannot find class com.aspose.html.Conversion`. Biblioteket innehåller allt du behöver för HTML‑rendering, DPI‑hantering och bildsparande.

## Steg 2: Förbered din käll‑HTML och destinationssökvägar

Du kan placera HTML‑filen var som helst på disken, men håll sökvägen enkel för att undvika escapningsproblem. I detta exempel antar vi en mapp som heter `reports` i projektets rot:

```java
String htmlPath = "reports/report.html";   // source HTML
String pngPath  = "reports/report.png";    // output PNG
```

> **Edge case:** På Windows, använd framåtsnedstreck (`/`) eller dubbla bakåtsnedstreck (`\\`). Att blanda dem kan orsaka `FileNotFoundException`.

## Steg 3: Konfigurera PNG‑spara‑alternativ och ställ in DPI

Detta är kärnan i **hur man ställer in DPI**. Klassen `PngSaveOptions` exponerar `setDpiX` och `setDpiY`. Du kan också välja en bakgrundsfärg för att **ersätta transparent bakgrund**—användbart när HTML‑innehållet har semi‑transparenta element.

```java
// Create PNG save options
PngSaveOptions pngOptions = new PngSaveOptions();

// Set horizontal and vertical DPI – 300 is a common print resolution
pngOptions.setDpiX(300);
pngOptions.setDpiY(300);

// Replace any transparency with solid white (you could pick any Color)
pngOptions.setBackgroundColor(Color.getWhite());
```

> **Varför 300 DPI?** De flesta skrivare förväntar sig minst 300 DPI för skarpt resultat. Lägre värden ser bra ut på skärmar men blir suddiga när de skrivs ut.

## Steg 4: Utför konverteringen

Nu anropar vi den statiska metoden `Conversion.convert`. Den läser HTML‑filen, renderar den med den begärda DPI‑en och skriver PNG‑filen.

```java
Conversion.convert(htmlPath, pngPath, pngOptions);
System.out.println("PNG created with 300 DPI at: " + pngPath);
```

Om allt går bra ser du ett konsolmeddelande som bekräftar filens plats.

## Steg 5: Verifiera resultatet (valfritt men rekommenderat)

Öppna den genererade PNG‑filen i en bildvisare som visar DPI—Windows Photo Viewer, macOS Preview, eller till och med `identify` från ImageMagick:

```bash
identify -format "%x x %y DPI\n" reports/report.png
```

Du bör se `300 x 300 DPI`. Om siffrorna är annorlunda, dubbelkolla att du anropade `setDpiX/Y` **innan** konverteringen.

## Fullt, körklart exempel

Nedan är den kompletta Java‑klassen som sätter ihop alla delar. Kopiera‑klistra in den i en fil med namnet `HtmlToPngCustom.java` i `src/main/java/com/example`.

```java
package com.example;

import com.aspose.html.Conversion;
import com.aspose.html.saving.PngSaveOptions;
import com.aspose.html.drawing.Color;

/**
 * Demonstrates how to set DPI while converting HTML to PNG using Aspose.HTML.
 * The example also shows how to export HTML as PNG, save HTML as PNG, and
 * replace transparent background with white.
 */
public class HtmlToPngCustom {
    public static void main(String[] args) throws Exception {

        // Step 1: Source HTML and destination PNG paths
        String htmlPath = "reports/report.html";
        String pngPath  = "reports/report.png";

        // Step 2: Create PNG options and configure high‑resolution output
        PngSaveOptions pngOptions = new PngSaveOptions();
        pngOptions.setDpiX(300);                         // Horizontal DPI
        pngOptions.setDpiY(300);                         // Vertical DPI
        pngOptions.setBackgroundColor(Color.getWhite()); // Replace transparency with white

        // Step 3: Convert the HTML document to a PNG image using the defined options
        Conversion.convert(htmlPath, pngPath, pngOptions);

        // Step 4: Confirm that the image has been created
        System.out.println("PNG created with 300 DPI at: " + pngPath);
    }
}
```

När du kör detta program genereras `reports/report.png` med 300 DPI, där eventuella transparenta områden blir vita.

## Vanliga frågor & fallgropar

### 1. *Kan jag använda ett annat DPI‑värde?*  
Absolut. Byt bara ut `300` mot `150`, `600` eller vad ditt arbetsflöde kräver. Tänk på att högre DPI ökar minnesförbrukning och bearbetningstid.

### 2. *Vad händer om min HTML refererar till extern CSS eller bilder?*  
Aspose.HTML löser relativa URL:er baserat på HTML‑filens plats. Se till att alla resurser är åtkomliga, eller bädda in dem med data‑URI:er för att hålla konverteringen självständig.

### 3. *Hur ändrar jag bakgrundsfärgen?*  
Byt `Color.getWhite()` mot någon annan statisk metod (`Color.getBlack()`, `Color.getRed()`) eller skapa en egen RGB‑färg: `new Color(255, 215, 0)` för guld.

### 4. *Är utdata alltid PNG?*  
Du kan exportera till JPEG, BMP eller TIFF genom att använda motsvarande `*SaveOptions`‑klass (`JpegSaveOptions`, `BmpSaveOptions` osv.). DPI‑inställningsmönstret förblir detsamma.

## Proffstips för produktionsanvändning

- **Batch‑bearbetning:** Placera konverteringslogiken i en loop och mata in en lista med HTML‑filer. Kom ihåg att återanvända samma `PngSaveOptions`‑instans för att minska objekt‑churn.
- **Minneshantering:** För mycket stora sidor, överväg att öka JVM‑heapen (`-Xmx2g`) för att undvika `OutOfMemoryError`.
- **Trådsäkerhet:** `Conversion.convert` är trådsäker, så du kan parallellisera konverteringar med `ExecutorService` för högre genomströmning.

## Slutsats

Du vet nu **hur man ställer in DPI** när du **konverterar HTML till PNG**, hur du **exporterar HTML som PNG**, och hur du **ersätter transparent bakgrund** med en solid färg med Aspose.HTML för Java. Det kompletta, körbara exemplet ovan bör fungera direkt—släng bara din HTML‑fil i `reports`‑mappen och kör klassen.

Nästa steg kan vara att utforska **att spara HTML som PNG** med olika bildformat, eller integrera denna rutin i en webbtjänst som genererar PDF‑filer på begäran. Oavsett är byggstenarna desamma: konfigurera spara‑alternativen, ställ in DPI, och låt Aspose sköta renderingen.

Lycka till med kodandet, och må dina PNG‑filer alltid vara skarpa! 

![Diagram som visar DPI‑konverteringsflöde – hur man ställer in DPI när man konverterar HTML till PNG](/images/dpi-conversion-diagram.png){: .img-responsive alt="hur man ställer in dpi när man konverterar html till png"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}