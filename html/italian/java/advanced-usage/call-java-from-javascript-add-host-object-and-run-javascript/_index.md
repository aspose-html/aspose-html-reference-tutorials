---
category: general
date: 2026-10-14
description: Chiama java da javascript usando Aspose.HTML. Scopri come aggiungere
  un oggetto host, eseguire javascript in java e fare il log da javascript in un tutorial
  conciso.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Chiama java da javascript usando Aspose.HTML. Questa guida mostra
  come aggiungere un oggetto host, eseguire javascript in java e fare il log da javascript,
  il tutto in poche righe di codice.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Chiama java da javascript – aggiungi un oggetto host e esegui javascript
  in java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Chiama java da javascript – aggiungi un oggetto host e esegui javascript in
  java
url: /it/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chiamare java da javascript – aggiungere un oggetto host ed eseguire javascript in java

Hai mai avuto bisogno di **call java from javascript** all'interno di un'applicazione Java? Forse stai costruendo un motore di report HTML dinamico o vuoi semplicemente esporre un logger Java a uno script controllato da te. In questo tutorial vedrai esattamente come aggiungere un oggetto host, eseguire JavaScript in Java e persino **log from JavaScript** di nuovo nella JVM—tutto con Aspose.HTML.

Percorreremo un esempio completo e eseguibile che crea un documento HTML vuoto, inietta una classe Java `Logger` come oggetto host, esegue un piccolo script e stampa il risultato sulla console. Nessun browser web esterno è necessario, nessuna “magia” mistica—solo codice Java puro che puoi copiare‑incollare ed eseguire oggi.

## Risposte rapide
- **Come aggiungo un oggetto host?** Registra un'istanza Java con `document.getWindow().addHostObject("name", object)`.  
- **Posso eseguire JavaScript in Java?** Sì—usa `document.getWindow().eval(yourScript)`.  
- **È possibile fare logging da JavaScript?** Assolutamente; l'oggetto host può esporre qualsiasi metodo `void log(String)`.  
- **Quale versione di Aspose.HTML è necessaria?** La versione 23.10 o successive supportano l'intera API degli oggetti host.  
- **Ho bisogno di un browser web?** No—Aspose.HTML fornisce un motore incorporato, quindi tutto gira in modalità head‑less.

## Cos'è call java from javascript?
**Call java from javascript** è la tecnica di esporre oggetti Java a un runtime JavaScript in modo che gli script possano invocare direttamente metodi Java. Aspose.HTML crea un motore JavaScript leggero all'interno di un processo Java, consentendo una comunicazione bidirezionale senza browser esterni.

## Perché usare Aspose.HTML per eseguire javascript in java?
Aspose.HTML supporta **oltre 50 formati di input e output** e può valutare JavaScript in un ambiente HTML5 pienamente conforme. Elabora script in circa 200 ms in media per codice a riga singola semplice, e lo fa senza caricare un intero stack di browser, riducendo l'uso di memoria fino all'80 % rispetto agli approcci basati su Selenium.

## Prerequisiti

- Java 17 (o qualsiasi JDK recente) installato e configurato.  
- Libreria Aspose.HTML per Java (versione 23.10 o successiva). Puoi ottenerla da Maven Central o dal sito Aspose.  
- Un IDE semplice o un editor di testo; l'esempio funziona anche da riga di comando.

> **Pro tip:** Se usi Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Oppure, per Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Ora che le basi sono pronte, immergiamoci nella soluzione passo‑passo.

## Come aggiungere un oggetto host e eseguire javascript in java?
`addHostObject` registra un oggetto Java come variabile globale nel contesto JavaScript. Carica il tuo `HTMLDocument`, registra un logger Java con il nome `"javaLogger"` usando `addHostObject`, e poi valuta un breve script che chiama `javaLogger.log`. L'intero flusso richiede solo tre chiamate API e funziona in qualsiasi runtime Java 17.

### Passo 1: crea un progetto java minimale

Per prima cosa, crea una nuova classe Java chiamata `JsHostObjectDemo`. La classe conterrà il nostro metodo `main` e la definizione dell'oggetto host. Tenere tutto in un unico file rende il tutorial autonomo e facile da copiare.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Perché un `HTMLDocument`?
`HTMLDocument` rappresenta un documento HTML in memoria e fornisce un motore JavaScript. La classe `HTMLDocument` avvia un ambiente di scripting HTML‑5 pienamente conforme. Anche se non carichiamo alcun markup, l'oggetto `window` del documento ci dà accesso al motore JavaScript, dove avviene la magia del **run javascript in java**. Inoltre è possibile manipolare il DOM, caricare risorse, o valutare script senza un browser.

## Come aggiungere l'oggetto host – “javaLogger”?
`Logger` è una semplice classe Java con un metodo `log(String)` che scrive messaggi sulla console. Registra l'istanza `Logger` con il nome `"javaLogger"` così che qualsiasi script valutato in questo documento possa chiamare `javaLogger.log(...)`. Questo è il fulcro della richiesta **add host object** e rende il logger disponibile come variabile globale per il codice JavaScript.

### Problemi comuni

- **Collisioni di nome** – Se nel tuo script esiste già una variabile globale chiamata `javaLogger`, l'oggetto host verrà sovrascritto. Scegli un nome univoco.  
- **Sicurezza dei thread** – L'oggetto host è condiviso tra le esecuzioni di script sullo stesso documento. Se prevedi di eseguire script in parallelo, rendi la classe host thread‑safe (ad esempio, usa `synchronized` o primitive di `java.util.concurrent`).

## Come scrivere ed eseguire javascript in java?
`eval` esegue una stringa JavaScript nel motore di scripting del documento e restituisce qualsiasi risultato. Fornisci un piccolo script a `eval`. Il motore risolve `javaLogger` dallo scope globale e invoca il suo metodo `log` con la stringa fornita. Puoi anche restituire valori, gestire eccezioni e concatenare più valutazioni per interazioni più complesse.

### Output previsto

L'esecuzione del metodo `main` stampa la seguente riga sulla console:

```
[JS] Hello from JavaScript!
```

## Come estendere l'host – più di un semplice logging?
Un oggetto host è qualsiasi istanza Java esposta a JavaScript tramite `addHostObject`. Aggiungi funzionalità extra aggiungendo metodi alla classe `Logger` o creando una nuova classe host. Di seguito un esempio rapido che restituisce anche un valore a JavaScript. L'oggetto host può esporre tipi complessi, eseguire I/O o interagire con altri servizi. Restituendo un valore, lo script può ricevere dati indietro, abilitando una comunicazione bidirezionale tra Java e JavaScript.

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Ora la console mostra:

```
[JS] 3+4=7
```

## Come pulire le risorse dopo l'esecuzione degli script?
`dispose` rilascia le risorse native detenute dall'istanza `HTMLDocument`. Quando hai finito di usare l'ambiente di scripting, chiama `dispose` sul `HTMLDocument` per liberare le risorse native. Non chiamare `dispose()` può provocare perdite di memoria, specialmente quando si creano molti documenti in cicli o servizi a lunga esecuzione. Avvolgi sempre l'uso in un blocco try‑with‑resources o assicurati che `document.dispose()` venga chiamato in un blocco finally.

```java
document.dispose(); // Important for long‑running applications
```

## Esempio completo funzionante

Di seguito il file sorgente completo che puoi compilare ed eseguire subito. Salvalo come `JsHostObjectDemo.java`, assicurati che il JAR di Aspose.HTML sia nel classpath, ed esegui `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

L'esecuzione di questo programma produce:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Domande frequenti

**D: Funziona su Android?**  
R: Sì. Aspose.HTML è una libreria pure‑Java, quindi gira su qualsiasi JVM, incluso il runtime ART di Android.

**D: E se devo passare oggetti complessi?**  
R: Puoi esporre POJO con getter e setter; il motore li mappa automaticamente a oggetti JavaScript. Collezioni come `java.util.List` o array sono anch'esse convertibili.

**D: Come funziona la gestione degli errori?**  
R: Se lo script lancia un errore JavaScript, `eval` propaga una `ScriptException`. Avvolgi la chiamata in un blocco try‑catch per registrare o recuperare.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**D: Posso eseguire più script in sequenza?**  
R: Assolutamente. Lo stesso `HTMLDocument` mantiene il suo scope globale, quindi puoi chiamare `eval` più volte. Gestisci i nomi delle variabili per evitare conflitti.

**D: L'oggetto host è sicuro per script non attendibili?**  
R: Tratta qualsiasi script esterno come input non attendibile. Convalida i parametri e considera l'uso di sandbox esponendo solo i metodi strettamente necessari.

## Best practice & consigli

- **Dai nomi chiari ai tuoi oggetti host**—`javaLogger`, `javaUtils`, ecc.—per evitare confusione.  
- **Mantieni i metodi host piccoli e privi di effetti collaterali** quando possibile; facilita il debug.  
- **Chiudi il documento** non appena hai finito; libera la memoria nativa allocata da Aspose.HTML.  
- **Convalida gli input** provenienti da JavaScript, specialmente se gli script provengono da fonti non attendibili. Trattali come qualsiasi dato esterno.

## Conclusione

Ora disponi di un esempio solido, end‑to‑end, su come **call java from javascript** tramite **adding a host object**, **running javascript in java**, e **logging from javascript** usando Aspose.HTML. Il pattern è potente: qualsiasi servizio Java può essere esposto a script, trasformando la tua applicazione Java in una piattaforma di scripting leggera.

Prossimi passi consigliati:

- Iniettare una pagina HTML completa e manipolare il DOM da JavaScript.  
- Usare l'oggetto host per trasmettere dati al lato Java (ad esempio, serializzazione JSON).  
- Integrare con altri motori di scripting come Nashorn o GraalVM per supportare più linguaggi.

Provalo, modifica le classi `Logger` o `Utils`, e scopri fin dove puoi spingere il concetto di **javascript host object** nei tuoi progetti.

---

**Ultimo aggiornamento:** 2026-10-14  
**Testato con:** Aspose.HTML per Java 23.10  
**Autore:** Aspose  






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Tutorial correlati

- [Enable Script Execution In Java Complete Aspose Html Guide](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Execute Javascript In Java Complete Guide To Running Js From](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [How To Sandbox Javascript Complete Aspose Html Guide](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}