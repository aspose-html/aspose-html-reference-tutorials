---
category: general
date: 2026-03-20
description: Ustaw user agent w sandboxie, aby wyodrębnić tytuł strony przy użyciu
  renderowania HTML w trybie headless – dowiedz się, jak ustawić DPI urządzenia i
  utworzyć instancję sandboxa.
draft: false
keywords:
- set user agent
- extract page title
- set device dpi
- create sandbox instance
- headless html rendering
language: pl
og_description: Ustaw user‑agent w piaskownicy, wyodrębnij tytuł strony i kontroluj
  DPI urządzenia, aby zapewnić niezawodne renderowanie HTML w trybie headless.
og_title: Ustawienie User Agent dla renderowania HTML w trybie headless – Kompletny
  przewodnik
tags:
- Java
- Web Scraping
- Headless Rendering
title: Ustaw User Agent dla renderowania HTML w trybie headless – Kompletny przewodnik
url: /pl/java/configuring-environment/set-user-agent-for-headless-html-rendering-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustawienie user‑agent dla renderowania HTML w trybie headless – Kompletny przewodnik

Czy kiedykolwiek potrzebowałeś **ustawić user‑agent** podczas scrapowania witryny, ale nie byłeś pewien, jak wpływa to na renderowaną stronę? Nie jesteś sam. W wielu scenariuszach headless serwer decyduje, jaki HTML wysłać na podstawie ciągu UA, więc prawidłowe ustawienie może być różnicą między pustą stroną a rzeczywistą treścią, której potrzebujesz.  

W tym samouczku przeprowadzimy Cię przez konfigurację sandboxu, **tworzenie instancji sandboxu**, dostosowanie **DPI urządzenia** oraz w końcu **wyodrębnienie tytułu strony** z sesji **headless HTML rendering**. Bez zbędnych wstępów — po prostu działający przykład w Javie, który możesz od razu dodać do swojego projektu.

> **Pro tip:** Jeśli już używasz Aspose.HTML (lub podobnej biblioteki), poniższe kroki odpowiadają 1‑do‑1 jej API. Jeśli korzystasz z innego stosu, traktuj sandbox jako dowolny kontekst przeglądarki headless (Playwright, Selenium itp.).

## Co zbudujesz

- Sandbox z niestandardowym ciągiem **user‑agent**.
- Renderowanie uwzględniające DPI, aby jednostki CSS (pt, in, cm) zachowywały się jak na prawdziwym ekranie.
- Czysty sposób na **wyodrębnienie tytułu strony** po pełnym wyrenderowaniu strony.
- Samodzielna klasa Java, którą możesz uruchomić z wiersza poleceń.

Wymagania? Tylko Java 8+ oraz plik JAR Aspose.HTML for Java w classpath. Nic więcej.

---

## Ustawienie user‑agent i konfiguracja sandboxu

Pierwszą rzeczą, którą musisz zrobić, jest poinformowanie silnika renderującego, jaką przeglądarkę udajesz. Odbywa się to za pomocą metody `SandboxConfiguration#setUserAgent`.

```java
import com.aspose.html.Sandbox;
import com.aspose.html.SandboxConfiguration;
import com.aspose.html.HTMLDocument;

/* Step 1: Configure the sandbox – screen size, DPI, and user‑agent */
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
sandboxConfig.setScreenSize(1280, 800);      // width × height in pixels
sandboxConfig.setDeviceDPI(96);              // DPI for CSS unit conversion
sandboxConfig.setUserAgent("AsposeHTML/1.0"); // <-- set user agent
```

Dlaczego to ważne? Wiele witryn serwuje uproszczony układ nieznanym agentom (np. „bot”) i ukrywa dane, których naprawdę potrzebujesz. Naśladując prawdziwą przeglądarkę, zmuszasz serwer do zwrócenia pełnej strony.

![set user agent configuration](/images/set-user-agent.png "Illustration of set user agent in sandbox configuration")

*Tekst alternatywny obrazu: zrzut ekranu konfiguracji ustawienia user‑agent.*

## Utworzenie instancji sandboxu dla renderowania HTML w trybie headless

Gdy konfiguracja jest gotowa, uruchom sandbox. Pomyśl o tym jak o uruchomieniu headless Chrome, które istnieje wyłącznie w pamięci.

```java
/* Step 2: Create the sandbox using the configuration */
try (Sandbox sandboxInstance = new Sandbox(sandboxConfig)) {
    // The sandbox is now ready for rendering tasks.
    // Anything you do inside this block runs headlessly.
}
```

Użycie wzorca try‑with‑resources zapewnia prawidłowe zwolnienie sandboxu, uwalniając zasoby natywne. Jeśli zapomnisz go zamknąć, możesz wyciekać pamięć lub uchwyty plików — coś, co zauważyłem u nowicjuszy.

## Ustawienie DPI urządzenia dla dokładnego renderowania CSS

Wywołanie `setDeviceDPI` nie jest jedynie dodatkiem; bezpośrednio wpływa na sposób obliczania jednostek CSS, takich jak `pt` czy `mm`. Jeśli renderujesz faktury, PDF‑y lub jakąkolwiek stronę wrażliwą na układ, dopasowanie docelowego DPI zapewnia, że zrzuty ekranu lub wyodrębnione dane wyglądają dokładnie tak, jak na prawdziwym monitorze.

Już widziałeś to wywołanie w fragmencie konfiguracji, ale oto szybka kontrola:

```java
int dpi = sandboxConfig.getDeviceDPI(); // should return 96
System.out.println("Sandbox DPI set to: " + dpi);
```

Jeśli potrzebujesz wyższej rozdzielczości (np. dla zasobów w stylu retina), zwiększ wartość do `144` lub `192`. Pamiętaj jednak, aby zachować proporcjonalny rozmiar ekranu; w przeciwnym razie układ może się przepełnić.

## Wyodrębnienie tytułu strony z wyrenderowanego dokumentu

Teraz, gdy sandbox działa, załaduj stronę i pobierz jej tytuł. Metoda `HTMLDocument#getTitle` odczytuje znacznik `<title>` *po* pełnym przetworzeniu DOM strony.

```java
/* Step 3: Load a web page inside the sandboxed environment */
HTMLDocument htmlDoc = new HTMLDocument(sandboxInstance, "https://example.com");

/* Step 4: Work with the rendered document – extract its title */
String pageTitle = htmlDoc.getTitle();
System.out.println("Title: " + pageTitle);
```

Uruchomienie powyższego przeciwko `https://example.com` wypisuje:

```
Title: Example Domain
```

To jest krok **wyodrębniania tytułu strony** w praktyce. Jeśli witryna używa JavaScriptu do dynamicznego ustawiania tytułu, sandbox wykona skrypt (zakładając, że włączono skrypty, co jest domyślne). Jeśli kiedykolwiek zobaczysz pusty ciąg, sprawdź ponownie, czy po uruchomieniu skryptów strona rzeczywiście zawiera element `<title>`.

## Pełny działający przykład

Łącząc wszystko razem, oto pełna, gotowa do uruchomienia klasa. Śmiało skopiuj i wklej do `Main.java` oraz uruchom `javac Main.java && java Main`.

```java
import com.aspose.html.Sandbox;
import com.aspose.html.SandboxConfiguration;
import com.aspose.html.HTMLDocument;

/**
 * Demonstrates how to set user agent, configure DPI,
 * create a sandbox instance, and extract the page title
 * using headless HTML rendering.
 */
public class Main {
    public static void main(String[] args) {
        // 1️⃣ Configure sandbox: screen, DPI, and user‑agent
        SandboxConfiguration config = new SandboxConfiguration();
        config.setScreenSize(1280, 800);
        config.setDeviceDPI(96);
        config.setUserAgent("AsposeHTML/1.0"); // <-- set user agent

        // 2️⃣ Create sandbox (auto‑close with try‑with‑resources)
        try (Sandbox sandbox = new Sandbox(config);
             // 3️⃣ Load the page inside the sandbox
             HTMLDocument doc = new HTMLDocument(sandbox, "https://example.com")) {

            // 4️⃣ Extract and print the title
            String title = doc.getTitle();
            System.out.println("Title: " + title);
        } catch (Exception e) {
            // Simple error handling – in real code you might log this
            System.err.println("Rendering failed: " + e.getMessage());
        }
    }
}
```

### Oczekiwany wynik

```
Title: Example Domain
```

Jeśli zamienisz `https://example.com` na dowolny inny URL, zobaczysz tytuł tej strony — pod warunkiem, że witryna nie blokuje agentów headless. To cały **pipeline renderowania HTML w trybie headless** w mniej niż 30 linijkach Javy.

---

## Częste pytania i przypadki brzegowe

| Question | Answer |
|----------|--------|
| *Co zrobić, jeśli witryna blokuje nieznane UA?* | Użyj popularnego ciągu przeglądarki, np. `"Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/119.0 Safari/537.36"`. Sandbox pozwala ustawić dowolny dowolny UA. |
| *Czy muszę włączyć JavaScript?* | Jest włączony domyślnie. Jeśli wyłączyłeś go wcześniej, wywołaj `config.setEnableJavaScript(true)`. |
| *Jak zrobić zrzut ekranu zamiast tylko tytułu?* | Po załadowaniu dokumentu, wywołaj `htmlDoc.save("page.png", SaveFormat.PNG)`. DPI ustawione wcześniej wpłynie na rozmiar obrazu. |
| *Czy mogę renderować wiele stron w jednym sandboxie?* | Tak. Ponownie użyj tego samego obiektu `Sandbox`; po prostu utwórz nowe obiekty `HTMLDocument` dla każdego URL. |
| *A co z certyfikatami HTTPS?* | Sandbox ufa domyślnemu keystore Java. W przypadku certyfikatów samopodpisanych, zaimportuj je do magazynu zaufania JVM lub wyłącz weryfikację poprzez `config.setIgnoreCertificateErrors(true)`. |

---

## Wskazówki dla produkcyjnego scrapowania

1. **Rotuj User Agenty** – Przechowuj listę popularnych ciągów UA i losowo wybieraj jeden przy każdym żądaniu. Zmniejsza to ryzyko wykrycia.  
2. **Szanuj Robots.txt** – Mimo że działasz w trybie headless, etyczne scrapowanie oznacza przestrzeganie polityki crawlowania witryny.  
3. **Ogranicz częstotliwość żądań** – Wstaw `Thread.sleep(500)` pomiędzy wywołaniami, aby nie przeciążać serwera.  
4. **Cache'uj wyrenderowany HTML** – Jeśli potrzebujesz tej samej strony wielokrotnie, zapisz HTML na dysku i używaj go ponownie; renderowanie jest zasobożerne CPU.  
5. **Monitoruj pamięć** – Sandbox trzyma zasoby natywne. W długotrwałych zadaniach okresowo wywołuj `System.gc()` lub restartuj sandbox po przetworzeniu partii URL‑i.  

---

## Podsumowanie

Teraz wiesz, jak **ustawić user‑agent** dla niezawodnego **renderowania HTML w trybie headless**, skonfigurować **DPI urządzenia**, **utworzyć instancję sandboxu** oraz **wyodrębnić tytuł strony** w czystym przepływie pracy w Javie. Pełny przykład powyżej działa od razu, wypisuje tytuł i pozostawia miejsce na rozszerzenia, takie jak zrzuty ekranu czy konwersja do PDF.

Następnie spróbuj zamienić URL na witrynę, która serwuje inną treść w zależności od ciągu UA, lub poeksperymentuj z wyższymi wartościami DPI, aby zobaczyć, jak zmieniają się układy CSS. Możesz także zbadać przeciążenia `HTMLDocument.save` w bibliotece, aby generować PDF‑y — kolejny przydatny sposób archiwizacji wyrenderowanych stron.

Miłego kodowania i niech Twoje scrapers pozostaną niewykryte!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}