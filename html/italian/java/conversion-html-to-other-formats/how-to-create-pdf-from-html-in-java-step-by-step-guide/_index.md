---
category: general
date: 2026-10-02
description: Crea PDF da HTML in Java con una singola chiamata. Questo tutorial mostra
  come convertire HTML in PDF, configurare le opzioni e gestire i problemi comuni.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- how to convert html to pdf
- html to pdf conversion java
- convert html file to pdf
language: it
lastmod: 2026-10-02
og_description: Crea PDF da HTML in Java usando HtmlConverter. Segui questa guida
  completa per convertire HTML in PDF, impostare le opzioni e evitare insidie.
og_image_alt: Diagram showing create pdf from html process in Java
og_title: Crea PDF da HTML in Java – conversione rapida e affidabile
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Create pdf from html in Java with a single call. This tutorial shows
    how to convert html to pdf, configure options, and handle common issues.
  headline: How to create pdf from html in Java – step‑by‑step guide
  type: TechArticle
- description: Create pdf from html in Java with a single call. This tutorial shows
    how to convert html to pdf, configure options, and handle common issues.
  name: How to create pdf from html in Java – step‑by‑step guide
  steps:
  - name: Why this approach works
    text: '* **Single responsibility** – the `convertHtmlToPdf` method isolates the
      conversion logic, making the code easy to test. * **Resource safety** – `try‑with‑resources`
      guarantees that the `PDDocument` is closed, preventing file‑handle leaks. *
      **Flexibility** – you can swap `HtmlRenderer` for another '
  - name: 1️⃣ Specify the source HTML file and the target PDF file
    text: '```java private static final String INPUT_PATH = "YOUR_DIRECTORY/input.html";
      private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf"; ``` *Replace
      `YOUR_DIRECTORY` with an absolute or relative path that your Java process can
      read/write.*'
  - name: 2️⃣ Load the HTML content
    text: '```java String html = Files.readString(Path.of(INPUT_PATH)); ``` Reading
      the file as a `String` preserves the original markup and makes it easy to feed
      the converter. The method assumes UTF‑8; if your HTML uses a different charset,
      use `Files.readAllBytes` and decode accordingly.'
  - name: 3️⃣ Convert the HTML document to PDF
    text: '```java byte[] pdfBytes = convertHtmlToPdf(html); ``` `convertHtmlToPdf`
      encapsulates **how to convert html to pdf**. Inside, `HtmlRenderer` parses the
      markup, applies CSS, and draws the result onto a PDF page. This is the heart
      of the **html to pdf conversion java** process.'
  - name: 4️⃣ Write the PDF file
    text: '```java Files.write(Path.of(OUTPUT_PATH), pdfBytes, StandardOpenOption.CREATE,
      StandardOpenOption.TRUNCATE_EXISTING); ``` The `Files.write` call creates the
      output file if it does not exist, or overwrites it otherwise. The method throws
      `IOException` if the directory is missing or the process lacks '
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: Come creare PDF da HTML in Java – guida passo passo
url: /it/java/conversion-html-to-other-formats/how-to-create-pdf-from-html-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare PDF da HTML in Java – guida passo‑passo

Se hai bisogno di **creare pdf da html** in un'applicazione Java, questa guida ti mostra una soluzione completa, pronta all'uso. Vedrai come **convertire html in pdf** con una singola chiamata di metodo, configurare la conversione e gestire i casi limite tipici.

Copriamo tutto ciò che devi sapere: le dipendenze necessarie, un file sorgente completo e consigli per la risoluzione dei problemi. Alla fine sarai in grado di **convertire file html in pdf** in modo affidabile in qualsiasi progetto Java.

## Prerequisiti

* JDK 17 o versioni successive installato  
* Maven 3.8+ (o Gradle) per gestire le dipendenze  
* Familiarità di base con Java I/O  

L'esempio utilizza la classe open‑source **HtmlConverter** della libreria *pdfbox‑layout*, che avvolge Apache PDFBox per il rendering HTML. Se preferisci un'altra libreria, gli stessi passaggi si applicano—basta adeguare le istruzioni di import.

## Aggiungi la dipendenza necessaria

Aggiungi le seguenti coordinate Maven al tuo `pom.xml`. Questo includerà PDFBox e l'helper HTML‑to‑PDF.

```xml
<dependency>
    <groupId>org.apache.pdfbox</groupId>
    <artifactId>pdfbox</artifactId>
    <version>3.0.2</version>
</dependency>
<dependency>
    <groupId>com.github.jhonnymertz</groupId>
    <artifactId>pdfbox-layout</artifactId>
    <version>1.0.0</version>
</dependency>
```

Se usi Gradle, l'equivalente è:

```gradle
implementation "org.apache.pdfbox:pdfbox:3.0.2"
implementation "com.github.jhonnymertz:pdfbox-layout:1.0.0"
```

> **Consiglio:** Mantieni le dipendenze aggiornate; le versioni più recenti correggono bug di rendering e aggiungono supporto CSS.

## Creare pdf da html – flusso di lavoro complessivo

La conversione consiste in tre passaggi logici:

1. **Leggi il file HTML sorgente** – assicurati che il percorso sia corretto e che il file sia codificato in UTF‑8.  
2. **Invoca il convertitore** – la libreria analizza l'HTML, applica il CSS e genera un documento PDF.  
3. **Scrivi il PDF su disco** – gestisci le eccezioni I/O e conferma che il file sia stato creato.

Di seguito trovi una classe Java completa e autonoma che implementa questo flusso di lavoro.

```java
package com.example.pdfconverter;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

import org.apache.pdfbox.pdmodel.PDDocument;
import org.apache.pdfbox.pdmodel.PDPage;
import org.apache.pdfbox.pdmodel.PDPageContentStream;
import org.apache.pdfbox.pdmodel.common.PDRectangle;
import org.apache.pdfbox.layout.Document;
import org.apache.pdfbox.layout.element.Paragraph;
import org.apache.pdfbox.layout.renderer.HtmlRenderer;

/**
 * Simple utility that demonstrates how to create pdf from html in Java.
 *
 * The class reads an HTML file, converts it to PDF, and saves the result.
 * It uses Apache PDFBox together with the pdfbox‑layout HtmlRenderer.
 *
 * Adjust INPUT_PATH and OUTPUT_PATH to match your environment.
 */
public class HtmlToPdfConverter {

    // --------------------------------------------------------------------
    // 1️⃣  Define input and output locations
    // --------------------------------------------------------------------
    private static final String INPUT_PATH  = "YOUR_DIRECTORY/input.html";
    private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf";

    public static void main(String[] args) {
        try {
            // --------------------------------------------------------------
            // 2️⃣  Load the HTML content (UTF‑8 is assumed)
            // --------------------------------------------------------------
            String html = Files.readString(Path.of(INPUT_PATH));

            // --------------------------------------------------------------
            // 3️⃣  Perform the conversion
            // --------------------------------------------------------------
            byte[] pdfBytes = convertHtmlToPdf(html);

            // --------------------------------------------------------------
            // 4️⃣  Write the PDF file to disk
            // --------------------------------------------------------------
            Files.write(Path.of(OUTPUT_PATH), pdfBytes,
                    StandardOpenOption.CREATE,
                    StandardOpenOption.TRUNCATE_EXISTING);

            System.out.println("✅ PDF created successfully at " + OUTPUT_PATH);
        } catch (IOException e) {
            System.err.println("❌ Failed to convert HTML to PDF: " + e.getMessage());
            e.printStackTrace();
        }
    }

    /**
     * Core conversion logic.
     *
     * @param html the raw HTML string
     * @return a byte array containing the generated PDF
     * @throws IOException if PDF generation fails
     */
    private static byte[] convertHtmlToPdf(String html) throws IOException {
        // Create a new PDFBox document – this is the container for the output.
        try (PDDocument pdDocument = new PDDocument()) {

            // The HtmlRenderer parses the HTML and draws it onto a PDF page.
            HtmlRenderer renderer = new HtmlRenderer(pdDocument);
            renderer.renderHtml(html);

            // Save the document into a byte array so we can write it later.
            return toByteArray(pdDocument);
        }
    }

    /**
     * Helper that converts a PDDocument into a byte array.
     *
     * @param document the populated PDFBox document
     * @return PDF content as a byte array
     * @throws IOException if writing fails
     */
    private static byte[] toByteArray(PDDocument document) throws IOException {
        try (java.io.ByteArrayOutputStream out = new java.io.ByteArrayOutputStream()) {
            document.save(out);
            return out.toByteArray();
        }
    }
}
```

### Perché questo approccio funziona

* **Responsabilità singola** – il metodo `convertHtmlToPdf` isola la logica di conversione, rendendo il codice facile da testare.  
* **Sicurezza delle risorse** – `try‑with‑resources` garantisce che il `PDDocument` sia chiuso, prevenendo perdite di handle di file.  
* **Flessibilità** – puoi sostituire `HtmlRenderer` con un'altra implementazione (ad es., *OpenHTMLtoPDF*) senza modificare il codice I/O circostante, utile quando ti serve **html to pdf conversion java** che supporta CSS avanzato.

## Spiegazione passo‑passo

### 1️⃣ Specifica il file HTML sorgente e il file PDF di destinazione
```java
private static final String INPUT_PATH  = "YOUR_DIRECTORY/input.html";
private static final String OUTPUT_PATH = "YOUR_DIRECTORY/output.pdf";
```
*Sostituisci `YOUR_DIRECTORY` con un percorso assoluto o relativo che il tuo processo Java possa leggere/scrivere.*

### 2️⃣ Carica il contenuto HTML
```java
String html = Files.readString(Path.of(INPUT_PATH));
```
Leggere il file come `String` preserva il markup originale e facilita l'invio al convertitore. Il metodo assume UTF‑8; se il tuo HTML utilizza un charset diverso, usa `Files.readAllBytes` e decodifica di conseguenza.

### 3️⃣ Converti il documento HTML in PDF
```java
byte[] pdfBytes = convertHtmlToPdf(html);
```
`convertHtmlToPdf` incapsula **come convertire html in pdf**. All'interno, `HtmlRenderer` analizza il markup, applica il CSS e disegna il risultato su una pagina PDF. Questo è il cuore del processo di **html to pdf conversion java**.

### 4️⃣ Scrivi il file PDF
```java
Files.write(Path.of(OUTPUT_PATH), pdfBytes,
        StandardOpenOption.CREATE,
        StandardOpenOption.TRUNCATE_EXISTING);
```
La chiamata `Files.write` crea il file di output se non esiste, altrimenti lo sovrascrive. Il metodo lancia `IOException` se la directory è mancante o il processo non ha i permessi di scrittura.

## Gestione dei problemi comuni

| Problema | Sintomi | Soluzione |
|-------|----------|-----|
| **File di input mancante** | `java.nio.file.NoSuchFileException` | Verifica che `INPUT_PATH` punti a un file esistente. Usa `Files.exists(Path)` per un controllo preliminare. |
| **CSS non supportato** | Il layout appare semplice o rotto | Usa un motore più ricco di funzionalità come *OpenHTMLtoPDF* (aggiungi la sua dipendenza Maven e sostituisci `HtmlRenderer` con `PdfRendererBuilder`). |
| **HTML di grandi dimensioni che causa pressione di memoria** | `OutOfMemoryError` | Esegui lo streaming dell'HTML a blocchi o aumenta l'heap JVM (`-Xmx2g`). |
| **Caratteri Unicode visualizzati come �** | Testo illeggibile nel PDF | Assicurati che il file HTML sia salvato come UTF‑8 e che il font del renderer supporti i glifi richiesti (incorpora un font tramite `renderer.setDefaultFont("Arial Unicode MS")`). |

## Esempio completo funzionante

Salva la classe sopra come `src/main/java/com/example/pdfconverter/HtmlToPdfConverter.java`, regola i percorsi ed esegui:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.pdfconverter.HtmlToPdfConverter"
```

Se tutto è configurato correttamente, vedrai:

```
✅ PDF created successfully at YOUR_DIRECTORY/output.pdf
```

Apri `output.pdf` con qualsiasi visualizzatore PDF—dovresti vedere la pagina HTML renderizzata esattamente come appare in un browser.

## Conclusione

Ora sai come **creare pdf da html** in Java usando un modello conciso e pronto per la produzione. Il tutorial ha coperto:

* Aggiungere le dipendenze Maven necessarie  
* Leggere un file HTML in modo sicuro  
* Eseguire l'operazione **convert html file to pdf** con `HtmlRenderer`  
* Scrivere il PDF risultante e gestire gli errori I/O  

Da qui puoi esplorare argomenti avanzati come **convert html to pdf** con intestazioni/piedi pagina personalizzati, lo streaming di documenti di grandi dimensioni, o il passaggio a un motore di rendering diverso per un supporto CSS più ricco.

**Passaggi successivi**

* Prova **how to convert html to pdf** con *OpenHTMLtoPDF* per una migliore gestione di CSS3.  
* Sperimenta aggiungendo una pagina di copertina o un indice usando direttamente PDFBox.  
* Approfondisci la generazione di PDF lato server per servizi web, dove restituisci i byte del PDF in una risposta HTTP.

Buon coding e goditi il flusso di lavoro fluido per trasformare HTML in PDF di alta qualità!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Create PDF from HTML in Java – Complete Step‑by‑Step Guide](/html/english/java/conversion-html-to-other-formats/create-pdf-from-html-in-java-complete-step-by-step-guide/)
- [html to pdf tutorial: Convert HTML to PDF in Java in One Line](/html/english/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java-in-one-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}