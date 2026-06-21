---
category: general
date: 2026-04-03
description: Scopri come utilizzare il sandbox in Aspose.HTML Java per impostare l'user
  agent, definire le dimensioni e ottenere immediatamente la dimensione della viewport.
  Codice completo, spiegazioni e consigli inclusi.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: it
og_description: Scopri come utilizzare il sandbox in Aspose.HTML Java per impostare
  l'user agent, definire le dimensioni e ottenere immediatamente la dimensione della
  viewport. Guida completa con codice e best practice.
og_title: Come usare Sandbox – Imposta User Agent e ottieni la dimensione della viewport
tags:
- AsposeHTML
- Java
- Sandbox
title: Come usare Sandbox – Impostare l'User Agent e ottenere la dimensione della
  viewport
url: /it/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare Sandbox – Impostare User Agent e Ottenere la Dimensione del Viewport

Ti sei mai chiesto **come usare sandbox** quando si rende HTML con Aspose.HTML for Java? Forse ti sei imbattuto in un ostacolo cercando di simulare una dimensione di schermo specifica o hai bisogno di falsificare una stringa user‑agent affinché la pagina si comporti come se fosse visitata da un browser mobile.  

La buona notizia è che l’API sandbox ti permette di fare esattamente questo, e puoi anche recuperare la dimensione del viewport calcolata dopo il caricamento della pagina. In questo tutorial vedremo come creare una sandbox, impostare la dimensione, impostare un user agent personalizzato, caricare una pagina remota e infine leggere le dimensioni del viewport. Alla fine saprai **come impostare la dimensione**, **come ottenere il viewport** e perché questi passaggi sono importanti per un rendering headless affidabile.

> **Quick win:** avrai una classe Java eseguibile che stampa qualcosa come `Viewport: 1280×800` in pochi secondi.

---

## Cosa ti serve

- **Aspose.HTML for Java** versione 24.6 o successiva (l’API che utilizziamo è stata introdotta in 24.5).  
- Un kit di sviluppo Java 17+ (qualsiasi JDK recente va bene).  
- Un IDE o un semplice editor di testo—non sono richiesti plugin speciali.  
- Accesso a Internet se vuoi caricare un URL esterno come `https://example.com`.

Questo è tutto. Non è obbligatorio usare Maven/Gradle; puoi semplicemente aggiungere i JAR al classpath manualmente se preferisci.  

---

## Come usare Sandbox – Panoramica

La sandbox isola il motore di rendering dal sistema operativo host, consentendoti di definire uno schermo virtuale (larghezza, altezza, DPI) e una stringa **user agent** personalizzata. Pensala come una piccola finestra del browser che vive interamente in memoria. Quando successivamente chiedi al `HTMLDocument` la sua vista predefinita, il motore restituisce la **dimensione del viewport** calcolata in base alle impostazioni della sandbox.  

Di seguito il flusso ad alto livello:

1. **Create** un `DocumentSandbox` e configura larghezza, altezza, DPI e user‑agent.  
2. **Load** un `HTMLDocument` all’interno di quella sandbox.  
3. **Query** la vista predefinita del documento per ottenere la dimensione del viewport.  

Passiamo ora a ciascun passaggio.

---

## Passo 1: Creare una Sandbox e Impostare la Dimensione

Per prima cosa avviamo una sandbox e le diciamo quanto grande deve essere lo schermo virtuale. Qui rispondi alla domanda **come impostare la dimensione** per un rendering headless.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Pro tip:** se stai testando un layout responsive, prova una larghezza stretta come `360` per emulare un telefono, o una larga come `1920` per un desktop. La sandbox rispetta il DPI impostato, quindi uno schermo ad alta densità (es. 144 DPI) influenzerà le media‑query che usano `device-pixel-ratio`.

---

## Passo 2: Impostare User Agent per la Sandbox

Perché preoccuparsi di un **user agent** personalizzato? Alcuni siti forniscono markup o script diversi a seconda del browser segnalato. Chiamando `setUserAgent` puoi ingannare la pagina facendole credere di essere visitata da Chrome, Firefox o da un dispositivo mobile.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Ora la pagina penserà di essere visualizzata su un iPhone. Se devi **impostare user agent** al valore predefinito, riutilizza semplicemente la stringa “AsposeHTML/24.6 …” mostrata in precedenza.

---

## Passo 3: Caricare un Documento HTML nella Sandbox

Con la sandbox pronta, possiamo caricare qualsiasi URL o file HTML locale. Il costruttore `HTMLDocument` accetta la sandbox come secondo argomento, collegando i due elementi.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

Il blocco `try‑with‑resources` garantisce che il documento venga eliminato correttamente, liberando le risorse native che Aspose.HTML alloca in background.

---

## Passo 4: Ottenere la Dimensione del Viewport dal Documento

Ecco il momento tanto atteso: recuperare la **dimensione del viewport** calcolata dal motore di rendering. Questo risponde a **come ottenere il viewport** dopo che la pagina è stata impaginata.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Quando esegui il programma, dovresti vedere qualcosa del genere:

```
Viewport: 1280×800
```

Se hai modificato le dimensioni della sandbox nel Passo 1, i numeri stampati rifletteranno i nuovi valori—perfetto per test automatizzati che verificano i breakpoint responsive.

---

## Esempio Completo

Di seguito trovi la classe completa, pronta per l’esecuzione, che mette insieme tutti i pezzi. Copiala in un file chiamato `SandboxExample.java`, aggiungi i JAR di Aspose.HTML al classpath ed esegui `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Output previsto** (supponendo le impostazioni della sandbox sopra):

```
Viewport: 1280×800
```

Se imposti una larghezza/altezza diversa nella sandbox, l’output cambierà di conseguenza—esattamente ciò di cui hai bisogno quando testi design responsive.

---

## Casi Limite e Domande Frequenti

### E se la pagina usa `window.innerWidth` invece delle media query CSS?

La dimensione dello schermo virtuale della sandbox influenza sia il layout CSS sia il valore di `window.innerWidth/innerHeight` in JavaScript. Quindi **come ottenere il viewport** tramite JavaScript restituirà gli stessi numeri che vedi nella console Java.

### Posso eseguire più sandbox in parallelo?

Sì. Ogni istanza di `DocumentSandbox` è indipendente, quindi puoi creare un pool di thread, assegnare a ciascun thread la propria sandbox con dimensioni diverse e rendere decine di pagine contemporaneamente. Ricorda solo di mantenere i JAR thread‑safe (lo sono).

### L’impostazione DPI influisce sul ridimensionamento delle immagini?

Assolutamente. Un DPI più alto fa sì che un pixel CSS corrisponda a più pixel del dispositivo, il che può far apparire le immagini ad alta risoluzione più nitide. Se stai testando risorse in stile retina, prova `sandbox.setDeviceDpi(144)`.

### Come gestire certificati HTTPS auto‑firmati

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}