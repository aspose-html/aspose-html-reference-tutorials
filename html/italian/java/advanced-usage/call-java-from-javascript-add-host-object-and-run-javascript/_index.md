---
category: general
date: 2026-03-14
description: Scopri come chiamare Java da JavaScript usando Aspose.HTML. Questa guida
  mostra come aggiungere un oggetto host, eseguire JavaScript in Java e fare il log
  da JavaScript.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: it
og_description: Chiama Java da JavaScript usando Aspose.HTML. Aggiungi un oggetto
  host, esegui JavaScript in Java e registra i log da JavaScript in un unico tutorial.
og_title: Chiama Java da JavaScript – Guida completa con oggetto host
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Chiamare Java da JavaScript – Aggiungere un oggetto host ed eseguire JavaScript
  in Java
url: /it/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chiamare Java da JavaScript – Aggiungere un oggetto host ed eseguire JavaScript in Java

Hai mai dovuto **chiamare Java da JavaScript** all'interno di un'applicazione Java? Forse stai costruendo un motore di report HTML dinamico o semplicemente vuoi esporre un logger Java a uno script che controlli. In questo tutorial vedrai esattamente come aggiungere un oggetto host, eseguire JavaScript in Java e persino **loggare da JavaScript** al JVM—tutto con Aspose.HTML.

Percorreremo un esempio completo e funzionante che crea un documento HTML vuoto, inietta una classe Java `Logger` come oggetto host, esegue un piccolo script e stampa il risultato sulla console. Nessun browser esterno richiesto, nessuna “magia” misteriosa—solo codice Java puro che puoi copiare‑incollare ed eseguire subito.

## Prerequisiti

- Java 17 (o qualsiasi JDK recente) installato e configurato.  
- Libreria Aspose.HTML per Java (versione 23.10 o successiva). Puoi ottenerla da Maven Central o dal sito Aspose.  
- Un IDE semplice o un editor di testo; l'esempio funziona anche da riga di comando.

> **Suggerimento:** Se usi Maven, aggiungi la seguente dipendenza al tuo `pom.xml`:

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

Ora che abbiamo sistemato le basi, immergiamoci nella soluzione passo‑per‑passo.

## Step 1: Creare un progetto Java minimale

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

La classe `HTMLDocument` di Aspose.HTML avvia un ambiente di scripting completo conforme a HTML‑5. Anche se non carichiamo alcun markup, l'oggetto `window` del documento ci dà accesso al motore JavaScript, dove avviene la magia del **run JavaScript in Java**.

## Step 2: Aggiungere l'oggetto host – “javaLogger”

La riga

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

esegue il lavoro pesante per il requisito di **add host object**. Registrando l'istanza `Logger` con il nome `"javaLogger"`, qualsiasi script valutato in questo documento può chiamare `javaLogger.log(...)`. Questo è il fulcro del concetto di **javascript host object**: un ponte che permette a JavaScript di accedere alla JVM.

### Problemi comuni

- **Collisioni di nome** – Se nel tuo script esiste già una variabile globale chiamata `javaLogger`, l'oggetto host verrà sovrascritto. Scegli un nome univoco.  
- **Sicurezza dei thread** – L'oggetto host è condiviso tra le esecuzioni di script sullo stesso documento. Se prevedi di eseguire script in parallelo, rendi la classe host thread‑safe (ad esempio, usa `synchronized` o primitive di `java.util.concurrent`).

## Step 3: Scrivere ed eseguire JavaScript

Lo script che passiamo a `eval` è deliberatamente piccolo:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Quando `document.getWindow().eval(script)` viene eseguito, il motore cerca `javaLogger` nello scope globale, trova l'oggetto Java che abbiamo aggiunto e invoca il suo metodo `log` con la stringa fornita.

### Output previsto

Eseguendo il metodo `main` viene stampata la seguente riga sulla console:

```
[JS] Hello from JavaScript!
```

Quella piccola riga dimostra che abbiamo **call java from javascript** con successo, e il **log from javascript** appare esattamente dove comparirebbe un normale messaggio `System.out` di Java.

## Step 4: Estendere l'host – più di un semplice logger

Se devi esporre funzionalità aggiuntive (ad esempio accesso a file, query di database), aggiungi semplicemente altri metodi alla classe `Logger`—oppure crea una nuova classe host. Ecco un rapido esempio che restituisce anche un valore:

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

Questo dimostra la flessibilità del pattern **javascript host object**: puoi esporre qualsiasi API Java ti serva, purché i tipi di dato siano convertibili tra Java e JavaScript (primitive, stringhe, array, ecc.).

## Step 5: Pulire le risorse

Quando hai finito di usare l'ambiente di scripting, elimina il `HTMLDocument` per liberare le risorse native:

```java
document.dispose(); // Important for long‑running applications
```

Saltare la fase di disposal può causare perdite di memoria, specialmente se crei molti documenti in un ciclo.

## Esempio completo funzionante

Di seguito trovi il file sorgente completo che puoi compilare ed eseguire subito. Salvalo come `JsHostObjectDemo.java`, assicurati che il JAR di Aspose.HTML sia nel classpath e avvia `java JsHostObjectDemo`.

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

Eseguendo questo programma ottieni:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

Questo è l’intero workflow di **call java from javascript** in poche righe di codice.

## Domande frequenti

### Funziona su Android?

Aspose.HTML è una libreria pure‑Java, quindi gira su qualsiasi JVM, compreso Dalvik/ART di Android. Basta includere il JAR e avrai le stesse capacità di host‑object.

### E se devo passare oggetti complessi?

Puoi esporre POJO (plain old Java objects) con campi, getter e setter. Il motore li mapperà automaticamente a oggetti JavaScript. Per le collezioni, usa `java.util.List` o array—entrambi sono convertibili.

### Come funziona la gestione degli errori?

Se lo script genera un errore JavaScript, `eval` propaga una `ScriptException`. Avvolgi la chiamata in un blocco try‑catch per loggare o recuperare:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Posso eseguire più script in sequenza?

Assolutamente. La stessa istanza di `HTMLDocument` mantiene lo scope globale, quindi puoi chiamare `eval` più volte. Fai solo attenzione a eventuali collisioni di nome tra gli script.

## Best practice e consigli

- **Dai nomi chiari ai tuoi oggetti host**—`javaLogger`, `javaUtils`, ecc.—per evitare confusione.  
- **Mantieni i metodi host piccoli e privi di effetti collaterali** quando possibile; facilita il debug.  
- **Elimina il documento** non appena hai finito; libera la memoria nativa allocata da Aspose.HTML.  
- **Convalida gli input** provenienti da JavaScript, soprattutto se gli script provengono da fonti non fidate. Trattali come qualsiasi altro dato esterno.

## Conclusione

Ora disponi di un esempio solido, end‑to‑end, su come **call java from javascript** tramite **adding a host object**, **running JavaScript in Java** e **logging from JavaScript** usando Aspose.HTML. Il pattern è potente: qualsiasi servizio Java può essere esposto agli script, trasformando la tua applicazione Java in una piattaforma di scripting leggera.

Prossimi passi da esplorare:

- Iniettare una pagina HTML completa e manipolare il DOM da JavaScript.  
- Usare l'oggetto host per trasmettere dati al lato Java (ad esempio serializzazione JSON).  
- Integrare altri motori di scripting come Nashorn o GraalVM per supportare più linguaggi.

Provalo, modifica le classi `Logger` o `Utils`, e scopri fin dove puoi spingere il concetto di **javascript host object** nei tuoi progetti.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}