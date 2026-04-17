---
category: general
date: 2026-03-26
description: Esempio di top‑level await che mostra await delay in JavaScript, classe
  di incremento del contatore e campi pubblici di classe in JavaScript in una demo
  live.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: it
og_description: Esempio di top‑level await che dimostra await delay in JavaScript,
  classe di incremento del contatore e campi di classe pubblici in JavaScript in un
  tutorial conciso.
og_title: Esempio di top‑level await – Utilizzo di await delay in JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Esempio di top‑level await – Utilizzare await delay in JavaScript
url: /it/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# esempio di top level await – Utilizzare await delay in JavaScript

Ti sei mai chiesto come mettere in pausa l'esecuzione di un modulo senza avvolgere tutto in un IIFE async? È esattamente quello che permette un **top level await example**. In questo tutorial percorreremo una piccola pagina web che utilizza `await delay javascript` per rimandare il lavoro, poi crea una `increment counter class` che sfrutta **public class fields javascript**. Alla fine avrai uno snippet completo, pronto da copiare‑incollare, che funziona in qualsiasi browser moderno.

Copriamo tutto, dalla definizione di una classe con un campo pubblico al collegamento di un semplice helper di delay basato su promise. Nessuna libreria esterna, nessun passaggio di build—solo HTML puro, un `<script type="module">` e le più recenti funzionalità ECMAScript. Se sei già a tuo agio con le funzioni async, vedrai perché il top‑level await sembra un'estensione naturale. Se sei nuovo alla sintassi **javascript class public field**, non preoccuparti—spieghiamo il perché di ogni riga.

## Cosa imparerai

- Come funziona un **top level await example** all'interno di uno script di modulo.
- Il pattern per un helper `await delay javascript` che imita `setTimeout` con le promise.
- Come scrivere una **increment counter class** che utilizza un campo pubblico (`count`) e un blocco di inizializzazione statico.
- L'output previsto della console e come verificare che il blocco statico venga eseguito prima del resto dello script.
- Suggerimenti per risolvere problemi comuni, come i browser più vecchi che non supportano il top‑level await.

> **Consiglio professionale:** I browser moderni (Chrome 106+, Firefox 102+, Edge 106+) supportano già il top‑level await. Se devi supportare ambienti più vecchi, considera di fare il bundle con uno strumento come Vite o Babel.

## Passo 1 – Definire una classe con un campo pubblico e un blocco statico

Il primo elemento della nostra demo è una classe che memorizza un contatore numerico. Nota la riga `count = 0;`—questa è la sintassi **public class fields javascript** introdotta in ES2022. Crea una proprietà di istanza senza un costruttore.

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

**Perché un blocco statico?** Consente di eseguire una logica di inizializzazione una tantum (come il logging) nel momento in cui il modulo viene analizzato, *prima* che venga eseguito qualsiasi top‑level await. Questo garantisce che il messaggio appaia per primo nella console, dimostrando che la classe è stata valutata in anticipo.

## Passo 2 – Creare un helper `await delay javascript`

Ora abbiamo bisogno di una piccola funzione di delay basata su promise. È essenzialmente un wrapper attorno a `setTimeout`, ma restituire una promise la rende attendibile.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Caso limite:** Se `ms` è negativo o non è un numero, `setTimeout` lo tratta come `0`. Potresti aggiungere una validazione, ma per una demo la singola riga mantiene il codice leggibile.

## Passo 3 – Usare il Top‑Level Await per mettere in pausa l'esecuzione

Ora arriva la star dello spettacolo: il top‑level await. Poiché il nostro script è un modulo (`type="module"`), possiamo inserire `await` direttamente nello scope superiore. Questo mette in pausa il modulo finché la promise non si risolve, permettendoci di controllare l'ordine degli effetti collaterali.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Domanda comune:** “Posso usare il top‑level await in un normale tag `<script>`?” No—solo gli script di tipo modulo lo supportano. Se dimentichi `type="module"`, otterrai un errore di sintassi.

## Passo 4 – Istanziare la classe, incrementare e registrare il risultato

Infine mettiamo tutto insieme: creiamo un'istanza, chiamiamo `increment()`, e stampiamo il conteggio finale. Questo dimostra la **increment counter class** in azione.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Output previsto della console

```
Counter class initialized
Final count: 1
```

Se apri la pagina in DevTools, dovresti vedere il messaggio del blocco statico apparire **prima** che il delay termini, confermando che la classe è stata valutata per prima.

## Passo 5 – Perché usare i campi pubblici della classe invece di un costruttore?

Potresti chiederti perché non abbiamo scritto:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Entrambi gli approcci funzionano, ma **public class fields javascript** offrono una sintassi più pulita e dichiarativa. Il campo è definito una sola volta, non all'interno di ogni chiamata al costruttore, il che può risultare più leggibile quando la classe diventa più grande. Inoltre, i blocchi statici non possono essere inseriti dentro un costruttore, quindi separare la logica di inizializzazione diventa più naturale.

## Passo 6 – Adattare l'esempio per applicazioni reali

In produzione avrai spesso bisogno di più di un singolo contatore. Ecco alcune idee rapide:

- **Contatori multipli:** Memorizzali in una `Map` indicizzata per identificatore.
- **Stato persistente:** Sostituisci `console.log` con scritture su `localStorage`.
- **Inizializzazione async:** Usa il blocco statico per recuperare la configurazione da un server prima che vengano create le istanze.

Tutti questi pattern traggono ancora vantaggio dal top‑level await, perché puoi recuperare i dati una sola volta al caricamento del modulo e garantire che siano pronti per ogni consumatore.

## Domande frequenti

**Q: Il top‑level await blocca altri moduli?**  
A: No. Ogni modulo viene eseguito in modo indipendente. Solo il modulo che contiene l'await è messo in pausa; gli altri moduli continuano a caricarsi in parallelo.

**Q: Cosa succede se la promise di delay viene rifiutata?**  
A: Un rifiuto non gestito interromperà la valutazione del modulo e verrà mostrato come errore nella console. Avvolgi l'await in un `try…catch` se hai bisogno di un fallback elegante.

**Q: La parola chiave `static` è obbligatoria?**  
A: Non per il contatore stesso, ma il blocco statico è un modo comodo per dimostrare che il codice viene eseguito *una sola volta* al momento del caricamento—ottimo per logging o rilevamento di funzionalità.

## Conclusione

Hai appena costruito un **top level await example** che mostra `await delay javascript`, una **increment counter class**, e la potenza di **public class fields javascript**. Lo snippet completo e eseguibile è qui sopra, e l'output della console dimostra che il blocco statico viene eseguito prima del codice con delay.

Da qui puoi sperimentare flussi async più complessi, sostituire il delay con una chiamata API reale, o espandere la classe con metodi aggiuntivi. Ricorda, il JavaScript moderno ti permette di trattare i moduli come entità async di prima classe—senza wrapper aggiuntivi.

Buon coding, e sentiti libero di condividere le tue varianti nei commenti. Se hai trovato utile questa guida, condividila con un collega che sta ancora lottando con i pattern async!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}