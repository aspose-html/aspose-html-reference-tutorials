---
date: 2025-12-01
description: Dowiedz się, jak dostosować rozmiar strony PDF, renderować HTML jako
  PDF i generować PDF z HTML przy użyciu Aspose.HTML dla Javy. Łatwo kontroluj wymiary
  stron.
language: pl
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Dostosuj rozmiar strony PDF w Aspose.HTML dla Javy
url: /java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dostosuj rozmiar strony PDF przy użyciu Aspose.HTML dla Javy

Generowanie plików PDF z HTML jest powszechnym wymogiem dla raportów, faktur i e‑książek. Kiedy **dostosowujesz rozmiar strony PDF**, zapewniasz, że końcowy dokument odpowiada układowi zaprojektowanemu w HTML. W tym samouczku nauczysz się, jak renderować HTML jako PDF, ustawiać własne wymiary i kontrolować, czy strona automatycznie rozszerza się do najszerszej zawartości. Przejdziemy przez kompletny, praktyczny przykład z użyciem Aspose.HTML dla Javy.

## Szybkie odpowiedzi
- **Co oznacza „dostosowanie rozmiaru strony PDF”?** Umożliwia określenie szerokości i wysokości każdej strony PDF lub pozwala rendererowi automatycznie dopasować najszerszy element.  
- **Jakiej biblioteki użyto?** Aspose.HTML for Java (najnowsza wersja).  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.  
- **Czy mogę zmieniać wymiary programowo?** Tak – użyj `PageSetup` i właściwości `AdjustToWidestPage`.  
- **Czy jest kompatybilny z Java 8+?** Oczywiście – API działa z dowolnym JDK 8 lub nowszym.

## Co to jest „dostosowanie rozmiaru strony PDF”?
Dostosowanie rozmiaru strony PDF oznacza konfigurowanie wymiarów każdej strony tworzonej przez renderer HTML. Możesz ustawić stały rozmiar (np. A4, Letter) lub pozwolić rendererowi obliczyć optymalną szerokość na podstawie zawartości. Daje to precyzyjną kontrolę nad układem, paginacją i wiernością wizualną.

## Dlaczego dostosowywać rozmiar strony PDF przy konwersji HTML do PDF?
- **Zachowaj zamierzenia projektowe:** Zapobiegaj przycinaniu lub rozciąganiu treści.  
- **Optymalizuj pod druk:** Dopasuj rozmiar papieru wymaganego przez dalsze procesy.  
- **Popraw czytelność:** Unikaj nadmiernych białych przestrzeni lub ściśniętego tekstu.  
- **Dokumenty dynamiczne:** Automatycznie dopasuj szerokie tabele lub obrazy bez ręcznych obliczeń.

## Wymagania wstępne
Przed rozpoczęciem upewnij się, że masz:

- **Java Development Kit (JDK) 8 lub wyższy** zainstalowany na Twoim komputerze.  
- **Aspose.HTML for Java** – pobierz najnowszy plik JAR ze [strony oficjalnego wydania](https://releases.aspose.com/html/java/).  
- **Plik HTML**, który chcesz przekonwertować (w przykładzie użyjemy `FirstFile.html`).  

## Importowanie pakietów
Najpierw zaimportuj klasy, których będziemy potrzebować. Poniższy blok kodu jest niezmieniony w stosunku do oryginalnego samouczka.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## Krok 1: Odczyt zawartości HTML
Odczytujemy plik źródłowy HTML przy użyciu `FileInputStream`. Ten krok przygotowuje surowy kod do dalszej manipulacji.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Krok 2: Zapis (i opcjonalne wzbogacenie) HTML
Tutaj kopiujemy oryginalny HTML do nowego pliku i wstrzykujemy kilka stylów inline, aby pokazać, jak stylizacja wpływa na wynik PDF. Śmiało zamień przykładowy CSS na własny.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
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

## Krok 3: Renderowanie HTML do PDF – dwa scenariusze
Teraz zobaczymy, jak **generować PDF z HTML** przy użyciu dwóch różnych strategii rozmiaru strony.

### 3.1 Rozmiar strony NIE jest dostosowany do szerokości zawartości
W tym przypadku ustalamy stałe wymiary strony (100 × 100 punktów). Jeśli jakikolwiek element przekroczy te limity, zostanie przycięty.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 Rozmiar strony DOSTOSOWANY do szerokości zawartości
Tutaj włączamy `AdjustToWidestPage`, więc renderer automatycznie rozszerza szerokość strony, aby pomieścić najszerszy element, zachowując stałą wysokość.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## Jak ustawić wymiary PDF (jak zmienić rozmiar strony PDF) w kodzie
Obiekt `PageSetup` jest kluczowy:

- `setAnyPage(Page page)`: definiuje podstawową szerokość × wysokość.  
- `setAdjustToWidestPage(boolean)`: przełącza automatyczne rozszerzanie.  

Dostosowując te dwie właściwości, możesz **ustawiać wymiary PDF** w dowolnym scenariuszu, niezależnie od tego, czy potrzebujesz statycznej strony A4, czy dynamicznej szerokości dopasowanej do układu HTML.

## Typowe problemy i wskazówki
| Problem | Dlaczego się pojawia | Rozwiązanie |
|-------|----------------|-----|
| Zawartość jest przycinana | Stały rozmiar jest za mały | Zwiększ wartości `Size` lub włącz `AdjustToWidestPage`. |
| Tekst jest rozmyty | Domyślna rozdzielczość DPI renderowania jest niska | Użyj `PdfRenderingOptions.setResolution(int dpi)`, aby zwiększyć jakość. |
| Brak stylów | Zewnętrzny CSS nie został załadowany | Osadź CSS inline lub użyj `HTMLDocument.setBaseUrl()`, aby wskazać folder z arkuszami stylów. |
| Duże pliki HTML powodują błąd OutOfMemoryError | Renderer ładuje cały dokument do pamięci | Przetwarzaj dokument w częściach lub zwiększ pamięć JVM (`-Xmx`). |

## Najczęściej zadawane pytania

**Q: Czym jest Aspose.HTML for Java?**  
A: To biblioteka Java, która umożliwia tworzenie, edytowanie i renderowanie dokumentów HTML, w tym konwersję do PDF, PNG i innych formatów.

**Q: Jak mogę dostosować rozmiar strony PDF przy konwersji HTML do PDF przy użyciu Aspose.HTML for Java?**  
A: Użyj klasy `PageSetup` i ustaw `AdjustToWidestPage` na `true` (auto‑rozmiar) lub `false` (rozmiar stały). Następnie przypisz żądany `Size` za pomocą `new Page(new Size(width, height))`.

**Q: Czy mogę dostosować stylizację treści HTML przed konwersją do PDF?**  
A: Tak – możesz wstrzykiwać CSS, modyfikować DOM lub używać zewnętrznych arkuszy stylów. Samouczek demonstruje wstrzykiwanie CSS inline.

**Q: Gdzie mogę znaleźć dokumentację Aspose.HTML for Java?**  
A: Kompleksowa dokumentacja jest dostępna [tutaj](https://reference.aspose.com/html/java/).

**Q: Czy dostępna jest darmowa wersja próbna Aspose.HTML for Java?**  
A: Oczywiście – pobierz wersję próbną ze [strony wydania](https://releases.aspose.com/html/java/).

## Podsumowanie
Teraz wiesz, jak **dostosować rozmiar strony PDF**, **renderować HTML jako PDF** i **ustawiać własne wymiary PDF** przy użyciu Aspose.HTML for Java. Eksperymentuj z różnymi rozmiarami stron, ustawieniami DPI i modyfikacjami CSS, aby dopracować wynik pod swoje konkretne zastosowanie. Jeśli napotkasz problemy, odwołaj się do oficjalnej dokumentacji lub forów wsparcia Aspose.

---

**Ostatnia aktualizacja:** 2025-12-01  
**Testowano z:** Aspose.HTML for Java 24.12 (latest)  
**Autor:** Aspose  
**Powiązane zasoby:** [API Reference](https://reference.aspose.com/html/java/) | [Download Free Trial](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}