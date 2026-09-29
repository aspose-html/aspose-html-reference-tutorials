---
category: general
date: 2026-09-29
description: Tanulja meg, hogyan válasszon ki elemeket osztály alapján, olvassa be
  a HTML-t fájlból, és találja meg a külső hivatkozásokat Java-ban. Ez a lépésről‑lépésre
  útmutató hatékonyan bemutatja a NodeList iterálását.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: hu
lastmod: 2026-09-29
og_description: Válasszon ki elemeket osztály alapján Java-ban, olvassa be a HTML-t
  fájlból, és találja meg a külső hivatkozásokat a querySelectorAll segítségével.
  Kövesse a teljes példát a NodeList iterálásához.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Elemek kiválasztása osztály alapján Java-ban – teljes útmutató a querySelectorAll
  használatához
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
title: Hogyan válasszunk ki elemeket osztály szerint Java-ban a querySelectorAll segítségével
url: /hu/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan válasszunk ki elemeket osztály szerint Java-ban a querySelectorAll használatával

Ha Java-ban HTML-fájlt dolgozol fel, és **osztály szerint kell elemeket kiválasztani**, ez az útmutató pontosan megmutatja, hogyan kell ezt megtenni. Megtanulod, hogyan olvass HTML-t fájlból, használod a `querySelectorAll`-t külső linkek megtalálásához, és biztonságosan iterálod a kapott `NodeList`-et.

A HTML kezelése Java-ban gyakran nehézkesnek tűnik, de a modern könyvtárak egy tömör, CSS‑selector‑alapú API-t biztosítanak. Az alábbi példa **jsoup**-ot (1.17.2 verzió) használ, mivel ez megvalósítja a `querySelectorAll`‑stílusú szelektorokat, és egy `Elements` gyűjteményt ad vissza, amely úgy viselkedik, mint egy `NodeList`. Szükség esetén ugyanazt a logikát más DOM megvalósításokra is adaptálhatod.

## Előkövetelmények

* JDK 17 vagy újabb telepítve.
* Maven vagy Gradle a függőségkezeléshez.
* Alapvető ismeretek a Java stream-ekkel és a DOM modellel.

Add hozzá a jsoup-ot a projektedhez:

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

## 1. lépés: HTML beolvasása fájlból

Az első feladat a HTML dokumentum betöltése a lemezről. A `Jsoup.parse(Path, Charset)` beolvassa a fájlt, és felépít egy DOM-fát, amelyet lekérdezhetsz.

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

*Miért fontos*: A fájl egyszeri betöltése elkerüli az ismételt I/O műveleteket, miközben később elemeket iterálsz. A `Document` objektum a teljes DOM-ot tartalmazza, ami gyors szelektor lekérdezéseket tesz lehetővé.

## 2. lépés: `querySelectorAll` használata elemek osztály szerinti kiválasztásához

Most, hogy a dokumentum a memóriában van, **osztály szerint választhatod ki az elemeket** egy CSS szelektor segítségével. Az `"a.external"` szelektor olyan `<a>` tageket egyeztet, amelyek `external` osztályt tartalmaznak – pontosan ami szükséges a **külső linkek megtalálásához**.

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

*Miért fontos*: Az osztály szelektor használata kifejező és hatékony is egyben. A könyvtár a szelektort egy optimalizált bejárássá alakítja, így nem kell manuális ciklusokat írnod minden csomóponton.

## 3. lépés: NodeList (Elements) iterálása Java-ban

A `Elements` implementálja a `Iterable<Element>` interfészt, ami azt jelenti, hogy egy szokásos `for‑each` ciklust használhatsz a **NodeList Java** objektumok iterálásához. Az alábbi ciklus kiírja minden link `href` attribútumát.

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

*Miért fontos*: A közvetlen iteráció olvashatóvá teszi a kódot, és elkerüli a gyűjtemény stream-mé alakításának többletterhelését, ha csak egyszerű kimenetre van szükség.

## Teljes működő példa

A három lépés összevonásával egy önálló programot kapsz, amelyet a parancssorból futtathatsz.

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

### Várt kimenet

Tegyük fel, hogy az `input.html` tartalma a következő:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

A program futtatása a következőt írja ki:

```
External link: https://example.com
External link: https://openai.com
```

## Pro tippek és gyakori buktatók

* **A kódolás számít** – Mindig UTF‑8 (vagy a forrásnak megfelelő karakterkódolás) használatával olvasd a fájlt. A helytelen kódolás torzíthatja az attribútumértékek karaktereit.
* **Több osztály** – Ha egy elemnek több osztálya van (pl. `class="btn external"`), a `"a.external"` szelektor továbbra is egyezik, mivel a CSS osztály szelektorok a token jelenlétét ellenőrzik, nem a pontos karakterláncot.
* **Teljesítmény tipp** – Ha csak a `href` attribútumra van szükséged, kérheted közvetlenül a `doc.select("a.external[href]").eachAttr("href")` segítségével. Ez elkerüli a teljes `Element` objektumok létrehozását minden egyezéshez.
* **Null biztonság** – A `link.attr("href")` üres stringet ad vissza, ha az attribútum hiányzik, így nem kell null ellenőrzést végezni a kiírás előtt.

## Gyakran ismételt kérdések

**Q: Működik ez olyan HTML fragmentumokkal, amelyeknek nincs `<html>` gyökérelem?**  
A: Igen. A `Jsoup.parse` a bemenetet fragmentumként kezeli, és automatikusan hozzáadja a hiányzó gyökérelemeket, így a szelektorok a fragmentum body-ján is működnek.

**Q: Használhatom a `querySelectorAll`-t jsoup nélkül?**  
A: A standard Java DOM API (`org.w3c.dom`) nem tartalmaz `querySelectorAll`-t. Olyan könyvtárak, mint a **HTMLUnit** vagy a **jodd-lagarto**, hasonló metódusokat biztosítanak. Az itt bemutatott minta – betöltés, CSS-szel kiválasztás, iterálás – változatlan marad.

**Q: Mi a teendő, ha a linkeket módosítani szeretném a kiírás helyett?**  
A: Miután megkaptad az egyes `Element`-eket, meghívhatod a `link.attr("href", "newUrl")`-t, majd a dokumentumot visszaírhatod a lemezre a `Files.writeString` segítségével.

## Összegzés

Most már tudod, hogyan **válassz ki elemeket osztály szerint**, **olvasd be a HTML-t fájlból**, **találd meg a külső linkeket**, és **iteráld a NodeList-et Java-ban** a `querySelectorAll`‑stílusú szelektorok használatával. A teljes példa egy tiszta, production‑kész munkafolyamatot mutat be, amelyet beágyazhatsz nagyobb adatgyűjtő vagy átalakító csővezetékekbe.

Ezután fedezd fel a kapcsolódó témákat, mint a **dinamikus tartalom feldolgozása HTMLUnit-tal**, **módosított HTML visszaírása a lemezre**, vagy **Java stream-ek használata a link URL-ek listába gyűjtéséhez**. Mindegyik a itt bemutatott osztály‑alapú kiválasztás alaptechnikájára épül. Boldog kódolást!

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Hogyan kérdezzünk le HTML-t Java-ban – Elek kiválasztása, szűrés attribútum szerint, és szöveg lekérése](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [NodeList iterálása Java-ban – HTML beolvasása és kép src lekérése](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [HTML dokumentumok betöltése fájlból Aspose.HTML for Java-ban](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}