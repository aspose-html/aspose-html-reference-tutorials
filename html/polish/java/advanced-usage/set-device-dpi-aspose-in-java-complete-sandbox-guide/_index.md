---
category: general
date: 2026-06-16
description: Dowiedz się, jak ustawić DPI urządzenia w Aspose oraz szerokość i wysokość
  viewportu podczas renderowania HTML w sandboxie Aspose.HTML w Javie. Dołączony kod
  krok po kroku.
draft: false
keywords:
- set device dpi aspose
- set viewport width height
language: pl
og_description: Odkryj, jak ustawić DPI urządzenia w Aspose i określić szerokość oraz
  wysokość viewportu przy użyciu sandboxu Aspose.HTML dla Javy. Pełny kod i wyjaśnienie.
og_title: Ustaw DPI urządzenia Aspose w Javie – Kompletny przewodnik po Sandbox
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  headline: set device dpi aspose in Java – Complete Sandbox Guide
  type: TechArticle
- description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  name: set device dpi aspose in Java – Complete Sandbox Guide
  steps:
  - name: Configure sandbox options (including DPI and viewport size).
    text: Configure sandbox options (including DPI and viewport size).
  - name: Instantiate a `DocumentSandbox` with those options.
    text: Instantiate a `DocumentSandbox` with those options.
  - name: Load an external HTML page inside the sandbox.
    text: Load an external HTML page inside the sandbox.
  - name: Perform a simple DOM operation—printing the page title.
    text: Perform a simple DOM operation—printing the page title.
  type: HowTo
tags:
- Aspose.HTML
- Java
- HTML rendering
- Sandbox
title: Ustaw DPI urządzenia w Aspose w Javie – kompletny przewodnik po Sandbox
url: /pl/java/advanced-usage/set-device-dpi-aspose-in-java-complete-sandbox-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device dpi aspose – Java Sandbox Tutorial

Zastanawiałeś się kiedyś, jak **ustawić DPI urządzenia w Aspose** podczas renderowania strony internetowej w Javie? Nie jesteś sam. Wielu programistów napotyka problem, gdy potrzebują, aby renderowana strona wyglądała dokładnie tak, jak na prawdziwym ekranie — szczególnie gdy DPI ma znaczenie dla obliczeń układu.

W tym przewodniku przeprowadzimy Cię przez praktyczny przykład, który nie tylko **ustawia DPI urządzenia w Aspose**, ale także pokazuje, jak **ustawić szerokość i wysokość viewportu**, aby strona zachowywała się tak, jak w oknie przeglądarki o wymiarach 1280 × 800 pikseli. Na końcu będziesz mieć działający fragment kodu, jasne wyjaśnienie każdego kroku oraz wskazówki, jak unikać typowych pułapek.

## What This Tutorial Covers

Zaczniemy od przedstawienia wymagań wstępnych, a potem przejdziemy do czterech zwięzłych kroków:

1. Skonfiguruj opcje sandboxu (w tym DPI i rozmiar viewportu).  
2. Utwórz `DocumentSandbox` z tymi opcjami.  
3. Załaduj zewnętrzną stronę HTML wewnątrz sandboxu.  
4. Wykonaj prostą operację DOM — wypisanie tytułu strony.

Zobaczysz, dlaczego każdy element ma znaczenie, jak dostosować ustawienia dla różnych urządzeń i jak powinien wyglądać wynik. Nie potrzebujesz dodatkowej dokumentacji; wszystko, czego potrzebujesz, znajduje się tutaj.

## Prerequisites

- Java 8 lub nowsza (biblioteka Aspose.HTML for Java obsługuje JDK 8+).  
- Pliki JAR Aspose.HTML for Java dodane do classpath projektu.  
- IDE lub narzędzie budujące (Maven/Gradle) do kompilacji i uruchomienia kodu.  
- Dostęp do Internetu, jeśli planujesz ładować żywy URL, np. `https://example.com`.

Jeśli wszystkie te elementy są spełnione, zaczynamy.

## Step 1: Set device DPI aspose – Define Sandbox Options

Pierwszą rzeczą, którą musisz zrobić, jest poinformowanie sandboxu, jakim „ekranem” się udajesz. Tu wkracza **ustawianie DPI urządzenia w Aspose**. DPI (dots per inch) wpływa na interpretację jednostek CSS `px`, co może zmienić rozmiary czcionek, skalowanie obrazów i zapytania medialne.

```java
// Step 1: Create sandbox options and configure DPI and viewport.
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
sandboxOptions.setViewportWidth(1280);         // set viewport width height
sandboxOptions.setViewportHeight(800);         // set viewport width height
```

> **Dlaczego to ważne:**  
> *Wywołanie `setDeviceDpi` mówi Aspose.HTML, aby traktować jeden piksel CSS jako 1/96 cala, co odzwierciedla większość monitorów stacjonarnych. Jeśli pominiesz ten krok, układ może wyglądać zbyt mało lub zbyt duży na ekranach o wysokim DPI.*

## Step 2: Create the Sandbox with the Configured Options

Teraz, gdy opcje są gotowe, potrzebujesz instancji sandboxu, która je respektuje. Myśl o sandboxie jako o małym, odizolowanym silniku przeglądarki, który nie dotyka Twojego systemu plików.

```java
// Step 2: Initialise the DocumentSandbox using the options above.
DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);
```

> **Pro tip:**  
> Ponowne użycie tego samego `DocumentSandbox` dla wielu stron oszczędza pamięć, ale pamiętaj, aby zresetować opcje, jeśli później potrzebujesz innego DPI lub viewportu.

## Step 3: Load an HTML Document Inside the Sandbox

Gdy sandbox jest gotowy, ładowanie strony jest proste. Konstruktor `HTMLDocument` przyjmuje URL oraz sandbox, który właśnie utworzyłeś.

```java
// Step 3: Load a remote HTML page using the sandbox.
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);
```

> **Edge case:**  
> Jeśli docelowa strona blokuje automatyczne żądania, możesz otrzymać błąd 403. W takim wypadku pobierz HTML lokalnie i załaduj go z ścieżki pliku lub ustaw własny ciąg user‑agent za pomocą `sandboxOptions`.

## Step 4: Perform Normal DOM Operations – Print the Page Title

W tym momencie strona jest w pełni wyrenderowana w sandboxie, więc każde zapytanie DOM działa dokładnie tak, jak w pełnoprawnej przeglądarce. Zachowajmy to proste i pobierzmy tytuł.

```java
// Step 4: Access the DOM – print the page title.
System.out.println("Title: " + htmlDoc.getTitle());
```

**Expected output**

```
Title: Example Domain
```

Jeśli zobaczysz coś innego, sprawdź, czy URL jest dostępny i czy nie zmieniłeś przypadkowo wartości DPI lub viewportu.

## Why Setting Viewport Width Height Is Crucial

Możesz zapytać: „Dlaczego w ogóle **ustawiamy szerokość i wysokość viewportu**?” Odpowiedź leży w projektowaniu responsywnym. Media queries takie jak `@media (max-width: 600px)` reagują na wymiary viewportu, a nie na fizyczny rozmiar ekranu. Określając `1280` × `800`, zapewniasz, że strona renderuje układ „desktopowy”, nawet jeśli uruchamiasz kod na serwerze bez wyświetlacza.

```java
sandboxOptions.setViewportWidth(1280);   // set viewport width height
sandboxOptions.setViewportHeight(800);   // set viewport width height
```

Zmiana tych liczb pozwala symulować tablety, telefony czy nawet ultrawide monitory bez opuszczania IDE.

## Full Working Example

Poniżej znajduje się kompletny, gotowy do uruchomienia kod klasy Java, który łączy wszystkie elementy. Skopiuj‑wklej go do pliku o nazwie `SandboxExample.java`, dodaj JAR‑y Aspose.HTML do classpath i uruchom `javac SandboxExample.java && java SandboxExample`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) {
        // Step 1: Define sandbox options – set device DPI and viewport.
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
        sandboxOptions.setViewportWidth(1280);         // set viewport width height
        sandboxOptions.setViewportHeight(800);         // set viewport width height

        // Step 2: Create a DocumentSandbox using the defined options.
        DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);

        // Step 3: Load an HTML document inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 4: Perform normal DOM operations – print the page title.
        System.out.println("Title: " + htmlDoc.getTitle());
    }
}
```

> **Quick verification:**  
> Uruchom program. Jeśli zobaczysz `Title: Example Domain`, wszystko jest poprawnie skonfigurowane. Jeśli nie, sprawdź konsolę pod kątem wyjątków — najczęstsze problemy wynikają z brakujących JAR‑ów lub ograniczeń sieciowych.

## Common Pitfalls & How to Avoid Them

| Symptom | Likely Cause | Fix |
|---|---|---|
| `NullPointerException` on `htmlDoc.getTitle()` | Sandbox failed to load the page | Verify the URL, add a try‑catch around the `HTMLDocument` constructor, or enable logging via `sandboxOptions.setLogLevel(...)`. |
| Layout looks zoomed in/out | DPI not set correctly | Ensure `sandboxOptions.setDeviceDpi(96)` (or your target DPI). |
| Media queries never trigger | Viewport dimensions missing | Double‑check that you called both `setViewportWidth` **and** `setViewportHeight`. |
| Out‑of‑memory error on large pages | Re‑using a single sandbox for many heavy pages | Create a new `DocumentSandbox` per page or call `documentSandbox.dispose()` after use. |

## Extending the Example

Teraz, gdy wiesz, jak **ustawić DPI urządzenia w Aspose** i **ustawić szerokość i wysokość viewportu**, możesz dalej eksperymentować:

- **Capture a screenshot** of the rendered page using `htmlDoc.renderToBitmap(...)`.  
- **Inject custom CSS** before rendering to test dark‑mode themes.  
- **Run JavaScript** inside the sandbox with `htmlDoc.getWindow().eval(...)`.  

Wszystkie te działania respektują DPI i viewport, które skonfigurowałeś, dając Ci niezawodne środowisko testowe dla responsywnych układów.

## Conclusion

Przeszliśmy razem przez zwięzłe, kompleksowe rozwiązanie pokazujące, jak **ustawić DPI urządzenia w Aspose** oraz **ustawić szerokość i wysokość viewportu** przy użyciu sandboxu Aspose.HTML w Javie. Masz teraz solidne podstawy do renderowania stron dokładnie tak, jak wyglądałyby na dowolnym urządzeniu, wszystko w bezpiecznym, odizolowanym środowisku.

Gotowy na kolejny krok? Spróbuj wyrenderować stronę używającą układu CSS Grid lub pobierz zdalny arkusz stylów i zobacz, jak DPI wpływa na renderowanie czcionek. Sandbox daje Ci swobodę eksperymentowania bez wpływu na system hosta.

Jeśli napotkasz problemy, zostaw komentarz poniżej lub sprawdź dokumentację Aspose.HTML for Java — choć wszystko, czego potrzebujesz, jest już tutaj. Szczęśliwego kodowania!  

![set device dpi aspose sandbox diagram](https://example.com/images/set-device-dpi-aspose.png "Diagram przedstawiający konfigurację DPI i viewportu w sandboxie Aspose.HTML")


## What Should You Learn Next?

Poniższe tutoriale obejmują tematy ściśle powiązane, które rozwijają techniki przedstawione w tym przewodniku. Każdy zasób zawiera kompletne, działające przykłady kodu oraz szczegółowe wyjaśnienia, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia w własnych projektach.

- [Create PDF from HTML using Aspose.HTML for Java – Sandbox](/html/english/java/configuring-environment/implement-sandboxing/)
- [Create PDF from HTML – Set User Style Sheet in Aspose.HTML for Java](/html/english/java/configuring-environment/set-user-style-sheet/)
- [How to Set Charset in Aspose.HTML for Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}