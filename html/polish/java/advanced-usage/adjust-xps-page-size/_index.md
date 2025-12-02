---
date: 2025-11-29
description: Dowiedz się, jak konwertować HTML do XPS i dostosowywać rozmiar strony
  XPS przy użyciu Aspose.HTML dla Javy. Łatwo kontroluj wymiary wyjściowe.
language: pl
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Konwertuj HTML do XPS i dostosuj rozmiar strony XPS przy użyciu Aspose.HTML
  dla Javy
url: /java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konwertowanie HTML do XPS i dostosowywanie rozmiaru strony XPS przy użyciu Aspose.HTML dla Java

W tym samouczku dowiesz się **jak konwertować HTML do XPS** i precyzyjnie dostosować rozmiar otrzymanej strony przy użyciu Aspose.HTML dla Java. Niezależnie od tego, czy generujesz raporty do druku, faktury czy dokumenty archiwalne, kontrola wymiarów XPS zapewnia, że wynik wygląda dokładnie tak, jak tego oczekujesz. Przeprowadzimy Cię przez każdy krok — od konfiguracji środowiska po renderowanie końcowego pliku XPS — abyś mógł od razu zintegrować tę funkcję w swoich aplikacjach Java.

## Szybkie odpowiedzi
- **Co oznacza „konwertowanie HTML do XPS”?** Renderuje dokument HTML do pliku XPS, zachowując układ i stylizację.  
- **Czy potrzebna jest licencja?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.  
- **Jaką wersję Javy obsługuje?** Java 8 lub wyższą (zalecany JDK 11+).  
- **Czy mogę zmienić rozmiar strony?** Tak — Aspose.HTML pozwala określić własne wymiary przed renderowaniem.  
- **Jak długo trwa konwersja?** Zazwyczaj poniżej sekundy dla standardowych stron; większe dokumenty mogą zająć więcej czasu.

## Co to jest konwertowanie HTML do XPS?
Konwertowanie HTML do XPS oznacza przekształcenie pliku znaczników przeznaczonego dla sieci w dokument XPS (XML Paper Specification) — format o stałym układzie, gotowy do druku, podobny do PDF. Jest to przydatne, gdy potrzebujesz dokumentów wysokiej jakości, niezależnych od urządzenia, do archiwizacji lub drukowania z aplikacji Java.

## Dlaczego warto dostosować rozmiar strony XPS?
Dostosowanie rozmiaru strony daje kontrolę nad fizycznymi wymiarami końcowego dokumentu (np. A4, Letter, własne etykiety). Zapobiega niepożądanemu skalowaniu, zapewnia idealne dopasowanie treści i może zmniejszyć rozmiar pliku poprzez usunięcie niepotrzebnej białej przestrzeni.

## Wymagania wstępne

Zanim zaczniemy, upewnij się, że spełnione są następujące wymagania:

1. **Środowisko programistyczne Java** – zainstalowany Java Development Kit (JDK) na Twoim systemie.  
2. **Biblioteka Aspose.HTML for Java** – pobierz i dołącz bibliotekę Aspose.HTML for Java do swojego projektu. Bibliotekę znajdziesz [tutaj](https://releases.aspose.com/html/java/).  
3. **Plik HTML wejściowy** – przygotuj plik HTML, który chcesz wyrenderować i dostosować rozmiar strony XPS. Możesz użyć własnego pliku HTML w tym samouczku.

## Importowanie pakietów

Najpierw zaimportuj klasy, których będziesz potrzebować. Pakiety te zapewniają dostęp do obsługi dokumentów, renderowania i funkcji konfigurowania stron.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Krok 1: Ustaw nazwę pliku wejściowego

Odczytaj źródłowy plik HTML przy użyciu `FileInputStream`. Ten strumień dostarcza surowy HTML do silnika Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Krok 2: Utwórz dokument HTML i ustaw style

Utwórz instancję `HTMLDocument`, która reprezentuje treść do renderowania. W tym przykładzie wstrzykujemy mały blok CSS, aby pokazać stylizację — możesz go zamienić na własny znacznik.

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

## Krok 3: Utwórz opcje renderowania XPS

Zainicjuj `XpsRenderingOptions`, aby przechowywać wszystkie ustawienia wpływające na konwersję z HTML do XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Krok 4: Dostosuj rozmiar strony

Zdefiniuj własny rozmiar strony (szerokość × wysokość w punktach) i określ renderującemu, czy ma automatycznie rozszerzać się do najszerszej strony. Ustawienie `adjustToWidestPage` na `false` zachowuje dokładne wymiary, które podasz.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Krok 5: Renderuj wynik

Na koniec utwórz `XpsDevice` z skonfigurowanymi opcjami i wyrenderuj dokument HTML. Wynikiem jest w pełni sformatowany plik XPS z niestandardowymi wymiarami strony, które ustawiłeś.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Typowe problemy i rozwiązania

| Problem | Dlaczego się pojawia | Rozwiązanie |
|---------|----------------------|-------------|
| **Pusty wynik XPS** | Strumień wejściowy nie został zamknięty lub HTMLDocument wskazuje niewłaściwy plik. | Upewnij się, że `FileInputStream` jest prawidłowo zamknięty w bloku try‑with‑resources i ścieżka do pliku jest poprawna. |
| **Rozmiar strony nie zastosowany** | `adjustToWidestPage` pozostawiono jako `true`. | Ustaw `pageSetup.setAdjustToWidestPage(false);` jak pokazano w Kroku 4. |
| **Nieobsługiwany CSS** | Aspose.HTML obsługuje podzbiór CSS. | Używaj podstawowego układu, czcionek i kolorów; unikaj zaawansowanych selektorów lub CSS Grid. |
| **LicenseException** | Uruchamianie bez ważnej licencji w środowisku produkcyjnym. | Zastosuj tymczasową lub zakupioną licencję przed renderowaniem (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Najczęściej zadawane pytania

**Q: Czym jest Aspose.HTML for Java?**  
A: Aspose.HTML for Java to biblioteka Java, która umożliwia programistom manipulowanie i konwertowanie dokumentów HTML do różnych formatów, takich jak XPS, PDF i obrazy.

**Q: Gdzie mogę pobrać Aspose.HTML for Java?**  
A: Bibliotekę Aspose.HTML for Java możesz pobrać z [tego linku](https://releases.aspose.com/html/java/).

**Q: Czy dostępna jest darmowa wersja próbna Aspose.HTML for Java?**  
A: Tak, darmową wersję próbną Aspose.HTML for Java możesz uzyskać [tutaj](https://releases.aspose.com/).

**Q: Jak mogę uzyskać tymczasową licencję dla Aspose.HTML for Java?**  
A: Aby uzyskać tymczasową licencję dla Aspose.HTML for Java, odwiedź [tą stronę](https://purchase.aspose.com/temporary-license/).

**Q: Czy mogę uzyskać wsparcie dla Aspose.HTML for Java?**  
A: Tak, pomoc i wsparcie możesz uzyskać od społeczności Aspose na [forum Aspose](https://forum.aspose.com/).

**Q: Czy mogę konwertować HTML do XPS na serwerze bez interfejsu graficznego?**  
A: Oczywiście. Aspose.HTML działa w środowiskach bez GUI; wystarczy, że środowisko uruchomieniowe Java jest prawidłowo skonfigurowane.

**Q: Czy biblioteka obsługuje własne marginesy strony?**  
A: Tak. Użyj `PageSetup.setMarginTop()`, `setMarginBottom()` itd., przed przypisaniem `PageSetup` do opcji renderowania.

## Podsumowanie

Przeszliśmy cały proces **konwertowania HTML do XPS** i dostosowywania rozmiaru strony przy użyciu Aspose.HTML for Java. Postępując zgodnie z tymi krokami, możesz generować gotowe do druku dokumenty XPS, które spełniają dokładne wymagania układu. Śmiało eksperymentuj z różnymi wymiarami stron, stylami lub nawet dodawaj nagłówki i stopki, aby dopasować je do potrzeb projektu.

Jeśli masz pyt lub potrzebujesz dalszej pomocy, zapoznaj się z [dokumentacją Aspose.HTML for Java](https://reference.aspose.com/html/java/) lub dołącz do dyskusji na [forum Aspose](https://forum.aspose.com/).

---

**Ostatnia aktualizacja:** 2025-11-29  
**Testowano z:** Aspose.HTML for Java 11 (najnowsza w momencie pisania)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}