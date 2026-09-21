---
date: 2026-02-04
description: Dowiedz się, jak tworzyć PDF z HTML, ustawiając niestandardowy arkusz
  stylów użytkownika w Aspose.HTML dla Javy, i łatwo konwertować HTML na PDF za pomocą
  usługi User Agent Service.
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Utwórz PDF z HTML – Ustaw arkusz stylów użytkownika w Aspose.HTML dla Javy
url: /pl/java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz PDF z HTML – Ustaw arkusz stylów użytkownika w Aspose.HTML dla Javy

## Wprowadzenie
W tym samouczku dowiesz się, jak **utworzyć PDF z HTML** przy użyciu Aspose.HTML dla Javy, jednocześnie stosując własny arkusz stylów użytkownika.  
Czy kiedykolwiek chciałeś dostosować wygląd swoich dokumentów HTML własnym, niepowtarzalnym stylem? Wyobraź sobie, że tworzysz stronę internetową i potrzebujesz, aby nagłówki wyróżniały się określonym kolorem, a akapity wyglądały spójnie na różnych urządzeniach. Właśnie tutaj wkraczają *arkusz stylów użytkownika* oraz **User Agent Service**. Przejdziemy przez każdy krok — od napisania prostego pliku HTML, skonfigurowania agenta użytkownika, po ostateczne **konwertowanie HTML do PDF** — abyś mógł od razu zobaczyć rezultat.

## Szybkie odpowiedzi
- **Co oznacza „utworzyć PDF z HTML”?** Oznacza to renderowanie dokumentu HTML (z CSS, obrazami, czcionkami itp.) i zapisanie wizualnego wyniku jako pliku PDF.  
- **Jakiego komponentu Aspose potrzebuję?** Biblioteka Aspose.HTML dla Javy dostarcza silnik konwersji oraz User Agent Service.  
- **Czy potrzebna jest licencja do testów?** Darmowa wersja próbna wystarczy do rozwoju; licencja komercyjna jest wymagana w środowisku produkcyjnym.  
- **Czy mogę używać zewnętrznego pliku CSS?** Tak — możesz podłączać zewnętrzne arkusze stylów tak samo, jak w zwykłej przeglądarce.  
- **Jak długo trwa konwersja?** Dla prostego dokumentu, takiego jak ten w przewodniku, konwersja kończy się w mniej niż sekundę.

## Wymagania wstępne
Przed przystąpieniem do kodu upewnij się, że masz następujące elementy:

1. **Aspose.HTML for Java** – pobierz najnowszy plik JAR z [strony wydań Aspose](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – sprawdź, że `java -version` zwraca wersję 8 lub wyższą.  
3. **IDE** – IntelliJ IDEA, Eclipse lub NetBeans będą w porządku.  
4. **Podstawowa znajomość HTML/CSS** – przydatna, ale nieobowiązkowa.

## Importowanie pakietów
Aby rozpocząć, zaimportuj niezbędne klasy Javy. Jedynym wyraźnym importem potrzebnym w tym przykładzie jest `java.io.IOException`; klasy Aspose są odwoływane później pełnymi nazwami.

```java
import java.io.IOException;
```

## Krok 1: Utwórz prosty dokument HTML
Najpierw napiszmy minimalny plik HTML (`document.html`), który będzie źródłem naszej konwersji do PDF.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Wskazówka:** Trzymaj plik HTML w tym samym katalogu co kod źródłowy Javy, aby uniknąć problemów ze ścieżkami.

## Krok 2: Skonfiguruj Aspose.HTML
Utwórz obiekt `Configuration`. Ten obiekt działa jako kontener dla wszystkich usług (w tym User Agent Service), które będą używane później.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Dlaczego używać usługi User Agent?
**User Agent Service** daje niskopoziomową kontrolę nad opcjami renderowania, takimi jak domyślny zestaw znaków, język, czcionki oraz — co najważniejsze w tym samouczku — własny arkusz stylów użytkownika. Stosując style na tym poziomie, zapewniasz spójny wygląd nawet wtedy, gdy oryginalny HTML nie zawiera własnego CSS.

## Krok 3: Uzyskaj dostęp do usługi User Agent  
**User Agent Service** pozwala wstrzyknąć własny arkusz stylów, ustawić domyślny zestaw znaków i kontrolować inne opcje renderowania.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Krok 4: Zdefiniuj i zastosuj arkusz stylów użytkownika  
Teraz podajemy reguły CSS, które będą stylizować HTML podczas renderowania. To właśnie tutaj **używamy usługi User Agent**, aby ustawić arkusz stylów.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Dlaczego to ważne:** Stosując arkusz stylów na poziomie agenta użytkownika, zapewniasz, że style będą respektowane nawet wtedy, gdy oryginalny HTML nie odwołuje się do pliku CSS.

## Krok 5: Załaduj dokument HTML z niestandardową konfiguracją  
Przekaż zarówno ścieżkę do pliku, jak i instancję `Configuration` do konstruktora `HTMLDocument`. Dzięki temu arkusz stylów użytkownika zostanie powiązany z dokumentem.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Krok 6: Konwertuj HTML do PDF  
Gdy dokument jest w pełni wystylizowany, wywołaj statyczną metodę `convertHTML`, aby **konwertować HTML do PDF**. Obiekt `PdfSaveOptions` pozwala precyzyjnie dostroić wynik (np. rozmiar strony, kompresję).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Wynik:** `user-agent-stylesheet_out.pdf` będzie zawierał nagłówek w brązowym kolorze oraz akapit z tłem GhostWhite, dokładnie tak, jak zdefiniowano w arkuszu stylów.

## Krok 7: Zwolnij zasoby  
Zawsze zwalniaj obiekty Aspose, aby uwolnić pamięć natywną.

```java
if (document != null) {
    document.dispose();
}
if (configuration != null) {
    configuration.dispose();
}
```

## Typowe problemy i rozwiązania
| Problem | Przyczyna | Rozwiązanie |
|-------|-------|-----|
| **Pusty plik PDF** | Nie zastosowano arkusza stylów lub dokument nie został załadowany z konfiguracją. | Upewnij się, że `configuration` jest przekazywany do `HTMLDocument` oraz że `setUserStyleSheet` jest wywoływany przed załadowaniem. |
| **Ostrzeżenie o nieobsługiwanej właściwości CSS** | Aspose.HTML nie obsługuje niektórych zaawansowanych funkcji CSS. | Używaj wyłącznie właściwości CSS wymienionych w dokumentacji Aspose.HTML lub przejdź na prostsze style. |
| **FileNotFoundException** | Nieprawidłowa ścieżka do `document.html`. | Użyj ścieżki bezwzględnej lub umieść plik HTML w katalogu głównym projektu. |

## Najczęściej zadawane pytania

**P: Czy mogę zastosować różne style dla różnych elementów HTML?**  
O: Oczywiście! Możesz zdefiniować dowolną liczbę reguł CSS w arkuszu stylów użytkownika.

**P: Co zrobić, jeśli muszę zmienić arkusz stylów dynamicznie?**  
O: Wywołaj ponownie `setUserStyleSheet` przed utworzeniem nowej instancji `HTMLDocument`; nowe style zostaną zastosowane przy kolejnej konwersji.

**P: Czy można używać zewnętrznych plików CSS z Aspose.HTML dla Javy?**  
O: Tak — możesz zarówno podłączyć zewnętrzny arkusz stylów w HTML, jak i wczytać jego zawartość i przekazać ją do `setUserStyleSheet`.

**P: Jak Aspose.HTML radzi sobie z nieobsługiwanymi właściwościami CSS?**  
O: Nieobsługiwane właściwości są ignorowane, co pozwala reszcie arkusza stylów renderować się bez błędów.

**P: Czy mogę konwertować HTML do formatów innych niż PDF?**  
O: Tak, Aspose.HTML obsługuje konwersję do XPS, TIFF, PNG, JPEG i innych, używając odpowiedniej klasy `SaveOptions`.

## Podsumowanie
Właśnie zobaczyłeś, jak **utworzyć PDF z HTML** ustawiając własny arkusz stylów użytkownika przy pomocy Aspose.HTML dla Javy. Ten przepływ pracy daje pełną kontrolę nad wyglądem generowanego PDF, co czyni go idealnym rozwiązaniem do automatycznego generowania raportów, faktur czy wszelkich scenariuszy, w których spójne stylowanie jest kluczowe. Śmiało eksperymentuj z bardziej złożonym CSS, zewnętrznymi czcionkami lub dodatkowymi formatami konwersji, aby rozbudować tę bazę.

---

**Ostatnia aktualizacja:** 2026-02-04  
**Testowano z:** Aspose.HTML for Java 24.11 (najnowsza w momencie pisania)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}