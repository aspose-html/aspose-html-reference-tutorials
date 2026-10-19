---
category: general
date: 2026-10-19
description: Ustaw device pixel ratio w Java przy użyciu Aspose.HTML sandbox. Dowiedz
  się, jak ustawić szerokość i wysokość ekranu oraz pobrać tytuł strony java w pełnym,
  działającym przykładzie.
draft: false
keywords:
- get page title java
- device pixel ratio java
- create virtual device java
- set screen width height
lastmod: 2026-10-19
og_description: Pobierz tytuł strony java z Aspose.HTML sandbox. Ten przewodnik pokazuje,
  jak ustawić szerokość i wysokość ekranu oraz device pixel ratio w Java w kilku prostych
  krokach.
og_image_alt: 'Developer guide: set device pixel ratio in Java using Aspose.HTML sandbox'
og_title: Pobierz tytuł strony java – ustaw device pixel ratio w samouczku Java sandbox
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how
    to set screen width height and get page title java with a complete, runnable example.
  headline: Get page title java – set device pixel ratio in Java sandbox tutorial
  type: TechArticle
- questions:
  - answer: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio`
      value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing
      its options is not supported.
    question: Can I change the pixel ratio at runtime?
  - answer: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run
      the same load‑and‑title logic for each.
    question: What if I need to test multiple devices?
  - answer: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the
      JVM’s keystore or, for testing only, disable verification (not recommended for
      production).
    question: Does this work with HTTPS sites that have self‑signed certificates?
  - answer: The `HTMLDocument` API provides `save` methods that can export the rendered
      page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after
      loading.
    question: How do I capture a screenshot instead of just the title?
  - answer: Each `Sandbox` instance is isolated, but you should avoid sharing a single
      instance across multiple threads without synchronization.
    question: Is the sandbox thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- mobile emulation
title: Pobierz tytuł strony java – ustaw device pixel ratio w samouczku Java sandbox
url: /pl/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pobierz tytuł strony java – ustaw współczynnik pikseli urządzenia w samouczku piaskownicy Java

Czy kiedykolwiek potrzebowałeś **ustawić współczynnik pikseli urządzenia** podczas testowania responsywnej witryny w Javie? Nie jesteś jedyny. Wielu programistów napotyka problem, gdy strona wygląda idealnie na komputerze, ale psuje się na telefonach z wysoką rozdzielczością DPI. Dobre wieści? Dzięki piaskownicy Aspose.HTML możesz emulować iPhone X (lub dowolne urządzenie) bezpośrednio z kodu Java — bez przeglądarki.

W tym przewodniku przejdziemy przez **jak ustawić szerokość i wysokość ekranu**, skonfigurujemy **współczynnik pikseli urządzenia**, a na końcu **get page title java**, aby zweryfikować, że wszystko zostało poprawnie wyrenderowane. Po zakończeniu będziesz mieć samodzielny program, który możesz wkleić do dowolnego projektu i od razu rozpocząć testowanie układów mobilnych.

## Szybkie odpowiedzi
- **Jak ustawić współczynnik pikseli urządzenia w Javie?** Użyj `SandboxOptions.setDevicePixelRatio(double)` przed utworzeniem piaskownicy.  
- **Która metoda zwraca tytuł strony?** Wywołaj `htmlDocument.getTitle()` na załadowanym `HTMLDocument`.  
- **Czy mogę emulować inne urządzenia?** Tak — utwórz nowy `SandboxOptions` z żądaną szerokością, wysokością i współczynnikiem pikseli.  
- **Czy potrzebny jest sterownik przeglądarki?** Nie, piaskownica Aspose.HTML jest bezgłowa i działa wyłącznie w Javie.  
- **Jakiej wersji Aspose.HTML potrzebuję?** Wersja 23.7 lub nowsza obsługuje wszystkie funkcje emulacji mobilnej.

## Co to jest get page title java?
`get page title java` to operacja pobierania elementu `<title>` z dokumentu HTML przy użyciu kodu Java. Pozwala potwierdzić, że strona załadowana w kontekście wirtualnego urządzenia wyrenderowała oczekiwany tytuł. Pobieranie tytułu jest powszechnym krokiem w automatycznej walidacji, aby upewnić się, że właściwa strona została załadowana po zastosowaniu parametrów emulacji urządzenia.

## Dlaczego używać piaskownicy Aspose.HTML do emulacji mobilnej?
Aspose.HTML obsługuje **30+** formatów wejściowych i wyjściowych — w tym HTML, CSS, SVG i PDF — i może renderować strony bez uruchamiania pełnej przeglądarki. Jego piaskownica przetwarza setki‑tysięcy‑stronowe witryny, utrzymując zużycie pamięci poniżej 200 MB, co czyni ją idealną dla potoków CI.

## Wymagania wstępne

- Java 8 lub nowszy (kod kompiluje się również z JDK 11)  
- Biblioteka Aspose.HTML dla Javy (wersja 23.7 lub nowsza) — możesz pobrać ją z Maven Central  
- IDE lub proste środowisko linii poleceń `javac`  
- Dostęp do Internetu dla adresu demonstracyjnego (`https://responsive.example.com`)

Bez dodatkowych frameworków, bez Selenium, tylko czysta Java i Aspose.HTML.

## Jak ustawić szerokość i wysokość ekranu oraz współczynnik pikseli urządzenia w Javie

Klasa `SandboxOptions` pozwala określić wymiary ekranu wirtualnego urządzenia oraz gęstość pikseli. Aby emulować konkretne urządzenie mobilne, musisz skonfigurować piaskownicę z żądaną szerokością, wysokością ekranu i współczynnikiem pikseli urządzenia. Tworząc obiekt `SandboxOptions` i ustawiając te właściwości, silnik renderujący będzie traktował stronę tak, jakby była wyświetlana na tym urządzeniu, zapewniając prawidłowe działanie zapytań media CSS i skalowanie obrazów.

Utwórz instancję `SandboxOptions`, ustaw szerokość na **375**, wysokość na **812**, a współczynnik pikseli urządzenia na **3.0**. Następnie przekaż te opcje do nowego `Sandbox`. To w pełni konfiguruje wirtualne urządzenie przed załadowaniem jakiejkolwiek strony.

Klasa `SandboxOptions` definiuje rozmiar ekranu i gęstość pikseli wirtualnego urządzenia. Jest punktem wyjścia dla każdego scenariusza emulacji mobilnej.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Dlaczego to ważne:**  
> Wywołanie `setDevicePixelRatio` skaluje wszystko — od obrazów po renderowanie czcionek — więc strona myśli, że jest na prawdziwym telefonie. Jeśli pominiesz to, układ może przejść na zapytania media CSS w stylu desktopowym, co podważa cel testowania mobilnego.

## Jak utworzyć instancję piaskownicy

Klasa `Sandbox` reprezentuje środowisko przeglądarki bez interfejsu graficznego, które renderuje HTML przy użyciu wcześniej zdefiniowanych opcji. Po skonfigurowaniu `SandboxOptions` utwórz instancję `Sandbox` z tymi opcjami, aby uzyskać odizolowany kontekst renderowania. Ta piaskownica działa jak lekka przeglądarka, stosując określone rozmiary ekranu i gęstość pikseli, i może być ponownie użyta do wielu ładowań stron, zachowując czystość środowiska.

Utwórz `Sandbox` z wcześniej skonfigurowanymi `SandboxOptions`. Piaskownica zachowuje się jak mała, bezgłowa przeglądarka, respektująca określone wymiary i współczynnik pikseli.

Obiekt `Sandbox` jest odizolowanym silnikiem renderującym Aspose.HTML, działającym bez interfejsu użytkownika. Gwarantuje, że każdy test uruchamiany jest w czystym środowisku.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Pro tip:** Możesz ponownie używać tego samego obiektu `Sandbox` dla wielu ładowań stron; wystarczy zmienić URL, a piaskownica zachowa te same cechy urządzenia.

## Jak załadować stronę w piaskownicy

Klasa `HTMLDocument` reprezentuje przetworzony plik HTML w pamięci, zapewniając dostęp do DOM i możliwości renderowania. Gdy piaskownica jest gotowa, utwórz `HTMLDocument`, przekazując docelowy URL oraz instancję piaskownicy. To ładuje i renderuje stronę przy użyciu ustawień wirtualnego urządzenia, umożliwiając interakcję z DOM lub wyodrębnianie informacji, takich jak tytuł.

Utwórz `HTMLDocument`, przekazując docelowy URL oraz instancję `Sandbox`. To wymusza renderowanie dokumentu przy użyciu wirtualnego urządzenia ustawionego wcześniej.

Klasa `HTMLDocument` reprezentuje przetworzony plik HTML w pamięci i udostępnia metody manipulacji DOM oraz wyodrębniania metadanych.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Jeśli URL jest nieosiągalny lub strona zawiera błędy, Aspose.HTML zgłosi wyjątek. W kodzie produkcyjnym warto otoczyć to blokiem `try‑catch` i zalogować błąd, ale w samouczku pozostajemy przy prostym podejściu.

## Jak zweryfikować przy użyciu get page title java

Metoda `getTitle()` zwraca zawartość elementu `<title>` dokumentu HTML jako zwykły łańcuch znaków. Odczytanie tytułu to najszybsza kontrola poprawności. Po załadowaniu strony wywołaj `htmlDocument.getTitle()`, aby uzyskać tekst tytułu. To proste sprawdzenie potwierdza, że strona została poprawnie wyrenderowana w ustawieniach emulowanego urządzenia i zapewnia szybki sposób walidacji nawigacji lub zmian treści w testach automatycznych.

Wywołaj `htmlDocument.getTitle()` na załadowanym dokumencie i wydrukuj wynik. Jeśli piaskownica poprawnie zastosowała **współczynnik pikseli urządzenia**, tytuł będzie zgodny z tym, co zobaczysz na prawdziwym iPhone X.

Metoda `getTitle()` zwraca zawartość elementu `<title>` jako zwykły łańcuch znaków, umożliwiając walidację renderowania bez wizualnej inspekcji.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Oczekiwany wynik (przykład):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Jeśli zobaczysz wydrukowany tytuł, udało Ci się pomyślnie **ustawić współczynnik pikseli urządzenia**, **ustawić szerokość i wysokość ekranu** oraz **pobrać tytuł strony** przy użyciu Javy.

## Pełny, uruchamialny przykład

Poniżej znajduje się kompletny program, który możesz skopiować i wkleić do pliku o nazwie `SandboxDemo.java`. Upewnij się, że pliki JAR Aspose.HTML znajdują się na ścieżce klas (`-cp` flag) przed kompilacją.

Klasa `SandboxDemo` łączy wszystkie poprzednie kroki w jeden, wykonywalny przykład.

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

Powinieneś zobaczyć tytuł wydrukowany w konsoli, potwierdzający, że strona została wyrenderowana z żądanym **współczynnikiem pikseli urządzenia**.

## Najczęściej zadawane pytania i przypadki brzegowe

**P: Czy mogę zmienić współczynnik pikseli w czasie działania?**  
O: Tak — utwórz nowy `SandboxOptions` z inną wartością `setDevicePixelRatio` i zainstaluj nową `Sandbox`. Ponowne użycie tej samej piaskownicy po zmianie jej opcji nie jest wspierane.

**P: Co zrobić, jeśli muszę testować wiele urządzeń?**  
O: Przejdź w pętli po liście `SandboxOptions` (np. iPhone 8, Pixel 4) i wykonaj tę samą logikę ładowania i pobierania tytułu dla każdego.

**P: Czy to działa z witrynami HTTPS posiadającymi własne certyfikaty?**  
O: Aspose.HTML respektuje domyślny magazyn zaufanych certyfikatów Javy. Dodaj certyfikat do keystore JVM lub, wyłącznie w celach testowych, wyłącz weryfikację (niezalecane w produkcji).

**P: Jak zrobić zrzut ekranu zamiast tylko tytułu?**  
O: API `HTMLDocument` udostępnia metody `save`, które mogą wyeksportować wyrenderowaną stronę do PNG lub JPEG. Użyj `htmlDoc.save("output.png", SaveFormat.PNG);` po załadowaniu.

**P: Czy piaskownica jest bezpieczna wątkowo?**  
O: Każda instancja `Sandbox` jest odizolowana, ale nie należy współdzielić jednej instancji pomiędzy wieloma wątkami bez synchronizacji.

## Przegląd wizualny

![Diagram przedstawiający ustawienie współczynnika pikseli urządzenia w mobilnej piaskownicy](https://example.com/images/sandbox-diagram.png "diagram ustawienia współczynnika pikseli urządzenia")

[Diagram przedstawiający ustawienie współczynnika pikseli urządzenia w mobilnej piaskownicy](https://example.com/images/sandbox-diagram.png "diagram ustawienia współczynnika pikseli urządzenia")

*Ilustracja powyżej przedstawia przepływ od konfiguracji `SandboxOptions` (w tym **ustawienie szerokości i wysokości ekranu** oraz **ustawienie współczynnika pikseli urządzenia**) po załadowanie URL i wyodrębnienie tytułu.*

## Zakończenie

Teraz wiesz, **jak ustawić współczynnik pikseli urządzenia** w Javie, **jak ustawić szerokość i wysokość ekranu** dla dokładnej emulacji mobilnej oraz **jak pobrać tytuł strony java**, aby potwierdzić, że renderowanie zakończyło się sukcesem. Ten zwięzły przepływ pracy eliminuje potrzebę ciężkich przeglądarek podczas automatycznych testów UI i idealnie wpasowuje się w potoki CI.

Gotowy na kolejny krok? Spróbuj wyeksportować wyrenderowaną stronę jako obraz, lub eksperymentuj z debugowaniem zapytań media CSS, przełączając `devicePixelRatio` między 1.0 a 3.0. Możesz także zbadać funkcje konwersji PDF w Aspose.HTML, aby uzyskać wersję do druku widoku mobilnego.

Miłego kodowania i niech Twoje układy mobilne zawsze wyglądają ostro — bez względu na gęstość pikseli!

**Ostatnia aktualizacja:** 2026-10-19  
**Testowano z:** Aspose.HTML 23.7 for Java  
**Autor:** Aspose

## Powiązane samouczki

- [Pobierz tytuł HTML Java renderowanie strony w piaskownicy z szerokością ekranu](/html/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/)
- [Utwórz kompletny przewodnik po piaskownicy Aspose HTML w Javie](/html/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/)
- [Ustaw współczynnik pikseli urządzenia w Javie – kompletny przewodnik](/html/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}