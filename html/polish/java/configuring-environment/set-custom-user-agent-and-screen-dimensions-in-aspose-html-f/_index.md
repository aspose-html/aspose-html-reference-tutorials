---
category: general
date: 2026-09-29
description: Ustaw niestandardowy agent użytkownika w Aspose.HTML dla Javy i dowiedz
  się, jak ustawić wirtualny rozmiar ekranu, aby uzyskać dokładne renderowanie HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: pl
lastmod: 2026-09-29
og_description: Ustaw niestandardowy agent użytkownika w Aspose.HTML dla Javy i dowiedz
  się, jak ustawić wirtualny rozmiar ekranu, aby uzyskać dokładne renderowanie HTML.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Ustaw własny agent użytkownika i wymiary ekranu w Aspose.HTML dla Javy
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Ustaw niestandardowy agent użytkownika i wymiary ekranu w Aspose.HTML dla Javy
url: /pl/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw niestandardowy user‑agent i wymiary ekranu w Aspose.HTML dla Javy

Jeśli potrzebujesz **ustawić niestandardowy user‑agent** podczas renderowania HTML przy użyciu Aspose.HTML dla Javy, ten przewodnik pokaże Ci dokładnie, jak to zrobić. Konfigurując sandbox, zyskujesz również możliwość **ustawienia wirtualnego rozmiaru ekranu**, zapewniając, że układ odpowiada rzeczywistemu widokowi przeglądarki.

Zakończysz ten tutorial pełnym, uruchamialnym programem, który **określa user‑agent**, **ustawia szerokość ekranu** i **ustawia wysokość ekranu**. Nie są wymagane żadne zewnętrzne narzędzia — wystarczy Aspose.HTML dla Javy oraz środowisko uruchomieniowe Java 8+.

## Czego się nauczysz

* Jak utworzyć `SandboxConfiguration`, aby odizolować renderowanie.  
* Jak **ustawić niestandardowy user‑agent** i dlaczego ma to znaczenie dla responsywnych stron.  
* Jak **ustawić wirtualny rozmiar ekranu** (szerokość i wysokość) dla dokładnego układu.  
* Jak załadować plik HTML w sandboxie i zapisać przetworzony wynik.  
* Typowe pułapki i wskazówki najlepszych praktyk przy renderowaniu w sandboxie.  

> **Wymagania wstępne** – Potrzebujesz ważnej licencji Aspose.HTML dla Javy, Java 8 lub nowszej oraz IDE (IntelliJ IDEA, Eclipse lub VS Code). Przykład używa lokalnego pliku `input.html`, ale działa również dowolny dostępny URL.  

![Diagram przepływu sandbox](sandbox-flow.png "przykład ustawienia niestandardowego user‑agent w Javie")

## Krok 1: Utwórz konfigurację sandbox (podstawa)

Sandbox izoluje środowisko renderowania od hosta JVM, co jest niezbędne, gdy chcesz **ustawić niestandardowy user‑agent** lub zmienić rozmiar viewportu.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Dlaczego ten krok?*  
`SandboxConfiguration` przechowuje wszystkie opcje renderowania, w tym **wymiary ekranu** i ciągi **user‑agent**. Konfigurując go przed załadowaniem dokumentu, zapewniasz, że silnik HTML respektuje te ustawienia od pierwszego żądania.

## Krok 2: Ustaw wymiary ekranu, aby naśladować rzeczywiste urządzenie

Responsywne witryny często odczytują `window.innerWidth` i `window.innerHeight`. Aby silnik myślał, że działa na ekranie 1024 × 768, **ustawiasz wirtualny rozmiar ekranu**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Dlaczego to ważne* – Jeśli pominiesz **ustawienie wymiarów ekranu**, renderer może domyślnie używać małego viewportu, co spowoduje, że zapytania CSS media wybiorą układ mobilny. Poprzez wyraźne **ustawienie szerokości ekranu** i **ustawienie wysokości ekranu**, kontrolujesz, które reguły CSS zostaną zastosowane.

## Krok 3: Określ niestandardowy ciąg user‑agent

Niektóre strony internetowe dostarczają różną treść w zależności od nagłówka user‑agent. Aby **określić user‑agent**, po prostu ustaw go w konfiguracji sandbox:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Dlaczego używać niestandardowego user‑agent?*  
Niestandardowy ciąg może ominąć wykrywanie botów, uruchomić funkcje dostępne tylko na komputerach stacjonarnych lub przetestować, jak strona zachowuje się w konkretnej wersji przeglądarki. Silnik Aspose przekazuje tę wartość w każdym żądaniu HTTP wykonywanym podczas ładowania zewnętrznych zasobów (CSS, obrazy, skrypty).

## Krok 4: Załaduj dokument HTML wewnątrz sandbox

Teraz, gdy sandbox jest w pełni skonfigurowany, załaduj plik HTML. Konstruktor przyjmujący ścieżkę do pliku i `SandboxConfiguration` automatycznie stosuje wszystkie zdefiniowane ustawienia.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Jeśli potrzebujesz załadować zdalny URL, zamień ścieżkę do pliku na ciąg URL — Aspose.HTML nadal będzie respektować **ustawiony niestandardowy user‑agent** i **wymiary ekranu**.

## Krok 5: Zapisz przetworzony wynik

Po zakończeniu ładowania dokumentu możesz zapisać go w dowolnym obsługiwanym formacie. Tutaj zapisujemy plik HTML w sandboxie, który odzwierciedla wszelkie zmiany DOM spowodowane niestandardowymi ustawieniami.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

Zapisany plik będzie zawierał tę samą strukturę, ale wszystkie skrypty, które odpytały `navigator.userAgent` lub sprawdziły `window.innerWidth`, zobaczą teraz podane przez Ciebie wartości.

## Pełny, uruchamialny przykład

Połączenie wszystkich kroków daje Ci samodzielny program, który możesz skopiować, wkleić i uruchomić.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Oczekiwany wynik

Uruchomienie programu tworzy `sandboxed_output.html`. Jeśli otworzysz go w przeglądarce i sprawdzisz `navigator.userAgent` w konsoli, zobaczysz **AsposeHTML/1.0**. Analogicznie, `window.innerWidth` zwróci **1024**, potwierdzając, że **ustawienie wymiarów ekranu** działało zgodnie z zamierzeniami.

## Częste pytania i obsługa przypadków brzegowych

| Pytanie | Odpowiedź |
|----------|-----------|
| **Co jeśli strona ładuje dodatkowe zasoby z innej domeny?** | Sandbox przekazuje **niestandardowy user‑agent** w każdym żądaniu, ale zasady cross‑origin nadal obowiązują. Użyj `sandboxConfig.setAllowCrossDomain(true)`, jeśli musisz złagodzić te ograniczenia. |
| **Czy mogę zmienić rozmiar ekranu po załadowaniu dokumentu?** | Nie. Wymiary ekranu są odczytywane podczas początkowego przebiegu układu. Aby renderować z innym rozmiarem, utwórz nową `SandboxConfiguration` i ponownie załaduj dokument. |
| **Czy muszę wywołać `document.close()`?** | `HTMLDocument` implementuje `AutoCloseable`. Użycie bloku try‑with‑resources zapewnia prawidłowe czyszczenie, ale jawne wywołanie `close()` jest opcjonalne w prostych skryptach. |
| **Jak to się różni od ustawiania user‑agent w kliencie HTTP?** | Ustawienie user‑agent w sandboxie wpływa na **wszystkie** żądania zasobów wykonywane przez silnik HTML, nie tylko na początkowe pobranie HTML. To bardziej przypomina zachowanie prawdziwej przeglądarki. |
| **Czy sandbox jest bezpieczny dla nieufnego HTML?** | Tak. Sandbox izoluje dostęp do systemu plików i ogranicza wywołania sieciowe zgodnie z konfiguracją, zmniejszając ryzyko, że złośliwe skrypty wpłyną na hosta JVM. |

## Porady profesjonalne

* **Ponowne użycie konfiguracji** – Jeśli renderujesz wiele stron z tym samym viewportem, utwórz jedną `SandboxConfiguration` i używaj jej ponownie, aby uniknąć kosztów tworzenia obiektów.  
* **Debugowanie przy użyciu logowania** – Włącz logowanie Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`), aby zobaczyć, które zasoby zostały pobrane z niestandardowym user‑agentem.  
* **Łączenie z zapytaniami media CSS** – Dostosowując **ustawienie szerokości ekranu**, możesz testować, jak Twój responsywny projekt zachowuje się na tabletach, telefonach lub dużych komputerach bez otwierania prawdziwej przeglądarki.  

## Podsumowanie

Teraz wiesz, jak **ustawić niestandardowy user‑agent** i **ustawić wymiary ekranu** podczas renderowania HTML przy użyciu Aspose.HTML dla Javy. Konfigurując sandbox, izolujesz środowisko, kontrolujesz viewport i zapewniasz, że zewnętrzne zasoby widzą dokładnie te nagłówki, które określisz. Ta technika jest niezbędna do testowania responsywnych układów, omijania blokad botów lub odtwarzania funkcji dostępnych tylko na komputerach stacjonarnych w zautomatyzowanych pipeline'ach.  

Następnie możesz zbadać **jak ustawić niestandardowe ciasteczka** lub **wykonać zrzuty ekranu renderowanego** przy użyciu API renderowania Aspose.HTML — oba zagadnienia opierają się na tym samym wzorcu konfiguracji sandbox, który właśnie opanowałeś.  

Miłego kodowania!

## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Renderowanie w wysokiej rozdzielczości w Javie – przechwytywanie zrzutów ekranu stron internetowych z niestandardowym user‑agentem](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [Jak załadować HTML, ustawić DPI urządzenia i odczytać kolor tła](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Utwórz plik HTML w Javie i skonfiguruj usługę sieciową (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}