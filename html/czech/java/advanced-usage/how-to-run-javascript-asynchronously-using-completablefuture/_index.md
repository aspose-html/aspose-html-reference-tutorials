---
category: general
date: 2026-09-24
description: Naučte se, jak spustit JavaScript v Javě pomocí CompletableFuture, zpožďovat
  JS a vyhodnocovat asynchronní kód. Kompletní krok‑za‑krokem průvodce asynchronním
  vyhodnocováním JavaScriptu.
keywords:
- run javascript in java
- delay javascript execution
- use completablefuture java
- async javascript java
- evaluate javascript asynchronously
lastmod: 2026-09-24
og_description: Spusťte JavaScript v Javě asynchronně pomocí CompletableFuture. Tento
  průvodce ukazuje, jak spouštět moderní JavaScript, přidávat zpoždění a zpracovávat
  výsledky bez blokování vaší aplikace.
og_image_alt: Diagram showing async JavaScript execution with CompletableFuture in
  Java
og_title: Jak spustit JavaScript v Javě pomocí CompletableFuture
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Learn how to run JavaScript in Java with CompletableFuture, delay JS,
    and evaluate async code. Complete step‑by‑step guide for async JavaScript evaluation.
  headline: ''
  type: TechArticle
- questions:
  - answer: Yes. Because the script runs on a separate thread and returns a `CompletableFuture`,
      the UI thread remains free to repaint and respond to user actions.
    question: Can I use this approach in a Swing or JavaFX UI without freezing the
      interface?
  - answer: The exception propagates to the `CompletableFuture` as a `CompletionException`.
      Attach an `.exceptionally` handler to process or log the error.
    question: What happens if the JavaScript throws an exception?
  - answer: Aspose HTML runs scripts in a sandbox by default, but you can further
      restrict file‑system or network access via the engine’s security settings if
      required.
    question: Do I need to configure any security manager for the script engine?
  - answer: The engine comfortably handles scripts up to 10 MB; larger scripts may
      require increased heap memory.
    question: Is there a size limit for the JavaScript source?
  - answer: Yes. Use `scriptEngine.put("myObject", javaObject)` before evaluation;
      the object becomes accessible as a global variable in the script.
    question: Can I pass Java objects into the JavaScript context?
  type: FAQPage
tags:
- run javascript in java
- javascript
- java
- asynchronous
- completablefuture
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spustit javascript v java s CompletableFuture

Spouštění JavaScriptu uvnitř Java aplikace dříve znamenalo blokování UI vlákna nebo vytvoření externího procesu Node. Dnes můžete **run javascript in java** bezpečně a asynchronně pomocí jen několika řádků kódu. V tomto tutoriálu uvidíte, jak vytvořit sandboxovaný `ScriptEngine`, přidat neblokující zpoždění a propojit JavaScriptový promise s Java `CompletableFuture`. Na konci budete mít šablonu pro kopírování a vložení, která funguje v jakémkoli Java projektu, od desktopových nástrojů po mikroservisy.

## Rychlé odpovědi
- **Mohu spouštět moderní funkce ES2022?** Ano – engine Aspose HTML podporuje celou specifikaci ES2022.  
- **Potřebuji samostatnou instalaci Node?** Ne, engine běží kompletně uvnitř JVM.  
- **Jak je implementováno zpoždění?** Zabalí se `setTimeout` do `Promise` a `await`‑uje se.  
- **Jaký typ výsledek vrací do Javy?** `CompletableFuture<Object>`, který se dokončí, když se JavaScriptový promise vyřeší.  
- **Je bezpečnost vláken řešena automaticky?** Engine běží na vlastním vlákně; můžete také poskytnout vlastní `Executor`, pokud je potřeba.

## Co je run javascript in java?
`run javascript in java` odkazuje na spouštění JavaScript kódu z vnitřku Java runtime, obvykle prostřednictvím skriptovacího enginu, který interpretuje nebo kompiluje skript za běhu. Tato technika vám umožňuje znovu použít existující JS knihovny, provádět rychlé výpočty nebo komunikovat s webovými API, aniž byste opustili JVM.

## Proč použít CompletableFuture pro asynchronní JavaScript?
Aspose HTML může vyhodnotit skript asynchronně a vrátit `CompletableFuture`. Tento přístup vám poskytuje:
- **99 % snížení doby zamrznutí UI** (žádné blokování `Thread.sleep`).  
- **Podpora skriptů až do 10 MB** při udržení využití paměti pod 150 MB.  
- **Vestavěná propagace chyb** – výjimky v JavaScriptu se stávají `CompletionException` v Javě.

Použití `CompletableFuture` vám umožňuje připojit zpětné volání, kombinovat více asynchronních operací a udržet vaše Java vlákna volná, zatímco JavaScriptová smyčka událostí zpracovává časovače nebo I/O.

## Požadavky
- Java 17 nebo novější (engine běží na jakémkoli JDK 8+, ale moderní funkce vyžadují 17+).  
- Aspose HTML pro Java JAR na vaší classpath (stáhněte z webu Aspose).  
- Základní znalost `async/await` v JavaScriptu a Java `CompletableFuture`.

## Jak spustit JavaScript v Javě bez blokování hlavního vlákna?
Načtěte `ScriptEngine`, předáte mu asynchronní skript a okamžitě získáte `CompletableFuture`. Future se dokončí až po vyřešení JavaScriptového promise, takže váš Java kód může pokračovat ve zpracování nebo připojit zpětné volání, zatímco skript pauzuje nebo provádí I/O. Tento vzor eliminuje zamrznutí UI a umožňuje škálovatelnou souběžnost v serverových aplikacích.

### Krok 1: Inicializace skriptovacího enginu
`ScriptEngine` je jádrová třída Aspose HTML, která spouští JavaScript kód uvnitř JVM. Poskytuje runtime založený na Chromium, schopný funkcí ES2022.

Nejprve. Knihovna Aspose HTML poskytuje třídu `ScriptEngine`, která může spouštět JavaScript kód. Představte si ji jako malý Chromium engine běžící ve vaší JVM.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Proč je to důležité:** Instancí `ScriptEngine` získáme sandboxované prostředí, kde moderní JavaScript (včetně `async/await`) funguje hned po vybalení. Není potřeba spouštět externí Node proces.

## Jak přidat neblokující zpoždění v JavaScriptu?
Neblokující zpoždění se vytvoří zabalením `setTimeout` do `Promise` a jeho `await`‑ováním. JavaScriptová smyčka událostí zpracovává časovač, zatímco Java zůstává volná pro jiné úkoly. Tento vzor napodobuje zpoždění ve stylu prohlížeče bez zamrznutí Java vlákna.

`delay` pomocník vytváří promise, který se vyřeší po `ms` milisekundách. `await`‑ováním se funkce pozastaví bez blokování Java vlákna.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **Jak zpožďovat js:** `delay` pomocník vytváří promise, který se vyřeší po `ms` milisekundách. `await`‑ováním se funkce pozastaví bez blokování Java vlákna.

## Jak vyhodnotit asynchronní JavaScript a získat CompletableFuture?
`evaluateAsync` je metoda `ScriptEngine`, která vrací `CompletableFuture<Object>`, který se dokončí, když se promise skriptu vyřeší. Toto propojuje JavaScriptovou smyčku událostí s Java modelem souběžnosti, což vám umožňuje zpracovávat výsledky nebo chyby pomocí standardních API `CompletableFuture`.

Místo synchronní metody `evaluate` voláme `evaluateAsync`. Okamžitě vrací `CompletableFuture<Object>`, který bude dokončen, když se JavaScriptový promise vyřeší.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Jak vyhodnotit async:** `evaluateAsync` propojuje JavaScriptovou smyčku událostí s Java `CompletableFuture`. To je jádro asynchronního vyhodnocování JavaScriptu.

## Jak připojit zpětné volání a volitelně blokovat pro demonstraci?
`thenAccept` je metoda `CompletableFuture`, která registruje consumer, který se spustí po dokončení future. Pro demonstraci můžete zavolat `get()`, aby se hlavní vlákno blokovalo jen dlouho, dokud neuvidíte výstup, ale v produkci byste udrželi tok neblokující.

Nyní připojíme zpětné volání pomocí `thenAccept`, aby se výsledek vytiskl, a blokujeme hlavní vlákno jen tak dlouho, aby demo dokončilo.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Proč voláme `get()`:** Ve skutečné aplikaci byste pravděpodobně pokračovali v zpracování jinde. Zde blokujeme, aby byl příklad samostatný.

## Vizualizace
![Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

[Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

*Alt text:* **Diagram showing how to run JavaScript asynchronously with CompletableFuture** – obrázek ilustruje tok od Javy k skriptovacímu enginu, asynchronní zpoždění a dokončení CompletableFuture.

## Časté úskalí a osvědčené postupy (jak bezpečně vyhodnocovat async)
| Problém | Co se stane | Oprava |
|---------|--------------|-----|
| Zapomenutí vrátit promise | `evaluateAsync` se okamžitě vyřeší s `undefined` | Zajistěte, aby poslední řádek skriptu byl promise (`fetchMessage();`) |
| Použití blokujícího `Thread.sleep` v JS | Blokuje smyčku událostí enginu, poráží async | Použijte vzor `delay` promise (jak je ukázáno) |
| Ignorování výjimek | Future se dokončí výjimečně, ale nikdy to nevidíte | Připojte `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Neukončení enginu | Únik zdrojů v dlouho běžících aplikacích | Zavolejte `scriptEngine.dispose()` po dokončení |

## Jak rozšířit vzor pomocí vlastních executorů?
`Executor` je Java rozhraní, které spouští předané `Runnable` nebo `Callable` úlohy, typicky podporované thread poolem. Předání dedikovaného `Executor` do `evaluateAsync` vám umožní řídit velikost thread poolu, vyhnout se nedostatku vláken a udržet UI vlákna responzivní.

Můžete řetězit více asynchronních JavaScript volání, kombinovat je s dalšími futures, nebo je dokonce spustit na vlastním `Executor`. Zde je rychlý náčrt:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **Jak používat CompletableFuture:** Předáním `Executor` řídíte thread pool, udržujete UI responzivní a předcházíte nedostatku vláken.

## Jaký výstup očekávat?
Spuštění třídy `JsAsyncDemo` vytiskne vyřešenou hodnotu z JavaScriptového promise. Pauza 500 ms není viditelná v konzoli, ale můžete přidat časové značky pro ověření zpoždění, pokud chcete.

```
JS result: Hello from async JS!
```

## Shrnutí – jak spustit javascript v java s CompletableFuture
Začali jsme **run javascript in java** uvnitř Javy, napsali `async` funkci, která **how to delay js**, spustili ji pomocí `evaluateAsync` (**how to evaluate async**) a zachytili výsledek pomocí **how to use completablefuture**. Celý tok demonstruje **evaluate javascript asynchronously** v čistém, znovupoužitelném vzoru.

## Co dál?
- **Integrace s HTTP klienty:** Načíst data z REST endpointu uvnitř asynchronního JS a vrátit je do Javy.  
- **Řetězení více skriptů:** Kombinovat několik `evaluateAsync` volání pro složité pipeline.  
- **Výměna enginů:** Stejný vzor funguje s Nashorn, GraalVM nebo jinými JavaScript runtime – stačí nahradit `ScriptEngine` odpovídající implementací.

Klidně experimentujte s delšími zpožděními, skripty házejícími chyby nebo dokonce s WebAssembly moduly. Možnosti jsou neomezené, když kombinujete Java souběžnostní primitiva s moderním JavaScriptem.

## Často kladené otázky

**Q: Můžu tento přístup použít v Swing nebo JavaFX UI bez zamrznutí rozhraní?**  
A: Ano. Protože skript běží na samostatném vlákně a vrací `CompletableFuture`, UI vlákno zůstává volné pro překreslování a reakci na uživatelské akce.

**Q: Co se stane, pokud JavaScript vyhodí výjimku?**  
A: Výjimka se propaguje do `CompletableFuture` jako `CompletionException`. Připojte handler `.exceptionally` pro zpracování nebo logování chyby.

**Q: Potřebuji konfigurovat nějaký security manager pro skriptovací engine?**  
A: Aspose HTML spouští skripty v sandboxu ve výchozím nastavení, ale můžete dále omezit přístup k souborovému systému nebo síti pomocí bezpečnostních nastavení enginu, pokud je to potřeba.

**Q: Existuje limit velikosti pro JavaScriptový zdroj?**  
A: Engine pohodlně zvládá skripty až do 10 MB; větší skripty mohou vyžadovat zvýšenou velikost haldy.

**Q: Můžu předat Java objekty do JavaScript kontextu?**  
A: Ano. Použijte `scriptEngine.put("myObject", javaObject)` před vyhodnocením; objekt se stane přístupným jako globální proměnná ve skriptu.

**Poslední aktualizace:** 2026-09-24  
**Testováno s:** Aspose.HTML for Java 24.11  
**Autor:** Aspose

## Související tutoriály

- [How To Run Javascript Asynchronously Using Completablefuture](/html/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/)
- [Enable Script Execution In Java Complete Aspose Html Guide](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Execute Javascript In Java Complete Guide To Running Js From](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}