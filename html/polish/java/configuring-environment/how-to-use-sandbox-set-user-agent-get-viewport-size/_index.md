---
category: general
date: 2026-04-03
description: Dowiedz się, jak używać sandbox w Aspose.HTML Java, aby ustawić user
  agent, rozmiar i natychmiast uzyskać rozmiar widoku. Pełny kod, wyjaśnienia i wskazówki
  w zestawie.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: pl
og_description: Dowiedz się, jak używać sandbox w Aspose.HTML Java, aby ustawić agent
  użytkownika, rozmiar i natychmiast uzyskać rozmiar okna widoku. Kompletny przewodnik
  z kodem i najlepszymi praktykami.
og_title: Jak korzystać z Sandbox – ustaw User Agent i uzyskaj rozmiar viewportu
tags:
- AsposeHTML
- Java
- Sandbox
title: Jak używać Sandbox – Ustaw agent użytkownika i pobierz rozmiar obszaru widoku
url: /pl/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak używać Sandbox – Ustaw User Agent i uzyskaj rozmiar Viewportu

Zastanawiałeś się kiedyś **jak używać sandbox** przy renderowaniu HTML przy użyciu Aspose.HTML for Java? Być może napotkałeś problem przy symulacji określonego rozmiaru ekranu lub musisz podrobić ciąg user‑agent, aby strona zachowywała się tak, jakby była odwiedzana z przeglądarki mobilnej.  

Dobre wiadomości są takie, że API sandbox pozwala zrobić dokładnie to, a dodatkowo możesz pobrać obliczony rozmiar viewportu po załadowaniu strony. W tym samouczku przejdziemy przez tworzenie sandboxu, ustawianie rozmiaru, ustawianie własnego user‑agenta, ładowanie zdalnej strony i w końcu odczyt wymiarów viewportu. Po zakończeniu będziesz wiedział **jak ustawić rozmiar**, **jak uzyskać viewport** oraz dlaczego te kroki są ważne dla niezawodnego renderowania headless.

> **Szybki sukces:** w ciągu kilku sekund będziesz mieć uruchamialną klasę Java, która wypisze coś w stylu `Viewport: 1280×800`.

---

## Co będzie potrzebne

- **Aspose.HTML for Java** w wersji 24.6 lub nowszej (używane API zostało wprowadzone w 24.5).  
- Zestaw deweloperski Java 17+ (dowolny aktualny JDK).  
- IDE lub prosty edytor tekstu — nie są wymagane żadne specjalne wtyczki.  
- Dostęp do Internetu, jeśli chcesz załadować zewnętrzny URL, np. `https://example.com`.

To wszystko. Nie jest obowiązkowe używanie Maven/Gradle; możesz ręcznie dodać pliki JAR do classpath, jeśli wolisz.  

---

## Jak używać Sandbox – Przegląd

Sandbox izoluje silnik renderujący od systemu operacyjnego, pozwalając zdefiniować wirtualny ekran (szerokość, wysokość, DPI) oraz własny ciąg **user agent**. To jak miniaturowe okno przeglądarki, które istnieje wyłącznie w pamięci. Kiedy później zapytasz `HTMLDocument` o jego domyślny widok, silnik zwróci **rozmiar viewportu**, który obliczył na podstawie ustawień sandboxu.  

Poniżej schemat wysokiego poziomu:

1. **Utwórz** `DocumentSandbox` i skonfiguruj szerokość, wysokość, DPI oraz user‑agent.  
2. **Załaduj** `HTMLDocument` wewnątrz tego sandboxu.  
3. **Zapytaj** domyślny widok dokumentu o rozmiar viewportu.  

Przejdźmy do każdego kroku.

---

## Krok 1: Utwórz Sandbox i ustaw rozmiar

Najpierw uruchamiamy sandbox i określamy, jak duży ma być wirtualny ekran. To właśnie tutaj odpowiadasz na pytanie **jak ustawić rozmiar** dla renderowania headless.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Wskazówka:** Jeśli testujesz responsywny układ, wypróbuj wąską szerokość, np. `360`, aby emulować telefon, lub szeroką, np. `1920`, dla komputera stacjonarnego. Sandbox respektuje ustawione DPI, więc ekran o wysokiej gęstości (np. 144 DPI) wpłynie na media‑queries używające `device-pixel-ratio`.

---

## Krok 2: Ustaw User Agent dla Sandboxu

Po co własny **user agent**? Niektóre witryny dostarczają inny markup lub skrypty w zależności od zgłaszanego przeglądarki. Wywołując `setUserAgent` możesz oszukać stronę, by myślała, że jest odwiedzana z Chrome, Firefox lub urządzenia mobilnego.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Teraz strona będzie myślała, że renderuje się na iPhone. Jeśli potrzebujesz **ustawić user agent** z powrotem na domyślny, po prostu użyj wcześniejszego ciągu „AsposeHTML/24.6 …”.

---

## Krok 3: Załaduj dokument HTML wewnątrz Sandboxu

Gdy sandbox jest gotowy, możemy załadować dowolny URL lub lokalny plik HTML. Konstruktor `HTMLDocument` przyjmuje sandbox jako drugi argument, łącząc je ze sobą.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

Blok `try‑with‑resources` zapewnia prawidłowe zwolnienie dokumentu, uwalniając natywne zasoby, które Aspose.HTML przydziela pod maską.

---

## Krok 4: Pobierz rozmiar Viewportu z dokumentu

Oto moment, na który czekałeś: pobranie **rozmiaru viewportu**, który obliczył silnik renderujący. To odpowiada na pytanie **jak uzyskać viewport** po ułożeniu strony.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Po uruchomieniu programu powinieneś zobaczyć coś w stylu:

```
Viewport: 1280×800
```

Jeśli zmieniłeś wymiary sandboxu w Kroku 1, wydrukowane liczby odzwierciedlą te nowe wartości — idealne do automatycznych testów weryfikujących punkty przełamania responsywności.

---

## Pełny działający przykład

Poniżej znajduje się kompletna, gotowa do uruchomienia klasa, która łączy wszystkie elementy. Skopiuj‑wklej ją do pliku o nazwie `SandboxExample.java`, dodaj pliki JAR Aspose.HTML do classpath i uruchom `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Oczekiwany wynik** (przy założonych ustawieniach sandboxu):

```
Viewport: 1280×800
```

Jeśli ustawisz inną szerokość/wysokość w sandboxie, wynik się odpowiednio zmieni — dokładnie to, czego potrzebujesz przy testowaniu projektów responsywnych.

---

## Przypadki brzegowe i najczęstsze pytania

### Co jeśli strona używa `window.innerWidth` zamiast zapytań CSS?

Wirtualny rozmiar ekranu sandboxu wpływa zarówno na układ CSS, jak i na JavaScript‑owe `window.innerWidth/innerHeight`. Dlatego **jak uzyskać viewport** za pomocą JavaScript zwróci te same liczby, które widzisz w konsoli Java.

### Czy mogę uruchamiać wiele sandboxów równolegle?

Tak. Każda instancja `DocumentSandbox` jest niezależna, więc możesz uruchomić pulę wątków, przydzielić każdemu wątkowi własny sandbox o różnych wymiarach i renderować dziesiątki stron jednocześnie. Pamiętaj tylko, aby JAR‑y były bezpieczne wątkowo (są).

### Czy ustawienie DPI wpływa na skalowanie obrazów?

Zdecydowanie. Wyższe DPI sprawia, że jeden piksel CSS mapuje się na więcej pikseli urządzenia, co może powodować, że obrazy o wysokiej rozdzielczości będą wyglądały ostrzej. Jeśli testujesz zasoby w stylu retina, wypróbuj `sandbox.setDeviceDpi(144)`.

### Jak obsłużyć certyfikaty HTTPS, które są samodzielnie

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}