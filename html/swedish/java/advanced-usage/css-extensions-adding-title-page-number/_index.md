---
date: 2026-06-24
description: Lär dig hur du konverterar HTML till PDF i Java med Aspose.HTML, ställer
  in sidomarginaler, lägger till sidnummer och sidhuvuden/sidfötter på ett effektivt
  sätt.
keywords:
- html to pdf java
- pdf from html java
- html to pdf tutorial
linktitle: CSS-utökningar - Lägga till titel och sidnummer
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to convert HTML to PDF Java with Aspose.HTML, set page margins,
    add page numbers and headers/footers efficiently.
  headline: How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML
  type: TechArticle
- description: Learn how to convert HTML to PDF Java with Aspose.HTML, set page margins,
    add page numbers and headers/footers efficiently.
  name: How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML
  steps:
  - name: Initialize Configuration and Define Custom Page Margins
    text: The `Configuration` object holds global settings for the rendering engine.
      By accessing its `IUserAgentService` you can inject a CSS style sheet that has
      the highest priority, ensuring your margins, header, and footer are applied.
  - name: Create the HTML Document
    text: '`HTMLDocument` represents a single HTML file in memory. When you pass the
      previously created `Configuration` to its constructor, the renderer automatically
      uses the custom `@page` rule you defined in Step 1.'
  - name: Render to an XPS File (or any supported output)
    text: '`XpsDevice` writes the rendered pages to an XPS container, but you can
      swap it for `PdfDevice` to get a PDF file instead. The same margin and footer
      definitions are honoured, so the output looks identical regardless of format.'
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java provides a complete HTML‑to‑PDF conversion engine.
    question: What library is needed?
  - answer: Yes – add a CSS `@page` rule to a user‑style sheet and the renderer respects
      it.
    question: Can I control margins programmatically?
  - answer: PDF, XPS, and raster image formats (PNG, JPEG) all honor the same `@page`
      definitions.
    question: Which output formats support margins?
  - answer: A valid Aspose.HTML license is required for any non‑trial deployment.
    question: Do I need a license for production?
  - answer: Absolutely – the library runs on Java 11, 17, and newer LTS releases.
    question: Is this compatible with Java 11+?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Hur man konverterar HTML till PDF i Java - Ställ in sidomarginaler med Aspose.HTML
url: /sv/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man konverterar HTML till PDF Java: Ställ in sidomarginaler med Aspose.HTML

I den här handledningen kommer du att upptäcka **hur man konverterar HTML till PDF Java**‑stil med Aspose.HTML för Java samtidigt som du lär dig att ange anpassade sidomarginaler, infoga sidnummer och lägga till en dokumenttitel. Vi går igenom tydliga, steg‑för‑steg‑instruktioner som du kan kopiera in i ditt eget projekt, så att du kan producera professionella PDF‑filer direkt från HTML på bara några minuter.

## Snabba svar
- **Vilket bibliotek behövs?** Aspose.HTML for Java tillhandahåller en komplett HTML‑till‑PDF konverteringsmotor.  
- **Kan jag kontrollera marginaler programatiskt?** Ja – lägg till en CSS `@page`‑regel i ett användar‑stilmall och renderaren respekterar den.  
- **Vilka utdataformat stödjer marginaler?** PDF, XPS och rasterbildformat (PNG, JPEG) följer alla samma `@page`‑definitioner.  
- **Behöver jag en licens för produktion?** En giltig Aspose.HTML‑licens krävs för alla icke‑testdistributioner.  
- **Är detta kompatibelt med Java 11+?** Absolut – biblioteket körs på Java 11, 17 och nyare LTS‑utgåvor.  
- **Kan jag lägga till sidnummer i Java?** Ja – använd `@bottom-right`‑rutan i CSS `@page`‑regeln för att infoga `counter(page)`.

## Vad är inställning av HTML‑sidomarginaler i Java?
Att ställa in HTML‑sidomarginaler i Java innebär att instruera Aspose.HTML:s renderingsmotor att tillämpa CSS‑`@page`‑egenskaper innan HTML‑innehållet rasteriseras till PDF eller XPS. Genom att definiera en anpassad `@page`‑regel styr du det utskrivbara området, lägger till sidnummer och infogar sidhuvud‑/sidfot‑innehåll – allt utan en webbläsare.

## Varför använda Aspose.HTML för marginalkontroll?
Aspose.HTML ger dig pixel‑perfekt server‑sidrendering som fungerar konsekvent över PDF-, XPS- och bildutdata. Det stödjer **50+ in‑ och utdataformat** och kan bearbeta dokument med flera hundra sidor utan att ladda hela filen i minnet, vilket ger konverteringshastigheter upp till **3 × snabbare** än headless‑browser‑lösningar på liknande hårdvara.

## Förutsättningar

Innan vi börjar, se till att du har följande förutsättningar på plats:

1. **Java‑utvecklingsmiljö** – JDK 11 eller senare installerat och `JAVA_HOME` konfigurerad.  
2. **Aspose.HTML for Java** – Ladda ner och installera biblioteket från [här](https://releases.aspose.com/html/java/).  
3. **En giltig licensfil** – Krävs för produktionsbyggen; en tillfällig testlicens fungerar för testning.  
4. Du kan också utforska alla Aspose‑utgåvor [här](https://releases.aspose.com/).

## Importera paket

`import`‑satserna importerar Aspose.HTML‑klasser till Java‑namnrymden så att du kan referera till dem utan fullt kvalificerade namn.

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Så konverterar du HTML till PDF Java med anpassade sidomarginaler

Läs in din HTML, tillämpa ett användar‑stilmall som definierar `@page`‑regeln och rendera dokumentet till PDF (eller XPS) i tre koncisa steg. Detta tillvägagångssätt eliminerar behovet av separat sidhuvud‑/sidfot‑kod och garanterar att marginalerna respekteras på alla sidor.

### Steg 1: Initiera konfiguration och definiera anpassade sidomarginaler

`Configuration`‑objektet innehåller globala inställningar för renderingsmotorn. Genom att komma åt dess `IUserAgentService` kan du injicera en CSS‑stilmall med högsta prioritet, vilket säkerställer att dina marginaler, sidhuvud och sidfot tillämpas.

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

### Steg 2: Skapa HTML‑dokumentet

`HTMLDocument` representerar en enskild HTML‑fil i minnet. När du skickar den tidigare skapade `Configuration` till dess konstruktor använder renderaren automatiskt den anpassade `@page`‑regeln du definierade i Steg 1.

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

### Steg 3: Rendera till en XPS‑fil (eller annat stödformat)

`XpsDevice` skriver de renderade sidorna till en XPS‑behållare, men du kan byta ut den mot `PdfDevice` för att få en PDF‑fil istället. Samma marginal‑ och sidfotdefinitioner respekteras, så utdata ser identisk ut oavsett format.

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

## Vanliga problem & tips

- **Marginalerna ser oförändrade ut** – Verifiera att ingen annan stilmall åsidosätter `@page`‑regeln. Anropet `setUserStyleSheet` tvingar din regel till högsta prioritet.  
- **Sidnummer visar “NaN”** – Detta sker med Aspose.HTML‑versioner äldre än 23.10, som saknar `counter(page)`‑funktionen. Uppgradera till den senaste versionen.  
- **Utdatafilen är tom** – Säkerställ att katalogen `Resources.output` finns och att Java‑processen har skrivrättigheter.  
- **Stora dokument orsakar hög minnesanvändning** – Använd streaming‑API:t (`XpsDevice` med `setPageCountLimit`) för att bearbeta sidor i batchar.  

## Vanliga frågor

### Q1: Vad är Aspose.HTML för Java?

**A:** Aspose.HTML for Java är ett server‑sidobibliotek som gör det möjligt för utvecklare att programatiskt skapa, redigera, rendera och konvertera HTML‑dokument, med stöd för PDF, XPS, bild och EPUB‑utdata.

### Q2: Kan jag anpassa sidomarginalerna ytterligare?

**A:** Ja – redigera CSS‑koden i `setUserStyleSheet`. Du kan ändra någon av `margin-*`‑värdena eller lägga till ytterligare `@top-*` / `@bottom-*`‑rutor för mer komplexa sidhuvuden eller sidfötter.

### Q3: Hur kan jag lägga till mer innehåll i HTML‑dokumentet?

**A:** Ersätt strängen i `new HTMLDocument("<div>Hello World!!!</div>", …)` med din egen markup, eller ladda en extern fil med hjälp av konstruktorn `HTMLDocument(String url, …)`.

### Q4: Är Aspose.HTML för Java kompatibel med andra dokumentformat?

**A:** Absolut. Samma `HTMLDocument` kan renderas till PDF, XPS, PNG, JPEG eller EPUB genom att byta ut utmatningsenheten (t.ex. `PdfDevice`, `PngDevice`).

### Q5: Behöver jag en licens för att använda Aspose.HTML för Java?

**A:** Ja, en licens krävs för produktionsanvändning. Du kan skaffa en provlicens eller köpa en licens från [här](https://purchase.aspose.com/buy) eller [här](https://releases.aspose.com/).

### Q6: Hur ställer jag in olika marginaler för udda och jämna sidor?

**A:** Använd pseudo‑klasserna `@page :left` och `@page :right` i ditt stilmall för att definiera olika marginaler för vänster‑hand (jämna) och höger‑hand (udda) sidor.

### Q7: Kan jag bädda in anpassade typsnitt i det renderade dokumentet?

**A:** Ja. Lägg till `@font-face`‑regler i användar‑stilmallen och referera till dessa typsnitt i din HTML‑markup; renderaren kommer att bädda in dem i den slutliga PDF‑ eller XPS‑filen.

## Slutsats

Du har nu ett komplett, produktionsklart recept för **hur man konverterar HTML till PDF Java** med Aspose.HTML, inklusive anpassade sidomarginaler, sidnummer och en dokumenttitel. Genom att utnyttja CSS‑`@page`‑regler får du full kontroll över layouten utan att skriva extra Java‑kod för sidhuvuden eller sidfötter. Experimentera med ytterligare `@page`‑rutor, anpassade typsnitt eller olika utmatningsenheter för att möta de exakta behoven i ditt rapport‑ eller faktureringssystem.

För djupare vägledning, konsultera den officiella [Aspose.HTML för Java-dokumentation](https://reference.aspose.com/html/java/) och gå med i communityn på [Aspose supportforum](https://forum.aspose.com/).

**Senast uppdaterad:** 2026-06-24  
**Testat med:** Aspose.HTML for Java 23.12  
**Författare:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Relaterade handledningar

- [Lägg till sidnummer med Aspose.HTML Java – Avancerad användning](/html/java/advanced-usage/)
- [Justera PDF‑sidstorlek med Aspose.HTML för Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Hur man konverterar HTML till PDF Java – Med Aspose.HTML för Java](/html/java/conversion-html-to-other-formats/convert-html-to-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}