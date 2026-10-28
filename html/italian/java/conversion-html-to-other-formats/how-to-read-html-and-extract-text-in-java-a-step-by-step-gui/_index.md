---
category: general
date: 2026-10-28
description: Come leggere HTML in Java ed estrarre il testo dai file HTML. Impara
  a convertire HTML in testo con Jsoup, coprendo la lettura di HTML da file e le tecniche
  Java per convertire HTML in testo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: it
lastmod: 2026-10-28
og_description: Come leggere HTML in Java ed estrarre il testo dai file HTML. Questo
  tutorial mostra una soluzione completa per convertire l'HTML in testo usando Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Come leggere HTML ed estrarre testo in Java – guida rapida
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: Come leggere l'HTML ed estrarre il testo in Java – una guida passo passo
url: /it/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come leggere HTML ed estrarre testo in Java – una guida passo‑passo

Se hai bisogno di **how to read html** da un file locale, questa guida fornisce una soluzione completa. Imparerai a caricare un documento HTML, estrarre il testo semplice e, facoltativamente, convertire l'HTML in testo con un controllo fine. Alla fine del tutorial potrai eseguire il codice di esempio e vedere il testo estratto stampato sulla console.

Leggere file HTML è un compito comune quando si elaborano dati web‑scraped, si generano report o si pulisce contenuto generato dagli utenti. I passaggi seguenti coprono tutto ciò di cui hai bisogno, dall'aggiunta della libreria necessaria alla gestione di casi particolari come markup malformato o problemi di codifica dei caratteri.

## Cosa ti servirà

- Java 17 o versioni successive (il codice si compila anche con versioni precedenti)
- Maven o Gradle per la gestione delle dipendenze, oppure il JAR di Jsoup aggiunto manualmente
- Un file HTML chiamato `input.html` posizionato nella directory `src/main/resources` del progetto (puoi cambiare il percorso in seguito)

## Configura la libreria Jsoup

Jsoup è una libreria leggera e ben documentata che analizza l'HTML in una struttura simile al DOM. Gestisce HTML danneggiato in modo elegante, il che la rende ideale per compiti di **extract text from html**.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Se preferisci un download manuale, posiziona il JAR nel tuo classpath e importa `org.jsoup.*` nel tuo file sorgente.

## Carica HTML da un file

Il primo passo programmatico è leggere il file in un oggetto `Document`. Jsoup offre un metodo statico `parse` che accetta un `File` e il nome di un charset.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Why this matters:** `Jsoup.parse(File, String)` legge i byte grezzi, li decodifica secondo il charset fornito e costruisce un DOM pulito. Questo approccio è più sicuro rispetto a leggere il file in una stringa da soli perché Jsoup normalizza le interruzioni di riga e corregge automaticamente gli errori di markup più comuni.

## Estrai testo semplice dall'HTML

Una volta ottenuto un `Document`, recuperare il testo visibile è una singola chiamata di metodo. Il metodo `text()` concatena il contenuto testuale di tutti gli elementi scartando tag, script e stili.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

La chiamata `body()` limita l'estrazione all'elemento `<body>`, che è il target tipico quando **read html from file** per l'analisi del contenuto. La stringa risultante contiene spazi bianchi compressi in spazi singoli, simulando come un browser renderebbe il testo.

### Output previsto

Supponendo che `input.html` contenga:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

L'esecuzione del programma stampa:

```
Extracted text:
Hello World This is a demo page.
```

## Converti HTML in testo con opzioni aggiuntive

A volte serve più controllo rispetto a quanto fornisce `text()`—ad esempio, preservare le interruzioni di riga, mantenere la numerazione delle liste o ignorare certi tag. `NodeTraversor` di Jsoup combinato con un `NodeVisitor` personalizzato ti offre questa flessibilità.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Sostituisci la semplice chiamata `doc.body().text()` con:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Why this works:** Il visitatore attraversa il DOM in profondità, aggiungendo una nuova riga prima di ogni elemento di livello blocco (es. `<p>`, `<div>`, `<h1>`). Questo mantiene la separazione dei paragrafi, utile quando **convert html to text** per la leggibilità o per pipeline NLP successive.

## Problemi comuni e migliori pratiche

| Problema | Perché si verifica | Correzione consigliata |
|----------|--------------------|------------------------|
| Charset errato | I file salvati in ISO‑8859‑1 ma analizzati come UTF‑8 producono caratteri illeggibili. | Rileva il charset dal meta tag del file (`<meta charset="...">`) o passa il nome corretto a `Jsoup.parse`. |
| File di grandi dimensioni | Caricare un file HTML molto grande in memoria può causare `OutOfMemoryError`. | Esegui lo streaming del file con `Jsoup.parse(File, String, String baseUri)` e processa i nodi in modo incrementale, oppure aumenta la dimensione dell'heap JVM. |
| Testo indesiderato di script/style | `text()` rimuove il contenuto di script e style, ma i visitatori personalizzati potrebbero includerlo involontariamente. | Ignora i nodi il cui nome del tag è `script` o `style` all'interno del metodo `head` del visitatore. |
| Mantenere gli spazi bianchi | Il collasso degli spazi può perdere la formattazione necessaria per la conversione in markdown. | Usa `Element.wholeText()` per i nodi di testo grezzi, poi elabora manualmente gli spazi bianchi. |

Affrontare queste problematiche garantisce che la tua soluzione **html to text java** funzioni in modo affidabile su input diversi.

## Esempio completo eseguibile

Di seguito trovi un programma autonomo che dimostra l'intero flusso di lavoro—from dependency setup to output verification. Copia il codice in un file chiamato `HtmlToTextDemo.java`, posiziona un file `input.html` accanto e esegui `javac && java` come mostrato.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Esecuzione del programma

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

La console mostra sia l'estrazione semplice che il dettagliato

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come usare XPath in Java – Leggere HTML ed estrarre testo](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [Come analizzare HTML in Java – Estrarre testo da articoli HTML](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Estrarre testo da HTML con Java – Guida completa passo‑passo](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}