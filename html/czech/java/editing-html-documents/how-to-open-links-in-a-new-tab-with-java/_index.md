---
category: general
date: 2026-10-28
description: Naučte se otevírat odkazy v novém panelu parsováním HTML v Javě, vyhledáváním
  externích odkazů a přidáním atributu target="_blank".
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: cs
lastmod: 2026-10-28
og_description: 'Otevřít odkazy v novém panelu pomocí Javy: parsovat HTML, najít externí
  odkazy, přidat target=''_blank'' a uložit upravené HTML.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Otevřete odkazy v novém panelu pomocí Javy – krok za krokem průvodce
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
title: Jak otevřít odkazy v nové kartě pomocí Javy
url: /cs/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak otevřít odkazy v novém panelu v Javě

Pokud potřebujete **otevřít odkazy v novém panelu** ze statického HTML souboru, tento návod vám přesně ukáže, jak na to. Naučíte se **parsovat HTML v Javě**, **najít externí odkazy**, **přidat target blank** a **uložit upravené HTML** aniž byste opustili své IDE.

Otevírání externích odkazů v novém panelu prohlížeče zlepšuje uživatelský zážitek a udržuje návštěvníky na původní stránce. Níže uvedené řešení funguje s libovolným HTML dokumentem, vyžaduje pouze populární knihovnu jsoup a běží na Java 8 nebo novější.

## Požadavky

* JDK 8 + nainstalováno  
* Nástroj pro sestavování (Maven nebo Gradle) pro stažení **jsoup** závislosti  
* HTML soubor, který obsahuje značky `<a>` s třídou `external`

Webový server ani další frameworky nejsou potřeba — jsoup vše zvládne lokálně.

## Krok 1: Nastavte jsoup ve svém projektu

Přidejte jsoup jako závislost. Pokud používáte Maven, vložte následující do souboru `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Pro Gradle přidejte tento řádek do souboru `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Tyto souřadnice stáhnou nejnovější stabilní verzi (k říjnu 2026). Po synchronizaci můžete importovat třídy z `org.jsoup` ve svých Java souborech.

## Krok 2: Parsujte HTML dokument

Parsování souboru je první krok k **otevření odkazů v novém panelu**. Metoda `Jsoup.parse` načte soubor do mutovatelné struktury podobné DOM.

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

*Proč je to důležité*: `Document` vám poskytuje CSS‑stylové selektory, což usnadňuje nalezení požadovaných elementů.

## Krok 3: Najděte externí odkazy

Nyní vyhledejte každý element `<a>`, který má třídu `external`. To splňuje požadavek **najít externí odkazy**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` je kolekce odpovídajících uzlů. Pokud selektor vrátí prázdnou sadu, váš HTML buď neobsahuje tuto třídu, nebo používá jinou konvenci — upravit selektor podle potřeby.

## Krok 4: Přidejte `target="_blank"` ke každému odkazu

Pro každý uzel vrácený **najít externí odkazy** nastavte atribut `target` na `_blank`. Tím splníte krok **přidat target blank** a zajistíte, že prohlížeč otevře odkaz v novém panelu.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

Metoda `attr` přepíše jakoukoli existující hodnotu `target`, což garantuje konzistentní chování u všech externích odkazů.

## Krok 5: Uložte upravené HTML

Po aktualizaci DOM zapište změny zpět do souboru. Tím dokončíte část **uložit upravené html** tutoriálu.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` serializuje celý dokument, zachovává odsazení a formátování tak, jak jej jsoup původně načetl.

## Kompletní funkční příklad

Spojením všech kroků získáte samostatný program, který můžete zkopírovat, vložit a spustit.

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

### Očekávaný výstup

Předpokládejme, že `sample.html` obsahuje:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Po spuštění programu bude `updated.html` obsahovat:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Pouze externí odkaz získal atribut `target="_blank"`, což znamená, že prohlížeče jej nyní otevřou v novém panelu.

## Profesionální tipy a běžné úskalí

* **Pro tip:** Pokud chcete považovat odkazy začínající na `http://` nebo `https://` za externí i bez CSS třídy, rozšiřte selektor: `doc.select("a[href^=http]")`.
* **Edge case:** Některé stránky již specifikují `target="_self"`; volání `attr` jej přepíše a zajistí jednotné chování.
* **Performance:** U velmi velkých HTML souborů zvažte streamovací parsování (`Jsoup.parse(File, String, String, Parser.htmlParser())`) pro snížení paměťové náročnosti.
* **Testing:** Ověřte výsledek otevřením `updated.html` v prohlížeči a kontrolou odkazu pomocí vývojářských nástrojů — hledejte atribut `target`.

## Závěr

Nyní máte kompletní, spustitelné řešení pro **otevření odkazů v novém panelu** pomocí Javy. Tutoriál pokrýval, jak **parsovat html v java**, **najít externí odkazy**, **přidat target blank** a **uložit upravené html**, vše s lehkou knihovnou jsoup.

Odtud můžete:

* Rozšířit selektor tak, aby zachytával i jiné vzory odkazů (např. `rel="external"`).  
* Propojit tuto logiku s krokem sestavení, který zpracuje všechny HTML soubory v projektu.  
* Integrovat kód do většího pipeline pro správu obsahu.

Neváhejte experimentovat s různými selektory nebo výstupními formáty a sdílet své výsledky s komunitou!

## Co byste se měli naučit dál?

Následující tutoriály se věnují úzce souvisejícím tématům, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak používat CSS v Javě – načíst HTML, spočítat odkazy a vyhodnotit XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [Jak parsovat HTML v Javě – extrahovat text z HTML článků](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Vytvořit nový HTML prvek v Javě – kompletní průvodce Aspose.HTML](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}