---
category: general
date: 2026-03-26
description: Top-level await‑voorbeeld dat await‑delay in JavaScript, een increment‑tellerklasse
  en publieke klassevelden in JavaScript laat zien in een live‑demo.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: nl
og_description: Top‑level‑await‑voorbeeld dat wachtvertraging in JavaScript, een tellerklasse
  met increment en openbare klassevelden in JavaScript demonstreert in een beknopte
  tutorial.
og_title: top level await voorbeeld – Gebruik await delay in JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: top level await voorbeeld – Gebruik await delay in JavaScript
url: /nl/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# top‑level await‑voorbeeld – Await delay gebruiken in JavaScript

Heb je je ooit afgevraagd hoe je de uitvoering van een module kunt pauzeren zonder alles in een async IIFE te wikkelen? Dat is precies wat een **top‑level await‑voorbeeld** je laat doen. In deze tutorial lopen we een kleine webpagina door die `await delay javascript` gebruikt om werk uit te stellen, en vervolgens een `increment counter class` maakt die **public class fields javascript** benut. Aan het einde heb je een volledige copy‑and‑paste‑snippet die in elke moderne browser werkt.

We behandelen alles, van het definiëren van een klasse met een publiek veld tot het aansluiten van een eenvoudige promise‑gebaseerde delay‑helper. Geen externe libraries, geen build‑stap—alleen platte HTML, een `<script type="module">`, en de nieuwste ECMAScript‑features. Als je al vertrouwd bent met async‑functies, zul je zien waarom top‑level await aanvoelt als een natuurlijke uitbreiding. Als je nieuw bent met de **javascript class public field**‑syntaxis, maak je geen zorgen—wij leggen het waarom achter elke regel uit.

## Wat je gaat leren

- Hoe een **top‑level await‑voorbeeld** werkt binnen een module‑script.
- Het patroon voor een `await delay javascript`‑helper die `setTimeout` nabootst met promises.
- Hoe je een **increment counter class** schrijft die een publiek veld (`count`) en een statisch initialisatieblok gebruikt.
- Verwachte console‑output en hoe je verifieert dat het statische blok wordt uitgevoerd vóór de rest van het script.
- Tips voor het oplossen van veelvoorkomende valkuilen, zoals oudere browsers die top‑level await niet ondersteunen.

> **Pro tip:** Moderne browsers (Chrome 106+, Firefox 102+, Edge 106+) ondersteunen al top‑level await. Als je oudere omgevingen moet ondersteunen, overweeg dan bundeling met een tool als Vite of Babel.

## Stap 1 – Definieer een klasse met een publiek veld en een statisch blok

Het eerste onderdeel van onze demo is een klasse die een numerieke teller opslaat. Let op de regel `count = 0;`—dit is de **public class fields javascript**‑syntaxis geïntroduceerd in ES2022. Het creëert een instantie‑eigenschap zonder constructor.

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

**Waarom een statisch blok?** Het stelt ons in staat om eenmalige initialisatielogica (zoals logging) uit te voeren op het moment dat de module wordt geparseerd, *voordat* enige top‑level await wordt uitgevoerd. Dit garandeert dat het bericht als eerste in de console verschijnt, wat bewijst dat de klasse vroeg werd geëvalueerd.

## Stap 2 – Maak een `await delay javascript`‑helper

Vervolgens hebben we een klein promise‑gebaseerd delay‑functie nodig. Het is in wezen een wrapper rond `setTimeout`, maar door een promise te retourneren wordt het await‑baar.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Edge case:** Als `ms` negatief of geen getal is, behandelt `setTimeout` het als `0`. Je zou validatie kunnen toevoegen, maar voor een demo houdt de één‑regelige versie de code leesbaar.

## Stap 3 – Gebruik top‑level await om uitvoering te pauzeren

Nu volgt de ster van de show: top‑level await. Omdat ons script een module is (`type="module"`), kunnen we `await` direct in de bovenste scope plaatsen. Dit pauzeert de module totdat de promise wordt opgelost, waardoor we de volgorde van side‑effects kunnen bepalen.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Veelgestelde vraag:** “Kan ik top‑level await gebruiken in een normale `<script>`‑tag?” Nee—alleen modulescripts ondersteunen dit. Als je `type="module"` vergeet, krijg je een syntax‑fout.

## Stap 4 – Instantieer de klasse, verhoog en log het resultaat

Tot slot zetten we alles bij elkaar: maak een instantie, roep `increment()` aan, en geef de uiteindelijke teller weer. Dit demonstreert de **increment counter class** in actie.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Verwachte console‑output

```
Counter class initialized
Final count: 1
```

Als je de pagina opent in DevTools, zou je het statische‑blok‑bericht **vóór** het einde van de delay moeten zien, wat bevestigt dat de klasse eerst werd geëvalueerd.

## Stap 5 – Waarom publieke klasse‑velden gebruiken in plaats van een constructor?

Je vraagt je misschien af waarom we niet schreven:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Beide benaderingen werken, maar **public class fields javascript** geven je een schonere, meer declaratieve syntaxis. Het veld wordt één keer gedefinieerd, niet binnen elke constructor‑aanroep, wat makkelijker leesbaar kan zijn wanneer de klasse groter wordt. Bovendien kunnen statische blokken niet binnen een constructor worden geplaatst, waardoor het scheiden van initialisatielogica natuurlijker wordt.

## Stap 6 – Het voorbeeld aanpassen voor real‑world apps

In productie heb je vaak meer dan één teller nodig. Hier zijn een paar snelle ideeën:

- **Meerdere tellers:** Bewaar ze in een `Map` met een identifier als sleutel.
- **Persistente staat:** Vervang `console.log` door writes naar `localStorage`.
- **Async initialisatie:** Gebruik het statische blok om configuratie van een server op te halen voordat er instanties worden gemaakt.

Al deze patronen profiteren nog steeds van top‑level await, omdat je data één keer kunt ophalen bij het laden van de module en kunt garanderen dat het klaar is voor elke consument.

## Veelgestelde vragen

**V: Blokkeert top‑level await andere modules?**  
A: Nee. Elke module draait onafhankelijk. Alleen de module die de await bevat wordt gepauzeerd; andere modules blijven parallel laden.

**V: Wat als de delay‑promise wordt afgewezen?**  
A: Een onbehandelde afwijzing stopt de evaluatie van de module en verschijnt als een fout in de console. Om een elegante fallback te bieden, wikkel je de await in een `try…catch`.

**V: Is het `static`‑keyword vereist?**  
A: Niet voor de teller zelf, maar het statische blok is een handige manier om te laten zien dat code *eenmalig* bij het laden wordt uitgevoerd—ideaal voor logging of feature‑detectie.

## Conclusie

Je hebt zojuist een **top‑level await‑voorbeeld** gebouwd dat `await delay javascript`, een **increment counter class**, en de kracht van **public class fields javascript** demonstreert. De volledige, uitvoerbare snippet staat hierboven, en de console‑output bewijst dat het statische blok vóór de vertraagde code wordt uitgevoerd.  

Vanaf hier kun je experimenteren met complexere async‑stromen, de delay vervangen door een echte API‑call, of de klasse uitbreiden met extra methoden. Onthoud dat modern JavaScript je toestaat modules te behandelen als eersteklas async‑entiteiten—geen extra wrappers nodig.

Veel plezier met coderen, en deel gerust je variaties in de reacties. Als je deze gids nuttig vond, deel hem dan met een collega die nog worstelt met async‑patronen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}