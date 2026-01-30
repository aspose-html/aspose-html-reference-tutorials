---
date: 2026-01-02
description: Dowiedz się, jak konwertować EPUB na PDF w Javie przy użyciu Aspose.HTML,
  ustawiając niestandardowy rozmiar strony PDF oraz inne opcje zapisu PDF.
linktitle: Specifying PDF Save Options for EPUB to PDF
second_title: Java HTML Processing with Aspose.HTML
title: 'Niestandardowy rozmiar strony PDF: Określanie opcji zapisu PDF dla konwersji
  EPUB do PDF'
url: /pl/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Niestandardowy rozmiar strony PDF: Określanie opcji zapisu PDF dla konwersji EPUB do PDF

## Wprowadzenie

Aspose.HTML for Java ułatwia **konwersję EPUB do PDF** i daje pełną kontrolę nad wynikiem, w tym możliwość ustawienia **niestandardowego rozmiaru strony PDF**. W tym przewodniku krok po kroku przeprowadzimy Cię przez wszystko, co jest potrzebne — od przygotowania środowiska po dostosowanie `PdfSaveOptions`, aby wygenerowany PDF miał dokładnie takie wymiary strony, jakie są wymagane. Niezależnie od tego, czy budujesz pipeline publikacji, platformę e‑learningową, czy po prostu potrzebujesz automatyzacji konwersji dokumentów, znajdziesz tutaj przydatne techniki.

## Szybkie odpowiedzi
- **Jaki jest główny cel tego samouczka?** Konwersja pliku EPUB do PDF przy zastosowaniu niestandardowego rozmiaru strony PDF.  
- **Której biblioteki użyto?** Aspose.HTML for Java.  
- **Czy potrzebna jest licencja?** Dostępna jest bezpłatna wersja próbna; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Czy mogę zmienić kolor tła?** Tak, przy użyciu `PdfSaveOptions`.  
- **Czy Java 8+ jest wspierana?** Oczywiście — działa na każdym nowoczesnym środowisku uruchomieniowym Javy.

## Czym jest niestandardowy rozmiar strony PDF?

Niestandardowy rozmiar strony PDF pozwala określić dokładną szerokość i wysokość każdej strony w wygenerowanym PDF, zamiast polegać na standardowych rozmiarach, takich jak A4 czy Letter. Jest to szczególnie przydatne w przypadku e‑booków, ulotek lub wszelkich sytuacji, w których układ wizualny musi odpowiadać określonemu projektowi.

## Dlaczego warto używać Aspose.HTML do konwersji EPUB na PDF?

- **Wysoka wierność:** Zachowuje złożone układy, czcionki i obrazy.  
- **Precyzyjna kontrola:** Umożliwia dostosowanie rozmiaru strony, tła, marginesów i innych ustawień za pomocą `PdfSaveOptions`.  
- **Wieloplatformowość:** Działa na Windows, Linux i macOS przy użyciu tego samego kodu Java.  
- **Wydajność:** Zoptymalizowany silnik renderujący zapewnia szybkie konwersje.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz:

- **Środowisko programistyczne Java:** Zainstalowany i skonfigurowany JDK 8 lub nowszy.  
- **Aspose.HTML for Java:** Pobierz najnowszy plik JAR ze [strony internetowej](https://releases.aspose.com/html/java/).  
- **Plik EPUB:** Dokument `.epub`, który chcesz przekonwertować.  

Teraz, gdy wszystko jest gotowe, przejdźmy do rzeczywistych kroków konwersji.

## Krok 1: Otwórz plik EPUB

Najpierw musimy otworzyć plik EPUB przy użyciu `FileInputStream`. Ten strumień zostanie później przekazany do konwertera.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

## Krok 2: Zdefiniuj opcje zapisu PDF

Tutaj ustawiamy **niestandardowy rozmiar strony PDF** oraz opcjonalny kolor tła. Dostosuj wartości w pikselach, aby odpowiadały żądanym wymiarom.

```java
com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
anyPage.setSize(new com.aspose.html.drawing.Size(
    com.aspose.html.drawing.Length.fromPixels(3000),
    com.aspose.html.drawing.Length.fromPixels(1000))
);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
```

### Wskazówka:
- **Piksele vs. Punkty:** `Length.fromPixels` konwertuje piksele ekranu na punkty PDF (1 punkt = 1/72 cala). Wybierz wartości odzwierciedlające ostateczny rozmiar wydruku, którego potrzebujesz.

## Krok 3: Konwertuj EPUB do PDF

Gdy strumień wejściowy i niestandardowe opcje są gotowe, wywołaj konwerter. Wyjściowy PDF zostanie zapisany w określonej przez Ciebie lokalizacji.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

## Pełny kod źródłowy

```java
Specifying PDF Save Options for EPUB to PDF
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of the PdfSaveOptions with a custom page-size and a background-color.
            com.aspose.html.saving.PdfSaveOptions options = new com.aspose.html.saving.PdfSaveOptions();
            com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
            com.aspose.html.drawing.Page anyPage = new com.aspose.html.drawing.Page();
            anyPage.setSize(new com.aspose.html.drawing.Size(
                    com.aspose.html.drawing.Length.fromPixels(3000),
                    com.aspose.html.drawing.Length.fromPixels(1000))
            );
            pageSetup.setAnyPage(anyPage);
            options.setPageSetup(pageSetup);
            options.setBackgroundColor(com.aspose.html.drawing.Color.getAliceBlue());
            // Call the ConvertEPUB method to convert the EPUB to PDF.
            com.aspose.html.converters.Converter.convertEPUB(
                    fileInputStream,
                    options,
                    Resources.output("output.pdf")
            );
        }
```

## Typowe problemy i rozwiązania

| Problem | Przyczyna | Rozwiązanie |
|-------|-------|-----|
| **Strony PDF są puste** | Strumień wejściowy zamknięty przed konwersją | Utrzymaj blok `try‑with‑resources` otwarty aż do zakończenia `convertEPUB`. |
| **Nieprawidłowe wymiary stron** | Użycie pikseli, które nie odpowiadają żądanemu rozmiarowi wydruku | Przelicz żądane cale na punkty (`1 cal = 72 punkty`), a następnie na piksele przy użyciu `Length.fromPixels`. |
| **Brakujące czcionki** | Czcionki nie są osadzone w pliku EPUB | Upewnij się, że czcionki są zawarte w pliku EPUB lub zainstaluj je na maszynie hosta. |

## Najczęściej zadawane pytania (FAQ)

### Czy Aspose.HTML for Java jest darmową biblioteką?
Aspose.HTML for Java jest biblioteką komercyjną, ale możesz uzyskać bezpłatną wersję próbną ze swojej [strony internetowej](https://releases.aspose.com/).

### Jakie formaty EPUB są obsługiwane przy konwersji?
Aspose.HTML for Java obsługuje konwersję różnych formatów EPUB, zapewniając kompatybilność z większością dokumentów EPUB.

### Czy mogę dalej dostosować wyjściowy PDF?
Tak, możesz dostosować wyjściowy PDF, modyfikując ustawienia strony, kolor tła oraz inne opcje w `PdfSaveOptions`.

### Czy wersja próbna Aspose.HTML for Java ma jakieś ograniczenia?
Wersja próbna może mieć pewne ograniczenia, dlatego zaleca się sprawdzenie dokumentacji w celu uzyskania szczegółów.

### Gdzie mogę uzyskać wsparcie dla Aspose.HTML for Java?
Odpowiedzi na pytania i wsparcie znajdziesz na [forum Aspose.HTML](https://forum.aspose.com/).

---

**Ostatnia aktualizacja:** 2026-01-02  
**Testowano z:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}