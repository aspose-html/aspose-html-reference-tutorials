---
category: general
date: 2026-10-14
description: Wywołaj java z javascript przy użyciu Aspose.HTML. Dowiedz się, jak dodać
  host object, wykonać javascript w java oraz logować z javascript w zwięzłym tutorialu.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Wywołaj java z javascript przy użyciu Aspose.HTML. Ten przewodnik
  pokazuje, jak dodać host object, wykonać javascript w java oraz logować z javascript,
  wszystko w kilku linijkach kodu.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Wywołaj java z javascript – dodaj host object i uruchom javascript w java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Wywołaj java z javascript – dodaj host object i uruchom javascript w java
url: /pl/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wywołaj Java z JavaScript – dodaj obiekt hosta i uruchom JavaScript w Javie

Czy kiedykolwiek potrzebowałeś **call java from javascript** w aplikacji Java? Może budujesz dynamiczny silnik raportów HTML lub po prostu chcesz udostępnić logger Java skryptowi, którym sterujesz. W tym samouczku zobaczysz dokładnie, jak dodać obiekt hosta, uruchomić JavaScript w Javie i nawet **log from JavaScript** z powrotem do JVM — wszystko przy użyciu Aspose.HTML.

Przejdziemy przez kompletny, działający przykład, który tworzy pusty dokument HTML, wstrzykuje klasę Java `Logger` jako obiekt hosta, wykonuje mały skrypt i wypisuje wynik na konsolę. Nie wymaga zewnętrznej przeglądarki, żadnej mistycznej „magii” — po prostu czysty kod Java, który możesz skopiować‑wkleić i uruchomić już dziś.

## Szybkie odpowiedzi
- **Jak dodać obiekt hosta?** Register a Java instance with `document.getWindow().addHostObject("name", object)`.  
- **Czy mogę wykonać JavaScript w Javie?** Yes—use `document.getWindow().eval(yourScript)`.  
- **Czy logowanie z JavaScript jest możliwe?** Absolutely; the host object can expose any `void log(String)` method.  
- **Jakiej wersji Aspose.HTML potrzebuję?** Version 23.10 or newer supports the full host‑object API.  
- **Czy potrzebuję przeglądarki internetowej?** No—Aspose.HTML provides an embedded engine, so everything runs head‑less.

## Czym jest call java from javascript?
**Call java from javascript** to technika udostępniania obiektów Java środowisku uruchomieniowemu JavaScript, aby skrypty mogły wywoływać metody Java bezpośrednio. Aspose.HTML tworzy lekkie środowisko JavaScript wewnątrz procesu Java, umożliwiając płynną dwukierunkową komunikację bez zewnętrznych przeglądarek.

## Dlaczego używać Aspose.HTML do wykonywania javascript w java?
Aspose.HTML obsługuje **ponad 50 formatów wejścia i wyjścia** i może oceniać JavaScript w w pełni zgodnym środowisku HTML5. Przetwarza skrypty w średnim czasie do 200 ms dla prostego jednowierszowego kodu i robi to bez ładowania pełnego stosu przeglądarki, co zmniejsza zużycie pamięci nawet o 80 % w porównaniu z podejściami opartymi na Selenium.

## Wymagania wstępne

- Java 17 (lub dowolny nowszy JDK) zainstalowany i skonfigurowany.  
- Biblioteka Aspose.HTML for Java (wersja 23.10 lub nowsza). Możesz ją pobrać z Maven Central lub ze strony Aspose.  
- Proste IDE lub edytor tekstu; przykład działa również z wiersza poleceń.

> **Wskazówka:** Jeśli używasz Maven, dodaj następującą zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Lub, dla Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Teraz, gdy podstawy są już ustalone, zanurzmy się w rozwiązanie krok po kroku.

## Jak dodać obiekt hosta i uruchomić javascript w java?
`addHostObject` rejestruje obiekt Java jako zmienną globalną w kontekście JavaScript. Załaduj swój `HTMLDocument`, zarejestruj logger Java pod nazwą "javaLogger" używając `addHostObject`, a następnie oceń krótki skrypt wywołujący `javaLogger.log`. Cały przepływ wymaga tylko trzech wywołań API i działa w dowolnym środowisku Java 17.

### Krok 1: utwórz minimalny projekt java

Najpierw utwórz nową klasę Java o nazwie `JsHostObjectDemo`. Klasa będzie zawierać naszą metodę `main` oraz definicję obiektu hosta. Trzymanie wszystkiego w jednym pliku sprawia, że samouczek jest samodzielny i łatwy do skopiowania.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Dlaczego `HTMLDocument`?

`HTMLDocument` reprezentuje pamięciowy dokument HTML i udostępnia silnik JavaScript. Klasa `HTMLDocument` uruchamia pełne środowisko skryptowe zgodne z HTML‑5. Mimo że nie ładujemy żadnego kodu HTML, obiekt `window` dokumentu daje dostęp do silnika JavaScript, gdzie zachodzi magia **run javascript in java**. Dodatkowo możesz manipulować DOM, ładować zasoby lub oceniać skrypty bez przeglądarki.

## Jak dodać obiekt hosta – „javaLogger”?
`Logger` to prosta klasa Java z metodą `log(String)`, która zapisuje komunikaty na konsolę. Zarejestruj instancję `Logger` pod nazwą "javaLogger", aby każdy skrypt oceniany w tym dokumencie mógł wywołać `javaLogger.log(...)`. To jest sedno wymogu **add host object** i udostępnia logger jako zmienną globalną w kodzie JavaScript.

### Typowe pułapki

- **Kolizje nazw** – Jeśli w swoim skrypcie masz już zmienną globalną o nazwie `javaLogger`, obiekt hosta zostanie nadpisany. Wybierz unikalną nazwę.  
- **Bezpieczeństwo wątków** – Obiekt hosta jest współdzielony pomiędzy wykonywaniami skryptów w tym samym dokumencie. Jeśli planujesz uruchamiać skrypty równocześnie, uczynij klasę hosta bezpieczną wątkowo (np. użyj `synchronized` lub prymitywów z `java.util.concurrent`).

## Jak napisać i wykonać javascript w java?
`eval` wykonuje ciąg znaków JavaScript w silniku skryptowym dokumentu i zwraca dowolny wynik. Przekaż mały skrypt do `eval`. Silnik rozwiązuje `javaLogger` z zakresu globalnego i wywołuje jego metodę `log` z podanym ciągiem. Możesz także zwracać wartości, obsługiwać wyjątki i łączyć wiele ocen dla bardziej złożonych interakcji.

### Oczekiwany wynik

```
[JS] Hello from JavaScript!
```

## Jak rozszerzyć obiekt hosta – więcej niż tylko logowanie?
Obiekt hosta to dowolna instancja Java udostępniona JavaScript poprzez `addHostObject`. Udostępnij dodatkową funkcjonalność, dodając metody do klasy `Logger` lub tworząc nową klasę hosta. Poniżej szybki przykład, który także zwraca wartość do JavaScript. Obiekt hosta może udostępniać złożone typy, wykonywać operacje I/O lub współdziałać z innymi usługami. Zwracając wartość, skrypt może otrzymać dane z powrotem, umożliwiając dwukierunkową komunikację między Javą a JavaScript.

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Teraz konsola wyświetla:

```
[JS] 3+4=7
```

## Jak zwolnić zasoby po uruchomieniu skryptów?
`dispose` zwalnia natywne zasoby trzymane przez instancję `HTMLDocument`. Gdy skończysz korzystać ze środowiska skryptowego, zwolnij `HTMLDocument`, aby uwolnić zasoby natywne. Nie wywołanie `dispose()` może prowadzić do wycieków pamięci, szczególnie przy tworzeniu wielu dokumentów w pętlach lub długotrwałych usługach. Zawsze otaczaj użycie blokiem try‑with‑resources lub upewnij się, że `document.dispose()` jest wywoływane w klauzuli finally.

```java
document.dispose(); // Important for long‑running applications
```

## Pełny działający przykład

Poniżej znajduje się kompletny plik źródłowy, który możesz od razu skompilować i uruchomić. Zapisz go jako `JsHostObjectDemo.java`, upewnij się, że plik JAR Aspose.HTML znajduje się w classpath, i uruchom `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

Uruchomienie tego programu daje:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Najczęściej zadawane pytania

**Q: Czy to działa na Androidzie?**  
A: Tak. Aspose.HTML jest czystą biblioteką Java, więc działa na dowolnej JVM, w tym na środowisku ART Androida.

**Q: Co jeśli muszę przekazać złożone obiekty?**  
A: Możesz udostępnić POJO z getterami i setterami; silnik mapuje je automatycznie na obiekty JavaScript. Kolekcje takie jak `java.util.List` lub tablice również są konwertowalne.

**Q: Jak działa obsługa błędów?**  
A: Jeśli skrypt zgłosi błąd JavaScript, `eval` propaguje `ScriptException`. Otocz wywołanie blokiem try‑catch, aby zalogować lub odzyskać.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: Czy mogę uruchamiać wiele skryptów kolejno?**  
A: Zdecydowanie. Ten sam `HTMLDocument` zachowuje swój zakres globalny, więc możesz wywoływać `eval` wielokrotnie. Po prostu zarządzaj nazwami zmiennych, aby uniknąć konfliktów.

**Q: Czy obiekt hosta jest bezpieczny dla niezaufanych skryptów?**  
A: Traktuj każdy zewnętrzny skrypt jako nieufny. Waliduj parametry i rozważ sandboxowanie, udostępniając tylko niezbędne metody.

## Najlepsze praktyki i wskazówki

- **Nazwij swoje obiekty hosta jasno** — `javaLogger`, `javaUtils` itd. — aby uniknąć nieporozumień.  
- **Utrzymuj metody hosta małe i bez efektów ubocznych** kiedy to możliwe; ułatwia to debugowanie.  
- **Zwolnij dokument** jak tylko skończysz; uwalnia to pamięć natywną przydzieloną przez Aspose.HTML.  
- **Waliduj dane wejściowe** z JavaScript, szczególnie jeśli skrypty pochodzą z nieufnych źródeł. Traktuj je jak każde zewnętrzne dane.

## Zakończenie

Masz teraz solidny, kompletny przykład, jak **call java from javascript** poprzez **dodanie obiektu hosta**, **uruchomienie javascript w java** i **logowanie z javascript** przy użyciu Aspose.HTML. Ten wzorzec jest potężny: dowolna usługa Java może być udostępniona skryptom, przekształcając Twoją aplikację Java w lekką platformę skryptową.

Następnie możesz zbadać:

- Wstrzykiwanie pełnej strony HTML i manipulowanie DOM z JavaScript.  
- Użycie obiektu hosta do przesyłania danych z powrotem do części Java (np. serializacja JSON).  
- Integracja z innymi silnikami skryptowymi, takimi jak Nashorn lub GraalVM, w celu szerszego wsparcia językowego.

Spróbuj, zmodyfikuj klasy `Logger` lub `Utils` i zobacz, jak daleko możesz rozwinąć koncepcję **javascript host object** w swoich własnych projektach.

---

**Ostatnia aktualizacja:** 2026-10-14  
**Testowano z:** Aspose.HTML for Java 23.10  
**Autor:** Aspose  

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Powiązane samouczki

- [Włącz wykonywanie skryptów w Java – kompletny przewodnik Aspose HTML](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Wykonaj JavaScript w Java – kompletny przewodnik uruchamiania JS](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [Jak sandboxować JavaScript – kompletny przewodnik Aspose HTML](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}