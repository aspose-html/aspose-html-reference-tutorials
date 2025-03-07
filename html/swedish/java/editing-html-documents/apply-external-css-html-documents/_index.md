---
title: Tillämpa extern CSS på HTML-dokument i Aspose.HTML för Java
linktitle: Tillämpa extern CSS på HTML-dokument i Aspose.HTML för Java
second_title: Java HTML-bearbetning med Aspose.HTML
description: Upptäck hur du applicerar extern CSS på HTML-dokument med Aspose.HTML för Java! Följ denna steg-för-steg-guide för en komplett handledning.
weight: 12
url: /sv/java/editing-html-documents/apply-external-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tillämpa extern CSS på HTML-dokument i Aspose.HTML för Java

## Introduktion
När du arbetar med HTML-dokument kan tillämpning av stilar göra stor skillnad i presentation och användarupplevelse. Om du dyker in i Java och vill lära dig hur du applicerar externa CSS-stilar på dina HTML-dokument med hjälp av Aspose.HTML-biblioteket, är du på rätt plats! Den här guiden syftar till att belysa processen steg-för-steg, vilket gör det enkelt även för dem som kanske är nya i Java eller CSS.
## Förutsättningar
Innan du dyker in i koden finns det några saker du måste ha på plats:
### 1. Java Development Kit (JDK)
 Se till att du har JDK installerat på din maskin. Du kan ladda ner den senaste versionen från[Oracles Java-webbplats](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML för Java
Du måste ha konfigurerat Aspose.HTML för Java. Om du inte har gjort detta än, gå till[Aspose nedladdningssida](https://releases.aspose.com/html/java/) och ta biblioteket.
### 3. En IDE- eller textredigerare
Välj en integrerad utvecklingsmiljö (IDE) som IntelliJ IDEA, Eclipse eller till och med en enkel textredigerare för att skriva din Java-kod.
### 4. Grundläggande kunskaper i Java
Bekantskap med Java-programmering och grunderna i CSS kommer säkerligen att hjälpa dig att följa med mer bekvämt.
## Importera paket
När du har ställt in allt är nästa steg att importera de nödvändiga paketen i ditt Java-projekt. Här är vad du behöver:
```java
import com.aspose.html.HTMLDocument;
```
Dessa importer gör att du kan manipulera HTML-dokument och rendera dem till olika format, till exempel PDF.

Vi delar upp vår handledning i hanterbara steg. Varje steg guidar dig genom processen att applicera externa CSS-stilar på ett HTML-dokument med Aspose.HTML för Java.
## Steg 1: Skapa ett HTML-dokument
Först och främst måste vi skapa vårt HTML-dokument. Vi börjar med att definiera innehållet med en enkel HTML-struktur.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Här definierade vi en grundläggande HTML-struktur, inklusive en`<div>` med två stycken. De`HTMLDocument` klass används för att skapa en dokumentrepresentation av vårt HTML-innehåll.
## Steg 2: Skapa ett stilelement
 Därefter kommer vi att skapa en`style` element för att hålla våra CSS-regler.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 Med hjälp av`createElement` metod för`HTMLDocument` , skapar vi en ny`<style>` element och ställ in dess innehåll så att det inkluderar våra CSS-definitioner för två klasser:`frame1` och`frame2`. Dessa klasser definierar marginaler, utfyllnad, dimensioner, bakgrundsfärger, teckensnittsfamiljer och textfärger.
## Steg 3: Lägg till stilen i dokumenthuvudet
Nu när vi har vår CSS på plats måste vi lägga till vårt stilelement i dokumentets huvud.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Vi hämtar huvudet på dokumentet och lägger till vårt nyskapade`style` element. Denna åtgärd integrerar effektivt vår CSS i HTML-dokumentet, vilket gör att den kan utforma vårt HTML-innehåll.
## Steg 4: Tillämpa klasser på HTML-element
Därefter kommer vi att tillämpa de tidigare definierade CSS-klasserna på våra paragrafelement.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Här kommer vi åt de första och sista styckeelementen i dokumentet och tilldelar dem CSS-klasserna vi skapade. Denna uppgift säkerställer att de följer de stilar som definieras i vår CSS.
## Steg 5: Ställ in ytterligare stilegenskaper
För att förbättra utseendet ytterligare kommer vi att ställa in ytterligare stilegenskaper för våra stycken.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

I det här steget finjusterar vi våra stilar. Det första styckets teckenstorlek ökas och centreras, medan det sista styckets färg, teckenstorlek och teckensnittsfamilj definieras. Denna förfining är avgörande för läsbarhet och estetisk tilltalande.
## Steg 6: Spara HTML-dokumentet
När vi har tillämpat våra stilar är det dags att spara HTML-dokumentet.
```java
document.save("edit-internal-css.html");
```

 Här använder vi`save` metod för`HTMLDocument` klass för att skriva det modifierade HTML-innehållet till en fil, och på så sätt bevara våra stilar och ändringar.
## Steg 7: Gör dokumentet till PDF
Låt oss slutligen göra dokumentet till ett PDF-format för utmatning.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 Med hjälp av`PdfDevice` klass, ställer vi in renderingen av vårt HTML-dokument till en PDF. Detta steg är nyckeln när du vill dela det formaterade dokumentet i ett universellt tillgängligt format.
## Slutsats
Och där har du det – att använda extern CSS på HTML-dokument med Aspose.HTML för Java är både enkelt och givande! Med bara några rader kod kan du förvandla vanlig text till visuellt tilltalande och professionellt utformade dokument. Så oavsett om du designar för personligt bruk, skapar rapporter eller utvecklar webbinnehåll, är det en kraftfull färdighet att ha i din verktygslåda att förstå hur man manipulerar HTML och CSS i Java.
## FAQ's
### Vad är Aspose.HTML för Java?
Aspose.HTML for Java är ett kraftfullt bibliotek som gör det möjligt för utvecklare att arbeta med HTML-dokument i Java-applikationer, vilket ger ett brett utbud av funktioner, från HTML-manipulation till rendering.
### Behöver jag en Internetanslutning för att använda Aspose.HTML?
Nej, när du har laddat ner de nödvändiga biblioteksfilerna kan du använda Aspose.HTML offline.
### Kan jag använda flera CSS-filer på ett HTML-dokument?
 Ja, du kan skapa flera`<link>` element och lägg till dem i dokumentets huvud för olika CSS-filer.
### Är det någon skillnad mellan intern och extern CSS?
Ja! Intern CSS definieras i ett HTML-dokument, medan extern CSS placeras i en separat fil och länkas till dokumentet.
### Hur kan jag få support för Aspose.HTML för Java?
 Du kan få tillgång till gemenskapsstöd via[Aspose forum](https://forum.aspose.com/c/html/29) för alla frågor eller problem du kan stöta på.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
