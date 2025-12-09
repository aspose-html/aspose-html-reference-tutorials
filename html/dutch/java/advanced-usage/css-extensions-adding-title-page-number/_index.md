---
date: 2025-12-05
description: Leer hoe u HTML-paginamarges instelt in Java met Aspose.HTML, en paginanummers
  en titels aan uw documenten toevoegt.
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Hoe HTML-paginamarges instellen in Java met Aspose.HTML
url: /nl/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe HTML-paginamarges instellen in Java met Aspose.HTML

In deze tutorial ontdek je **hoe je HTML-paginamarges in Java**‑stijl instelt met Aspose.HTML voor Java. We lopen door het maken van aangepaste paginamarges, het invoegen van paginanummers en het toevoegen van een documenttitel — allemaal met duidelijke, stap‑voor‑stap code die je kunt kopiëren naar je eigen project.

## Snelle antwoorden
- **Welke bibliotheek is nodig?** Aspose.HTML for Java  
- **Kan ik marges programmatisch regelen?** Ja, via een CSS `@page`‑regel in het gebruikers‑stijlblad  
- **Welke uitvoerformaten ondersteunen marges?** XPS, PDF en andere rasterformaten  
- **Heb ik een licentie nodig voor productie?** Een geldige Aspose.HTML‑licentie is vereist voor niet‑trial gebruik  
- **Is dit compatibel met Java 11+?** Absoluut – de bibliotheek werkt met moderne Java‑versies  

## Wat betekent “HTML-paginamarges instellen in Java”?
HTML-paginamarges instellen in Java betekent het configureren van de renderengine (geleverd door Aspose.HTML) om CSS‑page‑box‑eigenschappen toe te passen voordat het document wordt geconverteerd naar een afdrukbaar formaat zoals XPS of PDF. Door een aangepaste `@page`‑regel te definiëren, beheer je het afdrukbare gebied, paginanummers en header/footer‑inhoud.

## Waarom Aspose.HTML gebruiken voor marge‑beheer?
- **Precieze lay‑out** – CSS `@page` geeft je pixel‑perfecte controle over marges, headers en footers.  
- **Cross‑format consistentie** – Dezelfde marge‑definities werken voor XPS, PDF en afbeeldings‑output.  
- **Geen browser‑afhankelijkheid** – Rendering gebeurt server‑side, dus je hebt geen headless browser nodig.  

## Vereisten

Voordat we beginnen, zorg ervoor dat je de volgende vereisten hebt:

1. **Java‑ontwikkelomgeving** – JDK 11 of later geïnstalleerd.  
2. **Aspose.HTML for Java** – Download en installeer de bibliotheek van [hier](https://releases.aspose.com/html/java/).  

## Pakketten importeren

Om te beginnen, importeer je de benodigde Aspose.HTML‑klassen:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Hoe HTML-paginamarges in Java instellen – Stapsgewijze gids

### Stap 1: Configuratie initialiseren en aangepaste paginamarges definiëren

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

In dit blok maken we een `Configuration`‑object, verkrijgen de `IUserAgentService` en injecteren een CSS `@page`‑regel die de marges, een rechtsonder paginateller en een boven‑midden documenttitel definieert.

### Stap 2: Het HTML‑document maken

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Hier instantieren we een `HTMLDocument` met een eenvoudige “Hello World”‑snippet. Dezelfde configuratie van Stap 1 wordt toegepast, zodat de aangepaste marges gerespecteerd worden bij het renderen van het document.

### Stap 3: Renderen naar een XPS‑bestand (of een ander ondersteund formaat)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Deze stap maakt een `XpsDevice` die de gerenderde pagina's naar `output.xps` schrijft. De marges, paginanummers en titel die je eerder hebt gedefinieerd, verschijnen in het uiteindelijke bestand.

## Veelvoorkomende problemen & tips

- **Marges lijken onveranderd** – Zorg ervoor dat de `@page`‑regel niet wordt overschreven door andere stylesheets. De `setUserStyleSheet`‑aanroep dwingt deze naar de hoogste prioriteit.  
- **Paginanummers tonen “NaN”** – Controleer of je Aspose.HTML versie 23.10 of nieuwer gebruikt; oudere versies missen de `currentPageNumber()`‑functie.  
- **Uitvoerbestand is leeg** – Bevestig dat het pad `Resources.output` correct wordt opgelost en dat je schrijfrechten hebt.  

## Veelgestelde vragen

### Q1: Wat is Aspose.HTML for Java?

**A:** Aspose.HTML for Java is een Java‑bibliotheek die krachtige tools biedt voor het werken met HTML‑documenten in Java‑applicaties, inclusief conversie, rendering en manipulatie.

### Q2: Kan ik de paginamarges verder aanpassen?

**A:** Ja, bewerk eenvoudig de CSS binnen `setUserStyleSheet`. Je kunt elke `margin-*`‑waarde wijzigen of extra `@top-*` / `@bottom-*`‑boxen toevoegen.

### Q3: Hoe kan ik meer inhoud aan het HTML‑document toevoegen?

**A:** Vervang de string in `new HTMLDocument("<div>Hello World!!!</div>", …)` door je eigen HTML‑markup, of laad een extern bestand met de `HTMLDocument(String url, …)`‑constructor.

### Q4: Is Aspose.HTML for Java compatibel met andere documentformaten?

**A:** Absoluut. Hetzelfde `HTMLDocument` kan worden gerenderd naar PDF, XPS, afbeeldingen, of zelfs EPUB door het uitvoerapparaat te wisselen (bijv. `PdfDevice`, `PngDevice`).

### Q5: Heb ik een licentie nodig voor het gebruik van Aspose.HTML for Java?

**A:** Ja, een licentie is vereist voor productiegebruik. Je kunt een proefversie verkrijgen of een licentie aanschaffen via [hier](https://purchase.aspose.com/buy) of [hier](https://releases.aspose.com/).

### Q6: Hoe stel ik verschillende marges in voor oneven en even pagina's?

**A:** Gebruik de `@page :left` en `@page :right` pseudo‑klassen in je stylesheet om verschillende marges te definiëren voor linker‑hand (even) en rechter‑hand (oneven) pagina's.

### Q7: Kan ik aangepaste lettertypen in het gerenderde document insluiten?

**A:** Ja. Voeg `@font-face`‑regels toe aan de gebruikers‑stylesheet en verwijs naar de lettertypen in je HTML‑inhoud.

## Conclusie

Je hebt nu **hoe je HTML-paginamarges in Java** instelt met Aspose.HTML onder de knie, en je weet hoe je paginanummers en een titel kunt toevoegen om je documenten er professioneel uit te laten zien. Voel je vrij om te experimenteren met extra `@page`‑boxen, aangepaste lettertypen, of verschillende uitvoerformaten om aan de behoeften van je project te voldoen.

Als je tegen uitdagingen aanloopt, zijn de officiële [Aspose.HTML for Java-documentatie](https://reference.aspose.com/html/java/) en het [Aspose‑ondersteuningsforum](https://forum.aspose.com/) uitstekende plekken om hulp te vinden.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 23.12  
**Author:** Aspose