---
title: Justera PDF-sidans storlek med Aspose.HTML för Java
linktitle: Justera PDF-sidans storlek
second_title: Java HTML-bearbetning med Aspose.HTML
description: Lär dig hur du justerar PDF-sidstorlek med Aspose.HTML för Java. Skapa högkvalitativa PDF-filer från HTML utan ansträngning. Kontrollera siddimensionerna effektivt.
type: docs
weight: 15
url: /sv/java/advanced-usage/adjust-pdf-page-size/
---

dagens digitala tidsålder ökar behovet av att generera högkvalitativa PDF-filer från HTML-innehåll. Aspose.HTML för Java är ett kraftfullt Java-bibliotek som låter dig konvertera HTML-dokument till PDF-format utan ansträngning. I den här handledningen kommer vi att fokusera på att justera sidstorleken när du konverterar HTML till PDF med Aspose.HTML för Java.

## Förutsättningar

Innan du börjar, se till att du har följande förutsättningar på plats:

- Java Development Environment: Se till att du har Java Development Kit (JDK) installerat på ditt system.
-  Aspose.HTML for Java: Du måste ladda ner och installera Aspose.HTML for Java från webbplatsen[här](https://releases.aspose.com/html/java/).
- HTML-dokument: Du bör ha ett HTML-dokument redo för konvertering. Om inte, skapa en eller använd en befintlig HTML-fil.

## Importera paket

För att börja måste du importera de nödvändiga paketen för att fungera med Aspose.HTML för Java. Följande kodavsnitt visar hur du gör detta:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Nu när du har förutsättningarna på plats och har importerat de nödvändiga paketen, låt oss dela upp processen för att justera PDF-sidans storlek i flera steg:

## Steg 1: Läsa HTML-innehåll

Först måste du läsa HTML-innehållet som du vill konvertera till PDF. I det här exemplet kommer vi att läsa HTML från en fil med namnet "FirstFile.html."

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Steg 2: Skriva HTML-innehåll

Därefter kommer du att skriva HTML-innehållet till en fil med namnet "FirstFileOut.html."

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Lägg till anpassade HTML-stilar eller innehåll här
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

## Steg 3: Återge HTML till PDF

Nu ska du återge HTML-innehållet till en PDF-fil. Vi kommer att täcka två scenarier: ett där sidstorleken inte anpassas till innehållets bredd och ett annat där den justeras.

### Sidstorlek ej justerad

I det här scenariot är sidstorleken inställd på en fast bredd och höjd, vilket kan beskära innehållet om det överskrider dessa dimensioner.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Skapa en HTMLDocument-instans från HTML-filen
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Ställ in alternativ för PDF-rendering
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Återge utgången
pdf_renderer.render(device, html_document);
```

### Sidstorlek anpassad till innehållsbredd

I det här scenariot justeras sidstorleken efter innehållets bredd.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Återge utgången
pdf_renderer.render(device, html_document);
```

## Slutsats

I den här handledningen har vi utforskat hur du justerar PDF-sidstorleken när du konverterar HTML till PDF med Aspose.HTML för Java. Du har lärt dig förutsättningarna, importerat de nödvändiga paketen och följt en steg-för-steg-guide för att uppnå denna uppgift. Med Aspose.HTML för Java kan du enkelt kontrollera sidstorleken på dina genererade PDF-filer, och se till att ditt innehåll visas som avsett.

 Experimentera gärna med olika sidstorlekar och inställningar för att möta dina specifika krav. Om du stöter på några problem eller har ytterligare frågor, tveka inte att söka hjälp från[Aspose.HTML för Java-dokumentation](https://reference.aspose.com/html/java/) eller den[Aspose supportforum](https://forum.aspose.com/).

## FAQ's

### F1: Vad är Aspose.HTML för Java?

S1: Aspose.HTML för Java är ett Java-bibliotek som låter dig arbeta med HTML-dokument, manipulera, konvertera och rendera dem till olika format, inklusive PDF.

### F2: Hur kan jag justera PDF-sidstorleken när jag konverterar HTML till PDF med Aspose.HTML för Java?

 S2: Du kan justera PDF-sidans storlek genom att använda`PageSetup` klass och ställa in`AdjustToWidestPage` egendom till`true` eller "false", beroende på dina krav.

### F3: Kan jag anpassa utformningen av HTML-innehåll innan jag konverterar det till PDF?

S3: Ja, du kan anpassa stilen genom att lägga till CSS- och HTML-element i ditt HTML-innehåll innan du konverterar det till PDF, som visas i handledningen.

### F4: Var kan jag hitta dokumentationen för Aspose.HTML för Java?

 S4: Du kan hänvisa till dokumentationen[här](https://reference.aspose.com/html/java/) för omfattande information och exempel.

### F5: Finns det en gratis testversion tillgänglig för Aspose.HTML för Java?

 S5: Ja, du kan få tillgång till en gratis testversion av Aspose.HTML för Java från[denna länk](https://releases.aspose.com/).