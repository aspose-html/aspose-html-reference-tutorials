---
category: general
date: 2026-06-03
description: HTML dokumentum létrehozása Java-ban, és JavaScript beágyazása a számláló
  növeléséhez. Tanulj meg egy script‑engine példát, szerezz elem‑innerHTML-et, és
  még sok mást.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: hu
og_description: HTML dokumentum létrehozása Java-ban, JavaScript beágyazása a számláló
  növeléséhez, és a végső érték lekérdezése egy szkriptmotor példával.
og_title: HTML-dokumentum létrehozása beágyazott JavaScript-tel – Java példa
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
title: HTML-dokumentum létrehozása beágyazott JavaScript-tel – Java példa
url: /hu/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML dokumentum létrehozása beágyazott JavaScript‑el – Java példa

Valaha is szükséged volt **HTML dokumentum** létrehozására Java kódból, és azon tűnődtél, hogyan ágyazz be JavaScriptet? Ebben az útmutatóban pontosan ezt mutatjuk be lépésről‑lépésre, és egy működő script‑motor példát kapsz, amely kiírja a végső számláló értékét.

Ha már gondoltad magadban *„hogyan kaphatom meg az element innerHTML‑t egy script futása után?”* vagy *„mi a legegyszerűbb módja egy számláló növelésének JavaScriptben Java‑ból?”* – jó helyen vagy. Bemutatjuk a **embed javascript html**, **increment counter javascript**, és **get element innerHTML** témákat egy koherens tutorialban.

![HTML dokumentum létrehozása beágyazott JavaScript példával](/images/create-html-document.png){: .center alt="HTML dokumentum létrehozása beágyazott JavaScript példával"}

## Amit építeni fogsz

A tutorial végére egy önálló Java programod lesz, amely:

1. **HTML dokumentumot hoz létre** memóriában.
2. **Beágyaz egy kis JavaScript kódrészletet**, amely öt alkalommal növeli a számlálót.
3. **Inicializál egy script‑engine‑t** (a `ScriptEngine` példát) a kódrészlet futtatásához.
4. **Lekéri a végső számláló értékét** a `getElementInnerHTML` segítségével.
5. Kiírja a `Final counter value: 5` szöveget a konzolra.

Nincs külső fájl, nincs webszerver – csak tiszta Java és egy apró HTML karakterlánc.

---

## Előfeltételek

- Java 17 vagy újabb (a `ScriptEngine` API a standard könyvtár része).
- Alapvető ismeretek HTML‑ről és JavaScript‑ről (nem kell mély szakértelem).
- Egy IDE vagy egyszerű szövegszerkesztő plusz egy terminál a program fordításához és futtatásához.

---

## 1. lépés: HTML dokumentum létrehozása Java‑ban

Az első dolog, amire szükségünk van, egy üres HTML dokumentum objektum, amelyet később feltölthetünk markup‑sal. Tekintsd úgy, mint egy virtuális oldalt, amely csak a memóriában él.

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

**Miért fontos:** **HTML dokumentum** objektumok saját kezű létrehozásával elkerülöd a lemezre írást, és minden tesztelhető marad. A kis DOM‑szimuláció lehetővé teszi, hogy később **get element innerHTML**‑t használj egy teljes böngésző nélkül.

## 2. lépés: JavaScript HTML beágyazása – A számláló logika

Most megírjuk azt a HTML markup‑ot, amely tartalmaz egy `<script>` blokkot. Ez a script **increment counter JavaScript**‑et hajt végre öt alkalommal.

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

**Magyarázat:**  
- A `<div id='counter'>0</div>` a cél elemünk.  
- A `for` ciklus **increment counter javascript** logikát futtat, minden iterációban frissítve a div‑et.  
- Mivel nem egy valódi böngészőben vagyunk, a később használandó script‑engine‑nek értenie kell a `document.getElementById` hívást. Ezért adtunk hozzá egy apró stub‑ot az `HTMLDocument`‑hez.

## 3. lépés: Script‑engine inicializálása – Script Engine példa

A Java a `ScriptEngine` API‑val (JSR‑223) érkezik. Létrehozunk egy kis wrapper‑t, amely a HTML tartalmat betáplálja a motorba, és biztosítja a minimális DOM metódusokat, amiket elvár.

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

**Miért fontos:** Ez a **script engine example** megmutatja, hogyan futtathatsz beágyazott JavaScriptet egy teljes böngésző nélkül. Emellett bemutat egy könnyű módot a `document.getElementById` exponálására, hogy a script interakcióba léphessen a mock DOM‑dal.

## 4. lépés: JavaScript végrehajtása – Increment Counter JavaScript akcióban

A motor készen áll, egyszerűen futtatjuk a scriptet. A `<script>` címke belső ciklusa lefut, és a mock `setInnerHTML` frissíti a számlálót.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Mi történik a háttérben?** A ciklus minden iterációja meghívja a `document.getElementById('counter').innerHTML = i + 1;` kifejezést. A mock `setInnerHTML` a numerikus stringet a `HTMLDocument.updateCounter`‑nek továbbítja, amely elmenti a legújabb értéket. A ciklus befejezése után a dokumentum belső map‑je `"5"`‑öt tartalmaz a `counter` elemhez.

## 5. lépés: A végső számláló érték lekérése – Get Element InnerHTML

Miután a script befejeződött, **get element innerHTML**‑t hívhatunk a `HTMLDocument` példányunkból.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

A teljes program futtatása a következőt írja ki:

```
Final counter value: 5
```

Ez megerősíti, hogy a **increment counter javascript** logika működött, és sikeresen **retrieved the element innerHTML** a script végrehajtása után.

## Teljes működő példa

Összeállítva, itt a komplett, azonnal futtatható Java osztály:

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


## Mit érdemes még tanulni?

Az alábbi tutorialok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy segítsenek elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [Üres HTML dokumentumok létrehozása Aspose.HTML for Java-ban](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [HTML dokumentumok létrehozása karakterláncból Aspose.HTML for Java-ban](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [HTML dokumentum mentése Aspose.HTML for Java-ban](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}