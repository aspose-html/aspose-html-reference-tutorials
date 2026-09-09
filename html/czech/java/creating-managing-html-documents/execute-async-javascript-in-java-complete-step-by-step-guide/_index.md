---
category: general
date: 2026-02-10
description: Naučte se, jak spouštět asynchronní JavaScript v Javě, načíst HTML soubor
  v Javě, číst místní JSON a spouštět JavaScript fetch — vše s Aspose.HTML.
draft: false
keywords:
- execute async javascript
- load html file java
- read local json
- run javascript fetch
language: cs
og_description: Spouštění asynchronního JavaScriptu v Javě je snadné. Postupujte podle
  tohoto tutoriálu, jak načíst HTML soubor v Javě, přečíst místní JSON a spustit JavaScript
  fetch pomocí Aspose.HTML.
og_title: Spouštění asynchronního JavaScriptu v Javě – Kompletní průvodce
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: Spuštění asynchronního JavaScriptu v Javě – kompletní krok‑za‑krokem průvodce
url: /cs/java/creating-managing-html-documents/execute-async-javascript-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# spuštění asynchroního JavaScriptu v Javě – Kompletní průvodce krok za krokem

Už jste někdy potřebovali **spustit asynchronní JavaScript** z Java aplikace, ale nevíte, kde začít? Nejste v tom sami; mnoho vývojářů narazí na tuto překážku při pokusu propojit server‑side Java s client‑side skripty. Dobrou zprávou je, že s Aspose.HTML můžete spustit plnohodnotný `fetch` požadavek, načíst lokální JSON soubor a získat výsledek zpět do vašeho Java kódu—bez prohlížeče.

V tomto tutoriálu vás provedeme načtením HTML souboru v Javě, načtením lokálního JSON payloadu a použitím vzoru `run javascript fetch` pro asynchronní získání dat. Na konci budete mít spustitelný příklad, který vytiskne titulek z JSON do konzole, plus tipy pro zvládání okrajových případů a běžných úskalí.

---

## Co budete potřebovat

- **Java 17** (nebo jakýkoli aktuální JDK; Aspose.HTML funguje s Java 8+)
- **Aspose.HTML for Java** JARs – můžete si stáhnout nejnovější verzi z Maven Central repository nebo z oficiálního Aspose webu.
- Malý **HTML** soubor (`async.html`), který hostí skriptovací engine (může být prázdný, potřebujeme jen dokument).
- **JSON** soubor (`data.json`) umístěný vedle HTML souboru.
- Vaše oblíbené IDE (IntelliJ IDEA, Eclipse, VS Code…) – cokoliv, co vám vyhovuje.

Žádné další frameworky, žádný Node.js, žádné headless prohlížeče. Pouze čistá Java a Aspose.HTML.

---

## Krok 1: Načtení HTML souboru v Javě  

Než budeme moci spustit jakýkoli skript, potřebujeme instanci `HTMLDocument`. Představte si ji jako „prohlížeč“, který žije uvnitř vašeho JVM.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.net.URL;

/* Load the local HTML file – replace YOUR_DIRECTORY with the actual path */
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("file:///YOUR_DIRECTORY/async.html"));
```

> **Proč je tento krok důležitý:**  
> `HTMLDocument` vytvoří DOM, zaregistruje vestavěné objekty (jako `fetch`) a poskytne vám `ScriptEngine` svázaný s tímto dokumentem. Bez dokumentu není kam JavaScript spustit.

---

## Krok 2: Získání JavaScriptového enginu  

Aspose.HTML balí V8‑based engine, který rozumí modernímu ECMAScriptu, včetně `async/await` a `fetch`. Vytáhněte jej z dokumentu:

```java
import com.aspose.html.scripting.ScriptEngine;

/* The engine is automatically linked to the document’s context */
ScriptEngine scriptEngine = htmlDoc.getScriptEngine();
```

> **Pro tip:** Pokud plánujete engine znovu použít napříč více skripty, uchovejte si odkaz místo vytváření nového `HTMLDocument` pokaždé—tím ušetříte paměť a zrychlíte běh.

---

## Krok 3: Spuštění fetch volání pomocí `run javascript fetch`  

Nyní napíšeme skutečný asynchronní JavaScript. Metoda `evaluateAsync` vrací objekt podobný `java.util.concurrent.CompletableFuture`, který se vyřeší na konečnou hodnotu.

```java
/* This script fetches the JSON file, parses it, and extracts the "title" property */
Object titleResult = scriptEngine.evaluateAsync(
        "fetch('YOUR_DIRECTORY/data.json')" +
        ".then(r => r.json())" +
        ".then(d => d.title);"
);
```

> **Co se děje pod kapotou?**  
> - `fetch` načte lokální `data.json` pomocí file URL.  
> - První `.then` převede stream odpovědi na JavaScriptový objekt.  
> - Druhý `.then` vytáhne pole `title`, které je pak marshaled zpět do Javy jako obyčejný `Object`.

Pokud dáváte přednost novějšímu syntaktickému stylu `async/await`, můžete úryvek nahradit tímto:

```java
Object titleResult = scriptEngine.evaluateAsync(
        "(async () => {" +
        "  const r = await fetch('YOUR_DIRECTORY/data.json');" +
        "  const d = await r.json();" +
        "  return d.title;" +
        "})()"
);
```

Obě verze fungují; vyberte si tu, která vašemu týmu čte lépe.

---

## Krok 4: Vytištění načteného titulku  

Nakonec zobrazíme výsledek. `Object` vrácený metodou `evaluateAsync` je již rozbalený, takže stačí jednoduché `toString()`.

```java
System.out.println("Fetched title: " + titleResult);
```

**Očekávaný výstup do konzole** (předpokládáme, že `data.json` obsahuje `{ "title": "Aspose Rocks!" }`):

```
Fetched title: Aspose Rocks!
```

Pokud JSON soubor chybí nebo je poškozený, Aspose.HTML vyhodí `ScriptException`. Zachyťte ji, abyste zabránili zhroucení aplikace:

```java
try {
    Object titleResult = scriptEngine.evaluateAsync(...);
    System.out.println("Fetched title: " + titleResult);
} catch (Exception e) {
    System.err.println("Failed to fetch title: " + e.getMessage());
}
```

---

## Kompletní funkční příklad  

Níže je kompletní, připravený k zkopírování program. Nahraďte `YOUR_DIRECTORY` absolutní cestou ke složce, která obsahuje `async.html` a `data.json`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.net.URL;
import com.aspose.html.scripting.ScriptEngine;

/**
 * Demonstrates how to execute async javascript in Java,
 * load html file java, read local json and run javascript fetch.
 */
public class JsExecution {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load the HTML document from a local file
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("file:///YOUR_DIRECTORY/async.html"));

        // 2️⃣ Obtain the JavaScript engine associated with the document
        ScriptEngine scriptEngine = htmlDoc.getScriptEngine();

        // 3️⃣ Execute an asynchronous fetch that reads the local JSON
        Object titleResult = scriptEngine.evaluateAsync(
                "fetch('YOUR_DIRECTORY/data.json')" +
                ".then(r => r.json())" +
                ".then(d => d.title);"
        );

        // 4️⃣ Output the fetched title
        System.out.println("Fetched title: " + titleResult);
    }
}
```

> **Rychlá kontrola:**  
> - `async.html` může být prázdný soubor `<html></html>`.  
> - `data.json` musí být validní JSON a umístěn přesně tam, kam ukazuje cesta.  
> - Ujistěte se, že file URL používají dopředná lomítka (`/`) i na Windows; schéma `file:///` se postará o konverzi.

---

## Řešení běžných okrajových případů  

| Situace | Na co si dát pozor | Doporučené řešení |
|-----------|-------------------|-----------------|
| **JSON nenalezen** | `fetch` se vyřeší s 404 odpovědí, což vede k odmítnutému promise. | Zabalte skript do `try/catch` bloku nebo před voláním `json()` zkontrolujte `response.ok`. |
| **Velký JSON payload** | Blokuje JVM, zatímco engine parsuje obrovský objekt. | Použijte streaming API (`response.body.getReader()`) uvnitř skriptu, nebo rozdělte soubor na menší části. |
| **Omezení cross‑origin** | I když čteme lokální soubor, Aspose ve výchozím nastavení vynucuje same‑origin politiku. | Nastavte `scriptEngine.getSettings().setAllowFileAccess(true)`, pokud narazíte na chyby oprávnění. |
| **Více asynchronních volání** | Každé `evaluateAsync` vytvoří vlastní řetězec promise, který může být těžko koordinovatelný. | Řetězte volání uvnitř jednoho skriptu nebo použijte `Promise.all` pro paralelní běh. |

---

## Pro tipy a osvědčené postupy  

- **Cacheujte `ScriptEngine`**, pokud budete spouštět mnoho skriptů; tím se vyhnete opakované inicializaci V8 runtime.  
- **Znovu použijte stejný `HTMLDocument`**, když potřebujete manipulovat s DOM (např. dynamicky vkládat skripty).  
- **Logujte surový JavaScript** před vyhodnocením při ladění; syntaktické chyby se projeví jako `ScriptException` s číslem řádku, kde k chybě došlo.  
- **Udržujte JSON malý** pro demonstrační účely. Ve výrobě zvažte kompresi souboru nebo jeho servírování přes HTTP, aby `fetch` mohl využít vestavěné cachování.  
- **Uzamkněte verzi Aspose.HTML** ve vašem `pom.xml`, abyste se vyhnuli neočekávaným breaking changes:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

---

## Vizualizace  

![snímek výsledku spuštění asynchroního JavaScriptu](https://example.com/placeholder.png "výstup konzole spuštění asynchroního JavaScriptu")

*Alt text obrázku:* **spuštění asynchroního JavaScriptu** výstup konzole zobrazující načtený titulek.

---

## Závěr  

Právě jsme ukázali **jak spustit asynchronní JavaScript** z Javy, načíst HTML soubor, přečíst lokální JSON soubor a použít vzor `run javascript fetch` k získání dat zpět do vašeho JVM. Kompletní příklad běží pod jednou sekundou, vyžaduje jen Aspose.HTML a funguje na jakékoli platformě, která podporuje Javu.

Dále můžete zkoumat:

- **Spouštění více fetchů** paralelně pomocí `Promise.all`.  
- **Vkládání vlastních Java objektů** do kontextu skriptu pro bohatší interoperabilitu.  
- **Použití `async/await`** pro čitelnější kód.

Všechny tyto rozšíření stále stojí na jádru – načítání HTML, čtení JSON a spouštění JavaScript fetch – takže už máte základ pro hlubší experimenty.

Máte otázky nebo narazíte na problém? Zanechte komentář a šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}