---
date: 2026-08-28
description: Justera XPS-sidstorlek medan du konverterar HTML till XPS i Java med
  Aspose.HTML. Rendera HTML till XPS med exakta dimensioner.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: Justera XPS-sidstorlek
og_description: Justera XPS-sidstorlek medan du konverterar HTML till XPS i Java med
  Aspose.HTML. Lär dig rendera HTML till XPS med exakta dimensioner på några sekunder.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Justera XPS-sidstorlek vid konvertering av HTML till XPS i Java
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Justera XPS-sidstorlek vid konvertering av HTML till XPS i Java
url: /sv/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Justera XPS-sidstorlek vid konvertering av HTML till XPS i Java

I den här handledningen kommer du att lära dig **hur du justerar XPS-sidstorlek** när du konverterar HTML till XPS med Aspose.HTML för Java. Oavsett om du behöver utskrivbara fakturor, arkiveringsrapporter eller anpassade etiketter, ger kontrollen över sidmåtten en garanti för att den slutgiltiga XPS-filen ser exakt ut som avsett. Vi går igenom miljöinställning, renderingsalternativ och den slutgiltiga XPS-genereringen så att du kan bädda in denna funktion direkt i dina Java‑applikationer.

## Snabba svar
- **Vad betyder “convert HTML to XPS”?** Det renderar ett HTML‑dokument till en XPS‑fil och bevarar layout och stil.  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Vilken Java‑version stöds?** Java 8 eller högre (JDK 11+ rekommenderas).  
- **Kan jag ändra sidstorlek?** Ja – Aspose.HTML låter dig ange anpassade dimensioner innan rendering.  
- **Hur lång tid tar konverteringen?** Vanligtvis under en sekund för vanliga sidor; större dokument kan ta längre tid.

## Vad är konvertering av HTML till XPS?

Att konvertera HTML till XPS innebär att ta en webb‑orienterad markup‑fil och producera ett XPS‑dokument (XML Paper Specification) – ett fast layout‑, utskriftsklart format liknande PDF. Detta är användbart när du behöver högupplösta, enhetsoberoende dokument för arkivering eller utskrift från Java‑applikationer.

## Varför justera XPS-sidstorleken?

Att justera XPS‑sidstorleken ger dig kontroll över de fysiska dimensionerna på det slutgiltiga dokumentet (t.ex. A4, Letter, anpassade etiketter). Det förhindrar oönskad skalning, säkerställer att innehållet passar perfekt och kan minska filstorleken genom att eliminera onödigt vitt utrymme.

## Hur renderar man HTML till XPS med en anpassad sidstorlek?

Läs in din HTML, konfigurera `XpsRenderingOptions` med en `PageSetup` som definierar den exakta bredden och höjden du behöver, och rendera sedan till en `XpsDevice`. Detta tvåstegsförlopp låter dig behålla layouten intakt samtidigt som du påtvingar de dimensioner du anger, allt i ett enda API‑anrop.

## Förutsättningar

Innan vi börjar, se till att du har följande förutsättningar på plats:

1. **Java‑utvecklingsmiljö** – Java Development Kit (JDK) installerat på ditt system.  
2. **Aspose.HTML för Java‑bibliotek** – Ladda ner och inkludera Aspose.HTML för Java‑biblioteket i ditt projekt. Du kan hitta biblioteket på [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).  
3. **Inmatnings‑HTML‑fil** – Förbered en HTML‑fil som du vill rendera och justera XPS‑sidstorleken för. Du kan använda din egen HTML‑fil för den här handledningen.

## Importera paket

`Page`‑klassen representerar sidmått och inställningar för XPS‑utdata. `HtmlRenderer`‑klassen utför konverteringen från HTML till XPS.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Steg‑för‑steg‑guide

Nedan följer en kortfattad, numrerad genomgång som speglar de ursprungliga stegen samtidigt som extra kontext läggs till för tydlighet.

### Steg 1: ange indatafilens namn

`FileInputStream`‑klassen läser råa byte från en fil och tillhandahåller HTML‑källan till renderaren.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Steg 2: skapa ett HTML‑dokument och ange stilar

`HTMLDocument`‑klassen representerar ett HTML‑DOM i minnet som används av Aspose.HTML för rendering.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Steg 3: skapa XPS‑renderingsalternativ

`XpsRenderingOptions`‑klassen innehåller inställningar som styr hur HTML renderas till XPS, såsom sidstorlek och bildkvalitet.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Steg 4: justera sidstorleken  

**Hur man ställer in XPS‑sidstorlek** – Definiera en anpassad sidstorlek (bredd × höjd i punkter) och ange för renderaren om den automatiskt ska expandera till den bredaste sidan. Att sätta `adjustToWidestPage` till `false` bevarar de exakta dimensionerna du anger.

`PageSetup`‑klassen definierar sidstorlek, marginaler och orientering för XPS‑utdata.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Steg 5: rendera utdata

`XpsDevice`‑klassen är renderingsmålet som skriver det bearbetade innehållet till en XPS‑fil.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Vanliga problem och lösningar

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **Tom XPS‑utdata** | Inmatningsströmmen är inte stängd eller så pekar HTMLDocument på fel fil. | Se till att `FileInputStream` är korrekt inlindad i ett try‑with‑resources‑block och att filsökvägen är korrekt. |
| **Sidstorlek tillämpas inte** | `adjustToWidestPage` är kvar på `true`. | Sätt `pageSetup.setAdjustToWidestPage(false);` som visas i Steg 4. |
| **CSS stöds inte** | Aspose.HTML stödjer en delmängd av CSS. | Håll dig till grundläggande layout, typsnitt och färger; undvik avancerade selektorer eller CSS Grid. |
| **LicenseException** | Kör utan en giltig licens i produktion. | Applicera din temporära eller köpta licens innan rendering (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Vanliga frågor

**Q: Vad är Aspose.HTML för Java?**  
A: Aspose.HTML för Java är ett Java‑bibliotek som låter utvecklare manipulera och konvertera HTML‑dokument till olika format, såsom XPS, PDF och bilder. Du kan ladda ner biblioteket från [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).

**Q: Var kan jag ladda ner Aspose.HTML för Java?**  
A: Du kan ladda ner Aspose.HTML för Java‑biblioteket från [Aspose product releases page](https://releases.aspose.com/).

**Q: Finns det en gratis provversion av Aspose.HTML för Java?**  
A: Ja, du kan få en gratis provversion av Aspose.HTML för Java från [temporary license request page](https://purchase.aspose.com/temporary-license/).

**Q: Hur kan jag skaffa en temporär licens för Aspose.HTML för Java?**  
A: För att få en temporär licens för Aspose.HTML för Java, besök [temporary license request page](https://purchase.aspose.com/temporary-license/).

**Q: Kan jag få support för Aspose.HTML för Java?**  
A: Ja, du kan söka hjälp och support från Aspose‑communityn på [Aspose Forum](https://forum.aspose.com/).

**Q: Kan jag konvertera HTML till XPS på en huvudlös server?**  
A: Absolut. Aspose.HTML fungerar i miljöer utan GUI; se bara till att Java‑runtime är korrekt konfigurerad.

**Q: Stöder biblioteket anpassade sidmarginaler?**  
A: Ja. Använd `PageSetup.setMarginTop()`, `setMarginBottom()`, etc., innan du tilldelar `PageSetup` till renderingsalternativen.

## Slutsats

Vi har gått igenom hela processen för **konvertering av HTML till XPS** och **justering av XPS‑sidstorlek** med Aspose.HTML för Java. Genom att följa dessa steg kan du skapa utskriftsklara XPS‑dokument som matchar dina exakta layoutkrav. Känn dig fri att experimentera med olika sidmått, stilar eller till och med lägga till sidhuvuden och sidfötter för att passa ditt projekts behov.

Om du har några frågor eller behöver ytterligare hjälp, utforska [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) eller gå med i samtalet på [Aspose Forum](https://forum.aspose.com/).

---

**Senast uppdaterad:** 2026-08-28  
**Testad med:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Författare:** Aspose

## Relaterade handledningar

- [Konvertera HTML till XPS med Aspose.HTML för Java](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [Justera PDF‑sidstorlek med Aspose.HTML för Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [EPUB till XPS‑konvertering med Aspose.HTML för Java](/html/java/converting-epub-to-xps/convert-epub-to-xps/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}