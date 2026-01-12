---
date: 2026-01-02
description: Lär dig hur du konverterar EPUB till PDF i Java med Aspose.HTML samtidigt
  som du ställer in en anpassad PDF‑sidstorlek och andra PDF‑spara‑alternativ.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Anpassad PDF‑sidstorlek: ange PDF‑sparalternativ för EPUB till PDF'
url: /sv/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassad PDF-sidstorlek: Ange PDF‑sparalternativ för EPUB till PDF

## Introduktion

Aspose.HTML for Java gör det enkelt att **konvertera EPUB till PDF** och ger dig full kontroll över resultatet, inklusive att ange en **anpassad PDF‑sidstorlek**. I den här steg‑för‑steg‑guiden går vi igenom allt du behöver – från att förbereda din miljö till att justera `PdfSaveOptions` så att den genererade PDF‑filen matchar exakt de sidmått du kräver. Oavsett om du bygger en publiceringspipeline, en e‑learning‑plattform eller bara behöver automatisera dokumentkonvertering, kommer du att finna teknikerna här värdefulla.

## Snabba svar
- **Vad är huvudsyftet med den här handledningen?** Konvertera en EPUB‑fil till PDF samtidigt som en anpassad PDF‑sidstorlek tillämpas.  
- **Vilket bibliotek används?** Aspose.HTML for Java.  
- **Behöver jag en licens?** En gratis provversion finns tillgänglig; en kommersiell licens krävs för produktion.  
- **Kan jag ändra bakgrundsfärg?** Ja, med `PdfSaveOptions`.  
- **Stöds Java 8+?** Absolut – någon modern Java‑runtime fungerar.

## Vad är en anpassad PDF‑sidstorlek?

En anpassad PDF‑sidstorlek låter dig definiera exakt bredd och höjd för varje sida i den genererade PDF‑filen, istället för att förlita dig på standardstorlekar som A4 eller Letter. Detta är särskilt användbart för e‑böcker, flyers eller någon situation där den visuella layouten måste matcha en specifik design.

## Varför använda Aspose.HTML för konvertering från EPUB till PDF?

- **Hög noggrannhet:** Bevarar komplexa layouter, typsnitt och bilder.  
- **Finjusterad kontroll:** Justera sidstorlek, bakgrund, marginaler och mer via `PdfSaveOptions`.  
- **Plattformsoberoende:** Fungerar på Windows, Linux och macOS med samma Java‑kod.  
- **Prestanda:** Optimerad renderingsmotor för snabba konverteringar.

## Förutsättningar

Innan vi börjar, se till att du har:

- **Java‑utvecklingsmiljö:** JDK 8 eller senare installerad och konfigurerad.  
- **Aspose.HTML for Java:** Ladda ner den senaste JAR‑filen från [webbplatsen](https://releases.aspose.com/html/java/).  
- **EPUB‑fil:** En `.epub`‑dokument som du vill konvertera.  

Nu när allt är klart, låt oss dyka in i de faktiska konverteringsstegen.

## Steg 1: Öppna EPUB‑filen

Först måste vi öppna EPUB‑filen med en `FileInputStream`. Denna ström kommer att skickas till konverteraren senare.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Steg 2: Definiera PDF‑sparalternativ

Här ställer vi in den **anpassade PDF‑sidstorleken** och eventuell bakgrundsfärg. Justera pixelvärdena så att de matchar dina önskade dimensioner.

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

### Proffstips:
- **Pixlar vs. punkter:** `Length.fromPixels` konverterar skärm‑pixlar till PDF‑punkter (1 punkt = 1/72 tum). Välj värden som motsvarar den slutliga tryckstorleken du behöver.

## Steg 3: Konvertera EPUB till PDF

När inmatningsströmmen och de anpassade alternativen är klara, anropa konverteraren. Den genererade PDF‑filen sparas till den plats du anger.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Fullständig källkod

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
|-------|-------|-----|
| **PDF‑sidor är tomma** | Inmatningsström stängd före konvertering | Håll `try‑with‑resources`‑blocket öppet tills efter `convertEPUB`. |
| **Felaktiga sidmått** | Använder pixlar som inte motsvarar önskad tryckstorlek | Konvertera önskade tum till punkter (`1 tum = 72 punkter`) och sedan till pixlar med `Length.fromPixels`. |
| **Saknade typsnitt** | Typsnitt är inte inbäddade i EPUB | Säkerställ att typsnitten är paketerade i EPUB eller installera dem på värddatorn. |

## Vanliga frågor (FAQ)

### Är Aspose.HTML for Java ett gratis bibliotek?
Aspose.HTML for Java är ett kommersiellt bibliotek, men du kan få en gratis provversion från deras [webbplats](https://releases.aspose.com/).

### Vilka EPUB‑format stöds för konvertering?
Aspose.HTML for Java stödjer konvertering av olika EPUB‑format, vilket säkerställer kompatibilitet med de flesta EPUB‑dokument.

### Kan jag anpassa PDF‑utdata ytterligare?
Ja, du kan anpassa PDF‑utdata genom att justera sidinställningarna, bakgrundsfärgen och andra inställningar i `PdfSaveOptions`.

### Finns det några begränsningar i provversionen av Aspose.HTML for Java?
Provversionen kan ha vissa begränsningar, så det rekommenderas att kontrollera dokumentationen för detaljer.

### Var kan jag få support för Aspose.HTML for Java?
Du kan hitta svar på dina frågor och söka support på [Aspose.HTML‑forumet](https://forum.aspose.com/).

---

**Senast uppdaterad:** 2026-01-02  
**Testad med:** Aspose.HTML for Java 24.11 (senaste vid skrivande)  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}