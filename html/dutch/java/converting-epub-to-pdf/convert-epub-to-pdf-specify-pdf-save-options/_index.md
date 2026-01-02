---
date: 2026-01-02
description: Leer hoe u EPUB naar PDF kunt converteren in Java met Aspose.HTML terwijl
  u een aangepast PDF-paginaformaat en andere PDF-opslagopties instelt.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Aangepaste PDF-paginagrootte: PDF-opslagopties specificeren voor EPUB naar
  PDF'
url: /nl/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aangepaste PDF-paginagrootte: PDF-opslagopties specificeren voor EPUB naar PDF

## Inleiding

Aspose.HTML for Java maakt het eenvoudig om **EPUB naar PDF** te **converteren** en geeft je volledige controle over de output, inclusief het instellen van een **aangepaste PDF-paginagrootte**. In deze stapsgewijze handleiding lopen we alles door wat je nodig hebt—van het voorbereiden van je omgeving tot het aanpassen van de `PdfSaveOptions` zodat de gegenereerde PDF exact overeenkomt met de paginagrootte die je vereist. Of je nu een publicatie‑pipeline bouwt, een e‑learningplatform, of gewoon documentconversie wilt automatiseren, je zult de technieken hier waardevol vinden.

## Snelle antwoorden
- **Wat is het primaire doel van deze tutorial?** Een EPUB‑bestand naar PDF converteren terwijl een aangepaste PDF-paginagrootte wordt toegepast.  
- **Welke bibliotheek wordt gebruikt?** Aspose.HTML for Java.  
- **Heb ik een licentie nodig?** Een gratis proefversie is beschikbaar; een commerciële licentie is vereist voor productie.  
- **Kan ik de achtergrondkleur wijzigen?** Ja, met `PdfSaveOptions`.  
- **Wordt Java 8+ ondersteund?** Absoluut—elke moderne Java‑runtime werkt.

## Wat is een aangepaste PDF-paginagrootte?

Een aangepaste PDF-paginagrootte stelt je in staat de exacte breedte en hoogte van elke pagina in de uitvoer‑PDF te definiëren, in plaats van te vertrouwen op standaardformaten zoals A4 of Letter. Dit is vooral nuttig voor e‑books, flyers of elke situatie waarin de visuele lay‑out moet overeenkomen met een specifiek ontwerp.

## Waarom Aspose.HTML gebruiken voor EPUB‑naar‑PDF-conversie?

- **Hoge getrouwheid:** Behoudt complexe lay‑outs, lettertypen en afbeeldingen.  
- **Fijnmazige controle:** Pas paginagrootte, achtergrond, marges en meer aan via `PdfSaveOptions`.  
- **Cross‑platform:** Werkt op Windows, Linux en macOS met dezelfde Java‑code.  
- **Prestaties:** Geoptimaliseerde renderengine voor snelle conversies.

## Voorwaarden

- **Java-ontwikkelomgeving:** JDK 8 of later geïnstalleerd en geconfigureerd.  
- **Aspose.HTML for Java:** Download de nieuwste JAR van de [website](https://releases.aspose.com/html/java/).  
- **EPUB‑bestand:** Een `.epub`‑document dat je wilt converteren.  

Nu alles klaar is, laten we duiken in de daadwerkelijke conversiestappen.

## Stap 1: Open het EPUB‑bestand

Eerst moeten we het EPUB‑bestand openen met een `FileInputStream`. Deze stream wordt later aan de converter doorgegeven.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Stap 2: Definieer PDF-opslagopties

Hier stellen we de **aangepaste PDF-paginagrootte** en een optionele achtergrondkleur in. Pas de pixelwaarden aan om overeen te komen met de gewenste afmetingen.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

### Pro‑tip:
- **Pixels vs. Points:** `Length.fromPixels` zet schermpixels om naar PDF‑points (1 point = 1/72 inch). Kies waarden die de uiteindelijke afdrukgrootte weerspiegelen die je nodig hebt.

## Stap 3: Converteer EPUB naar PDF

Met de invoerstroom en aangepaste opties klaar, roep je de converter aan. De uitvoer‑PDF wordt opgeslagen op de locatie die je opgeeft.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Volledige broncode

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Veelvoorkomende problemen en oplossingen

| Probleem | Oorzaak | Oplossing |
|----------|---------|-----------|
| **PDF-pagina's zijn leeg** | Invoerstroom gesloten vóór conversie | Houd het `try‑with‑resources`‑blok open tot na `convertEPUB`. |
| **Onjuiste paginagrootte** | Pixels die niet overeenkomen met de gewenste afdrukgrootte | Converteer gewenste inches naar points (`1 inch = 72 points`) en vervolgens naar pixels met `Length.fromPixels`. |
| **Ontbrekende lettertypen** | Lettertypen niet ingebed in EPUB | Zorg ervoor dat de lettertypen in de EPUB zijn verpakt of installeer ze op de hostmachine. |

## Veelgestelde vragen (FAQ's)

### Is Aspose.HTML for Java een gratis bibliotheek?
Aspose.HTML for Java is een commerciële bibliotheek, maar je kunt een gratis proefversie verkrijgen via hun [website](https://releases.aspose.com/).

### Welke EPUB-formaten worden ondersteund voor conversie?
Aspose.HTML for Java ondersteunt de conversie van verschillende EPUB-formaten, waardoor compatibiliteit met de meeste EPUB‑documenten wordt gegarandeerd.

### Kan ik de PDF-output verder aanpassen?
Ja, je kunt de PDF-output aanpassen door de paginainstelling, achtergrondkleur en andere instellingen in de `PdfSaveOptions` te wijzigen.

### Zijn er beperkingen aan de proefversie van Aspose.HTML for Java?
De proefversie kan enkele beperkingen hebben, dus het wordt aanbevolen de documentatie te raadplegen voor details.

### Waar kan ik ondersteuning krijgen voor Aspose.HTML for Java?
Je kunt antwoorden op je vragen vinden en ondersteuning zoeken op het [Aspose.HTML‑forum](https://forum.aspose.com/).

**Laatst bijgewerkt:** 2026-01-02  
**Getest met:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}