---
category: general
date: 2026-03-26
description: Maak PDF met aangepaste grootte van HTML met Aspose.HTML voor Java. Leer
  hoe je HTML naar PDF converteert en de PDF-paginagrootte instelt in slechts een
  paar stappen.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: nl
og_description: Maak PDF met aangepaste afmetingen vanuit HTML met Aspose. Deze gids
  laat zien hoe je HTML naar PDF converteert, de PDF-paginagrootte wijzigt en de paginagrootte
  van PDF moeiteloos instelt.
og_title: PDF met aangepaste grootte maken – Snelle gids voor het converteren van
  HTML naar PDF
tags:
- aspose
- java
- pdf
- html
title: PDF met aangepaste grootte maken – HTML naar PDF converteren met Aspose
url: /nl/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF met aangepaste afmetingen maken – HTML naar PDF converteren met Aspose

Heb je ooit **PDF met aangepaste afmetingen** moeten maken vanuit een HTML‑bestand? In deze tutorial laten we je zien hoe je **HTML naar PDF** kunt **converteren** en de paginagrootte van de PDF kunt instellen met Aspose.HTML voor Java.  

Als je facturen, rapporten of e‑books maakt, zijn de exacte paginadimensies cruciaal—anders ziet je lay‑out er scheef uit of wordt er iets afgesneden.  

We lopen stap voor stap door het hele proces, van het laden van de bron‑HTML tot het aanpassen van marges, en eindigen met een kant‑klaar PDF‑bestand. Geen vage verwijzingen, alleen een compleet, direct uitvoerbaar voorbeeld dat je vandaag nog kunt kopiëren en plakken.

## Wat je nodig hebt

- **Java 17** (of een recente JDK).  
- **Aspose.HTML for Java** JAR‑bestanden – haal de nieuwste versie op uit de Maven‑repository of van de Aspose‑website.  
- Een simpel `input.html`‑bestand in een map die jij beheert.  
- Een IDE of teksteditor naar keuze; ik programmeer meestal in IntelliJ IDEA, maar Eclipse werkt ook prima.

Met deze voorwaarden kom je later geen “class not found”‑fouten tegen.  

Laten we beginnen.

![Voorbeeld van PDF met aangepaste afmetingen](/images/create-pdf-custom-size.png "Schermafbeelding van een PDF gegenereerd met aangepaste paginagrootte en marges – create pdf custom size")

## PDF met aangepaste afmetingen maken – Kernstappen

Hieronder staat het volledige Java‑programma dat je uiteindelijk krijgt. Kopieer het gerust naar een bestand genaamd `ConvertHtmlToPdfCustomPage.java` en voer het uit nadat je de Aspose‑afhankelijkheden aan je project hebt toegevoegd.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### Stap 1 – HTML naar PDF converteren: Document laden

Het eerste wat we doen is de **HTML laden** die we willen omzetten naar een PDF.  
`HTMLDocument` leest het bestand, lost relatieve koppelingen op en bouwt een DOM die Aspose kan renderen.  

> **Waarom dit belangrijk is:** Als de HTML CSS‑ of afbeeldingsbestanden verwijst, haalt Aspose deze op relatief ten opzichte van het bestandspad. Een absoluut pad (`YOUR_DIRECTORY/input.html`) voorkomt “file not found”‑verrassingen.

### Stap 2 – PDF‑paginagrootte wijzigen: Opties configureren

Hier maken we een `PdfConversionOptions`‑object.  
- `setPageSize(PageSize.A4)` vertelt Aspose de standaard A4‑afmetingen te gebruiken (210 × 297 mm).  
- `setPageOrientation(...)` draait de pagina als je landschapsmodus nodig hebt.  
- `setMargins(new Margin(20, 20, 20, 20))` geeft aan elke kant een marge van 20 punt.

Je kunt `PageSize.A4` vervangen door `PageSize.LETTER` of zelfs een **aangepaste grootte** door een `SizeF`‑object mee te geven, bijvoorbeeld:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **Pro‑tip:** Eén punt is gelijk aan 1/72 inch. Als je in millimeters denkt, vermenigvuldig dan met 2,83465 om punten te krijgen.

### Stap 3 – PDF genereren vanuit HTML: Conversie uitvoeren

`Converter.convertHTML` doet het zware werk. Het neemt het geladen `HTMLDocument`, het uitvoerpad en de opties die we zojuist hebben ingesteld.  

Wil je de **PDF‑paginagrootte** dynamisch bepalen op basis van de inhoud, dan kun je de benodigde afmetingen berekenen vóór deze stap en `pdfOptions` dienovereenkomstig aanpassen.

### Stap 4 – Resultaat verifiëren

De `System.out.println`‑regel is optioneel, maar geeft snelle feedback wanneer je het programma vanuit een console uitvoert. Na uitvoering open je `custom_page.pdf` – je zou een A4‑portret‑PDF moeten zien met overal een uniforme marge van 20 punt, precies zoals we hebben opgegeven.

## HTML naar PDF – Veelvoorkomende variaties

### Een stream gebruiken in plaats van een bestandspad

Soms heb je geen fysiek bestand; misschien komt de HTML uit een database of een API. In dat geval wikkel je de string in een `ByteArrayInputStream`:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

Het tweede argument is de basis‑URL voor het oplossen van relatieve bronnen.

### Pagina‑oriëntatie wijzigen

Is je rapport breed, schakel dan over naar landschapsmodus:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### Marges fijn afstellen

Marges accepteren zwevende‑kommagetallen, dus je kunt 0,5 pt instellen voor een haar­dunne rand:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### Grote HTML‑bestanden verwerken

Voor enorme documenten kun je overwegen **geheugen‑efficiënte streaming** in te schakelen:

```java
pdfOptions.setUseMemoryCache(true);
```

Dit vertelt Aspose om tussen­resultaten naar tijdelijke bestanden te schrijven in plaats van alles in RAM te houden.

## PDF‑paginagrootte instellen – Randgevallen & valkuilen

- **Ontbrekende lettertypen:** Als je HTML een aangepast lettertype gebruikt dat niet op de server is geïnstalleerd, valt de PDF terug op een standaardlettertype. Embed het lettertype met `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);`.  
- **Afbeeldingsschaling:** Hoge‑resolutie‑afbeeldingen kunnen de PDF onnodig vergroten. Gebruik `pdfOptions.setImageResolution(150);` om te verkleinen terwijl je de kwaliteit behoudt.  
- **CSS‑compatibiliteit:** Niet alle CSS‑eigenschappen worden volledig ondersteund. Houd je aan standaard‑layouttechnieken (flexbox werkt, maar grid kan eigenaardigheden vertonen).  
- **Pad‑rechten:** Zorg dat het proces schrijfrechten heeft voor `YOUR_DIRECTORY`. Anders wordt een `IOException` gegooid.

## Verwachte output

Het uitvoeren van het programma levert een PDF op die er ongeveer zo uitziet (conceptuele illustratie):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- Paginagrootte: **A4** (210 × 297 mm).  
- Oriëntatie: **Portret**.  
- Marges: **20 pt** aan elke zijde.  

Open het bestand met een PDF‑viewer (Adobe Reader, Chrome, enz.) om te bevestigen.

## Afronding

Je weet nu hoe je **PDF met aangepaste afmetingen** kunt maken vanuit een HTML‑bron met Aspose.HTML voor Java. De tutorial besloeg de volledige pijplijn: **HTML naar PDF converteren**, **PDF‑paginagrootte wijzigen**, **PDF‑paginagrootte instellen**, en **PDF genereren vanuit HTML** met aangepaste marges.  

Voel je vrij om te experimenteren—verwissel `PageSize.LETTER` voor legal size, pas de marges aan, of embed je eigen lettertypen. Als volgende stap kun je **watermerken toevoegen**, **de PDF versleutelen**, of **meerdere HTML‑bestanden batch‑verwerken**. Al die onderwerpen bouwen voort op dezelfde kernconcepten die we net hebben behandeld.

Heb je een vraag over een specifiek randgeval? Laat een reactie achter, en ik help je graag verder. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}