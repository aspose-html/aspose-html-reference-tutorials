---
category: general
date: 2026-07-02
description: Wczytaj HTML z adresu URL przy użyciu Aspose.HTML dla Javy, następnie
  wybierz elementy z atrybutem, wyodrębnij linki do pobrania i policz węzły XPath
  w kilku prostych krokach.
draft: false
keywords:
- load html from url
- select elements with attribute
- extract download links
- search html with css
- count xpath nodes
language: pl
og_description: Wczytaj HTML z URL w Javie, a następnie użyj selektorów CSS i XPath,
  aby wybrać elementy z atrybutem, wyodrębnić linki do pobrania i policzyć węzły XPath.
og_title: Wczytaj HTML z URL w Javie – Pełny poradnik CSS i XPath
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
title: Ładowanie HTML z adresu URL w Javie – Kompletny przewodnik z CSS i XPath
url: /pl/java/creating-managing-html-documents/load-html-from-url-in-java-complete-guide-with-css-xpath/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ładowanie HTML z URL w Javie – Kompletny przewodnik z CSS i XPath

Kiedykolwiek potrzebowałeś **załadować HTML z URL** w aplikacji Java i wyciągnąć konkretne linki bez pisania pełnoprawnego web‑crawlera? Nie jesteś sam. Niezależnie od tego, czy tworzysz menedżer pobierania, agregator treści, czy po prostu jesteś ciekawy odwiedzanych stron, możliwość pobrania strony, **przeszukiwania HTML przy użyciu CSS**, a następnie **liczenia węzłów XPath** jest przydatną umiejętnością.

W tym samouczku przeprowadzimy Cię przez cały proces: od pobrania zdalnej strony do pamięci, po użycie selektora CSS do **wybierania elementów z atrybutem**, wyodrębnienie tych **linków do pobrania**, a na końcu weryfikację tego samego wyniku przy użyciu zapytania XPath. Bez zewnętrznych usług, tylko czysta Java i biblioteka Aspose.HTML for Java.

> **Prerequisites** – Będziesz potrzebował zainstalowanego Java 8+, Maven lub Gradle do zarządzania zależnościami oraz podstawowej znajomości HTML i składni Javy. Jeśli jesteś nowy w Aspose.HTML, nie martw się; omówimy konfigurację krok po kroku.

---

## Co zbudujesz

Po zakończeniu tego przewodnika będziesz mieć uruchamialną klasę Java, która:

1. **Ładuje HTML z URL** (np. `https://example.com`).
2. **Przeszukuje DOM przy użyciu selektora CSS**, aby znaleźć każdy znacznik `<a>`, którego `href` zawiera „download”.
3. **Wyodrębnia i wypisuje każdy link do pobrania**.
4. **Wykonuje równoważne zapytanie XPath** i wypisuje, ile węzłów zostało znalezionych.

Zobaczysz także mały diagram wizualizujący przepływ — na wypadek, gdybyś był wzrokowcem.

![Diagram przedstawiający przepływ ładowania HTML z URL, wybierania elementów, wyodrębniania linków i liczenia węzłów XPath](load-html-from-url-diagram.png)

---

## Krok 1: Dodaj Aspose.HTML for Java do swojego projektu

Na początek. Aspose.HTML jest biblioteką komercyjną, ale oferuje darmową wersję próbną, która doskonale sprawdza się w celach edukacyjnych.

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

> **Wskazówka:** Jeśli później napotkasz `NoClassDefFoundError`, sprawdź ponownie, czy plik JAR `aspose-html` znajduje się na ścieżce klas w czasie wykonywania.

---

## Krok 2: Ładuj HTML z URL i zainicjalizuj dokument

Teraz, gdy biblioteka jest już dostępna, możemy faktycznie **załadować HTML z URL**. Klasa `HTMLDocument` przyjmuje ciąg znaków URL i zajmuje się żądaniem HTTP, przekierowaniami oraz wykrywaniem zestawu znaków.

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

**Dlaczego to działa:** `HTMLDocument` wewnętrznie tworzy `HttpWebRequest`, podąża za przekierowaniami i buduje drzewo DOM, które zachowuje się tak jak `document` przeglądarki. Oznacza to, że możemy od razu używać zarówno selektorów CSS, jak i XPath.

---

## Krok 3: Przeszukaj HTML przy użyciu CSS – Wybierz elementy z atrybutem

Najbardziej czytelny sposób na zlokalizowanie elementów to użycie selektora CSS. W naszym przypadku chcemy każdy `<a>`, którego atrybut `href` zawiera słowo „download”. Składnia selektora `a[href*='download']` robi dokładnie to.

```java
// Step 3: Find all anchor elements whose href contains "download"
NodeList downloadLinks = document.selectElements("a[href*='download']");

// Quick sanity check – how many did we find?
System.out.println("CSS found " + downloadLinks.getLength() + " nodes.");
```

### Co oznacza selektor

| Część | Znaczenie |
|------|-----------|
| `a` | dowolny element `<a>` |
| `[href*='download']` | atrybut `href`, który **zawiera** podciąg `download` (`*=` jest operatorem „zawiera”) |

> **Przypadek brzegowy:** Jeśli strona używa względnych URL (np. `href="/files/download.zip"`), Aspose.HTML zachowa je w takiej formie. Możesz później potrzebować rozwiązać je względem bazowego URL.

---

## Krok 4: Wyodrębnij linki do pobrania

Teraz, gdy mamy `NodeList`, wyciągnięcie rzeczywistych URL-i jest trywialne. Rzutujemy każdy węzeł na `Element` i odczytujemy jego atrybut `href`.

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

**Wynik, który zobaczysz** (przykładowe wyjście):

```
CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx
```

Jeśli potrzebujesz tylko surowej wartości atrybutu, pomiń wywołanie `resolve`. Krok rozwiązywania jest przydatny, gdy później podajesz te URL-e do pobieracza.

---

## Krok 5: Przeszukaj HTML przy użyciu XPath – Policz węzły XPath

Czasami wolisz XPath — szczególnie gdy potrzebujesz bardziej złożonych zapytań hierarchicznych. Równoważne wyrażenie XPath dla naszego selektora CSS to:

```xpath
//a[contains(@href,'download')]
```

Uruchommy je i zobaczmy, ile węzłów otrzymamy.

```java
// Step 5: Perform the same search using XPath
NodeList xpathNodes = document.selectNodes("//a[contains(@href,'download')]");

// Output the count
System.out.println("\nXPath found " + xpathNodes.getLength() + " nodes.");
```

Wynik powinien odpowiadać liczbie z CSS, potwierdzając, że oba podejścia są równoważne:

```
XPath found 3 nodes.
```

> **Dlaczego oba?** Używanie obu selektorów w tym samym kodzie daje elastyczność. CSS jest zwięzły przy prostych sprawdzaniach atrybutów, podczas gdy XPath błyszczy, gdy trzeba nawigować w górę/dół drzewa lub łączyć wiele warunków.

---

## Krok 6: Pełny działający przykład

Łącząc wszystko razem, oto pełna klasa, którą możesz skopiować i wkleić do swojego IDE oraz uruchomić od razu.

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

### Oczekiwany wynik w konsoli (może się różnić w zależności od witryny)

```
Document loaded from https://example.com

CSS found 3 nodes.

--- Extracted Download Links ---
https://example.com/files/report-download.pdf
https://example.com/downloads/setup.exe
https://cdn.example.com/assets/manual-download.docx

XPath found 3 nodes.
```

Uruchom program, a natychmiast zobaczysz wszystkie linki zawierające „download”. Zmień selektor lub ciąg XPath, aby dopasować własne kryteria — np. `a[href$='.pdf']` dla samych PDF‑ów, lub `//div[@class='product']//a` dla stron produktów.

---

## Częste pułapki i jak ich unikać

| Problem | Objaw | Rozwiązanie |
|---------|-------|-------------|
| **Błędy certyfikatu HTTPS** | `javax.net.ssl.SSLHandshakeException` | Dodaj menedżera zaufania lub użyj URL z ważnym certyfikatem. Do szybkiego testowania możesz wyłączyć weryfikację certyfikatu, ale nigdy w produkcji. |
| **Pętle przekierowań** | Program się zawiesza lub zgłasza `Too many redirects` | Ustaw rozsądny limit przekierowań (`document.setRedirectLimit(5)`) lub ręcznie sprawdź docelowy URL. |
| **Względne URL‑e** | Wyodrębnione linki zaczynają się od `/` zamiast pełnej domeny | Użyj `document.getBaseUrl().resolve(relative)` jak pokazano w przykładzie. |
| **Duże strony** | Wysokie zużycie pamięci | Strumieniuj odpowiedź lub użyj przeciążeń `HTMLDocument`, które ograniczają rozmiar DOM. |
| **Brak licencji Aspose** | W czasie wykonywania zgłasza `LicenseException` po wygaśnięciu wersji próbnej | Kup licencję lub kontynuuj używanie wersji próbnej do eksperymentów niekomercyjnych. |

---

## Kolejne kroki i powiązane tematy

- **Pobierz pliki** – połącz wyodrębnione URL‑e z `HttpURLConnection` Javy lub Apache HttpClient, aby rzeczywiście pobrać zasoby.
- **Przetwarzanie równoległe** – użyj `CompletableFuture`, aby pobierać wiele plików jednocześnie.
- **Zaawansowane selektory CSS** – wypróbuj `a[href$='.zip']` dla rozszerzeń plików lub `div[data-id]` aby wybrać elementy z niestandardowymi atrybutami.
- **Funkcje XPath** – poznaj `starts-with()`, `ends-with()` oraz operatory logiczne (`and`, `or`) dla bardziej szczegółowych zapytań.
- **Sanityzacja HTML** – jeśli planujesz wyświetlać pobrany HTML, rozważ użycie biblioteki takiej jak Jsoup do jego czyszczenia.

---

## Podsumowanie

Właśnie pokazaliśmy, jak **załadować HTML z URL** w Javie, następnie **przeszukać HTML przy użyciu CSS**, aby **wybrać elementy z atrybutem**, **wyodrębnić linki do pobrania**, a na końcu **policzyć węzły XPath**, aby zweryfikować wynik. Podejście jest zwięzłe, opiera się na jednej bibliotece i działa zarówno dla prostych zadań scrapowania, jak i bardziej zaawansowanej analizy DOM.  

Śmiało modyfikuj selektory

## Co powinieneś nauczyć się dalej?

Poniższe samouczki obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Ładowanie dokumentów HTML ze strumienia przy użyciu Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-stream/)
- [Ładowanie dokumentów HTML z pliku w Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Obsługa zdarzeń ładowania dokumentu w Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/handle-document-load-events/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}