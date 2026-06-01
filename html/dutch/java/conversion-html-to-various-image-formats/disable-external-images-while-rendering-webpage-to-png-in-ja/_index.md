---
category: general
date: 2026-05-31
description: Schakel externe afbeeldingen uit wanneer je een webpagina rendert naar
  PNG in Java met Aspose HTML. Leer hoe je een webpagina veilig in een sandbox laadt
  en een HTML‑document opslaat als PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: nl
og_description: Schakel externe afbeeldingen uit bij het renderen van een webpagina
  naar PNG in Java. Deze stapsgewijze handleiding laat zien hoe je een webpagina in
  een sandbox laadt en een HTML‑document opslaat als PNG.
og_title: Externe afbeeldingen uitschakelen tijdens het renderen van een webpagina
  naar PNG in Java
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
title: Externe afbeeldingen uitschakelen bij het renderen van een webpagina naar PNG
  in Java
url: /nl/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Externe afbeeldingen uitschakelen tijdens het renderen van een webpagina naar PNG in Java

Heb je ooit **externe afbeeldingen moeten uitschakelen** wanneer je een webpagina naar PNG rendert in Java? Misschien bouw je een thumbnail‑service die geïsoleerd moet blijven van het openbare internet, of je wilt simpelweg garanderen dat er tijdens de conversie geen afbeeldingen van derden lekken. Hoe dan ook, je bent op de juiste plek.

In deze tutorial lopen we stap voor stap door het laden van een webpagina in een sandbox, het uitschakelen van het ophalen van externe afbeeldingen, en uiteindelijk het opslaan van het HTML‑document als een PNG‑bestand — alles met Aspose.HTML voor Java. Aan het einde heb je een kant‑klaar voorbeeld, plus een reeks praktische tips om de gebruikelijke valkuilen te vermijden.

## Wat je zult leren

- **Hoe HTML naar afbeelding te renderen in Java** met behulp van Aspose.HTML’s `Converter`.
- De exacte stappen om een **webpagina in een sandbox te laden** met een aangepast viewport en DPI.
- De configuratie die nodig is om **externe afbeeldingen uit te schakelen** terwijl de pagina nog steeds wordt gerenderd.
- Hoe je een **HTML‑document als PNG opslaat** (of een ander ondersteund formaat) op schijf.
- Afhandeling van randgevallen, prestatie‑tips en probleemoplossend advies.

### Vereisten

- Java 8 of nieuwer geïnstalleerd (de code werkt ook met JDK 11+).
- Maven of Gradle om de Aspose.HTML voor Java‑bibliotheek te downloaden.
- Basiskennis van Java‑syntaxis en exception‑handling.
- Een internetverbinding voor het initiële paginaverzoek (tenzij je de HTML lokaal serveert).

> **Pro tip:** Als je achter een corporate proxy werkt, stel dan de JVM‑eigenschappen `http.proxyHost` en `http.proxyPort` in voordat je het voorbeeld uitvoert.

---

## Stap 1: Zet je project op en voeg Aspose.HTML toe

Allereerst — voeg de Aspose.HTML‑dependency toe. Als je Maven gebruikt, plaats dit in je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Voor Gradle is het equivalent:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Zodra de bibliotheek op het classpath staat, kun je beginnen met coderen.

---

## Stap 2: **Externe afbeeldingen uitschakelen** met een sandbox‑omgeving

Het hart van de oplossing zit in `DocumentSandbox`. Door `false` door te geven voor de *allowExternalImages*‑vlag, instrueren we Aspose.HTML om alle `<img>`‑tags die naar URL’s buiten de sandbox wijzen te negeren. Dit is precies de mechaniek die **externe afbeeldingen uitschakelt**.

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

> **Waarom dit belangrijk is:** Zonder de sandbox zou de renderer proberen elke afbeelding die door de pagina wordt gerefereerd te downloaden, wat traag, onbetrouwbaar of zelfs een beveiligingsrisico kan zijn. Het instellen van de vlag op `false` garandeert een schone, zelf‑containende render‑pass.

---

## Stap 3: **Webpagina in sandbox laden**  

Nu wijzen we Aspose.HTML naar de URL die we willen vastleggen. De `HTMLDocument`‑constructor accepteert de sandbox‑instantie en past automatisch de beperkingen toe die we zojuist hebben gedefinieerd.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Als de pagina sterk leunt op externe scripts voor de lay‑out, kun je merken dat er inhoud ontbreekt omdat we ook scripts hebben uitgeschakeld. In dat geval kun je de `allowExternalScripts`‑vlag op `true` zetten, terwijl `allowExternalImages` op `false` blijft.

---

## Stap 4: **Webpagina naar PNG renderen**  

Met het document geladen, is het omzetten naar een afbeelding één‑regelige code via `Converter.convert`. Het `ImageSaveOptions`‑object laat je het uitvoerformaat kiezen; hier kiezen we PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Het resulterende bestand, `sandboxed.png`, bevat een snapshot van de pagina **zonder externe afbeeldingen** — alleen de inline SVG‑s of base64‑gecodeerde graphics blijven eventueel over.

---

## Stap 5: Controleer de output en los veelvoorkomende problemen op

Na het uitvoeren van het programma, open `sandboxed.png` in een willekeurige afbeeldingsviewer. Je zou de paginalay‑out, tekst en CSS‑styling moeten zien, maar alle `<img src="http://…">`‑elementen zullen leeg zijn (vaak weergegeven als een wit rechthoekje of volledig weggelaten).

### Typische haperingen en hoe ze op te lossen

| Symptoom | Waarschijnlijke oorzaak | Oplossing |
|---|---|---|
| Lege pagina | De doel‑URL blokkeert het verzoek (bijv. Cloudflare) | Voeg juiste headers toe aan de sandbox‑user‑agent of gebruik een proxy. |
| Ontbrekende lettertypen | Lettertype‑bestanden worden extern gehost | Installeer de lettertypen lokaal of embed ze als `@font-face` met data‑URI’s. |
| Layout‑verschuiving | CSS verwijst naar externe stylesheets die geblokkeerd werden | Zet `allowExternalScripts` tijdelijk op `true` *alleen* voor CSS‑laden, en voer opnieuw uit. |
| `java.lang.OutOfMemoryError` | Een zeer grote pagina wordt gerenderd op hoge DPI | Verklein viewport‑grootte of DPI, of vergroot de JVM‑heap (`-Xmx2g`). |

---

## Stap 6: Voorbeeld uitbreiden – Opslaan in andere formaten

Dezelfde code werkt voor JPEG, BMP of zelfs PDF. Verander simpelweg de `SaveFormat`‑enum:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Wil je een PDF, vervang dan `ImageSaveOptions` door `PdfSaveOptions` en pas de bestands­extensie overeenkomstig aan.

---

## Volledig werkend voorbeeld (Kopieer‑en‑Plak klaar)

Hieronder vind je het **complete, uitvoerbare programma**. Maak een nieuwe Java‑klasse, plak de code, zorg dat de map `output` bestaat, en voer het uit.

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

**Verwachte console‑output**:

```
PNG image saved to: output/sandboxed.png
```

Open `sandboxed.png` — je ziet de pagina gerenderd **zonder externe afbeeldingen**.

---

## Veelgestelde vragen

**V: Kan ik nog steeds afbeeldingen weergeven die in de HTML zijn ingebed?**  
A: Ja. Inline `data:`‑URI’s of base64‑gecodeerde afbeeldingen worden beschouwd als onderdeel van het document en verschijnen in de PNG.

**V: Wat als ik sommige externe afbeeldingen wil behouden maar andere wil blokkeren?**  
A: De sandbox werkt als een alles‑of‑niets‑schakelaar. Voor fijnmazige controle download je de toegestane afbeeldingen zelf, embed je ze als data‑URI’s, en render je vervolgens.

**V: Werkt deze aanpak op headless servers?**  
A: Absoluut. Aspose.HTML is een pure‑Java bibliotheek; er is geen display‑server of browser‑engine nodig.

**V: Hoe verschilt dit van Selenium of Puppeteer?**  
A: Selenium bestuurt een echte browser, wat zwaar en moeilijk te sandboxen is. Aspose.HTML rendert HTML direct in het geheugen, wat zorgt voor deterministische prestaties en eenvoudigere beveiligingscontroles zoals **externe afbeeldingen uitschakelen**.

---

## Conclusie

Je beschikt nu over een solide, end‑to‑end recept voor **het uitschakelen van externe afbeeldingen tijdens het renderen van een webpagina naar PNG in Java**. Door gebruik te maken van `DocumentSandbox` krijg je strakke controle over welke externe bronnen zijn toegestaan, wat zowel de veiligheid als de reproduceerbaarheid waarborgt. Vanaf hier kun je experimenteren met verschillende viewport‑groottes, DPI‑instellingen of uitvoerformaten — elke aanpassing opent een nieuw pad voor het genereren van thumbnails, previews of archief‑snapshots.

Klaar voor de volgende uitdaging? Probeer een batch van URL’s parallel te renderen, of integreer deze logica in een Spring Boot‑microservice die PNG’s on‑demand levert. De mogelijkheden zijn eindeloos wanneer je de flexibiliteit van Aspose.HTML combineert met de concurrency‑tools van Java.

Happy coding, en vergeet niet je succesverhalen te delen in de reacties!

## Wat moet je hierna leren?

- [Hoe Aspose te gebruiken om HTML naar PNG te renderen – Stapsgewijze handleiding](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Hoe HTML naar PNG te renderen met Aspose – Complete gids](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [Hoe CSS te bewerken – Geavanceerde externe CSS‑bewerking met Aspose.HTML voor Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}