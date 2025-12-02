---
date: 2025-12-01
description: Leer hoe u de PDF-paginaformaat kunt aanpassen, HTML als PDF kunt renderen
  en PDF kunt genereren vanuit HTML met Aspose.HTML voor Java. Beheer paginagrootte
  eenvoudig.
language: nl
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: PDF-paginagrootte aanpassen met Aspose.HTML voor Java
url: /java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-paginaformaat aanpassen met Aspose.HTML voor Java

Het genereren van PDF's vanuit HTML is een veelvoorkomende eis voor rapporten, facturen en e‑books. Wanneer je **PDF-paginaformaat aanpast**, zorg je ervoor dat het uiteindelijke document overeenkomt met de lay-out die je in HTML hebt ontworpen. In deze tutorial leer je hoe je HTML rendert als PDF, aangepaste afmetingen instelt en bepaalt of de pagina automatisch wordt uitgebreid tot de breedste inhoud. We lopen stap voor stap door een compleet, praktisch voorbeeld met Aspose.HTML voor Java.

## Snelle antwoorden
- **Wat betekent “PDF-paginaformaat aanpassen”?** Het stelt je in staat de breedte en hoogte van elke PDF-pagina te definiëren of de renderer automatisch de breedste element te laten passen.  
- **Welke bibliotheek wordt gebruikt?** Aspose.HTML voor Java (nieuwste versie).  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.  
- **Kan ik afmetingen programmatisch wijzigen?** Ja – gebruik `PageSetup` en de eigenschap `AdjustToWidestPage`.  
- **Is dit compatibel met Java 8+?** Absoluut – de API werkt met elke JDK 8 of hoger.

## Wat betekent “PDF-paginaformaat aanpassen”?
PDF-paginaformaat aanpassen houdt in dat je de afmetingen van elke pagina die de HTML-renderer maakt, configureert. Je kunt een vaste grootte instellen (bijv. A4, Letter) of de renderer de optimale breedte laten berekenen op basis van de inhoud. Dit geeft je precieze controle over lay-out, paginering en visuele getrouwheid.

## Waarom PDF-paginaformaat aanpassen bij het converteren van HTML naar PDF?
- **Ontwerpintentie behouden:** Voorkom dat inhoud wordt afgekapt of uitgerekt.  
- **Optimaliseren voor afdrukken:** Stem af op het papierformaat dat door downstream processen wordt vereist.  
- **Leesbaarheid verbeteren:** Vermijd overmatig witruimte of samengeperste tekst.  
- **Dynamische documenten:** Pas automatisch brede tabellen of afbeeldingen aan zonder handmatige berekeningen.

## Vereisten
Voordat je begint, zorg dat je het volgende hebt:

- **Java Development Kit (JDK) 8 of hoger** geïnstalleerd op je machine.  
- **Aspose.HTML voor Java** – download de nieuwste JAR van de [officiële releasepagina](https://releases.aspose.com/html/java/).  
- **Een HTML‑bestand** dat je wilt converteren (we gebruiken `FirstFile.html` in het voorbeeld).  

## Pakketten importeren
Eerst importeren we de klassen die we nodig hebben. Het onderstaande code‑blok is ongewijzigd ten opzichte van de originele tutorial.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## Stap 1: HTML-inhoud lezen
We lezen het bron‑HTML‑bestand met een `FileInputStream`. Deze stap bereidt de ruwe markup voor latere manipulatie voor.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Stap 2: HTML schrijven (en eventueel verrijken)
Hier kopiëren we de originele HTML naar een nieuw bestand en voegen een paar inline‑stijlen toe om te laten zien hoe styling de PDF‑output beïnvloedt. Vervang gerust de voorbeeld‑CSS door je eigen stijlregels.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Stap 3: HTML renderen naar PDF – Twee scenario's
Nu bekijken we hoe je **PDF genereert vanuit HTML** met twee verschillende strategieën voor pagina‑formaat.

### 3.1 Paginaformaat NIET aangepast aan de breedte van de inhoud
In dit geval fixeren we de paginagrootte (100 × 100 punten). Als een element deze limieten overschrijdt, wordt het bijgesneden.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 Paginaformaat AANGEPAST aan de breedte van de inhoud
Hier schakelen we `AdjustToWidestPage` in, zodat de renderer de paginabreedte automatisch uitbreidt om het breedste element te huisvesten terwijl de hoogte vast blijft.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## Hoe PDF-dimensies instellen (hoe PDF-paginaformaat wijzigen) in code
Het `PageSetup`‑object is de sleutel:

- `setAnyPage(Page page)`: definieert de basisbreedte × hoogte.  
- `setAdjustToWidestPage(boolean)`: schakelt automatisch verbreden in of uit.  

Door deze twee eigenschappen aan te passen kun je **PDF-dimensies instellen** voor elk scenario, of je nu een statische A4‑pagina nodig hebt of een dynamische breedte die je HTML‑lay-out volgt.

## Veelvoorkomende problemen & tips
| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| Inhoud wordt afgekapt | Vaste grootte is te klein | Verhoog de `Size`‑waarden of schakel `AdjustToWidestPage` in. |
| Tekst ziet er wazig uit | Standaard DPI voor rendering is laag | Gebruik `PdfRenderingOptions.setResolution(int dpi)` om de kwaliteit te verhogen. |
| Stijlen ontbreken | Externe CSS niet geladen | Voeg CSS inline toe of gebruik `HTMLDocument.setBaseUrl()` om naar je stylesheet‑map te wijzen. |
| Grote HTML‑bestanden veroorzaken OutOfMemoryError | Renderer laadt het hele document in het geheugen | Verwerk het document in delen of vergroot de JVM‑heap (`-Xmx`). |

## Veelgestelde vragen

**Q: Wat is Aspose.HTML voor Java?**  
A: Het is een Java‑bibliotheek waarmee je HTML‑documenten kunt maken, bewerken en renderen, inclusief conversie naar PDF, PNG en andere formaten.

**Q: Hoe kan ik het PDF-paginaformaat aanpassen bij het converteren van HTML naar PDF met Aspose.HTML voor Java?**  
A: Gebruik de `PageSetup`‑klasse en stel `AdjustToWidestPage` in op `true` (auto‑size) of `false` (vaste grootte). Wijs vervolgens de gewenste `Size` toe via `new Page(new Size(width, height))`.

**Q: Kan ik de styling van HTML‑inhoud aanpassen voordat ik deze converteer naar PDF?**  
A: Ja – je kunt CSS injecteren, de DOM wijzigen of externe stylesheets gebruiken. De tutorial toont hoe je inline CSS kunt toevoegen.

**Q: Waar vind ik de documentatie voor Aspose.HTML voor Java?**  
A: Uitgebreide documentatie is beschikbaar [hier](https://reference.aspose.com/html/java/).

**Q: Is er een gratis proefversie beschikbaar voor Aspose.HTML voor Java?**  
A: Absoluut – download een proefversie van de [releasepagina](https://releases.aspose.com/html/java/).

## Conclusie
Je weet nu hoe je **PDF-paginaformaat aanpast**, **HTML rendert als PDF**, en **aangepaste PDF‑dimensies instelt** met Aspose.HTML voor Java. Experimenteer met verschillende paginagroottes, DPI‑instellingen en CSS‑aanpassingen om de output perfect af te stemmen op jouw specifieke gebruikssituatie. Als je tegen problemen aanloopt, raadpleeg dan de officiële documentatie of de Aspose‑ondersteuningsforums.

---

**Last Updated:** 2025-12-01  
**Tested With:** Aspose.HTML for Java 24.12 (latest)  
**Author:** Aspose  
**Related Resources:** [API Reference](https://reference.aspose.com/html/java/) | [Download Free Trial](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}