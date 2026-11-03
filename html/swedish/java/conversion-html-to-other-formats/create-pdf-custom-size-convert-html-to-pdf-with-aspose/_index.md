---
category: general
date: 2026-03-26
description: Skapa PDF med anpassad storlek från HTML med Aspose.HTML för Java. Lär
  dig hur du konverterar HTML till PDF och ställer in PDF-sidans storlek på bara några
  steg.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: sv
og_description: Skapa PDF med anpassad storlek från HTML med Aspose. Den här guiden
  visar hur du konverterar HTML till PDF, ändrar PDF‑sidstorlek och ställer in PDF‑sidstorlek
  enkelt.
og_title: Skapa PDF i anpassad storlek – Snabbguide för att konvertera HTML till PDF
tags:
- aspose
- java
- pdf
- html
title: Skapa PDF i anpassad storlek – Konvertera HTML till PDF med Aspose
url: /sv/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa PDF med anpassad storlek – Konvertera HTML till PDF med Aspose

Har du någonsin behövt **skapa PDF med anpassad storlek** från en HTML‑fil? I den här handledningen visar vi dig hur du **konverterar HTML till PDF** och ställer in PDF‑sidstorlek med Aspose.HTML för Java.  

Om du bygger fakturor, rapporter eller e‑böcker är det viktigt att få exakt sidstorlek—annars blir layouten felplacerad eller klipps av.  

Vi går igenom varje steg, från att läsa in käll‑HTML till att justera marginaler, och avslutar med en färdig PDF. Inga vaga referenser, bara ett komplett, körbart exempel som du kan kopiera‑klistra idag.

## Vad du behöver

- **Java 17** (eller någon nyare JDK).  
- **Aspose.HTML for Java** JAR‑filer – du kan hämta den senaste versionen från Maven‑arkivet eller Aspose‑webbplatsen.  
- En enkel `input.html`‑fil placerad i en mapp du kontrollerar.  
- En IDE eller textredigerare du föredrar; jag kodar vanligtvis i IntelliJ IDEA, men Eclipse fungerar lika bra.

Att ha dessa förutsättningar betyder att du inte får “class not found”-fel halvvägs.  

Nu, låt oss dyka ner.

![Exempel på PDF med anpassad storlek](/images/create-pdf-custom-size.png "Skärmbild som visar en PDF genererad med anpassad sidstorlek och marginaler – create pdf custom size")

## Skapa PDF med anpassad storlek – Grundsteg

Nedan är det fullständiga Java‑programmet du kommer att få. Kopiera det gärna till en fil som heter `ConvertHtmlToPdfCustomPage.java` och kör den efter att du har lagt till Aspose‑beroenden i ditt projekt.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### Steg 1 – Konvertera HTML till PDF: Ladda dokumentet

Det första vi gör är att **ladda HTML** som vi vill omvandla till en PDF.  
`HTMLDocument` läser filen, löser relativa länkar och bygger ett DOM som Aspose kan rendera.  

> **Varför detta är viktigt:** Om HTML‑filen refererar till CSS eller bilder kommer Aspose att hämta dem relativt till filsökvägen. Att använda en absolut sökväg (`YOUR_DIRECTORY/input.html`) undviker “file not found”-överraskningar.

### Steg 2 – Ändra PDF‑sidstorlek: Konfigurera alternativ

Här skapar vi ett `PdfConversionOptions`‑objekt.  
- `setPageSize(PageSize.A4)` instruerar Aspose att använda standard A4‑dimensionerna (210 × 297 mm).  
- `setPageOrientation(...)` roterar sidan om du behöver liggande läge.  
- `setMargins(new Margin(20, 20, 20, 20))` ger en marginal på 20 punkt på varje sida.

Du kan ersätta `PageSize.A4` med `PageSize.LETTER` eller till och med en **anpassad storlek** genom att skicka ett `SizeF`‑objekt, t.ex.:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **Proffstips:** En punkt motsvarar 1/72 tum. Om du räknar i millimeter, multiplicera med 2,83465 för att få punkter.

### Steg 3 – Generera PDF från HTML: Köra konverteringen

`Converter.convertHTML` gör det tunga arbetet. Den tar det inlästa `HTMLDocument`, utsökvägen och de alternativ vi just konfigurerade.  

Om du vill **ställa in PDF‑sidstorlek** dynamiskt baserat på innehållet, kan du beräkna de nödvändiga dimensionerna innan detta steg och justera `pdfOptions` därefter.

### Steg 4 – Verifiera resultatet

`System.out.println`‑raden är valfri, men den ger snabb återkoppling när du kör programmet från en konsol. Efter körning, öppna `custom_page.pdf` – du bör se en A4‑stående PDF med enhetliga 20‑punkt‑marginaler, exakt som vi angav.

## Konvertera HTML till PDF – Vanliga variationer

### Använda en ström istället för en filsökväg

Ibland har du ingen fysisk fil; kanske kommer HTML‑en från en databas eller ett API. I så fall omsluter du strängen i en `ByteArrayInputStream`:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

Det andra argumentet är bas‑URL:en för att lösa relativa resurser.

### Ändra sidorientering

Om din rapport är bred, byt till liggande läge:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### Finjustera marginaler

Marginaler accepterar flyttal, så du kan sätta 0,5 pt för en hårtunn kant:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### Hantera stora HTML‑filer

För enorma dokument, överväg att aktivera **minnes‑effektiv strömning**:

```java
pdfOptions.setUseMemoryCache(true);
```

Detta instruerar Aspose att skriva mellanstegsdatan till temporära filer istället för att hålla allt i RAM.

## Ställ in PDF‑sidstorlek – Edge Cases & Fallgropar

- **Saknade typsnitt:** Om din HTML använder ett anpassat typsnitt som inte är installerat på servern, kommer PDF‑en att falla tillbaka på ett standardtypsnitt. Bädda in typsnittet med `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);`.  
- **Bildskalning:** Högupplösta bilder kan göra PDF‑en stor. Använd `pdfOptions.setImageResolution(150);` för att minska upplösningen samtidigt som kvaliteten bevaras.  
- **CSS‑kompatibilitet:** Inte alla CSS‑egenskaper stöds fullt ut. Håll dig till standardlayouttekniker (flexbox fungerar, men grid kan ha egenheter).  
- **Sökvägsbehörigheter:** Säkerställ att processen har skrivbehörighet till `YOUR_DIRECTORY`. Annars kastas ett `IOException`.

## Förväntad utdata

När programmet körs genereras en PDF som ser ut så här (konceptuell illustration):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- Sidstorlek: **A4** (210 × 297 mm).  
- Orientering: **Stående**.  
- Marginaler: **20 pt** på varje sida.  

Öppna filen med någon PDF‑visare (Adobe Reader, Chrome, etc.) för att bekräfta.

## Sammanfattning

Du vet nu hur du **skapar PDF med anpassad storlek** från en HTML‑källa med Aspose.HTML för Java. Handledningen täckte hela kedjan: **konvertera HTML till PDF**, **ändra PDF‑sidstorlek**, **ställa in PDF‑sidstorlek**, och **generera PDF från HTML** med anpassade marginaler.  

Känn dig fri att experimentera—byt `PageSize.LETTER` mot legal‑storlek, justera marginaler eller bädda in egna typsnitt. Därefter kan du utforska **lägga till vattenstämplar**, **kryptera PDF‑en**, eller **batch‑processa flera HTML‑filer**. Alla dessa ämnen bygger på samma grundläggande koncept som vi just gått igenom.

Har du en fråga om ett specifikt edge case? Lämna en kommentar nedan, så hjälper jag dig att felsöka. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}