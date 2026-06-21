---
category: general
date: 2026-04-23
description: Hoe querySelectorAll in Java te gebruiken om elementen op klasse te filteren,
  attribuutwaarden te lezen en de NodeList te itereren voor productgegevensextractie.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: nl
og_description: Hoe querySelectorAll in Java te gebruiken om elementen op klasse te
  filteren, attribuutwaarden te lezen en de NodeList te itereren voor productgegevensextractie.
og_title: Hoe querySelectorAll in Java te gebruiken – Filteren op klasse
tags:
- Java
- HTML parsing
- DOM manipulation
title: Hoe querySelectorAll te gebruiken in Java – Filteren op klasse
url: /nl/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe querySelectorAll in Java te gebruiken – Filteren op klasse

querySelectorAll in Java gebruiken is de sleutel wanneer je specifieke elementen uit een HTML‑document moet halen. In deze tutorial filteren we elementen op klasse, lezen we attribuutwaarden, en itereren we over een NodeList om productprijzen van een cataloguspagina te halen.  

Heb je ooit naar een enorm HTML‑bestand gekeken en je afgevraagd hoe je alleen de “on‑sale” kaarten kunt halen zonder een eigen parser te schrijven? Dat is precies het probleem dat we hier oplossen—geen extra bibliotheken behalve Aspose.HTML, en een handvol eenvoudige stappen.

Je eindigt met een compleet, uitvoerbaar programma dat:

* **Selecteert elementen** met een CSS‑selector (`select elements css selector`),
* **Filtert op klasse** (`filter elements by class`),
* **Leest een aangepast attribuut** (`how to read attribute`),
* **Itereert over de resulterende NodeList** (`iterate nodelist java`).

Ervaring met Aspose.HTML is niet vereist—alleen een basis Java‑omgeving en een HTML‑bestand om tegen te testen.

![hoe querySelectorAll in Java te gebruiken voorbeeld](https://example.com/images/queryselectorall-java.png "hoe querySelectorAll in Java te gebruiken")

---

## Wat je nodig hebt

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| **Java 17+** | Moderne taalfeatures en betere module‑afhandeling. |
| **Aspose.HTML for Java** (latest version) | Biedt de `Document`‑klasse en CSS‑selector engine. |
| **catalog.html** (sample HTML) | De bron waartegen we een query uitvoeren. |
| **IDE or plain `javac`** | Om de demo te compileren en uit te voeren. |

Als je Aspose.HTML nog niet aan je project hebt toegevoegd, plaats dan de JAR in je `libs`‑map en voeg deze toe aan de classpath:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Stap 1 – Laad het HTML‑document

Voordat je iets kunt queryen, heb je een `Document`‑object nodig dat het HTML‑bestand vertegenwoordigt. Beschouw het als het laden van een spreadsheet voordat je cellen kunt lezen.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Waarom dit belangrijk is:** De `Document`‑klasse parseert de markup naar een DOM‑boom, waardoor de CSS‑selector engine kan werken. Als je deze stap overslaat, houd je alleen een platte string over en kun je `querySelectorAll` niet gebruiken.

---

## Stap 2 – Selecteer elementen met een CSS‑selector

Nu volgt het hart van de zaak: **hoe querySelectorAll te gebruiken**. De methode accepteert elke geldige CSS‑selector, zodat je zo precies—of zo breed—kunt zijn als je wilt. Voor ons scenario willen we productkaarten die:

* de klasse `product-card` hebben,
* ook gemarkeerd zijn met de klasse `sale`,
* en een `data-price` attribuut bevatten.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Uitleg:**  
> * `.product-card.sale` → filtert elementen die **beide** klassen bevatten.  
> * `[data-price]` → zorgt ervoor dat het attribuut bestaat, waardoor je effectief **elementen filtert op klasse** **en** attribuut in één oproep.  
> * Het resultaat is een `NodeList`, een geordende collectie waar je over kunt itereren.

Als je ooit **elementen wilt selecteren met een css selector** voor een ander patroon, wijzig dan gewoon de string—geen code‑herwerking nodig.

---

## Stap 3 – Itereer de NodeList in Java

Een `NodeList` gedraagt zich veel als een array, maar implementeert geen `Iterable`. Daarom gebruiken we een klassieke `for`‑loop—perfect voor **iterate nodelist java** scenario's.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Waarom een `for`‑loop?**  
> Het geeft je directe toegang tot de index, wat handig kan zijn voor logging of conditionele vertakkingen. Als je de voorkeur geeft aan een `while`‑loop, blijft de logica identiek—verander alleen de loop‑constructie.

---

## Stap 4 – Lees het `data-price` attribuut

Nu beantwoorden we eindelijk **hoe je een attribuut leest** van een element. In de DOM‑API retourneert `getAttribute` de ruwe string, precies zoals die in de markup staat.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Tip:** Als het attribuut mogelijk ontbreekt, retourneert `getAttribute` `null`. Je kunt dat afvangen met een eenvoudige controle:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Stap 5 – Output de resultaten

Tot slot printen we elke prijs naar de console. Dit weerspiegelt een real‑world scenario waarin je de waarden waarschijnlijk naar een database of een API‑payload zou sturen.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Verwachte console‑output

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Als de selector geen overeenkomende nodes vindt, wordt de loop simpelweg nooit uitgevoerd—er wordt geen uitzondering gegooid. Dat is een mooie veiligheidsvoorziening voor **edge cases** waarin de catalogus leeg kan zijn.

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is het volledige bestand dat je kunt kopiëren‑plakken in `CssSelectorDemo.java`:

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

Sla het bestand op, compileer en voer uit—zie de prijzen verschijnen. 🎉

---

## Veelgestelde vragen & Pro‑tips

| Vraag | Antwoord |
|-------|----------|
| *Wat als ik ook op tag‑naam moet selecteren?* | Plaats gewoon de tag vooraan: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Kan ik meerdere attribuutfilters combineren?* | Zeker. Voorbeeld: `[data-price][data-stock]` behoudt alleen elementen die **beide** attributen hebben. |
| *Is `querySelectorAll` hoofdlettergevoelig?* | Ja—CSS‑selectors behandelen klasse‑ en attribuutnamen als hoofdlettergevoelig in HTML5. |
| *Hoe ga ik om met een enorm HTML‑bestand?* | Aspose.HTML streamt het document, maar je kunt de selector ook beperken tot een subboom (`someElement.querySelectorAll(...)`). |
| *Wat

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}