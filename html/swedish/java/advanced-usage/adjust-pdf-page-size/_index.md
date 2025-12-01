---
date: 2025-12-01
description: Lär dig hur du justerar PDF‑sidstorlek, renderar HTML som PDF och genererar
  PDF från HTML med Aspose.HTML för Java. Kontrollera sidmått enkelt.
language: sv
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Justera PDF-sidstorlek med Aspose.HTML för Java
url: /java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Justera PDF‑sidstorlek med Aspose.HTML för Java

Att generera PDF‑filer från HTML är ett vanligt krav för rapporter, fakturor och e‑böcker. När du **justerar PDF‑sidstorlek** säkerställer du att det slutgiltiga dokumentet matchar den layout du designade i HTML. I den här handledningen lär du dig hur du renderar HTML som PDF, anger egna dimensioner och styr om sidan automatiskt ska expandera till det bredaste innehållet. Vi går igenom ett komplett, praktiskt exempel med Aspose.HTML för Java.

## Snabba svar
- **Vad betyder “justera PDF‑sidstorlek”?** Det låter dig definiera bredd och höjd för varje PDF‑sida eller låta renderaren automatiskt anpassa sig till det bredaste elementet.  
- **Vilket bibliotek används?** Aspose.HTML för Java (senaste versionen).  
- **Behöver jag en licens?** En gratis provversion fungerar för utveckling; en kommersiell licens krävs för produktion.  
- **Kan jag ändra dimensionerna programatiskt?** Ja – använd `PageSetup` och egenskapen `AdjustToWidestPage`.  
- **Är detta kompatibelt med Java 8+?** Absolut – API‑et fungerar med alla JDK 8 eller nyare.

## Vad är “justera PDF‑sidstorlek”?
Att justera PDF‑sidstorlek innebär att konfigurera dimensionerna för varje sida som HTML‑renderaren skapar. Du kan ange en fast storlek (t.ex. A4, Letter) eller låta renderaren beräkna optimal bredd baserat på innehållet. Detta ger dig exakt kontroll över layout, sidindelning och visuell trohet.

## Varför justera PDF‑sidstorlek vid konvertering från HTML till PDF?
- **Bevara designintentionen:** Förhindra att innehåll kapas av eller sträcks.  
- **Optimera för utskrift:** Matcha papperstorleken som krävs av efterföljande processer.  
- **Förbättra läsbarheten:** Undvik överdrivet vitt utrymme eller trång text.  
- **Dynamiska dokument:** Anpassa automatiskt breda tabeller eller bilder utan manuella beräkningar.

## Förutsättningar
Innan du börjar, se till att du har:

- **Java Development Kit (JDK) 8 eller högre** installerat på din maskin.  
- **Aspose.HTML för Java** – ladda ner den senaste JAR‑filen från den [officiella releasesidan](https://releases.aspose.com/html/java/).  
- **En HTML‑fil** som du vill konvertera (vi använder `FirstFile.html` i exemplet).  

## Importera paket
Först importerar vi de klasser vi behöver. Kodblocket nedan är oförändrat från den ursprungliga handledningen.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## Steg 1: Läs HTML‑innehållet
Vi läser käll‑HTML‑filen med en `FileInputStream`. Detta steg förbereder den råa markupen för senare manipulation.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Steg 2: Skriv (och eventuellt berika) HTML‑en
Här kopierar vi den ursprungliga HTML‑en till en ny fil och injicerar några inline‑stilar för att demonstrera hur styling påverkar PDF‑utdata. Byt gärna ut exempel‑CSS‑en mot din egen.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Steg 3: Rendera HTML till PDF – två scenarier
Nu ser vi hur man **genererar PDF från HTML** med två olika sidstorleksstrategier.

### 3.1 Sidstorlek **INTE** justerad efter innehållsbredd
I detta fall fixerar vi siddimensionerna (100 × 100 points). Om något element överskrider dessa gränser klipps det bort.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 Sidstorlek **JUSTERAD** efter innehållsbredd
Här aktiverar vi `AdjustToWidestPage`, så renderaren automatiskt expanderar sidbredden för att rymma det bredaste elementet medan höjden förblir fast.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## Hur man sätter PDF‑dimensioner (hur man ändrar PDF‑sidstorlek) i kod
`PageSetup`‑objektet är nyckeln:

- `setAnyPage(Page page)`: definierar basbredd × höjd.  
- `setAdjustToWidestPage(boolean)`: växlar automatisk breddökning.  

Genom att justera dessa två egenskaper kan du **sätta PDF‑dimensioner** för alla scenarier, oavsett om du behöver en statisk A4‑sida eller en dynamisk bredd som följer din HTML‑layout.

## Vanliga problem & tips
| Problem | Varför det händer | Lösning |
|---------|-------------------|---------|
| Innehåll kapas | Fast storlek är för liten | Öka `Size`‑värdena eller aktivera `AdjustToWidestPage`. |
| Text blir suddig | Renderings‑DPI är låg som standard | Använd `PdfRenderingOptions.setResolution(int dpi)` för att öka kvaliteten. |
| Stilar saknas | Extern CSS laddas inte | Bädda in CSS inline eller använd `HTMLDocument.setBaseUrl()` för att peka på din stilarksmapp. |
| Stora HTML‑filer ger OutOfMemoryError | Renderaren laddar hela dokumentet i minnet | Processa dokumentet i delar eller öka JVM‑heap (`-Xmx`). |

## Vanliga frågor

**Q: Vad är Aspose.HTML för Java?**  
A: Det är ett Java‑bibliotek som låter dig skapa, redigera och rendera HTML‑dokument, inklusive konvertering till PDF, PNG och andra format.

**Q: Hur kan jag justera PDF‑sidstorlek när jag konverterar HTML till PDF med Aspose.HTML för Java?**  
A: Använd `PageSetup`‑klassen och sätt `AdjustToWidestPage` till `true` (auto‑size) eller `false` (fast storlek). Tilldela sedan önskad `Size` via `new Page(new Size(width, height))`.

**Q: Kan jag anpassa styling av HTML‑innehållet innan konvertering till PDF?**  
A: Ja – du kan injicera CSS, ändra DOM eller använda externa stilark. Handledningen demonstrerar inline‑CSS‑injektion.

**Q: Var kan jag hitta dokumentationen för Aspose.HTML för Java?**  
A: Omfattande dokumentation finns [här](https://reference.aspose.com/html/java/).

**Q: Finns det en gratis provversion av Aspose.HTML för Java?**  
A: Absolut – ladda ner en provversion från [releases‑sidan](https://releases.aspose.com/html/java/).

## Slutsats
Du vet nu hur du **justerar PDF‑sidstorlek**, **renderar HTML som PDF** och **sätter egna PDF‑dimensioner** med Aspose.HTML för Java. Experimentera med olika sidstorlekar, DPI‑inställningar och CSS‑justeringar för att perfektionera utdata för ditt specifika användningsfall. Om du stöter på problem, se den officiella dokumentationen eller Aspose‑supportforumen.

---

**Senast uppdaterad:** 2025-12-01  
**Testat med:** Aspose.HTML för Java 24.12 (senaste)  
**Författare:** Aspose  
**Relaterade resurser:** [API‑referens](https://reference.aspose.com/html/java/) | [Ladda ner gratis provversion](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}