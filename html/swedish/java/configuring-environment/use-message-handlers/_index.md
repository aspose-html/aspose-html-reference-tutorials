---
date: 2025-12-08
description: Lär dig hur du konverterar HTML till PNG med Aspose.HTML för Java samtidigt
  som du hanterar brutna länkar och fångar upp saknade resurser med hjälp av anpassade
  meddelandehanterare.
language: sv
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Hur man konverterar HTML till PNG och använder meddelandehanterare i Aspose.HTML
  för Java
url: /java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertera HTML till PNG med Aspose.HTML för Java – Använda meddelandehanterare

## Introduction  
I den här handledningen kommer du att lära dig **hur man konverterar HTML till PNG** med Aspose.HTML för Java och samtidigt **hantera brutna länkar** eller saknade resurser med en anpassad meddelandehanterare. Vi går igenom hur man skapar en enkel HTML‑fil, skriver den till disk, laddar den och fångar eventuella nätverksfel – perfekt för utvecklare som behöver pålitlig **html to image conversion** i produktionsklassade Java‑applikationer.

## Quick Answers
- **Vad täcker handledningen?** Konvertera HTML till PNG och hantera saknade resurser med en meddelandehanterare.  
- **Vilket bibliotek används?** Aspose.HTML för Java.  
- **Behöver jag en licens?** En tillfällig licens rekommenderas för provbyggen.  
- **Kan jag skriva HTML‑filen från Java?** Ja – se steget “write html file java”.  
- **Kommer hanteraren att fånga brutna länkar?** Absolut; den loggar alla svar som inte är 200.

## What is a Message Handler in Aspose.HTML?  
En meddelandehanterare är en krok i nätverksstacken som låter dig **fånga saknade resurser** (t.ex. en brutna bild‑URL) innan de orsakar ett undantag. Genom att inspektera svarskod kan du logga, ersätta eller försöka igen – vilket ger dig full kontroll över nätverksoperationer.

## Why Convert HTML to PNG?  
Att konvertera HTML till en bild är användbart för att skapa miniatyrer, e‑post‑förhandsgranskningar eller PDF‑liknande snapshots när du inte behöver en fullständig PDF‑konvertering. Aspose.HTML erbjuder en snabb, server‑sidig **html to image conversion**‑motor som fungerar utan en webbläsare.

## Prerequisites
1. **Java Development Kit (JDK)** – ladda ner från [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – hämta de senaste JAR‑filerna från [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse eller NetBeans.  
4. **Basic Java knowledge** – du bör vara bekväm med try‑with‑resources och objekt‑disposal.  
5. **Temporary license** (optional) – undvik provbegränsningar via en [temporary license](https://purchase.aspose.com/temporary-license/).

## Import Packages
Innan vi börjar, importera de nödvändiga Java‑klasserna:

```java
import java.io.IOException;
```

Dessa importeringar ger oss åtkomst till fil‑I/O och Aspose.HTML:s nätverks‑API:er.

## Step 1: Write the HTML File (write html file java)  
Skapa först ett litet HTML‑snutt som refererar till en bild som **inte finns**. Detta låter oss testa hanteraren.

```java
String code = "<img src='missing.jpg'>";
```

## Step 2: Persist the HTML to Disk  
Spara snutten till en fil som heter `document.html`. Denna fil kommer senare att laddas med Aspose.HTML‑motorn.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Step 3: Create a Custom Message Handler (catch missing resource)  
Nu definierar vi en hanterare som kontrollerar HTTP‑statuskoden. Om den inte är `200` loggar vi ett vänligt meddelande.

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

## Step 4: Register the Handler with the Network Service  
Lägg till den anpassade hanteraren i Aspose.HTML:s nätverkstjänst så att den deltar i varje begäran.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Step 5: Load the HTML Document (load html document java)  
När konfigurationen är klar, läs in HTML‑filen. Den saknade bilden kommer att trigga den hanterare vi just lagt till.

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

## Step 6: Convert HTML to PNG (convert html to png)  
Slutligen konverterar vi det inlästa dokumentet till en PNG‑bild. Detta demonstrerar hela **html to image conversion**‑arbetsflödet.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Step 7: Clean Up Resources  
Disposera alltid `Configuration`‑objektet för att frigöra inhemska resurser och undvika minnesläckor.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Common Pitfalls & Tips
- **Recursive invoke call:** Den anpassade hanteraren måste anropa `invoke(context);` *efter* din logik för att fortsätta kedjan. Att glömma detta kan stoppa andra hanterare från att köras.  
- **Missing license warnings:** Utan en giltig licens kan konverteringen lägga till ett vattenstämpel eller begränsa utskriftsstorleken.  
- **Path issues:** Säkerställ att `document.html` skrivs till arbetskatalogen eller ange en absolut sökväg.  

## Frequently Asked Questions

**Q: What is Aspose.HTML for Java?**  
A: Det är ett robust bibliotek som låter Java‑utvecklare skapa, manipulera och konvertera HTML‑dokument utan en webbläsare.

**Q: Why use message handlers in Aspose.HTML for Java?**  
A: De låter dig **handle broken links**, logga saknade resurser eller modifiera begäran/svar i realtid.

**Q: Can I chain multiple message handlers?**  
A: Ja—lägg till varje hanterare i listan `network.getMessageHandlers()`; de körs i den ordning de lades till.

**Q: Is disposing of Configuration and HTMLDocument objects required?**  
A: Absolut; disposering frigör inhemskt minne och förhindrar läckor i långlivade applikationer.

**Q: Besides missing images, what other errors can handlers manage?**  
A: Alla icke‑200 HTTP‑svar—timeout, 404‑sidor, autentiseringsfel osv.—kan avlyssnas och hanteras.

## Conclusion  
Du har nu ett komplett, produktionsklart exempel på **converting HTML to PNG** samtidigt som du **handling broken links** och **catching missing resources** med Aspose.HTML för Java. Inkorpora detta mönster i större projekt för att få fin‑granulerad kontroll över nätverksoperationer och generera pålitliga bild‑snapshotar av ditt HTML‑innehåll.

---

**Last Updated:** 2025-12-08  
**Tested With:** Aspose.HTML for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}