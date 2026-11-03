---
category: general
date: 2026-03-04
description: Hoe HTML te markeren door tekst in HTML te zoeken en elke overeenkomst
  te omhullen met een <mark>-tag. Stapsgewijze Java‑gids om tekst te vervangen door
  mark‑elementen.
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: nl
og_description: Hoe HTML te markeren door tekst in HTML te zoeken en overeenkomsten
  te omhullen met een <mark>-tag. Volledig Java-voorbeeld voor het vervangen van tekst
  met een <mark>-tag.
og_title: Hoe HTML markeren – Zoek tekst en vervang door <mark>
tags:
- Aspose.HTML
- Java
- Text Processing
title: Hoe HTML markeren – Zoek tekst en vervang door <mark>
url: /nl/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe HTML markeren – Tekst zoeken & vervangen met `<mark>`

Heb je je ooit afgevraagd **hoe je HTML kunt markeren** wanneer een bepaald woord meerdere keren voorkomt? Misschien bouw je een documentatiesite, een blogengine, of moet je gewoon een merknaam benadrukken op een statische pagina. Het goede nieuws? Het is best eenvoudig zodra je weet hoe je tekst in HTML kunt zoeken en de resultaten kunt omhullen met een `<mark>`‑element.

In deze tutorial lopen we een volledige Java‑oplossing door die een HTML‑bestand laadt, zoekt naar een doelwoord, elk voorkomen vervangt door een `<mark>`‑tag, en tenslotte de gemarkeerde versie opslaat. Aan het einde kun je **woord in HTML markeren**, **voorkomens van woord markeren**, en zelfs **tekst vervangen met mark** zonder de omliggende markup te breken.

> **Wat je nodig hebt**  
> • Java 17 of nieuwer (de code werkt ook met eerdere versies)  
> • Aspose.HTML for Java‑bibliotheek (gratis proefversie of gelicentieerde kopie)  
> • Een simpel HTML‑bestand dat je wilt verwerken  

Als je deze basis hebt, laten we erin duiken.  

![Schermafbeelding die gemarkeerde HTML‑output toont – hoe html markeren](/images/highlight-html-example.png "voorbeeld van hoe html markeren")

## Stap 1 – Laad het HTML‑document (Hoe HTML markeren)

Eerst moeten we het bronbestand in het geheugen laden. Aspose.HTML’s `Document`‑klasse doet al het zware werk, door de markup te parseren naar een DOM‑achtige structuur die we kunnen doorzoeken.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**Waarom dit belangrijk is:** Het laden van het document geeft ons een schoon objectmodel, zodat we tekst‑nodes veilig kunnen manipuleren zonder ons zorgen te maken over het breken van tags of attributen. Het normaliseert ook witruimte, waardoor de latere **tekst zoeken in html** stap betrouwbaarder wordt.

## Stap 2 – Tekst zoeken in HTML voor het doelwoord

Nu het document klaar is, zoeken we naar elk voorkomen van het woord dat we willen benadrukken. De `searchText`‑methode retourneert een lijst van `TextMatch`‑objecten, elk beschrijvend waar de match zich in de DOM bevindt.

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**Pro tip:** Het zoeken is standaard hoofdlettergevoelig. Als je een hoofdletterongevoelige zoekopdracht nodig hebt, zet dan zowel de documenttekst als `searchTerm` naar dezelfde hoofdlettervorm voordat je `searchText` aanroept, of gebruik een op reguliere expressies gebaseerde aanpak die de bibliotheek biedt.

## Stap 3 – Tekst vervangen door `<mark>` (Woord in HTML markeren)

Voor elke match reconstrueren we de tekst van de omvattende node en voegen we een `<mark>`‑element rond het exacte woord in. Dit zorgt ervoor dat we alleen de doeltekst beïnvloeden en de rest van de HTML onaangeroerd laten.

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**Uitleg:**  
- `getStartOffset`/`getEndOffset` geven ons de exacte tekenposities van de match binnen de bovenliggende node.  
- Door de originele tekst te slicen (`textBefore` en `textAfter`) behouden we alles andere precies zoals het was.  
- Het omhullen van de match met `<mark>` is de canonieke manier om **tekst te vervangen met mark** en native browser‑markering te krijgen zonder extra CSS.

### Randgevallen & Tips

- **Meerdere matches in dezelfde node:** De lus verwerkt elke `TextMatch` opeenvolgend. Omdat we elke keer de volledige node‑inhoud vervangen, verschuiven latere offsets. Aspose.HTML retourneert matches in documentvolgorde, dus de eenvoudige vervanging werkt in de meeste gevallen. Als je overlappende matches tegenkomt, verzamel dan eerst alle matches en bouw de node in één stap opnieuw op.  
- **Elementen die geen ruwe HTML kunnen bevatten:** Als de bovenliggende node een `<script>`‑ of `<style>`‑blok is, zou het invoegen van `<mark>` de pagina breken. Je kunt die nodes overslaan door `parentNode.getNodeName()` te controleren vóór vervanging.

## Stap 4 – Sla het gemarkeerde document op (Voorkomens van woord markeren)

Nadat alle vervangingen zijn uitgevoerd, schrijven we de aangepaste DOM terug naar schijf. Het uitvoerbestand bevat de originele markup plus de nieuwe `<mark>`‑tags, waardoor **voorkomens van woord** “Aspose” gemarkeerd worden.

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

Open `highlighted.html` in een willekeurige browser, en je ziet elk “Aspose” omgeven door een geelachtige achtergrond (de standaardstijl voor `<mark>`). Als je een eigen uitstraling wilt, voeg dan een kleine CSS‑regel toe:

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## Veelgestelde vragen (Tekst zoeken in HTML – FAQ)

**V: Wat als het woord voorkomt binnen een attribuutwaarde?**  
A: `searchText` kijkt alleen naar de tekstinhoud van nodes, niet naar attribuut‑strings. Om attribuutwaarden te markeren moet je over elementen itereren en attributen handmatig inspecteren.

**V: Kan ik meerdere verschillende woorden in één keer markeren?**  
A: Zeker. Bouw een lijst met termen, loop erdoorheen, en voer dezelfde vervangingslogica uit. Let wel op overlappende matches.

**V: Werkt dit met uitsluitend HTML5‑tags zoals `<section>` of `<article>`?**  
A: Ja. Aspose.HTML ondersteunt volledig moderne HTML5‑elementen, dus de DOM‑traversal werkt ongeacht het type tag.

## Volledig werkend voorbeeld (Alle stappen gecombineerd)

Hieronder staat het complete, kant‑klaar Java‑programma dat de volledige workflow demonstreert — van het laden van het bestand tot het opslaan van de gemarkeerde output.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**Verwachte output:** Open `highlighted.html` en je ziet elk voorkomen van “Aspose” gemarkeerd. Geen andere delen van de pagina worden aangepast, en het bestand blijft een geldig HTML‑document.

## Conclusie

We hebben behandeld **hoe je HTML kunt markeren** door programmatisch **tekst te zoeken in HTML**, elk resultaat te omhullen met een `<mark>`‑tag, en tenslotte de wijzigingen op te slaan. Deze aanpak stelt je in staat **woord in HTML te markeren**, **voorkomens van woord te markeren**, en **tekst te vervangen met mark** zonder fragiele string‑manipulatiecode te schrijven.

Volgende stappen? Probeer het script uit te breiden naar:

- Het accepteren van de zoekterm als command‑line‑argument.  
- Het genereren van een CSS‑bestand dat een aangepaste markeerkleur definieert.  
- Het verwerken van een hele map HTML‑bestanden in één batch.  

Die variaties verdiepen je begrip van zowel de Aspose.HTML‑API als algemene tekst‑verwerkingspatronen.  

Als je ergens vastloopt of ideeën hebt voor verdere verbeteringen, laat dan een reactie achter. Veel plezier met markeren!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}