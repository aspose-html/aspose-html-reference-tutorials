---
category: general
date: 2026-09-29
description: Dowiedz się, jak wybierać elementy po klasie, odczytywać HTML z pliku
  i znajdować zewnętrzne linki w Javie. Ten przewodnik krok po kroku opisuje efektywne
  iterowanie NodeList.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: pl
lastmod: 2026-09-29
og_description: Wybierz elementy po klasie w Javie, odczytaj HTML z pliku i znajdź
  zewnętrzne linki za pomocą querySelectorAll. Skorzystaj z pełnego przykładu, aby
  iterować po NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Wybieranie elementów po klasie w Java – kompletny przewodnik z querySelectorAll
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
title: Jak wybierać elementy po klasie w Javie przy użyciu querySelectorAll
url: /pl/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak wybierać elementy po klasie w Javie przy użyciu querySelectorAll

Jeśli potrzebujesz **wybierać elementy po klasie** podczas przetwarzania pliku HTML w Javie, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Nauczysz się czytać HTML z pliku, używać `querySelectorAll` do znajdowania linków zewnętrznych oraz bezpiecznie iterować otrzymany `NodeList`.

Praca z HTML w Javie często wydaje się ciężka, ale nowoczesne biblioteki oferują zwięzłe API oparte na selektorach CSS. Poniższy przykład używa **jsoup** (wersja 1.17.2), ponieważ implementuje selektory w stylu `querySelectorAll` i zwraca kolekcję `Elements`, która zachowuje się jak `NodeList`. Możesz dostosować tę samą logikę do innych implementacji DOM, jeśli zajdzie taka potrzeba.

## Wymagania wstępne

Zanim zaczniesz, upewnij się, że masz:

* JDK 17 lub nowszy zainstalowany.
* Maven lub Gradle do zarządzania zależnościami.
* Podstawową znajomość strumieni w Javie oraz modelu DOM.

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

## Krok 1: Odczyt HTML z pliku

Pierwszym zadaniem jest załadowanie dokumentu HTML z dysku. `Jsoup.parse(Path, Charset)` odczytuje plik i buduje drzewo DOM, które możesz przeszukiwać.

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

*Dlaczego to ważne*: Załadowanie pliku raz eliminuje wielokrotne operacje I/O podczas iteracji po elementach później. Obiekt `Document` przechowuje pełny DOM, umożliwiając szybkie zapytania selektorów.

## Krok 2: Użyj `querySelectorAll` do wybierania elementów po klasie

Teraz, gdy dokument jest w pamięci, możesz **wybierać elementy po klasie** używając selektora CSS. Selektor `"a.external"` dopasowuje znaczniki `<a>` posiadające klasę `external` — dokładnie to, czego potrzebujesz, aby **znaleźć linki zewnętrzne**.

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

*Dlaczego to ważne*: Użycie selektora klasy jest zarówno ekspresyjne, jak i wydajne. Biblioteka tłumaczy selektor na zoptymalizowane przeszukiwanie, więc nie musisz pisać ręcznych pętli po każdym węźle.

## Krok 3: Iteracja NodeList (Elements) w Javie

`Elements` implementuje `Iterable<Element>`, co oznacza, że możesz użyć standardowej pętli `for‑each` do **iteracji obiektów NodeList w Javie**. Poniższa pętla wypisuje atrybut `href` każdego linku.

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

*Dlaczego to ważne*: Bezpośrednia iteracja utrzymuje kod czytelnym i unika narzutu związanego z konwersją kolekcji na strumień, gdy potrzebujesz jedynie prostego wyjścia.

## Pełny działający przykład

Połączenie trzech kroków daje samodzielny program, który możesz uruchomić z wiersza poleceń.

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

### Oczekiwany wynik

Zakładając, że `input.html` zawiera:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Uruchomienie programu wypisuje:

```
External link: https://example.com
External link: https://openai.com
```

## Porady i typowe pułapki

* **Kodowanie ma znaczenie** – Zawsze odczytuj plik w UTF‑8 (lub w zestawie znaków odpowiadającym Twojemu źródłu). Nieprawidłowe kodowanie może uszkodzić znaki w wartościach atrybutów.
* **Wiele klas** – Jeśli element ma kilka klas (np. `class="btn external"`), selektor `"a.external"` nadal dopasowuje, ponieważ selektory klas CSS sprawdzają obecność tokenu, a nie dokładny ciąg znaków.
* **Wskazówka wydajnościowa** – Jeśli potrzebujesz tylko atrybutu `href`, możesz go pobrać bezpośrednio za pomocą `doc.select("a.external[href]").eachAttr("href")`. To unika tworzenia pełnych obiektów `Element` dla każdego dopasowania.
* **Bezpieczeństwo null** – `link.attr("href")` zwraca pusty ciąg, jeśli atrybut jest nieobecny, więc nie musisz sprawdzać null przed wypisaniem.

## Najczęściej zadawane pytania

**Q: Czy to działa z fragmentami HTML, które nie mają korzenia `<html>`?**  
A: Tak. `Jsoup.parse` traktuje wejście jako fragment i automatycznie dodaje brakujące elementy korzenia, co pozwala selektorom działać na ciele fragmentu.

**Q: Czy mogę używać `querySelectorAll` bez jsoup?**  
A: Standardowe API DOM w Javie (`org.w3c.dom`) nie zawiera `querySelectorAll`. Biblioteki takie jak **HTMLUnit** lub **jodd-lagarto** oferują podobne metody. Wzorzec przedstawiony tutaj — ładowanie, wybieranie przy pomocy CSS, iteracja — pozostaje taki sam.

**Q: Co zrobić, jeśli muszę zmodyfikować linki zamiast je tylko wypisywać?**  
A: Po uzyskaniu każdego `Element` możesz wywołać `link.attr("href", "newUrl")`, a następnie zapisać dokument z powrotem na dysk przy użyciu `Files.writeString`.

## Zakończenie

Teraz wiesz, jak **wybierać elementy po klasie**, **czytać HTML z pliku**, **znajdować linki zewnętrzne** oraz **iterować NodeList w Javie** przy użyciu selektorów w stylu `querySelectorAll`. Pełny przykład pokazuje czysty, gotowy do produkcji przepływ pracy, który możesz wbudować w większe pipeline’y do scrapowania lub transformacji.

Następnie, eksploruj powiązane tematy, takie jak **parsowanie dynamicznej treści przy użyciu HTMLUnit**, **zapisywanie zmodyfikowanego HTML z powrotem na dysk**, lub **używanie strumieni Java do zbierania URL‑ów linków do listy**. Każdy z nich opiera się na podstawowej technice wyboru opartej na klasie, przedstawionej tutaj. Szczęśliwego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak zapytać HTML w Javie – wybierać elementy, filtrować po atrybucie i pobierać tekst](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Iteracja NodeList w Javie – odczyt HTML i pobieranie src obrazu](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Ładowanie dokumentów HTML z pliku w Aspose.HTML dla Javy](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}