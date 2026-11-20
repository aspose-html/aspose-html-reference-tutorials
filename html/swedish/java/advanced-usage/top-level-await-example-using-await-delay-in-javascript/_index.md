---
category: general
date: 2026-03-26
description: Exempel på top‑level await som visar await‑delay i JavaScript, en inkrementerande
  räknarklass och offentliga klassfält i JavaScript i en live‑demo.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: sv
og_description: Exempel på top‑level await som demonstrerar await delay i JavaScript,
  en inkrementerande räknarklass och offentliga klassfält i JavaScript i en kortfattad
  handledning.
og_title: exempel på top‑level await – Använda await delay i JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Exempel på top‑level await – Använda await delay i JavaScript
url: /sv/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# top level await example – Using await delay in JavaScript

Har du någonsin funderat på hur du kan pausa modulens körning utan att omsluta allt i en async IIFE? Det är precis vad ett **top level await example** låter dig göra. I den här handledningen går vi igenom en liten webbsida som använder `await delay javascript` för att skjuta upp arbete, och sedan skapar en `increment counter class` som utnyttjar **public class fields javascript**. I slutet har du ett komplett, kopiera‑och‑klistra‑snutt som körs i vilken modern webbläsare som helst.

Vi täcker allt från att definiera en klass med ett offentligt fält till att koppla ihop en enkel promise‑baserad fördröjningshjälp. Inga externa bibliotek, ingen byggprocess—bara ren HTML, ett `<script type="module">` och de senaste ECMAScript‑funktionerna. Om du redan är bekväm med async‑funktioner kommer du att se varför top‑level await känns som en naturlig förlängning. Om du är ny på **javascript class public field**‑syntaxen, oroa dig inte—vi förklarar varför varje rad finns där.

## What You’ll Learn

- Hur ett **top level await example** fungerar i ett modul‑script.
- Mönstret för en `await delay javascript`‑hjälp som efterliknar `setTimeout` med promises.
- Hur du skriver en **increment counter class** som använder ett offentligt fält (`count`) och ett statiskt initieringsblock.
- Förväntad konsolutskrift och hur du verifierar att det statiska blocket körs innan resten av skriptet.
- Tips för felsökning av vanliga fallgropar, såsom äldre webbläsare som inte stödjer top‑level await.

> **Pro tip:** Moderna webbläsare (Chrome 106+, Firefox 102+, Edge 106+) stödjer redan top‑level await. Om du behöver stödja äldre miljöer, överväg att paketera med ett verktyg som Vite eller Babel.

## Step 1 – Define a Class with a Public Field and a Static Block

Den första delen av vår demo är en klass som lagrar en numerisk räknare. Lägg märke till raden `count = 0;`—detta är **public class fields javascript**‑syntaxen som introducerades i ES2022. Den skapar en instans‑egenskap utan en konstruktor.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Varför ett statiskt block?** Det låter oss köra engångs‑initialiseringslogik (som loggning) precis när modulen parsas, *innan* någon top‑level await körs. Detta garanterar att meddelandet visas först i konsolen, vilket bevisar att klassen utvärderades tidigt.

## Step 2 – Create an `await delay javascript` Helper

Nästa steg är en liten promise‑baserad fördröjningsfunktion. Den är i princip ett omslag runt `setTimeout`, men genom att returnera ett promise blir den await‑bar.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Edge case:** Om `ms` är negativt eller inte ett tal, behandlar `setTimeout` det som `0`. Du kan lägga till validering, men för en demo håller en‑rad‑lösningen koden läsbar.

## Step 3 – Use Top‑Level Await to Pause Execution

Nu kommer stjärnan i showen: top‑level await. Eftersom vårt skript är en modul (`type="module"`), kan vi placera `await` direkt i top‑scopen. Detta pausar modulen tills promisen löser sig, vilket låter oss styra ordningen på bieffekter.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Common question:** “Kan jag använda top‑level await i ett vanligt `<script>`‑tagg?” Nej—endast modul‑scripts stödjer det. Om du glömmer `type="module"` får du ett syntaxfel.

## Step 4 – Instantiate the Class, Increment, and Log the Result

Till sist sätter vi ihop allt: skapar en instans, anropar `increment()`, och skriver ut det slutgiltiga värdet. Detta demonstrerar **increment counter class** i aktion.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Expected Console Output

```
Counter class initialized
Final count: 1
```

Om du öppnar sidan i DevTools bör du se meddelandet från det statiska blocket visas **innan** fördröjningen slutförs, vilket bekräftar att klassen utvärderades först.

## Step 5 – Why Use Public Class Fields Instead of a Constructor?

Du kanske undrar varför vi inte skrev:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Båda tillvägagångssätten fungerar, men **public class fields javascript** ger en renare, mer deklarativ syntax. Fältet definieras en gång, inte i varje konstruktor‑anrop, vilket kan vara lättare att läsa när klassen blir större. Dessutom kan statiska block inte placeras i en konstruktor, så att separera initieringslogik blir mer naturligt.

## Step 6 – Adapting the Example for Real‑World Apps

I produktion behöver du ofta mer än en enda räknare. Här är några snabba idéer:

- **Multiple counters:** Store them in a `Map` keyed by identifier.
- **Persisted state:** Replace `console.log` with `localStorage` writes.
- **Async initialization:** Use the static block to fetch configuration from a server before any instances are created.

Alla dessa mönster drar fortfarande nytta av top‑level await, eftersom du kan hämta data en gång vid modulens laddning och garantera att den är klar för varje konsument.

## Frequently Asked Questions

**Q: Does top‑level await block other modules?**  
A: No. Each module runs independently. Only the module that contains the await is paused; other modules continue loading in parallel.

**Q: What if the delay promise rejects?**  
A: An unhandled rejection will abort the module evaluation and surface as an error in the console. Wrap the await in a `try…catch` if you need graceful fallback.

**Q: Is the `static` keyword required?**  
A: Not for the counter itself, but the static block is a handy way to demonstrate that code runs *once* at load time—great for logging or feature‑detection.

## Conclusion

Du har precis byggt ett **top level await example** som visar `await delay javascript`, en **increment counter class**, och kraften i **public class fields javascript**. Den kompletta, körbara snutten finns ovan, och konsolutskriften bevisar att det statiska blocket körs innan den fördröjda koden.  

Härifrån kan du experimentera med mer komplexa async‑flöden, byta ut fördröjningen mot ett riktigt API‑anrop, eller utöka klassen med fler metoder. Kom ihåg att modern JavaScript låter dig behandla moduler som förstklassiga async‑entiteter—utan extra omslag.

Lycka till med kodandet, och dela gärna dina varianter i kommentarerna. Om du fann den här guiden användbar, dela den med en kollega som fortfarande kämpar med async‑mönster!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}