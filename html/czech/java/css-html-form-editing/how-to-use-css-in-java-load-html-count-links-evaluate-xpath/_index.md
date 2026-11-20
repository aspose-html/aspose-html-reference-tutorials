---
category: general
date: 2026-06-16
description: Jak použít CSS k načtení HTML souboru a počítání odkazů v Javě. Naučte
  se počítat HTML elementy a vyhodnocovat XPath v Javě v jednom jasném příkladu.
draft: false
keywords:
- how to use css
- load html file
- how to count links
- count html elements
- evaluate xpath java
language: cs
og_description: Jak použít CSS v Javě k načtení HTML souboru, spočítání odkazů a vyhodnocení
  XPath výrazů — vše v jednom praktickém průvodci.
og_title: Jak používat CSS v Javě – načíst HTML, spočítat odkazy a vyhodnotit XPath
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  headline: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  type: TechArticle
- description: How to use CSS to load HTML file and count links in Java. Learn to
    count html elements and evaluate xpath java in a single, clear example.
  name: How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath
  steps:
  - name: What if the HTML file is malformed?
    text: Both the CSS and XPath engines are tolerant of minor markup errors (missing
      closing tags, unquoted attributes). However, severe malformations may cause
      the parser to abort. In production, wrap the loading step in a try‑catch block
      and log the exception.
  - name: Can I combine CSS and XPath in a single expression?
    text: Not directly; each engine has its own syntax. The typical pattern is to
      use the one that expresses the condition most naturally (CSS for structural
      queries, XPath for attribute functions) and then merge the results in Java if
      needed.
  - name: How do I count elements across multiple files?
    text: 'Just place the loading logic inside a loop:'
  - name: Does this work with Java 8?
    text: Yes—provided you use a library version that targets Java 8 or higher. The
      code shown does not rely on newer language features.
  type: HowTo
tags:
- Java
- HTML parsing
- CSS selectors
- XPath
title: Jak používat CSS v Javě – načíst HTML, spočítat odkazy a vyhodnotit XPath
url: /cs/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat CSS v Javě – Načíst HTML, počítat odkazy a vyhodnotit XPath

Už jste se někdy zamysleli **jak používat CSS** selektory při zpracování HTML souboru v Javě? Možná stavíte web‑crawler, scraper, nebo jen potřebujete auditovat statický web. Dobrá zpráva? Nemusíte psát vlastní parser od nuly — moderní knihovny vám umožní kombinovat CSS4 selektory s XPath 3.1 výrazy v jednom přehledném workflow.

V tomto tutoriálu projdeme **jak načíst HTML soubor**, použijeme CSS selektor k počítání odkazů uvnitř navigačního panelu a poté **vyhodnotíme XPath** k počítání konkrétních elementů obrázků. Na konci budete mít kompletní, spustitelný program, který vytiskne počet odpovídajících uzlů, a pochopíte, proč je každá část důležitá.

## Požadavky

- Java 17 (nebo jakýkoli aktuální JDK) nainstalovaný na vašem počítači  
- Maven nebo Gradle pro správu závislostí (v příkladu použijeme Maven)  
- Malý úryvek HTML uložený jako `input.html` ve složce, kterou ovládáte  

Žádné další nástroje nejsou potřeba — stačí textový editor a terminál.

## Co tutoriál pokrývá

- **Načtení HTML souboru** do struktury podobné DOM pomocí třídy *HTMLDocument*  
- Použití **CSS4 selektoru** (`nav a[data-role]`) k nalezení navigačních odkazů  
- Spuštění **XPath 3.1 výrazu** pro nalezení tagů `<img>`, jejichž `src` končí na `.png` a které zároveň mají atribut `alt`  
- **Počítání** výsledků obou dotazů a jejich výpis do konzole  
- Úplný zdrojový kód, vysvětlení „proč“, a rychlý pohled na možné okrajové případy  

Pojďme na to.

---

## Krok 1 – Jak načíst HTML soubor pomocí HTMLDocument

Než budete moci něco dotazovat, musí být HTML dokument parsován do modelu, který lze procházet. Třída `HTMLDocument` z knihovny **jsoup‑plus** (nebo jakýkoli podobný HTML‑aware parser) dělá právě to.

```java
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Load the HTML document from the file system
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/input.html");
        // From here on we can query the DOM using CSS or XPath
```

*Proč je to důležité:*  
Načtení souboru jednou a uchování reference (`doc`) zabraňuje opakovanému I/O, což může být úzké hrdlo výkonu při zpracování velkých dávek stránek.

---

## Krok 2 – Jak použít CSS k počítání odkazů uvnitř `<nav>`

Nyní, když je dokument v paměti, můžeme použít CSS4 selektor k zachycení každého `<a>` elementu, který žije uvnitř `<nav>` a zároveň nese atribut `data‑role`. Jedná se o běžný vzor pro navigační menu, která používají datové atributy pro JavaScript háčky.

```java
        // Use a CSS4 selector to find every <a> inside a <nav> that has a data‑role attribute
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");
```

*Vysvětlení:*  
- `nav a[data-role]` znamená „jakýkoli `<a>` element s atributem `data‑role`, který je potomkem elementu `<nav>`.“  
- Selektor je kompatibilní s **CSS4**, což znamená, že můžete také použít pseudo‑třídy jako `:not()` nebo `:has()`, pokud se vaše potřeby rozšíří.

> **Pro tip:** Pokud potřebujete jen přímé potomky, nahraďte mezeru znakem `>` (`nav > a[data-role]`). Tím zmenšíte prohledávaný prostor a můžete urychlit zpracování velkých dokumentů.

---

## Krok 3 – Vyhodnocení XPath v Javě pro počítání konkrétních `<img>` elementů

XPath vyniká, když potřebujete filtrování založené na atributech, které není v CSS tak přímočaré. Zde najdeme každý `<img>`, jehož `src` končí na `.png` **a** který také definuje atribut `alt` — užitečné pro audity přístupnosti.

```java
        // Use an XPath 3.1 expression to locate all <img> elements whose src ends with .png and have an alt attribute
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");
```

*Proč XPath?*  
- `ends-with()` funkce je součástí XPath 3.1, umožňuje porovnání koncovky bez použití regulárních výrazů.  
- Kombinace více predikátů (`and @alt`) zajišťuje, že počítáte jen obrázky, které jsou jak správně zdrojové, tak i popsané.

Pokud vaše knihovna podporuje jen XPath 1.0, museli byste použít `contains(@src, '.png')` a poté filtrovat v Javě — méně přesný přístup.

---

## Krok 4 – Jak počítat HTML elementy a vypsat výsledky

Nakonec získáme délky obou objektů `NodeList` a vypíšeme je. Toto je část **jak počítat odkazy** v hádance, ale funguje pro jakoukoli kolekci uzlů.

```java
        // Output the number of matches for each query
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Očekávaný výstup v konzoli** (při předpokladu, že ukázkové HTML obsahuje 3 odpovídající odkazy a 2 odpovídající obrázky):

```
Nav links: 3
PNG images with alt: 2
```

Pokud jsou počty nula, dvakrát zkontrolujte syntaxi selektoru nebo ověřte, že `input.html` skutečně obsahuje očekávané elementy.

---

## Kompletní funkční příklad

Níže je kompletní, samostatný program, který můžete zkopírovat do souboru pojmenovaného `CssXPathDemo.java`. Obsahuje potřebné importy, jednoduchý úryvek `pom.xml` pro Maven a minimální HTML ukázku pro testování.

```java
/* CssXPathDemo.java */
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the HTML document
        HTMLDocument doc = new HTMLDocument("input.html");

        // Step 2: CSS selector – count navigation links with data-role
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");

        // Step 3: XPath expression – count PNG images that have alt text
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");

        // Step 4: Print the results
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Maven `pom.xml` excerpt** (add this dependency to pull in the HTML‑aware parser that supports both CSS4 and XPath 3.1):

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>html-parser-plus</artifactId>
        <version>2.3.1</version>
    </dependency>
</dependencies>
```

**Sample `input.html`** (place it in the same directory as the Java file):

```html
<!DOCTYPE html>
<html lang="en">
<head><title>Test Page</title></head>
<body>
<nav>
    <a href="/home" data-role="main">Home</a>
    <a href="/about" data-role="secondary">About</a>
    <a href="/contact">Contact</a>
</nav>
<img src="logo.png" alt="Company Logo">
<img src="banner.jpg">
<img src="icon.png" alt="Icon">
</body>
</html>
```

Spuštěním `mvn compile exec:java -Dexec.mainClass=CssXPathDemo` získáte očekávané počty uvedené výše.

---

## Okrajové případy a časté otázky

### Co když je HTML soubor poškozený?

Obě enginy, CSS i XPath, jsou tolerantní k menším chybám v markup (chybějící uzavírací tagy, neuzavřené atributy). Nicméně vážnější poškození může způsobit, že parser selže. V produkci obalte krok načítání do try‑catch bloku a logujte výjimku.

### Můžu kombinovat CSS a XPath v jednom výrazu?

Ne přímo; každý engine má vlastní syntaxi. Typický vzor je použít ten, který podmínku vyjadřuje nejpřirozeněji (CSS pro strukturální dotazy, XPath pro funkce atributů) a případně sloučit výsledky v Javě.

### Jak počítat elementy napříč více soubory?

Jednoduše umístěte logiku načítání do smyčky:

```java
for (Path p : Files.newDirectoryStream(Paths.get("html_folder"), "*.html")) {
    HTMLDocument doc = new HTMLDocument(p.toString());
    // repeat the queries...
}
```

### Funguje to s Java 8?

Ano — za předpokladu, že použijete verzi knihovny cílící na Java 8 nebo vyšší. Ukázaný kód nevyužívá novější jazykové funkce.

---

## Závěr

Ukázali jsme **jak používat CSS** selektory spolu s **evaluate xpath java** výrazy k **načtení HTML souboru**, **počítání odkazů** a **počítání html elementů**, které splňují konkrétní kritéria. Hlavní poznatky jsou:

- Načtěte dokument jednou pomocí `HTMLDocument`.  
- Využijte CSS4 pro jednoduché strukturální dotazy (`nav a[data-role]`).  
- Využijte XPath 3.1 pro výkonné funkce atributů (`ends-with(@src, '.png')`).  
- Získejte délku `NodeList` pro přesné počty.  

Odtud můžete skript rozšířit: přidat další selektory, zapisovat výsledky do CSV, nebo jej integrovat do většího crawling pipeline. Kombinace CSS a XPath vám dává flexibilitu řešit prakticky jakýkoli HTML‑scraping úkol.

Jste připraveni experimentovat? Zkuste vyměnit CSS selektor za `section article[data-id]` nebo změnit XPath tak, aby cílil na `<video>` tagy s konkrétním kodekem. Možnosti jsou neomezené.

Pokud vám tento průvodce přišel užitečný, klidně ho sdílejte, dejte hvězdičku repozitáři nebo zanechte komentář s vašimi vlastními případy použití. Šťastné kódování!

![diagram příkladu použití css](https://example.com/diagram.png "diagram příkladu použití css")

---


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak přidat CSS – Inline CSS do HTML dokumentů v Aspose.HTML pro Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Jak upravit CSS – Pokročilé externí úpravy CSS s Aspose.HTML pro Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)
- [Jak upravit strom HTML dokumentu v Aspose.HTML pro Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}