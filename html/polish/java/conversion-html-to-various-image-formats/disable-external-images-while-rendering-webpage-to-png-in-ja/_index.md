---
category: general
date: 2026-05-31
description: Wyłącz zewnętrzne obrazy podczas renderowania strony internetowej do
  formatu PNG w Javie przy użyciu Aspose HTML. Dowiedz się, jak bezpiecznie załadować
  stronę w piaskownicy i zapisać dokument HTML jako PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: pl
og_description: Wyłącz zewnętrzne obrazy podczas renderowania strony internetowej
  do formatu PNG w Javie. Ten przewodnik krok po kroku pokazuje, jak załadować stronę
  w piaskownicy i zapisać dokument HTML jako PNG.
og_title: Wyłącz zewnętrzne obrazy podczas renderowania strony internetowej do PNG
  w Javie
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Wyłącz zewnętrzne obrazy podczas renderowania strony internetowej do PNG w
  Javie
url: /pl/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wyłączanie zewnętrznych obrazów podczas renderowania strony internetowej do PNG w Javie

Kiedykolwiek potrzebowałeś **wyłączyć zewnętrzne obrazy** przy renderowaniu strony internetowej do PNG w Javie? Być może tworzysz usługę miniatur, która musi pozostać odizolowana od publicznego internetu, albo po prostu chcesz mieć pewność, że żadne obrazy osób trzecich nie wyciekną podczas konwersji. Tak czy inaczej, trafiłeś we właściwe miejsce.

W tym samouczku przejdziemy przez ładowanie strony w piaskownicy, wyłączanie pobierania zewnętrznych obrazów oraz zapisanie dokumentu HTML jako pliku PNG — wszystko przy użyciu Aspose.HTML dla Javy. Po zakończeniu będziesz mieć gotowy przykład oraz kilka praktycznych wskazówek, jak uniknąć typowych pułapek.

## Czego się nauczysz

- **Jak renderować HTML do obrazu w Javie** przy użyciu `Converter` z Aspose.HTML.  
- Dokładne kroki, aby **załadować stronę w piaskownicy** z własnym viewportem i DPI.  
- Konfigurację potrzebną do **wyłączenia zewnętrznych obrazów** przy jednoczesnym renderowaniu strony.  
- Jak **zapisać dokument HTML jako PNG** (lub w innym obsługiwanym formacie) na dysku.  
- Obsługę przypadków brzegowych, wskazówki wydajnościowe i porady rozwiązywania problemów.

### Wymagania wstępne

- Java 8 lub nowsza (kod działa także z JDK 11+).  
- Maven lub Gradle do pobrania biblioteki Aspose.HTML dla Javy.  
- Podstawowa znajomość składni Javy i obsługi wyjątków.  
- Połączenie internetowe do początkowego załadowania strony (chyba że serwujesz HTML lokalnie).

> **Pro tip:** Jeśli pracujesz za korporacyjnym proxy, ustaw właściwości JVM `http.proxyHost` i `http.proxyPort` przed uruchomieniem przykładu.

---

## Krok 1: Skonfiguruj projekt i dodaj Aspose.HTML

Na początek — dodaj zależność Aspose.HTML. Jeśli używasz Maven, wstaw to do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Dla Gradle, odpowiednik wygląda tak:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Gdy biblioteka znajdzie się na classpath, możesz przystąpić do kodowania.

---

## Krok 2: **Wyłącz zewnętrzne obrazy** przy użyciu środowiska piaskownicy

Serce rozwiązania tkwi w `DocumentSandbox`. Przekazując `false` dla flagi *allowExternalImages*, instruujemy Aspose.HTML, aby ignorował wszystkie znaczniki `<img>` wskazujące na URL‑e spoza piaskownicy. To właśnie mechanizm **wyłączający zewnętrzne obrazy**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Dlaczego to ważne:** Bez piaskownicy renderer próbowałby pobrać każdy obraz odwołany przez stronę, co może być wolne, zawodliwe lub nawet stanowić zagrożenie bezpieczeństwa. Ustawienie flagi na `false` zapewnia czysty, samodzielny przebieg renderowania.

---

## Krok 3: **Załaduj stronę w piaskownicy**  

Teraz wskazujemy Aspose.HTML na URL, który chcemy przechwycić. Konstruktor `HTMLDocument` przyjmuje instancję piaskownicy, automatycznie stosując zdefiniowane ograniczenia.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Jeśli strona mocno polega na zewnętrznych skryptach do układu, możesz zauważyć brak niektórych elementów, ponieważ wyłączyliśmy także skrypty. W takim wypadku przełącz flagę `allowExternalScripts` na `true`, pozostawiając `allowExternalImages` ustawione na `false`.

---

## Krok 4: **Renderuj stronę do PNG**  

Po załadowaniu dokumentu konwersja do obrazu to jednowierszowy kod przy użyciu `Converter.convert`. Obiekt `ImageSaveOptions` pozwala wybrać format wyjściowy; tutaj wybieramy PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Powstały plik, `sandboxed.png`, zawiera migawkę strony **bez żadnych zewnętrznych obrazów** — pozostają jedynie wbudowane SVG‑y lub grafiki zakodowane w base64, jeśli takie istnieją.

---

## Krok 5: Zweryfikuj wynik i debuguj typowe problemy

Po uruchomieniu programu otwórz `sandboxed.png` w dowolnym przeglądarce obrazów. Powinieneś zobaczyć układ strony, tekst i style CSS, ale wszystkie elementy `<img src="http://…">` będą puste (często wyświetlane jako biały prostokąt lub całkowicie pominięte).

### Typowe problemy i ich rozwiązania

| Objaw | Prawdopodobna przyczyna | Rozwiązanie |
|---|---|---|
| Pusta strona | Docelowy URL zablokował żądanie (np. Cloudflare) | Dodaj odpowiednie nagłówki do user‑agenta piaskownicy lub użyj proxy. |
| Brak czcionek | Pliki czcionek są hostowane zewnętrznie | Zainstaluj czcionki lokalnie lub osadź je jako `@font-face` z data URI. |
| Przesunięcie układu | Odwołania CSS do zewnętrznych arkuszy stylów zostały zablokowane | Ustaw `allowExternalScripts` na `true` *tylko* dla ładowania CSS, potem uruchom ponownie. |
| `java.lang.OutOfMemoryError` | Renderowanie bardzo dużej strony przy wysokim DPI | Zmniejsz rozmiar viewportu lub DPI, albo zwiększ pamięć JVM (`-Xmx2g`). |

---

## Krok 6: Rozszerzenie przykładu – zapis w innych formatach

Ten sam kod działa dla JPEG, BMP, a nawet PDF. Wystarczy zmienić wartość enumu `SaveFormat`:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Jeśli potrzebujesz PDF, zamień `ImageSaveOptions` na `PdfSaveOptions` i dostosuj rozszerzenie pliku.

---

## Pełny działający przykład (gotowy do kopiowania)

Poniżej znajduje się **kompletny, gotowy do uruchomienia program**. Utwórz nową klasę Javy, wklej kod, upewnij się, że katalog `output` istnieje, i uruchom go.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Oczekiwany wynik** (konsola):

```
PNG image saved to: output/sandboxed.png
```

Otwórz `sandboxed.png` — zobaczysz stronę wyrenderowaną **bez żadnych zewnętrznych obrazów**.

---

## Najczęściej zadawane pytania

**P: Czy nadal mogę wyświetlać obrazy osadzone w samym HTML?**  
O: Tak. Wbudowane URI typu `data:` lub obrazy zakodowane w base64 są traktowane jako część dokumentu i pojawią się w PNG.

**P: Co zrobić, jeśli chcę zachować niektóre zewnętrzne obrazy, a inne zablokować?**  
O: Piaskownica działa jako przełącznik „wszystko albo nic”. Aby uzyskać drobniejszą kontrolę, samodzielnie pobierz dozwolone obrazy, osadź je jako data URI, a następnie renderuj.

**P: Czy to rozwiązanie działa na serwerach bez interfejsu graficznego?**  
O: Absolutnie. Aspose.HTML to czysto‑Java biblioteka; nie wymaga serwera wyświetlania ani silnika przeglądarki.

**P: Jak to się różni od użycia Selenium lub Puppeteer?**  
O: Selenium steruje prawdziwą przeglądarką, co jest ciężkie i trudniejsze do sandboxowania. Aspose.HTML renderuje HTML bezpośrednio w pamięci, co daje deterministyczną wydajność i prostsze kontrole bezpieczeństwa, takie jak **wyłączanie zewnętrznych obrazów**.

---

## Zakończenie

Masz teraz solidny, kompletny przepis na **wyłączanie zewnętrznych obrazów przy renderowaniu strony internetowej do PNG w Javie**. Dzięki `DocumentSandbox` zyskujesz ścisłą kontrolę nad dozwolonymi zasobami zewnętrznymi, zapewniając zarówno bezpieczeństwo, jak i powtarzalność. Od tego momentu możesz eksperymentować z różnymi rozmiarami viewportu, ustawieniami DPI czy formatami wyjściowymi — każdy parametr otwiera nowe możliwości generowania miniatur, podglądów czy archiwalnych zrzutów.

Gotowy na kolejny krok? Spróbuj renderować zestaw URL‑i równolegle lub wbuduj tę logikę w mikrousługę Spring Boot, która zwraca PNG na żądanie. Nie ma granic, gdy połączysz elastyczność Aspose.HTML z możliwościami współbieżności Javy.

Miłego kodowania i nie zapomnij podzielić się swoimi sukcesami w komentarzach!

## Co powinieneś nauczyć się dalej?

- [Jak używać Aspose do renderowania HTML do PNG – przewodnik krok po kroku](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Jak renderować HTML do PNG z Aspose – kompletny przewodnik](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [Jak edytować CSS – zaawansowana edycja zewnętrznego CSS z Aspose.HTML dla Javy](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}