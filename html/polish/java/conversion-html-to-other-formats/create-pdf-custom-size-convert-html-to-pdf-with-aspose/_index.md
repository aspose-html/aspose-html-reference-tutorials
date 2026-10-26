---
category: general
date: 2026-03-26
description: Utwórz PDF o niestandardowym rozmiarze z HTML przy użyciu Aspose.HTML
  dla Javy. Dowiedz się, jak konwertować HTML do PDF i ustawić rozmiar strony PDF
  w kilku prostych krokach.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: pl
og_description: Utwórz PDF o niestandardowym rozmiarze z HTML przy użyciu Aspose.
  Ten przewodnik pokaże, jak konwertować HTML na PDF, zmieniać rozmiar strony PDF
  i łatwo ustawiać rozmiar strony PDF.
og_title: Utwórz PDF o niestandardowym rozmiarze – szybki przewodnik konwersji HTML
  do PDF
tags:
- aspose
- java
- pdf
- html
title: Utwórz PDF o niestandardowym rozmiarze – konwertuj HTML na PDF przy użyciu
  Aspose
url: /pl/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tworzenie PDF o niestandardowym rozmiarze – konwersja HTML do PDF przy użyciu Aspose

Czy kiedykolwiek potrzebowałeś **utworzyć PDF o niestandardowym rozmiarze** z pliku HTML? W tym samouczku pokażemy, jak **konwertować HTML do PDF** i ustawić rozmiar strony PDF przy użyciu Aspose.HTML dla Javy.  

Jeśli tworzysz faktury, raporty lub e‑booki, dokładne wymiary strony mają znaczenie — w przeciwnym razie układ będzie wyśrodkowany nieprawidłowo lub zostanie obcięty.  

Przejdziemy przez każdy krok, od wczytania źródłowego HTML po dostosowanie marginesów, i zakończymy gotowym PDF. Bez niejasnych odniesień, tylko kompletny, gotowy do uruchomienia przykład, który możesz skopiować i wkleić już dziś.

## Czego będziesz potrzebować

- **Java 17** (lub dowolny nowszy JDK).  
- **Aspose.HTML for Java** JAR‑y – możesz pobrać najnowszą wersję z repozytorium Maven lub ze strony Aspose.  
- Prosty plik `input.html` umieszczony w wybranym przez Ciebie folderze.  
- IDE lub edytor tekstu według własnego wyboru; zazwyczaj koduję w IntelliJ IDEA, ale Eclipse również się sprawdza.

Posiadanie tych wymagań wstępnych oznacza, że nie napotkasz błędów „class not found” w połowie procesu.  

Teraz zanurzmy się.

![Przykład tworzenia PDF o niestandardowym rozmiarze](/images/create-pdf-custom-size.png "Zrzut ekranu pokazujący PDF wygenerowany z niestandardowym rozmiarem strony i marginesami – create pdf custom size")

## Tworzenie PDF o niestandardowym rozmiarze – Kluczowe kroki

Poniżej znajduje się pełny program w Javie, który otrzymasz. Śmiało skopiuj go do pliku o nazwie `ConvertHtmlToPdfCustomPage.java` i uruchom po dodaniu zależności Aspose do swojego projektu.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### Krok 1 – Konwersja HTML do PDF: Ładowanie dokumentu

Pierwszą rzeczą, którą robimy, jest **wczytanie HTML**, który chcemy przekształcić w PDF.  
`HTMLDocument` odczytuje plik, rozwiązuje względne odnośniki i buduje DOM, który Aspose może renderować.

> **Dlaczego to ważne:** Jeśli HTML odwołuje się do CSS lub obrazów, Aspose pobierze je względem ścieżki pliku. Użycie ścieżki bezwzględnej (`YOUR_DIRECTORY/input.html`) zapobiega niespodziankom typu „file not found”.

### Krok 2 – Zmiana rozmiaru strony PDF: Konfigurowanie opcji

Tworzymy tutaj obiekt `PdfConversionOptions`.  
- `setPageSize(PageSize.A4)` instruuje Aspose, aby użył standardowych wymiarów A4 (210 × 297 mm).  
- `setPageOrientation(...)` obraca stronę, jeśli potrzebny jest tryb poziomy.  
- `setMargins(new Margin(20, 20, 20, 20))` ustawia margines 20 punktów po każdej stronie.

Możesz zamienić `PageSize.A4` na `PageSize.LETTER` lub nawet **niestandardowy rozmiar**, przekazując obiekt `SizeF`, np.:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **Pro tip:** Jeden punkt to 1/72 cala. Jeśli myślisz w milimetrach, pomnóż przez 2.83465, aby uzyskać liczbę punktów.

### Krok 3 – Generowanie PDF z HTML: Uruchamianie konwersji

`Converter.convertHTML` wykonuje najcięższą pracę. Przyjmuje wczytany `HTMLDocument`, ścieżkę wyjściową oraz opcje, które właśnie skonfigurowaliśmy.  

Jeśli chcesz **ustawić rozmiar strony PDF** dynamicznie w zależności od zawartości, możesz obliczyć wymagane wymiary przed tym krokiem i odpowiednio dostosować `pdfOptions`.

### Krok 4 – Weryfikacja wyniku

Linia `System.out.println` jest opcjonalna, ale zapewnia szybki feedback podczas uruchamiania programu z konsoli. Po wykonaniu otwórz `custom_page.pdf` – powinieneś zobaczyć PDF w formacie A4 w orientacji pionowej z jednolitymi marginesami 20 punktów, dokładnie tak, jak określiliśmy.

## Konwersja HTML do PDF – Typowe warianty

### Użycie strumienia zamiast ścieżki pliku

Czasami nie masz fizycznego pliku; może HTML pochodzi z bazy danych lub API. W takim przypadku otocz ciąg w `ByteArrayInputStream`:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

Drugi argument to bazowy URL służący do rozwiązywania względnych zasobów.

### Zmiana orientacji strony

Jeśli Twój raport jest szeroki, przełącz na orientację poziomą:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### Drobne dopasowanie marginesów

Marginesy akceptują wartości zmiennoprzecinkowe, więc możesz ustawić 0,5 pt dla bardzo cienkiej krawędzi:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### Obsługa dużych plików HTML

Dla ogromnych dokumentów rozważ włączenie **wydajnego pamięciowo strumieniowania**:

```java
pdfOptions.setUseMemoryCache(true);
```

Powoduje to, że Aspose zapisuje dane pośrednie do plików tymczasowych zamiast trzymać wszystko w pamięci RAM.

## Ustawianie rozmiaru strony PDF – przypadki brzegowe i pułapki

- **Brak czcionek:** Jeśli Twój HTML używa niestandardowej czcionki niezainstalowanej na serwerze, PDF przejdzie na domyślną. Osadź czcionkę za pomocą `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);`.  
- **Skalowanie obrazów:** Obrazy o wysokiej rozdzielczości mogą zwiększyć rozmiar PDF. Użyj `pdfOptions.setImageResolution(150);`, aby zmniejszyć rozdzielczość przy zachowaniu jakości.  
- **Kompatybilność CSS:** Nie wszystkie właściwości CSS są w pełni obsługiwane. Trzymaj się standardowych technik układu (flexbox działa, ale grid może mieć drobne problemy).  
- **Uprawnienia do ścieżki:** Upewnij się, że proces ma prawo zapisu do `YOUR_DIRECTORY`. W przeciwnym razie zostanie rzucony `IOException`.

## Oczekiwany wynik

Uruchomienie programu generuje PDF, który wygląda tak (ilustracja koncepcyjna):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- Rozmiar strony: **A4** (210 × 297 mm).  
- Orientacja: **Pionowa**.  
- Marginesy: **20 pt** po każdej stronie.  

Otwórz plik w dowolnym przeglądarce PDF (Adobe Reader, Chrome itp.), aby potwierdzić.

## Podsumowanie

Teraz wiesz, jak **utworzyć PDF o niestandardowym rozmiarze** z źródła HTML przy użyciu Aspose.HTML dla Javy. Samouczek obejmował cały proces: **konwersję HTML do PDF**, **zmianę rozmiaru strony PDF**, **ustawienie rozmiaru strony PDF** oraz **generowanie PDF z HTML** z niestandardowymi marginesami.  

Śmiało eksperymentuj — zamień `PageSize.LETTER` na rozmiar legal, dostosuj marginesy lub osadź własne czcionki. Następnie możesz zbadać **dodawanie znaków wodnych**, **szyfrowanie PDF** lub **przetwarzanie wsadowe wielu plików HTML**. Wszystkie te tematy opierają się na tych samych podstawowych koncepcjach, które właśnie omówiliśmy.

Masz pytanie dotyczące konkretnego przypadku brzegowego? Napisz komentarz poniżej, a pomogę Ci rozwiązać problem. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}