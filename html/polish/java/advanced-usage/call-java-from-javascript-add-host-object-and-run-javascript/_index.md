---
category: general
date: 2026-03-14
description: Dowiedz się, jak wywoływać Javę z JavaScript przy użyciu Aspose.HTML.
  Ten przewodnik pokazuje, jak dodać obiekt hosta, uruchomić JavaScript w Javie i
  logować z JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: pl
og_description: Wywołaj Javę z JavaScript przy użyciu Aspose.HTML. Dodaj obiekt hosta,
  uruchom JavaScript w Javie i loguj z JavaScript w jednym samouczku.
og_title: Wywołaj Javę z JavaScript – Kompletny przewodnik z obiektem hosta
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Wywołaj Javę z JavaScript – dodaj obiekt hosta i uruchom JavaScript w Javie
url: /pl/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wywoływanie Java z JavaScript – Dodawanie obiektu hosta i uruchamianie JavaScript w Javie

Czy kiedykolwiek potrzebowałeś **wywołać Java z JavaScript** w aplikacji Java? Być może tworzysz dynamiczny silnik raportów HTML lub po prostu chcesz udostępnić logger Java skryptowi, którym sterujesz. W tym samouczku pokażemy dokładnie, jak dodać obiekt hosta, uruchomić JavaScript w Javie i nawet **logować z JavaScript** z powrotem do JVM — wszystko przy użyciu Aspose.HTML.

Przejdziemy przez kompletny, gotowy do uruchomienia przykład, który tworzy pusty dokument HTML, wstrzykuje klasę Java `Logger` jako obiekt hosta, wykonuje mały skrypt i wypisuje wynik na konsolę. Nie wymaga zewnętrznej przeglądarki, nie ma żadnej mistycznej „magii” — po prostu czysty kod Java, który możesz skopiować‑wklepać i uruchomić już dziś.

## Prerequisites

- Java 17 (lub dowolny nowszy JDK) zainstalowany i skonfigurowany.
- Biblioteka Aspose.HTML for Java (wersja 23.10 lub nowsza). Można ją pobrać z Maven Central lub ze strony Aspose.
- Prosty IDE lub edytor tekstu; przykład działa również z wiersza poleceń.

> **Pro tip:** Jeśli używasz Maven, dodaj następującą zależność do swojego `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Albo dla Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Teraz, gdy mamy podstawy, przejdźmy do rozwiązania krok po kroku.

## Step 1: Create a Minimal Java Project

Najpierw utwórz nową klasę Java o nazwie `JsHostObjectDemo`. Klasa będzie zawierała naszą metodę `main` oraz definicję obiektu hosta. Trzymanie wszystkiego w jednym pliku sprawia, że samouczek jest samodzielny i łatwy do skopiowania.

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

### Why an `HTMLDocument`?

Klasa `HTMLDocument` z Aspose.HTML uruchamia pełne środowisko skryptowe zgodne z HTML‑5. Nawet jeśli nie ładujemy żadnego kodu HTML, obiekt `window` dokumentu daje dostęp do silnika JavaScript, gdzie odbywa się magia **run JavaScript in Java**.

## Step 2: Add the Host Object – “javaLogger”

Linia

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

wykona ciężką pracę dla wymogu **add host object**. Rejestrując instancję `Logger` pod nazwą `"javaLogger"`, każdy skrypt oceniany w tym dokumencie może wywołać `javaLogger.log(...)`. To jest sedno koncepcji **javascript host object**: most, który pozwala JavaScriptowi sięgnąć do JVM.

### Common Pitfalls

- **Naming collisions** – Jeśli w Twoim skrypcie już istnieje zmienna globalna o nazwie `javaLogger`, obiekt hosta zostanie nadpisany. Wybierz unikalną nazwę.
- **Thread safety** – Obiekt hosta jest współdzielony pomiędzy wykonaniami skryptów w tym samym dokumencie. Jeśli planujesz uruchamiać skrypty równocześnie, upewnij się, że klasa hosta jest wątkowo‑bezpieczna (np. używając `synchronized` lub prymitywów z `java.util.concurrent`).

## Step 3: Write and Execute JavaScript

Skrypt, który przekazujemy do `eval`, jest celowo bardzo mały:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Gdy `document.getWindow().eval(script)` zostanie wywołane, silnik wyszukuje `javaLogger` w swoim globalnym zasięgu, znajduje dodany obiekt Java i wywołuje jego metodę `log` z podanym ciągiem znaków.

### Expected Output

Uruchomienie metody `main` wypisuje następującą linię na konsolę:

```
[JS] Hello from JavaScript!
```

Ta mała linia dowodzi, że udało się **call java from javascript**, a **log from javascript** pojawia się dokładnie tam, gdzie normalnie pojawiłaby się wiadomość `System.out` w Javie.

## Step 4: Extending the Host – More Than Just Logging

Jeśli potrzebujesz udostępnić dodatkową funkcjonalność (np. dostęp do plików, zapytania do bazy danych), po prostu dodaj kolejne metody do klasy `Logger` — albo utwórz zupełnie nową klasę hosta. Oto szybki przykład, który dodatkowo zwraca wartość:

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

Pokazuje to elastyczność wzorca **javascript host object**: możesz udostępnić dowolne API Java, pod warunkiem że typy danych są konwertowalne między Javą a JavaScript (prymitywy, stringi, tablice itp.).

## Step 5: Clean Up Resources

Gdy skończysz pracę ze środowiskiem skryptowym, zwolnij `HTMLDocument`, aby uwolnić zasoby natywne:

```java
document.dispose(); // Important for long‑running applications
```

Pomijanie zwalniania może prowadzić do wycieków pamięci, szczególnie jeśli tworzysz wiele dokumentów w pętli.

## Full Working Example

Poniżej znajduje się kompletny plik źródłowy, który możesz od razu skompilować i uruchomić. Zapisz go jako `JsHostObjectDemo.java`, upewnij się, że JAR Aspose.HTML znajduje się w classpath i uruchom `java JsHostObjectDemo`.

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

To cały przepływ **call java from javascript** w kilku linijkach kodu.

## Frequently Asked Questions

### Does this work on Android?

Aspose.HTML jest czystą biblioteką Java, więc działa na każdej maszynie JVM, w tym na Androidzie (Dalvik/ART). Wystarczy dołączyć JAR i będziesz mieć te same możliwości obiektu hosta.

### What if I need to pass complex objects?

Możesz udostępnić POJO (plain old Java objects) zawierające pola, gettery i settery. Silnik automatycznie zamapuje je na obiekty JavaScript. Dla kolekcji używaj `java.util.List` lub tablic — oba są konwertowalne.

### How does error handling work?

Jeśli skrypt wyrzuci błąd JavaScript, `eval` przekaże `ScriptException`. Owiń wywołanie w blok try‑catch, aby zalogować lub odzyskać kontrolę:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Can I run multiple scripts sequentially?

Oczywiście. Ta sama instancja `HTMLDocument` zachowuje swój globalny zakres, więc możesz wywoływać `eval` wielokrotnie. Pamiętaj tylko o możliwych konfliktach nazw zmiennych między skryptami.

## Best Practices & Tips

- **Name your host objects clearly** — `javaLogger`, `javaUtils` itp. — aby uniknąć nieporozumień.
- **Keep host methods small and side‑effect free** kiedy to możliwe; ułatwia to debugowanie.
- **Dispose of the document** tak szybko, jak skończysz; zwalnia to pamięć natywną przydzieloną przez Aspose.HTML.
- **Validate inputs** pochodzące z JavaScript, szczególnie jeśli skrypty pochodzą z niepewnych źródeł. Traktuj je jak każde inne dane zewnętrzne.

## Conclusion

Masz teraz solidny, kompletny przykład, jak **call java from javascript** poprzez **adding a host object**, **running JavaScript in Java** oraz **logging from JavaScript** przy użyciu Aspose.HTML. Ten wzorzec jest potężny: dowolna usługa Java może być udostępniona skryptom, zamieniając Twoją aplikację Java w lekką platformę skryptową.

Następnie możesz zbadać:

- Wstrzykiwanie pełnej strony HTML i manipulowanie DOM z poziomu JavaScript.
- Użycie obiektu hosta do strumieniowego przesyłania danych z powrotem do Javy (np. serializacja JSON).
- Integrację z innymi silnikami skryptowymi, takimi jak Nashorn czy GraalVM, aby uzyskać szersze wsparcie językowe.

Spróbuj, zmodyfikuj klasy `Logger` lub `Utils` i zobacz, jak daleko możesz posunąć koncepcję **javascript host object** w własnych projektach.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}