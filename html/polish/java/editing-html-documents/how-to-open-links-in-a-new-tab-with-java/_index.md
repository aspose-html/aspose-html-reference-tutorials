---
category: general
date: 2026-10-28
description: Dowiedz się, jak otwierać linki w nowej karcie, parsując HTML w Javie,
  znajdując linki zewnętrzne i dodając atrybut target="_blank".
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: pl
lastmod: 2026-10-28
og_description: 'Otwórz linki w nowej karcie przy użyciu Javy: parsuj HTML, znajdź
  linki zewnętrzne, dodaj target="_blank" i zapisz zmodyfikowany HTML.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Otwieranie linków w nowej karcie w Javie – przewodnik krok po kroku
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
title: Jak otworzyć linki w nowej karcie w Javie
url: /pl/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak otworzyć linki w nowej karcie przy użyciu Javy

Jeśli potrzebujesz **otworzyć linki w nowej karcie** z pliku HTML statycznego, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Nauczysz się **parsować HTML w Javie**, **znajdować linki zewnętrzne**, **dodawać target blank** oraz **zapisywać zmodyfikowany HTML** bez wychodzenia z IDE.

Otwieranie linków zewnętrznych w nowej karcie przeglądarki poprawia doświadczenie użytkownika i utrzymuje go na pierwotnej stronie. Poniższe rozwiązanie działa z każdym dokumentem HTML, wymaga jedynie popularnej biblioteki jsoup i działa na Javie 8 lub nowszej.

## Wymagania wstępne

Zanim rozpoczniesz, upewnij się, że masz:

* Zainstalowany JDK 8 +  
* Narzędzie budujące (Maven lub Gradle), aby pobrać zależność **jsoup**  
* Plik HTML zawierający znaczniki `<a>` z klasą `external`

Nie potrzebujesz serwera WWW ani dodatkowych frameworków — jsoup obsługuje wszystko lokalnie.

## Krok 1: Dodaj jsoup do projektu

Dodaj jsoup jako zależność. Jeśli używasz Maven, umieść to w `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Dla Gradle, dodaj następującą linię do `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Te współrzędne pobierają najnowszą stabilną wersję (stan na październik 2026). Po synchronizacji możesz importować klasy z `org.jsoup` w swoich plikach źródłowych Javy.

## Krok 2: Parsowanie dokumentu HTML

Parsowanie pliku to pierwszy krok w kierunku **open links new tab**. Metoda `Jsoup.parse` wczytuje plik do modyfikowalnej struktury podobnej do DOM‑u.

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

*Dlaczego to ważne*: `Document` udostępnia selektory w stylu CSS, co sprawia, że łatwo znaleźć potrzebne elementy.

## Krok 3: Znajdź linki zewnętrzne

Teraz zlokalizuj każdy element `<a>` posiadający klasę `external`. To spełnia wymaganie **find external links**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` to kolekcja pasujących węzłów. Jeśli selektor zwróci pusty zestaw, Twój HTML może nie zawierać tej klasy lub używać innej konwencji nazewnictwa — dostosuj selektor odpowiednio.

## Krok 4: Dodaj `target="_blank"` do każdego linku

Dla każdego węzła zwróconego przez **find external links**, ustaw atrybut `target` na `_blank`. To realizuje krok **add target blank** i zapewnia, że przeglądarki otworzą link w nowej karcie.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

Metoda `attr` nadpisuje istniejącą wartość `target`, gwarantując spójne zachowanie we wszystkich zewnętrznych odnośnikach.

## Krok 5: Zapisz zmodyfikowany HTML

Po zaktualizowaniu DOM, zapisz zmiany z powrotem do pliku. To kończy część **save modified html** tutorialu.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` serializuje cały dokument, zachowując wcięcia i formatowanie tak, jak jsoup pierwotnie je sparsował.

## Pełny działający przykład

Połączenie wszystkich kroków daje samodzielny program, który możesz skopiować, wkleić i uruchomić.

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

### Oczekiwany wynik

Załóżmy, że `sample.html` zawiera:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Po uruchomieniu programu, `updated.html` będzie zawierał:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Tylko link zewnętrzny otrzymał atrybut `target="_blank"`, co oznacza, że przeglądarki otworzą go teraz w nowej karcie.

## Pro tipy i typowe pułapki

* **Pro tip:** Jeśli chcesz traktować linki zaczynające się od `http://` lub `https://` jako zewnętrzne, nawet bez klasy CSS, rozszerz selektor: `doc.select("a[href^=http]")`.
* **Edge case:** Niektóre strony już określają `target="_self"`; wywołanie `attr` nadpisuje je, zapewniając spójne zachowanie.
* **Wydajność:** Dla bardzo dużych plików HTML rozważ parsowanie strumieniowe (`Jsoup.parse(File, String, String, Parser.htmlParser())`), aby zmniejszyć zużycie pamięci.
* **Testowanie:** Zweryfikuj wynik, otwierając `updated.html` w przeglądarce i sprawdzając link w narzędziach deweloperskich — szukaj atrybutu `target`.

## Podsumowanie

Masz teraz kompletną, gotową do uruchomienia metodę **open links in a new tab** przy użyciu Javy. Tutorial pokazał, jak **parse html in java**, **find external links**, **add target blank** oraz **save modified html**, wszystko przy użyciu lekkiej biblioteki jsoup.

Od tego momentu możesz:

* Rozszerzyć selektor, aby obsługiwał inne wzorce linków (np. `rel="external"`).  
* Połączyć tę logikę z krokiem budowania, który przetwarza wszystkie pliki HTML w projekcie.  
* Zintegrować kod z większym potokiem zarządzania treścią.

Śmiało eksperymentuj z różnymi selektorami lub formatami wyjściowymi i podziel się wynikami ze społecznością!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy blisko powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne przykłady kodu oraz wyjaśnienia krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}