---
category: general
date: 2026-03-18
description: Maak snel een PDF van HTML in Java. Leer hoe je HTML naar PDF converteert,
  een iPhone‑scherm simuleert en de schermgrootte instelt voor responsieve PDF‑bestanden.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- simulate iphone screen
- how to set screen
- how to convert html
language: nl
og_description: Maak PDF van HTML in Java. Deze gids laat zien hoe je HTML naar PDF
  converteert, een iPhone-scherm simuleert en schermafmetingen instelt voor perfecte
  responsieve PDF's.
og_title: PDF maken van HTML met mobiel viewport – Java‑tutorial
tags:
- Java
- Aspose.HTML
- PDF
- Responsive Design
- Mobile Viewport
title: PDF maken van HTML met mobiel viewport – Complete Java‑gids
url: /nl/java/conversion-html-to-other-formats/create-pdf-from-html-with-mobile-viewport-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak PDF van HTML met Mobiele Viewport – Complete Java-gids

Heb je ooit **PDF van HTML moeten maken**, maar zag de output eruit als een desktoppagina op een klein telefoonscherm? Je bent niet de enige. Wanneer je een responsieve website naar PDF converteert, negeert de standaard viewport vaak de mobiele breakpoints, waardoor je met een krappe rommel blijft zitten.  

Het goede nieuws? Je kunt **HTML naar PDF converteren** terwijl je **een iPhone‑scherm simuleert**, allemaal met eenvoudige Java‑code. In deze tutorial lopen we elke stap door—hoe je de schermgrootte instelt, hoe je de device‑scale factor aanpast, en waarom die instellingen belangrijk zijn voor een pixel‑perfecte PDF.

> **Pro tip:** Als je al Aspose.HTML hebt gebruikt voor eenvoudige conversies, zul je de viewport‑aanpassingen slechts een paar extra regels verwijderd vinden.

---

## Wat je zult leren

* Hoe je **PDF van HTML kunt maken** met Aspose.HTML voor Java.  
* De exacte code om **iPhone‑scherm** dimensies te **simuleren** (375 × 667 px @ 2× dichtheid).  
* Waar je **hoe je scherm instelt** opties in de conversiepijplijn plaatst.  
* Veelvoorkomende valkuilen bij het converteren van responsieve pagina's en hoe je ze kunt vermijden.  
* Een compleet, kant‑klaar Java‑voorbeeld dat je kunt copy‑pasten in je IDE.

### Vereisten

* Java 17 of nieuwer (de code compileert met oudere versies, maar 17 wordt aanbevolen).  
* Aspose.HTML voor Java‑bibliotheek – je kunt de nieuwste JAR downloaden van de [Aspose website](https://products.aspose.com/html/java).  
* Een eenvoudig HTML‑bestand (`input.html`) dat je wilt omzetten naar een PDF.  
* Basiskennis van Maven of Gradle (we laten een Maven‑fragment zien).

---

## Stap 1 – Voeg Aspose.HTML toe aan je project

Allereerst moet je de bibliotheek op je classpath hebben. Als je Maven gebruikt, voeg dan deze dependency toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Waarom dit belangrijk is:** Aspose.HTML doet het zware werk—HTML parseren, CSS toepassen en de lay-out rasteren. Zonder dit zou je zelf een volledige browser‑engine moeten schrijven, wat een *boel* werk is.

Als je de voorkeur geeft aan Gradle, is het equivalent:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

---

## Stap 2 – Bereid Load‑opties voor en simuleer een iPhone‑viewport

Nu configureren we de **hoe je scherm instelt** parameters. De `HtmlLoadOptions`‑klasse laat je Aspose vertellen welke grootte en pixel‑dichtheid de browser moet nabootsen.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class ViewportDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create load options for the HTML document
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // 2️⃣ Simulate a mobile viewport (iPhone 6/7/8) – 375 × 667 pixels with retina density
        loadOptions.setScreenSize(new Size(375, 667));
        loadOptions.setDeviceScaleFactor(2.0);

        // 3️⃣ Convert the HTML file to PDF using the configured viewport
        Converter.convertDocument(
                "YOUR_DIRECTORY/input.html",          // source HTML
                "YOUR_DIRECTORY/output.pdf",          // destination PDF
                new PdfSaveOptions(),
                loadOptions);

        // 4️⃣ Notify that the conversion is complete
        System.out.println("Responsive conversion using mobile viewport.");
    }
}
```

### Waarom deze getallen?

* **375 × 667** komt overeen met de logische CSS‑pixelafmetingen van een iPhone 6/7/8 in portretmodus.  
* **DeviceScaleFactor = 2.0** vertelt de renderer dat elke CSS‑pixel overeenkomt met twee fysieke pixels, wat de Retina‑display nabootst.  

Als je een ander apparaat nodig hebt—bijvoorbeeld een iPhone 12 Pro Max—verander je de grootte naar `428 × 926` en houd je de schaalfactor op `3.0`.

---

## Stap 3 – Voer de conversie uit en controleer de output

Compileer en voer de klasse uit:

```bash
mvn compile exec:java -Dexec.mainClass=ViewportDemo
```

Nadat het programma is voltooid, open `output.pdf`. Je zou moeten zien:

* Alle media‑queries die zich richten op `max-width: 375px` worden correct toegepast.  
* Afbeeldingen worden scherp gerenderd dankzij de 2× schaalfactor.  
* Tekst die de mobiele lettergrootte‑hiërarchie respecteert die je in CSS hebt gedefinieerd.

Als de PDF er nog steeds uitziet als een desktoppagina, controleer dan of je HTML responsieve meta‑tags gebruikt:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Zonder die tag zal zelfs een perfecte viewport‑instelling de mobiele stylesheet niet activeren.

---

## Stap 4 – Externe bronnen verwerken (Afbeeldingen, Lettertypen, CSS)

Wanneer je **HTML naar PDF converteert**, probeert Aspose.HTML elke gekoppelde bron op te halen. Als je een pagina converteert die zich op een lokaal bestandssysteem bevindt, werken absolute URL's (`file:///…`) prima. Voor externe assets kun je tegen het volgende aanlopen:

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| **404‑fouten voor afbeeldingen** | De HTML verwijst naar een URL die authenticatie vereist. | Gebruik `HtmlLoadOptions.setBaseUrl("file:///C:/myproject/")` om relatieve paden op te lossen, of embed afbeeldingen als Base64. |
| **Ontbrekende webfonts** | De PDF‑engine kan het lettertype‑bestand niet downloaden. | Download de `.woff`/`.ttf`‑bestanden lokaal en verwijs ernaar met een relatief pad. |
| **CSS niet toegepast** | Het CSS‑bestand wordt geblokkeerd door CORS. | Host de CSS op een server die cross‑origin verzoeken toestaat, of inline de CSS in de HTML. |

Een snelle manier om het laden van bronnen te testen is de conversie‑aanroep in een try‑catch‑blok te wikkelen en de `Exception`‑melding af te drukken. Aspose.HTML biedt gedetailleerde logs die naar de exacte URL wijzen die mislukt is.

```java
try {
    Converter.convertDocument(...);
} catch (Exception ex) {
    System.err.println("Conversion failed: " + ex.getMessage());
}
```

---

## Stap 5 – Geavanceerde aanpassingen (optioneel)

### a) PDF‑paginasize wijzigen

Standaard maakt Aspose.HTML een PDF‑pagina die overeenkomt met de viewport‑grootte. Als je liever A4 of Letter wilt, voeg dan een `PdfSaveOptions`‑configuratie toe:

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PageSize.A4);
Converter.convertDocument("input.html", "output.pdf", pdfOptions, loadOptions);
```

### b) Programma‑matig een header/footer toevoegen

Je kunt na de conversie een eenvoudige header/footer injecteren met Aspose.PDF (een aparte bibliotheek). De workflow is:

1. Converteer HTML → PDF (zoals getoond).  
2. Open de resulterende PDF met Aspose.PDF.  
3. Voeg `HeaderFooter`‑objecten toe aan elke pagina.

```java
import com.aspose.pdf.*;

Document pdfDoc = new Document("output.pdf");
for (Page page : pdfDoc.getPages()) {
    page.addHeaderFooter(new HeaderFooter("Generated on " + LocalDate.now()));
}
pdfDoc.save("output-with-header.pdf");
```

### c) Batch‑conversie

Als je een map met HTML‑bestanden hebt, loop er dan over:

```java
Files.list(Paths.get("html_folder"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(p -> {
         String pdfPath = p.toString().replace(".html", ".pdf");
         Converter.convertDocument(p.toString(), pdfPath, new PdfSaveOptions(), loadOptions);
     });
```

---

## Veelgestelde vragen (FAQ's)

**Q: Werkt dit met JavaScript‑zware pagina's?**  
A: Aspose.HTML ondersteunt een subset van JavaScript. Eenvoudige DOM‑manipulatie en CSS‑wijzigingen werken meestal, maar complexe frameworks (React, Angular) hebben mogelijk een vooraf gerenderde statische HTML‑snapshot nodig.

**Q: Wat als ik een pagina moet converteren die `@media print`‑regels gebruikt?**  
A: De bibliotheek respecteert `@media print` automatisch. Als je echter ook een mobiele viewport instelt, kan de `print`‑stylesheet sommige mobiele stijlen overschrijven. Test beide scenario's.

**Q: Kan ik een aangepaste DPI voor de PDF instellen?**  
A: Ja. Gebruik `PdfSaveOptions.setDpi(300)` vóór de conversie. Een hogere DPI levert grotere bestanden op, maar scherpere afbeeldingen.

---

## Verwachte resultaat screenshot

Hieronder zie je een illustratie van de uiteindelijke PDF‑pagina (mobiele viewport gesimuleerd).  
![Screenshot van PDF gegenereerd door create pdf from html demo die iPhone‑grootte lay‑out toont]  

*Afbeeldings‑alt‑tekst bevat het primaire zoekwoord voor SEO.*

---

## Conclusie

Je hebt nu een solide **create pdf from html** workflow die mobiele breakpoints respecteert, een iPhone‑scherm simuleert, en je volledige controle over paginagroottes geeft. Door `HtmlLoadOptions` aan te passen kun je “**how to set screen**” voor elk apparaat beantwoorden, en door `Converter.convertDocument` te gebruiken heb je **how to convert html** in Java onder de knie.

Klaar voor de volgende uitdaging? Probeer deze aanpak te combineren met Aspose.PDF om watermerken toe te voegen, meerdere PDF's te combineren, of het document met een wachtwoord te beveiligen. En vergeet niet te experimenteren met andere apparaten—verander gewoon de `Size`‑ en `DeviceScaleFactor`‑waarden om de gewenste pixel‑dichtheid te matchen.

Veel plezier met coderen, en moge je PDF's altijd net zo scherp op papier zijn als op een telefoonscherm! 

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}