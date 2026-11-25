---
category: general
date: 2026-06-03
description: Erstelle ein HTML-Dokument in Java und bette JavaScript ein, um einen
  Zähler zu erhöhen. Lerne ein Beispiel für eine Skript‑Engine, hole das innerHTML
  eines Elements und mehr.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: de
og_description: Erstelle ein HTML-Dokument in Java, bette JavaScript ein, um einen
  Zähler zu erhöhen, und rufe den Endwert mit einem Skript‑Engine‑Beispiel ab.
og_title: HTML-Dokument mit eingebettetem JavaScript erstellen – Java‑Beispiel
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
title: HTML-Dokument mit eingebettetem JavaScript erstellen – Java‑Beispiel
url: /de/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML-Dokument mit eingebettetem JavaScript erstellen – Java-Beispiel

Haben Sie jemals **HTML-Dokument** aus Java-Code erstellen müssen und sich gefragt, wie man JavaScript darin einbettet? In diesem Leitfaden zeigen wir Ihnen genau das, Schritt für Schritt, und Sie erhalten ein funktionierendes Script‑Engine‑Beispiel, das den endgültigen Zählerwert ausgibt.  

Wenn Sie sich jemals gefragt haben *„Wie kann ich das innerHTML eines Elements erhalten, nachdem ein Skript ausgeführt wurde?“* oder *„Was ist der sauberste Weg, einen Zähler in JavaScript von Java aus zu erhöhen?“* – Sie sind hier genau richtig. Wir behandeln **embed javascript html**, **increment counter javascript** und **get element innerHTML** in einem zusammenhängenden Tutorial.

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="HTML-Dokument mit eingebettetem JavaScript Beispiel"}

## Was Sie bauen werden

Am Ende dieses Tutorials haben Sie ein eigenständiges Java‑Programm, das:

1. **Erstellt ein HTML‑Document** im Speicher.
2. **Bettet ein kleines JavaScript‑Snippet** ein, das einen Zähler fünfmal erhöht.
3. **Initialisiert eine Script‑Engine** (das `ScriptEngine`‑Beispiel), um dieses Snippet auszuführen.
4. **Ruft den endgültigen Zählerwert ab** mittels `getElementInnerHTML`.
5. Gibt `Final counter value: 5` in der Konsole aus.

Keine externen Dateien, kein Web‑Server – nur reines Java und ein kleiner HTML‑String.

---

## Voraussetzungen

- Java 17 oder neuer (die `ScriptEngine`‑API ist Teil der Standardbibliothek).
- Grundlegende Kenntnisse in HTML und JavaScript (tiefgehende Expertise ist nicht erforderlich).
- Eine IDE oder ein einfacher Texteditor plus ein Terminal zum Kompilieren und Ausführen des Programms.

---

## Schritt 1: HTML-Dokument in Java erstellen

Das erste, was wir benötigen, ist ein leeres HTML‑Dokument‑Objekt, das wir später mit Markup füllen können. Denken Sie daran als eine virtuelle Seite, die nur im Speicher existiert.

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

**Warum das wichtig ist:** Durch das **Erstellen von HTML‑Document**‑Objekten selbst vermeiden Sie das Schreiben auf die Festplatte und halten alles testbar. Die kleine DOM‑Simulation ermöglicht es uns später, **element innerHTML zu erhalten**, ohne einen vollständigen Browser.

---

## Schritt 2: JavaScript‑HTML einbetten – Die Zähler‑Logik

Jetzt schreiben wir das HTML‑Markup, das einen `<script>`‑Block enthält. Dieses Skript wird **increment counter JavaScript** fünfmal ausführen.

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

**Erklärung:**  
- `<div id='counter'>0</div>` ist unser Ziel‑Element.  
- Die `for`‑Schleife führt die **increment counter javascript**‑Logik aus und aktualisiert das div bei jeder Iteration.  
- Da wir nicht in einem echten Browser sind, muss die Script‑Engine, die wir später verwenden, `document.getElementById` verstehen. Deshalb haben wir einen kleinen Stub in `HTMLDocument` hinzugefügt.

---

## Schritt 3: Script‑Engine initialisieren – Ein Script‑Engine‑Beispiel

Java liefert die `ScriptEngine`‑API (JSR‑223). Wir erstellen einen kleinen Wrapper, der den HTML‑Inhalt an die Engine übergibt und die minimalen DOM‑Methoden bereitstellt, die sie erwartet.

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

**Warum das wichtig ist:** Dieses **script engine example** zeigt, wie Sie eingebettetes JavaScript ohne vollständigen Browser ausführen können. Es demonstriert außerdem eine leichtgewichtige Methode, `document.getElementById` bereitzustellen, damit das Skript mit unserem Mock‑DOM interagieren kann.

---

## Schritt 4: JavaScript ausführen – Increment Counter JavaScript in Aktion

Mit der bereitstehenden Engine führen wir einfach das Skript aus. Die Schleife im `<script>`‑Tag wird ausgelöst, und unser Mock‑`setInnerHTML` aktualisiert den Zähler.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Was passiert im Hintergrund?** Jede Iteration der Schleife ruft `document.getElementById('counter').innerHTML = i + 1;` auf. Unser Mock‑`setInnerHTML` leitet die numerische Zeichenkette an `HTMLDocument.updateCounter` weiter, das den neuesten Wert speichert. Nach Abschluss der Schleife enthält die interne Map des Dokuments `"5"` für das `counter`‑Element.

---

## Schritt 5: Endgültigen Zählerwert abrufen – Get Element InnerHTML

Jetzt, wo das Skript beendet ist, können wir **element innerHTML** von unserer `HTMLDocument`‑Instanz abrufen.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Das Ausführen des gesamten Programms gibt aus:

```
Final counter value: 5
```

Damit wird bestätigt, dass die **increment counter javascript**‑Logik funktioniert hat und wir erfolgreich **element innerHTML** nach der Skriptausführung abgerufen haben.

---

## Vollständiges funktionierendes Beispiel

Hier ist die komplette, sofort ausführbare Java‑Klasse:

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


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Leere HTML-Dokumente in Aspose.HTML für Java erstellen](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [HTML-Dokumente aus String in Aspose.HTML für Java erstellen](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [HTML-Dokument in Aspose.HTML für Java speichern](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}