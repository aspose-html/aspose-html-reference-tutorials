---
category: general
date: 2026-01-01
description: Naučte se, jak dotazovat HTML pomocí Javy, jak vybírat CSS a jak extrahovat
  prvky z HTML pomocí praktických příkladů a počítání uzlů.
draft: false
keywords:
- how to query html
- how to select css
- extract elements from html
- select multiple css classes
- how to count nodes
language: cs
og_description: Zvládněte, jak dotazovat HTML v Javě, naučte se vybírat CSS, extrahovat
  prvky z HTML a počítat uzly pomocí skutečných příkladů kódu.
og_title: Jak dotazovat HTML v Javě – kompletní tutoriál
tags:
- Java
- HTML parsing
- Aspose.HTML
title: Jak dotazovat HTML v Javě – kompletní tutoriál
url: /cs/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dotazovat HTML v Javě – Kompletní tutoriál

Už jste se někdy zamýšleli **jak dotazovat HTML** z Java programu, aniž byste si roztrhali vlasy? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují získat data ze statického katalogu nebo stáhnout jednoduchou stránku, a běžné DOM triky působí nešikovně.  

Dobrá zpráva? Několik řádků kódu vám umožní načíst HTML soubor, spustit XPath nebo CSS selektory a dokonce spočítat uzly, na které vám záleží – vše v jednom přehledném toku. V tomto průvodci si projdeme **jak dotazovat HTML**, **jak vybírat CSS**, a ukážeme vám, jak **extrahovat elementy z HTML**, **vybrat více CSS tříd** a **jak spočítat uzly** pomocí Aspose.HTML pro Java.

## Co se naučíte

- Načíst HTML dokument z disku nebo URL.  
- Použít XPath k nalezení elementů, které splňují složité podmínky.  
- Použít CSS selektory, včetně dotazů na více tříd.  
- Programově spočítat výsledky.  
- Tipy, úskalí a varianty pro reálné scénáře.

*Požadavky*: Java 8+, Maven nebo Gradle a kopie knihovny Aspose.HTML pro Java (bezplatná zkušební verze stačí pro experimentování).

---

![příklad dotazování HTML](https://example.com/images/query-html.png "Snímek obrazovky ukazující, jak dotazovat HTML pomocí Javy")

## Jak dotazovat HTML – Načtení dokumentu

Než budete moci klást jakékoli otázky, potřebujete objekt dokumentu, který budete zkoumat. Třída `HTMLDocument` z Aspose.HTML dělá těžkou práci.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document you want to query
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");
```

> **Proč je to důležité** – Načtení souboru vytvoří DOM strom v paměti. Odtud můžete spouštět jak XPath, tak CSS dotazy, aniž byste se museli starat o síťovou latenci nebo špatně formátovaný markup. Pokud soubor není nalezen, Aspose vyhodí jasnou výjimku `FileNotFoundException`, což usnadňuje ladění.

### Pro tip
Pokud získáváte HTML ze vzdáleného webu, stačí předat řetězec URL do `HTMLDocument` – Aspose ho pro vás stáhne a parsuje.

## Jak vybírat CSS – Použití CSS selektorů

Jakmile je DOM připraven, výběr uzlů pomocí CSS je tak jednoduchý jako jednorázový řádek. Získáme každý element, který má buď třídu `featured`, nebo `highlight`.

```java
        // Step 2: Locate elements marked as featured or highlighted using a CSS selector
        List<Element> featuredElements = document.selectCss(".featured, .highlight");

        // Step 3: Output the number of elements found by the CSS selector
        System.out.println("Featured elements: " + featuredElements.size());
```

> **Vysvětlení** – Selektor `.featured, .highlight` říká enginu, aby vrátil *jakýkoli* element, jehož atribut `class` obsahuje `featured` **nebo** `highlight`. Toto je kanonický způsob, jak **vybrat více CSS tříd** v jednom dotazu.

### Hraniční případ
Pokud element obsahuje obě třídy (např. `<div class="featured highlight">`), objeví se **jednou** ve výsledném seznamu, čímž se zabrání dvojímu počítání.

## Extrahovat elementy z HTML – Kombinace XPath a CSS

XPath vyniká, když potřebujete relační logiku, například „všechny `<book>` uzly, kde cena přesahuje 30“. Zde je přesný úryvek z původního příkladu:

```java
        // Step 4: Find all <book> elements with a price greater than 30 using XPath
        List<Element> expensiveBooks = document.selectXPath("//book[price>30]");

        // Step 5: Output the number of books that match the XPath query
        System.out.println("Expensive books count: " + expensiveBooks.size());
```

> **Proč XPath?** – XPath dokáže přímo vyhodnocovat číselné porovnání (`price>30`), což CSS neumí. Také vám umožní procházet vztahy rodič/dítě bez dalšího kódu.

### Varianta
Pokud potřebujete získat *názvy* těch drahých knih, můžete připojit druhý dotaz:

```java
        List<Element> titles = expensiveBooks.get(0).selectXPath("./title");
        System.out.println("First expensive book title: " + titles.get(0).getTextContent());
```

## Vybrat více CSS tříd – Pokročilé triky s selektory

Někdy chcete cílit na elementy, které **současně** mají několik tříd, např. `class="product featured"`. Syntaxe CSS pro to je spojený selektor bez čárek.

```java
        // Example: select <div> elements that are both .product and .featured
        List<Element> productFeatured = document.selectCss("div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured.size());
```

> **Klíčový bod** – Mezera mezi názvy tříd nesmí být; mezera by znamenala „potomek“. Tento vzor je zásadní, když **vybíráte více CSS tříd**, které společně stylují komponentu.

## Jak spočítat uzly – Získání přesných součtů

Počítání uzlů je často posledním krokem v pipeline pro extrakci dat. Už jste viděli použití `list.size()` po každém dotazu, ale zabalíme to do znovupoužitelné pomůcky.

```java
    /**
     * Returns the count of elements that match the given CSS selector.
     */
    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    /**
     * Returns the count of elements that match the given XPath expression.
     */
    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        System.out.println("Expensive books: " + countByXPath(doc, "//book[price>30]"));
        System.out.println("Featured items: " + countByCss(doc, ".featured, .highlight"));
        System.out.println("Product‑featured divs: " + countByCss(doc, "div.product.featured"));
    }
```

> **Proč to zabalit?** – Centralizace logiky počítání usnadňuje testování kódu a snižuje duplicitu. Také to objasňuje **jak spočítat uzly** pro budoucí čtenáře.

### Časté úskalí
- **Mezery v atributu class** – `"featured "` (koncová mezera) stále odpovídá `.featured`, protože selektor ořezává bílé znaky.  
- **Rozlišování velkých a malých písmen** – HTML názvy tříd jsou v XML režimu citlivé na velikost písmen; ujistěte se, že váš zdrojový HTML používá jednotné psaní.

## Kompletní funkční příklad

Spojením všeho dohromady získáte samostatný program, který můžete zkopírovat a vložit do svého IDE:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.Element;
import java.util.List;

public class QueryDemo {

    private static int countByCss(HTMLDocument doc, String selector) {
        return doc.selectCss(selector).size();
    }

    private static int countByXPath(HTMLDocument doc, String xpath) {
        return doc.selectXPath(xpath).size();
    }

    public static void main(String[] args) throws Exception {
        // Load the HTML file (adjust the path as needed)
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/catalog.html");

        // XPath: books priced over 30
        int expensiveBooks = countByXPath(document, "//book[price>30]");
        System.out.println("Expensive books count: " + expensiveBooks);

        // CSS: featured or highlighted elements
        int featured = countByCss(document, ".featured, .highlight");
        System.out.println("Featured elements: " + featured);

        // CSS: elements that are both .product and .featured
        int productFeatured = countByCss(document, "div.product.featured");
        System.out.println("Product‑featured divs: " + productFeatured);
    }
}
```

**Očekávaný výstup** (při typickém `catalog.html`):

```
Expensive books count: 4
Featured elements: 7
Product‑featured divs: 2
```

Pokud váš soubor obsahuje méně odpovídajících uzlů, čísla se upraví podle toho – žádná překvapení.

---

## Závěr

Probrali jsme **jak dotazovat HTML** pomocí Aspose.HTML pro Java, ukázali **jak vybírat CSS**, ukázali vám, jak **extrahovat elementy z HTML**, řešili **vybrat více CSS tříd** a vysvětlili **jak spočítat uzly** spolehlivě.  

Hlavní ponaučení? Načíst dokument jednou a poté znovu použít stejnou instanci `HTMLDocument` vám umožní kombinovat XPath a CSS dotazy bez výkonových penalizací.  

Jste připraveni na další krok? Zkuste řetězit selektory pro získání hodnot atributů (`@href`, `@src`) nebo exportovat výsledek do JSON pro další zpracování. Můžete také prozkoumat zpracování stránkování, pokud váš zdrojový HTML pokrývá více stránek.

Máte složitý selektor nebo hraniční případ, který se vám nedaří vyřešit? Zanechte komentář níže a pojďme to společně rozlousknout. Šťastné dotazování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}