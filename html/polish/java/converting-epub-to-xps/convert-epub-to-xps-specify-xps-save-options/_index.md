---
date: 2026-03-29
description: Dowiedz się, jak używać Aspose.HTML dla Java, aby określić opcje zapisu
  XPS, konwertować EPUB na XPS i obsługiwać licencjonowanie.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Jak korzystać z opcji zapisu Aspose HTML dla EPUB do XPS
url: /pl/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać opcji zapisu Aspose HTML dla EPUB do XPS

W tym przewodniku pokażemy **jak używać Aspose** HTML Save Options, aby przekonwertować dokument EPUB do XPS z pełną kontrolą nad wymiarami strony, kolorem tła i kwestiami licencyjnymi. Niezależnie od tego, czy budujesz potok przetwarzania wsadowego, czy jednorazowe narzędzie konwersji, te kroki pomogą Ci szybko uzyskać niezawodne wyniki.

## Szybkie odpowiedzi
- **Co robi Aspose HTML Save Options?** Umożliwia dostosowanie rozmiaru strony, koloru tła i innych ustawień renderowania przy zapisywaniu do formatów takich jak XPS.  
- **Która biblioteka jest wymagana?** Aspose.HTML for Java (latest version).  
- **Czy potrzebuję licencji?** Darmowa wersja próbna działa w celach oceny; licencja komercyjna jest wymagana w produkcji.  
- **Czy mogę zmienić wymiary strony?** Tak – możesz ustawić dowolną szerokość i wysokość za pomocą `PageSetup`.  
- **Czy konwersja jest szybka?** Dla typowych plików EPUB konwersja kończy się w ciągu kilku sekund na nowoczesnej maszynie JVM.

## Co oznacza „how to use aspose” w tym kontekście?
Wyrażenie **how to use Aspose** odnosi się do praktycznych kroków wykorzystania biblioteki Aspose.HTML do manipulacji i konwersji dokumentów internetowych. W tym samouczku koncentrujemy się na **aspose html save options**, które pozwalają precyzyjnie dostroić wynik przy **konwersji EPUB do XPS**.

## Dlaczego używać Aspose.HTML dla Java do konwersji EPUB do XPS?
- **Wysoka wierność** – zachowuje skomplikowane układy, czcionki i grafikę wektorową.  
- **Programowa kontrola** – automatyzuj konwersje wsadowe w aplikacjach Java.  
- **Brak zewnętrznych zależności** – czysta biblioteka Java, bez komponentów natywnych.  
- **Dostosowywalny wynik** – dzięki opcjom zapisu możesz dopasować XPS do swoich dokładnych potrzeb, np. **określić wymiary strony** lub ustawić własne tło.  

## Wymagania wstępne

Zanim przejdziemy do kodu, upewnij się, że masz następujące:

1. **Środowisko programistyczne Java** – zainstalowany JDK 8 lub nowszy.  
2. **Biblioteka Aspose.HTML for Java** – pobierz ją z [download link](https://releases.aspose.com/html/java/).  
3. **Plik EPUB** – źródłowy plik EPUB, który chcesz **convert EPUB to XPS**.  

Posiadanie ich gotowych pozwoli Ci podążać za krokami bez przerw.

## Importowanie pakietów

Najpierw zaimportuj wymagane klasy. Umieść importy na początku swojego pliku źródłowego Java:

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

Te importy dają dostęp do silnika konwersji oraz **Aspose HTML Save Options** potrzebnych do precyzyjnego dostrajania.

## Otwórz plik EPUB

Następnie otwórz plik EPUB, który chcesz przekonwertować. Pomocnicza metoda `Resources.input` ładuje plik z folderu zasobów demo:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Użycie bloku try‑with‑resources zapewnia automatyczne zamknięcie strumienia.

## Utwórz XPS Save Options (konfiguracja rozmiaru strony i tła)

Teraz tworzymy instancję `XpsSaveOptions` i dostosowujemy ją. To miejsce, w którym **save options** naprawdę błyszczą:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Rozmiar strony** – ustawiony na 3000 × 1000 pikseli w tym przykładzie; dostosuj do docelowego rozmiaru papieru lub użyj `Length.fromInches`, aby **specify page dimensions** w calach.  
- **Kolor tła** – `AliceBlue` pokazuje, jak zmienić tło płótna; możesz wybrać dowolny `Color`.  

Te ustawienia są częścią **aspose html save options**, które wpływają na ostateczny dokument XPS.

## Konwertuj EPUB do XPS

Na koniec wywołaj konwerter z strumieniem, skonfigurowanymi opcjami i ścieżką wyjściową:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Gdy ta linia zostanie wykonana, Aspose.HTML odczytuje EPUB, stosuje ustawienia strony i kolor tła, które zdefiniowałeś, i zapisuje w pełni zgodny plik XPS.

## Typowe problemy i wskazówki

- **Nieprawidłowe wymiary strony** – upewnij się, że wymiary są podane w pikselach (lub użyj `Length.fromInches`).  
- **Brakujące czcionki** – osadź wymagane czcionki w EPUB lub zainstaluj je na hoście JVM, aby uniknąć domyślnego zastąpienia.  
- **Duże pliki** – w przypadku bardzo dużych EPUB-ów zwiększ przydział pamięci JVM (`-Xmx`), aby zapobiec `OutOfMemoryError`.  
- **Licencjonowanie Aspose HTML** – upewnij się, że przed konwersją wczytano ważną licencję; w przeciwnym razie pojawi się znak wodny wersji próbnej.

## Zakończenie

Korzystając z **Aspose HTML Save Options**, uzyskasz precyzyjną kontrolę nad tym, jak EPUB jest renderowany do XPS. Powyższe kroki pokazują, jak **how to convert EPUB**, ustawić **page dimensions**, zmienić tło i wykonać konwersję przy użyciu kilku linii kodu Java. Zintegruj ten wzorzec w swoich potokach przetwarzania wsadowego, aby efektywnie automatyzować zadania publikacyjne.

## Najczęściej zadawane pytania

**Q: Czym jest Aspose.HTML for Java?**  
A: To biblioteka Java, która umożliwia programistom tworzenie, edytowanie, renderowanie i konwertowanie HTML, EPUB oraz innych dokumentów internetowych bez potrzeby przeglądarki.

**Q: Czy mogę używać tego w projekcie komercyjnym?**  
A: Tak. Do użytku produkcyjnego potrzebna jest ważna licencja. Możesz ją kupić na [purchase page](https://purchase.aspose.com/buy).

**Q: Czy dostępna jest darmowa wersja próbna?**  
A: Oczywiście. Pobierz wersję próbną z [here](https://releases.aspose.com/).

**Q: Gdzie mogę uzyskać wsparcie?**  
A: Wsparcie społeczności oraz oficjalna pomoc są dostępne na forach Aspose pod adresem [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: Jakie są wymagania systemowe?**  
A: Java Development Kit (JDK) 8+ oraz system operacyjny wspierany przez środowisko Aspose. Upewnij się, że Twoje środowisko spełnia wymienione wcześniej wymagania wstępne.

---

**Ostatnia aktualizacja:** 2026-03-29  
**Testowano z:** Aspose.HTML for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}