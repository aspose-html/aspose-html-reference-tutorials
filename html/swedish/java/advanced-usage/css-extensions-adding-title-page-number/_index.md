---
date: 2025-12-05
description: Lär dig hur du ställer in HTML‑sidmarginaler i Java med Aspose.HTML och
  lägger till sidnummer och titlar i dina dokument.
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Hur man ställer in HTML‑sidmarginaler i Java med Aspose.HTML
url: /sv/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man ställer in HTML‑sidmarginaler i Java med Aspose.HTML

I den här handledningen kommer du att upptäcka **hur man ställer in HTML‑sidmarginaler i Java**‑stil med Aspose.HTML för Java. Vi går igenom att skapa anpassade sidmarginaler, infoga sidnummer och lägga till en dokumenttitel – allt med tydlig, steg‑för‑steg‑kod som du kan kopiera till ditt eget projekt.

## Snabba svar
- **Vilket bibliotek behövs?** Aspose.HTML for Java  
- **Kan jag kontrollera marginaler programatiskt?** Ja, via en CSS `@page`‑regel i användar‑stilmallen  
- **Vilka utdataformat stödjer marginaler?** XPS, PDF och andra rasterformat  
- **Behöver jag en licens för produktion?** En giltig Aspose.HTML‑licens krävs för icke‑testanvändning  
- **Är detta kompatibelt med Java 11+?** Absolut – biblioteket fungerar med moderna Java‑versioner  

## Vad är “Setting HTML Page Margins Java”?
Att ställa in HTML‑sidmarginaler i Java innebär att konfigurera renderingsmotorn (tillhandahållen av Aspose.HTML) för att tillämpa CSS‑page‑box‑egenskaper innan dokumentet konverteras till ett utskriftsformat som XPS eller PDF. Genom att definiera en anpassad `@page`‑regel styr du det utskrivbara området, sidnummer samt sidhuvud‑/sidfot‑innehåll.

## Varför använda Aspose.HTML för marginalkontroll?
- **Precise layout** – CSS `@page` ger dig pixel‑perfekt kontroll över marginaler, sidhuvuden och sidfötter.  
- **Cross‑format consistency** – Samma marginaldefinitioner fungerar för XPS, PDF och bildutdata.  
- **No browser dependency** – Rendering sker på server‑sidan, så du behöver ingen headless‑browser.  

## Förutsättningar

Innan vi börjar, se till att du har följande förutsättningar på plats:

1. **Java Development Environment** – JDK 11 eller senare installerat.  
2. **Aspose.HTML for Java** – Ladda ner och installera biblioteket från [here](https://releases.aspose.com/html/java/).  

## Importera paket

För att komma igång, importera de nödvändiga Aspose.HTML‑klasserna:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Hur man ställer in HTML‑sidmarginaler i Java – Steg‑för‑steg‑guide

### Steg 1: Initiera konfiguration och definiera anpassade sidmarginaler

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

I detta block skapar vi ett `Configuration`‑objekt, hämtar `IUserAgentService` och injicerar en CSS `@page`‑regel som definierar marginalerna, en nedre‑höger sidräknare och en över‑mitten dokumenttitel.

### Steg 2: Skapa HTML‑dokumentet

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Här instansierar vi ett `HTMLDocument` med ett enkelt “Hello World”‑snutt. Samma konfiguration från Steg 1 tillämpas, så de anpassade marginalerna respekteras när dokumentet renderas.

### Steg 3: Rendera till en XPS‑fil (eller någon annan stödd utdata)

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

Detta steg skapar en `XpsDevice` som skriver de renderade sidorna till `output.xps`. Marginalerna, sidnumren och titeln du definierade tidigare kommer att visas i den slutliga filen.

## Vanliga problem & tips
- **Margins appear unchanged** – Se till att `@page`‑regeln inte åsidosätts av andra stilmallar. Anropet `setUserStyleSheet` tvingar den till högsta prioritet.  
- **Page numbers show “NaN”** – Verifiera att du använder Aspose.HTML version 23.10 eller nyare; äldre versioner saknar funktionen `currentPageNumber()`.  
- **Output file is blank** – Bekräfta att sökvägen `Resources.output` löser sig korrekt och att du har skrivrättigheter.  

## Vanliga frågor

### Q1: Vad är Aspose.HTML för Java?

**A:** Aspose.HTML for Java är ett Java‑bibliotek som erbjuder kraftfulla verktyg för att arbeta med HTML‑dokument i Java‑applikationer, inklusive konvertering, rendering och manipulation.

### Q2: Kan jag anpassa sidmarginalerna ytterligare?

**A:** Ja, redigera bara CSS‑koden i `setUserStyleSheet`. Du kan ändra någon av `margin-*`‑värdena eller lägga till ytterligare `@top-*` / `@bottom-*`‑boxar.

### Q3: Hur kan jag lägga till mer innehåll i HTML‑dokumentet?

**A:** Ersätt strängen i `new HTMLDocument("<div>Hello World!!!</div>", …)` med din egen HTML‑markup, eller ladda en extern fil med hjälp av konstruktorn `HTMLDocument(String url, …)`.

### Q4: Är Aspose.HTML för Java kompatibelt med andra dokumentformat?

**A:** Absolut. Sam `HTMLDocument` kan renderas till PDF, XPS, bilder eller till och med EPUB genom att byta ut utmatningsenheten (t.ex. `PdfDevice`, `PngDevice`).

### Q5: Behöver jag en licens för att använda Aspose.HTML för Java?

**A:** Ja, en licens krävs för produktionsanvändning. Du kan få en provlicens eller köpa en licens från [here](https://purchase.aspose.com/buy) eller [here](https://releases.aspose.com/).

### Q6: Hur ställer jag in olika marginaler för udda och jämna sidor?

**A:** Använd pseudo‑klasserna `@page :left` och `@page :right` i din stilmall för att definiera separata marginaler för vänster‑hand (jämna) och höger‑hand (udda) sidor.

### Q7: Kan jag bädda in anpassade typsnitt i det renderade dokumentet?

**A:** Ja. Lägg till `@font-face`‑regler i användar‑stilmallen och referera till typsnitten i ditt HTML‑innehåll.

## Slutsats

Du har nu bemästrat **hur man ställer in HTML‑sidmarginaler i Java** med Aspose.HTML, och du vet hur du lägger till sidnummer och en titel för att få dina dokument att se professionella ut. Känn dig fri att experimentera med ytterligare `@page`‑boxar, anpassade typsnitt eller olika utdataformat för att passa ditt projekts behov.

Om du stöter på några problem, är den officiella [Aspose.HTML for Java-dokumentationen](https://reference.aspose.com/html/java/) och [Aspose supportforum](https://forum.aspose.com/) utmärkta platser för att få hjälp.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 23.12  
**Author:** Aspose  

---