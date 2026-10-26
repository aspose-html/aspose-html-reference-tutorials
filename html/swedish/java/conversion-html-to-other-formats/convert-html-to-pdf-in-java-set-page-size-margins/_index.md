---
category: general
date: 2026-04-26
description: Konvertera HTML till PDF i Java med Aspose.HTML – lär dig hur du ställer
  in PDF‑sidstorlek, lägger till PDF‑marginaler och exporterar HTML som PDF på några
  rader.
draft: false
keywords:
- convert html to pdf
- set pdf page size
- add pdf margins
- export html as pdf
- how to set margins
language: sv
og_description: Konvertera HTML till PDF i Java med Aspose.HTML. Denna guide visar
  hur du ställer in PDF-sidstorlek, lägger till PDF-marginaler och exporterar HTML
  som PDF snabbt.
og_title: Konvertera HTML till PDF i Java – Ställ in sidstorlek och marginaler
tags:
- Java
- Aspose.HTML
- PDF conversion
title: Konvertera HTML till PDF i Java – Ställ in sidstorlek och marginaler
url: /sv/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-set-page-size-margins/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera HTML till PDF i Java – Ställ in sidstorlek och marginaler

Behöver du **convert HTML to PDF in Java**? Kämpar du med **set PDF page size** eller **add PDF margins**? Du är inte ensam. I många projekt måste den slutgiltiga PDF-filen matcha företagets varumärke, och det innebär exakta sidmått och prydliga marginaler.  

I den här handledningen går vi igenom ett komplett, färdigt att köra exempel som **export html as pdf** med Aspose.HTML-biblioteket. I slutet kommer du att veta *how to set margins* och varför PDF‑A‑1b‑kompatibilitet kan vara en livräddare för arkivering. Inga vaga referenser—bara koden du kan kopiera och klistra in och köra.

## Vad du behöver

- **Java 17** (eller någon recent JDK) – API:et fungerar med Java 8+ men nyare versioner ger bättre prestanda.  
- **Aspose.HTML for Java** JAR-filer – du kan hämta dem från Maven Central‑arkivet eller Aspose‑webbplatsen.  
- En enkel **input.html**‑fil som du vill omvandla till en PDF.  
- Lite diskutrymme för utdatafilen (PDF‑filen blir några hundra kilobyte).  

Det är allt. Inga extra ramverk, inga externa tjänster. Om du har dessa delar kan vi börja.

## Konvertera HTML till PDF – Steg‑för‑steg‑översikt

Nedan är den övergripande flödet vi kommer att följa:

1. **Point to the HTML source** – lokal fil, fjärr‑URL eller en `InputStream`.  
2. **Configure PDF saving options** – ställ in sidstorlek, marginaler och PDF‑A‑kompatibilitet.  
3. **Run the conversion** – låt Aspose göra det tunga arbetet.  

Varje steg är uppdelat i sin egen sektion, så att du kan plocka ut de delar du behöver.

## Steg 1: Ange HTML‑källan

Det första konvertern behöver är en referens till den HTML du vill omvandla till en PDF. Aspose.HTML är flexibel: du kan ge den en sökväg, en URL eller till och med en ström om din HTML finns i minnet.

```java
// Step 1 – Define where the HTML comes from
String htmlPath = "YOUR_DIRECTORY/input.html"; // replace with your actual file
```

> **Why this matters:** Att använda en enkel sträng håller exemplet enkelt, men i verkliga scenarier kan du hämta HTML från en webbtjänst eller en databas. API:et accepterar även `java.net.URL` eller `java.io.InputStream`, vilket är praktiskt när du inte vill skriva en temporär fil.

## Steg 2: Ställ in PDF‑sidstorlek

De flesta PDF‑filer har som standard storleken **Letter**, vilket kan se konstigt ut om din publik förväntar sig **A4**. Att ändra sidstorleken är en endaste rad med `PdfSaveOptions`.

```java
// Step 2 – Create PDF options and set the page size to A4
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PdfPageSize.A4); // this is the “set pdf page size” step
```

> **Pro tip:** Om du behöver en anpassad storlek (t.ex. ett kvittformat) låter Aspose dig skicka ett `SizeF`‑objekt med exakt bredd och höjd i punkter.

## Steg 3: Lägg till PDF‑marginaler

Marginaler håller ditt innehåll från att klänga sig fast vid sidans kant. De mäts i punkter (1 mm ≈ 2.8346 pt), men Aspose ger dig en praktisk `Margin`‑klass som accepterar millimeter direkt.

```java
// Step 3 – Define 20 mm margins on all sides (how to set margins)
pdfOptions.setMargins(new Margin(20, 20, 20, 20));
```

> **Why you care:** Utan marginaler kan rubriker bli avklippta vid utskrift, och sidfötter kan försvinna i skrivarens icke‑utskrivbara område. Enhetliga marginaler får även PDF‑filen att se professionell ut.

## Steg 4: Aktivera PDF‑A‑1b‑kompatibilitet (valfritt men rekommenderat)

Om du arkiverar dokument av juridiska eller regulatoriska skäl, säkerställer PDF‑A‑1b att filen är självständig och framtidssäker.

```java
// Step 4 – Make the PDF archival‑ready
pdfOptions.setPdfACompliance(PdfACompliance.PdfA1b);
```

> **Quick note:** PDF‑A‑kompatibilitet kan öka filstorleken något eftersom teckensnitt inbäddas. Det är ett litet pris att betala för långsiktig läsbarhet.

## Steg 5: Utför konverteringen

Nu när allt är konfigurerat är den faktiska konverteringen ett enda statiskt anrop. Aspose hanterar renderingsmotorn, CSS, JavaScript (om aktiverat) och bildinbäddning bakom kulisserna.

```java
// Step 5 – Convert the HTML to PDF using the configured options
Converter.convertHtmlToPdf(htmlPath, "YOUR_DIRECTORY/output.pdf", pdfOptions);
```

Det är hela programmet! Sätt ihop alla kodsnuttar så har du en körbar klass.

## Fullt fungerande exempel

Nedan är det kompletta Java‑programmet som du kan kopiera till `ConvertHtmlToPdfCustom.java`. Ersätt platshållar‑sökvägarna med faktiska platser på din maskin.

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPdfCustom {
    public static void main(String[] args) throws Exception {

        // Step 1: Specify the source HTML file (local file, URL, or stream)
        String htmlPath = "YOUR_DIRECTORY/input.html";

        // Step 2: Configure PDF output options
        //   • A4 page size
        //   • 20 mm margins on all sides
        //   • PDF‑A‑1b compliance for archival
        PdfSaveOptions pdfOptions = new PdfSaveOptions();
        pdfOptions.setPageSize(PdfPageSize.A4);
        pdfOptions.setMargins(new Margin(20, 20, 20, 20));
        pdfOptions.setPdfACompliance(PdfACompliance.PdfA1b);

        // Step 3: Convert the HTML to PDF using the configured options
        Converter.convertHtmlToPdf(htmlPath, "YOUR_DIRECTORY/output.pdf", pdfOptions);
    }
}
```

### Förväntat resultat

Att köra programmet skapar `output.pdf` som:

- Är **A4** (210 mm × 297 mm).  
- Har **20 mm** marginaler på vänster, höger, topp och botten.  
- Är **PDF‑A‑1b**‑kompatibel, vilket betyder att alla teckensnitt är inbäddade och filen är självständig.  
- Återskapar troget layouten av `input.html` (bilder, tabeller och CSS‑stilar bevaras).

Du kan öppna PDF‑filen i vilken visare som helst (Adobe Acrobat, Foxit eller till och med Chrome) och du bör se en ren sida med en bekväm vit kant runt innehållet.

![convert html to pdf output preview](/images/convert-html-to-pdf.png)

*Figur: En snabb titt på den genererade PDF‑filen efter konvertering.*

## Vanliga frågor och specialfall

### Vad händer om min HTML innehåller extern CSS eller bilder?

Aspose.HTML följer samma regler som webbläsare. Så länge URL‑erna är åtkomliga (absoluta eller relativa till HTML‑filens mapp) kommer konvertern att hämta dem. Om du kör koden på en server utan internetåtkomst, överväg att bädda in resurser som **data‑URI**‑strängar eller förladda dem i en `MemoryStream`.

### Hur konverterar jag en **URL** istället för en fil?

Byt helt enkelt ut `htmlPath`‑strängen mot en URL:

```java
String htmlPath = "https://example.com/report.html";
```

Samma `Converter.convertHtmlToPdf`‑överladdning kommer att ladda ner och rendera sidan.

### Kan jag ändra marginalenheterna till tum eller punkter?

Ja. `Margin`‑konstruktorn accepterar också `float left, float top, float right, float bottom` i **points**. Om du föredrar tum, multiplicera med 72 (1 tum = 72 pt). Till exempel, 0,5 tum marginaler blir `new Margin(36, 36, 36, 36)`.

### Vad händer om jag behöver en **annan sidorientering** (landskap)?

Ställ in `PageOrientation`‑egenskapen innan du anropar `setPageSize`:

```java
pdfOptions.setPageOrientation(PageOrientation.Landscape);
pdfOptions.setPageSize(PdfPageSize.A4);
```

### Finns det ett sätt att **lägga till ett sidhuvud/sidfot** automatiskt?

Aspose.HTML låter dig injicera HTML‑snuttar som fungerar som sidhuvuden eller sidfötter via `PdfPageTemplate`‑klassen. Du skapar ett litet HTML‑fragment med önskad text, och tilldelar det till `pdfOptions.getPageTemplate().setHeaderHtml(...)` (eller `.setFooterHtml(...)`). Det är ett eget ämne, men huvudpoängen är: du kan behandla sidhuvuden/sidfötter som vanlig HTML.

## Tips för produktionsklar kod

- **License the library** – the free

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}