---
category: general
date: 2026-10-28
description: Jak odczytać HTML w Javie i wyodrębnić tekst z plików HTML. Dowiedz się,
  jak konwertować HTML na tekst przy użyciu Jsoup, obejmując techniki odczytu HTML
  z pliku oraz konwersji HTML na tekst w Javie.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: pl
lastmod: 2026-10-28
og_description: Jak odczytywać HTML w Javie i wyodrębniać tekst z plików HTML. Ten
  samouczek pokazuje kompletną metodę konwersji HTML na tekst przy użyciu Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Jak odczytać HTML i wyodrębnić tekst w Javie – szybki przewodnik
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: Jak czytać HTML i wyodrębniać tekst w Javie – przewodnik krok po kroku
url: /pl/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak czytać HTML i wyodrębniać tekst w Javie – przewodnik krok po kroku

Jeśli potrzebujesz **how to read html** z lokalnego pliku, ten przewodnik zapewnia kompletną rozwiązanie. Nauczysz się ładować dokument HTML, wyodrębniać czysty tekst oraz opcjonalnie konwertować HTML na tekst z precyzyjną kontrolą. Po zakończeniu samouczka będziesz mógł uruchomić przykładowy kod i zobaczyć wyodrębniony tekst wypisany w konsoli.

Czytanie plików HTML jest powszechnym zadaniem przy przetwarzaniu danych pobranych ze stron, generowaniu raportów lub czyszczeniu treści generowanych przez użytkowników. Poniższe kroki obejmują wszystko, czego potrzebujesz, od dodania wymaganej biblioteki po obsługę przypadków brzegowych, takich jak niepoprawny znacznik lub problemy z kodowaniem znaków.

## Czego będziesz potrzebować

- Java 17 lub nowsza (kod kompiluje się również w starszych wersjach)
- Maven lub Gradle do zarządzania zależnościami, lub ręcznie dodany plik JAR Jsoup
- Plik HTML o nazwie `input.html` umieszczony w katalogu `src/main/resources` projektu (ścieżkę można później zmienić)

## Konfiguracja biblioteki Jsoup

Jsoup to lekka, dobrze udokumentowana biblioteka, która parsuje HTML do struktury podobnej do DOM. Radzi sobie z uszkodzonym HTML‑em w sposób elegancki, co czyni ją idealną do zadań **extract text from html**.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Jeśli wolisz ręczne pobranie, umieść plik JAR na classpath i zaimportuj `org.jsoup.*` w swoim pliku źródłowym.

## Ładowanie HTML z pliku

Pierwszy programistyczny krok to odczytanie pliku do obiektu `Document`. Jsoup oferuje statyczną metodę `parse`, która przyjmuje `File` oraz nazwę zestawu znaków.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Dlaczego to ważne:** `Jsoup.parse(File, String)` odczytuje surowe bajty, dekoduje je zgodnie z podanym zestawem znaków i buduje czysty DOM. To podejście jest bezpieczniejsze niż ręczne wczytywanie pliku do łańcucha, ponieważ Jsoup normalizuje zakończenia linii i automatycznie naprawia typowe błędy znaczników.

## Wyodrębnianie czystego tekstu z HTML

Gdy masz już `Document`, pobranie widocznego tekstu wymaga jednego wywołania metody. Metoda `text()` konkatenatuje treść tekstową wszystkich elementów, pomijając tagi, skrypty i style.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

Wywołanie `body()` ogranicza wyodrębnianie do elementu `<body>`, co jest typowym celem, gdy **read html from file** w analizie treści. Wynikowy łańcuch zawiera spacje zredukowane do pojedynczych, naśladując sposób, w jaki przeglądarka renderuje tekst.

### Oczekiwany wynik

Zakładając, że `input.html` zawiera:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

Uruchomienie programu wypisuje:

```
Extracted text:
Hello World This is a demo page.
```

## Konwersja HTML na tekst z dodatkowymi opcjami

Czasami potrzebna jest większa kontrola niż oferuje `text()` — np. zachowanie podziałów linii, utrzymanie numeracji list lub pomijanie określonych tagów. `NodeTraversor` Jsoup w połączeniu z własnym `NodeVisitor` daje taką elastyczność.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Zastąp proste wywołanie `doc.body().text()` następującym kodem:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Dlaczego to działa:** Odwiedzający przegląda DOM w głębokości, dodając znak nowej linii przed każdym elementem blokowym (np. `<p>`, `<div>`, `<h1>`). Dzięki temu zachowana jest separacja akapitów, co jest przydatne, gdy **convert html to text** dla czytelności lub dalszych potoków NLP.

## Częste pułapki i najlepsze praktyki

| Problem | Dlaczego występuje | Zalecane rozwiązanie |
|---------|--------------------|----------------------|
| Zły zestaw znaków | Pliki zapisane w ISO‑8859‑1, ale parsowane jako UTF‑8 powodują zniekształcone znaki. | Wykryj zestaw znaków z meta tagu pliku (`<meta charset="...">`) lub przekaż prawidłową nazwę do `Jsoup.parse`. |
| Duże pliki | Ładowanie bardzo dużego pliku HTML do pamięci może spowodować `OutOfMemoryError`. | Strumieniuj plik przy użyciu `Jsoup.parse(File, String, String baseUri)` i przetwarzaj węzły stopniowo, lub zwiększ rozmiar sterty JVM. |
| Niechciany tekst skryptów/stylów | `text()` usuwa zawartość skryptów i stylów, ale niestandardowi odwiedzający mogą przypadkowo ją uwzględniać. | Pomiń węzły, których nazwa tagu to `script` lub `style` w metodzie `head` odwiedzającego. |
| Zachowanie białych znaków | Zbijanie spacji może utracić formatowanie potrzebne przy konwersji do markdown. | Użyj `Element.wholeText()` dla surowych węzłów tekstowych, a następnie ręcznie przetwórz białe znaki. |

Rozwiązanie tych problemów zapewnia, że twoje rozwiązanie **html to text java** działa niezawodnie na różnych danych wejściowych.

## Pełny, uruchamialny przykład

Poniżej znajduje się samodzielny program demonstrujący cały przepływ — od konfiguracji zależności po weryfikację wyniku. Skopiuj kod do pliku o nazwie `HtmlToTextDemo.java`, umieść obok niego plik `input.html` i uruchom `javac && java`, jak pokazano.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Uruchamianie programu

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

Konsola wyświetla zarówno proste wyodrębnienie, jak i szczegółowe

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Jak używać XPath w Javie – Czytaj HTML i wyodrębniaj tekst](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [Jak parsować HTML w Javie – Wyodrębniaj tekst z artykułów HTML](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Wyodrębnianie tekstu z HTML w Javie – Kompletny przewodnik krok po kroku](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}