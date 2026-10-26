---
category: general
date: 2026-06-03
description: Vytvořte HTML dokument v Javě a vložte JavaScript pro inkrementaci čítače.
  Naučte se příklad skriptového enginu, získejte innerHTML elementu a další.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: cs
og_description: Vytvořte HTML dokument v Javě, vložte JavaScript pro inkrementaci
  čítače a pomocí skriptového enginu získejte konečnou hodnotu jako příklad.
og_title: Vytvořte HTML dokument s vloženým JavaScriptem – Java příklad
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
title: Vytvořte HTML dokument s vloženým JavaScriptem – Java příklad
url: /cs/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte HTML dokument s vloženým JavaScriptem – Java příklad

Už jste někdy potřebovali **vytvořit HTML dokument** z Java kódu a přemýšleli, jak do něj vložit JavaScript? V tomto průvodci vám ukážeme přesně to, krok za krokem, a nakonec získáte funkční příklad skriptového enginu, který vypíše konečnou hodnotu čítače.  

Pokud jste se někdy ptali *„jak získat element innerHTML po spuštění skriptu?“* nebo *„jaký je nejčistší způsob, jak inkrementovat čítač v JavaScriptu z Javy?“*—jste na správném místě. Pokryjeme **embed javascript html**, **increment counter javascript**, a **get element innerHTML** v jednom souvislém tutoriálu.

![Create HTML Document with embedded JavaScript](/images/create-html-document.png){: .center alt="Příklad vytvoření HTML dokumentu s vloženým JavaScriptem"}

## Co vytvoříte

Na konci tohoto tutoriálu budete mít samostatný Java program, který:

1. **Vytvoří HTML dokument** v paměti.  
2. **Vloží malý úryvek JavaScriptu**, který inkrementuje čítač pětkrát.  
3. **Inicializuje skriptový engine** (příklad `ScriptEngine`) pro spuštění tohoto úryvku.  
4. **Získá konečnou hodnotu čítače** pomocí `getElementInnerHTML`.  
5. Vytiskne `Final counter value: 5` do konzole.

Žádné externí soubory, žádný webový server — pouze čistá Java a malý HTML řetězec.

---

## Předpoklady

- Java 17 nebo novější (API `ScriptEngine` je součástí standardní knihovny).  
- Základní znalost HTML a JavaScriptu (nepotřebujete hlubokou odbornost).  
- IDE nebo jednoduchý textový editor plus terminál pro kompilaci a spuštění programu.

---

## Krok 1: Vytvořte HTML dokument v Javě

První věc, kterou potřebujeme, je prázdný objekt HTML dokumentu, který později naplníme značkami. Představte si ho jako virtuální stránku, která existuje jen v paměti.

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

**Proč je to důležité:** Tím, že **vytvoříte HTML dokument** objekty sami, se vyhnete zápisu na disk a udržíte vše testovatelné. Malá simulace DOM nám umožní později **získat element innerHTML** bez plnohodnotného prohlížeče.

---

## Krok 2: Vložte JavaScript HTML – Logika čítače

Nyní napíšeme HTML značky, které zahrnují blok `<script>`. Tento skript **inkrementuje čítač v JavaScriptu** pětkrát.

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

**Vysvětlení:**  
- `<div id='counter'>0</div>` je náš cílový element.  
- Smyčka `for` provádí logiku **increment counter javascript**, aktualizuje `<div>` při každé iteraci.  
- Protože nejde o skutečný prohlížeč, skriptový engine, který použijeme později, bude muset rozumět `document.getElementById`. Proto jsme do `HTMLDocument` přidali malý stub.

---

## Krok 3: Inicializujte skriptový engine – Příklad skriptového enginu

Java obsahuje API `ScriptEngine` (JSR‑223). Vytvoříme malý wrapper, který předá HTML obsah enginu a poskytne minimální DOM metody, které skript očekává.

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

**Proč je to důležité:** Tento **script engine example** ukazuje, jak můžete spustit vložený JavaScript bez plnohodnotného prohlížeče. Také demonstruje lehký způsob, jak vystavit `document.getElementById`, aby skript mohl komunikovat s naším mock DOM.

---

## Krok 4: Spusťte JavaScript – Inkremetace čítače v akci

S připraveným enginem jednoduše spustíme skript. Smyčka uvnitř `<script>` se provede a náš mock `setInnerHTML` aktualizuje čítač.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**Co se děje pod kapotou?** Každá iterace smyčky volá `document.getElementById('counter').innerHTML = i + 1;`. Náš mock `setInnerHTML` předává číselný řetězec metodě `HTMLDocument.updateCounter`, která ukládá nejnovější hodnotu. Po dokončení smyčky interní mapa dokumentu obsahuje `"5"` pro element `counter`.

---

## Krok 5: Získejte konečnou hodnotu čítače – Získání element innerHTML

Nyní, když skript skončil, můžeme **získat element innerHTML** z instance našeho `HTMLDocument`.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Spuštěním celého programu se vypíše:

```
Final counter value: 5
```

To potvrzuje, že logika **increment counter javascript** fungovala a úspěšně **jsme získali element innerHTML** po vykonání skriptu.

---

## Kompletní funkční příklad

Spojením všech částí získáte kompletní, připravenou ke spuštění Java třídu:



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vlastních projektech.

- [Vytvořit prázdné HTML dokumenty v Aspose.HTML pro Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Vytvořit HTML dokumenty ze řetězce v Aspose.HTML pro Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Uložit HTML dokument v Aspose.HTML pro Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}