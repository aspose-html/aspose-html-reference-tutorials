---
date: 2025-12-05
description: Dowiedz się, jak tworzyć pliki PDF z HTML, ustawiając własny arkusz stylów
  użytkownika w Aspose.HTML for Java, i łatwo konwertować HTML na PDF przy użyciu
  usługi User Agent Service.
language: pl
linktitle: Set User Style Sheet in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Utwórz PDF z HTML – Ustaw arkusz stylów użytkownika w Aspose.HTML dla Javy
url: /java/configuring-environment/set-user-style-sheet/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz PDF z HTML – Ustaw arkusz stylów użytkownika w Aspose.HTML dla Javy

## Wprowadzenie
W tym samouczku nauczysz się, jak **utworzyć PDF z HTML** przy użyciu Aspose.HTML dla Javy, stosując własny arkusz stylów użytkownika.  
Czy kiedykolwiek chciałeś dostosować wygląd swoich dokumentów HTML własnym, niepowtarzalnym stylem? Wyobraź sobie, że tworzysz stronę internetową i potrzebujesz, aby nagłówki wyróżniały się określonym kolorem, a akapity wyglądały spójnie na różnych urządzeniach. Właśnie tutaj wchodzą w grę *arkusz stylów użytkownika* oraz **User Agent Service**. Przeprowadzimy Cię przez każdy krok — od napisania prostego pliku HTML, skonfigurowania agenta użytkownika, po ostateczne **konwertowanie HTML do PDF** — abyś mógł od razu zobaczyć rezultat.

## Szybkie odpowiedzi
- **Co oznacza „utworzyć PDF z HTML”?** Oznacza to renderowanie dokumentu HTML (z CSS, obrazami, czcionkami itp.) i zapisanie wizualnego wyniku jako pliku PDF.  
- **Jaki komponent Aspose jest wymagany?** Biblioteka Aspose.HTML dla Javy zapewnia silnik konwersji oraz usługę User Agent Service.  
- **Czy potrzebna jest licencja do testowania?** Darmowa wersja próbna działa w środowisku deweloperskim; licencja komercyjna jest wymagana w produkcji.  
- **Czy mogę użyć zewnętrznego pliku CSS?** Tak – możesz podłączyć zewnętrzne arkusze stylów tak jak w zwykłej przeglądarce.  
- **Jak długo trwa konwersja?** Dla prostego dokumentu, takiego jak w tym przewodniku, konwersja kończy się w mniej niż sekundę.

## Wymagania wstępne
Zanim przejdziesz do kodu, upewnij się, że masz następujące elementy:

1. **Aspose.HTML for Java** – pobierz najnowszy plik JAR ze [strony wydań Aspose](https://releases.aspose.com/html/java/).  
2. **Java Development Kit (JDK) 8+** – upewnij się, że `java -version` zwraca 8 lub wyższą wersję.  
3. **IDE** – IntelliJ IDEA, Eclipse lub NetBeans będą działać bez problemu.  
4. **Podstawowa znajomość HTML/CSS** – przydatna, ale nie obowiązkowa.

## Importowanie pakietów
Aby rozpocząć, zaimportuj niezbędne klasy Javy. Jedyny wyraźny import potrzebny w tym przykładzie to `java.io.IOException`; klasy Aspose są odwoływane później w pełnych nazwach kwalifikowanych.

```java
import java.io.IOException;
```

## Krok 1: Utwórz prosty dokument HTML
Najpierw napiszemy minimalny plik HTML (`document.html`), który posłuży jako źródło do konwersji PDF.

```java
String code = "<h1>User Agent Service</h1>\r\n" +
        "<p>The User Agent Service allows you to specify a custom user stylesheet, a primary character set for the document, language, and fonts settings.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Porada:** Trzymaj plik HTML w tym samym katalogu co kod źródłowy Javy, aby uniknąć problemów związanych ze ścieżkami.

## Krok 2: Skonfiguruj Aspose.HTML
Utwórz obiekt `Configuration`. Obiekt ten działa jako kontener dla wszystkich usług (w tym User Agent Service), które będą używane później.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Krok 3: Uzyskaj dostęp do User Agent Service  
**User Agent Service** pozwala wstrzyknąć własny arkusz stylów, ustawić domyślny zestaw znaków i kontrolować inne opcje renderowania.

```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

## Krok 4: Zdefiniuj i zastosuj arkusz stylów użytkownika  
Teraz podajemy reguły CSS, które będą stylizować HTML podczas renderowania. To tutaj **używamy usługi User Agent** do ustawienia arkusza stylów.

```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; font-size:2em; }\r\n" +
        "p { background-color:GhostWhite; color:SlateGrey; font-size:1.2em; }\r\n");
```

> **Dlaczego to ważne:** Stosując arkusz stylów na poziomie agenta użytkownika, zapewniasz, że style będą respektowane nawet wtedy, gdy oryginalny HTML nie odwołuje się do pliku CSS.

## Krok 5: Załaduj dokument HTML z niestandardową konfiguracją  
Przekaż zarówno ścieżkę do pliku, jak i instancję `Configuration` do konstruktora `HTMLDocument`. To powiąże arkusz stylów użytkownika z dokumentem.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
```

## Krok 6: Konwertuj HTML do PDF  
Gdy dokument jest w pełni wystylowany, wywołaj statyczną metodę `convertHTML`, aby **konwertować HTML do PDF**. Obiekt `PdfSaveOptions` pozwala dopasować wyjście (np. rozmiar strony, kompresję).

```java
com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.PdfSaveOptions(),
        "user-agent-stylesheet_out.pdf"
);
```

> **Wynik:** `user-agent-stylesheet_out.pdf` będzie zawierał nagłówek w kolorze brązowym oraz akapit z tłem GhostWhite, dokładnie tak, jak zdefiniowano w arkuszu stylów.

## Krok 7: Oczyść zasoby  
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
| **Blank PDF output** | Nie zastosowano arkusza stylów lub dokument nie został załadowany z konfiguracją. | Zweryfikuj, czy `configuration` jest przekazywany do `HTMLDocument` oraz czy `setUserStyleSheet` jest wywoływany przed ładowaniem. |
| **Unsupported CSS property warning** | Aspose.HTML nie obsługuje niektórych zaawansowanych właściwości CSS. | Używaj wyłącznie właściwości CSS wymienionych w dokumentacji Aspose.HTML lub przejdź na prostsze style. |
| **FileNotFoundException** | Nieprawidłowa ścieżka do `document.html`. | Użyj ścieżki bezwzględnej lub umieść plik HTML w katalogu głównym projektu. |

## Najczęściej zadawane pytania

**Q: Czy mogę zastosować różne style dla różnych elementów HTML?**  
A: Oczywiście! Możesz zdefiniować dowolną liczbę reguł CSS w arkuszu stylów użytkownika.

**Q: Co zrobić, jeśli muszę zmienić arkusz stylów dynamicznie?**  
A: Wywołaj ponownie `setUserStyleSheet` przed utworzeniem nowej instancji `HTMLDocument`; nowe style zostaną zastosowane przy kolejnej konwersji.

**Q: Czy można używać zewnętrznych plików CSS z Aspose.HTML dla Javy?**  
A: Tak – możesz albo podłączyć zewnętrzny arkusz stylów w HTML, albo wczytać jego zawartość i przekazać do `setUserStyleSheet`.

**Q: Jak Aspose.HTML radzi sobie z nieobsługiwanymi właściwościami CSS?**  
A: Nieobsługiwane właściwości są ignorowane, co pozwala reszcie arkusza stylów renderować się bez błędów.

**Q: Czy mogę konwertować HTML do formatów innych niż PDF?**  
A: Tak, Aspose.HTML obsługuje konwersję do XPS, TIFF, PNG, JPEG i innych przy użyciu odpowiedniej klasy `SaveOptions`.

## Podsumowanie
Widzisz już, jak **utworzyć PDF z HTML** ustawiając własny arkusz stylów użytkownika w Aspose.HTML dla Javy. Ten przepływ pracy daje pełną kontrolę nad wyglądem generowanego PDF, co czyni go idealnym rozwiązaniem do automatycznego generowania raportów, faktur lub wszelkich scenariuszy, w których spójne formatowanie jest kluczowe. Śmiało eksperymentuj z bardziej złożonym CSS, zewnętrznymi czcionkami lub dodatkowymi formatami konwersji, aby rozbudować tę bazę.

---

**Last Updated:** 2025-12-05  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}