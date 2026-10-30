---
category: general
date: 2026-03-04
description: Volání Java z JavaScriptu pomocí Aspose.HTML, spouštění asynchronního
  JavaScriptu a získávání JSON v Javě s jednoduchým příkladem. Naučte se efektivně
  spouštět JavaScriptový engine.
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: cs
og_description: Vyvolejte Java z JavaScriptu pomocí Aspose.HTML, spusťte asynchronní
  JavaScript a načtěte JSON v Javě. Kompletní kód, vysvětlení a tipy jsou zahrnuty.
og_title: Volání Javy z JavaScriptu – krok za krokem tutoriál asynchronního fetch
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: Volání Javy z JavaScriptu – Kompletní průvodce asynchronním fetch a vykonáváním
  JS enginu
url: /cs/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Volání Java z JavaScriptu – Kompletní tutoriál s asynchronním Fetch API

Už jste se někdy zamýšleli, jak **volat Java z JavaScriptu** bez opuštění vaší Java aplikace? Možná vytváříte server‑side HTML renderér, nebo potřebujete zpřístupnit nějakou Java logiku skriptu, který běží uvnitř dokumentu. Dobrou zprávou je, že Aspose.HTML to dělá hračkou. V tomto průvodci vám nejen ukážeme, jak *spustit asynchronní JavaScript* uvnitř dokumentu řízeného Javou, ale také jak **načíst JSON v Javě** pomocí moderního **asynchronního fetch API** a nakonec **bezpečně provést volání JavaScript engine**.

Stručně řečeno získáte kompletní, spustitelný příklad, který stáhne JSON payload z veřejného endpointu, předá jej Java host objektu a vypíše výsledek na konzoli. Žádné externí webové servery, žádné další knihovny – pouze čistá Java a Aspose.HTML.

## Co se naučíte

- Jak vytvořit prázdný HTML dokument pomocí Aspose.HTML.
- Jak získat a **spustit JavaScript engine** z Javy.
- Jak zaregistrovat Java host objekt, který může JavaScript volat.
- Jak napsat **asynchronní JavaScript** funkci využívající **asynchronní fetch API**.
- Jak zpracovat stažená data zpět v Javě pomocí čistého callbacku.
- Očekávaný výstup a tipy na řešení problémů.

### Předpoklady

- Java 17 nebo novější (kód se také kompiluje s JDK 11).
- Aspose.HTML for Java 23.7 (nebo nejnovější verze v době psaní).
- Základní znalost Javy a JavaScript promises.
- Přístup k internetu pro demo požadavek na `jsonplaceholder`.

Pokud vám některý z těchto bodů není známý, nepanikařte – každý krok je vysvětlen srozumitelně a uvidíte přesně, proč děláme to, co děláme.

---

## Krok 1 – Vytvoření prázdného HTML dokumentu a získání jeho JavaScript engine

První věc, kterou potřebujeme, je prázdný dokument, který nám poskytne sandboxované JavaScript prostředí. Třída `Document` z Aspose.HTML to přesně umožňuje.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**Proč je to důležité:** Objekt `Document` napodobuje okno prohlížeče a jeho `JavaScriptEngine` nám umožňuje spouštět skripty přesně tak, jako by to dělal prohlížeč. To je základ pro **call java from javascript** – engine funguje jako most.

---

## Krok 2 – Registrace host objektu, aby JavaScript mohl volat zpět do Javy

Aspose.HTML vám umožní vystavit libovolný Java objekt skriptovému světu. Vytvoříme anonymní třídu s jedinou metodou `onResult`, která jednoduše vypíše jakýkoli JSON, který obdrží.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**Vysvětlení:**  
- `addHostObject` naváže jméno `javaCallback` na anonymní Java objekt.  
- V JavaScriptu zavoláme `javaCallback.onResult(...)`.  
- Toto je jádro **call java from javascript** – skript se dostane do Java světa a Java reaguje.

> **Tip:** Udržujte metody host objektu `public` a jednoduché; složité objekty mohou způsobovat problémy se serializací.

---

## Krok 3 – Napsání asynchronní JavaScript funkce pomocí asynchronního Fetch API

Nyní přichází zábavná část: malý skript, který načte JSON ze vzdáleného endpointu. Použijeme `async/await`, což je moderní způsob, jak **run async JavaScript**.

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**Proč volíme `fetch` místo staršího XHR:**  
- `fetch` vrací `Promise`, což činí kód přehlednějším.  
- Pracuje nativně s `await`, takže tok čtení je shora dolů – ideální pro demonstraci **asynchronous fetch api**.  
- API je budoucnost‑bezpečné; většina prohlížečů a engine (včetně Aspose) jej podporuje bez dalších úprav.

---

## Krok 4 – Spuštění skriptu uvnitř JavaScript engine dokumentu

Nakonec předáme skript engine. Engine spustí malý event loop, vyřeší `fetch` promise a po dokončení zavolá zpět do Javy.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

Po spuštění třídy `AsyncJsTutorial` byste měli vidět něco podobného:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Tento výstup potvrzuje tři věci:

1. **asynchronous fetch API** úspěšně načetl data.  
2. JSON byl serializován a předán Javě.  
3. Naše volání **execute javascript engine** proběhlo bez deadlocků.

---

## Krok 5 – Zpracování chyb a okrajových případů (volitelné vylepšení)

Kód v reálném světě zřídka běží vždy perfektně. Níže najdete několik častých úskalí a způsoby, jak se proti nim bránit.

### 5.1 Selhání sítě

Pokud je vzdálený server nedostupný, `fetch` vyhodí výjimku. Zabalte volání do `try/catch` bloku:

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

Nyní Java strana obdrží chybovou zprávu místo zablokování.

### 5.2 Timeouty

Engine Aspose neexponuje nativní timeout pro `fetch`, ale můžete si jej implementovat v JavaScriptu:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 Více volání

Pokud potřebujete načíst několik zdrojů, jednoduše iterujte nebo mapujte pole URL. Host objekt lze rozšířit o parametr identifikátoru, který vám umožní korelovat odpovědi.

---

## Kompletní funkční příklad

Níže je **plný zdrojový soubor**, který můžete zkopírovat‑vložit do svého IDE. Žádné skryté závislosti, jen Aspose.HTML JAR na classpath.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**Očekávaný výstup na konzoli**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Pokud se objeví řádek začínající `Error:`, něco se pokazilo – pravděpodobně výpadek sítě.

---

## Vizualizace

![Diagram illustrating how Java calls JavaScript and receives async fetch results – call java from javascript](/images/java-js-async.png)

*Obrázek ukazuje tok: Java → JavaScriptEngine → async fetch → JavaCallback.*

---

## Často kladené otázky

**Lze tento přístup použít s jinými JavaScript engine?**  
Ano, jakýkoli engine, který poskytuje mechanismus host objektu (např. Nashorn, GraalVM), může fungovat, ale Aspose.HTML vám nabízí plnohodnotné prostředí podobné prohlížeči s vestavěným `fetch`.

**Co když potřebuji vrátit složitý Java objekt místo řetězce?**  
Můžete objekt na straně Javy serializovat do JSON a nechat JavaScript jej parsovat, nebo můžete exposeovat více metod na host objektu pro přijímání jednotlivých polí.

**Je implementace `fetch` plně standard‑compliant?**  
Aspose.HTML implementuje WHATWG Fetch Standard, takže získáte správnou podporu přesměrování, CORS a streamování.

**Blokuje toto Java vlákno během čekání na síť?**  
Ne. Volání `execute` se vrátí okamžitě a interní engine zpracovává promise asynchronně. Hlavní vlákno však zůstane aktivní, dokud skript nedokončí nebo explicitně neukončíte engine.

---

## Závěr

Prošli jsme praktickým scénářem, který vám umožní **call java from javascript**, **run async JavaScript** a **fetch JSON in Java** pomocí **asynchronous fetch API**. Vytvořením host objektu, napsáním úhledné `async` funkce a jejím spuštěním pomocí **JavaScript engine** Aspose.HTML získáte čistý, neblokující most mezi těmito dvěma runtime.

Vyzkoušejte to, změňte URL nebo přidejte další callbacky – vaše představivost je limit. Další kroky, které můžete zkusit:

- **Executing JavaScript engine** s více současnými skripty.  
- Použití **run async javascript** pro zpracování velkých datových sad paralelně.  
- Integrace tohoto vzoru do web‑služby, která dynamicky renderuje HTML za běhu.

Nebojte se experimentovat a neváhejte zanechat komentář, pokud narazíte na neočekávaný problém. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}