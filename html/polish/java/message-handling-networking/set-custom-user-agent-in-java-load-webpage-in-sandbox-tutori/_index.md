---
category: general
date: 2026-04-09
description: Ustaw niestandardowy user agent w Javie, aby wczytać stronę w sandboxie.
  Dowiedz się krok po kroku, jak ustawić user agent w Javie i emulować urządzenia
  mobilne.
draft: false
keywords:
- set custom user agent
- set user agent java
- load webpage in sandbox
- Aspose HTML sandbox
- Java web automation
language: pl
og_description: Ustaw niestandardowy user agent w Javie, aby ładować stronę w sandboxie.
  Skorzystaj z tego przewodnika, aby ustawić user agent w Javie, emulować urządzenia
  i wyodrębnić dane ze strony.
og_title: Ustaw niestandardowy user agent w Javie – Kompletny przewodnik po sandboxzie
tags:
- Aspose.HTML
- Java
- Web Scraping
title: Ustaw niestandardowy user agent w Javie – samouczek ładowania strony w piaskownicy
url: /pl/java/message-handling-networking/set-custom-user-agent-in-java-load-webpage-in-sandbox-tutori/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ustaw niestandardowy user agent w Javie – Ładowanie strony w sandboxie

Kiedykolwiek potrzebowałeś **ustawić niestandardowy user agent w Javie**, ale nie wiedziałeś, jak sprawić, by docelowa strona myślała, że korzystasz z przeglądarki mobilnej? Nie jesteś jedyny. Wiele stron serwuje różne HTML‑y lub nawet blokuje żądania, jeśli nagłówek *User‑Agent* nie wygląda znajomo. Dobra wiadomość? Dzięki Aspose.HTML możesz **ustawić niestandardowy user agent** wewnątrz sandboxa, załadować stronę i pracować z DOM‑em dokładnie tak, jakby prawdziwe urządzenie ją renderowało.

W tym samouczku przeprowadzimy Cię przez kompletny, działający przykład, który pokazuje, jak **ustawić user agent java**, skonfigurować sandbox, aby emulował iPhone’a, a następnie **załadować stronę w sandboxie**. Po zakończeniu będziesz mieć samodzielny program, który możesz wkleić do dowolnego projektu Java i od razu rozpocząć scrapowanie lub testowanie.

## Czego będziesz potrzebować

- Java 17 lub nowszy (kod używa nowoczesnego systemu modułów, ale starsze JDK działają po drobnych poprawkach)  
- Aspose.HTML for Java (najnowsza wersja w momencie pisania, 23.10)  
- Prosty IDE lub edytor tekstu; Maven/Gradle nie są wymagane dla tego fragmentu, ale potrzebny będzie JAR na classpath  
- Dostęp do Internetu dla przykładowego URL (`https://example.com`)

To wszystko—bez dodatkowych serwerów, bez przeglądarek headless, tylko kilka linii czystej Javy.

![Przykład ustawienia niestandardowego user agenta](https://example.com/image.png "ustawienie niestandardowego user agenta w sandboxie Java")

## Krok 1: Skonfiguruj sandbox – miejsce, w którym **ustawiasz niestandardowy user agent**

Sandbox to lekka, odizolowana środowisko, które naśladuje przeglądarkę. Najpierw tworzymy obiekt `SandboxOptions` i podajemy mu, jaki rozmiar ekranu oraz ciąg *User‑Agent* chcemy użyć.

```java
import com.aspose.html.sandbox.SandboxOptions;

// Step 1 – define sandbox options
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);               // iPhone width in CSS pixels
sandboxOptions.setScreenHeight(667);              // iPhone height
sandboxOptions.setUserAgent(
        "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
        "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1");
```

**Dlaczego to ważne:** Wywołanie `setUserAgent` to miejsce, w którym **ustawiasz niestandardowy user agent**. Dopasowując ciąg rzeczywistego urządzenia, przekonujesz serwer, aby dostarczył wersję mobilną, która często zawiera prostszy kod HTML — przydatny przy scrapowaniu lub testowaniu UI.

## Krok 2: Uruchom instancję sandboxa

Teraz, gdy opcje są gotowe, przekazujemy je do `HtmlDocumentSandbox`. Ten obiekt wymusi ustawienia dla wszystkiego, co w nim zostanie uruchomione.

```java
import com.aspose.html.sandbox.HtmlDocumentSandbox;

// Step 2 – create the sandbox with our options
HtmlDocumentSandbox sandbox = new HtmlDocumentSandbox(sandboxOptions);
```

**Porada:** Możesz ponownie używać tego samego sandboxa dla wielu ładowań stron, co oszczędza pamięć w porównaniu do uruchamiania nowej przeglądarki za każdym razem.

## Krok 3: Załaduj stronę, jednocześnie **ustawiając user agent java** w tle

Gdy sandbox jest aktywny, ładowanie strony jest tak proste, jak stworzenie obiektu `HTMLDocument`. Konstruktor przyjmuje URL oraz sandbox, który właśnie utworzyliśmy.

```java
import com.aspose.html.HTMLDocument;

// Step 3 – load the target page inside the sandbox
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", sandbox);
```

W tym momencie żądanie już zawiera nasz niestandardowy nagłówek *User‑Agent*. Jeśli przeanalizujesz ruch sieciowy (np. za pomocą Wireshark lub proxy), zobaczysz dokładny ciąg, który zdefiniowaliśmy wcześniej.

## Krok 4: Zweryfikuj, że strona została poprawnie załadowana – rezultat **load webpage in sandbox**

Wyciągnijmy tytuł z dokumentu, aby udowodnić, że wszystko zadziałało. To także pokazuje, jak możesz interagować z DOM po wyrenderowaniu strony.

```java
// Step 4 – read the title to confirm we loaded the page
System.out.println("Title (in sandbox): " + htmlDoc.getTitle());
```

**Oczekiwany wynik (może się różnić):**

```
Title (in sandbox): Example Domain
```

Jeśli zobaczysz wydrukowany tytuł, Twoje **load webpage in sandbox** zakończyło się sukcesem i niestandardowy user agent został zastosowany.

## Pełny, działający przykład

Po złożeniu wszystkich elementów razem otrzymujesz jedną klasę, którą możesz skompilować i uruchomić:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.HtmlDocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Configure the sandbox to emulate a mobile device
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);   // iPhone width in CSS pixels
        sandboxOptions.setScreenHeight(667);
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 2: Create a sandbox instance with the configured options
        HtmlDocumentSandbox sandbox = new HtmlDocumentSandbox(sandboxOptions);

        // Step 3: Load the web page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", sandbox);

        // Step 4: Work with the document as if it were rendered on the simulated device
        System.out.println("Title (in sandbox): " + htmlDoc.getTitle());
    }
}
```

Kompiluj za pomocą:

```bash
javac -cp "path/to/aspose-html.jar" SandboxExample.java
java -cp ".:path/to/aspose-html.jar" SandboxExample
```

Zastąp `path/to/aspose-html.jar` rzeczywistą ścieżką do pliku JAR Aspose.HTML.

## Typowe warianty i przypadki brzegowe

### Użycie innego profilu urządzenia

Jeśli potrzebujesz **ustawić niestandardowy user agent** dla tabletu z Androidem, po prostu zmień wymiary ekranu i ciąg user‑agent:

```java
sandboxOptions.setScreenWidth(800);
sandboxOptions.setScreenHeight(1280);
sandboxOptions.setUserAgent(
        "Mozilla/5.0 (Linux; Android 12; SM-G991U) " +
        "AppleWebKit/537.36 (KHTML, like Gecko) Chrome/106.0.5249.91 Mobile Safari/537.36");
```

### Obsługa przekierowań

Aspose.HTML automatycznie podąża za przekierowaniami, ale nagłówek *User‑Agent* jest zachowywany tylko, jeśli pozostajesz w tym samym sandboxie. Jeśli uruchamiasz nowy `HTMLDocument` dla każdego przekierowania, pamiętaj, aby przekazać tę samą instancję `sandbox`.

### Ładowanie stron HTTPS z certyfikatami samopodpisanymi

Do testów wewnętrznych możesz natrafić na stronę z certyfikatem samopodpisanym. Możesz złagodzić weryfikację certyfikatu, modyfikując `SandboxOptions`:

```java
sandboxOptions.setIgnoreCertificateErrors(true);
```

Używaj tego tylko w zaufanych środowiskach; w przeciwnym razie osłabia bezpieczeństwo.

## Wskazówki i pułapki

- **Porada:** Utrzymuj sandbox aktywny dla zadań wsadowych. Tworzenie i niszczenie go przy każdym żądaniu generuje dodatkowy narzut.
- **Uwaga:** Niektóre strony sprawdzają dodatkowe nagłówki (np. `Accept-Language`). Jeśli nadal Cię blokują, dodaj te nagłówki poprzez `sandboxOptions.getHeaders().add("Accept-Language", "en-US")`.
- **Uwaga o wydajności:** Sandbox działa w tym samym procesie, więc zużycie pamięci jest umiarkowane w porównaniu do pełnych przeglądarek jak Selenium. Jednak bardzo duże strony mogą nadal zużywać zauważalną ilość RAM‑u — monitoruj to, jeśli planujesz ładować dziesiątki stron jednocześnie.

## Zakończenie

Teraz wiesz, jak **ustawić niestandardowy user agent w Javie**, skonfigurować sandbox i **załadować stronę w sandboxie** przy użyciu Aspose.HTML. Pełny kod powyżej demonstruje cały przepływ — od definiowania `SandboxOptions` po wypisanie tytułu strony — więc możesz go od razu skopiować, wkleić i uruchomić.

Następnie rozważ rozszerzenie przykładu o wyodrębnianie konkretnych elementów (`htmlDoc.getElementById(...)`), robienie zrzutów ekranu (`sandbox.getScreenCapture()`), lub łączenie wielu URL‑ów w zadaniu crawl‑ującym. Wszystkie te zadania korzystają z tej samej techniki **set user agent java**, którą właśnie opanowałeś.

Śmiało eksperymentuj z różnymi ciągami urządzeń, rozmiarami ekranu lub nawet własnymi nagłówkami. Im więcej będziesz się bawić, tym lepiej zrozumiesz, jak serwery reagują na różne agenty — kluczowa umiejętność w automatyzacji sieci, testowaniu i ekstrakcji danych.

Szczęśliwego kodowania i niech Twoje żądania zawsze będą mile widziane!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}