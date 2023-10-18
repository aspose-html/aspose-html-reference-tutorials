---
title: Justera XPS-sidans storlek med Aspose.HTML för Java
linktitle: Justera XPS-sidans storlek
second_title: Java HTML-bearbetning med Aspose.HTML
description: Lär dig hur du justerar XPS-sidans storlek med Aspose.HTML för Java. Styr utmatningsmåtten för dina XPS-dokument enkelt.
type: docs
weight: 16
url: /sv/java/advanced-usage/adjust-xps-page-size/
---

I den här handledningen kommer vi att guida dig genom processen att justera XPS-sidstorleken med Aspose.HTML för Java. Detta kraftfulla bibliotek låter dig manipulera HTML-dokument och rendera dem till olika format, inklusive XPS. Det är viktigt att justera sidstorleken när du behöver kontrollera utdatamåtten för ditt XPS-dokument.

## Förutsättningar

Innan vi börjar, se till att du har följande förutsättningar på plats:

1. Java Development Environment: Se till att du har Java Development Kit (JDK) installerat på ditt system.

2.  Aspose.HTML for Java Library: Du måste ladda ner och inkludera Aspose.HTML for Java-biblioteket i ditt Java-projekt. Du hittar biblioteket[här](https://releases.aspose.com/html/java/).

3. Inmatning av HTML-fil: Förbered en HTML-fil som du vill rendera och justera XPS-sidstorleken för. Du kan använda din egen HTML-fil för denna handledning.

## Importera paket

Först måste du importera de nödvändiga paketen för att fungera med Aspose.HTML för Java. Inkludera dessa paket i början av din Java-klass:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Steg 1: Ställ in indatafilens namn

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 I det här steget läser vi din HTML-indatafil med hjälp av en`FileInputStream`.

## Steg 2: Skapa ett HTML-dokument och ställ in stilar

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Detta steg innebär att skapa en`HTMLDocument` och lägga till stilar till det.

## Steg 3: Skapa XPS-renderingsalternativ

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Här skapar vi XPS-renderingsalternativ för att konfigurera renderingsprocessen.

## Steg 4: Justera sidstorleken

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Det här steget innebär att ställa in sidstorleken och ange om den ska anpassas till den bredaste sidan.

## Steg 5: Gör utdata

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

I det sista steget återger vi XPS-utdata med de konfigurerade alternativen.

## Slutsats

den här handledningen har vi visat dig hur du justerar XPS-sidstorleken med Aspose.HTML för Java. Du kan styra utmatningsmåtten för dina XPS-dokument och se till att de uppfyller dina specifika krav. Med den medföljande koden och stegen kan du enkelt implementera den här funktionen i dina Java-applikationer.

 Om du har några frågor eller behöver ytterligare hjälp, besök gärna[Aspose.HTML för Java-dokumentation](https://reference.aspose.com/html/java/) eller be om hjälp på[Aspose Forum](https://forum.aspose.com/).

## FAQ's

### F1: Vad är Aspose.HTML för Java?

S1: Aspose.HTML for Java är ett Java-bibliotek som låter utvecklare manipulera och konvertera HTML-dokument till olika format, som XPS, PDF och bilder.

### F2: Var kan jag ladda ner Aspose.HTML för Java?

 S2: Du kan ladda ner Aspose.HTML for Java-biblioteket från[den här länken](https://releases.aspose.com/html/java/).

### F3: Finns det en gratis testversion tillgänglig för Aspose.HTML för Java?

 S3: Ja, du kan få en gratis provversion av Aspose.HTML för Java från[här](https://releases.aspose.com/).

### F4: Hur kan jag få en tillfällig licens för Aspose.HTML för Java?

 S4: För att få en tillfällig licens för Aspose.HTML för Java, besök[denna sida](https://purchase.aspose.com/temporary-license/).

### F5: Kan jag få support för Aspose.HTML för Java?

 S5: Ja, du kan söka hjälp och stöd från Aspose-gemenskapen på[Aspose Forum](https://forum.aspose.com/).