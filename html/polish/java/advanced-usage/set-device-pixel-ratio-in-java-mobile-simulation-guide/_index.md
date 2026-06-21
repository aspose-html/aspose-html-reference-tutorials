---
category: general
date: 2026-04-05
description: Dowiedz się, jak ustawić współczynnik pikseli urządzenia w Javie przy
  użyciu piaskownicy Aspose.HTML, ustawić niestandardowy agent użytkownika, symulować
  urządzenie mobilne, uzyskać obliczony styl w Javie oraz pobrać tło elementu.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- simulate mobile device
- get computed style java
- retrieve element background
language: pl
og_description: Ustaw współczynnik pikseli urządzenia w Javie przy użyciu piaskownicy
  Aspose.HTML, ustaw niestandardowy agent użytkownika, symuluj urządzenie mobilne,
  pobierz obliczony styl w Javie i pobierz tło elementu.
og_title: ustaw współczynnik pikseli urządzenia w Javie – przewodnik po symulacji
  mobilnej
tags:
- Aspose.HTML
- Java
- Web testing
title: Ustaw współczynnik pikseli urządzenia w Javie – przewodnik symulacji mobilnej
url: /pl/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-simulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ustaw współczynnik pikseli urządzenia w Javie – przewodnik po symulacji mobilnej

Czy kiedykolwiek potrzebowałeś **ustawić współczynnik pikseli urządzenia** w Javie, aby zobaczyć, jak strona wygląda na telefonie z ekranem Retina? Nie jesteś jedyny. Z Aspose.HTML możesz uruchomić sandbox, **ustawić własny user agent**, a nawet **pobrać tło elementu** – wszystko bez opuszczania IDE.

W tym samouczku przeprowadzimy Cię przez tworzenie sandboxu, który **symuluje zachowanie urządzenia mobilnego**, dostosowuje gęstość pikseli, pobiera obliczone CSS i wypisuje tło nagłówka. Po zakończeniu będziesz mieć kompletny, uruchamialny przykład działający z dowolną responsywną witryną. Bez zewnętrznych narzędzi, tylko czysta Java i biblioteka Aspose.HTML.

## Wymagania wstępne

- Java 17 lub nowsza (kod kompiluje się ze starszymi wersjami, ale zalecana jest 17).
- Aspose.HTML for Java 23.4 lub późniejsza – możesz pobrać plik JAR z Maven Central.
- Umiarkowana znajomość HTML i CSS (nie potrzeba nic zaawansowanego).
- Dostęp do Internetu dla strony demonstracyjnej (`https://example.com/responsive.html`).

> **Wskazówka:** Jeśli pracujesz za korporacyjnym proxy, ustaw właściwości proxy JVM przed uruchomieniem demonstracji.

## Krok 1: Jak **ustawić współczynnik pikseli urządzenia** w sandboxie

Pierwszą rzeczą, którą robisz, jest utworzenie instancji `Sandbox` i podanie jej logicznego rozmiaru viewportu urządzenia, które chcesz naśladować. Następnie używasz `setDevicePixelRatio`, aby poinformować silnik renderujący, że każdy piksel CSS odpowiada dwóm fizycznym pikselom — tak jak w iPhone 6/7/8.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // Create a sandbox that pretends to be a mobile phone
        Sandbox mobileSandbox = new Sandbox();

        // Define the logical screen size (width × height in CSS pixels)
        mobileSandbox.setViewportSize(new Size(375, 667)); // iPhone 6/7/8 dimensions

        // 👇 This is where we **set device pixel ratio** to 2.0
        mobileSandbox.setDevicePixelRatio(2.0);

        // Continue with the rest of the steps…
```

Dlaczego to ważne? Przeglądarki używają współczynnika pikseli urządzenia, aby określić, jak ostre będą obrazy i jak uruchamiają zapytania medialne takie jak `@media (min-device-pixel-ratio: 2)`. Dopasowując współczynnik, uzyskasz wierną reprezentację strony na ekranach o wysokiej gęstości.

## Krok 2: **ustawić własny user agent** dla realistycznych nagłówków żądania

Strony internetowe często serwują różny kod w zależności od ciągu `User‑Agent`. Aby Twój sandbox naprawdę uwierzył, że jest iPhone'em, musisz **ustawić własny user agent**. Zapobiega to przekierowaniu do wersji desktopowej lub otrzymaniu ogólnego fallbacku.

```java
        // Set a realistic iPhone user‑agent string
        mobileSandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1"
        );
```

Zwróć uwagę na podział linii i konkatenację łańcucha — utrzymuje to czytelność długości wiersza. Jeśli pominiesz ten krok, serwer może uznać, że używasz Chrome na komputerze i dostarczyć zupełnie inny układ, co podważa cel testowania **symulującego urządzenie mobilne**.

## Krok 3: Załaduj stronę i **symuluj zachowanie urządzenia mobilnego**

Teraz, gdy sandbox jest skonfigurowany, możesz załadować dowolny responsywny URL. Sandbox automatycznie zastosuje rozmiar viewportu, współczynnik pikseli i user‑agent, które właśnie ustawiłeś, skutecznie **symulując warunki urządzenia mobilnego**.

```java
        // Load the responsive HTML document inside the configured sandbox
        try (HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox)) {

            // From here on we work with the DOM just like a normal browser
```

Jeśli docelowa strona używa leniwego ładowania obrazów lub JavaScriptu zależnego od `window.innerWidth`, wszystko zachowa się dokładnie tak, jak na prawdziwym iPhone'ie. Jest to szczególnie przydatne w pipeline'ach CI, gdzie potrzebne są deterministyczne zrzuty ekranu lub weryfikacja CSS.

## Krok 4: Jak **pobrać obliczony styl w Javie** dla elementu

Gdy dokument zostanie załadowany, możesz zapytać dowolny element i poprosić silnik o jego *obliczone* wartości CSS. W Javie metoda to `getComputedStyle()`. To jest sedno użycia **get computed style java**.

```java
            // Locate the <header> element we want to inspect
            HTMLElement headerElement = htmlDoc.getElementsByTagName("header").item(0);

            // Retrieve the computed CSS style for that element
            CSSStyleDeclaration computedStyle = headerElement.getComputedStyle();

            // Now we can read any property—background‑color, font‑size, etc.
```

Dlaczego nie odczytać po prostu stylu inline? Ponieważ wiele stron ustawia kolory za pomocą zewnętrznych arkuszy stylów lub zapytań medialnych. `getComputedStyle` rozwiązuje wszystko po kaskadzie, dając ostateczną wartość, którą przeglądarka faktycznie wyrenderuje.

## Krok 5: **pobrać tło elementu** i wydrukować wynik

Na koniec wyodrębniamy kolor tła i wyświetlamy go. To demonstruje **retrieve element background** w czystym, jednowierszowym wyrażeniu.

```java
            // Output the background color that the browser would render
            System.out.println("Header background: " + computedStyle.getBackgroundColor());
        }
    }
}
```

Po uruchomieniu programu powinieneś zobaczyć coś podobnego do:

```
Header background: rgb(255, 255, 255)
```

Jeśli strona używa ciemnego nagłówka w wersji mobilnej, wynik to odzwierciedli — dokładnie to, co zobaczysz na urządzeniu z takim samym **ustawionym współczynnikiem pikseli urządzenia**.

## Przegląd wizualny

![Diagram pokazujący, jak ustawiony współczynnik pikseli urządzenia, własny user agent i viewport łączą się w sandboxie Aspose.HTML, aby symulować urządzenie mobilne](https://example.com/images/sandbox-diagram.png)

*Tekst alternatywny obrazu zawiera główne słowo kluczowe, pomagając zarówno robotom wyszukiwarek, jak i czytnikom ekranu.*

## Częste pułapki i jak ich unikać

- **Brak rozmiaru viewportu** – Jeśli pominiesz `setViewportSize`, sandbox domyślnie użyje viewportu o rozmiarze desktopowym i Twoje zapytania medialne nie zostaną uruchomione.
- **Nieprawidłowy współczynnik pikseli** – Użycie `1.0` podważa cel; większość nowoczesnych telefonów używa `2.0` lub `3.0`. Sprawdź specyfikacje urządzenia, jeśli potrzebujesz dokładnego dopasowania.
- **Niezgodności User‑Agent** – Niektóre strony sprawdzają `iPhone` *oraz* wersję `OS`. Trzymaj się pełnego ciągu, jak pokazano w Kroku 2.
- **Błędy ładowania zasobów** – Upewnij się, że sandbox ma dostęp do Internetu; w przeciwnym razie zewnętrzne CSS/JS nie zostaną załadowane, a `getComputedStyle` może zwrócić wartości domyślne.

## Rozszerzanie przykładu

Teraz, gdy możesz **ustawić współczynnik pikseli urządzenia**, **ustawić własny user agent**, **symulować urządzenie mobilne**, **pobrać obliczony styl w Javie** i **pobrać tło elementu**, możesz się zastanawiać, co jeszcze możesz zrobić.

- **Robienie zrzutów ekranu** – Aspose.HTML może renderować sandbox do PNG lub JPEG, idealne do testów regresji wizualnej.
- **Uruchamianie JavaScript** – Sandbox obsługuje wykonywanie skryptów, więc możesz testować dynamiczne zmiany UI.
- **Iterowanie po breakpointach** – Przejdź przez kilka szerokości viewportu i współczynników pikseli, aby zweryfikować responsywny projekt w całym spektrum.

## Zakończenie

Właśnie nauczyłeś się, jak **ustawić współczynnik pikseli urządzenia** w Javie, skonfigurować **własny user agent**, **symulować warunki urządzenia mobilnego**, **pobrać obliczony styl w Javie** oraz **pobrać tło elementu** przy użyciu API sandboxu Aspose.HTML. Pełny fragment kodu powyżej jest gotowy do wklejenia w dowolny projekt Java, skompilowania i uruchomienia.

Śmiało modyfikuj wymiary viewportu, wypróbuj inny URL lub eksperymentuj z innymi właściwościami CSS, takimi jak `font-size` czy `margin`. Ten sam wzorzec działa dla każdego elementu, który chcesz zbadać, czyniąc to podejście wszechstronnym narzędziem w Twoim zestawie do testowania stron internetowych.

Jeśli ten przewodnik okazał się pomocny, rozważ podzielenie się nim z zespołem lub oznaczenie gwiazdką repozytorium Aspose.HTML na GitHubie. Szczęśliwego kodowania i niech Twoje testy pixel‑perfect zawsze przechodzą!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}