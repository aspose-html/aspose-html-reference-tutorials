---
category: general
date: 2026-06-19
description: Come avviare un thread in Java con un Runnable riutilizzabile, avviare
  più thread, stampare il nome del thread e analizzare HTML con Java. Esempio passo‑passo.
draft: false
keywords:
- how to start thread
- start multiple threads
- print thread name
- parse html with java
- how to use runnable
language: it
og_description: Come avviare un thread in Java usando Runnable, eseguire più thread,
  stampare il nome del thread e analizzare HTML con Java in un unico esempio eseguibile.
og_title: Come avviare un thread in Java – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to start thread in Java with a reusable Runnable, start multiple
    threads, print thread name, and parse HTML with Java. Step‑by‑step example.
  headline: How to start thread in Java – Complete Guide
  type: TechArticle
tags:
- java
- multithreading
- html-parsing
- runnable
title: Come avviare un thread in Java – Guida completa
url: /it/java/creating-managing-html-documents/how-to-start-thread-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come avviare un thread in Java – Guida completa

Ti sei mai chiesto **come avviare un thread** in Java senza annegare nel codice boilerplate? Non sei l'unico. Che tu stia costruendo un web crawler, un aggiornatore di UI, o semplicemente abbia bisogno di delegare un calcolo pesante, padroneggiare la creazione dei thread è una competenza indispensabile per ogni sviluppatore Java.

In questo tutorial percorreremo uno scenario pratico: **analizzare HTML con Java**, stampare il nome del thread corrente e **avviare più thread** che condividono la stessa logica. Alla fine saprai **come usare Runnable**, avviare diversi worker e vedere l'output atteso — il tutto in un esempio autonomo che puoi copiare‑incollare subito.

## Cosa imparerai

- I passaggi esatti **come avviare un thread** usando la classe `Thread` e un `Runnable`.
- Come **avviare più thread** che eseguono lo stesso compito senza duplicare il codice.
- Il modo più semplice per **stampare il nome del thread** accanto ai risultati del tuo processamento.
- Un metodo pulito per **analizzare HTML con Java** usando un helper leggero `HTMLDocument` (o qualsiasi parser tu preferisca).
- Perché **come usare runnable** è importante per un codice riutilizzabile e testabile.

Nessuna libreria esterna è necessaria per l'esempio di base, ma indicheremo dove potresti sostituire Jsoup o un altro parser se ti serve più potenza.

---

## Passo 1: Definire un compito riutilizzabile – **come usare runnable**

La prima cosa da sapere **come usare runnable** è incapsulare il lavoro che vuoi che ogni thread esegua. Un `Runnable` è semplicemente un'interfaccia funzionale con un unico metodo `run()`, il che lo rende perfetto per le espressioni lambda.

```java
// Define the reusable task
Runnable extractTextLength = () -> {
    // Open the HTML file inside a try‑with‑resources block
    try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
        // Get the length of the body text
        int textLength = doc.getBody().getTextContent().length();

        // Print the thread name and the length
        System.out.println(Thread.currentThread().getName() + ": " + textLength);
    } catch (Exception e) {
        e.printStackTrace();
    }
};
```

**Perché è importante:** Tenendo la logica dentro un `Runnable`, puoi passarla a qualsiasi numero di oggetti `Thread`, a un pool di thread o anche a un executor service in seguito. Questo mantiene il tuo codice DRY e testabile.

---

## Passo 2: **Come avviare un thread** – crea il primo worker

Ora che abbiamo un `Runnable`, lanciare un thread è semplice come chiamare il costruttore di `Thread`. La domanda **come avviare un thread** trova risposta in una sola riga:

```java
// Start the first thread
Thread worker1 = new Thread(extractTextLength, "Worker-1");
worker1.start();   // <-- this actually starts the new thread
```

Nota il secondo argomento, `"Worker-1"`. Quel nome apparirà quando più tardi **stamperemo il nome del thread**, rendendo il debug molto meno criptico.

---

## Passo 3: **Avviare più thread** – riutilizza lo stesso Runnable

Vuoi processare diversi file HTML contemporaneamente? Basta creare un altro `Thread` con lo stesso `Runnable`. Questo dimostra **avviare più thread** senza copiare il codice del compito:

```java
// Start a second thread that runs the exact same task
Thread worker2 = new Thread(extractTextLength, "Worker-2");
worker2.start();
```

Sia `Worker-1` che `Worker-2` eseguiranno il blocco definito in `extractTextLength` in parallelo. Poiché il compito è senza stato (legge solo un file), non ci sono condizioni di gara di cui preoccuparsi.

---

## Passo 4: **Stampare il nome del thread** durante l'analisi dell'HTML

All'interno del `Runnable` abbiamo già chiamato `Thread.currentThread().getName()`. È il modo canonico per **stampare il nome del thread**. L'output sarà simile a questo (supponendo che il corpo HTML contenga 1 234 caratteri):

```
Worker-1: 1234
Worker-2: 1234
```

Se esegui il programma su un file più grande, ogni riga mostrerà la stessa lunghezza perché entrambi i thread leggono lo stesso file. Cambia il percorso o passa il nome del file come parametro per vedere risultati diversi.

---

## Passo 5: Esempio completo, eseguibile – dall'import all'esecuzione

Di seguito trovi il programma completo, **autonomo**, che puoi inserire in un file chiamato `HtmlThreadDemo.java`. Include un piccolo stub `HTMLDocument` così il codice compila anche se non hai a disposizione un parser reale. Sostituisci lo stub con Jsoup o qualsiasi libreria tu preferisca per l'uso in produzione.

```java
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Minimal HTMLDocument helper.
 * In a real project you would use Jsoup or another robust parser.
 */
class HTMLDocument implements AutoCloseable {
    private final String content;

    private HTMLDocument(String html) {
        this.content = html;
    }

    public static HTMLDocument load(String path) throws IOException {
        String html = new String(Files.readAllBytes(Paths.get(path)));
        return new HTMLDocument(html);
    }

    public Body getBody() {
        // Very naive extraction of <body>...</body>
        int start = content.indexOf("<body");
        if (start == -1) return new Body("");
        start = content.indexOf('>', start) + 1;
        int end = content.indexOf("</body>", start);
        if (end == -1) end = content.length();
        return new Body(content.substring(start, end));
    }

    @Override
    public void close() {
        // No resources to free in this stub
    }

    /** Simple wrapper for body text */
    static class Body {
        private final String text;
        Body(String text) { this.text = text; }
        public String getTextContent() { return text; }
    }
}

public class HtmlThreadDemo {

    public static void main(String[] args) {
        // Step 1: Define a reusable task (how to use runnable)
        Runnable extractTextLength = () -> {
            try (HTMLDocument doc = HTMLDocument.load("YOUR_DIRECTORY/page.html")) {
                int textLength = doc.getBody().getTextContent().length();
                // Step 4: Print thread name and length
                System.out.println(Thread.currentThread().getName() + ": " + textLength);
            } catch (Exception e) {
                e.printStackTrace();
            }
        };

        // Step 2 & 3: How to start thread and start multiple threads
        new Thread(extractTextLength, "Worker-1").start();
        new Thread(extractTextLength, "Worker-2").start();
    }
}
```

### Output atteso

Supponendo che `page.html` contenga 2 567 caratteri all'interno del tag `<body>`, vedrai qualcosa di simile:

```
Worker-1: 2567
Worker-2: 2567
```

Se il file non può essere letto, verrà stampata la stack trace — grazie al blocco `catch`.

---

## Problemi comuni & Pro Tips

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| **File non trovato** | Il percorso `"YOUR_DIRECTORY/page.html"` è relativo al punto da cui avvii la JVM. | Usa un percorso assoluto o `Paths.get("").toAbsolutePath()` per il debug. |
| **Condizioni di gara** | Se il `Runnable` muta uno stato condiviso, i thread possono scontrarsi. | Mantieni il compito senza stato, oppure sincronizza l'accesso agli oggetti condivisi. |
| **Troppi thread** | Creare decine di `Thread` può esaurire le risorse del sistema operativo. | Passa a un `ExecutorService` con un pool limitato dopo aver appreso le basi. |
| **Parsing HTML errato** | Lo stub `HTMLDocument` è semplificato; pagine complesse falliscono. | Sostituiscilo con Jsoup: `Document doc = Jsoup.parse(new File(path), "UTF‑8");` |

---

## Estendere l'esempio

Ora che sai **come avviare un thread**, potresti voler:

- **Analizzare file diversi** passando il nome del file al `Runnable` (usando un costruttore o una lambda che cattura una variabile).
- **Raccogliere i risultati** con un `ConcurrentLinkedQueue<Integer>` invece di limitarti a stampare.
- **Utilizzare un pool di thread** (`Executors.newFixedThreadPool(4)`) per una scalabilità migliore.
- **Sostituire il parser** con Jsoup, HtmlUnit, o qualsiasi libreria adatta al tuo progetto.

Tutti questi passaggi si basano sull'idea centrale trattata: definire un compito riutilizzabile, assegnarlo a uno o più thread e osservare quale thread sta eseguendo il lavoro tramite **stampare il nome del thread**.

---

## Conclusione

Abbiamo coperto **come avviare un thread** in Java, dimostrato **come usare runnable** per lavoro riutilizzabile, mostrato come **avviare più thread**, e illustrato un modo semplice per **analizzare HTML con Java** mentre **stampi il nome del thread** per ogni worker. Lo snippet di codice completo sopra è pronto per l'esecuzione, e i concetti si estendono a applicazioni più complesse e di livello produzione.

Sentiti libero di sperimentare: cambia il percorso del file, aumenta il numero di worker, o collega un parser HTML reale. I fondamenti rimangono gli stessi, e ora hai una solida base per qualsiasi progetto Java multithread.

Hai domande su thread safety, executor service o librerie di parsing HTML? Lascia un commento qui sotto, e buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Fixed thread pool java – Parallel HTML Cleaning with ExecutorService](/html/english/java/editing-html-documents/fixed-thread-pool-java-parallel-html-cleaning-with-executors/)
- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}