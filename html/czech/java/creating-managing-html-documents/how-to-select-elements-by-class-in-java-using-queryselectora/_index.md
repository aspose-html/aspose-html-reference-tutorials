---
category: general
date: 2026-09-29
description: Naučte se, jak vybírat prvky podle třídy, číst HTML ze souboru a najít
  externí odkazy v Javě. Tento krok‑za‑krokem průvodce pokrývá efektivní iteraci NodeListu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: cs
lastmod: 2026-09-29
og_description: Vyberte prvky podle třídy v Javě, načtěte HTML ze souboru a najděte
  externí odkazy pomocí querySelectorAll. Sledujte celý příklad pro iteraci NodeListu.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Výběr elementů podle třídy v Java – kompletní průvodce s querySelectorAll
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
title: Jak vybrat prvky podle třídy v Javě pomocí querySelectorAll
url: /cs/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak vybrat prvky podle třídy v Javě pomocí querySelectorAll

Pokud potřebujete **vybrat prvky podle třídy** při zpracování HTML souboru v Javě, tento návod vám přesně ukáže, jak na to. Naučíte se načíst HTML ze souboru, použít `querySelectorAll` k nalezení externích odkazů a bezpečně iterovat výsledný `NodeList`.

Práce s HTML v Javě často působí těžkopádně, ale moderní knihovny vám poskytují stručné API založené na CSS‑selektorech. Níže uvedený příklad používá **jsoup** (verze 1.17.2), protože implementuje selektory ve stylu `querySelectorAll` a vrací kolekci `Elements`, která se chová jako `NodeList`. Stejnou logiku můžete přizpůsobit i jiným implementacím DOM, pokud je to potřeba.

## Požadavky

* Nainstalovaný JDK 17 nebo novější.
* Maven nebo Gradle pro správu závislostí.
* Základní znalost Java streamů a modelu DOM.

Add jsoup to your project:

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

## Krok 1: Načtení HTML ze souboru

Prvním úkolem je načíst HTML dokument z disku. `Jsoup.parse(Path, Charset)` načte soubor a vytvoří DOM strom, který můžete dotazovat.

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

*Proč je to důležité*: Načtení souboru jednou zabraňuje opakovanému I/O při iteraci přes prvky později. Objekt `Document` obsahuje celý DOM, což umožňuje rychlé dotazy pomocí selektorů.

## Krok 2: Použití `querySelectorAll` k výběru prvků podle třídy

Jakmile je dokument v paměti, můžete **vybrat prvky podle třídy** pomocí CSS selektoru. Selektor `"a.external"` odpovídá značkám `<a>`, které mají třídu `external` — přesně to, co potřebujete k **nalezení externích odkazů**.

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

*Proč je to důležité*: Použití selektoru třídy je jak výmluvné, tak výkonné. Knihovna překládá selektor do optimalizované procházky, takže nemusíte psát ruční smyčky přes každý uzel.

## Krok 3: Iterace NodeList (Elements) v Javě

`Elements` implementuje `Iterable<Element>`, což znamená, že můžete použít standardní smyčku `for‑each` k **iteraci NodeList v Javě**. Níže uvedená smyčka vypíše atribut `href` každého odkazu.

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

*Proč je to důležité*: Přímá iterace udržuje kód čitelný a vyhýbá se režii převodu kolekce na stream, když potřebujete jen jednoduchý výstup.

## Kompletní funkční příklad

Spojením tří kroků získáte samostatný program, který můžete spustit z příkazové řádky.

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

### Očekávaný výstup

Předpokládejme, že `input.html` obsahuje:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Spuštěním programu se vypíše:

```
External link: https://example.com
External link: https://openai.com
```

## Profesionální tipy a běžné úskalí

* **Kódování má význam** – Vždy čtěte soubor s UTF‑8 (nebo s kódováním, které odpovídá vašemu zdroji). Nesprávné kódování může poškodit znaky v hodnotách atributů.
* **Více tříd** – Pokud má prvek několik tříd (např. `class="btn external"`), selektor `"a.external"` stále odpovídá, protože CSS selektory tříd kontrolují přítomnost tokenu, nikoli přesný řetězec.
* **Tip pro výkon** – Pokud potřebujete jen atribut `href`, můžete jej získat přímo pomocí `doc.select("a.external[href]").eachAttr("href")`. Tím se vyhnete vytváření kompletních objektů `Element` pro každou shodu.
* **Bezpečnost proti null** – `link.attr("href")` vrací prázdný řetězec, pokud atribut chybí, takže před výpisem nepotřebujete kontrolu na null.

## Často kladené otázky

**Q: Funguje to s HTML fragmenty, které postrádají kořen `<html>`?**  
A: Ano. `Jsoup.parse` považuje vstup za fragment a automaticky přidá chybějící kořenové elementy, což umožňuje selektorům fungovat na těle fragmentu.

**Q: Můžu použít `querySelectorAll` bez jsoup?**  
A: Standardní Java DOM API (`org.w3c.dom`) neobsahuje `querySelectorAll`. Knihovny jako **HTMLUnit** nebo **jodd-lagarto** poskytují podobné metody. Vzor zde ukázaný — načtení, výběr pomocí CSS, iterace — zůstává stejný.

**Q: Co když potřebuji upravit odkazy místo jejich pouhého výpisu?**  
A: Po získání každého `Element` můžete zavolat `link.attr("href", "newUrl")` a poté zapsat dokument zpět na disk pomocí `Files.writeString`.

## Závěr

Nyní víte, jak **vybrat prvky podle třídy**, **načíst HTML ze souboru**, **najít externí odkazy** a **iterovat NodeList v Javě** pomocí selektorů ve stylu `querySelectorAll`. Kompletní příklad ukazuje čistý, produkčně připravený workflow, který můžete začlenit do větších pipeline pro scraping nebo transformaci.

Dále prozkoumejte související témata, jako je **parsování dynamického obsahu pomocí HTMLUnit**, **zápis upraveného HTML zpět na disk**, nebo **použití Java streamů k sesbírání URL odkazů do seznamu**. Každé z nich staví na základní technice výběru podle třídy, která je zde demonstrována. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to query HTML in Java – Select elements, filter by attribute, and get text](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Iterate NodeList Java – Read HTML & Get Image src](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}