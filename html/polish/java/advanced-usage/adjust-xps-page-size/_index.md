---
title: Dostosuj rozmiar strony XPS za pomocą Aspose.HTML dla Java
linktitle: Dostosowywanie rozmiaru strony XPS
second_title: Przetwarzanie HTML w Javie za pomocą Aspose.HTML
description: Dowiedz się, jak dostosować rozmiar strony XPS za pomocą Aspose.HTML dla Java. Łatwo kontroluj wymiary wyjściowe swoich dokumentów XPS.
weight: 16
url: /pl/java/advanced-usage/adjust-xps-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dostosuj rozmiar strony XPS za pomocą Aspose.HTML dla Java


W tym samouczku przeprowadzimy Cię przez proces dostosowywania rozmiaru strony XPS za pomocą Aspose.HTML dla Java. Ta potężna biblioteka pozwala manipulować dokumentami HTML i renderować je w różnych formatach, w tym XPS. Dostosowanie rozmiaru strony jest niezbędne, gdy musisz kontrolować wymiary wyjściowe dokumentu XPS.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że spełnione są następujące wymagania wstępne:

1. Środowisko programistyczne Java: Upewnij się, że w systemie zainstalowany jest Java Development Kit (JDK).

2.  Aspose.HTML for Java Library: Musisz pobrać i uwzględnić Aspose.HTML for Java library w swoim projekcie Java. Możesz znaleźć bibliotekę[Tutaj](https://releases.aspose.com/html/java/).

3. Plik wejściowy HTML: Przygotuj plik HTML, który chcesz renderować i dostosuj rozmiar strony XPS. Możesz użyć własnego pliku HTML w tym samouczku.

## Importuj pakiety

Najpierw musisz zaimportować niezbędne pakiety, aby pracować z Aspose.HTML dla Java. Dołącz te pakiety na początku swojej klasy Java:

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

 W tym kroku odczytujemy plik wejściowy HTML za pomocą`FileInputStream`.

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

 Ten krok obejmuje utworzenie`HTMLDocument` i dodawanie do niego stylów.

## Krok 3: Utwórz opcje renderowania XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Tutaj tworzymy opcje renderowania XPS w celu skonfigurowania procesu renderowania.

## Krok 4: Dostosuj rozmiar strony

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Ten krok obejmuje ustawienie rozmiaru strony i określenie, czy ma on zostać dostosowany do najszerszej strony.

## Krok 5: Renderowanie wyjścia

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

W ostatnim kroku renderujemy dane wyjściowe XPS, korzystając ze skonfigurowanych opcji.

## Wniosek

tym samouczku pokazaliśmy, jak dostosować rozmiar strony XPS za pomocą Aspose.HTML dla Java. Możesz kontrolować wymiary wyjściowe swoich dokumentów XPS, upewniając się, że spełniają one Twoje specyficzne wymagania. Dzięki dostarczonemu kodowi i krokom możesz łatwo zaimplementować tę funkcję w swoich aplikacjach Java.

 Jeśli masz jakiekolwiek pytania lub potrzebujesz dalszej pomocy, możesz odwiedzić stronę[Aspose.HTML dla dokumentacji Java](https://reference.aspose.com/html/java/) lub poproś o pomoc w[Forum Aspose](https://forum.aspose.com/).

## Najczęściej zadawane pytania

### P1: Czym jest Aspose.HTML dla Java?

A1: Aspose.HTML for Java to biblioteka Java umożliwiająca programistom manipulowanie dokumentami HTML i konwertowanie ich na różne formaty, takie jak XPS, PDF i obrazy.

### P2: Gdzie mogę pobrać Aspose.HTML dla Java?

 A2: Bibliotekę Aspose.HTML dla języka Java można pobrać ze strony[ten link](https://releases.aspose.com/html/java/).

### P3: Czy jest dostępna bezpłatna wersja próbna Aspose.HTML dla Java?

 A3: Tak, możesz otrzymać bezpłatną wersję próbną Aspose.HTML dla Java na stronie[Tutaj](https://releases.aspose.com/).

### P4: W jaki sposób mogę uzyskać tymczasową licencję na Aspose.HTML dla Java?

 A4: Aby uzyskać tymczasową licencję na Aspose.HTML dla Java, odwiedź stronę[ta strona](https://purchase.aspose.com/temporary-license/).

### P5: Czy mogę uzyskać wsparcie dla Aspose.HTML dla Java?

 A5: Tak, możesz szukać pomocy i wsparcia w społeczności Aspose na[Forum Aspose](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
