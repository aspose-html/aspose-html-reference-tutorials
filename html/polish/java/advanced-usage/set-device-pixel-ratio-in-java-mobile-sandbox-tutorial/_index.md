---
category: general
date: 2026-02-10
description: Ustaw współczynnik pikseli urządzenia w Javie przy użyciu piaskownicy
  Aspose.HTML. Dowiedz się, jak ustawić szerokość i wysokość ekranu oraz uzyskać tytuł
  strony w Javie, z kompletnym, działającym przykładem.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: pl
og_description: Ustaw współczynnik pikseli urządzenia w Javie z sandboxem Aspose.HTML.
  Ten przewodnik pokazuje, jak ustawić szerokość i wysokość ekranu oraz pobrać tytuł
  strony w Javie w kilku prostych krokach.
og_title: Ustaw współczynnik pikseli urządzenia w Javie – poradnik Mobile Sandbox
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Ustaw współczynnik pikseli urządzenia w Javie – Poradnik Mobile Sandbox
url: /pl/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ustaw współczynnik pikseli urządzenia w Javie – Mobile Sandbox Tutorial

Kiedykolwiek potrzebowałeś **ustawić współczynnik pikseli urządzenia** podczas testowania responsywnej witryny w Javie? Nie jesteś jedyny. Wielu programistów napotyka problem, gdy strona wygląda idealnie na komputerze, ale psuje się na telefonach z wysoką rozdzielczością DPI. Dobre wieści? Dzięki sandboxowi Aspose.HTML możesz emulować iPhone X (lub dowolne urządzenie) bezpośrednio z kodu Java — bez przeglądarki.

W tym przewodniku przeprowadzimy Cię przez **ustawianie szerokości i wysokości ekranu**, konfigurację **współczynnika pikseli urządzenia** oraz w końcu **pobranie tytułu strony w Javie**, aby zweryfikować, że wszystko zostało poprawnie wyrenderowane. Na końcu będziesz mieć samodzielny program, który możesz wkleić do dowolnego projektu i od razu rozpocząć testowanie układów mobilnych.

## Wymagania wstępne

- Java 8 lub nowsza (kod kompiluje się również z JDK 11)  
- Biblioteka Aspose.HTML for Java (wersja 23.7 lub późniejsza) – możesz ją pobrać z Maven Central  
- IDE lub proste środowisko wiersza poleceń `javac`  
- Dostęp do Internetu dla adresu demo (`https://responsive.example.com`)

Bez dodatkowych frameworków, bez Selenium, tylko czysta Java i Aspose.HTML.

---

## Krok 1: Ustaw szerokość i wysokość ekranu oraz współczynnik pikseli urządzenia

Pierwszą rzeczą, której potrzebujemy, jest obiekt `SandboxOptions`, który informuje sandbox, jakim „urządzeniem” się podajemy. Tutaj użyjemy wymiarów iPhone X (375 × 812 pikseli CSS) oraz **współczynnika pikseli urządzenia** równym 3.0, co odzwierciedla wyświetlacz Retina o wysokim DPI.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Dlaczego to ważne:**  
> Wywołanie `setDevicePixelRatio` skaluje wszystko — od obrazów po renderowanie czcionek — więc strona myśli, że jest na prawdziwym telefonie. Jeśli pominiesz to, układ może przejść na zapytania CSS w stylu desktopowym, co podważa cel testowania mobilnego.

---

## Krok 2: Utwórz instancję sandboxa

Teraz zamieniamy te opcje w działający sandbox. Traktuj sandbox jako małą, bezgłową przeglądarkę, która respektuje zdefiniowane wymiary i współczynnik pikseli.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Wskazówka:** Możesz ponownie używać tego samego obiektu `Sandbox` do wielu ładowań stron; wystarczy zmienić URL, a sandbox zachowa te same cechy urządzenia.

---

## Krok 3: Załaduj stronę w sandboxie

Gdy sandbox jest gotowy, załadowanie strony jest tak proste, jak stworzenie `HTMLDocument` i przekazanie sandboxa jako drugiego argumentu. To wymusza renderowanie dokumentu przy użyciu wirtualnego urządzenia, które ustawiliśmy wcześniej.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Jeśli URL jest nieosiągalny lub strona zawiera błędy, Aspose.HTML zgłosi wyjątek. W kodzie produkcyjnym prawdopodobnie otoczyłbyś to blokiem `try‑catch` i zalogował błąd, ale w tym samouczku pozostajemy przy prostym podejściu.

---

## Krok 4: Weryfikacja za pomocą get page title java

Najszybszym sprawdzeniem jest odczytanie tytułu dokumentu. Jeśli sandbox poprawnie zastosował **współczynnik pikseli urządzenia**, tytuł będzie identyczny z tym, który zobaczyłbyś na prawdziwym iPhone X.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Oczekiwany wynik (przykład):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Jeśli zobaczysz wydrukowany tytuł, udało Ci się pomyślnie **ustawić współczynnik pikseli urządzenia**, **ustawić szerokość i wysokość ekranu** oraz **pobrać tytuł strony** przy użyciu Javy.

---

## Pełny, gotowy do uruchomienia przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do pliku o nazwie `SandboxDemo.java`. Upewnij się, że pliki JAR Aspose.HTML znajdują się na ścieżce klas (`-cp`), zanim skompilujesz.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Skompiluj i uruchom:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Powinieneś zobaczyć wydrukowany tytuł w konsoli, co potwierdza, że strona została wyrenderowana z żądanym **współczynnikiem pikseli urządzenia**.

---

## Najczęściej zadawane pytania i przypadki brzegowe

| Pytanie | Odpowiedź |
|----------|--------|
| **Czy mogę zmienić współczynnik pikseli w czasie działania?** | Tak — wystarczy utworzyć nowy `SandboxOptions` z inną wartością `setDevicePixelRatio` i zainicjować nowy `Sandbox`. Ponowne użycie tego samego sandboxa po zmianie jego opcji nie jest obsługiwane. |
| **Co zrobić, jeśli muszę testować wiele urządzeń?** | Iteruj po liście `SandboxOptions` (np. iPhone 8, Pixel 4) i wykonuj tę samą logikę ładowania i pobierania tytułu dla każdego. |
| **Czy to działa z witrynami HTTPS posiadającymi własne certyfikaty?** | Aspose.HTML respektuje domyślny magazyn zaufanych certyfikatów SSL Javy. Dodaj certyfikat do keystore JVM lub wyłącz weryfikację tylko do testów (niezalecane w produkcji). |
| **Jak zrobić zrzut ekranu zamiast tylko tytułu?** | API `HTMLDocument` udostępnia metody `save`, które mogą eksportować wyrenderowaną stronę do PNG lub JPEG. Użyj `htmlDoc.save("output.png", SaveFormat.PNG);` po załadowaniu. |
| **Czy sandbox jest bezpieczny wątkowo?** | Każda instancja `Sandbox` jest izolowana, ale nie powinno się współdzielić jednej instancji pomiędzy wieloma wątkami bez synchronizacji. |

---

## Przegląd wizualny

![Diagram przedstawiający ustawienie współczynnika pikseli urządzenia w sandboxie mobilnym](https://example.com/images/sandbox-diagram.png "diagram ustawienia współczynnika pikseli urządzenia")

*Powyższa ilustracja przedstawia przepływ od konfiguracji `SandboxOptions` (w tym **ustawianie szerokości i wysokości ekranu** oraz **ustawianie współczynnika pikseli urządzenia**) po załadowanie URL i wyodrębnienie tytułu.*

---

## Zakończenie

Teraz wiesz **jak ustawić współczynnik pikseli urządzenia** w Javie, jak **ustawić szerokość i wysokość ekranu** dla dokładnej emulacji mobilnej oraz jak **pobrać tytuł strony w Javie**, aby potwierdzić, że renderowanie się powiodło. Ten zwięzły przepływ eliminuje potrzebę ciężkich przeglądarek podczas automatycznych testów UI i łatwo wpasowuje się w potoki CI.

Gotowy na kolejny krok? Spróbuj wyeksportować wyrenderowaną stronę jako obraz, lub eksperymentuj z debugowaniem zapytań mediów CSS, przełączając `devicePixelRatio` między 1.0 a 3.0. Możesz także zbadać funkcje konwersji PDF w Aspose.HTML, aby uzyskać wersję do druku widoku mobilnego.

Szczęśliwego kodowania i niech Twoje układy mobilne zawsze wyglądają ostro — bez względu na gęstość pikseli!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}