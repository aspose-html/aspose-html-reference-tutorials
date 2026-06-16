---
category: general
date: 2026-06-16
description: Carica JSON con fetch usando Java. Impara come eseguire JavaScript da
  Java, l'optional chaining e creare HTMLDocument in Java in un unico tutorial.
draft: false
keywords:
- load json with fetch
- fetch json in javascript
- run javascript from java
- optional chaining tutorial
- create htmldocument in java
language: it
og_description: Carica JSON con fetch usando Java. Questo tutorial mostra come eseguire
  JavaScript da Java, utilizzare l'optional chaining e creare HTMLDocument in Java.
og_title: Carica JSON con Fetch in Java – Guida passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Load JSON with fetch using Java. Learn how to run JavaScript from Java,
    optional chaining, and create HTMLDocument in Java in one tutorial.
  headline: Load JSON with Fetch in Java – Complete Guide
  type: TechArticle
- description: Load JSON with fetch using Java. Learn how to run JavaScript from Java,
    optional chaining, and create HTMLDocument in Java in one tutorial.
  name: Load JSON with Fetch in Java – Complete Guide
  steps:
  - name: Expected Output
    text: '``` Title: delectus aut autem ```'
  - name: 1. What if the target API returns a non‑JSON response?
    text: '`response.json()` will throw a `SyntaxError`. Our `try/catch` block captures
      that, logging “Fetch failed”. You can extend the catch to retry or fallback
      to a static payload.'
  - name: 2. Can I use this approach with HTTPS certificates that aren’t trusted?
    text: The built‑in `fetch` respects the JVM’s default SSL context. If you need
      to trust a self‑signed cert, set a custom `SSLContext` before creating the `HTMLDocument`.
      That’s a bit beyond this tutorial, but the principle stays the same.
  - name: 3. Does this work on Android?
    text: Unfortunately, `HTMLDocument` isn’t part of the Android SDK. For mobile,
      you’d need a different JavaScript engine (e.g., GraalVM) or a native HTTP client.
  - name: 4. How does optional chaining differ from classic null checks?
    text: 'Instead of writing:'
  type: HowTo
tags:
- Java
- JavaScript
- Fetch API
- HTMLDocument
- Scripting
title: Carica JSON con Fetch in Java – Guida completa
url: /it/java/creating-managing-html-documents/load-json-with-fetch-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Carica JSON con Fetch – Tutorial Java Completo

Ti sei mai chiesto come **caricare JSON con fetch** rimanendo all'interno di una pura applicazione Java? Non sei l'unico. Molti sviluppatori si trovano in difficoltà quando devono chiamare un endpoint REST moderno ma non vogliono includere una pesante libreria client HTTP. La buona notizia? Puoi sfruttare la potenza della classe `HTMLDocument` simile a un browser, avviare un motore JavaScript e lasciare che `fetch` faccia il lavoro pesante—tutto da Java.

In questa guida percorreremo un esempio pratico che **recupera JSON in JavaScript**, esegue quello script da Java e mostra anche l'optional chaining. Alla fine saprai come **eseguire JavaScript da Java**, creare un `HTMLDocument` in Java e gestire elegantemente i campi JSON mancanti. Nessuna dipendenza esterna, solo il JDK e un pizzico di creatività.

## Cosa Copre Questo Tutorial

- Configurare un'istanza `HTMLDocument` in Java (`create htmldocument in java`).
- Ottenere il `ScriptEngine` incorporato e fornire JavaScript moderno.
- Scrivere uno snippet **fetch JSON in JavaScript** che utilizza `async/await` e optional chaining (`optional chaining tutorial`).
- Eseguire lo script tramite `engine.evaluate` (`run javascript from java`).
- Verificare l'output e gestire casi limite come errori di rete o proprietà mancanti.

Avrai bisogno di Java 17 o superiore, perché la demo si basa sul motore integrato compatibile con Nashorn fornito con il JDK. Se utilizzi un JDK più vecchio, aggiungi semplicemente la libreria di scripting appropriata—i dettagli sono nella sezione “Prerequisiti”.

---

## Prerequisiti

- **JDK 17+** installato e `JAVA_HOME` configurato.
- Familiarità di base con la sintassi Java e JavaScript asincrono.
- Un IDE o editor di testo (IntelliJ IDEA, VS Code, Eclipse—a tua scelta).

Non è necessario alcun client HTTP di terze parti o parser JSON; tutto vive all'interno dello script.

---

## Passo 1: Crea un HTMLDocument in Java

Prima di tutto—**create htmldocument in java**. La classe `HTMLDocument` ci fornisce un DOM leggero e, cosa più importante, un `ScriptEngine` integrato che può valutare JavaScript proprio come farebbe un browser.

```java
import org.w3c.dom.html.HTMLDocument;
import javax.script.ScriptEngine;

// Step 1: Instantiate an empty HTMLDocument.
HTMLDocument doc = new HTMLDocument();
```

> **Perché è importante:** L'`HTMLDocument` funge da sandbox. Fornisce un oggetto globale `window`, `fetch` e altre API web a cui lo script può accedere. Pensalo come un mini‑browser senza interfaccia.

---

## Passo 2: Ottieni il Motore JavaScript dal Documento

Ora dobbiamo **run javascript from java**. Il documento espone un `ScriptEngine` che comprende ECMAScript moderno (incluso `async/await`). Ottienilo così:

```java
// Step 2: Obtain the scripting engine linked to the document.
ScriptEngine engine = doc.getScriptEngine();
```

> **Consiglio professionale:** Se dovessi incontrare una `ScriptException` per funzionalità non supportate, assicurati di essere su JDK 17+. I JDK più vecchi includono un motore Nashorn legacy che non supporta async.

---

## Passo 3: Scrivi uno Snippet JavaScript Moderno (Tutorial Optional Chaining)

Ecco dove brilla la parte **fetch json in javascript**. Definiremo una stringa multilinea (blocco di testo Java 15+ `"""`) che recupera un payload JSON di esempio, usa `await` e dimostra l'optional chaining (`??`) per gestire valori mancanti.

```java
// Step 3: Define a modern JavaScript snippet.
String script = """
    async function loadData() {
        try {
            const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
            if (!response.ok) {
                console.error('Network error:', response.status);
                return;
            }
            const data = await response.json();
            // optional chaining tutorial – safely access title
            console.log('Title:', data.title ?? 'No title');
        } catch (err) {
            console.error('Fetch failed:', err);
        }
    }
    loadData();
    """;
```

**Cosa sta succedendo?**

- `fetch` invia una richiesta GET a una API placeholder pubblica.
- `await` sospende l'esecuzione finché la promise non si risolve, mantenendo il codice pulito.
- `data.title ?? 'No title'` è il pattern di optional chaining: se `title` è `null` o `undefined`, si ricade su `'No title'`.
- L'intero blocco è avvolto in un `try/catch` per evidenziare eventuali problemi di rete.

---

## Passo 4: Esegui lo Script all'interno del Documento

Infine, passiamo lo script al motore. Il motore lo esegue nello stesso thread, così vedrai l'output della console direttamente nel tuo processo Java.

```java
// Step 4: Run the JavaScript within the document's scripting environment.
engine.evaluate(script);
```

Quando esegui il programma, dovresti vedere qualcosa di simile:

```
Title: delectus aut autem
```

Se l'API cambia o il campo `title` scompare, l'output passa elegantemente a:

```
Title: No title
```

Questa è la bellezza dell'optional chaining—nessun `TypeError` che fa saltare la tua app Java.

---

## Esempio Completo Funzionante

Mettendo tutto insieme, ecco una classe Java autonoma che puoi copiare‑incollare in `Main.java` e eseguire con `java Main.java`.

```java
import org.w3c.dom.html.HTMLDocument;
import javax.script.ScriptEngine;
import javax.script.ScriptException;

public class Main {
    public static void main(String[] args) throws ScriptException {
        // 1️⃣ Create an empty HTMLDocument.
        HTMLDocument doc = new HTMLDocument();

        // 2️⃣ Get the JavaScript engine tied to the document.
        ScriptEngine engine = doc.getScriptEngine();

        // 3️⃣ Define a script that loads JSON with fetch and uses optional chaining.
        String script = """
            async function loadData() {
                try {
                    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                    if (!response.ok) {
                        console.error('Network error:', response.status);
                        return;
                    }
                    const data = await response.json();
                    // optional chaining tutorial – safely access title
                    console.log('Title:', data.title ?? 'No title');
                } catch (err) {
                    console.error('Fetch failed:', err);
                }
            }
            loadData();
            """;

        // 4️⃣ Execute the script.
        engine.evaluate(script);
    }
}
```

### Output Atteso

```
Title: delectus aut autem
```

Se rompi deliberatamente l'URL (ad esempio, cambi `todos/1` in `todos/9999`), vedrai il messaggio di fallback o un errore di rete, dimostrando una gestione degli errori robusta.

---

## Domande Frequenti & Casi Limite

### 1. E se l'API di destinazione restituisce una risposta non‑JSON?

`response.json()` lancerà un `SyntaxError`. Il nostro blocco `try/catch` cattura questo, registrando “Fetch failed”. Puoi estendere il catch per ritentare o ricorrere a un payload statico.

### 2. Posso usare questo approccio con certificati HTTPS non fidati?

`fetch` integrato rispetta il contesto SSL predefinito della JVM. Se devi fidarti di un certificato autofirmato, imposta un `SSLContext` personalizzato prima di creare l'`HTMLDocument`. È un po' oltre questo tutorial, ma il principio rimane lo stesso.

### 3. Funziona su Android?

Sfortunatamente, `HTMLDocument` non fa parte dell'SDK Android. Per mobile, avresti bisogno di un motore JavaScript diverso (ad es., GraalVM) o di un client HTTP nativo.

### 4. In che modo l'optional chaining differisce dai classici controlli null?

Invece di scrivere:

```javascript
if (data && data.title) {
    console.log(data.title);
} else {
    console.log('No title');
}
```

puoi semplicemente fare `data.title ?? 'No title'`. È conciso, meno soggetto a errori, e legge come un linguaggio naturale—perfetto per un **optional chaining tutorial**.

---

## Consigli Pro & Buone Pratiche

- **Riutilizza il motore:** Creare un nuovo `HTMLDocument` per ogni richiesta può essere costoso. Mantieni un'unica istanza viva se fai molte chiamate.
- **Sicurezza dei thread:** Il `ScriptEngine` non è thread‑safe di default. Sincronizza l'accesso o crea un pool di engine per carichi di lavoro concorrenti.
- **Logging:** Il `console.log` dello script scrive su `System.out`. Se ti serve un framework di logging adeguato, reindirizza `engine.getContext().setWriter(new PrintWriter(...))`.
- **Timeout:** `fetch` rispetta il timeout predefinito del browser (di solito nessuno). Puoi implementare un abort manuale usando l'API `AbortController` nello script se hai bisogno di un controllo più rigoroso.

---

## Conclusione

Abbiamo appena dimostrato come **load JSON with fetch** da un programma Java, sfruttando un motore JavaScript incorporato per eseguire codice `async/await` moderno e usando l'optional chaining per mantenere le cose ordinate. **Creando un HTMLDocument in Java**, ottieni un ambiente sandbox che rende **running JavaScript from Java** naturale, rimanendo comunque all'interno di codice Java puro.

Da qui potresti:

- Sostituire l'API placeholder con il tuo servizio (`fetch json in javascript` da un endpoint privato).
- Aggiungere una gestione degli errori o dei retry più sofisticata.
- Esplorare le capacità poliglotte di GraalVM per uno scripting ancora più ricco.

Provalo, modifica l'URL, magari aggiungi una richiesta `POST`—c'è un intero mondo di Java centrato sul web che puoi sbloccare senza introdurre librerie pesanti.

Buon coding, e sentiti libero di lasciare un commento se incontri problemi!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come Eseguire JavaScript in Java – Guida Completa](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Come Interrogare HTML in Java – Tutorial Completo](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Carica Documenti HTML da URL in Aspose.HTML per Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}