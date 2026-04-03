---
category: general
date: 2026-04-03
description: Lär dig hur du använder sandbox i Aspose.HTML Java för att ange användaragent,
  ställa in storlek och omedelbart hämta viewportens storlek. Fullständig kod, förklaringar
  och tips ingår.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: sv
og_description: Lär dig hur du använder sandbox i Aspose.HTML Java för att ställa
  in användaragent, ange storlek och omedelbart hämta viewportens storlek. Komplett
  guide med kod och bästa praxis.
og_title: Hur du använder Sandbox – Ställ in användaragent och hämta viewport‑storlek
tags:
- AsposeHTML
- Java
- Sandbox
title: Hur man använder Sandbox – Ställ in användaragent och hämta visningsområdets
  storlek
url: /sv/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder Sandbox – Ställ in User Agent & Hämta Viewport‑storlek

Har du någonsin funderat **hur man använder sandbox** när du renderar HTML med Aspose.HTML för Java? Kanske har du kört fast när du försökt simulera en specifik skärmstorlek eller behövt förfalska en user‑agent‑sträng så att sidan beter sig som om den besöks från en mobil webbläsare.  

Det goda nyheterna är att sandbox‑API:et låter dig göra exakt det, och du kan dessutom hämta den beräknade viewport‑storleken efter att sidan har laddats. I den här handledningen går vi igenom hur du skapar en sandbox, ställer in storlek, anger en egen user agent, laddar en fjärrsida och slutligen läser av viewport‑dimensionerna. När du är klar vet du **hur man ställer in storlek**, **hur man hämtar viewport** och varför dessa steg är viktiga för pålitlig headless‑rendering.

> **Snabb vinst:** du får en körbar Java‑klass som skriver ut något i stil med `Viewport: 1280×800` på några sekunder.

---

## Vad du behöver

- **Aspose.HTML för Java** version 24.6 eller nyare (API‑et vi använder introducerades i 24.5).  
- Ett Java 17+‑utvecklingskit (vilken JDK som helst från de senaste versionerna fungerar).  
- En IDE eller en enkel textredigerare – inga speciella tillägg krävs.  
- Internetåtkomst om du vill ladda en extern URL såsom `https://example.com`.

Det är allt. Ingen Maven/Gradle‑magik är obligatorisk; du kan lägga JAR‑filerna på classpath manuellt om du föredrar det.  

---

## Hur man använder Sandbox – Översikt

Sandboxen isolerar renderingsmotorn från värd‑OS:et, så att du kan definiera en virtuell skärm (bredd, höjd, DPI) och en egen **user agent**‑sträng. Tänk på den som ett litet webbläsarfönster som lever helt i minnet. När du senare frågar `HTMLDocument` om dess standardvy, rapporterar motorn **viewport‑storleken** som den beräknat utifrån sandbox‑inställningarna.  

Nedan är ett hög‑nivå‑flöde:

1. **Skapa** ett `DocumentSandbox` och konfigurera bredd, höjd, DPI och user‑agent.  
2. **Ladda** ett `HTMLDocument` i den sandboxen.  
3. **Fråga** dokumentets standardvy om viewport‑storleken.  

Låt oss gå igenom varje steg.

---

## Steg 1: Skapa en Sandbox och ange storlek

Först startar vi en sandbox och talar om för den hur stor den virtuella skärmen ska vara. Här svarar du på frågan **hur man ställer in storlek** för en headless‑rendering.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Proffstips:** Om du testar en responsiv layout, prova en smal bredd som `360` för att efterlikna en telefon, eller en bred som `1920` för en desktop. Sandboxen respekterar den DPI du anger, så en hög‑densitetsskärm (t.ex. 144 DPI) påverkar media‑queries som använder `device-pixel-ratio`.

---

## Steg 2: Ange User Agent för sandboxen

Varför bry sig om en egen **user agent**? Vissa webbplatser levererar olika markup eller skript beroende på vilken webbläsare som rapporteras. Genom att anropa `setUserAgent` kan du lura sidan att tro att den besöks från Chrome, Firefox eller en mobil enhet.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Nu kommer sidan att tro att den renderas på en iPhone. Om du behöver **ställa in user agent** tillbaka till standard, återanvänd bara den tidigare “AsposeHTML/24.6 …”‑strängen.

---

## Steg 3: Ladda ett HTML‑dokument i sandboxen

När sandboxen är klar kan vi ladda vilken URL eller lokal HTML‑fil som helst. `HTMLDocument`‑konstruktorn tar sandboxen som ett andra argument och binder ihop dem.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

`try‑with‑resources`‑blocket ser till att dokumentet frigörs korrekt, så att de inhemska resurser som Aspose.HTML allokerar under huven släpps.

---

## Steg 4: Hämta viewport‑storlek från dokumentet

Här är ögonblicket du har väntat på: att hämta **viewport‑storleken** som renderingsmotorn beräknat. Detta svarar på **hur man hämtar viewport** efter att sidan har layouats.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

När du kör programmet bör du se något i stil med:

```
Viewport: 1280×800
```

Om du ändrade sandbox‑dimensionerna i Steg 1 kommer de utskrivna siffrorna att spegla de nya värdena – perfekt för automatiserade tester som verifierar responsiva brytpunkter.

---

## Fullt fungerande exempel

Nedan är den kompletta, körklara klassen som sätter ihop alla bitar. Kopiera och klistra in den i en fil med namnet `SandboxExample.java`, lägg till Aspose.HTML‑JAR‑filerna på classpath och kör `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Förväntad utskrift** (givet sandbox‑inställningarna ovan):

```
Viewport: 1280×800
```

Om du anger en annan bredd/höjd i sandboxen kommer utskriften att förändras i enlighet med det – exakt vad du behöver när du testar responsiva designer.

---

## Edge Cases & Vanliga frågor

### Vad händer om sidan använder `window.innerWidth` istället för CSS‑media queries?

Sandboxens virtuella skärmstorlek påverkar både CSS‑layout och JavaScripts `window.innerWidth/innerHeight`. Så **hur man hämtar viewport** via JavaScript kommer att returnera samma siffror som du ser i Java‑konsolen.

### Kan jag köra flera sandboxes parallellt?

Ja. Varje `DocumentSandbox`‑instans är oberoende, så du kan starta en trådpool, ge varje tråd sin egen sandbox med olika dimensioner och rendera dussintals sidor samtidigt. Kom bara ihåg att JAR‑filerna är trådsäkra (de är).

### Påverkar DPI‑inställningen bildskalning?

Absolut. En högre DPI gör att en CSS‑pixel motsvarar fler enhetspixlar, vilket kan få högupplösta bilder att se skarpare ut. Om du testar retina‑liknande resurser, prova `sandbox.setDeviceDpi(144)`.

### Hur hanterar jag HTTPS‑certifikat som är själv‑signerade?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}