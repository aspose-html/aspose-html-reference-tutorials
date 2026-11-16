---
date: 2026-05-30
description: Dowiedz się, jak konwertować EPUB do PDF w Javie przy użyciu Aspose.HTML,
  ustawiając niestandardowy rozmiar strony PDF oraz inne opcje zapisu PDF.
keywords:
- custom pdf page size
- convert epub to pdf
- change pdf background color
- specify pdf page dimensions
- aspose.html java
linktitle: Określanie opcji zapisu PDF dla EPUB do PDF
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  headline: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  type: TechArticle
- description: Learn how to convert EPUB to PDF in Java with Aspose.HTML while setting
    a custom PDF page size and other PDF save options.
  name: Custom PDF Page Size - Specifying PDF Save Options for EPUB to PDF
  steps:
  - name: Open the EPUB File
    text: First, create a `FileInputStream` that points to your source `.epub`. Keeping
      the stream open until the conversion finishes prevents “blank page” errors.
  - name: Define PDF Save Options
    text: '`PdfSaveOptions` is Aspose.HTML''s configuration class that controls PDF
      output settings such as page size, background color, and margins. `Length.fromPixels`
      converts screen pixels to PDF points (1 point = 1/72 inch), allowing you to
      specify dimensions in familiar pixel units.'
  - name: Convert EPUB to PDF
    text: With the input stream and custom options ready, invoke the converter. The
      output PDF will be saved to the location you specify, preserving the exact page
      dimensions you defined. `PdfSaveOptions.setEnableParallelProcessing` is a method
      that enables parallel processing of pages during PDF conversion.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a commercial library, but you can obtain a free
      trial version from their [website](https://releases.aspose.com/).
    question: Is Aspose.HTML for Java a free library?
  - answer: Aspose.HTML for Java supports EPUB 2.0, EPUB 3.0, and EPUB 3.1, handling
      re‑flowable and fixed‑layout books with full CSS support.
    question: What EPUB formats are supported for conversion?
  - answer: Yes, you can customize the PDF output by adjusting the page setup, background
      color, compression level, and other settings in the `PdfSaveOptions`.
    question: Can I customize the PDF output further?
  - answer: The trial version may add a watermark to the first few pages and limits
      the maximum file size to 10 MB; purchase a license to remove these restrictions.
    question: Are there any limitations to the trial version of Aspose.HTML for Java?
  - answer: You can find answers to your questions and seek support on the [Aspose.HTML
      forum](https://forum.aspose.com/).
    question: Where can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Niestandardowy rozmiar strony PDF - Określanie opcji zapisu PDF dla EPUB do
  PDF
url: /pl/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-pdf-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Niestandardowy rozmiar strony PDF: Określanie opcji zapisu PDF dla EPUB do PDF

## Wprowadzenie

Aspose.HTML for Java ułatwia **konwersję EPUB do PDF** i daje pełną kontrolę nad wynikiem, w tym ustawienie **niestandardowego rozmiaru strony PDF**. W tym przewodniku krok po kroku przeprowadzimy Cię przez wszystko, czego potrzebujesz — od przygotowania środowiska po dostosowanie `PdfSaveOptions`, aby wygenerowany PDF miał dokładnie takie wymiary strony, jakich wymagasz. Niezależnie od tego, czy budujesz pipeline publikacji, platformę e‑learningową, czy po prostu potrzebujesz zautomatyzować konwersję dokumentów, znajdziesz tutaj przydatne techniki.

## Szybkie odpowiedzi
- **Jaki jest główny cel tego samouczka?** Konwersja pliku EPUB do PDF przy zastosowaniu niestandardowego rozmiaru strony PDF.  
- **Jakiej biblioteki użyto?** Aspose.HTML for Java.  
- **Czy potrzebna jest licencja?** Dostępna jest bezpłatna wersja próbna; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Czy mogę zmienić kolor tła?** Tak, przy użyciu `PdfSaveOptions`.  
- **Czy Java 8+ jest obsługiwana?** Absolutnie — działa każda nowoczesna maszyna wirtualna Java.

## Co to jest niestandardowy rozmiar strony PDF?

Niestandardowy rozmiar strony PDF pozwala określić dokładną szerokość i wysokość każdej strony w pliku PDF, zamiast polegać na standardowych rozmiarach, takich jak A4 czy Letter.  
Możesz ustawić wymiary w punktach (1 punkt = 1/72 cala) lub przeliczyć je z pikseli, co daje kontrolę piksel‑perfekcyjną nad ostatecznym układem. Jest to idealne rozwiązanie dla e‑booków, ulotek lub każdego projektu, który musi pasować do określonego formatu bez ręcznej obróbki po konwersji.

## Dlaczego warto używać Aspose.HTML do konwersji EPUB na PDF?

Aspose.HTML konwertuje EPUB do PDF w dwóch linijkach kodu, zachowując złożone układy, osadzone czcionki i obrazy wysokiej rozdzielczości. Obsługuje **ponad 50 formatów wejściowych i wyjściowych**, może renderować PDF‑y do **2 000 stron** bez ładowania całego pliku do pamięci i działa na Windows, Linux oraz macOS z identycznymi rezultatami. Biblioteka oferuje także szczegółowe opcje zapisu PDF, umożliwiając dostosowanie rozmiaru strony, koloru tła, marginesów i ustawień kompresji — wszystko z poziomu Javy.

## Wymagania wstępne
- **Środowisko programistyczne Java:** JDK 8 lub nowszy zainstalowany i skonfigurowany.  
- **Aspose.HTML for Java:** Pobierz najnowszy plik JAR ze [strony internetowej](https://releases.aspose.com/html/java/).  
- **Plik EPUB:** Dokument `.epub`, który chcesz przekonwertować.  

Teraz, gdy wszystko jest gotowe, przejdźmy do rzeczywistych kroków konwersji.

## Jak przekonwertować EPUB na PDF z niestandardowym rozmiarem strony?

`FileInputStream` to klasa Javy, która odczytuje surowe bajty z pliku.  
`PdfSaveOptions` to klasa w Aspose.HTML, która konfiguruje ustawienia wyjścia PDF, takie jak rozmiar strony i kolor tła.  
Wczytaj swój EPUB przy użyciu `FileInputStream`, skonfiguruj `PdfSaveOptions`, aby określić dokładne wymiary strony, i wywołaj konwerter. Poniższy trzyetapowy przepływ pracy wykonuje konwersję w mniej niż minutę dla typowych rozmiarów e‑booków i skaluje się do większych kolekcji przy minimalnych zmianach w kodzie.

### Krok 1: Otwórz plik EPUB

Najpierw utwórz `FileInputStream`, który wskazuje na Twój źródłowy plik `.epub`. Utrzymanie strumienia otwartego do momentu zakończenia konwersji zapobiega błędom „pustej strony”.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code for the next steps will go here.
}
```

### Krok 2: Zdefiniuj opcje zapisu PDF

`PdfSaveOptions` to klasa konfiguracyjna Aspose.HTML, która kontroluje ustawienia wyjścia PDF, takie jak rozmiar strony, kolor tła i marginesy.  
`Length.fromPixels` konwertuje piksele ekranu na punkty PDF (1 punkt = 1/72 cala), umożliwiając określenie wymiarów w znanych jednostkach pikseli.

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

#### Porada:
- **Piksele vs. Punkty:** `Length.fromPixels` konwertuje piksele ekranu na punkty PDF (1 punkt = 1/72 cala). Wybierz wartości odzwierciedlające ostateczny rozmiar wydruku, którego potrzebujesz.

### Krok 3: Konwertuj EPUB na PDF

Gdy strumień wejściowy i niestandardowe opcje są gotowe, wywołaj konwerter. Wyjściowy PDF zostanie zapisany w określonej przez Ciebie lokalizacji, zachowując dokładne wymiary strony, które zdefiniowałeś.

```java
com.aspose.html.converters.Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.pdf")
);
```

`PdfSaveOptions.setEnableParallelProcessing` to metoda, która włącza równoległe przetwarzanie stron podczas konwersji PDF.

## Pełny kod źródłowy

Pełny, działający przykład łączy trzy powyższe kroki w jednej klasie Java. Zastąp ścieżki zastępcze własnymi lokalizacjami plików.

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
| **Nieprawidłowe wymiary strony** | Użycie pikseli, które nie odpowiadają żądanemu rozmiarowi wydruku | Przelicz żądane cale na punkty (`1 inch = 72 points`), a następnie na piksele przy użyciu `Length.fromPixels`. |
| **Brakujące czcionki** | Czcionki nie są osadzone w EPUB | Upewnij się, że czcionki są zawarte w EPUB lub zainstaluj je na maszynie hosta. |
| **Spowolnienie wydajności przy dużych książkach** | Renderowanie każdej strony kolejno | Włącz renderowanie wielowątkowe za pomocą `PdfSaveOptions.setEnableParallelProcessing(true)`, aby przyspieszyć przetwarzanie EPUB‑ów powyżej 500 stron. |

## Najczęściej zadawane pytania (FAQ)

**P:** Czy Aspose.HTML for Java jest darmową biblioteką?  
**O:** Aspose.HTML for Java jest biblioteką komercyjną, ale możesz uzyskać bezpłatną wersję próbną ze [strony internetowej](https://releases.aspose.com/).

**P:** Jakie formaty EPUB są obsługiwane przy konwersji?  
**O:** Aspose.HTML for Java obsługuje EPUB 2.0, EPUB 3.0 i EPUB 3.1, obsługując książki reflowable i o stałym układzie z pełnym wsparciem CSS.

**P:** Czy mogę dalej dostosować wyjście PDF?  
**O:** Tak, możesz dostosować wyjście PDF, zmieniając ustawienia strony, kolor tła, poziom kompresji i inne opcje w `PdfSaveOptions`.

**P:** Czy istnieją ograniczenia wersji próbnej Aspose.HTML for Java?  
**O:** Wersja próbna może dodawać znak wodny do kilku pierwszych stron i ogranicza maksymalny rozmiar pliku do 10 MB; zakup licencję, aby usunąć te ograniczenia.

**P:** Gdzie mogę uzyskać wsparcie dla Aspose.HTML for Java?  
**O:** Odpowiedzi na pytania i wsparcie znajdziesz na [forum Aspose.HTML](https://forum.aspose.com/).

---

**Ostatnia aktualizacja:** 2026-05-30  
**Testowano z:** Aspose.HTML for Java 24.11 (najnowsza w momencie pisania)  
**Autor:** Aspose

## Powiązane samouczki

- [Dostosuj rozmiar strony PDF przy użyciu Aspose.HTML for Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Jak przekonwertować EPUB na PDF w Javie – używając Aspose.HTML](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-pdf/)
- [Konwertuj EPUB na PDF i obrazy przy użyciu Aspose.HTML for Java](/html/java/conversion-epub-to-image-and-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}