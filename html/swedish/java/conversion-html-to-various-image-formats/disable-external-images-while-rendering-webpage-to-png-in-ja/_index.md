---
category: general
date: 2026-05-31
description: Inaktivera externa bilder när du renderar en webbsida till PNG i Java
  med Aspose HTML. Lär dig att ladda webbsidan i en sandlåda på ett säkert sätt och
  spara HTML‑dokumentet som PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: sv
og_description: Inaktivera externa bilder när du renderar en webbsida till PNG i Java.
  Denna steg‑för‑steg‑guide visar hur du laddar en webbsida i en sandbox och sparar
  HTML‑dokumentet som PNG.
og_title: Inaktivera externa bilder vid rendering av webbsida till PNG i Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Inaktivera externa bilder vid rendering av webbplats till PNG i Java
url: /sv/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Inaktivera externa bilder vid rendering av webbsida till PNG i Java

Har du någonsin behövt **inaktivera externa bilder** när du renderar en webbsida till PNG i Java? Kanske bygger du en miniatyrtjänst som måste hållas isolerad från det offentliga internet, eller så vill du helt enkelt säkerställa att inga tredjepartsbilder läcker under konverteringen. Oavsett så har du hamnat på rätt plats.

I den här handledningen går vi igenom hur du laddar en webbsida i en sandbox, stänger av hämtning av externa bilder och slutligen sparar HTML‑dokumentet som en PNG‑fil – allt med Aspose.HTML för Java. När du är klar har du ett färdigt exempel samt några praktiska tips för att undvika vanliga fallgropar.

## Vad du kommer att lära dig

- **Hur du renderar HTML till bild i Java** med Aspose.HTML:s `Converter`.
- De exakta stegen för att **ladda webbsida i sandbox** med en anpassad viewport och DPI.
- Konfigurationen som behövs för att **inaktivera externa bilder** samtidigt som sidan renderas.
- Hur du **sparar HTML‑dokument som PNG** (eller något annat stödd format) på disk.
- Hantering av kantfall, prestandatips och felsökning.

### Förutsättningar

- Java 8 eller nyare installerat (koden fungerar även med JDK 11+).
- Maven eller Gradle för att hämta Aspose.HTML för Java‑biblioteket.
- Grundläggande kunskap om Java‑syntax och undantagshantering.
- En internetanslutning för den initiala sidladdningen (om du inte serverar HTML lokalt).

> **Pro tip:** Om du arbetar bakom en företagsproxy, sätt JVM‑egenskaperna `http.proxyHost` och `http.proxyPort` innan du kör exemplet.

---

## Steg 1: Ställ in ditt projekt och lägg till Aspose.HTML

Först och främst – lägg till Aspose.HTML‑beroendet. Om du använder Maven, lägg in följande i din `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

För Gradle är motsvarigheten:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

När biblioteket finns på klassökvägen är du redo att börja koda.

---

## Steg 2: **Inaktivera externa bilder** med en sandbox‑miljö

Kärnan i lösningen ligger i `DocumentSandbox`. Genom att skicka `false` för flaggan *allowExternalImages* instruerar vi Aspose.HTML att ignorera alla `<img>`‑taggar som pekar på URL:er utanför sandboxen. Detta är den exakta mekanismen som **inaktiverar externa bilder**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Varför detta är viktigt:** Utan sandboxen skulle renderaren försöka ladda ner varje bild som sidan refererar till, vilket kan vara långsamt, opålitligt eller till och med en säkerhetsrisk. Att sätta flaggan till `false` garanterar en ren, självständig renderingspass.

---

## Steg 3: **Ladda webbsida i sandbox**  

Nu pekar vi Aspose.HTML på den URL vi vill fånga. `HTMLDocument`‑konstruktorn accepterar sandbox‑instansen och applicerar automatiskt de restriktioner vi just definierat.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Om sidan är starkt beroende av externa skript för layouten kan du märka att innehåll saknas eftersom vi också inaktiverade skript. I så fall kan du sätta flaggan `allowExternalScripts` till `true` samtidigt som `allowExternalImages` hålls på `false`.

---

## Steg 4: **Rendera webbsida till PNG**  

När dokumentet är laddat blir konverteringen till en bild en enkelrad med `Converter.convert`. Objektet `ImageSaveOptions` låter dig välja output‑format; här väljer vi PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Den resulterande filen, `sandboxed.png`, innehåller ett ögonblicksbild av sidan **utan några externa bilder** – endast inbäddade SVG‑ eller base64‑kodade grafik återstår, om någon.

---

## Steg 5: Verifiera resultatet och felsök vanliga problem

Efter att programmet har körts, öppna `sandboxed.png` i en bildvisare. Du bör se sidlayout, text och CSS‑styling, men alla `<img src="http://…">`‑element kommer att vara tomma (ofta renderade som en vit rektangel eller helt uteblivna).

### Vanliga hinder och hur du löser dem

| Symptom | Trolig orsak | Lösning |
|---|---|---|
| Tom sida | Måladressen blockerade förfrågan (t.ex. Cloudflare) | Lägg till korrekta headers i sandboxens user‑agent eller använd en proxy. |
| Saknade typsnitt | Typsnittsfiler hostas externt | Installera typsnitten lokalt eller bädda in dem som `@font-face` med data‑URI:er. |
| Layoutförskjutning | CSS refererar till externa stilmallar som blockerades | Sätt `allowExternalScripts` till `true` *endast* för CSS‑laddning, kör sedan om. |
| `java.lang.OutOfMemoryError` | Rendering av en mycket stor sida med hög DPI | Minska viewport‑storlek eller DPI, eller öka JVM‑heap (`-Xmx2g`). |

---

## Steg 6: Utöka exemplet – spara i andra format

Samma kod fungerar för JPEG, BMP eller till och med PDF. Byt bara `SaveFormat`‑enum‑värdet:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Om du vill ha en PDF istället, ersätt `ImageSaveOptions` med `PdfSaveOptions` och justera filändelsen därefter.

---

## Fullt fungerande exempel (Kopiera‑klistra‑klart)

Nedan är det **kompletta, körbara programmet**. Skapa en ny Java‑klass, klistra in koden, se till att katalogen `output` finns, och kör.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Förväntad konsolutskrift**:

```
PNG image saved to: output/sandboxed.png
```

Öppna `sandboxed.png` – du ser sidan renderad **utan några externa bilder**.

---

## Vanliga frågor

**Q: Kan jag fortfarande visa bilder som är inbäddade i HTML?**  
A: Ja. Inline `data:`‑URI:er eller base64‑kodade bilder behandlas som en del av dokumentet och visas i PNG‑filen.

**Q: Vad om jag vill behålla vissa externa bilder men blockera andra?**  
A: Sandboxen fungerar som en hel‑eller‑inget‑växel. För finare kontroll kan du själv ladda ner de tillåtna bilderna, bädda in dem som data‑URI:er och sedan rendera.

**Q: Fungerar detta på huvudlösa servrar?**  
A: Absolut. Aspose.HTML är ett rent Java‑bibliotek; det kräver ingen display‑server eller webbläsarmotor.

**Q: Hur skiljer sig detta från att använda Selenium eller Puppeteer?**  
A: Selenium styr en riktig webbläsare, vilket är tungt och svårare att sandboxa. Aspose.HTML renderar HTML direkt i minnet, vilket ger deterministisk prestanda och enklare säkerhetskontroller som **inaktivera externa bilder**.

---

## Slutsats

Du har nu ett robust, end‑to‑end‑recept för **att inaktivera externa bilder medan du renderar en webbsida till PNG i Java**. Genom att utnyttja `DocumentSandbox` får du exakt kontroll över vilka externa resurser som tillåts, vilket säkerställer både säkerhet och reproducerbarhet. Därefter kan du experimentera med olika viewport‑storlekar, DPI‑inställningar eller output‑format – varje justering öppnar nya möjligheter för att skapa miniatyrer, förhandsgranskningar eller arkiverade snapshots.

Redo för nästa utmaning? Prova att rendera en batch av URL:er parallellt, eller integrera logiken i en Spring Boot‑mikrotjänst som returnerar PNG‑filer på begäran. Himlen är gränsen när du kombinerar Aspose.HTML:s flexibilitet med Javas samtidighetsverktyg.

Happy coding, and don’t forget to share your success stories in the comments!

## Vad du bör lära dig härnäst?

- [Hur du använder Aspose för att rendera HTML till PNG – Steg‑för‑steg‑guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Hur du renderar HTML till PNG med Aspose – Komplett guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [Hur du redigerar CSS – Avancerad extern CSS‑redigering med Aspose.HTML för Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}