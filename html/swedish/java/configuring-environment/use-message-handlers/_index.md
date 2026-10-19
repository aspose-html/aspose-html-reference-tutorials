---
date: 2026-05-04
description: Lär dig hur du utför HTML‑till‑PNG‑konvertering, avlyssnar nätverksförfrågningar
  i Java och hanterar trasiga länkar i Java med Aspose.HTML för Java.
keywords:
- html to png conversion
- intercept network requests java
- html to image conversion
- load html document java
- handle broken links java
linktitle: Använd meddelandehanterare i Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: HTML till PNG‑konvertering med Aspose.HTML‑meddelandehanterare i Java
url: /sv/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML till PNG-konvertering med Aspose.HTML-meddelandeshanterare i Java

## Introduktion till HTML till PNG-konvertering
I den här handledningen kommer du att upptäcka **hur man konverterar HTML till PNG** samtidigt som du elegant hanterar saknade resurser med Aspose.HTML för Java. Vi går igenom att skapa en liten HTML‑sida som pekar på en icke‑existerande bild, ansluta en **anpassad meddelandehanterare** för att **avlyssna nätverksförfrågningar**, konfigurera **nätverkstjänsten**, ladda dokumentet och slutligen utföra **html‑till‑bild‑konvertering**. I slutet har du ett robust mönster för både **hantera trasiga länkar java** och högkvalitativ PNG‑utdata—perfekt för rapporter, miniatyrbilder eller e‑post‑förhandsvisningar.

## Snabba svar
- **Vad gör en meddelandehanterare?** Den avlyssnar nätverksoperationer (som bildförfrågningar) och låter dig reagera på statuskoder som 404.  
- **Kan Aspose.HTML konvertera HTML till PNG?** Ja—`Converter.convertHTML` utför konverteringen i ett enda anrop.  
- **Behöver jag en licens för detta exempel?** En tillfällig licens tar bort utvärderingsgränser; en permanent licens krävs för produktionsanvändning.  
- **Vilken Java‑version fungerar?** Alla JDK 8+ (exemplet körs på JDK 11).  
- **Kan jag konfigurera nätverkstjänsten?** Absolut—använd `configuration.getService(INetworkService.class)` för att lägga till din hanterare.

## Vad är HTML till PNG-konvertering?
HTML‑till‑PNG‑konvertering renderar en webbsida (eller ett HTML‑fragment) till en rasterbild. Detta är användbart när du behöver statiska förhandsvisningar av dynamiskt innehåll, skapa miniatyrbilder för e‑post‑nyhetsbrev eller arkivera webbsidor som bilder.

## Varför använda meddelandehanterare för att avlyssna nätverksförfrågningar i Java?
Meddelandehanterare ger dig **fin‑granulär kontroll** över varje nätverksförfrågan—oavsett om det är en bild, CSS, JavaScript eller ett teckensnitt. Genom att avlyssna dessa förfrågningar kan du **logga saknade resurser**, tillhandahålla reservinnehåll eller till och med försöka ladda ner igen misslyckade filer, vilket gör din HTML‑bearbetningspipeline **robust** och **produktionsklar**.

## Förutsättningar
1. **Java Development Kit (JDK)** – ladda ner från [Oracle‑webbplatsen](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – hämta biblioteket från [Aspose releases‑sidan](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse eller NetBeans fungerar bra.  
4. **Grundläggande Java‑kunskaper** – du bör vara bekväm med klasser, try‑with‑resources och undantagshantering.  
5. **Tillfällig licens** – om du använder en provversion, skaffa en [tillfällig licens](https://purchase.aspose.com/temporary-license/) för att undvika vattenstämplar.

## Importera paket
Först importerar vi Java I/O‑klassen som vi behöver för filhantering. Resten av Aspose‑klasserna refereras med fullständiga namn senare, vilket håller importlistan prydlig.

```java
import java.io.IOException;
```

## Steg 1: Förbered HTML‑koden
Vi skapar ett minimalt HTML‑snutt som medvetet refererar till en saknad bild. Detta kommer att trigga vår hanterare när motorn försöker hämta resursen.

```java
String code = "<img src='missing.jpg'>";
```

## Steg 2: Skriv HTML‑koden till en fil
Därefter sparar vi snutten till *document.html*. Genom att använda ett try‑with‑resources‑block garanteras att `FileWriter` stängs korrekt.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Steg 3: Skriv en anpassad meddelandehanterare
Nu bygger vi en **anpassad meddelandehanterare** som kontrollerar HTTP‑statusen för varje nätverksförfrågan. Om svaret inte är `200` loggar vi en vänlig varning. Observera anropet till `invoke(context);` i slutet—det vidarebefordrar förfrågan till nästa hanterare i kedjan och förhindrar rekursion.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## Steg 4: Konfigurera nätverkstjänsten
För att göra Aspose.HTML medveten om vår hanterare hämtar vi **nätverkstjänsten** från en `Configuration`‑instans och lägger till hanteraren i dess samling. Detta är steget där vi **konfigurerar nätverkstjänsten** för anpassat beteende.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Steg 5: Ladda HTML‑dokumentet
När konfigurationen är klar laddar vi *document.html*. Motorn använder nu vår nätverkstjänst, så förfrågan om den saknade bilden avlyssnas av den hanterare vi just lagt till.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## Steg 6: Konvertera HTML till PNG
Här är kärnan i processen för **html‑till‑bild‑konvertering**. Metoden `Converter.convertHTML` tar det laddade `HTMLDocument`, valfria `ImageSaveOptions` (där du kan justera DPI eller kvalitet) och filnamnet för utdata.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Steg 7: Rensa resurser
God Java‑praxis föreskriver att vi frigör alla inhemska resurser. `finally`‑blocket säkerställer att `Configuration` avyttras även om ett undantag kastas upp.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Vanliga problem och lösningar
- **Hanterarrekursion** – Anropa `invoke(context);` endast en gång för att undvika oändliga slingor.  
- **Saknad licens** – Utan en giltig licens kommer den genererade PNG‑filen att innehålla en vattenstämpel.  
- **Felaktiga filsökvägar** – Använd absoluta sökvägar eller ställ in arbetskatalogen korrekt när du laddar `document.html`.  
- **Ej stödda resurstyp** – Säkerställ att den resurs du vill avlyssna (bild, CSS, etc.) faktiskt begärs av HTML‑motorn.

## Vanliga frågor

**Q: Kan jag kedja flera meddelandehanterare?**  
A: Ja, du kan lägga till flera hanterare i samlingen `network.getMessageHandlers()`; de kommer att köras i den ordning de lades till.

**Q: Fungerar hanteraren även för CSS‑ eller skriptresurser?**  
A: Absolut—alla nätverksförfrågningar som görs av HTML‑motorn (bilder, CSS, JS, teckensnitt) passerar genom hanteraren.

**Q: Hur ändrar jag HTTP‑förfrågan innan den skickas?**  
A: Implementera en hanterare som modifierar `context.getRequest()` innan du anropar `invoke(context)`.

**Q: Finns det ett sätt att undertrycka varningen för specifika URL:er?**  
A: Inom hanteraren, inspektera `context.getRequest().getRequestUri()` och hoppa över loggningen villkorsbaserat.

**Q: Vilken version av Aspose.HTML krävs för dessa API:er?**  
A: Koden fungerar med Aspose.HTML för Java 22.10 och senare.

---

**Senast uppdaterad:** 2026-05-04  
**Testad med:** Aspose.HTML for Java 24.11  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}