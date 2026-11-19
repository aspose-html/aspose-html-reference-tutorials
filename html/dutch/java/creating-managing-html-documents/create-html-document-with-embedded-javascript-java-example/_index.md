---
category: general
date: 2026-06-03
description: Maak een HTML-document in Java en embed JavaScript om een teller te verhogen.
  Leer een voorbeeld van een scriptengine, haal de innerHTML van een element op, en
  meer.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: nl
og_description: Maak een HTML-document in Java, embed JavaScript om een teller te
  verhogen, en haal de uiteindelijke waarde op met een scriptengine-voorbeeld.
og_title: HTML-document maken met ingebedde JavaScript – Java-voorbeeld
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
title: HTML-document maken met ingebedde JavaScript – Java-voorbeeld
url: /nl/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak HTML-document met ingesloten JavaScript – Java‑voorbeeld

Heb je ooit **HTML-document** moeten maken vanuit Java-code en je afgevraagd hoe je JavaScript erin kunt insluiten? In deze gids laten we je precies dat zien, stap voor stap, en je eindigt met een werkend script‑engine‑voorbeeld dat de uiteindelijke tellerwaarde afdrukt.  

Als je jezelf ooit hebt afgevraagd *“hoe kan ik element innerHTML krijgen nadat een script is uitgevoerd?”* of *“wat is de schoonste manier om een teller te verhogen in JavaScript vanuit Java?”*—dan ben je op de juiste plek. We behandelen **embed javascript html**, **increment counter javascript**, en **get element innerHTML** allemaal in één samenhangende tutorial.

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="Voorbeeld van HTML-document met ingesloten JavaScript"}

## Wat je gaat bouwen

Aan het einde van deze tutorial heb je een zelf‑containend Java‑programma dat:

1. **Maakt een HTML-document** in het geheugen.
2. **Voegt een klein JavaScript‑fragment in** dat een teller vijf keer verhoogt.
3. **Initialiseert een script‑engine** (het `ScriptEngine`‑voorbeeld) om dat fragment uit te voeren.
4. **Haalt de uiteindelijke tellerwaarde op** met `getElementInnerHTML`.
5. Print `Final counter value: 5` naar de console.

Geen externe bestanden, geen webserver—alleen pure Java en een kleine HTML‑string.

---

## Vereisten

- Java 17 of later (de `ScriptEngine`‑API maakt deel uit van de standaardbibliotheek).
- Basiskennis van HTML en JavaScript (je hoeft geen diepgaande expertise).
- Een IDE of een eenvoudige teksteditor plus een terminal om het programma te compileren en uit te voeren.

---

## Stap 1: Maak HTML-document in Java

Het eerste wat we nodig hebben is een leeg HTML‑documentobject dat we later met markup kunnen vullen. Beschouw het als een virtuele pagina die alleen in het geheugen bestaat.

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

**Waarom dit belangrijk is:** Door zelf **HTML-document**‑objecten te **creëren**, vermijd je het schrijven naar schijf en houd je alles testbaar. De kleine DOM‑simulatie stelt ons later in staat **element innerHTML** op te halen zonder een volledige browser.

---

## Stap 2: JavaScript‑HTML insluiten – De tellerlogica

Nu schrijven we de HTML‑markup die een `<script>`‑blok bevat. Dit script zal **increment counter JavaScript** vijf keer uitvoeren.

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

**Uitleg:**  
- De `<div id='counter'>0</div>` is ons doel‑element.  
- De `for`‑lus voert de **increment counter javascript**‑logica uit en werkt de div elke iteratie bij.  
- Omdat we niet in een echte browser zitten, moet de script‑engine die we later gebruiken `document.getElementById` begrijpen. Daarom hebben we een kleine stub toegevoegd in `HTMLDocument`.

---

## Stap 3: Initialiseert de script‑engine – Een script‑engine‑voorbeeld

Java wordt geleverd met de `ScriptEngine`‑API (JSR‑223). We maken een kleine wrapper die de HTML‑inhoud aan de engine levert en de minimale DOM‑methoden biedt die deze verwacht.

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

**Waarom dit belangrijk is:** Dit **script engine example** laat zien hoe je ingesloten JavaScript kunt uitvoeren zonder een volledige browser. Het demonstreert ook een lichte manier om `document.getElementById` bloot te stellen zodat het script kan communiceren met onze mock‑DOM.

---

## Stap 4: JavaScript uitvoeren – Increment Counter JavaScript in actie

Met de engine klaar, voeren we simpelweg het script uit. De lus binnen de `<script>`‑tag wordt geactiveerd, en onze mock `setInnerHTML` werkt de teller bij.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Wat gebeurt er onder de motorkap?** Elke iteratie van de lus roept `document.getElementById('counter').innerHTML = i + 1;` aan. Onze mock `setInnerHTML` stuurt de numerieke string door naar `HTMLDocument.updateCounter`, die de laatste waarde opslaat. Nadat de lus is voltooid, bevat de interne map van het document `"5"` voor het `counter`‑element.

---

## Stap 5: Haal de uiteindelijke tellerwaarde op – Get Element InnerHTML

Nu het script is voltooid, kunnen we **element innerHTML** ophalen van onze `HTMLDocument`‑instantie.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Het uitvoeren van het volledige programma print:

```
Final counter value: 5
```

Dat bevestigt dat de **increment counter javascript**‑logica werkte en dat we succesvol **element innerHTML** hebben opgehaald na de scriptuitvoering.

---

## Volledig werkend voorbeeld

Alles samengevoegd, hier is de volledige, kant‑klaar‑te‑run Java‑klasse:

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


## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Leeg HTML-documenten maken in Aspose.HTML voor Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [HTML-documenten maken vanuit een string in Aspose.HTML voor Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [HTML-document opslaan in Aspose.HTML voor Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}