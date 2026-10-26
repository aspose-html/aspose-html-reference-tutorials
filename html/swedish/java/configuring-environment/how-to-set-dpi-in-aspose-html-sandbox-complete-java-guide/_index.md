---
category: general
date: 2026-04-02
description: Lär dig hur du ställer in DPI, viewportstorlek och user agent i Aspose.HTML
  Sandbox. Steg‑för‑steg Java‑exempel med fullständig kod och tips.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: sv
og_description: Behärska hur du ställer in DPI, viewport‑storlek och user agent i
  Aspose.HTML Sandbox med ett komplett Java‑exempel.
og_title: Hur man ställer in DPI i Aspose.HTML Sandbox – Java‑handledning
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Hur man ställer in DPI i Aspose.HTML Sandbox – Komplett Java‑guide
url: /sv/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man ställer in DPI i Aspose.HTML Sandbox – Komplett Java‑guide

Har du någonsin funderat **hur man ställer in DPI** när man renderar en webbsida med Aspose.HTML? Du är inte ensam. I många testscenarier behöver du att layouten matchar en specifik skärm‑densitet—tänk utskriftsklara PDF‑filer eller högupplösta skärmdumpar. Den goda nyheten är att Aspose.HTML‑sandboxen låter dig kontrollera DPI, viewport‑storlek och till och med user‑agent‑strängen i ett praktiskt paket.

I den här handledningen går vi igenom ett praktiskt Java‑exempel som **ställer in DPI**, **ställer in viewport‑storlek** och **ställer in user‑agent** på en gång. I slutet har du ett körbart program, förstår varför varje inställning är viktig och är redo att finjustera sandboxen för dina egna projekt.

---

## Vad du behöver

- **Java 17** (eller någon nyare JDK; API‑et är kompatibelt med Java 8+)
- **Aspose.HTML for Java**‑biblioteket (version 23.12 eller nyare)
- En IDE eller enkel textredigerare + kommandorads‑kompilering
- Internetåtkomst för exempel‑URL‑en (`https://example.com`)

Inga externa byggverktyg krävs; koden kompileras med `javac` och körs med `java`. Om du föredrar Maven eller Gradle, lägg bara till Aspose.HTML‑beroendet—inget krångligt.

---

## Steg 1: Skapa en sandbox som definierar renderingsmiljön

Sandboxen är där du berättar för Aspose.HTML vilken “skärm” du låtsas ha. Här sätter vi en **viewport på 1024 × 768**, ett **DPI på 96** och en anpassad **user‑agent‑string**.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Varför detta är viktigt:**  
- **DPI** påverkar hur CSS‑enheten `pt` översätts till pixlar; ett högre DPI ger skarpare rendering.  
- **Viewport‑storlek** bestämmer vilka layout‑breakpoints den responsiva CSS‑en träffar.  
- **User‑agent** kan trigga server‑sidans innehållsvariationer (mobil vs. desktop).

> **Pro tip:** Om du senare genererar PDF‑filer, matcha DPI‑värdet mot den önskade utskriftsupplösningen (t.ex. 300 dpi för högkvalitativa utskrifter).

---

## Steg 2: Ladda en webbsida i sandboxen

Nu pekar vi sandboxen på en URL. `HTMLDocument`‑konstruktorn accepterar sandboxen, så layout‑motorn respekterar de inställningar vi just definierade.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Vad händer under huven?**  
Aspose.HTML skapar ett isolerat renderingskontext, liknande en headless‑browser, men utan overheaden från en full Chromium‑instans. Detta gör operationen snabb och minnes‑lätt—perfekt för batch‑bearbetning.

---

## Steg 3: Interagera med DOM – Läs sidans titel

För demonstration hämtar vi titeln och skriver ut den. I ett verkligt scenario kan du ta en skärmdump, exportera till PDF eller skrapa data.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Förväntad utskrift** (när `https://example.com` är nåbar):

```
Title inside sandbox: Example Domain
```

Om webbplatsen returnerar en annan titel ser du den istället—ingen annan förändring behövs.

---

## Steg 4: Verifiera inställningarna (valfri felsökning)

Ibland vill du dubbelkolla att sandboxen verkligen respekterar ditt DPI och din viewport. Aspose.HTML exponerar inte dessa värden direkt, men du kan härleda dem genom att mäta elementens dimensioner.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Om du vet att CSS deklarerar elementet som `width: 200pt;`, så bör du vid **96 dpi** se `200pt * (96/72) ≈ 267px`. Ändra DPI och kör igen för att se siffran förändras—bevis på att **hur man ställer in dpi** faktiskt fungerar.

---

## Fullständig källkod i ett block

Kopiera och klistra in följande i `SandboxExample.java`. Den kompileras som den är; se bara till att Aspose.HTML‑JAR‑filen finns på din classpath.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Kompilera och kör:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Du bör se titeln skriven, vilket bekräftar att sandboxen fungerar med det **inställda dpi**, **inställda viewport‑storleken** och **inställda user‑agent** du angav.

---

## Vanliga frågor & edge‑cases

### Vad om jag behöver en annan DPI?

Ändra bara det andra argumentet i `DocumentSandbox`. För utskriftsklara PDF‑filer kan du använda `300`:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Högre DPI ger större pixeldimensioner för samma CSS‑punkter, vilket förbättrar rasterkvaliteten men använder mer minne.

### Kan jag ladda en lokal HTML‑fil istället för en URL?

Absolut. Byt ut URL‑en mot en filsökväg:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Se till att sökvägen är absolut och använder `file:///`‑schemat.

### Hur ändrar jag user‑agent efter att sandboxen har skapats?

Sandboxen är oföränderlig—så snart du passerar den till `HTMLDocument` är inställningarna låsta. För att använda en annan user‑agent, skapa en ny `DocumentSandbox` med den önskade strängen.

### Stöder Aspose.HTML JavaScript‑exekvering?

Ja, motorn kör de flesta klient‑sidiga skript. Om ett skript modifierar DOM efter laddning kan du vänta lite:

```java
webDoc.waitForLoad();
```

Eller använda logik liknande `setTimeout` i sidan innan du frågar efter element.

---

## Visuell bekräftelse (Bild)

Nedan är en konsol‑skärmdump som visar ett lyckat körresultat. Notera att titelutskriften matchar sidan, vilket bekräftar att sandboxen respekterade våra inställningar.

![Konsolutdata som visar hur man ställer in dpi i Aspose.HTML Sandbox](/images/console-output.png)

*Alt text:* *Konsolutdata som demonstrerar hur man ställer in dpi, viewport‑storlek och user‑agent i Aspose.HTML Sandbox.*

---

## Sammanfattning & nästa steg

Vi har gått igenom **hur man ställer in DPI** (96 dpi i exemplet), **hur man ställer in viewport‑storlek** (1024 × 768) och **hur man ställer in user‑agent** (anpassad sträng) med Aspose.HTML:s sandbox‑API. Den fullständiga, körbara Java‑programmet visar att dessa inställningar inte bara är teoretiska—de påverkar direkt rendering och DOM‑interaktion.

Redo för mer?

- **Export till PDF:** Efter att sidan har laddats, anropa `webDoc.save("output.pdf", SaveFormat.PDF);` för att generera en högupplöst PDF som återspeglar DPI‑värdet du satt.  
- **Ta en skärmdump:** Använd `webDoc.renderToBitmap("screenshot.png");` för pixelperfekta bilder.  
- **Lek med responsiva layouter:** Ändra viewport‑dimensionerna för att testa mobila breakpoints utan en riktig enhet.  

Experimentera med olika DPI‑värden, viewport‑kombinationer och user‑agents för att se hur servrar och CSS reagerar. Sandboxen är en lättviktig lekplats som sparar dig från att starta fulla webbläsare.

---

### Fortsätt utforska

- **Aspose.HTML Documentation** – djupdyk i `DocumentSandbox`‑alternativen.  
- **Advanced CSS Media Queries** – lär dig hur viewport‑storlek triggar olika stilar.  
- **User‑Agent Spoofing** – upptäck hur vissa webbplatser levererar alternativ markup baserat på agent‑strängen.

Har du frågor eller ett knepigt fall? Lämna en kommentar så felsöker vi tillsammans. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}