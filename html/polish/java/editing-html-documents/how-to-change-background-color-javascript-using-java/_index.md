---
category: general
date: 2026-09-29
description: Zmieniaj kolor tła w JavaScript w pliku HTML przy użyciu Javy. Dowiedz
  się, jak wczytać HTML w Javie, uruchomić JS w HTML oraz modyfikować HTML przy pomocy
  Javy, aby uzyskać nowy kolor tła strony.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: pl
lastmod: 2026-09-29
og_description: Zmieniaj kolor tła w JavaScript na stronie HTML przy użyciu Javy.
  Ten poradnik pokazuje, jak załadować HTML w Javie, uruchomić JavaScript w HTML oraz
  programowo ustawić tło strony.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Zmienianie koloru tła w JavaScript przy pomocy Javy – przewodnik krok po
  kroku
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: Jak zmienić kolor tła w JavaScript przy użyciu Javy
url: /pl/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak zmienić kolor tła javascript używając Javy

Jeśli potrzebujesz **change background color javascript** w istniejącym pliku HTML, możesz to zrobić w pełni z poziomu Javy, bez otwierania przeglądarki. Ten tutorial pokazuje, jak **load html in java**, wykonać mały fragment JavaScript oraz **modify html with java**, aby tło strony zostało zaktualizowane.  

Rozwiązanie działa z otwarto‑źródłową biblioteką **HTMLUnit**, która zapewnia przeglądarkę headless zdolną do oceny JavaScript dokładnie tak, jak prawdziwa przeglądarka. Po zakończeniu tego przewodnika będziesz mieć wielokrotnego użytku metodę, która **sets page background** na dowolny wybrany kolor.

## Wymagania wstępne

| Co potrzebujesz | Dlaczego to ważne |
|-----------------|-------------------|
| Java 8 lub nowsza | HTMLUnit wymaga co najmniej Java 8. |
| Narzędzie budowania Maven lub Gradle | Aby automatycznie pobrać zależność HTMLUnit. |
| Plik HTML, który chcesz edytować (np. `input.html`) | Dokument źródłowy, który zostanie załadowany i zmodyfikowany. |

Dodaj HTMLUnit do swojego projektu:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Wskazówka:** Użyj najnowszej stabilnej wersji HTMLUnit, aby uzyskać najdokładniejszy silnik JavaScript.

## Zmiana koloru tła javascript – ładowanie HTML w Javie

Pierwszym krokiem jest załadowanie dokumentu HTML do obiektu `HTMLPage`. Daje to API podobne do DOM oraz kontekst wykonania JavaScript.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Dlaczego to ważne*: `WebClient` tworzy środowisko piaskownicy, w którym może działać JavaScript, więc możesz **run js in html** dokładnie tak, jak przeglądarka użytkownika.

## Uruchom js w html, aby ustawić tło strony

Gdy strona jest załadowana, możesz ocenić dowolne wyrażenie JavaScript. Poniższy fragment zmienia styl `backgroundColor` elementu `<body>`.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*Wyjaśnienie*:  
- `document.body.style.backgroundColor` jest standardową właściwością DOM określającą tło strony.  
- Wywołując `eval`, **run js in html** bez potrzeby rzeczywistego okna przeglądarki.  
- Metoda jest wielokrotnego użytku dla dowolnego koloru, spełniając wymaganie **set page background**.

## Modyfikuj html przy użyciu Javy i zapisz wynik

Po wykonaniu skryptu DOM odzwierciedla nowy styl. Teraz możesz zapisać zaktualizowany HTML z powrotem na dysk.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

Połączenie wszystkiego razem daje pojedynczy, uruchamialny program:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### Oczekiwany wynik

Uruchomienie programu wypisuje:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

Otworzenie `js_modified.html` w dowolnej przeglądarce wyświetla stronę z jasnoniebieskim tłem, potwierdzając, że operacja **change background color javascript** zakończyła się sukcesem.

## Typowe warianty i przypadki brzegowe

| Sytuacja | Jak sobie radzić |
|----------|------------------|
| **Różne formaty kolorów** | Przekaż dowolną wartość zgodną z CSS (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Brak tagu `<body>`** | Skrypt zakończy się cichym niepowodzeniem; możesz najpierw upewnić się, że `<body>` istnieje, używając `page.getFirstByXPath("//body")`. |
| **Duże pliki HTML** | Wyłącz CSS (`setCssEnabled(false)`) i włącz tylko potrzebne funkcje JavaScript, aby zmniejszyć zużycie pamięci. |
| **Uruchamianie wielu skryptów** | Wywołuj `changeBackground` wielokrotnie lub utwórz metodę pomocniczą przyjmującą listę poleceń JavaScript. |

## Zakończenie

Teraz wiesz, jak **change background color javascript** poprzez załadowanie pliku HTML w Javie, **run js in html**, oraz **modify html with java**, aby **set page background** na dowolny wybrany kolor. Pełny przykład powyżej działa z najnowszą biblioteką HTMLUnit i może być zintegrowany z większymi pipeline'ami automatyzacji, takimi jak przetwarzanie wsadowe raportów HTML czy przygotowywanie szablonów e‑mail.

**Kolejne kroki**  
- Poznaj inne manipulacje DOM (np. wstawianie elementów, usuwanie skryptów).  
- Połącz to podejście z renderowaniem PDF, aby generować PDF‑y stylizowanych stron.  
- Spróbuj użyć innego silnika headless, takiego jak Selenium WebDriver, jeśli potrzebna jest pełna wierność przeglądarki.

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletny działający kod z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Pobierz obliczony styl Java – wyodrębnij kolor tła z HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [Jak załadować HTML, ustawić DPI urządzenia i odczytać kolor tła](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Generuj HTML z JavaScript w Javie – kompletny przewodnik krok po kroku](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}