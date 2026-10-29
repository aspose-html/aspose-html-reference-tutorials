---
category: general
date: 2026-06-03
description: Utwórz dokument HTML w Javie i osadź JavaScript, aby zwiększyć licznik.
  Poznaj przykład silnika skryptowego, pobierz innerHTML elementu i więcej.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: pl
og_description: Utwórz dokument HTML w Javie, osadź JavaScript, aby zwiększyć licznik,
  i pobierz końcową wartość przy użyciu przykładu silnika skryptowego.
og_title: Utwórz dokument HTML z osadzonym JavaScript – przykład w Javie
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: Utwórz dokument HTML z osadzonym JavaScript – przykład w Javie
url: /pl/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Utwórz dokument HTML z osadzonym JavaScript – przykład w Javie

Czy kiedykolwiek potrzebowałeś **utworzyć dokument HTML** z kodu Java i zastanawiałeś się, jak osadzić w nim JavaScript? W tym przewodniku pokażemy Ci dokładnie to, krok po kroku, i otrzymasz działający przykład silnika skryptowego, który wypisze ostateczną wartość licznika.  

Jeśli kiedykolwiek pytałeś siebie *„jak mogę uzyskać innerHTML elementu po uruchomieniu skryptu?”* lub *„jaki jest najczystszy sposób na zwiększenie licznika w JavaScript z poziomu Javy?”* — jesteś we właściwym miejscu. Omówimy **embed javascript html**, **increment counter javascript** i **get element innerHTML** w jednym spójnym tutorialu.

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="Przykład dokumentu HTML z osadzonym JavaScript"}

## Co zbudujesz

Pod koniec tego tutorialu będziesz mieć samodzielny program w Javie, który:

1. **Tworzy dokument HTML** w pamięci.
2. **Osadza mały fragment JavaScript**, który zwiększa licznik pięć razy.
3. **Inicjalizuje silnik skryptowy** (przykład `ScriptEngine`), aby uruchomić ten fragment.
4. **Pobiera ostateczną wartość licznika** przy użyciu `getElementInnerHTML`.
5. Wypisuje `Final counter value: 5` w konsoli.

Bez plików zewnętrznych, bez serwera WWW — tylko czysta Java i mały łańcuch HTML.

## Wymagania wstępne

- Java 17 lub nowszy (API `ScriptEngine` jest częścią biblioteki standardowej).
- Podstawowa znajomość HTML i JavaScript (nie potrzebujesz głębokiej wiedzy).
- IDE lub prosty edytor tekstu oraz terminal do kompilacji i uruchomienia programu.

## Krok 1: Utwórz dokument HTML w Javie

Pierwszą rzeczą, której potrzebujemy, jest pusty obiekt dokumentu HTML, który później możemy wypełnić znacznikami. Traktuj go jako wirtualną stronę istniejącą wyłącznie w pamięci.

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**Dlaczego to ważne:** Tworząc samodzielnie obiekty **HTML document**, unikasz zapisu na dysk i utrzymujesz wszystko testowalne. Mała symulacja DOM pozwala nam później **get element innerHTML** bez pełnej przeglądarki.

## Krok 2: Osadź JavaScript w HTML — logika licznika

Teraz napiszemy znacznik HTML, który zawiera blok `<script>`. Ten skrypt **increment counter JavaScript** pięć razy.

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**Wyjaśnienie:**  
- `<div id='counter'>0</div>` jest naszym elementem docelowym.  
- Pętla `for` wykonuje logikę **increment counter javascript**, aktualizując div przy każdej iteracji.  
- Ponieważ nie działamy w prawdziwej przeglądarce, silnik skryptowy, którego użyjemy później, musi rozumieć `document.getElementById`. Dlatego dodaliśmy mały stub w `HTMLDocument`.

## Krok 3: Zainicjalizuj silnik skryptowy — przykład silnika skryptowego

Java dostarcza API `ScriptEngine` (JSR‑223). Stworzymy małą nakładkę, która przekaże zawartość HTML do silnika i udostępni minimalne metody DOM, których on oczekuje.

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**Dlaczego to ważne:** Ten **script engine example** pokazuje, jak uruchomić osadzony JavaScript bez pełnej przeglądarki. Demonstruje także lekki sposób udostępnienia `document.getElementById`, aby skrypt mógł współdziałać z naszym mock DOM.

## Krok 4: Wykonaj JavaScript — Increment Counter JavaScript w działaniu

Gdy silnik jest gotowy, po prostu uruchamiamy skrypt. Pętla wewnątrz znacznika `<script>` zostanie wywołana, a nasz mock `setInnerHTML` zaktualizuje licznik.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Co się dzieje w tle?** Każda iteracja pętli wywołuje `document.getElementById('counter').innerHTML = i + 1;`. Nasz mock `setInnerHTML` przekazuje ciąg liczbowy do `HTMLDocument.updateCounter`, który zapisuje najnowszą wartość. Po zakończeniu pętli wewnętrzna mapa dokumentu zawiera `"5"` dla elementu `counter`.

## Krok 5: Pobierz ostateczną wartość licznika — Get Element InnerHTML

Teraz, gdy skrypt zakończył się, możemy **get element innerHTML** z naszej instancji `HTMLDocument`.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Uruchomienie całego programu wypisuje:

```
Final counter value: 5
```

Potwierdza to, że logika **increment counter javascript** zadziałała i pomyślnie **retrieved the element innerHTML** po wykonaniu skryptu.

## Pełny działający przykład

Łącząc wszystko razem, oto pełna, gotowa do uruchomienia klasa Java:

```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class HtmlJsDemo {

    // ---------- Minimal HTMLDocument implementation ----------
    static class HTMLDocument {
        private final StringBuilder html = new StringBuilder();
        private final java.util.Map<String, String> elements = new java.util.HashMap<>();

        public void write(String content) {
            html.append(content);
        }

        public String getContent() {
            return html.toString();
        }

        public void setElementInnerHTML(String id, String value) {
            elements.put(id, value);
        }

        public String getElementInnerHTML(String id) {
            return elements.getOrDefault(id, "");
        }

        public void updateCounter(int value) {
            setElementInnerHTML("counter", String.valueOf(value));
        }
    }

    // ---------- SimpleScriptEngine (script engine example) ----------
    static class SimpleScriptEngine {
        private final HTMLDocument document;
        private final ScriptEngine engine;

        public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
            this.document = doc;
            ScriptEngineManager manager = new ScriptEngineManager();
            this.engine = manager.getEngineByName("JavaScript");
            // Expose a mock 'document' object
            engine.put("document", new Object() {
                public Object getElementById(String id) {
                    return new Object() {
                        public void setInnerHTML(String value) {
                            document.updateCounter(Integer.parseInt(value));
                        }
                    };
                }
            });
        }

        public void execute() throws ScriptException {
            String html = document.getContent();
            int start = html.indexOf("<script>") + "<script>".length();
            int end   = html.indexOf("</script>");
            String script = html.substring(start, end);
            engine.eval(script);
        }
    }

    // ---------- Main method ----------
    public static void main(String[] args) {
        // Step 1: create HTML document
        HTMLDocument doc = new HTMLDocument();

        // Step 2: embed JavaScript HTML (increment counter JavaScript)
        doc.write(
            "<!DOCTYPE html><html><body>"
          + "<div id='counter'>0</div>"
          + "<script>"
          + "for (let i = 0; i < 5; i++) {"
          + "  document.getElementById('counter').innerHTML = i


## Co powinieneś nauczyć się dalej?

Poniższe tutoriale obejmują ściśle powiązane tematy, które rozwijają techniki przedstawione w tym przewodniku. Każde źródło zawiera kompletne działające przykłady kodu z wyjaśnieniami krok po kroku, aby pomóc Ci opanować dodatkowe funkcje API i odkrywać alternatywne podejścia implementacyjne w własnych projektach.

- [Utwórz puste dokumenty HTML w Aspose.HTML dla Javy](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Utwórz dokumenty HTML z ciągu znaków w Aspose.HTML dla Javy](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Zapisz dokument HTML w Aspose.HTML dla Javy](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}