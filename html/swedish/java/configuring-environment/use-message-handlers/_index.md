---
date: 2026-02-10
description: Lär dig hur du använder Aspose för att hantera trasiga länkar i Java,
  konvertera HTML till PNG och ladda HTML‑dokument i Java med Aspose.HTML för Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Konvertera HTML till PNG med Aspose.HTML‑meddelandehanterare i Java
url: /sv/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera HTML till PNG med Aspose.HTML Message Handlers i Java

## Introduction
I den här handledningen kommer du att upptäcka **hur man konverterar HTML till PNG** samtidigt som du elegant hanterar saknade resurser med Aspose.HTML för Java. Vi går igenom att skapa en liten HTML‑sida som pekar på en icke‑existerande bild, koppla en **custom message handler** för att **intercept network requests**, konfigurera **network service**, ladda dokumentet och slutligen utföra **html to image conversion**. I slutet har du ett robust mönster för både **handle broken links java** och högkvalitativ PNG‑utmatning—perfekt för rapporter, miniatyrer eller e‑postförhandsgranskningar.

## Quick Answers
- **Vad gör en message handler?** Den avbryter nätverksoperationer (som bildförfrågningar) och låter dig reagera på statuskoder såsom 404.  
- **Kan Aspose.HTML konvertera HTML till PNG?** Ja—`Converter.convertHTML` utför konverteringen i ett enda anrop.  
- **Behöver jag en licens för detta exempel?** En tillfällig licens tar bort utvärderingsbegränsningar; en permanent licens krävs för produktionsanvändning.  
- **Vilken Java‑version fungerar?** Alla JDK 8+ (exemplet körs på JDK 11).  
- **Kan jag konfigurera network service?** Absolut—använd `configuration.getService(INetworkService.class)` för att lägga till din handler.

## Prerequisites
Innan vi dyker ner, se till att du har följande redo:

1. **Java Development Kit (JDK)** – ladda ner från den [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – hämta biblioteket från den [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse eller NetBeans fungerar bra.  
4. **Basic Java knowledge** – du bör vara bekväm med klasser, try‑with‑resources och undantagshantering.  
5. **Temporary License** – om du använder en provversion, skaffa en [temporary license](https://purchase.aspose.com/temporary-license/) för att undvika vattenstämplar.

## Import Packages
Först importerar vi Java I/O‑klassen som vi behöver för filhantering. Resten av Aspose‑klasserna refereras med fullständiga namn senare, vilket håller importlistan prydlig.

```java
import java.io.IOException;
```

## Step 1: Prepare the HTML Code
Steg 1: Förbered HTML‑koden

Vi skapar ett minimalt HTML‑snutt som medvetet refererar till en saknad bild. Detta kommer att trigga vår handler när motorn försöker hämta resursen.

```java
String code = "<img src='missing.jpg'>";
```

## Step 2: Write the HTML Code to a File
Steg 2: Skriv HTML‑koden till en fil

Därefter sparar vi snutten till *document.html*. Att använda ett try‑with‑resources‑block garanterar att `FileWriter` stängs korrekt.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Step 3: Write a Custom Message Handler
Steg 3: Skriv en Custom Message Handler

Nu bygger vi en **custom message handler** som kontrollerar HTTP‑statusen för varje nätverksförfrågan. Om svaret inte är `200` loggar vi en vänlig varning. Observera anropet till `invoke(context);` i slutet—det vidarebefordrar förfrågan till nästa handler i kedjan, vilket förhindrar rekursion.

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

## Step 4: Configure the Network Service
Steg 4: Konfigurera Network Service

För att göra Aspose.HTML medveten om vår handler hämtar vi **network service** från en `Configuration`‑instans och lägger till handlern i dess samling. Detta är steget där vi **configure network service** för anpassat beteende.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Step 5: Load the HTML Document
Steg 5: Ladda HTML‑dokumentet

Med konfigurationen klar laddar vi *document.html*. Motorn använder nu vår network service, så förfrågan om den saknade bilden avbryts av den handler vi just lagt till.

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

## Step 6: Convert HTML to PNG
Steg 6: Konvertera HTML till PNG

Här är kärnan i processen för **html to image conversion**. Metoden `Converter.convertHTML` tar det laddade `HTMLDocument`, valfria `ImageSaveOptions` (där du kan justera DPI eller kvalitet) och filnamnet för utdata.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Step 7: Clean Up Resources
Steg 7: Rensa resurser

God Java‑praxis föreskriver att vi frigör alla inhemska resurser. `finally`‑blocket säkerställer att `Configuration` avyttras även om ett undantag kastas upp.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Why Use Message Handlers?
Varför använda Message Handlers?

Message handlers ger dig **fine‑grained control** över varje nätverksförfrågan—oavsett om det är en bild, CSS, JavaScript eller teckensnittsfil. Istället för att låta biblioteket misslyckas tyst kan du logga saknade resurser, tillhandahålla fallback‑innehåll eller till och med försöka igen. Detta gör din HTML‑bearbetningspipeline **robust**, **production‑ready** och enklare att felsöka.

## Common Issues and Solutions
Vanliga problem och lösningar

- **Handler recursion** – Anropa `invoke(context);` endast en gång för att undvika oändliga loopar.  
- **Missing license** – Utan en giltig licens kommer den genererade PNG‑filen att innehålla en vattenstämpel.  
- **Incorrect file paths** – Använd absoluta sökvägar eller ställ in arbetskatalogen korrekt när du laddar `document.html`.  
- **Unsupported resource types** – Säkerställ att den resurs du vill avbryta (bild, CSS osv.) faktiskt begärs av HTML‑motorn.

## Frequently Asked Questions

**Q: Kan jag kedja flera message handlers?**  
A: Ja, du kan lägga till flera handlers i samlingen `network.getMessageHandlers()`; de kommer att köras i den ordning de lades till.

**Q: Fungerar handlern för CSS‑ eller skriptresurser också?**  
A: Absolut—alla nätverksförfrågningar som görs av HTML‑motorn (bilder, CSS, JS, teckensnitt) passerar genom handlern.

**Q: Hur ändrar jag HTTP‑förfrågan innan den skickas?**  
A: Implementera en handler som modifierar `context.getRequest()` innan du anropar `invoke(context)`.

**Q: Finns det ett sätt att undertrycka varningen för specifika URL:er?**  
A: Inuti handlern, inspektera `context.getRequest().getRequestUri()` och hoppa villkorligt över loggningen.

**Q: Vilken version av Aspose.HTML krävs för dessa API:er?**  
A: Koden fungerar med Aspose.HTML for Java 22.10 och senare.

## Conclusion
Slutsats

Du har nu ett komplett, end‑to‑end‑exempel på **how to convert HTML to PNG** medan du använder en **custom message handler** för att **intercept network requests** och **handle broken links java**. Genom att konfigurera network service, ladda dokumentet och anropa konverteraren kan du på ett pålitligt sätt generera PNG‑miniatyrer eller helsidsskärmbilder i vilken Java‑applikation som helst.

---

**Senast uppdaterad:** 2026-02-10  
**Testad med:** Aspose.HTML for Java 24.11  
**Författare:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}