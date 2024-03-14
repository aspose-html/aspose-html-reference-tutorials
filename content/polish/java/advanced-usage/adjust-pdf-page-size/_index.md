---
title: Dostosuj rozmiar strony PDF za pomocą Aspose.HTML dla Java
linktitle: Dostosowywanie rozmiaru strony PDF
second_title: Przetwarzanie HTML w Javie za pomocą Aspose.HTML
description: Dowiedz się, jak dostosować rozmiar strony PDF za pomocą Aspose.HTML dla Java. Bez wysiłku twórz wysokiej jakości pliki PDF w formacie HTML. Skutecznie kontroluj wymiary strony.
type: docs
weight: 15
url: /pl/java/advanced-usage/adjust-pdf-page-size/
---

dzisiejszej epoce cyfrowej rośnie zapotrzebowanie na generowanie wysokiej jakości plików PDF z treści HTML. Aspose.HTML for Java to potężna biblioteka Java, która umożliwia bezproblemową konwersję dokumentów HTML do formatu PDF. W tym samouczku skupimy się na dostosowaniu rozmiaru strony podczas konwersji HTML na PDF przy użyciu Aspose.HTML dla Java.

## Warunki wstępne

Zanim zaczniesz, upewnij się, że spełnione są następujące wymagania wstępne:

- Środowisko programistyczne Java: Upewnij się, że w systemie jest zainstalowany zestaw Java Development Kit (JDK).
-  Aspose.HTML dla Java: Musisz pobrać i zainstalować Aspose.HTML dla Java ze strony internetowej[Tutaj](https://releases.aspose.com/html/java/).
- Dokument HTML: Powinieneś mieć dokument HTML gotowy do konwersji. Jeśli nie, utwórz go lub użyj istniejącego pliku HTML.

## Importuj pakiety

Aby rozpocząć, musisz zaimportować niezbędne pakiety do pracy z Aspose.HTML dla Java. Poniższy fragment kodu demonstruje, jak to zrobić:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Teraz, gdy masz już wymagania wstępne i zaimportowałeś niezbędne pakiety, podzielmy proces dostosowywania rozmiaru strony PDF na kilka kroków:

## Krok 1: Czytanie treści HTML

Najpierw musisz przeczytać treść HTML, którą chcesz przekonwertować na format PDF. W tym przykładzie odczytamy kod HTML z pliku o nazwie „FirstFile.html”.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Krok 2: Pisanie treści HTML

Następnie zapiszesz zawartość HTML do pliku o nazwie „FirstFileOut.html”.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Dodaj tutaj niestandardowe style lub treść HTML
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Krok 3: Renderowanie HTML do formatu PDF

Teraz wyrenderujesz zawartość HTML do pliku PDF. Omówimy dwa scenariusze: jeden, w którym rozmiar strony nie jest dostosowany do szerokości treści, i drugi, w którym jest on dostosowywany.

### Rozmiar strony nie został dostosowany

W tym scenariuszu rozmiar strony jest ustawiony na stałą szerokość i wysokość, co może spowodować przycięcie zawartości, jeśli przekroczy te wymiary.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Utwórz instancję HTMLDocument z pliku HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Ustaw opcje renderowania PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Renderuj dane wyjściowe
pdf_renderer.render(device, html_document);
```

### Rozmiar strony dostosowany do szerokości treści

W tym scenariuszu rozmiar strony jest dostosowywany w zależności od szerokości treści.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Renderuj dane wyjściowe
pdf_renderer.render(device, html_document);
```

## Wniosek

W tym samouczku omówiliśmy, jak dostosować rozmiar strony PDF podczas konwersji HTML na PDF przy użyciu Aspose.HTML dla Java. Znasz wymagania wstępne, zaimportowałeś wymagane pakiety i postępowałeś zgodnie z przewodnikiem krok po kroku, aby wykonać to zadanie. Dzięki Aspose.HTML dla Java możesz łatwo kontrolować rozmiar strony generowanych plików PDF, upewniając się, że zawartość jest wyświetlana zgodnie z przeznaczeniem.

 Możesz eksperymentować z różnymi rozmiarami stron i ustawieniami, aby spełnić swoje specyficzne wymagania. Jeśli napotkasz jakiekolwiek problemy lub masz dalsze pytania, nie wahaj się zwrócić o pomoc do[Aspose.HTML dla dokumentacji Java](https://reference.aspose.com/html/java/) albo[Forum wsparcia Aspose](https://forum.aspose.com/).

## Często zadawane pytania

### P1: Co to jest Aspose.HTML dla Java?

O1: Aspose.HTML for Java to biblioteka Java, która umożliwia pracę z dokumentami HTML, manipulowanie nimi, konwertowanie ich i renderowanie do różnych formatów, w tym PDF.

### P2: Jak mogę dostosować rozmiar strony PDF podczas konwersji HTML na PDF za pomocą Aspose.HTML dla Java?

 O2: Możesz dostosować rozmiar strony PDF za pomocą`PageSetup` klasę i ustawienie`AdjustToWidestPage` własność do`true` lub `false, w zależności od wymagań.

### P3: Czy mogę dostosować styl zawartości HTML przed konwersją jej do formatu PDF?

O3: Tak, możesz dostosować styl, dodając elementy CSS i HTML do treści HTML przed konwersją do formatu PDF, jak pokazano w samouczku.

### P4: Gdzie mogę znaleźć dokumentację Aspose.HTML dla Java?

 A4: Możesz zapoznać się z dokumentacją[Tutaj](https://reference.aspose.com/html/java/) w celu uzyskania wyczerpujących informacji i przykładów.

### P5: Czy dostępna jest bezpłatna wersja próbna Aspose.HTML dla Java?

 O5: Tak, możesz uzyskać dostęp do bezpłatnej wersji próbnej Aspose.HTML dla Java z[ten link](https://releases.aspose.com/).