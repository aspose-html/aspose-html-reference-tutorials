---
category: general
date: 2026-05-28
description: Recupera dati API in Java usando Aspose.HTML – impara come eseguire JavaScript
  asincrono, eseguire script asincrono e impostare l'attributo DOM dal JSON recuperato.
draft: false
keywords:
- fetch api data
- execute async javascript
- run async script
- set dom attribute
- how to run async
language: it
og_description: Recupera i dati dell'API in Java con Aspose.HTML. Questo tutorial
  mostra come eseguire JavaScript asincrono, eseguire script asincroni e impostare
  l'attributo DOM dai risultati dell'API.
og_title: Recupera dati API in Java – Guida passo‑passo Aspose.HTML
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
title: Recupera i dati dell'API in Java con Aspose.HTML - Guida completa
url: /it/java/message-handling-networking/fetch-api-data-in-java-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Recuperare dati API in Java con Aspose.HTML – Guida completa

Ti sei mai chiesto come **fetch api data** in Java senza lasciare il comfort del tuo IDE? Non sei solo. Molti sviluppatori si trovano in difficoltà quando devono chiamare un servizio remoto da una pagina HTML renderizzata da Aspose.HTML e poi riportare il risultato in Java.  

In questo tutorial vedremo un esempio pratico che **executes async javascript**, esegue un **async script** e infine **sets a DOM attribute** con il valore recuperato. Alla fine saprai esattamente *how to run async* operazioni in modo sicuro e recuperare i dati di cui hai bisogno.

## Cosa costruirai

Creeremo una piccola applicazione console Java che:

1. Carica un file HTML contenente una funzione async.  
2. Esegue uno script che utilizza la **fetch API** per chiamare l'endpoint pubblico di GitHub.  
3. Attende che la promise si risolva (fino a 10 secondi).  
4. Memorizza il conteggio delle stelle in un attributo personalizzato `data-stars` sull'elemento `<body>`.  
5. Legge quell'attributo in Java e lo stampa.

Nessuna libreria client HTTP esterna, nessun codice di threading aggiuntivo—solo Aspose.HTML che fa il lavoro pesante.

## Prerequisiti

- **Java 17** o versioni più recenti (il codice si compila con versioni precedenti, ma 17 è l'LTS attuale).  
- Libreria **Aspose.HTML for Java** (versione 23.9 o successiva).  
- Un semplice file HTML (`async-page.html`) posizionato da qualche parte sul disco.  
- Una connessione internet (la chiamata fetch colpisce `https://api.github.com`).  

If you already have a Maven project, add the Aspose.HTML dependency:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

Ora, immergiamoci nel codice.

## Passo 1: Preparare la pagina HTML

Per prima cosa, crea un file HTML minimale che ospiterà la funzione async. Non serve alcun markup elaborato—solo un tag `<body>`.

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

Salva questo file in una posizione accessibile, ad esempio `C:/temp/async-page.html`. Il percorso sarà usato nel codice Java.

![esempio di fetch api data](https://example.com/fetch-api-data.png "esempio di fetch api data")

*Testo alternativo dell'immagine: esempio di fetch api data che mostra l'output della console delle stelle di GitHub.*

## Passo 2: Caricare il documento HTML in Java

Con il file HTML pronto, lo apriamo usando `HTMLDocument` di Aspose.HTML. Il blocco `try‑with‑resources` garantisce che il documento venga smaltito correttamente.

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

Perché usare `HTMLDocument`? Ci fornisce un DOM completo, un motore JavaScript integrato e un modo comodo per interagire con la pagina da Java—tutto senza avviare un browser.

## Passo 3: Scrivere lo script async

Ora creiamo uno snippet JavaScript che **fetches API data**, attende la promise e poi **sets a DOM attribute**. Nota l'uso di `async/await`—lo stesso pattern che scriveresti in un browser.

```java
String script =
    "async function run() {" +
    "  const data = await fetch('https://api.github.com').then(r => r.json());" +
    "  document.body.setAttribute('data-stars', data.stargazers_count);" +
    "}" +
    "run();";
```

Alcune cose da evidenziare:

- La funzione `run` è dichiarata `async`, quindi possiamo `await` la chiamata `fetch`.  
- Dopo aver analizzato il JSON, memorizziamo `data.stargazers_count` in un attributo personalizzato `data-stars`.  
- Infine invochiamo `run()` immediatamente.  

Questo piccolo script fa tutto ciò di cui abbiamo bisogno per **run async script** e catturare il risultato.

## Passo 4: Eseguire lo script e attendere

Il `ScriptEngine` di Aspose.HTML può valutare JavaScript con un timeout. Passando `10000` indichiamo al motore di attendere fino a **10 secondi** per il completamento dell'operazione async.

```java
// Execute the script and wait (up to 10 seconds) for the async operation to finish
ScriptEngine engine = doc.getScriptEngine();
engine.evaluate(script, 10000);   // timeout in milliseconds
```

Se la richiesta supera il timeout, viene sollevata una `ScriptException`—perfetta per gestire condizioni di rete instabili. In produzione probabilmente avvolgerai questo in un try‑catch e riproverai se necessario.

## Passo 5: Recuperare l'attributo da Java

Dopo che lo script è completato, l'attributo `data-stars` fa ora parte del DOM. Recuperalo in Java con una semplice chiamata:

```java
// Retrieve the value set by the script from the document
String stars = doc.getBody().getAttribute("data-stars");
System.out.println("GitHub stars: " + stars);
```

Quella riga stampa qualcosa come `GitHub stars: 12345`. Il numero esatto cambia quotidianamente, ma il modello rimane lo stesso.

## Esempio completo funzionante

Mettendo insieme tutti i pezzi, ecco il programma completo, pronto‑da‑eseguire:

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

### Output previsto

```
GitHub stars: 84327
```

(Il tuo numero sarà diverso; la parte importante è che il valore è una **string** che rappresenta il conteggio delle stelle.)

## Domande comuni e casi particolari

### Cosa succede se la chiamata fetch fallisce?

Lo script solleverà un'eccezione JavaScript, che si propaga a `ScriptEngine.evaluate`. Puoi catturarla in Java:

```java
try {
    engine.evaluate(script, 10000);
} catch (ScriptException e) {
    System.err.println("Failed to fetch data: " + e.getMessage());
}
```

### Posso fare fetch da un'API privata che richiede autenticazione?

Certo—basta aggiungere gli header appropriati nello script:

```javascript
await fetch('https://api.example.com/secure', {
    headers: { 'Authorization': 'Bearer YOUR_TOKEN' }
}).then(r => r.json());
```

Ricorda di tenere i segreti fuori dal controllo di versione.

### Funziona su versioni Java più vecchie?

Aspose.HTML include il proprio motore JavaScript, quindi non hai bisogno di Nashorn o GraalVM. Tuttavia, la sintassi `try‑with‑resources` richiede Java 7+. Per Java 6 dovresti chiudere manualmente il documento.

## Consigli professionali

- **Reuse the ScriptEngine**: Se devi eseguire molti script async, mantieni viva un'unica istanza del motore—riduce l'overhead.  
- **Increase the timeout** per API più lente, ma non impostarlo a `Integer.MAX_VALUE`; vuoi comunque una rete di sicurezza.  
- **Validate the attribute** prima di usarla. L'attributo DOM potrebbe essere `null` se lo script non è mai stato eseguito.  
- **Log the raw JSON** durante lo sviluppo; è utile quando l'API cambia struttura.

## Prossimi passi

Ora che sai come **fetch api data**, puoi estendere il pattern:

- **Parse more complex JSON** e iniettare più attributi.  
- **Create tables** all'interno della pagina HTML basate sui dati recuperati.  
- **Combine with Aspose.PDF** per generare un PDF che contiene risultati API in tempo reale.  

Ognuno di questi si basa sulle stesse idee fondamentali: **execute async javascript**, **run async script**, e **set dom attribute** dal risultato. Sentiti libero di sperimentare—c'è molto potere nascosto nel motore script di Aspose.HTML.

---

*Buona programmazione! Se hai incontrato problemi, lascia un commento qui sotto e risolveremo insieme.*

## Tutorial correlati

- [Come eseguire JavaScript in Java – Guida completa](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Aggiungere un elemento al body con Aspose.HTML per Java usando un DOM Mutation Observer](/html/english/java/advanced-usage/dom-mutation-observer-observing-node-additions/)
- [Come impostare il timeout – Gestire il timeout di rete in Aspose.HTML per Java](/html/english/java/message-handling-networking/network-timeout/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}