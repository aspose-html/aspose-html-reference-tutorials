---
category: general
date: 2026-10-28
description: Leer hoe je links in een nieuw tabblad kunt openen door HTML te parseren
  in Java, externe links te vinden en target="_blank" toe te voegen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: nl
lastmod: 2026-10-28
og_description: 'Open links in een nieuw tabblad met Java: parse HTML, vind externe
  links, voeg target=''_blank'' toe en sla de aangepaste HTML op.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Open links in een nieuw tabblad met Java – stap‑voor‑stap gids
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Hoe links in een nieuw tabblad te openen met Java
url: /nl/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe links in een nieuw tabblad te openen met Java

Als je **links in een nieuw tabblad** moet openen vanuit een statisch HTML‑bestand, laat deze gids je precies zien hoe je dat doet. Je leert **HTML in Java te parseren**, **externe links te vinden**, **target blank toe te voegen**, en **gewijzigde HTML op te slaan** zonder je IDE te verlaten.

Het openen van externe links in een nieuw browsertabblad verbetert de gebruikerservaring en houdt bezoekers op de oorspronkelijke pagina. De onderstaande oplossing werkt met elk HTML‑document, vereist alleen de populaire jsoup‑bibliotheek, en draait op Java 8 of nieuwer.

## Vereisten

* JDK 8 + geïnstalleerd  
* Een build‑tool (Maven of Gradle) om de **jsoup**‑dependency binnen te halen  
* Een HTML‑bestand dat anker‑tags bevat met de klasse `external`

Je hebt geen webserver of extra frameworks nodig—jsoup regelt alles lokaal.

## Stap 1: jsoup instellen in je project

Voeg jsoup toe als dependency. Als je Maven gebruikt, plaats dit in `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Voor Gradle, voeg de volgende regel toe aan `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Deze coördinaten halen de nieuwste stabiele release op (vanaf oktober 2026). Na het synchroniseren kun je `org.jsoup`‑klassen importeren in je Java‑bronbestanden.

## Stap 2: Parse het HTML‑document

Het parseren van het bestand is de eerste stap naar **links in een nieuw tabblad openen**. De `Jsoup.parse`‑methode leest het bestand in een mutabele DOM‑achtige structuur.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Waarom dit belangrijk is*: `Document` geeft je CSS‑achtige selectors, waardoor het triviaal is de elementen te vinden die je nodig hebt.

## Stap 3: Externe links vinden

Zoek nu elk `<a>`‑element dat de klasse `external` heeft. Dit voldoet aan de **externe links vinden**‑vereiste.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` is een collectie van overeenkomende knooppunten. Als de selector een lege set retourneert, mist je HTML de klasse of gebruikt het een andere naamgevingsconventie—pas de selector dienovereenkomstig aan.

## Stap 4: Voeg `target="_blank"` toe aan elke link

Voor elke node die wordt geretourneerd door **externe links vinden**, stel je het `target`‑attribuut in op `_blank`. Dit voldoet aan de **add target blank**‑stap en zorgt ervoor dat browsers de link in een nieuw tabblad openen.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

De `attr`‑methode overschrijft elke bestaande `target`‑waarde, waardoor consistent gedrag over alle externe ankers wordt gegarandeerd.

## Stap 5: Sla de gewijzigde HTML op

Na het bijwerken van de DOM, schrijf je de wijzigingen terug naar een bestand. Dit voltooit het **save modified html**‑deel van de tutorial.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` serialiseert het volledige document, behoudt inspringing en opmaak zoals jsoup het oorspronkelijk heeft geparseerd.

## Volledig werkend voorbeeld

Alle stappen samenvoegen levert een zelfstandige programma op dat je kunt kopiëren, plakken en uitvoeren.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Verwachte output

Stel dat `sample.html` bevat:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Na het uitvoeren van het programma, zal `updated.html` bevatten:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Alleen de externe link heeft het `target="_blank"`‑attribuut gekregen, wat betekent dat browsers deze nu in een nieuw tabblad openen.

## Pro‑tips en veelvoorkomende valkuilen

* **Pro tip:** Als je links die beginnen met `http://` of `https://` als extern wilt behandelen, zelfs zonder een CSS‑klasse, breid dan de selector uit: `doc.select("a[href^=http]")`.
* **Edge case:** Sommige pagina's specificeren al `target="_self"`; de `attr`‑aanroep overschrijft dit, waardoor consistent gedrag wordt gegarandeerd.
* **Performance:** Voor zeer grote HTML‑bestanden, overweeg streaming‑parsing (`Jsoup.parse(File, String, String, Parser.htmlParser())`) om het geheugenverbruik te verminderen.
* **Testing:** Verifieer het resultaat door `updated.html` in een browser te openen en de link te inspecteren met de ontwikkelaarstools—zoek naar het `target`‑attribuut.

## Conclusie

Je hebt nu een complete, uitvoerbare oplossing om **links in een nieuw tabblad te openen** met Java. De tutorial behandelde hoe je **html in java parseert**, **externe links vindt**, **target blank toevoegt**, en **gewijzigde html opslaat**, allemaal met de lichte jsoup‑bibliotheek.

Vanaf hier kun je:

* De selector uitbreiden om andere linkpatronen te behandelen (bijv. `rel="external"`).  
* Deze logica combineren met een build‑stap die alle HTML‑bestanden in een project verwerkt.  
* De code integreren in een grotere content‑management‑pipeline.

Voel je vrij om te experimenteren met verschillende selectors of outputformaten, en deel je resultaten met de community!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe CSS in Java te gebruiken – HTML laden, links tellen & XPath evalueren](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [Hoe HTML in Java te parseren – Tekst extraheren uit HTML‑artikelen](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Nieuw HTML‑element maken met Java – Volledige Aspose.HTML‑gids](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}