---
category: general
date: 2026-06-16
description: Jak używać CSS do ładowania pliku HTML i liczenia linków w Javie. Naucz
  się liczyć elementy HTML i oceniać XPath w Javie w jednym, przejrzystym przykładzie.
draft: false
keywords:
- how to use css
- load html file
- how to count links
- count html elements
- evaluate xpath java
language: pl
og_description: Jak używać CSS w Javie do wczytywania pliku HTML, liczenia linków
  i oceny wyrażeń XPath — wszystko w jednym praktycznym przewodniku.
og_title: Jak używać CSS w Javie – Ładowanie HTML, liczenie linków i ocena XPath
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
title: Jak używać CSS w Javie – wczytywanie HTML, liczenie linków i ocena XPath
url: /pl/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać CSS w Javie – Ładowanie HTML, zliczanie linków i ocena XPath

Zastanawiałeś się kiedyś **jak używać selektorów CSS** podczas przetwarzania pliku HTML w Javie? Być może tworzysz web‑crawler, scraper lub po prostu potrzebujesz audytować statyczną stronę. Dobra wiadomość? Nie musisz pisać własnego parsera od podstaw — nowoczesne biblioteki pozwalają łączyć selektory CSS4 z wyrażeniami XPath 3.1 w jednym, schludnym przepływie pracy.

W tym samouczku przeprowadzimy Cię przez **sposób ładowania pliku HTML**, zastosowanie selektora CSS do zliczenia linków w pasku nawigacji oraz **ewaluację XPath** w celu policzenia konkretnych elementów obrazu. Po zakończeniu będziesz mieć kompletny, uruchamialny program, który wypisze liczbę pasujących węzłów, oraz zrozumiesz, dlaczego każdy element ma znaczenie.

## Wymagania wstępne

- Java 17 (lub dowolny nowszy JDK) zainstalowany na Twoim komputerze  
- Maven lub Gradle do zarządzania zależnościami (w przykładzie użyjemy Maven)  
- Mały fragment HTML zapisany jako `input.html` w folderze, którym zarządzasz  

Żadne inne narzędzia nie są wymagane — wystarczy edytor tekstu i terminal.

## Co obejmuje samouczek

- **Ładowanie pliku HTML** do struktury podobnej do DOM przy użyciu klasy *HTMLDocument*  
- Zastosowanie **selektora CSS4** (`nav a[data-role]`) do odnalezienia linków nawigacyjnych  
- Uruchomienie **wyrażenia XPath 3.1** w celu znalezienia tagów `<img>`, których `src` kończy się na `.png` i które dodatkowo posiadają atrybut `alt`  
- **Zliczanie** wyników obu zapytań i wypisywanie ich na konsolę  
- Pełny kod źródłowy, wyjaśnienia „dlaczego” oraz szybki przegląd możliwych przypadków brzegowych  

Zaczynajmy.

---

## Krok 1 – Jak załadować plik HTML przy użyciu HTMLDocument

Zanim będziesz mógł cokolwiek zapytać, dokument HTML musi zostać sparsowany do modelu, po którym można się poruszać. Klasa `HTMLDocument` z biblioteki **jsoup‑plus** (lub dowolnego podobnego parsera obsługującego HTML) robi dokładnie to.

```java
import com.example.html.HTMLDocument;
import com.example.html.NodeList;

public class CssXPathDemo {
    public static void main(String[] args) throws Exception {
        // Load the HTML document from the file system
        HTMLDocument doc = new HTMLDocument("YOUR_DIRECTORY/input.html");
        // From here on we can query the DOM using CSS or XPath
```

*Dlaczego to jest ważne:*  
Załadowanie pliku raz i utrzymanie referencji (`doc`) unika powtarzających się operacji I/O, co może stać się wąskim gardłem wydajności przy przetwarzaniu dużych partii stron.

---

## Krok 2 – Jak używać CSS do zliczania linków wewnątrz `<nav>`

Teraz, gdy dokument jest w pamięci, możemy użyć selektora CSS4, aby pobrać każdy element `<a>` znajdujący się wewnątrz `<nav>` i jednocześnie posiadający atrybut `data‑role`. Jest to powszechny wzorzec dla menu nawigacyjnych, które używają atrybutów danych jako punktów zaczepienia dla JavaScript.

```java
        // Use a CSS4 selector to find every <a> inside a <nav> that has a data‑role attribute
        NodeList navLinks = doc.querySelectorAll("nav a[data-role]");
```

*Wyjaśnienie:*  
- `nav a[data-role]` oznacza „dowolny element `<a>` z atrybutem `data‑role`, będący potomkiem elementu `<nav>`”.  
- Selektor jest kompatybilny z **CSS4**, co oznacza, że możesz także używać pseudo‑klas takich jak `:not()` czy `:has()`, jeśli Twoje zastosowanie się rozrośnie.

> **Wskazówka:** Jeśli potrzebujesz tylko bezpośrednich potomków, zamień spację na `>` (`nav > a[data-role]`). To zmniejsza obszar wyszukiwania i może przyspieszyć przetwarzanie dużych dokumentów.

---

## Krok 3 – Ewaluacja XPath w Javie w celu zliczenia konkretnych elementów `<img>`

XPath błyszczy, gdy potrzebujesz filtrowania opartego na atrybutach, które nie jest tak proste w CSS. Tutaj znajdziemy każdy `<img>`, którego `src` kończy się na `.png` **i** który dodatkowo definiuje atrybut `alt` — przydatne przy audytach dostępności.

```java
        // Use an XPath 3.1 expression to locate all <img> elements whose src ends with .png and have an alt attribute
        NodeList pngImages = doc.evaluate("//img[ends-with(@src, '.png') and @alt]");
```

*Dlaczego XPath?*  
- Funkcja `ends-with()` jest częścią XPath 3.1, umożliwiając dopasowanie przyrostka bez użycia wyrażeń regularnych.  
- Łączenie wielu predykatów (`and @alt`) zapewnia, że zliczasz tylko obrazy, które są zarówno poprawnie źródłowane, jak i opisane.

Jeśli Twoja biblioteka obsługuje tylko XPath 1.0, będziesz musiał użyć `contains(@src, '.png')` i następnie filtrować w Javie — mniej precyzyjne podejście.

---

## Krok 4 – Jak zliczyć elementy HTML i wypisać wyniki

Na koniec pobieramy długości obu obiektów `NodeList` i wypisujemy je. To jest część **jak zliczyć linki** w układance, ale działa dla dowolnej kolekcji węzłów.

```java
        // Output the number of matches for each query
        System.out.println("Nav links: " + navLinks.getLength());
        System.out.println("PNG images with alt: " + pngImages.getLength());
    }
}
```

**Oczekiwany output konsoli** (zakładając, że przykładowy HTML zawiera 3 pasujące linki i 2 pasujące obrazy):

```
Nav links: 3
PNG images with alt: 2
```

Jeśli liczniki wynoszą zero, sprawdź ponownie składnię selektora lub zweryfikuj, czy `input.html` rzeczywiście zawiera oczekiwane elementy.

---

## Pełny działający przykład

Poniżej znajduje się kompletny, samodzielny program, który możesz skopiować i wkleić do pliku o nazwie `CssXPathDemo.java`. Zawiera niezbędne importy, prosty fragment `pom.xml` dla Maven oraz minimalny przykład HTML do testów.

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

**Fragment `pom.xml` dla Maven** (dodaj tę zależność, aby pobrać parser HTML obsługujący zarówno CSS4, jak i XPath 3.1):

```xml
<dependencies>
    <dependency>
        <groupId>com.example</groupId>
        <artifactId>html-parser-plus</artifactId>
        <version>2.3.1</version>
    </dependency>
</dependencies>
```

**Przykładowy `input.html`** (umieść go w tym samym katalogu co plik Java):

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

Uruchomienie `mvn compile exec:java -Dexec.mainClass=CssXPathDemo` zwróci oczekiwane liczniki pokazane wcześniej.

---

## Przypadki brzegowe i częste pytania

### Co zrobić, gdy plik HTML jest niepoprawny?

Zarówno silniki CSS, jak i XPath tolerują drobne błędy w znacznikach (brakujące zamykające tagi, niecudzysłowione atrybuty). Jednak poważne zniekształcenia mogą spowodować przerwanie parsowania. W produkcji otocz krok ładowania blokiem try‑catch i zaloguj wyjątek.

### Czy mogę połączyć CSS i XPath w jednym wyrażeniu?

Nie bezpośrednio; każdy silnik ma własną składnię. Typowy wzorzec polega na użyciu tego, który najnaturalniej wyraża warunek (CSS do zapytań strukturalnych, XPath do funkcji atrybutów) i ewentualnym połączeniu wyników w Javie.

### Jak zliczyć elementy w wielu plikach?

Po prostu umieść logikę ładowania wewnątrz pętli:

```java
for (Path p : Files.newDirectoryStream(Paths.get("html_folder"), "*.html")) {
    HTMLDocument doc = new HTMLDocument(p.toString());
    // repeat the queries...
}
```

### Czy to działa z Java 8?

Tak — pod warunkiem użycia wersji biblioteki skierowanej na Java 8 lub wyższą. Pokazany kod nie korzysta z nowszych funkcji języka.

---

## Podsumowanie

Zademonstrowaliśmy **jak używać selektorów CSS** wraz z wyrażeniami **evaluate xpath java**, aby **załadować plik HTML**, **zliczyć linki** i **zliczyć elementy HTML**, które spełniają określone kryteria. Najważniejsze wnioski to:

- Załaduj dokument raz przy użyciu `HTMLDocument`.  
- Wykorzystaj CSS4 do prostych zapytań strukturalnych (`nav a[data-role]`).  
- Wykorzystaj XPath 3.1 do potężnych funkcji atrybutów (`ends-with(@src, '.png')`).  
- Pobierz długość `NodeList`, aby uzyskać dokładne liczby.  

Od tego momentu możesz rozbudować skrypt: dodać więcej selektorów, zapisać wyniki do CSV lub zintegrować go z większym pipeline'em crawlingowym. Połączenie CSS i XPath daje elastyczność potrzebną do rozwiązania praktycznie każdego wyzwania związanego ze scrapowaniem HTML.

Gotowy do eksperymentów? Spróbuj zamienić selektor CSS na `section article[data-id]` lub zmień XPath, aby celować w tagi `<video>` z określonym kodekiem. Nie ma ograniczeń.

Jeśli ten przewodnik okazał się pomocny, podziel się nim, dodaj gwiazdkę do repozytorium lub zostaw komentarz ze swoimi przypadkami użycia. Szczęśliwego kodowania!

![how to use css example diagram](https://example.com/diagram.png "how to use css example")

---


## Co warto nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}