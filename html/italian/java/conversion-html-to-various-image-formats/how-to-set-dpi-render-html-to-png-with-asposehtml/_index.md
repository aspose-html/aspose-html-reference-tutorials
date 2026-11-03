---
category: general
date: 2026-01-14
description: come impostare i dpi durante la conversione di un URL in PNG. Impara
  a renderizzare HTML in PNG, impostare le dimensioni del viewport e salvare HTML
  come PNG usando Aspose.HTML in Java.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: it
og_description: come impostare i dpi durante la conversione di un URL in PNG. Guida
  passo‑passo per renderizzare HTML in PNG, controllare le dimensioni del viewport
  e salvare HTML come PNG usando Aspose.HTML.
og_title: come impostare i DPI – Render HTML in PNG con AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: Come impostare i DPI – Render HTML in PNG con AsposeHTML
url: /it/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come impostare dpi – Render HTML to PNG con AsposeHTML

Ti sei mai chiesto **come impostare dpi** per un'immagine simile a uno screenshot generata da una pagina web? Forse ti serve un PNG a 300 DPI per la stampa, o una miniatura a bassa risoluzione per un'app mobile. In entrambi i casi, il trucco è dire al motore di rendering quale DPI logico desideri, quindi lasciarlo fare il lavoro pesante.  

In questo tutorial prenderemo un URL live, lo renderizzeremo in un file PNG, **imposteremo la dimensione del viewport**, regoleremo il DPI e infine **salveremo l'HTML come PNG** — tutto con Aspose.HTML per Java. Nessun browser esterno, nessuno strumento da riga di comando ingombrante — solo codice Java pulito che puoi inserire in qualsiasi progetto Maven o Gradle.

> **Consiglio:** Se ti serve solo una miniatura veloce, puoi mantenere il DPI a 96 DPI (il valore predefinito per la maggior parte degli schermi). Per risorse pronte per la stampa, aumentalo a 300 DPI o più.

![esempio di come impostare dpi](https://example.com/images/how-to-set-dpi.png "esempio di come impostare dpi")

## Cosa ti serve

- **Java 17** (o qualsiasi JDK recente).  
- **Aspose.HTML for Java** 24.10 o più recente. Puoi scaricarlo da Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Una connessione internet per recuperare la pagina di destinazione (l'esempio utilizza `https://example.com/sample.html`).  
- Permesso di scrittura sulla cartella di destinazione.

Tutto qui — niente Selenium, niente Chrome headless. Aspose.HTML esegue il rendering in‑processo, il che significa che rimani all'interno della JVM ed eviti l'overhead di avviare un browser.

## Passo 1 – Carica il documento HTML da un URL

Per prima cosa creiamo un'istanza di `HTMLDocument` che punta alla pagina che vogliamo catturare. Il costruttore scarica automaticamente l'HTML, lo analizza e prepara il DOM.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Perché è importante:* Caricando il documento direttamente, eviti la necessità di un client HTTP separato. Aspose.HTML rispetta i redirect, i cookie e anche l'autenticazione di base se inserisci le credenziali nell'URL.

## Passo 2 – Crea un Sandbox con DPI e Viewport desiderati

Un **sandbox** è il modo di Aspose.HTML di imitare un ambiente browser. Qui gli diciamo di fingere di essere uno schermo 1280 × 720 e, soprattutto, impostiamo il **DPI del dispositivo**. Cambiare il DPI modifica la densità di pixel dell'immagine renderizzata senza alterare le dimensioni logiche.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Perché potresti modificare questi valori:*
- **Viewport size** controlla il comportamento delle media query CSS (`@media (max-width: …)`).
- **Device DPI** influenza le dimensioni fisiche dell'immagine quando stampata. Un'immagine a 96 DPI appare bene sugli schermi; un'immagine a 300 DPI mantiene nitidezza sulla carta.

Se ti serve una miniatura quadrata, basta cambiare `setViewportSize(500, 500)` e mantenere il DPI basso.

## Passo 3 – Scegli PNG come formato di output

Aspose.HTML supporta diversi formati raster (PNG, JPEG, BMP, GIF). PNG è loss‑less, il che lo rende perfetto per gli screenshot in cui vuoi preservare ogni pixel.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Puoi anche regolare il livello di compressione (`pngOptionsCompressionLevel(9)`) se ti preoccupi delle dimensioni del file.

## Passo 4 – Renderizza e salva l'immagine

Ora diciamo al documento di **salvare** se stesso come immagine. Il metodo `save` accetta un percorso file e le opzioni precedentemente configurate.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Quando il programma termina, troverai un file PNG in `YOUR_DIRECTORY/sandboxed.png`. Aprilo — se hai impostato il DPI a 300, i metadati dell'immagine lo rifletteranno, anche se le dimensioni in pixel rimangono 1280 × 720.

## Passo 5 – Verifica il DPI (Opzionale ma utile)

Se vuoi ricontrollare che il DPI sia stato davvero applicato, puoi leggere i metadati PNG con una libreria leggera come **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Dovresti vedere `300` (o qualunque valore tu abbia impostato) stampato sulla console. Questo pass non è necessario per il rendering, ma è un rapido controllo di coerenza, soprattutto quando generi risorse per un flusso di lavoro di stampa.

## Domande comuni & casi limite

### “E se la pagina usa JavaScript per caricare contenuti?”

Aspose.HTML esegue un **sottoinsieme limitato** di JavaScript. Per la maggior parte dei siti statici funziona subito. Se la pagina dipende molto da framework lato client (React, Angular, Vue), potresti dover pre‑renderizzare la pagina o usare un browser headless. Tuttavia, l'impostazione del DPI funziona allo stesso modo una volta che il DOM è pronto.

### “Posso renderizzare un PDF invece di PNG?”

Assolutamente. Sostituisci `ImageSaveOptions` con `PdfSaveOptions` e cambia l'estensione di output in `.pdf`. L'impostazione del DPI influisce comunque sull'aspetto rasterizzato di eventuali immagini incorporate.

### “E per gli screenshot ad alta risoluzione per display retina?”

Basta raddoppiare le dimensioni del viewport mantenendo il DPI a 96 DPI, oppure mantenere il viewport e aumentare il DPI a 192. Il PNG risultante conterrà il doppio dei pixel, offrendoti quella nitidezza tipica dei display retina.

### “Devo pulire le risorse?”

`HTMLDocument` implementa `AutoCloseable`. In un'app di produzione, avvolgilo in un blocco try‑with‑resources:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi il programma completo pronto per l'esecuzione. Sostituisci `YOUR_DIRECTORY` con una cartella reale sul tuo computer.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Esegui la classe e otterrai un PNG che rispetta l'impostazione **come impostare dpi** che hai specificato.

## Conclusione

Abbiamo illustrato **come impostare dpi** quando **renderizzi HTML in PNG**, coperto il passaggio **imposta la dimensione del viewport** e mostrato come **salvare l'HTML come PNG** usando Aspose.HTML per Java. I punti chiave sono:

- Usa un **sandbox** per controllare DPI e viewport.  
- Scegli le giuste **ImageSaveOptions** per un output lossless.  
- Verifica i metadati DPI se devi garantire la qualità di stampa.  

Da qui puoi sperimentare con diversi valori DPI, viewport più grandi, o anche elaborare in batch un elenco di URL. Vuoi convertire un intero sito web in miniature PNG? Basta iterare su un array di URL e riutilizzare la stessa configurazione sandbox.

Buon rendering, e che i tuoi screenshot siano sempre pixel‑perfect!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}