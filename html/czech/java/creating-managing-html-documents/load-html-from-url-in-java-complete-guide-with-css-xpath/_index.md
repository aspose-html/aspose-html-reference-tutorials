---
category: general
date: 2026-07-02
description: Načtěte HTML z URL pomocí Aspose.HTML pro Javu, poté vyberte prvky s
  atributem, extrahujte odkazy ke stažení a spočítejte uzly XPath v několika snadných
  krocích.
draft: false
keywords:
- load html from url
- select elements with attribute
- extract download links
- search html with css
- count xpath nodes
language: cs
og_description: Načtěte HTML z URL v Javě, poté použijte CSS selektory a XPath k výběru
  elementů s atributem, extrahujte odkazy ke stažení a spočítejte uzly XPath.
og_title: Načíst HTML z URL v Javě – Kompletní tutoriál CSS a XPath
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Load HTML from URL using Aspose.HTML for Java, then select elements
    with attribute, extract download links, and count XPath nodes in a few easy steps.
  headline: Load HTML from URL in Java – Complete Guide with CSS & XPath
  type: TechArticle
- description: Load HTML from URL using Aspose.HTML for Java, then select elements
    with attribute, extract download links, and count XPath nodes in a few easy steps.
  name: Load HTML from URL in Java – Complete Guide with CSS & XPath
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-html</artifactId>
      <version>23.10</version> <!-- Check for the latest version --> </dependency>
      ```'
  - name: Gradle
    text: '```gradle implementation ''com.aspose:aspose-html:23.10'' ```'
  - name: What the selector means
    text: '| Part | Meaning | |------|---------| | `a` | any `<a>` element | | `[href*=''download'']`
      | attribute `href` that **contains** the substring `download` (`*=` is the “contains”
      operator) |'
  - name: Expected console output (may vary by site)
    text: '``` Document loaded from https://example.com'
  type: HowTo
tags:
- Java
- Aspose.HTML
- Web Scraping
title: Načtení HTML z URL v Javě – Kompletní průvodce s CSS a XPath
url: /cs/java/creating-managing-html-documents/load-html-from-url-in-java-complete-guide-with-css-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Načtení HTML z URL v Javě – Kompletní průvodce s CSS a XPath

Už jste někdy potřebovali **načíst HTML z URL** v Java aplikaci a získat konkrétní odkazy, aniž byste psali plnohodnotný web‑crawler? Nejste v tom sami. Ať už vytváříte správce stahování, agregátor obsahu, nebo jste jen zvědaví na stránky, které navštěvujete, schopnost načíst stránku, **prohledat HTML pomocí CSS** a následně **počítat uzly XPath** je užitečná dovednost.

V tomto tutoriálu projdeme celý proces: od načtení vzdálené stránky do paměti, přes použití CSS selektoru k **výběru prvků s atributem**, extrahování těch **odkazů ke stažení**, až po ověření stejného výsledku pomocí XPath dotazu. Žádné externí služby, jen čistá Java a knihovna Aspose.HTML for Java.

> **Požadavky** – Budete potřebovat nainstalovanou Javu 8+, Maven nebo Gradle pro správu závislostí a základní pochopení HTML a syntaxe Javy. Pokud jste v Aspose.HTML noví, nebojte se; krok za krokem vám ukážeme nastavení.

---

## Co vytvoříte

Na konci tohoto průvodce budete mít spustitelnou Java třídu, která:

1. **Načte HTML z URL** (např. `https://example.com`).
2. **Prohledá DOM pomocí CSS selektoru** a najde každý `<a>` tag, jehož `href` obsahuje „download“.
3. **Extrahuje a vypíše každý odkaz ke stažení**.
4. **Spustí ekvivalentní XPath dotaz** a vypíše, kolik uzlů bylo nalezeno.

Také uvidíte malý diagram, který vizualizuje tok—pro případ, že jste vizuální typ.

![Diagram zobrazující tok načítání HTML z URL, výběru prvků, extrakce odkazů a počítání uzlů XPath](load-html-from-url-diagram.png)

---

## Krok 1: Přidejte Aspose.HTML for Java do svého projektu

Nejprve základ. Aspose.HTML je komerční knihovna, ale nabízí bezplatnou zkušební verzi, která pro výukové účely funguje perfektně.

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

> **Tip:** Pokud později narazíte na `NoClassDefFoundError`, zkontrolujte, že jar `aspose-html` je ve vašem runtime classpath.

---

## Krok 2: Načtěte HTML z URL a inicializujte dokument

Nyní, když je knihovna k dispozici, můžeme skutečně **načíst HTML z URL**. Třída `HTMLDocument` přijímá řetězec URL a postará se o HTTP požadavek, přesměrování a detekci znakové sady.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class HtmlDownloader {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Define the target page
        String pageUrl = "https://example.com";

        // Step 2.2: Load the page into an HTMLDocument object
        HTMLDocument document = new HTMLDocument(pageUrl);

        System.out.println("Document loaded successfully.");
        // From here on we can query the DOM.
    }
}
```

**Proč to funguje:** `HTMLDocument` interně vytváří `HttpWebRequest`, následuje přesměrování a vytváří DOM strom, který se chová stejně jako `document` v prohlížeči. To znamená, že můžeme okamžitě používat jak CSS selektory, tak XPath.

---

## Krok 3: Prohledávejte HTML pomocí CSS – Vyberte prvky s atributem

Nejčtivější způsob, jak najít prvky, je pomocí CSS selektoru. V našem případě chceme každý `<a>`, jehož atribut `href` obsahuje slovo „download“. Syntaxe selektoru `a[href*='download']` dělá právě to.

```java
// Step 3: Find all anchor elements whose href contains "download"
NodeList downloadLinks = document.selectElements("a[href*='download']");

// Quick sanity check – how many did we find?
System.out.println("CSS found " + downloadLinks.getLength() + " nodes.");
```

### Co selektor znamená

| Part | Význam |
|------|--------|
| `a` | jakýkoli `<a>` element |
| `[href*='download']` | atribut `href`, který **obsahuje** podřetězec `download` (`*=` je operátor „obsahuje“) |

> **Hraniční případ:** Pokud stránka používá relativní URL (např. `href="/files/download.zip"`), Aspose.HTML je ponechá tak, jak jsou. Později je možná budete muset vyřešit vůči základní URL.

---

## Krok 4: Extrahujte odkazy ke stažení

Nyní, když máme `NodeList`, získání skutečných URL je triviální. Každý uzel přetypujeme na `Element` a přečteme jeho atribut `href`.

```java
System.out.println("\n--- Extracted Download Links ---");
for (int i = 0; i < downloadLinks.getLength(); i++) {
    Element anchor = (Element) downloadLinks.item(i);
    String href = anchor.getAttribute("href");
    // Resolve relative URLs to absolute ones (optional but handy)
    String absoluteHref = document.getBaseUrl().resolve(href).toString();
    System.out.println(absoluteHref);
}
```

**Výsledek, který uvidíte** (ukázkový výstup):

```
CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx
```

Pokud potřebujete jen surovou hodnotu atributu, přeskočte volání `resolve`. Krok řešení je užitečný, když později tyto URL předáváte do stahovače.

---

## Krok 5: Prohledávejte HTML pomocí XPath – Počítejte uzly XPath

Někdy dáváte přednost XPath—zejména když potřebujete složitější hierarchické dotazy. Ekvivalentní XPath výraz pro náš CSS selektor je:

```xpath
//a[contains(@href,'download')]
```

Spusťme ho a podívejme se, kolik uzlů získáme.

```java
// Step 5: Perform the same search using XPath
NodeList xpathNodes = document.selectNodes("//a[contains(@href,'download')]");

// Output the count
System.out.println("\nXPath found " + xpathNodes.getLength() + " nodes.");
```

Výstup by měl odpovídat počtu z CSS, což potvrzuje, že oba přístupy jsou ekvivalentní:

```
XPath found 3 nodes.
```

> **Proč oba?** Použití obou selektorů ve stejném kódu vám poskytuje flexibilitu. CSS je stručné pro jednoduché kontroly atributů, zatímco XPath vyniká, když potřebujete navigovat nahoru/dolů ve stromu nebo kombinovat více podmínek.

---

## Krok 6: Kompletní funkční příklad

Spojením všeho dohromady, zde je kompletní třída, kterou můžete zkopírovat a vložit do svého IDE a okamžitě spustit.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;

public class QueryExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the HTML document from a web page
        String url = "https://example.com";
        HTMLDocument document = new HTMLDocument(url);
        System.out.println("Document loaded from " + url);

        // 2️⃣ Search HTML with CSS – select elements with attribute
        NodeList cssMatches = document.selectElements("a[href*='download']");
        System.out.println("\nCSS found " + cssMatches.getLength() + " nodes.");

        // 3️⃣ Extract download links
        System.out.println("\n--- Extracted Download Links ---");
        for (int i = 0; i < cssMatches.getLength(); i++) {
            Element anchor = (Element) cssMatches.item(i);
            String href = anchor.getAttribute("href");
            // Resolve relative URLs (optional)
            String absolute = document.getBaseUrl().resolve(href).toString();
            System.out.println(absolute);
        }

        // 4️⃣ Search HTML with XPath – count xpath nodes
        NodeList xpathMatches = document.selectNodes("//a[contains(@href,'download')]");
        System.out.println("\nXPath found " + xpathMatches.getLength() + " nodes.");
    }
}
```

### Očekávaný výstup v konzoli (může se lišit podle stránky)

```
Document loaded from https://example.com

CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx

XPath found 3 nodes.
```

Spusťte program a okamžitě uvidíte všechny odkazy, které obsahují „download“. Změňte selektor nebo XPath řetězec podle vlastních kritérií—např. `a[href$='.pdf']` jen pro PDF, nebo `//div[@class='product']//a` pro produktové stránky.

---

## Časté úskalí a jak se jim vyhnout

| Problém | Příznak | Oprava |
|---------|---------|--------|
| **Chyby certifikátu HTTPS** | `javax.net.ssl.SSLHandshakeException` | Přidejte trust manager nebo použijte URL s platným certifikátem. Pro rychlé testování můžete zakázat validaci certifikátu, ale nikdy v produkci. |
| **Smyčky přesměrování** | Program se zasekne nebo vyhodí `Too many redirects` | Nastavte rozumný limit přesměrování (`document.setRedirectLimit(5)`) nebo URL ručně zkontrolujte. |
| **Relativní URL** | Extrahované odkazy začínají `/` místo úplné domény | Použijte `document.getBaseUrl().resolve(relative)` jak je ukázáno v příkladu. |
| **Velké stránky** | Vysoké využití paměti | Streamujte odpověď nebo použijte přetížení `HTMLDocument`, která omezují velikost DOM. |
| **Chybějící licence Aspose** | Runtime vyhodí `LicenseException` po vypršení zkušební verze | Zakupte licenci nebo pokračujte v používání zkušební verze pro nekomerční experimenty. |

---

## Další kroky a související témata

- **Stáhněte soubory** – kombinujte extrahované URL s `HttpURLConnection` v Javě nebo Apache HttpClient pro skutečné stažení zdrojů.
- **Paralelní zpracování** – použijte `CompletableFuture` pro souběžné stahování více souborů.
- **Pokročilé CSS selektory** – vyzkoušejte `a[href$='.zip']` pro soubory s příponou, nebo `div[data-id]` pro výběr prvků s vlastním atributem.
- **XPath funkce** – prozkoumejte `starts-with()`, `ends-with()` a logické operátory (`and`, `or`) pro podrobnější dotazy.
- **Sanitizace HTML** – pokud plánujete zobrazovat stažené HTML, zvažte použití knihovny jako Jsoup pro jeho vyčištění.

---

## Závěr

Právě jsme ukázali, jak **načíst HTML z URL** v Javě, poté **prohledat HTML pomocí CSS** k **výběru prvků s atributem**, **extrahovat odkazy ke stažení** a nakonec **počítat uzly XPath** pro ověření výsledku. Přístup je kompaktní, spoléhá na jedinou knihovnu a funguje jak pro jednoduché scraping úkoly, tak pro složitější analýzu DOM.

Neváhejte upravit selektory

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Načíst HTML dokumenty ze streamu s Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Načíst HTML dokumenty ze souboru v Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Zpracovat události načítání dokumentu v Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}