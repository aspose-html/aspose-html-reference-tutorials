---
category: general
date: 2026-02-16
description: Naučte se spouštět JavaScript v Javě pomocí CompletableFuture, odkládat
  JS a vyhodnocovat asynchronní kód. Kompletní krok‑za‑krokem průvodce asynchronním
  vyhodnocováním JavaScriptu.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: cs
og_description: Naučte se, jak spouštět JavaScript z Javy, odkládat JS a vyhodnocovat
  asynchronní kód pomocí CompletableFuture v tomto kompletním tutoriálu.
og_title: Jak spustit JavaScript asynchronně pomocí CompletableFuture
tags:
- javascript
- java
- asynchronous
- completablefuture
title: Jak spustit JavaScript asynchronně pomocí CompletableFuture
url: /cs/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

part.

Now produce final content with all markdown.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak spustit JavaScript asynchronně pomocí CompletableFuture

Už jste se někdy zamysleli nad **tím, jak spustit JavaScript** uvnitř Java aplikace, aniž byste blokovali hlavní vlákno? Možná potřebujete zavolat malý skript, který načte data, ale nechcete, aby se vaše UI zamrzlo. Dobrou zprávou je, že moderní Java knihovny vám umožňují vyhodnocovat JavaScript **asynchronně**, a můžete dokonce zavést zpoždění stejně jako v prohlížeči. V tomto průvodci vám ukážeme kompletní, spustitelný příklad, který používá Aspose HTML `ScriptEngine` spolu s `CompletableFuture`, aby **spustit JavaScript** a získat výsledek zpět v Javě.

Také se podíváme na **jak používat CompletableFuture**, **jak zpožďovat JS**, a **jak vyhodnocovat async** kód, abyste mohli **vyhodnocovat JavaScript asynchronně** v jakémkoli Java projektu. Na konci budete mít solidní šablonu, kterou můžete kopírovat‑vkládat, upravovat a začlenit do větších systémů.

---

## Co se naučíte

- Nastavit Java `ScriptEngine`, který dokáže spouštět moderní JavaScript ES2022.
- Napsat `async` funkci, která zahrnuje zpoždění (`jak zpožďovat js`).
- Zavolat `evaluateAsync` a získat `CompletableFuture` (`jak používat completablefuture`).
- Získat výsledek, jakmile se JavaScript promise vyřeší (`jak vyhodnocovat async`).
- Tipy pro zpracování chyb, správu vláken a rozšíření vzoru.

K žádným externím nástrojům pro sestavení není potřeba, kromě JAR souboru Aspose HTML pro Java, který můžete vložit do classpath. Ponořme se.

## Krok 1: Jak spustit JavaScript – Inicializace skriptovacího enginu

Nejprve. Knihovna Aspose HTML poskytuje třídu `ScriptEngine`, která může spouštět JavaScript kód. Představte si ji jako malý Chromium engine běžící uvnitř vašeho JVM.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Proč je to důležité:** Instancí `ScriptEngine` získáme sandboxované prostředí, kde moderní JavaScript (včetně `async/await`) funguje hned z krabice. Není potřeba spouštět externí Node proces.

## Krok 2: Jak zpožďovat JS – Napsat async funkci s Promise‑založeným časovačem

`setTimeout` v JavaScriptu je klasický způsob, jak pozastavit vykonávání. V moderním kódu jej zabalíme do `Promise`, abychom ho mohli `await`ovat. Přesně to uděláme v řetězci skriptu.

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

> **Jak zpožďovat js:** Pomocná funkce `delay` vytvoří promise, který se vyřeší po `ms` milisekundách. `await`ováním funkce se pozastaví bez blokování Java vlákna.

## Krok 3: Jak vyhodnocovat async – Spustit skript a získat CompletableFuture

Místo synchronní metody `evaluate` zavoláme `evaluateAsync`. Okamžitě vrátí `CompletableFuture<Object>`, který bude dokončen, až se JavaScript promise vyřeší.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Jak vyhodnocovat async:** `evaluateAsync` propojuje JavaScript event loop s Java `CompletableFuture`. To je jádro **vyhodnocování JavaScriptu asynchronně**.

## Krok 4: Jak používat CompletableFuture – Připojit callback a blokovat pro demo

Nyní připojíme callback pomocí `thenAccept`, který vytiskne výsledek, a blokujeme hlavní vlákno jen tak dlouho, aby demo dokončilo.

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

![Diagram ukazující, jak spustit JavaScript asynchronně pomocí CompletableFuture](https://example.com/diagram.png "Jak spustit JavaScript – Asynchronní tok")

*Alt text:* **Diagram ukazující, jak spustit JavaScript asynchronně pomocí CompletableFuture** – obrázek ilustruje tok od Javy k skriptovacímu enginu, async zpoždění a dokončení CompletableFuture.

## Časté úskalí a osvědčené postupy (Jak bezpečně vyhodnocovat async)

| Úskalí | Co se stane | Oprava |
|--------|-------------|--------|
| Zapomenutí vrátit promise | `evaluateAsync` se okamžitě vyřeší s `undefined` | Ujistěte se, že poslední řádek skriptu je promise (`fetchMessage();`) |
| Používání blokujícího `Thread.sleep` v JS | Blokuje event loop enginu, zruší async | Použijte vzor `delay` promise (jak je ukázáno) |
| Ignorování výjimek | Future se dokončí výjimečně, ale nikdy to nevidíte | Připojte `.exceptionally(e -> { e.printStackTrace(); return null; })` |
| Neukončení enginu | Únik zdrojů v dlouho běžících aplikacích | Zavolejte `scriptEngine.dispose()` po dokončení |

## Rozšíření vzoru (Jak používat CompletableFuture ve skutečných projektech)

Můžete řetězit více async JavaScript volání, kombinovat je s dalšími futures, nebo je spustit na vlastním `Executor`. Zde je rychlý náčrt:

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

## Očekávaný výstup

Spusťte třídu `JsAsyncDemo` a měli byste vidět:

```
JS result: Hello from async JS!
```

Pauza 500 ms není viditelná v konzoli, ale můžete přidat časové značky pro ověření zpoždění, pokud chcete.

## Shrnutí – Jak spustit JavaScript s CompletableFuture

Začali jsme **jak spustit JavaScript** uvnitř Javy, napsali `async` funkci, která **jak zpožďovat js**, spustili ji pomocí `evaluateAsync` (**jak vyhodnocovat async**) a zachytili výsledek pomocí **jak používat CompletableFuture**. Celý tok demonstruje **vyhodnocování JavaScriptu asynchronně** v čistém, znovupoužitelném vzoru.

## Co dál?

- **Integrace s HTTP klienty:** Načíst data z REST endpointu uvnitř async JS a vrátit je do Javy.
- **Použít více skriptů:** Řetězit několik volání `evaluateAsync` pro složité pipeline.
- **Vyměnit enginy:** Stejný vzor funguje s Nashorn, GraalVM nebo jinými JavaScript runtime – stačí nahradit `ScriptEngine`.

Neváhejte experimentovat s delšími zpožděními, skripty vyhazujícími chyby nebo dokonce s WebAssembly moduly. Možnosti jsou neomezené, když kombinujete Java konkurenční primitiva s moderním JavaScriptem.

### Máte otázky?

Pokud něco není jasné – možná se ptáte, jak zacházet s odmítnutým promise nebo jak předat proměnné z Javy do skriptu – zanechte komentář níže. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}