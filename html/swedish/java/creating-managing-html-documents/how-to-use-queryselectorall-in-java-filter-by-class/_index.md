---
category: general
date: 2026-04-23
description: Hur man använder querySelectorAll i Java för att filtrera element efter
  klass, läsa attributvärden och iterera över NodeList för att extrahera produktdata.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: sv
og_description: Hur man använder querySelectorAll i Java för att filtrera element
  efter klass, läsa attributvärden och iterera NodeList för att extrahera produktdata.
og_title: Hur man använder querySelectorAll i Java – Filtrera efter klass
tags:
- Java
- HTML parsing
- DOM manipulation
title: Hur man använder querySelectorAll i Java – Filtrera efter klass
url: /sv/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du querySelectorAll i Java – Filtrera efter klass

Att använda querySelectorAll i Java är nyckeln när du behöver hämta specifika element från ett HTML‑dokument. I den här handledningen kommer vi att filtrera element efter klass, läsa attributvärden och iterera en NodeList för att hämta produktpriser från en katalogsida.  

Har du någonsin stirrat på en enorm HTML‑fil och undrat hur du bara kan hämta “on‑sale”-kort utan att skriva en egen parser? Det är exakt det problem vi kommer att lösa här—utan extra bibliotek utöver Aspose.HTML, och med några enkla steg.

Du får ett komplett, körbart program som:

* **Väljer element** med en CSS‑selector (`select elements css selector`),
* **Filtrerar efter klass** (`filter elements by class`),
* **Läser ett anpassat attribut** (`how to read attribute`),
* **Itererar den resulterande NodeList** (`iterate nodelist java`).

Ingen tidigare erfarenhet av Aspose.HTML krävs—bara en grundläggande Java‑miljö och en HTML‑fil att testa mot.

![exempel på hur man använder querySelectorAll i Java](https://example.com/images/queryselectorall-java.png "hur man använder querySelectorAll i Java")

---

## Vad du behöver

| Krav | Varför det är viktigt |
|------|-----------------------|
| **Java 17+** | Moderna språkfunktioner och bättre modulhantering. |
| **Aspose.HTML for Java** (latest version) | Tillhandahåller `Document`‑klassen och CSS‑selector‑motorn. |
| **catalog.html** (sample HTML) | Källan vi kommer att fråga mot. |
| **IDE or plain `javac`** | För att kompilera och köra demonstrationen. |

Om du ännu inte har lagt till Aspose.HTML i ditt projekt, lägg JAR‑filen i din `libs`‑mapp och lägg till den i classpath:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Steg 1 – Ladda HTML‑dokumentet

Innan du kan göra någon sökning behöver du ett `Document`‑objekt som representerar HTML‑filen. Tänk på det som att ladda ett kalkylblad innan du kan läsa några celler.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Varför detta är viktigt:** `Document`‑klassen parsar markupen till ett DOM‑träd, vilket möjliggör att CSS‑selector‑motorn kan fungera. Att hoppa över detta steg skulle lämna dig med en vanlig sträng och ingen möjlighet att använda `querySelectorAll`.

---

## Steg 2 – Välj element med en CSS‑selector

Nu kommer kärnan i saken: **hur man använder querySelectorAll**. Metoden accepterar vilken giltig CSS‑selector som helst, så du kan vara så exakt—eller så bred—som du vill. För vårt scenario vill vi ha produktkort som:

* har klassen `product-card`,
* är också markerade med klassen `sale`,
* och har ett `data-price`‑attribut.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Förklaring:**  
> * `.product-card.sale` → filtrerar element som innehåller **båda** klasserna.  
> * `[data-price]` → säkerställer att attributet finns, vilket effektivt **filtrerar element efter klass** **och** attribut i ett enda anrop.  
> * Resultatet är en `NodeList`, som är en ordnad samling du kan iterera över.

Om du någonsin behöver **select elements css selector** för ett annat mönster, ändra bara strängen—ingen kodomskrivning krävs.

---

## Steg 3 – Iterera NodeList i Java

`NodeList` beter sig mycket som en array, men den implementerar inte `Iterable`. Därför använder vi en klassisk `for`‑loop—perfekt för **iterate nodelist java**‑scenarier.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Varför en `for`‑loop?**  
> Den ger dig direkt åtkomst till indexet, vilket kan vara praktiskt för loggning eller villkorlig förgrening. Om du föredrar en `while`‑loop, förblir logiken identisk—byt bara loop‑konstruktionen.

---

## Steg 4 – Läs `data-price`‑attributet

Nu svarar vi äntligen på **how to read attribute**‑värden från ett element. I DOM‑API:t returnerar `getAttribute` den råa strängen, exakt som den visas i markupen.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Tips:** Om attributet kan saknas returnerar `getAttribute` `null`. Du kan skydda dig mot det med en enkel kontroll:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Steg 5 – Skriv ut resultaten

Sist men inte minst skriver vi ut varje pris till konsolen. Detta speglar ett verkligt scenario där du troligen skulle skicka värdena till en databas eller ett API‑payload.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Förväntad konsolutmatning

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Om selectorn inte hittar några matchande noder körs loopen helt enkelt aldrig—inget undantag kastas. Det är ett bra skyddsnät för **edge cases** där katalogen kan vara tom.

---

## Fullt fungerande exempel

När vi sätter ihop allt, här är den kompletta filen som du kan kopiera‑klistra in i `CssSelectorDemo.java`:

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

Spara filen, kompilera och kör—se priserna strömma ut. 🎉

---

## Vanliga frågor & pro‑tips

| Fråga | Svar |
|-------|------|
| *Vad händer om jag också behöver välja efter taggnamn?* | Lägg bara till taggen i början: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Kan jag kedja flera attributfilter?* | Absolut. Exempel: `[data-price][data-stock]` behåller endast element som har **båda** attributen. |
| *Är `querySelectorAll` skiftlägeskänslig?* | Ja—CSS‑selectorer behandlar klass- och attributnamn som skiftlägeskänsliga i HTML5. |
| *Hur hanterar jag en enorm HTML‑fil?* | Aspose.HTML strömmar dokumentet, men du kan också begränsa selectorn till ett underträd (`someElement.querySelectorAll(...)`). |
| *What

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}