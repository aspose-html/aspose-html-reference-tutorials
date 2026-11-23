---
category: general
date: 2026-03-05
description: Hoe HTML in Java te query’en om een HTML‑bestand te lezen en afbeeldingen
  te extraheren. Leer hoe je een HTML‑bestand leest in Java, afbeelding‑URL’s ophaalt
  in Java, en over een NodeList iterereert in Java.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: nl
og_description: Hoe HTML te queryen in Java en afbeeldings‑URL’s op te halen. Deze
  gids laat zien hoe je een HTML‑bestand in Java leest, afbeeldingen vindt en over
  een NodeList in Java iterereert.
og_title: Hoe HTML te queryen in Java – Afbeeldings‑URL’s extraheren
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: Hoe HTML te bevragen in Java – Afbeeldings‑URL’s extraheren
url: /nl/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML in Java opvragen – Afbeeldings‑URL's extraheren

Heb je je ooit afgevraagd **hoe je HTML kunt opvragen** in Java om elke afbeelding op een pagina te halen? Je bent niet de enige—ontwikkelaars moeten voortdurend HTML‑bestanden lezen, afbeeldingen scrapen en vervolgens iets nuttigs met de URL's doen. In deze tutorial lopen we een praktisch voorbeeld door dat precies laat zien **hoe je HTML kunt opvragen**, een HTML‑bestand leest in Java‑stijl, en afbeeldings‑URL's op Java‑manier verkrijgt.

We gebruiken Aspose.HTML voor Java, maar de concepten—XPath, CSS‑selectoren en itereren over een `NodeList`—zijn toepasbaar op elke DOM‑bibliotheek. Aan het einde van deze gids ben je vertrouwd met **hoe je afbeeldingen kunt extraheren**, weet je **hoe je over NodeList in Java kunt itereren**, en heb je een kant‑klaar code‑fragment dat je in je project kunt gebruiken.

![Voorbeeld van HTML opvragen in Java](https://example.com/placeholder.png "Voorbeeld van HTML opvragen in Java")

---

## Wat je zult leren

- Een HTML‑document van schijf laden (read HTML file Java)  
- `<img>`‑tags vinden met zowel XPath als CSS‑selectoren (how to extract images)  
- Door de verkregen `NodeList` itereren (iterate over NodeList Java)  
- Het `src`‑attribuut van elke afbeelding afdrukken (get image URLs Java)

Geen externe services, geen complexe build‑tools—alleen plain Java en één Maven‑dependency.

---

## Voorvereisten

- Java 8 of nieuwer geïnstalleerd  
- Maven of Gradle voor dependency‑beheer  
- Basiskennis van HTML‑structuur  
- Optioneel maar handig: een simpel HTML‑bestand (`sample.html`) met enkele `<figure><img …></figure>`‑elementen  

Als je die hebt, kunnen we meteen beginnen.

---

## Stap 1: HTML‑bestand lezen in Java – Document laden

Allereerst moeten we de HTML in het geheugen brengen. De `HTMLDocument`‑klasse van Aspose.HTML doet het zware werk. Zie het als het openen van een boek zodat je naar elke pagina kunt bladeren.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Waarom dit belangrijk is:** Het laden van het bestand geeft je een DOM‑boom die je kunt doorzoeken. Als het pad onjuist is, krijg je een `FileNotFoundException`, dus controleer de locatie dubbel voordat je het programma start.

---

## Stap 2: Afbeeldingen vinden met XPath – Hoe je afbeeldingen kunt extraheren

XPath is een krachtige querytaal waarmee je knooppunten met laserprecisie kunt aanwijzen. Hier vragen we om elk `<img>`‑element binnen een `<figure>` dat bovendien een `alt`‑attribuut heeft.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Waarom XPath?** Het is beknopt en werkt zelfs wanneer de HTML rommelig is. De expressie `//figure/img[@alt]` betekent: “elk `<img>` onder een `<figure>` dat een `alt`‑attribuut draagt.” Als je op andere attributen wilt filteren, pas dan simpelweg de haakjes aan.

---

## Stap 3: Afbeeldingen vinden met CSS‑selector – Alternatieve manier om afbeeldingen te extraheren

Soms geef je de voorkeur aan CSS‑syntaxis omdat die overeenkomt met wat je in stylesheets schrijft. `querySelectorAll` accepteert dezelfde selector die je in een browser zou gebruiken.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Waarom beide?** Het tonen van beide methoden laat zien dat je de tool kunt kiezen waar je het meest mee vertrouwd bent. In de praktijk blijf je bij één aanpak, maar beide voorbeelden maken de tutorial completer.

---

## Stap 4: Over NodeList itereren in Java – Afbeeldings‑URL's ophalen in Java

Nu we een collectie hebben, moeten we er doorheen lopen. Hier komt **iterate over NodeList Java** om de hoek kijken. We halen het `src`‑attribuut van elke afbeelding op en printen het.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Waarom een klassieke `for`‑lus?** De Aspose `NodeList` implementeert geen `Iterable`, dus de verbeterde `for‑each`‑syntaxis compileert niet. Een index‑lus gebruiken is de betrouwbare manier **om over NodeList Java te itereren**.

---

## Verwachte output

Het programma uitvoeren tegen een voorbeeld‑HTML zoals:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Zal iets vergelijkbaars opleveren:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

Bevat je bestand meer `<img>`‑tags die aan de criteria voldoen, dan zullen de aantallen dienovereenkomstig toenemen.

---

## Veelvoorkomende valkuilen & pro‑tips

- **Problemen met bestands‑pad:** Gebruik een absoluut pad of plaats `sample.html` relatief ten opzichte van de werkdirectory van je project.  
- **Ontbrekend `alt`‑attribuut:** Onze XPath/CSS‑queries filteren op `[@alt]`. Als je *alle* afbeeldingen nodig hebt, laat dan de attribuutfilter weg (`//figure/img` of `figure img`).  
- **Prestaties:** Voor zeer grote documenten kun je overwegen streaming‑parsers te gebruiken, maar voor de meeste web‑scraping‑taken is de DOM‑aanpak prima.  
- **Encoding‑problemen:** Aspose.HTML respecteert de charset die in de HTML is gedeclareerd. Zie je onleesbare tekens, zorg dan dat het bestand is opgeslagen als UTF‑8.  

---

## Voorbeeld uitbreiden

Nu je **image URLs Java kunt ophalen**, wil je misschien:

1. **De afbeeldingen downloaden** met `java.net.URL` en `Files.copy`.  
2. **URL's opslaan in een database** voor latere verwerking.  
3. **Filteren op bestandsextensie** (`src.endsWith(".png")`).  

Al deze uitbreidingen zijn eenvoudige variaties op de lus die in Stap 4 wordt getoond.

---

## Conclusie

In deze gids hebben we **hoe je HTML kunt opvragen** in Java van begin tot eind behandeld: het bestand laden, afbeeldingen vinden met zowel XPath als CSS‑selectoren, en **over NodeList Java itereren** om het `src`‑attribuut van elke afbeelding te printen. Je hebt nu een solide basis voor **hoe je afbeeldingen kunt extraheren**, en je weet precies **hoe je HTML‑bestand in Java kunt lezen** met Aspose.HTML.

Voel je vrij de code aan te passen aan je eigen scraping‑behoeften—of je nu andere attributen wilt ophalen, `<a>`‑tags wilt verwerken, of de URL's aan een downloader wilt doorgeven. Het patroon blijft hetzelfde: laden, queryen, itereren en handelen.

Heb je vragen of wil je een cool use‑case delen? Laat een reactie achter hieronder, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}