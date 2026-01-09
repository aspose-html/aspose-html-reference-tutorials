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

# Określanie opcji zapisu Aspose HTML dla EPUB do XPS

Konwersja dokumentu EPUB do XPS może być przydatnym elementem procesu publikacji, a **Aspose HTML Save Options** zapewniają precyzyjną kontrolę nad wynikiem. W tym samouczku przeprowadzimy dokładne kroki potrzebne do skonfigurowania tych opcji zapisu przy użyciu Aspose.HTML dla Javy i wygenerowania wysokiej jakości pliku XPS.

## Quick Answers
- **Co robią Aspose HTML Save Options?** Pozwalają dostosować rozmiar strony, kolor tła i inne ustawienia renderowania podczas zapisywania do formatów takich jak XPS.  
- **Jakiej biblioteki wymaga?** Aspose.HTML for Java (najnowsza wersja).  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna wystarcza do oceny; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Czy mogę zmienić wymiary strony?** Tak – można ustawić dowolną szerokość i wysokość za pomocą `PageSetup`.  
- **Czy konwersja jest szybka?** Dla typowych plików EPUB konwersja kończy się w ciągu kilku sekund na nowoczesnej maszynie JVM.

## What Are Aspose HTML Save Options?
Aspose HTML Save Options to zestaw właściwości, które kontrolują sposób renderowania i zapisywania dokumentów HTML, EPUB lub innych dokumentów internetowych do docelowego formatu, takiego jak XPS, PDF lub pliki graficzne. Pozwalają definiować układ strony, kolory tła, marginesy i inne elementy, zapewniając, że powstały plik spełnia wymagania projektowe.

## Why Use Aspose.HTML for Java to Convert EPUB to XPS?
- **Wysoka wierność** – zachowuje skomplikowane układy, czcionki i grafikę wektorową.  
- **Programowa kontrola** – automatyzuj konwersje wsadowe w aplikacjach Java.  
- **Brak zewnętrznych zależności** – czysta biblioteka Java, bez komponentów natywnych.  
- **Dostosowywalny wynik** – dzięki opcjom zapisu możesz dopasować XPS dokładnie do swoich potrzeb.

## Prerequisites

Zanim przejdziemy do kodu, upewnij się, że masz następujące elementy:

1. **Środowisko programistyczne Java** – zainstalowany JDK 8 lub nowszy.  
2. **Biblioteka Aspose.HTML for Java** – pobierz ją z [linku do pobrania](https://releases.aspose.com/html/java/).  
3. **Plik EPUB** – źródłowy plik EPUB, który chcesz przekonwertować.  

Posiadanie ich przygotowanych pozwoli Ci przejść przez kroki bez przerw.

## Import Packages

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

Te importy dają dostęp do silnika konwersji oraz **Aspose HTML Save Options** potrzebnych do precyzyjnego dostosowania.

## Open the EPUB File

Następnie otwórz plik EPUB, który chcesz przekonwertować. Pomocnik `Resources.input` ładuje plik z folderu zasobów demonstracyjnych:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Użycie bloku try‑with‑resources zapewnia automatyczne zamknięcie strumienia.

## Create XPS Save Options (Configure Page Size & Background)

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

## Convert EPUB to XPS

Na koniec wywołaj konwerter ze strumieniem, skonfigurowanymi opcjami i ścieżką wyjściową:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Gdy ta linia zostanie wykonana, Aspose.HTML odczytuje EPUB, stosuje ustawienia strony i kolor tła, które zdefiniowałeś, i zapisuje w pełni zgodny plik XPS.

## Common Issues & Tips

- **Nieprawidłowe wymiary strony** – upewnij się, że wymiary są podane w pikselach (lub użyj `Length.fromInches`).  
- **Brakujące czcionki** – osadź wymagane czcionki w EPUB lub zainstaluj je na hoście JVM, aby uniknąć domyślnego zastąpienia.  
- **Duże pliki** – w przypadku bardzo dużych EPUB-ów zwiększ przydział pamięci JVM (`-Xmx`), aby zapobiec `OutOfMemoryError`.  

## Conclusion

Poprzez wykorzystanie **Aspose HTML Save Options** uzyskasz precyzyjną kontrolę nad tym, jak EPUB jest renderowany do XPS. Powyższe kroki pokazują, jak ustawić rozmiar strony, kolor tła i wykonać konwersję przy użyciu kilku linii kodu Java. Zintegruj ten wzorzec w swoich potokach przetwarzania wsadowego, aby efektywnie automatyzować zadania publikacyjne.

## Frequently Asked Questions

**P: Czym jest Aspose.HTML for Java?**  
O: To biblioteka Java, która umożliwia programistom tworzenie, edytowanie, renderowanie i konwertowanie dokumentów HTML, EPUB oraz innych dokumentów internetowych bez potrzeby przeglądarki.

**P: Czy mogę używać tego w projekcie komercyjnym?**  
O: Tak. Do użytku produkcyjnego potrzebna jest ważna licencja. Możesz ją zakupić na [stronie zakupu](https://purchase.aspose.com/buy).

**P: Czy dostępna jest darmowa wersja próbna?**  
O: Oczywiście. Pobierz wersję próbną z [tutaj](https://releases.aspose.com/).

**P: Gdzie mogę uzyskać wsparcie?**  
O: Wsparcie społeczności oraz oficjalna pomoc są dostępne na forum Aspose pod adresem [https://forum.aspose.com/](https://forum.aspose.com/).

**P: Jakie są wymagania systemowe?**  
O: Java Development Kit (JDK) 8+ oraz system operacyjny wspierany przez środowisko Aspose. Upewnij się, że Twoje środowisko spełnia wcześniej wymienione wymagania wstępne.

---

**Ostatnia aktualizacja:** 2026-01-09  
**Testowano z:** Aspose.HTML for Java 24.12  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}