---
category: general
date: 2026-04-03
description: Konvertera HTML till PDF med Aspose.HTML i Java med anpassad PDF‑sidstorlek,
  ange PDF‑marginaler och ange PDF‑sidbredd. Lär dig hur du konverterar HTML snabbt.
draft: false
keywords:
- convert html to pdf
- custom pdf page size
- set pdf margins
- how to convert html
- set pdf page width
language: sv
og_description: Konvertera HTML till PDF med Aspose.HTML i Java. Den här guiden visar
  hur du ställer in anpassad PDF‑sidstorlek, marginaler och sidbredd för perfekta
  resultat.
og_title: Konvertera HTML till PDF – Anpassad sidstorlek och marginaler i Java
tags:
- Java
- PDF
- Aspose.HTML
title: Konvertera HTML till PDF – Anpassad sidstorlek och marginaler i Java
url: /sv/java/conversion-html-to-other-formats/convert-html-to-pdf-custom-page-size-margins-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera HTML till PDF – Anpassad sidstorlek och marginaler i Java

Har du någonsin behövt **konvertera HTML till PDF** och undrat hur du kan kontrollera sidans dimensioner? I den här handledningen går vi igenom en komplett, färdig‑att‑köra‑lösning som visar hur du **konverterar HTML till PDF** med en *anpassad PDF‑sidstorlek*, hur du **ställer in PDF‑marginaler**, och till och med hur du **ställer in PDF‑sidbredd** med Aspose.HTML för Java.  

Om du bygger fakturor, rapporter eller e‑böcker, är dessa layoutjusteringar skillnaden mellan en tråkig textmassa och ett polerat dokument som ser exakt ut som du vill ha det.

## Vad du kommer att lära dig

* Hur du sätter upp ett enkelt Maven/Gradle‑projekt med Aspose.HTML.
* Varför valet av rätt sidstorlek är viktigt för utskrift och skärmrendering.
* Steg‑för‑steg‑koden för att **konvertera HTML till PDF** samtidigt som du anpassar höjd, bredd och marginaler.
* Vanliga fallgropar (som saknade CSS‑media‑queries) och hur du undviker dem.
* Hur du verifierar att PDF‑filen har genererats korrekt.

Ingen tidigare erfarenhet av Aspose krävs—bara en grundläggande Java‑IDE och förmågan att köra en `main`‑metod.

## Förutsättningar

* **Java 17** (eller någon nyare JDK) installerad på din maskin.  
* **Aspose.HTML for Java**‑biblioteket – du kan hämta den senaste JAR‑filen från Maven Central (`com.aspose:aspose-html:23.9` vid skrivandet).  
* En enkel HTML‑fil (`input.html`) som du vill omvandla till en PDF.  
* Valfritt: en bildredigerare om du vill förhandsgranska PDF‑utdata.

> **Proffstips:** Om du använder Maven, lägg till beroendet nedan i din `pom.xml`. Om du föredrar Gradle fungerar samma koordinater med `implementation`‑konfigurationen.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

```groovy
// Gradle
implementation 'com.aspose:aspose-html:23.9'
```

## Konvertera HTML till PDF – Ställa in projektet

Först och främst: skapa en ny Java‑klass kallad `PdfConversionAdvanced`. Denna klass kommer att innehålla hela konverteringslogiken. Importerna du behöver listas högst upp i filen—känn dig fri att kopiera‑klistra dem direkt.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.converters.pdf.*;

public class PdfConversionAdvanced {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1: Point to the source HTML file you want to convert.
        // -----------------------------------------------------------------
        String inputHtmlPath = "YOUR_DIRECTORY/input.html";

        // -----------------------------------------------------------------
        // Step 2: Create PdfSaveOptions and configure custom page size.
        // -----------------------------------------------------------------
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // A5 size in points (1 pt = 1/72 inch). Adjust as needed.
        pdfOptions.setPageWidth(420);   // set pdf page width
        pdfOptions.setPageHeight(595);  // set pdf page height

        // -----------------------------------------------------------------
        // Step 3: Define margins – 10 mm ≈ 28.35 points.
        // -----------------------------------------------------------------
        pdfOptions.setMarginTop(28.35);
        pdfOptions.setMarginBottom(28.35);
        pdfOptions.setMarginLeft(28.35);
        pdfOptions.setMarginRight(28.35);

        // -----------------------------------------------------------------
        // Step 4: Make sure the converter uses the "print" media type.
        // -----------------------------------------------------------------
        pdfOptions.setMediaType("print");

        // -----------------------------------------------------------------
        // Step 5: Perform the conversion.
        // -----------------------------------------------------------------
        String outputPdfPath = "YOUR_DIRECTORY/output.pdf";
        Converter.convert(inputHtmlPath, outputPdfPath, pdfOptions);

        // -----------------------------------------------------------------
        // Step 6: Confirm the file was created.
        // -----------------------------------------------------------------
        System.out.println("PDF created with custom layout at " + outputPdfPath);
    }
}
```

### Varför dessa inställningar är viktiga

* **Anpassad PDF‑sidstorlek** (`setPageWidth` / `setPageHeight`) låter dig rikta in dig på A5, Letter eller någon skräddarsydd dimension du behöver. Om du hoppar över detta, använder Aspose som standard A4, vilket kan slösa papper eller förstöra en design.
* **Ställ in PDF‑marginaler** säkerställer att innehållet inte ligger direkt mot sidans kanter—kritiskt för skrivare som kräver en icke‑utskrivbar kant.
* **Media‑typ “print”** tvingar motorn att tillämpa all `@media print`‑CSS du har definierat, vilket ger dig fin‑granulär kontroll över typsnitt, färger och layout som skiljer sig från skärmvisningen.

## Definiera en anpassad PDF‑sidstorlek

Om standardstorleken A4 inte passar ditt projekt, kan du använda vilka dimensioner du vill. Kodsnutten ovan visar redan en klassisk A5‑layout, men låt oss utforska några alternativ:

| Storlek | Bredd (pt) | Höjd (pt) |
|------|------------|------------|
| **Letter** | 612 | 792 |
| **Legal** | 612 | 1008 |
| **Anpassad 8×10 tum** | 576 | 720 |

För att använda en anpassad storlek, ersätt helt enkelt värdena som skickas till `setPageWidth` och `setPageHeight`. Kom ihåg: **1 point = 1/72 tum**, så en snabb multiplikation ger dig rätt siffror.

> **Obs:** Om du behöver byta från stående till liggande, byt bara plats på bredd‑ och höjdvärden.

## Ställ in PDF‑marginaler för exakt layout

Marginaler uttrycks också i punkter. Exemplet använder **10 mm** (≈ 28,35 pt) på alla sidor. Vill du ha en tajtare layout? Ändra siffrorna:

```java
pdfOptions.setMarginTop(14.18);    // 5 mm
pdfOptions.setMarginBottom(14.18);
pdfOptions.setMarginLeft(21.26);   // 7.5 mm
pdfOptions.setMarginRight(21.26);
```

Varför bry sig? Skrivare har ofta ett minimalt utskrivningsområde—genom att sätta marginaler förhindras att innehåll klipps bort. Dessutom ger en enhetlig marginal ditt PDF ett professionellt utseende, särskilt när du genererar kontrakt eller certifikat.

## Justera PDF‑sidbredd (och höjd) dynamiskt

Ibland innehåller den HTML du får redan en breddhint (t.ex. en `<div>` stylad till 800 px). Du kan beräkna den erforderliga PDF‑bredden i farten:

```java
int htmlWidthPx = 800;                     // example from HTML
double pointsPerPixel = 0.75;              // 96 DPI => 0.75 pt per pixel
pdfOptions.setPageWidth(htmlWidthPx * pointsPerPixel);
```

Denna teknik säkerställer att PDF‑en speglar den ursprungliga layouten utan förvrängning. Det är ett praktiskt knep när du **hur man konverterar HTML** som ursprungligen var designad för skärmvisning.

## Kör konverteringen och verifiera resultatet

När du har ställt in allt, kör `main`‑metoden. Om allt är korrekt kopplat, kommer du att se:

```
PDF created with custom layout at YOUR_DIRECTORY/output.pdf
```

Öppna den resulterande PDF‑filen i någon visare (Adobe Reader, Chrome eller ditt operativsystems förhandsgranskning). Du bör se:

* Den exakta sidstorlek du definierade.
* Enhetliga marginaler runt innehållet.
* CSS tillämpad som om sidan skrevs ut (tack vare `setMediaType("print")`).

![Exempel på konvertering av HTML till PDF](https://example.com/convert-html-to-pdf-output.png "exempel på konvertering av html till pdf")

*Bildens alt‑text innehåller det primära nyckelordet för SEO.*

## Vanliga edge‑case & hur du hanterar dem

| Problem | Symptom | Lösning |
|-------|---------|-----|
| **Saknad CSS** | Texten ser enkel ut, utan typsnitt eller färger. | Se till att `pdfOptions.setMediaType("print")` är satt, och att din HTML länkar till stilarket med en absolut sökväg eller bäddar in CSS inline. |
| **Stora bilder avklippta** | Bilder blir avklippta vid sidans kanter. | Ändra storlek på bilder i HTML eller sätt `pdfOptions.setImageResolution(300)` för att öka DPI, justera sedan marginalerna. |
| **Unicode‑tecken renderas inte** | Specialtecken visas som rutor. | Lägg till ett typsnitt som stödjer tecknen och referera till det i din CSS (`@font-face`). |
| **Prestandafördröjning på stora dokument** | Konverteringen tar >30 sekunder. | Använd `pdfOptions.setEnableThreading(true)` (om stöds) eller dela upp HTML‑en i mindre delar och slå sedan ihop PDF‑erna senare. |

## Fullt fungerande exempel (allt tillsammans)

Här är hela filen som du kan släppa in i ett nytt projekt. Ersätt `YOUR_DIRECTORY` med en faktisk mappsökväg på din maskin.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.converters.pdf.*;

public class PdfConversionAdvanced {
    public static void main(String[] args) throws Exception {

        // Step 1: Source HTML location
        String inputHtmlPath = "C:/pdf-demo/input.html";

        // Step 2: Configure PDF options – custom size and margins
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setPageWidth(420);   // custom pdf page width (A5)
        pdfOptions.setPageHeight(595);  // custom pdf page height (A5)

        // Set margins – 10 mm ≈ 28.35 pt
        pdfOptions.setMarginTop(28.35);
        pdfOptions.setMarginBottom(28.35);
        pdfOptions.setMarginLeft(28.35);
        pdfOptions.setMarginRight(28.35);

        // Ensure print CSS is used
        pdfOptions.setMediaType("print");

        // Step 3: Destination PDF file
        String outputPdfPath = "C:/pdf-demo/output.pdf";

        // Step 4: Perform conversion
        Converter.convert(inputHtmlPath, outputPdfPath, pdfOptions);

        // Step 5: Confirmation
        System.out.println("PDF created with custom layout at " + outputPdfPath);
    }
}
```

Att köra detta program genererar `output.pdf` med de exakta dimensionerna och marginalerna du specificerade, vilket ger dig en

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}