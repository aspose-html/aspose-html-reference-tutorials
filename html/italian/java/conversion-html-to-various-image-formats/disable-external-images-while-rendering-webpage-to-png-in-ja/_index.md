---
category: general
date: 2026-05-31
description: Disabilita le immagini esterne quando rendi una pagina web in PNG in
  Java usando Aspose HTML. Impara a caricare la pagina web in sandbox in modo sicuro
  e a salvare il documento HTML come PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: it
og_description: Disabilita le immagini esterne durante il rendering di una pagina
  web in PNG in Java. Questa guida passo‑passo mostra come caricare una pagina web
  in sandbox e salvare il documento HTML come PNG.
og_title: Disabilita le immagini esterne durante il rendering della pagina web in
  PNG in Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Disabilita le immagini esterne durante il rendering della pagina web in PNG
  con Java
url: /it/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Disabilitare le Immagini Esterne durante il Rendering di una Pagina Web in PNG con Java

Ti è mai capitato di **disabilitare le immagini esterne** quando rendi una pagina web in PNG con Java? Forse stai creando un servizio di miniature che deve rimanere isolato da Internet pubblico, oppure vuoi semplicemente garantire che nessuna immagine di terze parti fuoriesca durante la conversione. In ogni caso, sei nel posto giusto.

In questo tutorial ti guideremo passo passo nel caricamento di una pagina web in una sandbox, nella disattivazione del recupero delle immagini esterne e, infine, nel salvataggio del documento HTML come file PNG—tutto con Aspose.HTML per Java. Alla fine avrai un esempio pronto all'uso, oltre a una serie di consigli pratici per evitare le solite insidie.

## Cosa Imparerai

- **Come rendere HTML in immagine Java** usando `Converter` di Aspose.HTML.
- I passaggi esatti per **caricare una pagina web in sandbox** con un viewport e DPI personalizzati.
- La configurazione necessaria per **disabilitare le immagini esterne** mantenendo il rendering della pagina.
- Come **salvare il documento HTML come PNG** (o qualsiasi altro formato supportato) su disco.
- Gestione dei casi limite, suggerimenti sulle prestazioni e consigli per la risoluzione dei problemi.

### Prerequisiti

- Java 8 o versioni successive installate (il codice funziona anche con JDK 11+).
- Maven o Gradle per scaricare la libreria Aspose.HTML per Java.
- Familiarità di base con la sintassi Java e la gestione delle eccezioni.
- Una connessione Internet per il caricamento iniziale della pagina (a meno che non serva l'HTML localmente).

> **Suggerimento professionale:** Se lavori dietro un proxy aziendale, imposta le proprietà JVM `http.proxyHost` e `http.proxyPort` prima di eseguire l'esempio.

---

## Step 1: Configura il tuo progetto e aggiungi Aspose.HTML

Prima di tutto—aggiungi la dipendenza Aspose.HTML. Se usi Maven, inserisci questo nel tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Per Gradle, l'equivalente è:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Una volta che la libreria è nel classpath, sei pronto per iniziare a programmare.

---

## Step 2: **Disabilitare le Immagini Esterne** con un Ambiente Sandbox

Il cuore della soluzione risiede in `DocumentSandbox`. Passando `false` per il flag *allowExternalImages*, istruiamo Aspose.HTML a ignorare tutti i tag `<img>` che puntano a URL al di fuori della sandbox. Questo è il meccanismo esatto che **disabilita le immagini esterne**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Perché è importante:** Senza la sandbox, il renderer tenterebbe di scaricare ogni immagine referenziata dalla pagina, il che può essere lento, inaffidabile o addirittura un rischio di sicurezza. Impostare il flag su `false` garantisce un passaggio di rendering pulito e autonomo.

---

## Step 3: **Caricare la Pagina Web in Sandbox**  

Ora puntiamo Aspose.HTML all'URL che vogliamo catturare. Il costruttore `HTMLDocument` accetta l'istanza della sandbox, applicando automaticamente le restrizioni appena definite.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Se la pagina dipende molto da script esterni per il layout, potresti notare contenuti mancanti perché abbiamo anche disabilitato gli script. In tal caso, imposta il flag `allowExternalScripts` su `true` mantenendo `allowExternalImages` impostato su `false`.

---

## Step 4: **Renderizzare la Pagina Web in PNG**  

Con il documento caricato, convertirlo in immagine è una singola riga usando `Converter.convert`. L'oggetto `ImageSaveOptions` ti permette di scegliere il formato di output; qui scegliamo PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Il file risultante, `sandboxed.png`, contiene uno snapshot della pagina **senza alcuna immagine esterna**—rimangono solo gli SVG inline o le grafiche codificate in base64, se presenti.

---

## Step 5: Verifica l'Uscita e Risolvi i Problemi Comuni

Dopo aver eseguito il programma, apri `sandboxed.png` con qualsiasi visualizzatore di immagini. Dovresti vedere il layout della pagina, il testo e lo stile CSS, ma tutti gli elementi `<img src="http://…">` saranno vuoti (spesso renderizzati come un rettangolo bianco o omessi del tutto).

### Problemi tipici e come risolverli

| Sintomo | Causa probabile | Soluzione |
|---|---|---|
| Pagina vuota | L'URL di destinazione ha bloccato la richiesta (es. Cloudflare) | Aggiungi gli header appropriati allo user‑agent della sandbox o usa un proxy. |
| Font mancanti | I file dei font sono ospitati esternamente | Installa i font localmente o incorporali come `@font-face` con data URI. |
| Spostamento del layout | Il CSS fa riferimento a fogli di stile esterni che sono stati bloccati | Imposta `allowExternalScripts` su `true` *solo* per il caricamento del CSS, poi riesegui. |
| `java.lang.OutOfMemoryError` | Rendering di una pagina molto grande ad alto DPI | Riduci la dimensione del viewport o il DPI, oppure aumenta l'heap JVM (`-Xmx2g`). |

---

## Step 6: Estendere l'Esempio – Salvataggio in Altri Formati

Lo stesso codice funziona per JPEG, BMP o anche PDF. Basta cambiare l'enum `SaveFormat`:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Se ti serve un PDF, sostituisci `ImageSaveOptions` con `PdfSaveOptions` e adegua l'estensione del file di conseguenza.

---

## Esempio Completo (Pronto per il Copia‑Incolla)

Di seguito trovi il **programma completo e eseguibile**. Crea una nuova classe Java, incolla il codice, assicurati che la cartella `output` esista e avvialo.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Output previsto** (console):

```
PNG image saved to: output/sandboxed.png
```

Apri `sandboxed.png` – vedrai la pagina renderizzata **senza alcuna immagine esterna**.

---

## Domande Frequenti

**D: Posso ancora visualizzare le immagini incluse nell'HTML?**  
R: Sì. Gli URI `data:` inline o le immagini codificate in base64 sono trattate come parte del documento e appariranno nel PNG.

**D: E se devo mantenere alcune immagini esterne ma bloccarne altre?**  
R: La sandbox funziona come un interruttore tutto‑o‑niente. Per un controllo più fine, scarica le immagini consentite tu stesso, incorporale come URI `data:` e poi esegui il rendering.

**D: Questo approccio funziona su server headless?**  
R: Assolutamente. Aspose.HTML è una libreria pure‑Java; non richiede un server display né un motore browser.

**D: In che modo questo differisce dall'uso di Selenium o Puppeteer?**  
R: Selenium controlla un vero browser, che è più pesante e più difficile da sandboxare. Aspose.HTML renderizza HTML direttamente in memoria, offrendo prestazioni deterministiche e controlli di sicurezza più semplici come **disabilitare le immagini esterne**.

---

## Conclusione

Ora disponi di una ricetta solida, end‑to‑end, per **disabilitare le immagini esterne durante il rendering di una pagina web in PNG con Java**. Sfruttando `DocumentSandbox`, ottieni un controllo rigoroso sulle risorse esterne consentite, garantendo sia sicurezza sia riproducibilità. Da qui puoi sperimentare con diverse dimensioni del viewport, impostazioni DPI o formati di output—ogni variazione apre nuove possibilità per generare miniature, anteprime o snapshot di archivio.

Pronto per la prossima sfida? Prova a renderizzare un batch di URL in parallelo, o integra questa logica in un microservizio Spring Boot che restituisce PNG su richiesta. Il cielo è il limite quando combini la flessibilità di Aspose.HTML con gli strumenti di concorrenza di Java.

Buon coding, e non dimenticare di condividere le tue storie di successo nei commenti!

## Cosa Dovresti Imparare Dopo?

- [Come usare Aspose per renderizzare HTML in PNG – Guida passo‑passo](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [Come renderizzare HTML in PNG con Aspose – Guida completa](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [Come modificare CSS - Modifica avanzata di CSS esterno con Aspose.HTML per Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}