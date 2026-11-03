---
category: general
date: 2026-02-14
description: Dowiedz się, jak kompresować plik PDF podczas konwertowania HTML na PDF
  w Javie przy użyciu Aspose HTML. Zawiera ustawienie niestandardowego ekranu oraz
  pełny przykład kodu.
draft: false
keywords:
- how to compress pdf
- convert html to pdf
- html to pdf java
- aspose html pdf
- set custom screen
language: pl
og_description: Jak kompresować PDF podczas konwertowania HTML na PDF w Javie przy
  użyciu Aspose HTML. Pełny, krok po kroku, poradnik z niestandardowymi ustawieniami
  ekranu.
og_title: Jak skompresować PDF przy użyciu Aspose HTML to PDF – przewodnik Java
tags:
- Aspose
- Java
- PDF conversion
title: Jak skompresować PDF przy użyciu Aspose HTML to PDF – przewodnik Java
url: /pl/java/conversion-html-to-other-formats/how-to-compress-pdf-with-aspose-html-to-pdf-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak skompresować PDF przy użyciu Aspose HTML to PDF – przewodnik Java

Zastanawiałeś się kiedyś **jak skompresować pdf** w locie przy konwertowaniu stron HTML na PDF-y? Nie jesteś jedyny. Wielu programistów napotyka problem, gdy ich PDF-y rosną w rozmiarze po konwersji, szczególnie na stronach mobile‑first, gdzie liczy się przepustowość. Dobra wiadomość? Dzięki Aspose.HTML for Java możesz zmniejszyć te PDF‑y — i możesz także nakazać konwerterowi renderowanie strony tak, jakby była wyświetlana na urządzeniu o niestandardowych wymiarach.

W tym tutorialu przeprowadzimy Cię przez kompletny, działający przykład, który pokaże dokładnie **jak skompresować pdf** w wyniku, jak **konwertować html do pdf** w Javie oraz jak **ustawić niestandardowy ekran** tak, aby układ odpowiadał telefonowi 375×667 px. Po zakończeniu będziesz mieć jedną klasę, którą możesz wstawić do dowolnego projektu Maven lub Gradle i od razu zacząć generować odchudzone PDF‑y.

## Czego będziesz potrzebować

- **Java 17** (lub dowolny aktualny JDK; Aspose.HTML obsługuje Java 8+)
- **Aspose.HTML for Java** – możesz pobrać ją z Maven Central (`com.aspose:aspose-html:23.12` w momencie pisania)
- Prosty plik HTML (`input.html`), który chcesz przekonwertować na PDF
- IDE lub edytor tekstu; nie wymaga specjalnego frameworka

> **Wskazówka:** Jeśli używasz Maven, dodaj zależność w następujący sposób:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Teraz, gdy wymagania wstępne są załatwione, przejdźmy do rzeczywistych kroków.

## Krok 1: Utwórz sandbox i ustaw niestandardowy ekran

Pierwszą rzeczą, którą zazwyczaj robisz przy konwertowaniu HTML, jest określenie **jak strona ma być renderowana**. Aspose.HTML pozwala symulować dowolne urządzenie poprzez skonfigurowanie `Sandbox` z `Screen`. W naszym przypadku będziemy naśladować typowy ekran smartfona (375 px szerokości, 667 px wysokości, 96 dpi, skala 1.0).

```java
// Step 1 – create a sandbox that pretends we’re on a phone screen
Sandbox renderingSandbox = new Sandbox();
renderingSandbox.setScreen(new Screen(375, 667, 96, 1.0));
```

Po co używać sandboxu? Bez niego konwerter domyślnie używa widoku podobnego do pulpitu, co może powodować przesunięcia układu i niepotrzebnie duże strony PDF. Poprzez **ustawienie niestandardowego ekranu** zapewniasz, że PDF odpowiada projektowi mobilnemu i często zmniejsza liczbę stron — pośredni sposób na utrzymanie małego rozmiaru pliku.

## Krok 2: Skonfiguruj opcje konwersji PDF (w tym kompresję)

Teraz informujemy Aspose, że chcemy skompresowany PDF. Klasa `PdfConversionOptions` posiada flagę `setCompress`, która uruchamia wewnętrzny optymalizator PDF po renderowaniu. Możesz także dostosować inne opcje (np. wersję PDF lub jakość obrazu), jeśli potrzebujesz precyzyjniejszej kontroli.

```java
// Step 2 – define PDF options and enable compression
PdfConversionOptions pdfOptions = new PdfConversionOptions();
pdfOptions.setSandbox(renderingSandbox);   // attach the sandbox from Step 1
pdfOptions.setCompress(true);              // this is the key to how to compress pdf
```

Gdy wywołane zostanie `setCompress(true)`, Aspose usuwa duplikaty obiektów, zmniejsza rozdzielczość obrazów i usuwa nieużywane zasoby. Efektem jest zazwyczaj 30‑50 % redukcja rozmiaru pliku bez zauważalnej utraty jakości wizualnej.

## Krok 3: Wykonaj konwersję HTML‑do‑PDF

Gdy sandbox i opcje są gotowe, rzeczywista konwersja to jednowierszowy kod. Po prostu przekazujesz źródłowy URI HTML, docelowy URI PDF oraz skonstruowane opcje.

```java
// Step 3 – run the conversion
Converter.convert(
        Paths.get("YOUR_DIRECTORY/input.html").toUri(),
        Paths.get("YOUR_DIRECTORY/output.pdf").toUri(),
        pdfOptions);
```

Zastąp `YOUR_DIRECTORY` folderem zawierającym Twój `input.html`. Po zakończeniu wywołania, `output.pdf` znajdzie się obok niego, skompresowany i dopasowany do ekranu telefonu.

## Pełny, działający przykład

Poniżej znajduje się pełna klasa Java, która łączy wszystkie trzy kroki. Śmiało skopiuj i wklej ją do pliku o nazwie `ConvertWithSandbox.java`, dostosuj ścieżki i uruchom `javac` + `java` tak, jak zwykle.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.Screen;
import java.nio.file.Paths;

/**
 * Demonstrates how to compress PDF while converting HTML to PDF in Java.
 * It also shows how to set a custom screen (375×667 px) to mimic a mobile device.
 */
public class ConvertWithSandbox {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox with a custom screen size (mobile‑friendly)
        Sandbox renderingSandbox = new Sandbox();
        renderingSandbox.setScreen(new Screen(375, 667, 96, 1.0));

        // 2️⃣ Set up PDF conversion options – enable compression
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setSandbox(renderingSandbox);
        pdfOptions.setCompress(true); // <-- this is how to compress pdf

        // 3️⃣ Convert the HTML file to a compressed PDF
        Converter.convert(
                Paths.get("YOUR_DIRECTORY/input.html").toUri(),
                Paths.get("YOUR_DIRECTORY/output.pdf").toUri(),
                pdfOptions);

        System.out.println("Conversion complete! Check output.pdf – it should be smaller and fit a 375×667 screen.");
    }
}
```

### Oczekiwany rezultat

- **Rozmiar pliku:** Jeśli Twój oryginalny HTML wygenerował PDF o wielkości 2 MB, skompresowana wersja będzie zazwyczaj około 1 MB lub mniej.
- **Układ stron:** Strony PDF będą miały szerokość 375 pt (≈5 cali) i wysokość 667 pt, odpowiadając wymiarom podanym sandboxowi.
- **Wierność wizualna:** Tekst pozostaje ostry; obrazy są zmniejszane tylko na tyle, aby były czytelne na płótnie o rozmiarze telefonu.

Możesz zweryfikować redukcję rozmiaru, sprawdzając właściwości pliku przed i po konwersji.

## Typowe warianty i przypadki brzegowe

### 1. Chcesz większą kompresję?

`PdfConversionOptions` oferuje więcej ustawień:

```java
pdfOptions.setImageQuality(70);   // JPEG quality (0‑100)
pdfOptions.setRemoveUnusedObjects(true);
pdfOptions.setCompress(true);
```

Obniżenie `setImageQuality` dodatkowo zmniejsza rozmiar obrazów, ale uważaj na widoczne artefakty w zdjęciach wysokiej rozdzielczości.

### 2. Potrzebujesz innego rozmiaru ekranu?

Po prostu zmień wartości w konstruktorze `Screen`:

```java
renderingSandbox.setScreen(new Screen(1024, 768, 96, 1.0)); // tablet size
```

To przydatne, gdy masz responsywne projekty, które wyglądają inaczej na tabletach niż na telefonach.

### 3. Konwertowanie wielu plików HTML w pętli

Jeśli masz zestaw stron HTML, otocz wywołanie konwersji w pętli `for`:

```java
String[] files = {"page1.html", "page2.html"};
for (String file : files) {
    Converter.convert(
        Paths.get("src/html/" + file).toUri(),
        Paths.get("out/" + file.replace(".html", ".pdf")).toUri(),
        pdfOptions);
}
```

Ta sama instancja `pdfOptions` może być ponownie użyta, utrzymując spójną kompresję we wszystkich wynikach.

### 4. Obsługa zasobów zewnętrznych (CSS, obrazy)

Aspose.HTML rozwiązuje względne adresy URL na podstawie lokalizacji pliku HTML. Upewnij się, że wszystkie powiązane pliki CSS lub obrazy są dostępne w tym samym katalogu lub użyj bezwzględnych adresów URL (np. `https://example.com/style.css`). Jeśli zasób nie zostanie załadowany, konwerter zapisze ostrzeżenie, ale będzie kontynuował — więc nadal otrzymasz PDF, choć może brakować niektórych stylów.

## Najczęściej zadawane pytania

**P:** Czy kompresja wpływa na bezpieczeństwo PDF?  
**O:** Nie. Procedura kompresji optymalizuje jedynie wewnętrzną strukturę PDF; nie zmienia szyfrowania ani podpisów cyfrowych. Jeśli musisz podpisać PDF, zrób to *po* kompresji.

**P:** Czy mogę strumieniować wynik zamiast zapisywać go do pliku?  
**O:** Oczywiście. `Converter.convert` ma również przeciążoną wersję przyjmującą `OutputStream`. Zastąp docelowy URI `OutputStream` powiązanym z odpowiedzią servletu, na przykład.

**P:** Co zrobić, jeśli potrzebna jest zgodność z PDF/A?  
**O:** Użyj `PdfConversionOptions.setPdfACompliance(PdfACompliance.PdfA_1b)` przed wywołaniem `convert`. Kompresja nadal działa; Aspose zastosuje reguły specyficzne dla PDF/A po konwersji.

## Przegląd wizualny

![przykładowy diagram jak skompresować pdf](https://example.com/images/compress-pdf-diagram.png "Diagram przedstawiający przepływ konwersji od HTML → Sandbox (niestandardowy ekran) → Opcje PDF (kompresja) → PDF wyjściowy")

*Tekst alternatywny zawiera główne słowo kluczowe, aby spełnić wymagania SEO.*

## Zakończenie

Omówiliśmy **jak skompresować pdf** podczas konwertowania HTML do PDF w Javie, przedstawiliśmy przepływ **convert html to pdf** z użyciem Aspose.HTML oraz pokazaliśmy, jak **ustawić niestandardowy ekran** dla układów przyjaznych urządzeniom mobilnym. Pełny fragment kodu powyżej jest gotowy do uruchomienia, a wyjaśnienia dostarczają „dlaczego” każdej linii — dzięki czemu możesz dostosować rozwiązanie do własnych projektów.

Co dalej? Spróbuj eksperymentować z różnymi rozmiarami ekranu, dostosuj `setImageQuality` dla jeszcze większej kompresji lub połącz konwersję z etapem podpisywania PDF. Możesz także zbadać inne formaty wyjściowe Aspose (np. DOCX lub PNG) używając tej samej techniki sandbox.

Miłego kodowania i ciesz się odchudzonymi PDF‑ami!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}