---
date: 2026-01-09
description: Dowiedz się, jak używać Aspose.HTML dla Javy, aby określić opcje zapisu
  XPS i efektywnie konwertować EPUB na XPS.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Określanie opcji zapisu Aspose HTML przy konwersji EPUB na XPS
url: /pl/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# podłączenie do transmisji danych Aspose HTML dla EPUB do XPS

Konwersja dokumentu EPUB do XPS może być pozostałością procesu publikacji, a **Aspose HTML Save Options** precyzyjną kontrolą nad obliczeniem. W tym samouczku przeprowadziliśmy niezbędne kroki do konfiguracji tych zapisu przy użyciu Aspose.HTML dla Javy i wygenerowania wysokiej jakości plików XPS.

## Szybkie odpowiedzi
- **Co robi Aspose HTML Save Options?** Umożliwiają dostosowanie rozmiaru strony, koloru tła i innych ustawień renderowania podczas zapisywania do formatów takich jak XPS.
- **Jakiej biblioteki wymaga?** Aspose.HTML for Java (najnowsza wersja).
- **Czy egzamin jest licencjatem?** Dostępna wersja egzaminacyjna do egzaminu; licencjat komercyjny jest wymagany w środowisku produkcyjnym.
- **Czy można zmienić wymiary stron?** Tak – można ustawić szerokość i wysokość za pomocą `PageSetup`.
- **Czy konwersja jest szybka?** Dla typowych plików EPUB konwersja kończy się w ciągu kilku sekund na nowoczesnych maszynach JVM.

## Jakie są opcje zapisywania HTML Aspose?
Przypisz opcje HTML Save do zestawów właściwości, które kontrolują sposób renderowania i zaaplikacji dokumentów HTML, EPUB lub innych dokumentów internetowych do formatu docelowego, takiego jak XPS, PDF lub plików graficznych. Umożliwiają zdefiniowanie układu strony, kolorów tła, marginesów i innych elementów, uwzględniając, zastosowanie pliku spełniającego wymagania projektowe.

## Dlaczego warto używać Aspose.HTML dla Java do konwersji EPUB na XPS?
- **Wysoka wierność** – utworzony układ, rozbudowa i grafikę wektorową.
- **Programowa kontrola** – automatyzuje konwersje wsadowe w aplikacjach Java.
- **Brak zewnętrznych zależności** – czysta biblioteka Java, bez dostępu natywnych.
- **Dostosowywalny wynik** – dzięki opcjom zapisu aplikacji XPS dokładnie do Twoich potrzeb.

## Warunki wstępne

Zanim przejdziemy do kodu, sprawdź się, że masz dodatkowe elementy:

1. **Środowisko programistyczne Java** – gotowe JDK 8 lub nowszy.
2. **Biblioteka Aspose.HTML dla Java** – pobierz ją z [linku do pobrania](https://releases.aspose.com/html/java/).
3. **Plik EPUB** – źródłowy plik EPUB, który chcesz przekonwertować.

Posiadanie ich wytwarzanych przez przełączniki bez przerw.

## Importuj pakiety

Najpierw zaimportuj wymaganą klasę. Umieść importy na swoim pierwotnym pliku źródłowym Java:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

Te importy dają dostęp do silnika konwersji oraz **Aspose HTML Save Options** potrzebnych do precyzyjnego dostosowania.

## Otwórz plik EPUB

Następnie otwórz plik EPUB, który chcesz przekonwertować. Pomocnik `Resources.input` ładuje plik z folderu zasobów demonstracyjnych:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Użycie bloku try‑with‑resources zapewnia automatyczne zamknięcie strumienia.

## Utwórz opcje zapisu XPS (skonfiguruj rozmiar strony i tło)

Teraz tworzymy instancję `XpsSaveOptions` i dostosowujemy ją. To miejsce, w którym **opcje zapisu** naprawdę błyszczą:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Rozmiar strony** – w tym przykładzie ustawiony na 3000 × 1000 pikseli; dostosuj do rozmiaru docelowego papieru.  
- **Kolor tła** – `AliceBlue` pokazuje, jak zmienić tło płótna; możesz wybrać dowolny `Color`.  

Te ustawienia są częścią **Aspose HTML Save Options**, które wpływają na ostateczny dokument XPS.

## Konwertuj EPUB do XPS

Na koniec wywołaj konwerter ze strumieniem, skonfigurowanymi opcjami i ścieżką wyjściową:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Gdy ta linia zostanie wykonana, Aspose.HTML odczytuje EPUB, stosuje ustawienia strony i kolor tła, które zdefiniowałeś, i zapisuje w pełni zgodny plik XPS.

## Typowe problemy i wskazówki

- **Nieprawidłowe pomiary strony** – sprawdzić, że parametry są podane w pikselach (lub `Length.fromInches`).
- **Brakujące** – wymagane w EPUB lub zainstaluj je na hoście JVM, aby uzyskać dostęp do końcowego zastąpienia.
- **Duże pliki** – w przypadku bardzo dużego EPUB-ów zwiększ przydział pamięci JVM (`-Xmx`), aby zapobiec `OutOfMemoryError`.

## Wniosek

dodatkowe wykorzystanie **Aspose HTML Save Options** umożliwia precyzyjną kontrolę nad tym, jak EPUB jest renderowany do XPS. Uruchomienie, jak ustawić rozmiar strony, kolor tła i konwersję przy użyciu kilku linii kodu Java. Zintegruj te cechy w swoich potokach przetwarzania wsadowego, aby móc automatyzować zadania publikacyjne.

## Często zadawane pytania

**P: Czym jest Aspose.HTML dla Java?**
O: Do biblioteki Java, która umożliwia programistom tworzenie, edytowanie, renderowanie i konwertowanie dokumentów HTML, EPUB oraz innych dokumentów internetowych bez zastosowań.

**P: Czy można zastosować tego w projekcie komercyjnym?**
O: Tak. Do użytku produkcyjnego jest ważny licencjat. Możesz ją odwiedzić na [stronie zakupu](https://purchase.aspose.com/buy).

**P: Czy dostępna jest wersja próbna?**
O: Oczywiście. Pobierz wersję próbną z [tutaj](https://releases.aspose.com/).

**P: Gdzie mogę uzyskać wsparcie?**
O: Wsparcie społeczności oraz oficjalna pomoc są dostępne na forum Aspose pod adresem [https://forum.aspose.com/](https://forum.aspose.com/).

**P: Jakie są wymagania systemowe?**
O: Java Development Kit (JDK) 8+ oraz system inicjowany wspierany przez środowisko Aspose. zostanie spełniony, że Twoje środowisko spełnia wymagania wstępne.

---

**Aktualizacja Ostatnia:** 2026-01-09
**Testowano z:** Aspose.HTML dla Java 24.12
**Autor:** Asponuj  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}