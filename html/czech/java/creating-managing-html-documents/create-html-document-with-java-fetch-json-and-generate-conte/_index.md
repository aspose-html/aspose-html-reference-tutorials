---
category: general
date: 2026-02-11
description: Vytvořte HTML dokument v Javě pomocí Aspose.HTML. Naučte se, jak načíst
  JSON JavaScript, přidat element script, generovat HTML z JSON a převést JSON na pre.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: cs
og_description: Vytvořte HTML dokument v Javě s Aspose.HTML. Načtěte JSON JavaScript,
  přidejte element script, vygenerujte HTML z JSON a převěďte JSON na pre — vše v
  jednom tutoriálu.
og_title: Vytvořte HTML dokument v Javě – kompletní průvodce
tags:
- Aspose.HTML
- Java
- Web Automation
title: Vytvořte HTML dokument v Javě – načtěte JSON a generujte obsah
url: /cs/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření HTML dokumentu – Kompletní Java tutoriál

Už jste někdy potřebovali **create HTML document** za běhu, ale nebyli jste si jisti, jak do něj načíst vzdálená data? Nejste v tom sami. V mnoha projektech budete chtít načíst JSON pomocí JavaScriptu, vložit výsledek do stránky a poté uložit finální značkování jako statický soubor. Tento průvodce vám přesně ukáže, jak to provést pomocí Aspose.HTML pro Java.

Provedeme vás každým krokem: od vytvoření prázdného dokumentu, přes **fetch JSON JavaScript**, až po **add script element**, a nakonec **generate HTML from JSON** a **convert JSON to pre** tagy. Na konci budete mít připravený `fetchResult.html`, který obsahuje načtená data vykreslená jako hezky formátovaný JSON.

## Požadavky

- Java 17 nebo novější (kód se také kompiluje s JDK 11+)
- Aspose.HTML for Java knihovna (k dispozici přes Maven Central)
- Základní znalost HTML a async JavaScriptu
- IDE nebo čistý příkazový řádek `javac`/`java`

Není potřeba žádné další frameworky – vše běží lokálně.

## Krok 1: Nastavení projektu a import Aspose.HTML

Nejprve přidejte závislost Aspose.HTML do vašeho `pom.xml` (nebo si JAR stáhněte ručně).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Pro tip:** Udržujte číslo verze aktuální; novější vydání opravují chyby a vylepšují skriptovací engine.

## Krok 2: **Create HTML Document** – prázdné plátno

Začneme vytvořením prázdného `HTMLDocument`. Považujte ho za čistou stránku, do které později vložíme náš skript.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Proč potřebujeme objekt dokumentu? `ScriptEngine` z Aspose.HTML pracuje s DOM, ne s prostým řetězcem. Vytvořením správného dokumentu poskytneme engine skutečné prostředí pro spuštění našeho **fetch JSON JavaScript**.

## Krok 3: Napsání JavaScript úryvku – **Fetch JSON JavaScript** a **Convert JSON to pre**

Jádro tutoriálu spočívá v tomto víceřádkovém řetězci. Provádí asynchronní `fetch`, parsuje JSON a poté zapíše element `<pre>` s hezky formátovanými daty.

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

Všimněte si komentáře *Convert JSON to <pre>* – to je přesně to, co dělá volání `JSON.stringify(..., null, 2)`. Přidává odsazení, čímž je výstup čitelný pro člověka.

## Krok 4: **Add Script Element** do dokumentu

Nyní vytvoříme tag `<script>`, vložíme do něj náš kód a připojíme jej k tělu (`body`). Toto je část **add script element**.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Proč jej připojit k tělu? Ve skutečném prohlížeči by se skript spustil okamžitě po načtení. Připojením k DOM napodobíme toto chování, čímž zajistíme, že asynchronní fetch běží, když později spustíme engine.

## Krok 5: Spuštění Script Engine – nechte asynchronní fetch dokončit

Aspose.HTML poskytuje `ScriptEngine`, který může spouštět DOM‑založený JavaScript. Zavoláme `run()` a čekáme, až se řetězec promise vyřeší.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

Engine blokuje, dokud nejsou vyřešeny všechny nevyřízené úkoly (náš fetch), což zaručuje, že vygenerované HTML již obsahuje data.

## Krok 6: **Generate HTML from JSON** – uložení výsledku

Nakonec dokument uložíme na disk. Soubor nyní obsahuje blok `<pre>` s JSON payload.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

Spuštěním programu vznikne `fetchResult.html`. Otevřete jej v libovolném prohlížeči a uvidíte něco jako:

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

To je výsledek **generate HTML from JSON**, který jste hledali.

## Kompletní funkční příklad

Níže je kompletní, připravený ke spuštění zdrojový soubor. Zkopírujte, vložte, upravte výstupní cestu a spusťte `java JsFetchExample`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## Očekávaný výstup a ověření

1. **Console:** Uvidíte `HTML with fetched data saved.`  
2. **File (`fetchResult.html`):** Po otevření zobrazí JSON uvnitř `<pre>` bloku, pěkně odsazený.  
3. **Validation:** Pokud zobrazíte zdroj stránky, najdete pouze element `<pre>` – žádné další script tagy nezůstaly, protože engine je již vykonal.

## Často kladené otázky a okrajové případy

| Question | Answer |
|----------|--------|
| *Co když API vrátí chybu?* | Zabalte volání `fetch` do `try…catch` bloku a místo JSON zapište chybovou zprávu do těla. |
| *Mohu načíst více zdrojů?* | Ano – stačí řetězit další volání `await fetch(...)` nebo použít `Promise.all`. Konečný `innerHTML` může spojit několik `<pre>` bloků. |
| *Potřebuji nastavit CORS hlavičky?* | Protože skript běží v sandboxu Aspose.HTML, respektuje politiku stejného původu. Veřejný endpoint JSONPlaceholder již umožňuje cross‑origin požadavky. |
| *Jak změnit výstupní adresář za běhu?* | Předávejte cestu jako argument příkazové řádky (`args[0]`) a nahraďte pevně zakódovaný řetězec v `htmlDoc.save`. |
| *Je možné vložit CSS pro stylování?* | Určitě. Vytvořte element `<style>`, nastavte jeho `textContent` na váš CSS a připojte jej do `<head>` před spuštěním engine. |

## Tipy pro produkční použití

- **Cache the JSON** pokud je endpoint pomalý; můžete načtený řetězec zapsat do souboru a znovu jej použít.
- **Sanitize the data** před jeho vložením, zejména pokud zdroj není důvěryhodný. Používejte `JSON.stringify` bezpečně nebo escapujte HTML entity.
- **Configure the ScriptEngine timeout** (`scriptEngine.setTimeout(5000)`) aby nedošlo k zablokování při neodpovídajících službách.

## Vizualizovaný souhrn

![příklad vytvoření html dokumentu zobrazující vygenerované HTML s JSON uvnitř pre tagu](fetchResult.png "Snímek obrazovky vygenerovaného HTML dokumentu")

*Alt text:* *příklad vytvoření html dokumentu – vygenerovaný HTML soubor zobrazující načtený JSON uvnitř pre elementu.*

## Závěr

Nyní víte, jak programově v Javě **create HTML document**, **fetch JSON JavaScript**, **add script element**, **generate HTML from JSON** a **convert JSON to pre** pro čitelný výstup. celý workflow běží offline, vyžaduje pouze Aspose.HTML a vytváří čistý statický soubor, který můžete nasadit kdekoli.

Dále zkuste rozšířit skript tak, aby procházel pole objektů, přidal CSS stylování nebo vytvořil více stránek pomocí stejné techniky. Můžete také nahradit URL v `fetch` svou vlastní API, abyste proměnili dynamická data na statické snímky – ideální pro SEO‑přátelské předrenderování.

Šťastné programování a neváhejte sdílet své experimenty v komentářích!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}