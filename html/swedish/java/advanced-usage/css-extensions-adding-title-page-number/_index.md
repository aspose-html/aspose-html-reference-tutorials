---
title: Anpassa HTML-sidmarginaler med Aspose.HTML
linktitle: CSS-tillägg - Lägga till titel och sidnummer
second_title: Java HTML-bearbetning med Aspose.HTML
description: Lär dig hur du anpassar sidmarginaler, lägger till sidnummer och titlar till HTML-dokument med Aspose.HTML för Java.
weight: 10
url: /sv/java/advanced-usage/css-extensions-adding-title-page-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassa HTML-sidmarginaler med Aspose.HTML

Aspose.HTML for Java är ett kraftfullt bibliotek för bearbetning av HTML-dokument i Java-applikationer. I den här handledningen kommer vi att utforska hur du skapar anpassade sidmarginaler och lägger till sidnummer och titlar till dina HTML-dokument med Aspose.HTML för Java. Denna steg-för-steg-guide kommer att dela upp processen i hanterbara steg för att hjälpa dig att enkelt integrera dessa funktioner i dina HTML-dokument.

## Förutsättningar

Innan vi börjar, se till att du har följande förutsättningar på plats:

1. Java-utvecklingsmiljö: Se till att du har en Java-utvecklingsmiljö inställd på din dator.

2.  Aspose.HTML for Java: Ladda ner och installera Aspose.HTML for Java-biblioteket från[här](https://releases.aspose.com/html/java/).

## Importera paket

För att komma igång måste du importera nödvändiga paket från Aspose.HTML för Java. Lägg till följande importsatser till din Java-kod:

```java
// Importera Aspose.HTML-paket
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Låt oss nu dela upp processen att lägga till anpassade sidmarginaler, sidnummer och titlar i hanterbara steg:

## Steg 1: Initiera konfiguration och sidmarginaler

```java
// Initiera konfigurationsobjektet och ställ in sidmarginalerna för dokumentet
Configuration configuration = new Configuration();
try {
    // Skaffa tjänsten User Agent
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Ställ in stilen för anpassade marginaler och skapa märken på den
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

I det här steget initierar vi konfigurationsobjektet och ställer in anpassade sidmarginaler, inklusive positionen för sidräknaren och sidtiteln.

## Steg 2: Initiera ett HTML-dokument

```java
// Initiera ett HTML-dokument
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Här skapar vi ett HTML-dokument med ett exempel på innehåll (i det här fallet ett "Hello World"-meddelande) och tillämpar konfigurationen från steg 1.

## Steg 3: Initiera en utdataenhet och rendera dokumentet

```java
// Initiera en utenhet
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //Skicka dokumentet till utmatningsenheten
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

I det här steget ställer vi in en utdataenhet och renderar HTML-dokumentet. Dokumentet kommer att bearbetas och sparas som en XPS-fil med angivna sidmarginaler, sidnummer och titel.

## Slutsats

Grattis! Du har framgångsrikt lärt dig hur du skapar anpassade sidmarginaler och lägger till sidnummer och titlar till dina HTML-dokument med Aspose.HTML för Java. Denna anpassning låter dig skapa mer professionella och visuellt tilltalande dokument.

 Om du har några frågor eller stöter på några problem, besök gärna[Aspose.HTML för Java-dokumentation](https://reference.aspose.com/html/java/) eller sök hjälp på[Aspose supportforum](https://forum.aspose.com/).

## FAQ's

### F1: Vad är Aspose.HTML för Java?

S1: Aspose.HTML för Java är ett Java-bibliotek som tillhandahåller kraftfulla verktyg för att arbeta med HTML-dokument i Java-applikationer.

### F2: Kan jag anpassa sidmarginalerna ytterligare?

S2: Ja, du kan ändra CSS-stilarna i steg 1 för att anpassa sidmarginalerna enligt dina krav.

### F3: Hur kan jag lägga till mer innehåll i HTML-dokumentet?

S3: Du kan ändra HTML-innehållet i steg 2 genom att ersätta exempelinnehållet med ditt eget.

### F4: Är Aspose.HTML för Java kompatibelt med andra dokumentformat?

S4: Ja, Aspose.HTML för Java kan användas för att konvertera HTML-dokument till olika format, inklusive PDF, XPS och bilder.

### F5: Behöver jag en licens för att använda Aspose.HTML för Java?

 S5: Ja, du kan få en licens eller en gratis provperiod från[här](https://purchase.aspose.com/buy) eller[här](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
