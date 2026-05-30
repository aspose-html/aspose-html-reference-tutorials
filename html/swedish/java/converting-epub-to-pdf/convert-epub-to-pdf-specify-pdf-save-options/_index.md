---
date: 2026-05-30
description: Lär dig hur du konverterar EPUB till PDF i Java med Aspose.HTML samtidigt
  som du ställer in en anpassad PDF-sidstorlek och andra PDF-sparalternativ.
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: Specificera PDF-sparalternativ för EPUB till PDF
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Anpassad PDF-sidstorlek - Specificera PDF-sparalternativ för EPUB till PDF
url: /sv/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassad PDF-sidstorlek: Ange PDF‑sparalternativ för EPUB till PDF

## Introduktion

Aspose.HTML for Java gör det enkelt att **konvertera EPUB till PDF** och ger dig full kontroll över resultatet, inklusive att ange en **anpassad PDF-sidstorlek**. I den här steg‑för‑steg‑guiden går vi igenom allt du behöver—från att förbereda din miljö till att justera `PdfSaveOptions` så att den genererade PDF‑filen matchar exakt de sidmått du kräver. Oavsett om du bygger en publiceringspipeline, en e‑learning‑plattform eller bara behöver automatisera dokumentkonvertering, kommer du att finna teknikerna här värdefulla.

## Snabba svar
- **Vad är huvudsyftet med den här handledningen?** Konvertera en EPUB‑fil till PDF samtidigt som en anpassad PDF‑sidstorlek tillämpas.  
- **Vilket bibliotek används?** Aspose.HTML for Java.  
- **Behöver jag en licens?** En gratis provversion finns tillgänglig; en kommersiell licens krävs för produktion.  
- **Kan jag ändra bakgrundsfärg?** Ja, med `PdfSaveOptions`.  
- **Stöds Java 8+?** Absolut—vilken modern Java‑runtime som helst fungerar.

## Vad är en anpassad PDF‑sidstorlek?

En anpassad PDF‑sidstorlek låter dig definiera exakt bredd och höjd för varje sida i den genererade PDF‑filen, istället för att förlita dig på standardstorlekar som A4 eller Letter.  
Du kan ange dimensionerna i punkter (1 punkt = 1/72 tum) eller konvertera från pixlar, vilket ger dig pixel‑perfekt kontroll över den slutgiltiga layouten. Detta är idealiskt för e‑böcker, flygblad eller någon design som måste matcha ett fördefinierat format utan manuell efterbehandling.

## Varför använda Aspose.HTML för EPUB till PDF‑konvertering?

Aspose.HTML konverterar EPUB till PDF med två kodrader samtidigt som komplexa layouter, inbäddade typsnitt och högupplösta bilder bevaras. Det stödjer **50+ in‑ och utdataformat**, kan rendera PDF‑filer upp till **2 000 sidor** utan att ladda hela filen i minnet, och körs på Windows, Linux och macOS med identiska resultat. Biblioteket erbjuder också detaljerade PDF‑sparalternativ, så att du kan justera sidstorlek, bakgrundsfärg, marginaler och komprimeringsinställningar—allt från Java.

## Förutsättningar
- **Java‑utvecklingsmiljö:** JDK 8 eller senare installerad och konfigurerad.  
- **Aspose.HTML for Java:** Ladda ner den senaste JAR‑filen från [webbplatsen](https://releases.aspose.com/html/java/).  
- **EPUB‑fil:** Ett `.epub`‑dokument du vill konvertera.  

Nu när allt är klart, låt oss dyka ner i de faktiska konverteringsstegen.

## Så konverterar du EPUB till PDF med en anpassad sidstorlek?

`FileInputStream` är en Java‑klass som läser råa byte från en fil.  
`PdfSaveOptions` är en klass i Aspose.HTML som konfigurerar PDF‑utdatainställningar såsom sidstorlek och bakgrundsfärg.  
Läs in din EPUB med ett `FileInputStream`, konfigurera `PdfSaveOptions` för att ange de exakta sidmåtten, och anropa konverteraren. Det följande trestegs‑arbetsflödet utför konverteringen på under en minut för typiska e‑bokstorlekar, och det skalar till större samlingar med minimala kodändringar.

### Steg 1: Öppna EPUB‑filen

Först, skapa ett `FileInputStream` som pekar på din källa `.epub`. Att hålla strömmen öppen tills konverteringen är klar förhindrar fel med “tom sida”.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### Steg 2: Definiera PDF‑sparalternativ

`PdfSaveOptions` är Aspose.HTML:s konfigurationsklass som styr PDF‑utdatainställningar såsom sidstorlek, bakgrundsfärg och marginaler.  
`Length.fromPixels` konverterar skärm‑pixlar till PDF‑punkter (1 punkt = 1/72 tum), vilket låter dig ange dimensioner i välkända pixel‑enheter.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

#### Proffstips:
- **Pixlar vs. Punkter:** `Length.fromPixels` konverterar skärm‑pixlar till PDF‑punkter (1 punkt = 1/72 tum). Välj värden som motsvarar den slutliga tryckstorlek du behöver.

### Steg 3: Konvertera EPUB till PDF

Med indata‑strömmen och de anpassade alternativen klara, anropa konverteraren. Den genererade PDF‑filen sparas till den plats du anger, och bevarar exakt de sidmått du definierat.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` är en metod som möjliggör parallell bearbetning av sidor under PDF‑konvertering.

## Komplett källkod

Det fullständiga, körbara exemplet kombinerar de tre stegen ovan i en enda Java‑klass. Ersätt platshållar‑sökvägarna med dina egna filplatser.

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Vanliga problem och lösningar

| Problem | Orsak | Lösning |
|---------|-------|---------|
| **PDF‑sidor är tomma** | Indata‑strömmen stängdes före konvertering | Håll `try‑with‑resources`‑blocket öppet tills efter `convertEPUB`. |
| **Fel sidmått** | Använder pixlar som inte motsvarar önskad tryckstorlek | Konvertera önskade tum till punkter (`1 tum = 72 punkter`) och sedan till pixlar med `Length.fromPixels`. |
| **Saknade typsnitt** | Typsnitt inte inbäddade i EPUB | Säkerställ att typsnitten är paketerade i EPUB‑filen eller installera dem på värddatorn. |
| **Prestandaförsämring vid stora böcker** | Renderar varje sida sekventiellt | Aktivera flertrådad rendering via `PdfSaveOptions.setEnableParallelProcessing(true)` för snabbare bearbetning av EPUB‑filer med 500+ sidor. |

## Vanliga frågor (FAQ)

**Q: Är Aspose.HTML for Java ett gratis bibliotek?**  
A: Aspose.HTML for Java är ett kommersiellt bibliotek, men du kan få en gratis provversion från deras [webbplats](https://releases.aspose.com/).

**Q: Vilka EPUB‑format stöds för konvertering?**  
A: Aspose.HTML for Java stödjer EPUB 2.0, EPUB 3.0 och EPUB 3.1, och hanterar både flytande och fast layout‑böcker med fullt CSS‑stöd.

**Q: Kan jag anpassa PDF‑utdata ytterligare?**  
A: Ja, du kan anpassa PDF‑utdata genom att justera sidinställningarna, bakgrundsfärgen, komprimeringsnivån och andra inställningar i `PdfSaveOptions`.

**Q: Finns det några begränsningar i provversionen av Aspose.HTML for Java?**  
A: Provversionen kan lägga till ett vattenmärke på de första sidorna och begränsar maximal filstorlek till 10 MB; köp en licens för att ta bort dessa restriktioner.

**Q: Var kan jag få support för Aspose.HTML for Java?**  
A: Du kan hitta svar på dina frågor och söka support på [Aspose.HTML‑forumet](https://forum.aspose.com/).

---

**Senast uppdaterad:** 2026-05-30  
**Testad med:** Aspose.HTML for Java 24.11 (senaste vid skrivande)  
**Författare:** Aspose

## Relaterade handledningar

- [Justera PDF‑sidstorlek med Aspose.HTML för Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Hur man konverterar EPUB till PDF med Java – med Aspose.HTML](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [Konvertera EPUB till PDF och bilder med Aspose.HTML för Java](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}