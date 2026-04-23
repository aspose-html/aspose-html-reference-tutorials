---
category: general
date: 2026-04-23
description: Jak použít querySelectorAll v Javě k filtrování elementů podle třídy,
  čtení hodnot atributů a iteraci přes NodeList pro extrakci dat o produktech.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: cs
og_description: Jak použít querySelectorAll v Javě k filtrování prvků podle třídy,
  čtení hodnot atributů a iteraci NodeListu pro extrakci dat o produktech.
og_title: Jak použít querySelectorAll v Javě – filtrovat podle třídy
tags:
- Java
- HTML parsing
- DOM manipulation
title: Jak použít querySelectorAll v Javě – filtrování podle třídy
url: /cs/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít querySelectorAll v Javě – filtrování podle třídy

Použití querySelectorAll v Javě je klíčové, když potřebujete získat konkrétní elementy z HTML dokumentu. V tomto tutoriálu budeme filtrovat elementy podle třídy, číst hodnoty atributů a iterovat přes NodeList, abychom získali ceny produktů z katalogové stránky.  

Už jste někdy zíral na obrovský HTML soubor a přemýšlel, jak získat jen „on‑sale“ karty bez psaní vlastního parseru? To je přesně ten problém, který zde vyřešíme — žádné další knihovny kromě Aspose.HTML a několik jednoduchých kroků.

Získáte kompletní, spustitelný program, který:

* **Selects elements** using a CSS selector (`select elements css selector`),
* **Filters by class** (`filter elements by class`),
* **Reads a custom attribute** (`how to read attribute`),
* **Iterates the resulting NodeList** (`iterate nodelist java`).

Předchozí zkušenost s Aspose.HTML není vyžadována — stačí základní nastavení Javy a HTML soubor, na kterém můžete testovat.

![příklad použití querySelectorAll v Javě](https://example.com/images/queryselectorall-java.png "příklad použití querySelectorAll v Javě")

---

## Co budete potřebovat

| Požadavek | Proč je důležité |
|-------------|----------------|
| **Java 17+** | Moderní jazykové funkce a lepší správa modulů. |
| **Aspose.HTML for Java** (latest version) | Poskytuje třídu `Document` a engine pro CSS‑selector. |
| **catalog.html** (sample HTML) | Zdroj, proti kterému budeme dotazovat. |
| **IDE or plain `javac`** | Pro kompilaci a spuštění demonstrace. |

If you haven’t added Aspose.HTML to your project yet, drop the JAR into your `libs` folder and add it to the classpath:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Krok 1 – Načtení HTML dokumentu

Než budete moci něco dotazovat, potřebujete objekt `Document`, který představuje HTML soubor. Představte si to jako načtení tabulky, než budete moci číst buňky.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Proč je to důležité:** Třída `Document` parsuje značkovací jazyk do DOM stromu, což umožňuje fungování CSS‑selector engine. Vynechání tohoto kroku by vám zanechalo jen obyčejný řetězec a žádnou možnost použít `querySelectorAll`.

---

## Krok 2 – Výběr elementů pomocí CSS selektoru

Now comes the heart of the matter: **how to use querySelectorAll**. The method accepts any valid CSS selector, so you can be as precise—or as broad—as you like. For our scenario we want product cards that:

* má třídu `product-card`,
* je také označena třídou `sale`,
* a obsahuje atribut `data-price`.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Vysvětlení:**  
> * `.product-card.sale` → filtruje elementy, které obsahují **obě** třídy.  
> * `[data-price]` → zajišťuje, že atribut existuje, efektivně **filtruje elementy podle třídy** **a** atributu v jednom volání.  
> * Výsledkem je `NodeList`, což je uspořádaná kolekce, kterou můžete iterovat.  

Pokud budete někdy potřebovat **select elements css selector** pro jiný vzor, stačí změnit řetězec — není potřeba přepisovat kód.

---

## Krok 3 – Iterace NodeListu v Javě

`NodeList` se chová podobně jako pole, ale neimplementuje `Iterable`. Proto používáme klasický `for` cyklus — ideální pro scénáře **iterate nodelist java**.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Proč `for` cyklus?**  
> Poskytuje přímý přístup k indexu, což může být užitečné pro logování nebo podmíněné větvení. Pokud dáváte přednost `while` cyklu, logika zůstává stejná — stačí změnit konstrukci smyčky.

---

## Krok 4 – Čtení atributu `data-price`

Nyní konečně odpovídáme na otázku **how to read attribute** hodnot z elementu. V DOM API `getAttribute` vrací surový řetězec přesně tak, jak je v markup.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Tip:** Pokud může atribut chybět, `getAttribute` vrací `null`. Můžete se proti tomu chránit jednoduchou kontrolou:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Krok 5 – Výstup výsledků

Na závěr, vytiskneme každou cenu do konzole. To odráží reálný scénář, kde byste pravděpodobně hodnoty vložili do databáze nebo API payloadu.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Očekávaný výstup v konzoli

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Pokud selektor nenajde žádné odpovídající uzly, smyčka se jednoduše nikdy neprovede — výjimka není vyhozena. To je pěkná pojistka pro **edge cases**, kdy může být katalog prázdný.

---

## Kompletní funkční příklad

Putting it all together, here’s the complete file you can copy‑paste into `CssSelectorDemo.java`:

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

Uložte soubor, zkompilujte a spusťte — sledujte, jak se ceny vypisují. 🎉

---

## Často kladené otázky a tipy

| Otázka | Odpověď |
|----------|--------|
| *Co když potřebuji také vybírat podle názvu tagu?* | Stačí před řetězec přidat tag: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Mohu řetězit více filtrů atributů?* | Ano. Příklad: `[data-price][data-stock]` ponechá jen elementy, které mají **obě** atributy. |
| *Je `querySelectorAll` citlivý na velikost písmen?* | Ano — CSS selektory považují názvy tříd a atributů za citlivé na velikost písmen v HTML5. |
| *Jak zacházet s obrovským HTML souborem?* | Aspose.HTML streamuje dokument, ale můžete také omezit selektor na podstrom (`someElement.querySelectorAll(...)`). |
| *What

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}