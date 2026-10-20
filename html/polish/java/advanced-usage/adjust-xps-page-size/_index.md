---
date: 2026-08-28
description: Dostosuj rozmiar strony XPS podczas konwertowania HTML do XPS w Javie
  przy użyciu Aspose.HTML. Renderuj HTML do XPS z precyzyjnymi wymiarami.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: Dostosowywanie rozmiaru strony XPS
og_description: Dostosuj rozmiar strony XPS podczas konwertowania HTML do XPS w Javie
  przy użyciu Aspose.HTML. Dowiedz się, jak renderować HTML do XPS z precyzyjnymi
  wymiarami w ciągu kilku sekund.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Dostosuj rozmiar strony XPS podczas konwertowania HTML do XPS w Javie
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Dostosuj rozmiar strony XPS podczas konwertowania HTML do XPS w Javie
url: /pl/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dostosuj rozmiar strony XPS podczas konwertowania HTML do XPS w Javie

W tym samouczku dowiesz się **jak dostosować rozmiar strony XPS** podczas konwertowania HTML do XPS przy użyciu Aspose.HTML for Java. Niezależnie od tego, czy potrzebujesz drukowalnych faktur, raportów archiwalnych czy etykiet o niestandardowych rozmiarach, kontrolowanie wymiarów strony zapewnia, że ostateczny XPS wygląda dokładnie tak, jak zamierzono. Przeprowadzimy Cię przez konfigurację środowiska, opcje renderowania i generowanie końcowego XPS, abyś mógł wbudować tę funkcję bezpośrednio w swoje aplikacje Java.

## Szybkie odpowiedzi
- **Co oznacza „convert HTML to XPS”?** Renderuje dokument HTML do pliku XPS, zachowując układ i stylizację.  
- **Czy potrzebuję licencji?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.  
- **Jaką wersję Javy obsługuje?** Java 8 lub wyższą (zalecany JDK 11+).  
- **Czy mogę zmienić rozmiar strony?** Tak – Aspose.HTML pozwala określić niestandardowe wymiary przed renderowaniem.  
- **Jak długo trwa konwersja?** Zazwyczaj poniżej sekundy dla standardowych stron; większe dokumenty mogą zająć więcej czasu.

## Co to jest konwertowanie HTML do XPS?
Konwertowanie HTML do XPS oznacza wzięcie pliku znaczników przeznaczonego dla sieci i wygenerowanie dokumentu XPS (XML Paper Specification) — formatu o stałym układzie, gotowego do druku, podobnego do PDF. Jest to przydatne, gdy potrzebujesz dokumentów o wysokiej wierności, niezależnych od urządzenia, do archiwizacji lub drukowania z aplikacji Java.

## Dlaczego dostosować rozmiar strony XPS?
Dostosowanie rozmiaru strony XPS daje kontrolę nad fizycznymi wymiarami końcowego dokumentu (np. A4, Letter, etykiety niestandardowe). Zapobiega niepożądanemu skalowaniu, zapewnia idealne dopasowanie treści i może zmniejszyć rozmiar pliku poprzez usunięcie niepotrzebnej białej przestrzeni.

## Jak renderować HTML do XPS z niestandardowym rozmiarem strony?
Wczytaj swój HTML, skonfiguruj `XpsRenderingOptions` z `PageSetup`, który definiuje dokładną szerokość i wysokość, której potrzebujesz, a następnie renderuj do `XpsDevice`. Ten dwustopniowy przepływ pozwala zachować układ, jednocześnie wymuszając określone wymiary, wszystko w jednym wywołaniu API.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że masz następujące wymagania spełnione:

1. **Środowisko programistyczne Java** – Zainstalowany Java Development Kit (JDK) na Twoim systemie.  
2. **Biblioteka Aspose.HTML for Java** – Pobierz i dołącz bibliotekę Aspose.HTML for Java do swojego projektu. Bibliotekę znajdziesz na stronie [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).  
3. **Plik HTML wejściowy** – Przygotuj plik HTML, który chcesz renderować i dostosować rozmiar strony XPS. Możesz użyć własnego pliku HTML w tym samouczku.

## Importowanie pakietów

Klasa `Page` reprezentuje wymiary i ustawienia strony dla wyjścia XPS. Klasa `HtmlRenderer` wykonuje konwersję z HTML do XPS.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Przewodnik krok po kroku

Poniżej znajduje się zwięzły, numerowany przewodnik, który odzwierciedla oryginalne kroki, dodając dodatkowy kontekst dla jasności.

### Krok 1: ustaw nazwę pliku wejściowego

Klasa `FileInputStream` odczytuje surowe bajty z pliku, dostarczając źródło HTML do renderera.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Krok 2: utwórz dokument HTML i ustaw style

Klasa `HTMLDocument` reprezentuje w pamięci DOM HTML używany przez Aspose.HTML do renderowania.

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Krok 3: utwórz opcje renderowania XPS

Klasa `XpsRenderingOptions` przechowuje ustawienia kontrolujące, jak HTML jest renderowany do XPS, takie jak rozmiar strony i jakość obrazu.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Krok 4: dostosuj rozmiar strony  

**Jak ustawić rozmiar strony XPS** – Zdefiniuj niestandardowy rozmiar strony (szerokość × wysokość w punktach) i poinformuj renderer, czy ma automatycznie rozszerzać się do najszerszej strony. Ustawienie `adjustToWidestPage` na `false` zachowuje dokładne wymiary, które określisz.

Klasa `PageSetup` definiuje rozmiar strony, marginesy i orientację wyjścia XPS.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Krok 5: renderuj wynik

Klasa `XpsDevice` jest celem renderowania, który zapisuje przetworzoną zawartość do pliku XPS.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Typowe problemy i rozwiązania

| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| **Pusty wynik XPS** | Strumień wejściowy nie jest zamknięty lub HTMLDocument wskazuje niewłaściwy plik. | Upewnij się, że `FileInputStream` jest prawidłowo opakowany w blok try‑with‑resources i ścieżka do pliku jest dokładna. |
| **Rozmiar strony nie zastosowany** | `adjustToWidestPage` pozostawiono jako `true`. | Ustaw `pageSetup.setAdjustToWidestPage(false);` jak pokazano w Kroku 4. |
| **Nieobsługiwany CSS** | Aspose.HTML obsługuje podzbiór CSS. | Trzymaj się podstawowego układu, czcionek i kolorów; unikaj zaawansowanych selektorów lub CSS Grid. |
| **LicenseException** | Uruchamianie bez ważnej licencji w produkcji. | Zastosuj tymczasową lub zakupioną licencję przed renderowaniem (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Najczęściej zadawane pytania

**Q: Czym jest Aspose.HTML for Java?**  
**A:** Aspose.HTML for Java to biblioteka Java, która umożliwia programistom manipulację i konwersję dokumentów HTML do różnych formatów, takich jak XPS, PDF i obrazy. Bibliotekę możesz pobrać ze strony [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).

**Q: Gdzie mogę pobrać Aspose.HTML for Java?**  
**A:** Bibliotekę Aspose.HTML for Java możesz pobrać ze [strony z wydaniami produktów Aspose](https://releases.aspose.com/).

**Q: Czy dostępna jest darmowa wersja próbna Aspose.HTML for Java?**  
**A:** Tak, możesz uzyskać darmową wersję próbną Aspose.HTML for Java na [stronie z prośbą o tymczasową licencję](https://purchase.aspose.com/temporary-license/).

**Q: Jak mogę uzyskać tymczasową licencję dla Aspose.HTML for Java?**  
**A:** Aby uzyskać tymczasową licencję dla Aspose.HTML for Java, odwiedź [stronę z prośbą o tymczasową licencję](https://purchase.aspose.com/temporary-license/).

**Q: Czy mogę uzyskać wsparcie dla Aspose.HTML for Java?**  
**A:** Tak, możesz szukać pomocy i wsparcia w społeczności Aspose na [forum Aspose](https://forum.aspose.com/).

**Q: Czy mogę konwertować HTML do XPS na serwerze bez interfejsu graficznego?**  
**A:** Oczywiście. Aspose.HTML działa w środowiskach bez GUI; wystarczy zapewnić prawidłową konfigurację środowiska Java.

**Q: Czy biblioteka obsługuje niestandardowe marginesy strony?**  
**A:** Tak. Użyj `PageSetup.setMarginTop()`, `setMarginBottom()` itd., przed przypisaniem `PageSetup` do opcji renderowania.

## Podsumowanie

Przeszliśmy przez kompletny proces **konwertowania HTML do XPS** i **dostosowywania rozmiaru strony XPS** przy użyciu Aspose.HTML for Java. Postępując zgodnie z tymi krokami, możesz generować gotowe do druku dokumenty XPS, które spełniają dokładne wymagania układu. Śmiało eksperymentuj z różnymi wymiarami stron, stylami lub nawet dodawaj nagłówki i stopki, aby dopasować je do potrzeb projektu.

Jeśli masz pytania lub potrzebujesz dalszej pomocy, zapoznaj się z [dokumentacją Aspose.HTML for Java](https://reference.aspose.com/html/java/) lub dołącz do dyskusji na [forum Aspose](https://forum.aspose.com/).

---

**Ostatnia aktualizacja:** 2026-08-28  
**Testowano z:** Aspose.HTML for Java 24.11 (najnowsza w momencie pisania)  
**Autor:** Aspose

## Powiązane samouczki

- [Konwertuj HTML do XPS przy użyciu Aspose.HTML for Java](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [Dostosuj rozmiar strony PDF przy użyciu Aspose.HTML for Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Konwersja EPUB do XPS przy użyciu Aspose.HTML for Java](/html/java/converting-epub-to-xps/convert-epub-to-xps/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}