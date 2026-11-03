---
category: general
date: 2026-04-23
description: Dowiedz się, jak ustawić DPI przy konwersji SVG do PNG w ultra‑wysokiej
  jakości w Javie przy użyciu Aspose. Zawiera kod krok po kroku, wskazówki i obsługę
  przypadków brzegowych.
draft: false
keywords:
- how to set dpi
- convert svg to png
- svg to png java
- how to convert svg
- aspose svg to png
language: pl
og_description: Opanuj, jak ustawić DPI przy konwersji SVG do PNG przy użyciu Aspose
  HTML w Javie. Pełny kod, wyjaśnienia i wskazówki najlepszych praktyk.
og_title: Jak ustawić DPI przy konwertowaniu SVG na PNG – Poradnik Java
tags:
- Aspose
- Java
- SVG
- PNG
- Image Conversion
title: Jak ustawić DPI podczas konwertowania SVG na PNG przy użyciu Aspose – przewodnik
  Java
url: /pl/java/advanced-usage/how-to-set-dpi-when-converting-svg-to-png-with-aspose-java-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić DPI przy konwersji SVG do PNG przy użyciu Aspose – przewodnik Java

Zastanawiałeś się kiedyś **jak ustawić DPI** dla krystalicznie czystego PNG powstałego z SVG? Może tworzysz pipeline brandingowy i potrzebujesz logo w 600 dpi do druku, albo po prostu chcesz, aby obraz rastrowy wyglądał ostro na ekranach o wysokiej rozdzielczości. Dobra wiadomość: nie musisz zgadywać — Aspose HTML for Java robi to w mig.

W tym tutorialu przejdziemy krok po kroku, **jak ustawić DPI** podczas **konwersji SVG do PNG** przy użyciu biblioteki Aspose. Otrzymasz kompletny, gotowy do uruchomienia przykład kodu, wyjaśnienie każdej opcji konfiguracyjnej oraz kilka praktycznych wskazówek dla rzeczywistych projektów. Nie potrzebujesz żadnych zewnętrznych odnośników — wszystko, czego potrzebujesz, znajduje się tutaj.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- Java 17 (lub nowszy JDK) zainstalowany.
- Maven lub Gradle do zarządzania zależnościami (pokażemy fragment Maven).
- Plik SVG, który chcesz rasteryzować (np. `logo.svg`).
- Podstawową znajomość składni Javy — nic skomplikowanego, po prostu zwykłe `public static void main`.

Jeśli czegoś brakuje, pobierz to najpierw; dalsza część przewodnika zakłada, że wszystko jest już gotowe.

## Zależność Maven

Dodaj zależność Aspose HTML for Java do swojego pliku `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Użytkownicy Gradle mogą zamienić ten fragment na równoważną linię `implementation "com.aspose:aspose-html:23.12"`.

## Krok 1: Utwórz obiekt opcji konwersji

Pierwszą rzeczą, którą musisz zrobić, jest zainicjowanie `SvgConversionOptions`. Ten obiekt przechowuje wszystkie ustawienia, które możesz chcieć — DPI, kolor tła, skalowanie itp.

```java
// Step 1: Build conversion options for SVG → PNG
SvgConversionOptions conversionOptions = new SvgConversionOptions();
```

Dlaczego to ważne: bez jawnego ustawienia DPI, Aspose domyślnie używa 96 dpi, co jest w porządku dla sieci, ale daleko od gotowości do druku. Tworząc obiekt opcji, zyskujesz pełną kontrolę nad procesem rasteryzacji.

## Krok 2: Ustaw żądane DPI

Teraz odpowiadamy na kluczowe pytanie: **jak ustawić DPI**. Metoda `setDpi(int)` przyjmuje zwykłą liczbę całkowitą; typowe wartości wahają się od 72 dpi (niskiej rozdzielczości) do 1200 dpi (ultra‑wysokiej rozdzielczości). Dla większości zadań drukarskich 300 dpi to złoty środek; dla logo, które musi być skalowane, 600 dpi jest bezpiecznym wyborem.

```java
// Step 2: Define the resolution (DPI) – 600 DPI for ultra‑high‑quality output
conversionOptions.setDpi(600);
```

> **Pro tip:** Wartości DPI, które nie są wielokrotnościami 72, mogą czasami generować niecałkowite wymiary pikseli. Jeśli potrzebujesz dokładnego rozmiaru w pikselach, najpierw oblicz `pixel = cale * DPI`, a następnie dostosuj atrybut `viewBox` w SVG.

## Krok 3: Obsługa przezroczystości za pomocą koloru tła

Pliki SVG często zawierają przezroczyste obszary. PNG obsługuje przezroczystość, ale jeśli kierujesz się do workflow drukarskiego, który oczekuje nieprzezroczystego tła, warto je zamienić. Metoda `setBackgroundColor(String)` przyjmuje dowolny ciąg znaków zgodny z CSS.

```java
// Step 3: Replace transparent areas with white (or any color you prefer)
conversionOptions.setBackgroundColor("white");
```

Możesz także użyć `#FFFFFF`, `rgb(255,255,255)` lub nawet `transparent`, jeśli *chcesz* zachować kanał alfa.

## Krok 4: Wykonaj konwersję

Po skonfigurowaniu opcji, właściwa konwersja to pojedyncze wywołanie statyczne `Converter.convert`. Podaj ścieżkę wejściowego SVG, żądaną ścieżkę wyjściowego PNG oraz obiekt opcji.

```java
// Step 4: Convert the SVG file to a PNG using the configured options
Converter.convert(
        "YOUR_DIRECTORY/logo.svg",   // Input SVG
        "YOUR_DIRECTORY/logo.png",   // Output PNG
        conversionOptions);          // Options we just set
```

To wszystko — Aspose zajmuje się parsowaniem SVG, stosowaniem skalowania DPI, wypełnianiem tła i zapisem pliku PNG na dysku.

## Pełny, uruchamialny przykład

Poniżej znajduje się kompletny kod klasy Java, którą możesz skopiować i wkleić do pliku o nazwie `SvgToPngHighRes.java`. Zastąp `YOUR_DIRECTORY` rzeczywistą ścieżką na swoim komputerze.

```java
import com.aspose.html.converters.SvgConversionOptions;
import com.aspose.html.converters.Converter;

/**
 * Demonstrates how to set DPI when converting an SVG file to a high‑resolution PNG
 * using Aspose.HTML for Java.
 *
 * Prerequisites:
 *   - Aspose.HTML for Java library (Maven dependency shown earlier)
 *   - Java 17+ runtime
 *
 * Expected result:
 *   - logo.png created at 600 DPI with a white background.
 */
public class SvgToPngHighRes {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create conversion options for SVG → PNG
        SvgConversionOptions conversionOptions = new SvgConversionOptions();

        // 2️⃣ Set the desired resolution (DPI) – 600 DPI yields ultra‑high‑quality output
        conversionOptions.setDpi(600);

        // 3️⃣ Define a background color to replace any transparency (white works for most prints)
        conversionOptions.setBackgroundColor("white");

        // 4️⃣ Convert the SVG file to a PNG using the configured options
        Converter.convert(
                "YOUR_DIRECTORY/logo.svg",   // <-- change this to your source file
                "YOUR_DIRECTORY/logo.png",   // <-- change this to your target file
                conversionOptions);

        System.out.println("Conversion complete! Check YOUR_DIRECTORY/logo.png");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu wygeneruje `logo.png` w tym samym folderze. Otwórz plik w przeglądarce obrazów i sprawdź **właściwości obrazu** — powinieneś zobaczyć:

- **Rozdzielczość:** 600 dpi (lub wartość, którą ustawiłeś)
- **Wymiary:** Skalowane zgodnie z oryginalnym `viewBox` SVG pomnożonym przez czynnik DPI
- **Tło:** Jednolite białe (brak przezroczystych pikseli)

Jeśli otworzysz PNG w programie takim jak Photoshop, metadane DPI będą widoczne w *Obraz → Rozmiar obrazu*.

## Typowe przypadki brzegowe i jak sobie z nimi radzić

| Sytuacja | Na co zwrócić uwagę | Zalecane rozwiązanie |
|-----------|-------------------|----------------------|
| **Brak pliku SVG** | `FileNotFoundException` wyrzucany przez `Converter.convert` | Zweryfikuj ścieżkę przed konwersją przy użyciu `Files.exists(Paths.get(...))`. |
| **Nieobsługiwane funkcje SVG** (np. filtry niezaimplementowane) | Aspose może po cichu pominąć te elementy | Użyj `SvgConversionOptions.setEnableSvgFilters(true)`, jeśli potrzebujesz obsługi filtrów (dostępne w nowszych wersjach). |
| **Bardzo wysokie DPI (≥1200)** | Plik wyjściowy może stać się ogromny (setki MB) | Rozważ strumieniowanie wyniku lub obniżenie DPI dla dużych obrazów. |
| **Zachowanie przezroczystości** | Ustawiłeś kolor tła, ale tak naprawdę chcesz alfa | Pomiń `setBackgroundColor` lub przekaż `"transparent"`, aby zachować oryginalny kanał alfa. |
| **Konwersja wsadowa** | Ponowne tworzenie `SvgConversionOptions` dla każdego pliku jest nieefektywne | Utwórz jedną instancję `SvgConversionOptions` i używaj jej w pętli. |

## Najczęściej zadawane pytania

**P: Czy to działa z innymi formatami rastrowymi, takimi jak JPEG lub BMP?**  
O: Tak. Zastąp rozszerzenie pliku wyjściowego (`.png`) na `.jpg` lub `.bmp`, a Aspose automatycznie wybierze odpowiedni enkoder. Możesz także dopasować jakość JPEG za pomocą `JpegConversionOptions`.

**P: Czy mogę konwertować SVG przechowywane w tablicy bajtów zamiast w pliku?**  
O: Oczywiście. Skorzystaj z przeciążeń `Converter.convert(InputStream, OutputStream, conversionOptions)`, które działają na strumieniach — przydatne w usługach webowych.

**P: Czy ustawienie DPI jest tym samym co skalowanie obrazu?**  
O: DPI to znacznik metadanych, który mówi drukarkom, ile pikseli przypada na cal. Wewnątrz Aspose skaluje obraz rastrowy, aby dopasować go do DPI, więc wizualny rozmiar zmienia się, jeśli oglądasz PNG w 100 % zoom w przeglądarce respektującej DPI.

## Pro Tipy dla kodu gotowego do produkcji

1. **Cache'uj opcje** – Jeśli konwertujesz dziesiątki logo z tym samym DPI i tłem, utwórz `SvgConversionOptions` raz i używaj go wielokrotnie. Redukuje to narzut tworzenia obiektów.
2. **Waliduj wymiary wejściowe** – Dla bardzo dużych SVG oblicz oczekiwany rozmiar w pikselach (`width * DPI/96`) i przerwij, jeśli przekracza bezpieczny próg (np. 20 000 px), aby uniknąć `OutOfMemoryError`.
3. **Loguj metadane konwersji** – Zapisz DPI, nazwę pliku źródłowego i znacznik czasu w pliku logu; ułatwi to późniejsze debugowanie.
4. **Bezpieczeństwo wątkowe** – `Converter.convert` jest thread‑safe, więc możesz równolegle przetwarzać partie przy użyciu `ExecutorService`.

## Podsumowanie wizualne

![przykład ustawiania dpi](image.png){: .align-center alt="przykład ustawiania dpi"}

Diagram powyżej ilustruje przepływ: **SVG → ustaw DPI i tło → PNG**.

## Zakończenie

Teraz wiesz **jak ustawić DPI** przy **konwersji SVG do PNG** przy użyciu Aspose HTML for Java. Konfigurując `SvgConversionOptions`, kontrolujesz rozdzielczość, obsługę tła i wiele innych aspektów, zamieniając prosty plik wektorowy w gotowy do druku obraz rastrowy w zaledwie kilku linijkach kodu.

Zrób kolejny krok i wypróbuj:

- Konwersję całego folderu SVG w pętli wsadowej.
- Zmianę formatu wyjściowego na JPEG dla zasobów zoptymalizowanych pod sieć.
- Inne opcje konwersji Aspose, takie jak `setScaleX/Y` dla niestandardowego skalowania poza DPI.

Miłego kodowania i niech Twoje PNG będą zawsze tak ostre, jak tego potrzebujesz!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}