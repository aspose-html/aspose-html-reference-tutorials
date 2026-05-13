---
category: general
date: 2026-03-14
description: Dowiedz się, jak ustawić współczynnik pikseli urządzenia w Javie i zapisać
  stronę internetową jako PNG przy użyciu Aspose.HTML – kompletny przewodnik konwersji
  HTML do PNG.
draft: false
keywords:
- set device pixel ratio
- save webpage as png
- how to render png
- html to png conversion
- java html to image
language: pl
og_description: Dowiedz się, jak ustawić współczynnik pikseli urządzenia w Javie i
  zapisać stronę internetową jako PNG przy użyciu Aspose.HTML, krok po kroku omawiając
  konwersję HTML do PNG.
og_title: Ustaw współczynnik pikseli urządzenia w Javie – renderowanie HTML do PNG
tags:
- java
- aspose-html
- image-rendering
title: Ustaw współczynnik pikseli urządzenia w Javie – renderuj HTML do PNG
url: /pl/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-render-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device pixel ratio w Java – Render HTML to PNG

Czy kiedykolwiek potrzebowałeś **set device pixel ratio** podczas generowania zrzutu ekranu strony internetowej w Javie? Być może tworzysz usługę podglądu dla urządzeń mobilnych lub po prostu chcesz uzyskać wyraźną miniaturkę, która wygląda dobrze na ekranie Retina. Niezależnie od tego, jesteś we właściwym miejscu. W tym samouczku przeprowadzimy Cię przez cały proces **html to png conversion**, a zobaczysz dokładnie, jak **save webpage as png** przy użyciu biblioteki Aspose.HTML.

Omówimy wszystko, od konfigurowania sandboxu, który naśladuje widok iPhone'a, po załadowanie zdalnej strony HTML i w końcu zapisanie wyniku na dysku. Po zakończeniu będziesz wiedział, **how to render png** pliki programowo i będziesz miał wielokrotnego użytku fragment kodu, który możesz wstawić do dowolnego projektu Java, który potrzebuje możliwości **java html to image**.

## Czego będziesz potrzebował

- **Java Development Kit (JDK) 8 lub nowszy** – biblioteka działa z dowolnym aktualnym JDK.
- **Aspose.HTML for Java** – możesz pobrać najnowszy JAR z repozytorium Maven Aspose lub pobrać zip z oficjalnej strony.
- Środowisko **IDE** (IntelliJ IDEA, Eclipse lub nawet VS Code) – cokolwiek pozwala kompilować i uruchamiać Javę.
- Połączenie internetowe, jeśli planujesz ładować żywy URL (przykład używa `https://example.com/mobile.html`).

To wszystko. Nie są wymagane dodatkowe narzędzia budowania ani natywne pliki binarne.

## Krok 1: Skonfiguruj Sandbox i set device pixel ratio

Pierwszą rzeczą, którą musisz zrobić, jest stworzenie **Sandbox**, który udaje urządzenie mobilne. To tutaj faktycznie **set device pixel ratio** aby dopasować się do ekranu o wysokiej gęstości (na przykład 2× retina wyświetlacz iPhone'a).

```java
import com.aspose.html.rendering.SandboxOptions;

// Create sandbox options
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixel width of iPhone 6/7/8
sandboxOptions.setScreenHeight(667);         // CSS pixel height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
sandboxOptions.setUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
    "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

// Build the sandbox
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

**Dlaczego to ważne:** `devicePixelRatio` informuje silnik renderujący, ile fizycznych pikseli odpowiada jednemu pikselowi CSS. Bez ustawienia tego, wygenerowany obraz będzie wyglądał rozmycie na ekranach wysokiej rozdzielczości. Poprzez jawne zdefiniowanie, zapewniasz, że wygenerowany PNG ma odpowiednią ilość szczegółów.

> **Pro tip:** Jeśli celujesz w urządzenia z Androidem, możesz użyć `3.0` dla urządzeń z 3× skalowaniem. Dostosuj odpowiednio szerokość/wysokość.

## Krok 2: Załaduj stronę HTML do konwersji html to png

Teraz, gdy sandbox jest gotowy, możemy załadować stronę, którą chcemy przechwycić. Klasa `HTMLDocument` z Aspose.HTML przyjmuje URL oraz instancję sandboxu, więc strona renderuje się dokładnie tak, jak na symulowanym urządzeniu.

```java
import com.aspose.html.HTMLDocument;

// Load the remote page inside the sandbox
HTMLDocument document = new HTMLDocument(
    "https://example.com/mobile.html", // Replace with your own URL
    mobileSandbox);
```

**Co dzieje się pod maską?** Biblioteka pobiera HTML, parsuje CSS, uruchamia dowolny JavaScript (jeśli włączony) i układa stronę używając wymiarów viewportu zdefiniowanych wcześniej. Ten krok jest rdzeniem konwersji **java html to image**, ponieważ dostarcza w pełni wyrenderowany DOM gotowy do rasteryzacji.

> **Edge case:** Jeśli strona zależy od zewnętrznych czcionek, upewnij się, że są dostępne z maszyny uruchamiającej kod. W przeciwnym razie tekst może przejść na domyślną czcionkę, zmieniając wynik wizualny.

## Krok 3: Zapisz stronę jako PNG – how to render png z Aspose.HTML

Po wyrenderowaniu dokumentu, ostatnim elementem jest faktyczne zapisanie pliku PNG na dysku. Klasa `PngSaveOptions` pozwala dostosować poziom kompresji i inne ustawienia specyficzne dla PNG, ale domyślne wartości działają doskonale w większości scenariuszy.

```java
import com.aspose.html.saving.PngSaveOptions;

// Define PNG options (optional)
PngSaveOptions pngOptions = new PngSaveOptions();
// You could adjust pngOptions.setCompressionLevel(9); for maximum compression

// Save the rendered page as a PNG image
document.save("output/mobile_view.png", pngOptions);

System.out.println("Mobile view rendered and saved as PNG.");
```

Gdy uruchomisz program, w folderze `output` pojawi się plik `mobile_view.png`. Otwórz go, a zobaczysz dokładny zrzut zdalnej strony, wyrenderowany w wysokiej rozdzielczości, którą określiłeś przy użyciu **set device pixel ratio**.

### Szybka weryfikacja

```text
$ java -jar MobileRenderTutorial.jar
Mobile view rendered and saved as PNG.
$ ls output
mobile_view.png
```

Otwórz obraz w dowolnym przeglądarce; tekst powinien być ostry, ikony wyraźne, a układ identyczny z tym, co zobaczysz na prawdziwym iPhone.

## Opcjonalnie: Dostosowywanie potoku renderowania

### Dynamiczna zmiana DPI

Jeśli potrzebujesz generować obrazy dla wielu gęstości ekranu, opakuj tworzenie sandboxu w metodę:

```java
private static Sandbox createSandbox(double dpr) {
    SandboxOptions opts = new SandboxOptions();
    opts.setScreenWidth(375);
    opts.setScreenHeight(667);
    opts.setDevicePixelRatio(dpr); // Pass 1.0, 2.0, 3.0, etc.
    opts.setUserAgent("...");
    return new Sandbox(opts);
}
```

Następnie wywołaj `createSandbox(3.0)` dla urządzenia 3×. Ta elastyczność jest przydatna, gdy budujesz usługę zwracającą miniatury dla iPhone, iPad i tabletów z Androidem jednocześnie.

### Renderowanie bez JavaScript

Jeśli przechwytywana strona zawiera ciężkie skrypty, których nie potrzebujesz, możesz wyłączyć JavaScript dla szybszej **html to png conversion**:

```java
sandboxOptions.setJavaScriptEnabled(false);
```

Wyłączenie skryptów może skrócić czas renderowania o połowę, ale pamiętaj, że niektóre dynamiczne treści mogą zniknąć.

## Typowe pułapki i jak ich uniknąć

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Rozmyty wynik** | `devicePixelRatio` pozostawiony domyślnie (1.0) | Jawnie **set device pixel ratio** na 2.0 lub wyższą wartość |
| **Brakujące czcionki** | Zdalne czcionki zablokowane przez firewall | Upewnij się, że maszyna ma dostęp do internetu lub osadź czcionki lokalnie |
| **Błędy braku pamięci** | Renderowanie bardzo dużych stron przy wysokim DPI | Ogranicz rozmiar viewportu lub zmniejsz `devicePixelRatio` |
| **Nieprawidłowy URL** | Używanie ścieżki względnej bez bazowego URL | Podaj pełny, absolutny URL lub ustaw `document.setBaseUrl()` |

Rozwiązanie tych problemów na wczesnym etapie oszczędza Ci frustrujące sesje debugowania później.

## Pełny działający przykład

Poniżej znajduje się kompletny, gotowy do uruchomienia program w Javie. Skopiuj i wklej go do pliku o nazwie `MobileRenderTutorial.java`, dodaj JAR Aspose.HTML do classpath i uruchom.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.SandboxOptions;
import com.aspose.html.saving.PngSaveOptions;

public class MobileRenderTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that mimics a mobile device viewport
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixel width
        sandboxOptions.setScreenHeight(667);         // CSS pixel height
        sandboxOptions.setDevicePixelRatio(2.0);     // High‑density screen (set device pixel ratio)
        sandboxOptions.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // Step 2: Load the HTML page inside the sandbox
        HTMLDocument document = new HTMLDocument(
            "https://example.com/mobile.html", // Replace with your own URL
            mobileSandbox);

        // Step 3: Render the page to a PNG image
        PngSaveOptions pngOptions = new PngSaveOptions();
        document.save("output/mobile_view.png", pngOptions);

        System.out.println("Mobile view rendered.");
    }
}
```

> **Result:** Program tworzy `output/mobile_view.png`, wysokiej rozdzielczości zrzut ekranu, który respektuje **set device pixel ratio**, które zdefiniowałeś.

## Wizualne potwierdzenie

<img src="output/mobile_view.png" alt="przykładowy zrzut ekranu set device pixel ratio" width="400"/>

Powyższy obraz (placeholder) pokazuje końcowy PNG po procesie renderowania. Zauważ wyraźny tekst i prawidłowo skalowane elementy UI — dokładnie to, czego oczekujesz przy prawidłowym **set device pixel ratio**.

## Zakończenie

Masz teraz solidne pojęcie o tym, jak **set device pixel ratio** w Javie, wykonać **html to png conversion** oraz **save webpage as png** przy użyciu Aspose.HTML. To obejmuje niezbędny przepływ pracy „how to render png” i daje Ci wielokrotnego użytku wzorzec dla dowolnego zadania **java html to image**, które możesz napotkać.

Gotowy na kolejny krok? Spróbuj zamienić URL na dynamiczną stronę, eksperymentuj z różnymi wartościami `devicePixelRatio` lub zintegrować ten fragment kodu z endpointem Spring Boot, który zwraca PNG na żądanie. Nie ma granic, a mając solidne podstawy, rozszerzenie tego rozwiązania będzie bułką z masłem.

Miłego kodowania i śmiało zostaw komentarz

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}