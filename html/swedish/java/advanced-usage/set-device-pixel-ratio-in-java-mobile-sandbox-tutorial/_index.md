---
category: general
date: 2026-10-19
description: Sätt device pixel ratio i Java med Aspose.HTML sandbox. Lär dig hur du
  sätter screen width height och hämtar sidtitel java med ett komplett, körbart exempel.
draft: false
keywords:
- get page title java
- device pixel ratio java
- create virtual device java
- set screen width height
lastmod: 2026-10-19
og_description: Hämta sidtitel java med Aspose.HTML sandbox. Den här guiden visar
  hur du sätter screen width height och device pixel ratio i Java på några enkla steg.
og_image_alt: 'Developer guide: set device pixel ratio in Java using Aspose.HTML sandbox'
og_title: Hämta sidtitel java – sätt device pixel ratio i Java sandbox‑handledning
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how
    to set screen width height and get page title java with a complete, runnable example.
  headline: Get page title java – set device pixel ratio in Java sandbox tutorial
  type: TechArticle
- questions:
  - answer: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio`
      value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing
      its options is not supported.
    question: Can I change the pixel ratio at runtime?
  - answer: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run
      the same load‑and‑title logic for each.
    question: What if I need to test multiple devices?
  - answer: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the
      JVM’s keystore or, for testing only, disable verification (not recommended for
      production).
    question: Does this work with HTTPS sites that have self‑signed certificates?
  - answer: The `HTMLDocument` API provides `save` methods that can export the rendered
      page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after
      loading.
    question: How do I capture a screenshot instead of just the title?
  - answer: Each `Sandbox` instance is isolated, but you should avoid sharing a single
      instance across multiple threads without synchronization.
    question: Is the sandbox thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- mobile emulation
title: Hämta sidtitel java – sätt device pixel ratio i Java sandbox‑handledning
url: /sv/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hämta sidtitel java – ställ in enhetens pixelförhållande i Java sandbox‑handledning

Har du någonsin behövt **set device pixel ratio** medan du testar en responsiv webbplats i Java? Du är inte ensam. Många utvecklare stöter på problem när sidan ser perfekt ut på skrivbordet men går sönder på hög‑DPI‑telefoner. De goda nyheterna? Med Aspose.HTML:s sandbox kan du emulera en iPhone X (eller någon enhet) direkt från din Java‑kod—ingen webbläsare behövs.

I den här guiden går vi igenom **how to set screen width height**, konfigurerar **device pixel ratio**, och slutligen **get page title java** för att verifiera att allt renderas korrekt. När du är klar har du ett självständigt program som du kan lägga in i vilket projekt som helst och börja testa mobila layouter omedelbart.

## Snabba svar
- **Hur ställer jag in device pixel ratio i Java?** Använd `SandboxOptions.setDevicePixelRatio(double)` innan du skapar sandboxen.  
- **Vilken metod returnerar sidtiteln?** Anropa `htmlDocument.getTitle()` på den laddade `HTMLDocument`.  
- **Kan jag emulera andra enheter?** Ja—skapa en ny `SandboxOptions` med önskad bredd, höjd och pixelförhållande.  
- **Behöver jag en webbläsardrivrutin?** Nej, Aspose.HTML:s sandbox är huvudlös och körs enbart i Java.  
- **Vilken version av Aspose.HTML krävs?** Version 23.7 eller senare stödjer alla mobil‑emuleringsfunktioner.

## Vad är get page title java?
`get page title java` är operationen att hämta `<title>`‑elementet från ett HTML‑dokument med Java‑kod. Det låter dig bekräfta att en sida som laddats i ett virtuellt enhetssammanhang renderade den förväntade titeln. Att hämta titeln är ett vanligt steg i automatiserad validering för att säkerställa att rätt sida laddades efter att enhetsemuleringsparametrar tillämpats.

## Varför använda Aspose.HTML sandbox för mobilemulering?
Aspose.HTML stödjer **30+** in‑ och utdataformat—inklusive HTML, CSS, SVG och PDF—och kan rendera sidor utan att starta en fullständig webbläsare. Dess sandbox bearbetar webbplatser med hundratals sidor samtidigt som minnesanvändningen hålls under 200 MB, vilket gör den idealisk för CI‑pipelines.

## Förutsättningar

- Java 8 eller nyare (koden kompileras även med JDK 11)  
- Aspose.HTML för Java‑biblioteket (version 23.7 eller senare) – du kan hämta det från Maven Central  
- En IDE eller en enkel `javac`‑kommandoradsuppsättning  
- Internetåtkomst för demo‑URL:en (`https://responsive.example.com`)

Inga extra ramverk, ingen Selenium, bara ren Java och Aspose.HTML.

## Hur man ställer in skärmbredd‑höjd och device pixel ratio i Java

`SandboxOptions`‑klassen låter dig ange den virtuella enhetens skärmdimensioner och pixeldensitet. För att emulera en specifik mobil enhet måste du konfigurera sandboxen med önskad skärmbredd, höjd och device pixel ratio. Genom att skapa ett `SandboxOptions`‑objekt och sätta dessa egenskaper kommer renderingsmotorn att behandla sidan som om den visades på den enheten, vilket säkerställer att CSS‑media‑queries och bildskalning fungerar korrekt.

Skapa en `SandboxOptions`‑instans, sätt bredden till **375**, höjden till **812**, och device pixel ratio till **3.0**. Passa sedan dessa alternativ till en ny `Sandbox`. Detta konfigurerar den virtuella enheten fullständigt innan någon sida laddas.

`SandboxOptions`‑klassen definierar den virtuella enhetens skärmstorlek och pixeldensitet. Den är startpunkten för alla mobil‑emuleringsscenarier.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Varför detta är viktigt:**  
> `setDevicePixelRatio`‑anropet skalar allt—from images to font rendering—så sidan tror att den är på en riktig telefon. Om du hoppar över det kan layouten falla tillbaka till desktop‑stil CSS‑media‑queries, vilket undergräver syftet med mobiltestning.

## Hur man skapar sandbox‑instansen

`Sandbox`‑klassen representerar en huvudlös webbläsarmiljö som renderar HTML med de tidigare definierade alternativen. Efter att ha konfigurerat `SandboxOptions` skapar du en `Sandbox` med dessa alternativ för att få ett isolerat renderingssammanhang. Denna sandbox fungerar som en lättviktig webbläsare, tillämpar den skärmstorlek och pixeldensitet du angav, och kan återanvändas för flera sidladdningar samtidigt som miljön hålls ren.

Instansiera en `Sandbox` med de tidigare konfigurerade `SandboxOptions`. Sandboxen beter sig som en liten, huvudlös webbläsare som respekterar de dimensioner och den pixelratio du definierade.

`Sandbox`‑objektet är Aspose.HTML:s isolerade renderingsmotor som körs utan UI. Det garanterar att varje test körs i en ren miljö.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Pro tip:** Du kan återanvända samma `Sandbox`‑objekt för flera sidladdningar; bara ändra URL:en så behåller sandboxen samma enhetsegenskaper.

## Hur man laddar sidan i sandboxen

`HTMLDocument`‑klassen representerar en parsad HTML‑fil i minnet, och erbjuder DOM‑åtkomst samt renderingsmöjligheter. När sandboxen är klar, skapa ett `HTMLDocument` genom att skicka mål‑URL:en och sandbox‑instansen. Detta laddar och renderar sidan med de virtuella enhetsinställningarna, vilket låter dig interagera med DOM eller extrahera information såsom titeln.

Skapa ett `HTMLDocument` genom att skicka mål‑URL:en och `Sandbox`‑instansen. Detta tvingar dokumentet att renderas med den virtuella enhet du tidigare ställt in.

`HTMLDocument`‑klassen representerar en parsad HTML‑fil i minnet och tillhandahåller metoder för DOM‑manipulation och metadataextraktion.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Om URL:en är oåtkomlig eller sidan innehåller fel kommer Aspose.HTML att kasta ett undantag. För produktionskod skulle du omsluta detta i ett `try‑catch` och logga felet, men handledningen håller det enkelt.

## Hur man verifierar med get page title java

`getTitle()`‑metoden returnerar innehållet i HTML‑dokumentets `<title>`‑element som en vanlig sträng. Att läsa titeln är den snabbaste kontrollen. Efter att ha laddat sidan, anropa `htmlDocument.getTitle()` för att hämta titeltexten. Denna enkla kontroll bekräftar att sidan renderades korrekt under de emulerade enhetsinställningarna och ger ett snabbt sätt att validera navigation eller innehållsförändringar i automatiserade tester.

Anropa `htmlDocument.getTitle()` på det laddade dokumentet och skriv ut resultatet. Om sandboxen korrekt tillämpade **device pixel ratio**, kommer titeln att matcha vad du skulle se på en riktig iPhone X.

`getTitle()`‑metoden returnerar innehållet i `<title>`‑elementet som en vanlig sträng, vilket låter dig validera rendering utan visuell inspektion.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Förväntad utskrift (exempel):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Om du ser titeln skriven har du framgångsrikt **set device pixel ratio**, **set screen width height**, och **got the page title** med Java.

## Fullt, körbart exempel

Nedan är det kompletta programmet som du kan kopiera‑klistra in i en fil med namnet `SandboxDemo.java`. Se till att Aspose.HTML‑JAR‑filerna finns på din classpath (`-cp`‑flagga) innan du kompilerar.

`SandboxDemo`‑klassen binder ihop alla tidigare steg till ett enda, körbart exempel.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Kompilera och kör:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Du bör se titeln skriven till konsolen, vilket bekräftar att sidan renderades med önskad **device pixel ratio**.

## Vanliga frågor & edge cases

**Q: Kan jag ändra pixelförhållandet vid körning?**  
A: Ja—skapa en ny `SandboxOptions` med ett annat `setDevicePixelRatio`‑värde och instansiera en ny `Sandbox`. Att återanvända samma sandbox efter att ha ändrat dess alternativ stöds inte.

**Q: Vad händer om jag behöver testa flera enheter?**  
A: Loopa över en lista med `SandboxOptions` (t.ex. iPhone 8, Pixel 4) och kör samma ladd‑och‑titel‑logik för varje.

**Q: Fungerar detta med HTTPS‑sajter som har själv‑signerade certifikat?**  
A: Aspose.HTML respekterar Javas standard‑SSL‑trust‑store. Lägg till certifikatet i JVM:s keystore eller, enbart för testning, inaktivera verifiering (rekommenderas inte för produktion).

**Q: Hur fångar jag en skärmdump istället för bara titeln?**  
A: `HTMLDocument`‑API:n erbjuder `save`‑metoder som kan exportera den renderade sidan till PNG eller JPEG. Använd `htmlDoc.save("output.png", SaveFormat.PNG);` efter laddning.

**Q: Är sandboxen trådsäker?**  
A: Varje `Sandbox`‑instans är isolerad, men du bör undvika att dela en enda instans över flera trådar utan synkronisering.

## Visuell översikt

![Diagram som visar hur man ställer in device pixel ratio i mobil sandbox](https://example.com/images/sandbox-diagram.png "diagram för device pixel ratio")

[Diagram som visar hur man ställer in device pixel ratio i mobil sandbox](https://example.com/images/sandbox-diagram.png "diagram för device pixel ratio")

*Illustrationen ovan visar flödet från konfiguration av `SandboxOptions` (inklusive **set screen width height** och **set device pixel ratio**) till att ladda en URL och extrahera titeln.*

## Slutsats

Du vet nu **how to set device pixel ratio** i Java, hur du **set screen width height** för exakt mobilemulering, och hur du **get page title java** för att bekräfta att renderingen lyckades. Detta kompakta arbetsflöde eliminerar behovet av tunga webbläsare under automatiserad UI‑testning och passar smidigt in i CI‑pipelines.

Redo för nästa steg? Försök exportera den renderade sidan som en bild, eller experimentera med CSS‑media‑query‑debugging genom att växla `devicePixelRatio` mellan 1.0 och 3.0. Du kan också utforska Aspose.HTML:s PDF‑konverteringsfunktioner för att få en utskrivbar version av mobilvyn.

Lycka till med kodandet, och må dina mobila layouter alltid se skarpa ut—oavsett pixeldensitet!

---

**Senast uppdaterad:** 2026-10-19  
**Testat med:** Aspose.HTML 23.7 for Java  
**Författare:** Aspose

## Relaterade handledningar

- [Hämta HTML-titel Java rendera sida i sandbox med skärmbredd](/html/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/)
- [Skapa Aspose HTML sandbox komplett Java‑guide](/html/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/)
- [Ställ in device pixel ratio i Java komplett guide](/html/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}