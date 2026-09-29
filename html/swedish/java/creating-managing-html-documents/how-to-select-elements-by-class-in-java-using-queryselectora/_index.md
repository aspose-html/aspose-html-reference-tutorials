---
category: general
date: 2026-09-29
description: Lär dig hur du väljer element efter klass, läser HTML från fil och hittar
  externa länkar i Java. Denna steg‑för‑steg‑guide täcker hur du itererar en NodeList
  effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: sv
lastmod: 2026-09-29
og_description: Välj element efter klass i Java, läs HTML från fil och hitta externa
  länkar med querySelectorAll. Följ hela exemplet för att iterera en NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Välj element efter klass i Java – fullständig guide med querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Hur man väljer element efter klass i Java med querySelectorAll
url: /sv/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man väljer element efter klass i Java med querySelectorAll

Om du behöver **välja element efter klass** när du bearbetar en HTML‑fil i Java visar den här guiden exakt hur du gör det. Du lär dig att läsa HTML från fil, använda `querySelectorAll` för att hitta externa länkar och iterera den resulterande `NodeList` på ett säkert sätt.

Att arbeta med HTML i Java kan ofta kännas tungt, men moderna bibliotek ger dig ett koncist API baserat på CSS‑selektorer. Exemplet nedan använder **jsoup** (version 1.17.2) eftersom det implementerar `querySelectorAll`‑liknande selektorer och returnerar en `Elements`‑samling som beter sig som en `NodeList`. Du kan anpassa samma logik till andra DOM‑implementationer om så behövs.

## Förutsättningar

Innan du börjar, se till att du har:

* JDK 17 eller nyare installerat.
* Maven eller Gradle för beroendehantering.
* Grundläggande kunskap om Java‑streams och DOM‑modellen.

Lägg till jsoup i ditt projekt:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Steg 1: Läs HTML från fil

Den första uppgiften är att läsa in HTML‑dokumentet från disk. `Jsoup.parse(Path, Charset)` läser filen och bygger ett DOM‑träd som du kan fråga.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Varför detta är viktigt*: Att läsa in filen en gång undviker upprepad I/O när du itererar över element senare. `Document`‑objektet innehåller hela DOM‑trädet, vilket möjliggör snabba selektor‑frågor.

## Steg 2: Använd `querySelectorAll` för att välja element efter klass

Nu när dokumentet finns i minnet kan du **välja element efter klass** med en CSS‑selektor. Selektorn `"a.external"` matchar `<a>`‑taggar som har klassen `external` – exakt vad du behöver för att **hitta externa länkar**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Varför detta är viktigt*: Att använda en klass‑selektor är både uttrycksfullt och prestandaeffektivt. Biblioteket översätter selektorn till en optimerad traversal, så du behöver inte skriva manuella slingor över varje nod.

## Steg 3: Iterera NodeList (Elements) i Java

`Elements` implementerar `Iterable<Element>`, vilket betyder att du kan använda en vanlig `for‑each`‑loop för att **iterera NodeList Java**‑objekt. Loopen nedan skriver ut varje länks `href`‑attribut.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Varför detta är viktigt*: Direkt iteration håller koden läsbar och undviker overheaden av att konvertera samlingen till en stream när du bara behöver enkel utskrift.

## Fullt fungerande exempel

När du sätter ihop de tre stegen får du ett självständigt program som du kan köra från kommandoraden.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Förväntad output

Om `input.html` innehåller:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Skriver programmet ut:

```
External link: https://example.com
External link: https://openai.com
```

## Pro‑tips och vanliga fallgropar

* **Kodning är viktigt** – Läs alltid filen med UTF‑8 (eller den teckenkodning som matchar din källa). Fel kodning kan förstöra tecken i attributvärden.
* **Flera klasser** – Om ett element har flera klasser (t.ex. `class="btn external"`), matchar selektorn `"a.external"` fortfarande eftersom CSS‑klassselektorer kontrollerar närvaron av tokenen, inte den exakta strängen.
* **Prestandatips** – Om du bara behöver `href`‑attributet kan du begära det direkt med `doc.select("a.external[href]").eachAttr("href")`. Detta undviker att skapa fullständiga `Element`‑objekt för varje matchning.
* **Null‑säkerhet** – `link.attr("href")` returnerar en tom sträng om attributet saknas, så du behöver ingen null‑kontroll innan du skriver ut.

## Vanliga frågor

**Q: Fungerar detta med HTML‑fragment som saknar ett `<html>`‑rot?**  
A: Ja. `Jsoup.parse` behandlar indata som ett fragment och lägger automatiskt till saknade rotelement, så att selektorer fungerar på fragmentets body.

**Q: Kan jag använda `querySelectorAll` utan jsoup?**  
A: Standard‑Java‑DOM‑API (`org.w3c.dom`) innehåller inte `querySelectorAll`. Bibliotek som **HTMLUnit** eller **jodd-lagarto** erbjuder liknande metoder. Mönstret som visas här – ladda, välj med CSS, iterera – förblir detsamma.

**Q: Vad händer om jag vill modifiera länkarna istället för att bara skriva ut dem?**  
A: Efter att du har fått varje `Element` kan du anropa `link.attr("href", "newUrl")` och sedan skriva tillbaka dokumentet till disk med `Files.writeString`.

## Slutsats

Du vet nu hur du **väljer element efter klass**, **läser HTML från fil**, **hittar externa länkar** och **itererar en NodeList i Java** med `querySelectorAll`‑liknande selektorer. Det kompletta exemplet demonstrerar ett rent, produktionsklart arbetsflöde som du kan bädda in i större skrapnings‑ eller transformationspipeline.

Nästa steg är att utforska relaterade ämnen som **parsing av dynamiskt innehåll med HTMLUnit**, **skriva modifierad HTML tillbaka till disk**, eller **använda Java‑streams för att samla länkar till en lista**. Alla dessa bygger på den grundläggande tekniken för klass‑baserad selektion som demonstrerats här. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker nära besläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to query HTML in Java – Select elements, filter by attribute, and get text](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Iterate NodeList Java – Read HTML & Get Image src](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}