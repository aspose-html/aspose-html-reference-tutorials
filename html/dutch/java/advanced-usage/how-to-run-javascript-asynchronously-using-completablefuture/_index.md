---
category: general
date: 2026-02-16
description: Leer hoe je JavaScript in Java kunt uitvoeren met CompletableFuture,
  JS kunt vertragen en asynchrone code kunt evalueren. Complete stapsgewijze gids
  voor asynchrone JavaScript‑evaluatie.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: nl
og_description: Beheers hoe je JavaScript vanuit Java kunt uitvoeren, JS kunt vertragen
  en asynchrone code kunt evalueren met CompletableFuture in deze volledige tutorial.
og_title: Hoe JavaScript Asynchroon Uitvoeren met CompletableFuture
tags:
- javascript
- java
- asynchronous
- completablefuture
title: Hoe JavaScript Asynchroon Uitvoeren met CompletableFuture
url: /nl/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

translate them but keep code terms unchanged.

Let's produce translation.

We must keep code block placeholders unchanged.

Also tables: translate column headers and content.

Let's translate step by step.

I'll produce final markdown.

Be careful with alt text and image caption.

Also the "Alt text:" line.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe JavaScript Asynchroon Uitvoeren Met CompletableFuture

Heb je je ooit afgevraagd **hoe je JavaScript** kunt uitvoeren binnen een Java‑applicatie zonder de hoofdthread te blokkeren? Misschien moet je een klein script aanroepen dat gegevens ophaalt, maar wil je niet dat je UI bevriest. Het goede nieuws is dat moderne Java‑bibliotheken je in staat stellen JavaScript **asynchroon** te evalueren, en je kunt zelfs vertragingen introduceren zoals je in een browser zou doen. In deze gids laten we je een compleet, uitvoerbaar voorbeeld zien dat Aspose HTML’s `ScriptEngine` combineert met `CompletableFuture` om **hoe je JavaScript uitvoert** en het resultaat terug te krijgen in Java.

We behandelen ook **hoe je CompletableFuture gebruikt**, **hoe je JS vertraagt**, en **hoe je async‑code evalueert** zodat je **JavaScript asynchroon kunt evalueren** in elk Java‑project. Aan het einde heb je een solide sjabloon dat je kunt kopiëren‑plakken, aanpassen en integreren in grotere systemen.

---

## Wat je zult leren

- Een Java `ScriptEngine` configureren die moderne ES2022‑JavaScript kan uitvoeren.
- Een `async`‑functie schrijven die een vertraging bevat (`hoe je js vertraagt`).
- `evaluateAsync` aanroepen en een `CompletableFuture` ontvangen (`hoe je CompletableFuture gebruikt`).
- Het resultaat ophalen zodra de JavaScript‑promise wordt opgelost (`hoe je async evalueert`).
- Tips voor foutafhandeling, thread‑beheer en het uitbreiden van het patroon.

Er zijn geen externe build‑tools nodig, behalve de Aspose HTML for Java‑JAR, die je eenvoudig in je classpath kunt plaatsen. Laten we beginnen.

---

## Stap 1: Hoe JavaScript Uitvoeren – Initialiseert de Scripting‑Engine

Allereerst. De Aspose HTML‑bibliotheek biedt een `ScriptEngine`‑klasse die JavaScript‑code kan uitvoeren. Beschouw het als een kleine Chromium‑engine die binnen je JVM draait.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Waarom dit belangrijk is:** Door een `ScriptEngine` te instantieren krijgen we een sandbox‑omgeving waarin moderne JavaScript (inclusief `async/await`) direct werkt. Je hoeft geen extern Node‑proces op te starten.

---

## Stap 2: Hoe je JS Vertraagt – Schrijf een Async‑Functie met een Promise‑Gebaseerde Timer

JavaScript’s `setTimeout` is de klassieke manier om uitvoering te pauzeren. In moderne code wikkelen we dit in een `Promise` zodat we het kunnen `await`en. Dat is precies wat we doen in de script‑string.

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

> **Hoe je js vertraagt:** De `delay`‑helper maakt een promise die na `ms` milliseconden wordt afgehandeld. Door er `await` op uit te voeren, pauzeert de functie zonder de Java‑thread te blokkeren.

---

## Stap 3: Hoe je Async Evalueert – Voer het Script Uit en Krijg een CompletableFuture

In plaats van de synchrone `evaluate`‑methode, roepen we `evaluateAsync` aan. Deze retourneert direct een `CompletableFuture<Object>` die wordt voltooid zodra de JavaScript‑promise wordt opgelost.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Hoe je async evalueert:** `evaluateAsync` verbindt de JavaScript‑event‑loop met Java’s `CompletableFuture`. Dit is de kern van **JavaScript asynchroon evalueren**.

---

## Stap 4: Hoe je CompletableFuture Gebruikt – Voeg een Callback Toe en Blokkeer Voor Demo

Nu voegen we een callback toe met `thenAccept` om het resultaat te printen, en blokkeren we de hoofdthread net lang genoeg zodat de demo kan afronden.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Waarom we `get()` aanroepen:** In een echte applicatie zou je waarschijnlijk elders verder gaan met verwerken. Hier blokkeren we om het voorbeeld zelf‑voorzienend te houden.

---

## Visueel Overzicht

![Diagram showing how to run JavaScript asynchronously with CompletableFuture](https://example.com/diagram.png "How to Run JavaScript – Async Flow")

*Alt‑tekst:* **Diagram dat laat zien hoe je JavaScript asynchroon uitvoert met CompletableFuture** – de afbeelding illustreert de stroom van Java naar de script‑engine, de async‑vertraging en de voltooiing van de CompletableFuture.

---

## Veelvoorkomende Valkuilen & Best Practices (Hoe Async Veilig Evalueren)

| Valkuil | Wat gebeurt er | Oplossing |
|---------|----------------|-----------|
| Vergeten de promise te retourneren | `evaluateAsync` lost meteen op met `undefined` | Zorg dat de laatste regel van het script de promise is (`fetchMessage();`) |
| Blokkerende `Thread.sleep` in JS gebruiken | Blokkeert de event‑loop van de engine, ondermijnt async | Gebruik het `delay`‑promise‑patroon (zoals getoond) |
| Uitzonderingen negeren | Future voltooit uitzonderlijk, maar je ziet het niet | Voeg `.exceptionally(e -> { e.printStackTrace(); return null; })` toe |
| De engine niet afsluiten | Resource‑lekken in langdurige apps | Roep `scriptEngine.dispose()` aan wanneer je klaar bent |

---

## Het Patroon Uitbreiden (Hoe CompletableFuture in Real‑World Projecten Gebruiken)

Je kunt meerdere async‑JavaScript‑calls ketenen, combineren met andere futures, of ze zelfs laten draaien op een aangepaste `Executor`. Hier is een snelle schets:

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

> **Hoe je CompletableFuture gebruikt:** Door een `Executor` door te geven beheer je de thread‑pool, houd je de UI responsief en voorkom je thread‑starvation.

---

## Verwachte Output

Voer de `JsAsyncDemo`‑klasse uit en je zou moeten zien:

```
JS result: Hello from async JS!
```

De pauze van 500 ms is niet zichtbaar in de console, maar je kunt timestamps toevoegen om de vertraging te verifiëren indien gewenst.

---

## Samenvatting – Hoe JavaScript Uitvoeren met CompletableFuture

We begonnen met **hoe je JavaScript uitvoert** binnen Java, schreven een `async`‑functie die **hoe je js vertraagt**, voerden deze uit met `evaluateAsync` (**hoe je async evalueert**) en haalden het resultaat op met een **hoe je CompletableFuture gebruikt**. De volledige stroom demonstreert **JavaScript asynchroon evalueren** in een schoon, herbruikbaar patroon.

---

## Wat is het Volgende?

- **Integreren met HTTP‑clients:** Haal gegevens op van een REST‑endpoint binnen de async‑JS en retourneer ze naar Java.
- **Meerdere scripts gebruiken:** Keten verschillende `evaluateAsync`‑calls voor complexe pipelines.
- **Engines verwisselen:** Hetzelfde patroon werkt met Nashorn, GraalVM of andere JavaScript‑runtimes – vervang simpelweg `ScriptEngine`.

Voel je vrij om te experimenteren met langere vertragingen, scripts die fouten gooien, of zelfs WebAssembly‑modules. De mogelijkheden zijn eindeloos wanneer je Java’s concurrency‑primitieven combineert met moderne JavaScript.

---

### Vragen?

Als iets niet duidelijk is – misschien vraag je je af hoe je een afgewezen promise afhandelt of hoe je variabelen van Java naar het script doorgeeft – laat dan een reactie achter hieronder. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}