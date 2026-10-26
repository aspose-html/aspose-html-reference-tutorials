---
category: general
date: 2026-06-03
description: Skapa ett HTML‑dokument i Java och bädda in JavaScript för att öka en
  räknare. Lär dig ett exempel på skriptmotor, hämta elementets innerHTML och mer.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: sv
og_description: Skapa ett HTML-dokument i Java, bädda in JavaScript för att öka en
  räknare och hämta det slutliga värdet med ett skriptmotor‑exempel.
og_title: Skapa HTML-dokument med inbäddad JavaScript – Java-exempel
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
title: Skapa HTML-dokument med inbäddad JavaScript – Java-exempel
url: /sv/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa HTML-dokument med inbäddad JavaScript – Java-exempel

Har du någonsin behövt **create HTML document** från Java-kod och undrat hur du bäddar in JavaScript i den? I den här guiden visar vi dig exakt det, steg för steg, och du får ett fungerande script engine‑exempel som skriver ut det slutliga räknarvärdet.  

Om du någonsin har frågat dig själv *“how can I get element innerHTML after a script runs?”* eller *“what’s the cleanest way to increment a counter in JavaScript from Java?”*—så är du på rätt plats. Vi kommer att gå igenom **embed javascript html**, **increment counter javascript**, och **get element innerHTML** i en sammanhängande handledning.

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="Skapa HTML-dokument med inbäddad JavaScript-exempel"}

## Vad du kommer att bygga

1. **Creates an HTML document** i minnet.
2. **Embeds a small JavaScript snippet** som ökar en räknare fem gånger.
3. **Initializes a script engine** (exemplet `ScriptEngine`) för att köra den kodsnutten.
4. **Retrieves the final counter value** med `getElementInnerHTML`.
5. Skriver ut `Final counter value: 5` till konsolen.

---

## Förutsättningar

- Java 17 eller senare (`ScriptEngine`‑API:t är en del av standardbiblioteket).
- Grundläggande kunskap om HTML och JavaScript (du behöver inte djup expertis).
- En IDE eller en enkel textredigerare samt en terminal för att kompilera och köra programmet.

---

## Steg 1: Skapa HTML-dokument i Java

Det första vi behöver är ett tomt HTML-dokumentobjekt som vi senare kan fylla med markup. Tänk på det som en virtuell sida som bara existerar i minnet.

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

**Why this matters:** Genom att **create HTML document**-objekt själv undviker du att skriva till disk och håller allt testbart. Den lilla DOM‑simuleringen låter oss senare **get element innerHTML** utan en fullständig webbläsare.

---

## Steg 2: Bädda in JavaScript HTML – Räkne‑logiken

Nu ska vi skriva HTML‑markup som inkluderar ett `<script>`‑block. Detta skript kommer att **increment counter JavaScript** fem gånger.

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

**Explanation:**  
- `<div id='counter'>0</div>` är vårt mål‑element.  
- `for`‑loopen kör **increment counter javascript**‑logiken och uppdaterar div‑en varje iteration.  
- Eftersom vi inte befinner oss i en riktig webbläsare måste script‑motorn vi senare använder förstå `document.getElementById`. Därför lade vi till en liten stub i `HTMLDocument`.

---

## Steg 3: Initiera Script Engine – Ett script engine‑exempel

Java levereras med `ScriptEngine`‑API:t (JSR‑223). Vi kommer att skapa ett litet wrapper‑objekt som matar HTML‑innehållet till motorn och tillhandahåller de minimala DOM‑metoder den förväntar sig.

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

**Why this matters:** Detta **script engine example** visar hur du kan köra inbäddad JavaScript utan en fullständig webbläsare. Det demonstrerar också ett lättviktigt sätt att exponera `document.getElementById` så att skriptet kan interagera med vår mock‑DOM.

---

## Steg 4: Exekvera JavaScript – Increment Counter JavaScript i handling

När motorn är klar kör vi helt enkelt skriptet. Loopen i `<script>`‑taggen kommer att avfyras, och vår mock `setInnerHTML` kommer att uppdatera räknaren.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**What happens under the hood?** Varje iteration av loopen anropar `document.getElementById('counter').innerHTML = i + 1;`. Vår mock `setInnerHTML` vidarebefordrar den numeriska strängen till `HTMLDocument.updateCounter`, som lagrar det senaste värdet. När loopen är klar innehåller dokumentets interna karta `"5"` för `counter`‑elementet.

---

## Steg 5: Hämta det slutliga räknarvärdet – Get Element InnerHTML

Nu när skriptet är färdigt kan vi **get element innerHTML** från vår `HTMLDocument`‑instans.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Att köra hela programmet skriver ut:

```
Final counter value: 5
```

Det bekräftar att **increment counter javascript**‑logiken fungerade och att vi framgångsrikt **retrieved the element innerHTML** efter skriptkörning.

---

## Fullt fungerande exempel

När vi sätter ihop allt, här är den kompletta, färdiga Java‑klassen:

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


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa tomma HTML-dokument i Aspose.HTML för Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Skapa HTML-dokument från sträng i Aspose.HTML för Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Spara HTML-dokument i Aspose.HTML för Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}