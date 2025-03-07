---
title: Ange PDF-sparalternativ för EPUB till PDF
linktitle: Ange PDF-sparalternativ för EPUB till PDF
second_title: Java HTML-bearbetning med Aspose.HTML
description: Lär dig hur du konverterar EPUB till PDF i Java med Aspose.HTML, ett kraftfullt HTML-manipuleringsbibliotek.
weight: 12
url: /sv/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ange PDF-sparalternativ för EPUB till PDF


## Introduktion

Aspose.HTML för Java är ett kraftfullt verktyg för att arbeta med HTML- och EPUB-dokument. I den här steg-för-steg-guiden går vi igenom processen att konvertera en EPUB-fil till PDF med Aspose.HTML för Java. Oavsett om du är en erfaren utvecklare eller precis har börjat, kommer denna handledning att ge dig de kunskaper och färdigheter som krävs för att utföra denna uppgift effektivt.

## Förutsättningar

Innan vi börjar, se till att du har följande förutsättningar på plats:

- Java-utvecklingsmiljö: Du måste ha en Java-utvecklingsmiljö inställd på ditt system.

-  Aspose.HTML for Java: Ladda ner och installera Aspose.HTML for Java-biblioteket. Du kan hitta biblioteket och relaterad dokumentation på[webbplats](https://releases.aspose.com/html/java/).

- EPUB-fil: Du behöver en EPUB-fil som du vill konvertera till PDF.

Låt oss nu dyka in i steg-för-steg-guiden för att konvertera EPUB till PDF med Aspose.HTML för Java.

## Steg 1: Öppna EPUB-filen

 Börja med att öppna en befintlig EPUB-fil för läsning. Du kan använda en`FileInputStream` för att uppnå detta. Här är koden för detta steg:

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Din kod för nästa steg kommer här.
}
```

## Steg 2: Definiera PDF-sparalternativ

 Skapa en instans av`PdfSaveOptions` med anpassad sidstorlek och bakgrundsfärg. Du kan konfigurera sidinställningarna enligt dina krav. Så här kan du göra det:

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

## Steg 3: Konvertera EPUB till PDF

 Ring nu`ConvertEPUB` metod för att konvertera EPUB-filen till PDF. Ange indataström, PDF-sparalternativ och utdataplats. Så här går det till:

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

Grattis! Du har framgångsrikt konverterat en EPUB-fil till PDF med Aspose.HTML för Java. Du kan nu komma åt den konverterade PDF-filen på den angivna utdataplatsen.

## Komplett källkod
```java
Specifying PDF Save Options for EPUB to PDF
        // Öppna en befintlig EPUB-fil för läsning.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Skapa en instans av PdfSaveOptions med en anpassad sidstorlek och en bakgrundsfärg.
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
            // Anropa ConvertEPUB-metoden för att konvertera EPUB till PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```


## Slutsats

den här handledningen har vi lärt oss hur man använder Aspose.HTML för Java för att konvertera EPUB-filer till PDF-format. Detta mångsidiga bibliotek ger utvecklare kraftfulla verktyg för dokumenthantering. Genom att följa stegen som beskrivs i den här guiden kan du sömlöst integrera EPUB till PDF-konvertering i dina Java-applikationer.

## Vanliga frågor (FAQs)

### Är Aspose.HTML för Java ett gratis bibliotek?
 Aspose.HTML för Java är ett kommersiellt bibliotek, men du kan få en gratis testversion från deras[webbplats](https://releases.aspose.com/).

### Vilka EPUB-format stöds för konvertering?
Aspose.HTML för Java stöder konvertering av olika EPUB-format, vilket säkerställer kompatibilitet med de flesta EPUB-dokument.

### Kan jag anpassa PDF-utdata ytterligare?
 Ja, du kan anpassa PDF-utdata genom att justera sidinställningarna, bakgrundsfärgen och andra inställningar i`PdfSaveOptions`.

### Finns det några begränsningar för testversionen av Aspose.HTML för Java?
Testversionen kan ha vissa begränsningar, så det rekommenderas att du kontrollerar dokumentationen för detaljer.

### Var kan jag få support för Aspose.HTML för Java?
Du kan hitta svar på dina frågor och söka stöd på[Aspose.HTML forum](https://forum.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
