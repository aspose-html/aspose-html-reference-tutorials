---
category: general
date: 2026-05-28
description: Načíst data z API v Javě pomocí Aspose.HTML – naučte se, jak spustit
  asynchronní JavaScript, spustit asynchronní skript a nastavit atribut DOM z načteného
  JSONu.
draft: false
keywords:
- fetch api data
- execute async javascript
- run async script
- set dom attribute
- how to run async
language: cs
og_description: Načtěte data API v Javě s Aspose.HTML. Tento tutoriál ukazuje, jak
  spustit asynchronní JavaScript, spustit asynchronní skript a nastavit atribut DOM
  z výsledků API.
og_title: Načtení dat API v Javě – krok za krokem průvodce Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  headline: fetch api data in Java with Aspose.HTML - Complete Guide
  type: TechArticle
- description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  name: fetch api data in Java with Aspose.HTML - Complete Guide
  steps:
  - name: Expected Output
    text: '``` GitHub stars: 84327 ```'
  - name: What if the fetch call fails?
    text: 'The script will throw a JavaScript exception, which propagates to `ScriptEngine.evaluate`.
      You can catch it in Java:'
  - name: Can I fetch from a private API that requires authentication?
    text: 'Sure—just add the appropriate headers in the script:'
  - name: Does this work on older Java versions?
    text: Aspose.HTML ships with its own JavaScript engine, so you don’t need Nashorn
      or GraalVM. However, the `try‑with‑resources` syntax requires Java 7+. For Java
      6 you’d have to close the document manually.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Async JavaScript
title: Načtení dat API v Javě s Aspose.HTML – kompletní průvodce
url: /cs/java/message-handling-networking/fetch-api-data-in-java-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# načtení dat z API v Javě s Aspose.HTML – Kompletní průvodce

Už jste se někdy zamysleli, jak **fetch api data** v Javě získat, aniž byste opustili pohodlí svého IDE? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují zavolat vzdálenou službu z HTML stránky vykreslené pomocí Aspose.HTML a poté výsledek přenést zpět do Javy.  

V tomto tutoriálu projdeme praktickým příkladem, který **executes async javascript**, spustí **async script**, a nakonec **sets a DOM attribute** s načtenou hodnotou. Na konci přesně budete vědět, *jak spustit async* operace bezpečně a získat potřebná data.

## Co vytvoříte

Vytvoříme malou Java konzolovou aplikaci, která:

1. Načte HTML soubor obsahující async funkci.  
2. Spustí skript, který používá **fetch API** k volání veřejného endpointu GitHubu.  
3. Počká, až se promise vyřeší (až 10 sekund).  
4. Uloží počet hvězd do vlastního atributu `data-stars` na elementu `<body>`.  
5. Přečte tento atribut zpět v Javě a vypíše jej.

Žádné externí knihovny HTTP klienta, žádný extra kód pro vlákna — pouze Aspose.HTML, který odlehčí těžkou práci.

## Požadavky

- **Java 17** nebo novější (kód se kompiluje i s dřívějšími verzemi, ale 17 je aktuální LTS).  
- **Aspose.HTML for Java** knihovna (verze 23.9 nebo novější).  
- Jednoduchý HTML soubor (`async-page.html`) umístěný někde na disku.  
- Internetové připojení (volání fetch cílí na `https://api.github.com`).  

If you already have a Maven project, add the Aspose.HTML dependency:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

Nyní se ponořme do kódu.

## Krok 1: Připravte HTML stránku

Nejprve vytvořte minimální HTML soubor, který bude hostovat async funkci. Nepotřebujete žádné složité značky — pouze tag `<body>`.

```html
<!-- async-page.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Async Demo</title>
</head>
<body>
    <!-- The script we’ll inject later will populate this attribute -->
</body>
</html>
```

Uložte tento soubor na nějaké přístupné místo, např. `C:/temp/async-page.html`. Tato cesta bude použita v Javě.

![fetch api data example](https://example.com/fetch-api-data.png "fetch api data example")

*Alt text obrázku: fetch api data example ukazující výstup konzole s počtem hvězd na GitHubu.*

## Krok 2: Načtěte HTML dokument v Javě

S připraveným HTML souborem jej otevřeme pomocí `HTMLDocument` z Aspose.HTML. Blok `try‑with‑resources` zajišťuje, že dokument bude řádně uvolněn.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {
            // The rest of the steps go here...
        }
    }
}
```

Proč používat `HTMLDocument`? Poskytuje plnohodnotný DOM, vestavěný JavaScript engine a pohodlný způsob, jak interagovat se stránkou z Javy — vše bez spouštění prohlížeče.

## Krok 3: Napište async skript

Nyní vytvoříme úryvek JavaScriptu, který **fetches API data**, čeká na promise a poté **sets a DOM attribute**. Všimněte si použití `async/await` — stejného vzoru, jaký byste psali v prohlížeči.

```java
String script =
    "async function run() {" +
    "  const data = await fetch('https://api.github.com').then(r => r.json());" +
    "  document.body.setAttribute('data-stars', data.stargazers_count);" +
    "}" +
    "run();";
```

Několik věcí, na které je třeba upozornit:

- Funkce `run` je deklarována jako `async`, takže můžeme `await` volání `fetch`.
- Po parsování JSONu uložíme `data.stargazers_count` do vlastního atributu `data-stars`.
- Nakonec okamžitě zavoláme `run()`.

Tento malý skript dělá vše, co potřebujeme k **run async script** a zachycení výsledku.

## Krok 4: Spusťte skript a počkejte

`ScriptEngine` z Aspose.HTML může vyhodnocovat JavaScript s časovým limitem. Předáním `10000` říkáme enginu, aby čekal až **10 sekund** na dokončení async operace.

```java
// Execute the script and wait (up to 10 seconds) for the async operation to finish
ScriptEngine engine = doc.getScriptEngine();
engine.evaluate(script, 10000);   // timeout in milliseconds
```

Pokud požadavek trvá déle než timeout, je vyhozena `ScriptException` — ideální pro zpracování nestabilních síťových podmínek. V produkci byste to pravděpodobně zabalili do try‑catch a podle potřeby znovu spustili.

## Krok 5: Získejte atribut z Javy

Po dokončení skriptu je atribut `data-stars` nyní součástí DOM. Přetáhněte jej zpět do Javy jednoduchým voláním:

```java
// Retrieve the value set by the script from the document
String stars = doc.getBody().getAttribute("data-stars");
System.out.println("GitHub stars: " + stars);
```

Tento řádek vypíše něco jako `GitHub stars: 12345`. Přesné číslo se mění denně, ale vzor zůstává stejný.

## Kompletní funkční příklad

Sestavením všech částí dohromady získáte kompletní, připravený k spuštění program:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {

            // Step 2: Define a script that calls the async function and stores the result in a DOM attribute
            String script =
                "async function run() {" +
                "  const data = await fetch('https://api.github.com').then(r => r.json());" +
                "  document.body.setAttribute('data-stars', data.stargazers_count);" +
                "}" +
                "run();";

            // Step 3: Execute the script and wait (up to 10 seconds) for the async operation to finish
            ScriptEngine engine = doc.getScriptEngine();
            engine.evaluate(script, 10000);

            // Step 4: Retrieve the value set by the script from the document
            String stars = doc.getBody().getAttribute("data-stars");
            System.out.println("GitHub stars: " + stars);
        }
    }
}
```

### Očekávaný výstup

```
GitHub stars: 84327
```

(Vaše číslo bude jiné; důležité je, že hodnota je **string** představující počet hvězd.)

## Časté otázky a okrajové případy

### Co když volání fetch selže?

Skript vyhodí JavaScriptovou výjimku, která se propaguje do `ScriptEngine.evaluate`. Můžete ji zachytit v Javě:

```java
try {
    engine.evaluate(script, 10000);
} catch (ScriptException e) {
    System.err.println("Failed to fetch data: " + e.getMessage());
}
```

### Můžu fetchovat z privátního API, které vyžaduje autentizaci?

Jistě — stačí přidat příslušné hlavičky ve skriptu:

```javascript
await fetch('https://api.example.com/secure', {
    headers: { 'Authorization': 'Bearer YOUR_TOKEN' }
}).then(r => r.json());
```

Nezapomeňte uchovávat tajné údaje mimo verzovací systém.

### Funguje to na starších verzích Javy?

Aspose.HTML je dodáván s vlastním JavaScriptovým enginem, takže nepotřebujete Nashorn ani GraalVM. Nicméně syntaxe `try‑with‑resources` vyžaduje Java 7+. Pro Java 6 byste museli dokument uzavřít ručně.

## Profesionální tipy

- **Reuse the ScriptEngine**: Pokud potřebujete spouštět mnoho async skriptů, udržujte jednu instanci enginu aktivní — snižuje to režii.  
- **Increase the timeout** pro pomalejší API, ale nenastavujte jej na `Integer.MAX_VALUE`; stále chcete mít bezpečnostní limit.  
- **Validate the attribute** před jeho použitím. DOM atribut může být `null`, pokud se skript nikdy nespustil.  
- **Log the raw JSON** během vývoje; pomáhá, když se struktura API změní.

## Další kroky

Nyní, když víte, jak **fetch api data**, můžete rozšířit tento vzor:

- **Parse more complex JSON** a vložit více atributů.  
- **Create tables** uvnitř HTML stránky na základě načtených dat.  
- **Combine with Aspose.PDF** pro vytvoření PDF, které obsahuje živé výsledky API.  

Každý z nich staví na stejných základních myšlenkách: **execute async javascript**, **run async script** a **set dom attribute** z výsledku. Klidně experimentujte — v script enginu Aspose.HTML je skryta velká síla.

---

*Šťastné programování! Pokud narazíte na problémy, zanechte komentář níže a společně je vyřešíme.*

## Související tutoriály

- [How to Run JavaScript in Java – Complete Guide](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Append Element to Body with Aspose.HTML for Java using a DOM Mutation Observer](/html/english/java/advanced-usage/dom-mutation-observer-observing-node-additions/)
- [How to Set Timeout – Manage Network Timeout in Aspose.HTML for Java](/html/english/java/message-handling-networking/network-timeout/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}