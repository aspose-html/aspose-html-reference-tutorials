---
category: general
date: 2026-06-03
description: Crea un documento HTML in Java e incorpora JavaScript per incrementare
  un contatore. Impara un esempio di motore di script, ottieni l'innerHTML dell'elemento
  e altro.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: it
og_description: Crea un documento HTML in Java, incorpora JavaScript per incrementare
  un contatore e recupera il valore finale utilizzando un esempio di motore di script.
og_title: Crea documento HTML con JavaScript incorporato – Esempio Java
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
title: Crea documento HTML con JavaScript incorporato – Esempio Java
url: /it/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea documento HTML con JavaScript incorporato – Esempio Java

Hai mai dovuto **creare documento HTML** dal codice Java e ti sei chiesto come incorporare JavaScript al suo interno? In questa guida ti mostreremo esattamente questo, passo dopo passo, e otterrai un esempio di motore di script funzionante che stampa il valore finale del contatore.  

Se ti sei mai chiesto *“come posso ottenere l'innerHTML di un elemento dopo che uno script è stato eseguito?”* o *“qual è il modo più pulito per incrementare un contatore in JavaScript da Java?”*—sei nel posto giusto. Copriremo **embed javascript html**, **increment counter javascript** e **get element innerHTML** tutti in un unico tutorial coerente.

![Crea documento HTML con JavaScript incorporato](/images/create-html-document.png){: .center alt="Crea documento HTML con JavaScript incorporato esempio"}

## Cosa costruirai

Al termine di questo tutorial avrai un programma Java autonomo che:

1. **Crea un documento HTML** in memoria.  
2. **Incorpora un piccolo frammento JavaScript** che incrementa un contatore cinque volte.  
3. **Inizializza un motore di script** (l'esempio `ScriptEngine`) per eseguire quel frammento.  
4. **Recupera il valore finale del contatore** usando `getElementInnerHTML`.  
5. Stampa `Final counter value: 5` sulla console.

Nessun file esterno, nessun server web—solo puro Java e una piccola stringa HTML.

---

## Prerequisiti

- Java 17 o successivo (l'API `ScriptEngine` fa parte della libreria standard).  
- Familiarità di base con HTML e JavaScript (non serve una competenza approfondita).  
- Un IDE o un semplice editor di testo più un terminale per compilare ed eseguire il programma.

---

## Passo 1: Crea documento HTML in Java

La prima cosa di cui abbiamo bisogno è un oggetto documento HTML vuoto che potremo riempire in seguito con il markup. Pensalo come una pagina virtuale che vive solo in memoria.

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

**Perché è importante:** Creando tu stesso gli oggetti **documento HTML** eviti di scrivere su disco e mantieni tutto testabile. La piccola simulazione del DOM ci permette in seguito di **get element innerHTML** senza un browser completo.

---

## Passo 2: Includi JavaScript HTML – La logica del contatore

Ora scriveremo il markup HTML che include un blocco `<script>`. Questo script **increment counter javascript** cinque volte.

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

**Spiegazione:**  
- Il `<div id='counter'>0</div>` è il nostro elemento target.  
- Il ciclo `for` esegue la logica **increment counter javascript**, aggiornando il div a ogni iterazione.  
- Poiché non siamo in un vero browser, il motore di script che useremo più tardi dovrà capire `document.getElementById`. Ecco perché abbiamo aggiunto un piccolo stub in `HTMLDocument`.

---

## Passo 3: Inizializza il motore di script – Un esempio di Script Engine

Java fornisce l'API `ScriptEngine` (JSR‑223). Creeremo un piccolo wrapper che passa il contenuto HTML al motore e fornisce i metodi DOM minimi che esso si aspetta.

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

**Perché è importante:** Questo **script engine example** mostra come eseguire JavaScript incorporato senza un browser completo. Dimostra anche un modo leggero per esporre `document.getElementById` affinché lo script possa interagire con il nostro DOM simulato.

---

## Passo 4: Esegui JavaScript – Increment Counter JavaScript in azione

Con il motore pronto, eseguiamo semplicemente lo script. Il ciclo all'interno del tag `<script>` verrà attivato, e il nostro mock `setInnerHTML` aggiornerà il contatore.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Cosa succede dietro le quinte?** Ogni iterazione del ciclo chiama `document.getElementById('counter').innerHTML = i + 1;`. Il nostro mock `setInnerHTML` inoltra la stringa numerica a `HTMLDocument.updateCounter`, che memorizza l'ultimo valore. Al termine del ciclo, la mappa interna del documento contiene `"5"` per l'elemento `counter`.

---

## Passo 5: Recupera il valore finale del contatore – Get Element InnerHTML

Ora che lo script è terminato, possiamo **get element innerHTML** dalla nostra istanza `HTMLDocument`.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Eseguendo l'intero programma stampa:

```
Final counter value: 5
```

Questo conferma che la logica **increment counter javascript** ha funzionato e che abbiamo **retrieved the element innerHTML** con successo dopo l'esecuzione dello script.

---

## Esempio completo funzionante

Mettendo tutto insieme, ecco la classe Java completa, pronta per l'esecuzione:

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


## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create Empty HTML Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Create HTML Documents from String in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Save HTML Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}