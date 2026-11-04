---
category: general
date: 2026-06-19
description: Scopri come generare PDF da HTML usando un semplice esempio Java. Questo
  tutorial su HTML a PDF ti mostra come convertire un file HTML in PDF con OpenHTMLtoPDF.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: it
og_description: Il tutorial HTML to PDF ti mostra come generare PDF da HTML usando
  Java. Segui i passaggi per convertire rapidamente un file HTML in PDF.
og_title: 'Tutorial HTML a PDF: Guida alla conversione Java'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'Tutorial html to pdf: Converti HTML in PDF con Java'
url: /it/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf tutorial – Trasforma una pagina HTML in un PDF con Java

Ti sei mai chiesto come trasformare una pagina HTML statica in un elegante documento PDF senza uscire dal tuo IDE? Non sei solo. In questo **html to pdf tutorial** percorreremo un esempio Java completo, pronto‑da‑eseguire, che **generate pdf from html** in pochi minuti.

Copriamo tutto ciò di cui hai bisogno—configurazione del progetto, aggiunta della libreria giusta, scrittura del codice di conversione, e anche un rapido suggerimento per convertire una pagina web live in PDF. Alla fine sarai in grado di **convert html file pdf** sulla tua macchina, e comprenderai come **create pdf from html** per qualsiasi progetto futuro.

## What you’ll need

- Java 17 o superiore (il codice funziona con qualsiasi JDK recente)
- Maven o Gradle (mostreremo lo snippet Maven)
- Un piccolo file HTML che vuoi trasformare in PDF (ne creeremo uno al volo)
- Un IDE o un semplice editor di testo—come preferisci

Questo è tutto. Nessun server ingombrante, nessun SDK a pagamento, solo Java puro e una libreria open‑source gratuita.

## Step 1: html to pdf tutorial – Set up a Maven project

Prima di tutto. Crea un nuovo progetto Maven (o aggiungilo a uno esistente). L’unica dipendenza di cui hai realmente bisogno è **OpenHTMLtoPDF**, che si occupa del lavoro pesante di renderizzare HTML e CSS in un PDF.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Se usi Gradle, le stesse dipendenze possono essere aggiunte sotto `implementation` in `build.gradle`.  

Perché questo passaggio è importante: senza la libreria la JVM non ha idea di come tradurre i tag HTML in comandi di disegno PDF. OpenHTMLtoPDF è leggera, attivamente mantenuta, e supporta CSS‑2.1, quindi il tuo styling rimane intatto.

## Step 2: generate pdf from html – Prepare a sample HTML file

Creiamo un piccolo `input.html` accanto al nostro sorgente Java. Questo mantiene l’esempio auto‑contenuto e dimostra il flusso di lavoro **create pdf from html**.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

Puoi sostituire il contenuto con qualsiasi cosa—tabelle, immagini, anche JavaScript (anche se il renderer ignora gli script). La parte importante è che il file risieda nel classpath così il convertitore può individuarlo.

## Step 3: convert html file pdf – Write the conversion utility

Ora il cuore del **html to pdf tutorial**: una piccola classe `HtmlToPdfConverter` che legge l’HTML e scrive un PDF. Il codice qui sotto è un esempio completo e eseguibile; copialo in `src/main/java/com/example/HtmlToPdfConverter.java`.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Why this code works

1. **Resource flexibility** – il metodo controlla prima se il percorso fornito punta a un file reale; in caso contrario, ricade su una risorsa del classpath. Questo significa che potrai **convert webpage to pdf** in seguito passando una stringa URL (basta sostituire la chiamata `withHtmlContent` con `withUri`).

2. **Automatic directory creation** – `Files.createDirectories` garantisce che la cartella `target/` esista, così non otterrai l’errore “No such file or directory”.

3. **Single‑line conversion** – `PdfRendererBuilder` gestisce CSS, font e layout di pagina internamente. Non è necessario gestire manualmente le pagine PDF; la libreria lo fa per te, mantenendo l’esempio breve e focalizzato sul concetto **convert html file pdf**.

## Step 4: create pdf from html – Run the program and verify

Apri un terminale nella radice del progetto ed esegui:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Se tutto è configurato correttamente vedrai:

```
✅ PDF successfully created at target/output.pdf
```

Apri `target/output.pdf` con qualsiasi visualizzatore PDF. Dovresti vedere l’intestazione stilizzata “Monthly Sales Report”, il testo del paragrafo, e gli stessi margini che hai definito nel blocco `<style>` dell’HTML.

> **What if you don’t see the styling?**  
> Assicurati che il CSS sia inline o posizionato nella stessa cartella dell’HTML. OpenHTMLtoPDF risolve gli URL relativi in base al base URI che passi a `withHtmlContent`. Nello snippet sopra abbiamo passato `null`, il che funziona per CSS inline semplice. Per fogli di stile esterni, fornisci il percorso della directory come secondo argomento.

## Step 5: convert webpage to pdf – Handling remote URLs (optional)

A volte è necessario **convert webpage to pdf** direttamente da internet—pensa all’archiviazione di una ricevuta online. La libreria supporta questo tramite `withUri`. Ecco una rapida adattazione:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Chiamala così:



## What Should You Learn Next?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come convertire HTML in PDF con Java – Usando Aspose.HTML per Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convertire HTML in PDF con Java – Configurare l’Ambiente in Aspose.HTML](/html/english/java/configuring-environment/)
- [Convertire HTML in PDF in Java – Guida passo‑a‑passo con impostazioni di dimensione pagina](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}