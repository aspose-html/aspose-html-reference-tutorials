---
date: 2026-02-04
description: Dowiedz się, jak używać Aspose.HTML do konfigurowania czcionek, stosowania
  własnego CSS, używania tymczasowej licencji oraz generowania PDF z HTML w Javie.
linktitle: Configure Fonts in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Jak używać Aspose.HTML do konfigurowania czcionek w konwersji HTML‑do‑PDF w
  Javie
url: /pl/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konfiguracja czcionek dla HTML‑to‑PDF w Javie z Aspose.HTML

## Wprowadzenie
W tym samouczku odkryjesz **how to use Aspose.HTML**, aby skonfigurować czcionki dla konwersji HTML‑to‑PDF w Javie. Pracując z dokumentami HTML, ustawienie odpowiednich czcionek zapewnia, że wygenerowany PDF wygląda dokładnie tak jak oryginalna strona internetowa — zachowując kolory marki, typografię i układ. Niezależnie od tego, czy tworzysz raporty, faktury, czy jakikolwiek pipeline generowania dokumentów, właściwa konfiguracja czcionek jest kluczem do profesjonalnie wyglądających PDF‑ów. Przejdźmy przez cały proces, od przygotowania środowiska po konwersję HTML do PDF z własnymi czcionkami i CSS.

## Szybkie odpowiedzi
- **Jaki jest główny cel tego samouczka?** Skonfigurować czcionki dla konwersji HTML‑to‑PDF w Javie przy użyciu Aspose.HTML.  
- **Która biblioteka obsługuje konwersję?** Aspose.HTML for Java (klasa `Converter`).  
- **Czy potrzebna jest licencja?** Tymczasowa licencja Aspose usuwa ograniczenia wersji ewaluacyjnej; pełna licencja jest wymagana w środowisku produkcyjnym.  
- **Gdzie powinny znajdować się moje własne czcionki?** W folderze wskazywanym przez `FontsLookupFolder`, np. w katalogu `fonts` obok projektu.  
- **Czy mogę dostosować wyjście PDF?** Tak — użyj `PdfSaveOptions`, aby dostosować rozmiar strony, marginesy i inne ustawienia.

## Jak używać Aspose.HTML do konfiguracji czcionek
Poniżej wyjaśnimy, dlaczego obsługa czcionek ma znaczenie, jak zastosować własny CSS oraz jak **use temporary license**, aby odblokować pełną funkcjonalność podczas testowania rozwiązania.

## Wymagania wstępne
Zanim zaczniemy, upewnij się, że masz następujące elementy:

1. **Java Development Kit (JDK) 1.8+** – kod działa na dowolnym nowoczesnym JDK.  
2. **Aspose.HTML for Java** – pobierz najnowszy plik JAR z [Aspose website](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse lub dowolny edytor kompatybilny z Javą.  
4. **Podstawowa znajomość Javy** – powinieneś być zaznajomiony z klasami, metodami i operacjami I/O.  
5. **Licencja Aspose.HTML** – [temporary license](https://purchase.aspose.com/temporary-license/) usunie ograniczenia wersji ewaluacyjnej.

## Importowanie pakietów
Najpierw zaimportuj podstawowe klasy Javy i Aspose.HTML, które będą potrzebne.  

```java
import java.io.IOException;
```

Te importy dają dostęp do obsługi plików oraz API Aspose.HTML.

## Czym jest **html to pdf java** i dlaczego konfiguracja czcionek ma znaczenie?
Proces **html to pdf java** renderuje dokument HTML na stronę PDF. Czcionki są kluczowym elementem renderowania, ponieważ wpływają na układ, odstępy między wierszami i wierność wizualną. Wskazując Aspose.HTML na własny folder czcionek, zapewniasz, że PDF użyje dokładnie tych krojów, które zaprojektowałeś dla strony internetowej, eliminując czcionki zapasowe i zachowując spójność marki.

## Przewodnik krok po kroku

### Krok 1: Utwórz zawartość HTML
Zaczniemy od wygenerowania prostego pliku HTML, który później przekonwertujemy na PDF.

#### 1.1 Napisz kod HTML
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

Ten fragment definiuje nagłówek i akapit. Śmiało rozbuduj HTML o dodatkowe elementy, jeśli chcesz przetestować dodatkowe style.

#### 1.2 Zapisz HTML do pliku
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

`FileWriter` zapisuje łańcuch znaków do pliku `user-agent-fontsetting.html` w katalogu projektu. Po tym kroku będziesz mieć fizyczny plik HTML gotowy do przetworzenia.

### Krok 2: Skonfiguruj środowisko Aspose.HTML
Teraz skonfigurujemy obiekt `Configuration` Aspose.HTML, który pozwala kontrolować sposób renderowania HTML.

#### 2.1 Utwórz instancję Configuration
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

Obiekt `Configuration` jest punktem wejścia do dostosowywania opcji renderowania, takich jak obsługa czcionek i zachowanie agenta użytkownika.

#### 2.2 Uzyskaj dostęp do usługi User Agent
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

`IUserAgentService` zarządza arkuszami stylów, czcionkami i innymi szczegółami renderowania. Użyjemy go, aby wstrzyknąć własny CSS i wskazać folder czcionek.

### Krok 3: Zastosuj własne style i czcionki
Po przygotowaniu środowiska możemy dodać reguły CSS oraz poinformować Aspose.HTML, gdzie znajdują się nasze czcionki.

#### 3.1 Ustaw własny CSS
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

Ten CSS koloruje nagłówek na brązowo, a akapit na szaro. Możesz dodać dowolne prawidłowe reguły CSS — Aspose.HTML obsługuje pełną specyfikację CSS2.1 oraz wiele funkcji CSS3. *(To jest przykład **apply custom css**.)*

#### 3.2 Wskaż folder z własnymi czcionkami
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

Umieść dowolne pliki `.ttf` lub `.otf`, które chcesz używać, w folderze o nazwie `fonts` znajdującym się w katalogu głównym projektu. Aspose.HTML automatycznie załaduje te czcionki podczas renderowania.

> **Pro tip:** Jeśli masz wiele rodzin czcionek, uporządkuj je w podfolderach i dodaj każdy folder nadrzędny do `FontsLookupFolder` używając listy oddzielonej średnikami.

### Krok 4: Załaduj dokument HTML z konfiguracją
Teraz wczytujemy wcześniej utworzony plik HTML, stosując skonfigurowane ustawienia.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

Obiekt `HTMLDocument` reprezentuje teraz stylizowany HTML gotowy do konwersji.

### Krok 5: Konwertuj HTML do PDF
Na koniec wykonujemy **aspose html pdf conversion**, aby uzyskać plik PDF, który respektuje nasze własne czcionki i style.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

Obiekt `PdfSaveOptions` pozwala dostosować ustawienia wyjściowe, takie jak rozmiar strony, kompresja i metadane. Dla podstawowej konwersji domyślne opcje działają perfekcyjnie.

### Krok 6: Oczyść zasoby
Właściwe zwalnianie zasobów zapobiega wyciekom pamięci, szczególnie przy przetwarzaniu wielu dokumentów w długotrwałej aplikacji.

#### 6.1 Zwolnij HTMLDocument
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 Zwolnij Configuration
```java
if (configuration != null) {
    configuration.dispose();
}
```

Te wywołania zwalniają natywne zasoby przydzielone przez Aspose.HTML.

## Częste problemy i rozwiązania
| Problem | Rozwiązanie |
|-------|----------|
| **Fonts not showing** | Zweryfikuj, czy folder `fonts` jest poprawnie wskazany i zawiera prawidłowe pliki `.ttf`/`.otf`. Użyj ścieżek bezwzględnych, jeśli folder znajduje się poza katalogiem projektu. |
| **PDF looks blank** | Upewnij się, że ścieżka do pliku HTML jest prawidłowa i plik jest czytelny. Sprawdź, czy obiekt `Configuration` został przekazany do konstruktora `HTMLDocument`. |
| **License exception** | Zastosuj tymczasową lub pełną licencję Aspose przed wywołaniem jakichkolwiek API Aspose. Umieść plik licencji w classpath i załaduj go za pomocą `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`. |
| **Unexpected CSS rendering** | Aspose.HTML obsługuje większość CSS, ale nie wszystkie nowoczesne funkcje (np. CSS Grid). Uprość style lub użyj obsługiwanych właściwości CSS. |

## Najczęściej zadawane pytania

**Q: Czy mogę używać dowolnej czcionki z Aspose.HTML dla Javy?**  
A: Tak, każda czcionka TrueType (`.ttf`) lub OpenType (`.otf`), którą obsługuje Twój system operacyjny, może być użyta. Po prostu umieść pliki w folderze określonym w `FontsLookupFolder`.

**Q: Czy potrzebna jest licencja do używania Aspose.HTML dla Javy?**  
A: Choć możesz ocenić bibliotekę bez licencji, [temporary Aspose license](https://purchase.aspose.com/temporary-license/) usuwa ograniczenia wersji ewaluacyjnej. W środowisku produkcyjnym wymagana jest pełna licencja.

**Q: Jak mogę dostosować wyjście PDF?**  
A: Przekaż skonfigurowany obiekt `PdfSaveOptions` do `convertHTML`. Możesz ustawić rozmiar strony, marginesy, poziom kompresji i inne opcje.

**Q: Czy można zastosować bardziej złożone style CSS?**  
A: Tak, Aspose.HTML obsługuje szeroki zakres CSS. Złożone selektory, media queries i pseudo‑klasy działają tak, jak w przeglądarce, choć niektóre bardzo nowe funkcje CSS3/4 mogą nie być w pełni wspierane.

**Q: Gdzie mogę znaleźć więcej przykładów i dokumentacji?**  
A: Odwiedź oficjalną [Aspose.HTML for Java documentation page](https://reference.aspose.com/html/java/) po szczegółowe odniesienia API i dodatkowe przykłady kodu.

**Q: Jak tymczasowa licencja Aspose wpływa na konwersję?**  
A: Tymczasowa licencja usuwa limit 10 stron oraz znak wodny pojawiający się w trybie ewaluacyjnym, umożliwiając pełne przetestowanie workflow **aspose html pdf conversion**.

**Ostatnia aktualizacja:** 2026-02-04  
**Testowano z:** Aspose.HTML for Java 24.12 (najnowsza w momencie pisania)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}