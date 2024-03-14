---
title: Dostosuj rozmiar strony XPS za pomocą Aspose.HTML dla Java
linktitle: Dostosowywanie rozmiaru strony XPS
second_title: Przetwarzanie HTML w Javie za pomocą Aspose.HTML
description: Dowiedz się, jak dostosować rozmiar strony XPS za pomocą Aspose.HTML dla Java. Z łatwością kontroluj wymiary wyjściowe dokumentów XPS.
type: docs
weight: 16
url: /pl/java/advanced-usage/adjust-xps-page-size/
---

W tym samouczku przeprowadzimy Cię przez proces dostosowywania rozmiaru strony XPS przy użyciu Aspose.HTML dla Java. Ta potężna biblioteka umożliwia manipulowanie dokumentami HTML i renderowanie ich do różnych formatów, w tym XPS. Dostosowanie rozmiaru strony jest niezbędne, gdy trzeba kontrolować wymiary wyjściowe dokumentu XPS.

## Warunki wstępne

Zanim zaczniemy, upewnij się, że spełnione są następujące wymagania wstępne:

1. Środowisko programistyczne Java: Upewnij się, że w systemie jest zainstalowany zestaw Java Development Kit (JDK).

2.  Biblioteka Aspose.HTML dla Java: Musisz pobrać i dołączyć bibliotekę Aspose.HTML dla Java do swojego projektu Java. Możesz znaleźć drogę do biblioteki[Tutaj](https://releases.aspose.com/html/java/).

3. Wejściowy plik HTML: Przygotuj plik HTML, który chcesz wyrenderować, i dostosuj rozmiar strony XPS. W tym samouczku możesz użyć własnego pliku HTML.

## Importuj pakiety

Najpierw musisz zaimportować niezbędne pakiety do pracy z Aspose.HTML dla Java. Dołącz te pakiety na początku klasy Java:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Krok 1: Ustaw nazwę pliku wejściowego

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 Na tym etapie czytamy plik wejściowy HTML za pomocą rozszerzenia`FileInputStream`.

## Krok 2: Utwórz dokument HTML i ustaw style

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Ten krok polega na utworzeniu pliku`HTMLDocument` i dodawanie do niego stylów.

## Krok 3: Utwórz opcje renderowania XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Tutaj tworzymy opcje renderowania XPS, aby skonfigurować proces renderowania.

## Krok 4: Dostosuj rozmiar strony

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Ten krok obejmuje ustawienie rozmiaru strony i określenie, czy dostosować go do najszerszej strony.

## Krok 5: Wyrenderuj wynik

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

W ostatnim kroku renderujemy dane wyjściowe XPS, korzystając ze skonfigurowanych opcji.

## Wniosek

tym samouczku pokazaliśmy, jak dostosować rozmiar strony XPS za pomocą Aspose.HTML dla Java. Możesz kontrolować wymiary wyjściowe dokumentów XPS, upewniając się, że spełniają one Twoje specyficzne wymagania. Dzięki dostarczonemu kodowi i krokom możesz łatwo zaimplementować tę funkcję w swoich aplikacjach Java.

 Jeśli masz jakieś pytania lub potrzebujesz dalszej pomocy, odwiedź stronę[Aspose.HTML dla dokumentacji Java](https://reference.aspose.com/html/java/) lub poproś o pomoc na[Forum Aspose](https://forum.aspose.com/).

## Często zadawane pytania

### P1: Co to jest Aspose.HTML dla Java?

O1: Aspose.HTML for Java to biblioteka Java, która umożliwia programistom manipulowanie i konwertowanie dokumentów HTML do różnych formatów, takich jak XPS, PDF i obrazy.

### P2: Gdzie mogę pobrać Aspose.HTML dla Java?

 O2: Możesz pobrać bibliotekę Aspose.HTML dla Java z[ten link](https://releases.aspose.com/html/java/).

### P3: Czy dostępna jest bezpłatna wersja próbna Aspose.HTML dla Java?

 Odpowiedź 3: Tak, możesz uzyskać bezpłatną wersję próbną Aspose.HTML dla Java od[Tutaj](https://releases.aspose.com/).

### P4: Jak mogę uzyskać tymczasową licencję na Aspose.HTML dla Java?

 A4: Aby uzyskać tymczasową licencję na Aspose.HTML dla Java, odwiedź stronę[ta strona](https://purchase.aspose.com/temporary-license/).

### P5: Czy mogę uzyskać wsparcie dla Aspose.HTML dla Java?

 Odpowiedź 5: Tak, możesz szukać pomocy i wsparcia w społeczności Aspose na stronie[Forum Aspose](https://forum.aspose.com/).