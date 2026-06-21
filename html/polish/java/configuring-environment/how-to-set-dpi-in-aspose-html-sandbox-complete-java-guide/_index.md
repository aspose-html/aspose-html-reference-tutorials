---
category: general
date: 2026-04-02
description: Dowiedz się, jak ustawić DPI, rozmiar viewportu i agenta użytkownika
  w Aspose.HTML Sandbox. Przykład Java krok po kroku z pełnym kodem i wskazówkami.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: pl
og_description: Opanuj, jak ustawić DPI, rozmiar viewportu oraz agenta użytkownika
  w Aspose.HTML Sandbox, korzystając z pełnego przykładu w Javie.
og_title: Jak ustawić DPI w piaskownicy Aspose.HTML – samouczek Java
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Jak ustawić DPI w piaskownicy Aspose.HTML – Kompletny przewodnik Java
url: /pl/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak ustawić DPI w piaskownicy Aspose.HTML – Kompletny przewodnik Java

Zastanawiałeś się kiedyś **jak ustawić DPI** podczas renderowania strony internetowej przy użyciu Aspose.HTML? Nie jesteś jedyny. W wielu scenariuszach testowych potrzebny jest układ dopasowany do określonej gęstości ekranu — pomyśl o PDF‑ach gotowych do druku lub zrzutach ekranu w wysokiej rozdzielczości. Dobrą wiadomością jest to, że piaskownica Aspose.HTML pozwala kontrolować DPI, rozmiar viewportu i nawet ciąg user‑agent w jednym poręcznym pakiecie.

W tym samouczku przeprowadzimy praktyczny przykład w Javie, który **ustawia DPI**, **ustawia rozmiar viewportu** i **ustawia user‑agent** jednocześnie. Po zakończeniu będziesz mieć działający program, zrozumiesz, dlaczego każde ustawienie ma znaczenie, i będziesz gotowy dostosować piaskownicę do własnych projektów.

---

## Czego będziesz potrzebować

- **Java 17** (lub dowolny nowszy JDK; API jest kompatybilne z Java 8+)
- **Aspose.HTML for Java** library (wersja 23.12 lub nowsza)
- IDE lub prosty edytor tekstu + kompilacja z linii poleceń
- Dostęp do Internetu dla przykładowego URL (`https://example.com`)

Nie są wymagane żadne zewnętrzne narzędzia budujące; kod kompiluje się przy użyciu `javac` i uruchamia przy pomocy `java`. Jeśli wolisz Maven lub Gradle, po prostu dodaj zależność Aspose.HTML — nic skomplikowanego.

---

## Krok 1: Utwórz piaskownicę definiującą środowisko renderowania

Piaskownica to miejsce, w którym informujesz Aspose.HTML, jakim „ekranem” udajesz się posiadać. Tutaj ustawiamy **viewport 1024 × 768**, **DPI 96** oraz własny **ciąg user‑agent**.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Dlaczego to ważne:**  
- **DPI** wpływa na to, jak jednostki CSS `pt` przeliczane są na piksele; wyższe DPI daje ostrzejsze renderowanie.  
- **Rozmiar viewportu** określa punkty przerwania układu, które zostaną użyte przez responsywny CSS.  
- **User‑agent** może wywołać różnice w treści po stronie serwera (mobile vs desktop).

> **Porada:** Jeśli później generujesz PDF‑y, dopasuj DPI do docelowej rozdzielczości druku (np. 300 dpi dla wysokiej jakości wydruków).

---

## Krok 2: Załaduj stronę internetową wewnątrz piaskownicy

Teraz wskazujemy piaskownicę na URL. Konstruktor `HTMLDocument` przyjmuje piaskownicę, więc silnik układu respektuje właśnie zdefiniowane ustawienia.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Co się dzieje pod maską?**  
Aspose.HTML tworzy odizolowany kontekst renderowania, podobny do przeglądarki headless, ale bez obciążenia pełnej instancji Chromium. Dzięki temu operacja jest szybka i lekka pod względem pamięci — idealna do przetwarzania wsadowego.

---

## Krok 3: Interakcja z DOM — odczyt tytułu strony

Dla demonstracji pobierzemy tytuł i wypiszemy go. W rzeczywistym scenariuszu możesz zrobić zrzut ekranu, wyeksportować do PDF lub wyodrębnić dane.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Oczekiwany wynik** (gdy `https://example.com` jest dostępny):

```
Title inside sandbox: Example Domain
```

Jeśli strona zwróci inny tytuł, zobaczysz go zamiast tego — nie trzeba zmieniać niczego innego.

---

## Krok 4: Weryfikacja ustawień (opcjonalne debugowanie)

Czasami chcesz podwójnie sprawdzić, czy piaskownica naprawdę respektuje Twoje DPI i viewport. Aspose.HTML nie udostępnia tych wartości bezpośrednio, ale możesz je wywnioskować, mierząc wymiary elementów.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Jeśli wiesz, że CSS deklaruje element jako `width: 200pt;`, przy **96 dpi** powinieneś zobaczyć `200pt * (96/72) ≈ 267px`. Zmień DPI i uruchom ponownie, aby zobaczyć zmianę liczby — dowód, że **jak ustawić dpi** naprawdę działa.

---

## Pełny kod źródłowy w jednym bloku

Skopiuj i wklej poniższy kod do `SandboxExample.java`. Kompiluje się bez zmian; upewnij się tylko, że plik JAR Aspose.HTML znajduje się na ścieżce klas.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Kompiluj i uruchom:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Powinieneś zobaczyć wypisany tytuł, co potwierdza, że piaskownica działa z **ustawionym dpi**, **ustawionym rozmiarem viewportu** i **ustawionym user agent**, które podałeś.

---

## Częste pytania i przypadki brzegowe

### Co zrobić, jeśli potrzebuję innego DPI?

Po prostu zmień drugi argument `DocumentSandbox`. Dla PDF‑ów gotowych do druku możesz użyć `300`:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Wyższe DPI daje większe wymiary w pikselach dla tych samych punktów CSS, co poprawia jakość rastrową, ale zużywa więcej pamięci.

### Czy mogę załadować lokalny plik HTML zamiast URL?

Oczywiście. Zastąp URL ścieżką do pliku:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Upewnij się, że ścieżka jest absolutna i używa schematu `file:///`.

### Jak zmienić user‑agent po utworzeniu piaskownicy?

Piaskownica jest niezmienna — po przekazaniu jej do `HTMLDocument` ustawienia są zablokowane. Aby użyć innego user‑agent, utwórz nowy `DocumentSandbox` z żądanym ciągiem.

### Czy Aspose.HTML obsługuje wykonywanie JavaScript?

Tak, silnik uruchamia większość skryptów po stronie klienta. Jeśli skrypt modyfikuje DOM po załadowaniu, możesz chwilę poczekać:

```java
webDoc.waitForLoad();
```

Lub użyj logiki podobnej do `setTimeout` wewnątrz strony przed zapytaniem o elementy.

---

## Wizualne potwierdzenie (obraz)

Poniżej znajduje się zrzut ekranu konsoli pokazujący pomyślne uruchomienie. Zauważ, że wyświetlony tytuł odpowiada stronie, co potwierdza, że piaskownica respektowała nasze ustawienia.

![Console output showing how to set dpi in Aspose.HTML Sandbox](/images/console-output.png)

*Alt text:* *Wyjście konsoli demonstrujące, jak ustawić dpi, rozmiar viewportu i user agent w piaskownicy Aspose.HTML.*

---

## Podsumowanie i kolejne kroki

Omówiliśmy **jak ustawić DPI** (96 dpi w przykładzie), **ustawić rozmiar viewportu** (1024 × 768) i **ustawić user agent** (własny ciąg) przy użyciu API piaskownicy Aspose.HTML. Pełny, działający program w Javie dowodzi, że te ustawienia nie są tylko teoretyczne — bezpośrednio wpływają na renderowanie i interakcję z DOM.

Gotowy na więcej?

- **Eksport do PDF:** Po załadowaniu strony wywołaj `webDoc.save("output.pdf", SaveFormat.PDF);`, aby wygenerować PDF o wysokiej rozdzielczości odzwierciedlający ustawione DPI.  
- **Zrób zrzut ekranu:** Użyj `webDoc.renderToBitmap("screenshot.png");` dla obrazów o idealnej rozdzielczości pikseli.  
- **Eksperymentuj z responsywnymi układami:** Zmieniaj wymiary viewportu, aby testować breakpointy mobilne bez rzeczywistego urządzenia.

Eksperymentuj z różnymi wartościami DPI, kombinacjami viewportu i user‑agentami, aby zobaczyć, jak serwery i CSS reagują. Piaskownica to lekka piaskownica, która oszczędza Ci konieczności uruchamiania pełnych przeglądarek.

---

### Kontynuuj eksplorację

- **Dokumentacja Aspose.HTML** – szczegółowe informacje o opcjach `DocumentSandbox`.  
- **Zaawansowane zapytania media CSS** – dowiedz się, jak rozmiar viewportu wyzwala różne style.  
- **Spoofing User‑Agent** – odkryj, jak niektóre witryny dostarczają alternatywny markup w zależności od ciągu agenta.

Masz pytania lub trudny przypadek? Napisz komentarz, a wspólnie rozwiążemy problem. Szczęśliwego kodowania!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}