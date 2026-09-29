---
category: general
date: 2026-09-29
description: Imposta un user agent personalizzato in Aspose.HTML per Java e scopri
  come impostare la dimensione dello schermo virtuale per una resa HTML accurata.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: it
lastmod: 2026-09-29
og_description: Imposta un agente utente personalizzato in Aspose.HTML per Java e
  scopri come impostare la dimensione dello schermo virtuale per una resa HTML accurata.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Imposta un agente utente personalizzato e le dimensioni dello schermo in
  Aspose.HTML per Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Imposta agente utente personalizzato e dimensioni dello schermo in Aspose.HTML
  per Java
url: /it/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta user agent personalizzato e dimensioni dello schermo in Aspose.HTML per Java

Se hai bisogno di **impostare un user agent personalizzato** durante il rendering di HTML con Aspose.HTML per Java, questa guida ti mostra esattamente come farlo. Configurando un sandbox ottieni anche la possibilità di **impostare la dimensione virtuale dello schermo**, garantendo che il layout corrisponda a una viewport reale del browser.

Concluderai questo tutorial con un programma completo e eseguibile che **specifica il user agent**, **imposta la larghezza dello schermo** e **imposta l'altezza dello schermo**. Non sono necessari strumenti esterni—solo Aspose.HTML per Java e un runtime Java 8+.

## Cosa imparerai

* Come creare un `SandboxConfiguration` per isolare il rendering.
* Come **impostare un user agent personalizzato** e perché è importante per le pagine responsive.
* Come **impostare la dimensione virtuale dello schermo** (larghezza e altezza) per un layout accurato.
* Come caricare un file HTML nel sandbox e salvare il risultato elaborato.
* Problemi comuni e consigli di best‑practice per il rendering in sandbox.

> **Prerequisiti** – È necessaria una licenza valida di Aspose.HTML per Java, Java 8 o superiore, e un IDE (IntelliJ IDEA, Eclipse o VS Code). L'esempio utilizza un file locale `input.html`, ma funziona qualsiasi URL raggiungibile.

![Diagramma del flusso del sandbox](sandbox-flow.png "esempio di impostazione di user agent personalizzato in Java")

## Passo 1: Crea una configurazione sandbox (la base)

Il sandbox isola l'ambiente di rendering dalla JVM host, il che è essenziale quando si desidera **impostare un user agent personalizzato** o modificare la dimensione della viewport.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Perché questo passo?*  
`SandboxConfiguration` contiene tutte le opzioni di rendering, incluse le **dimensioni dello schermo** e le stringhe **user‑agent**. Configurandola prima di caricare il documento, garantisci che il motore HTML rispetti tali impostazioni fin dalla prima richiesta.

## Passo 2: Imposta le dimensioni dello schermo per imitare un dispositivo reale

I siti responsive spesso leggono `window.innerWidth` e `window.innerHeight`. Per far sì che il motore pensi di essere in esecuzione su uno schermo 1024 × 768, **imposti la dimensione virtuale dello schermo**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Perché è importante* – Se ometti **l'impostazione delle dimensioni dello schermo**, il renderer potrebbe usare una viewport molto piccola, facendo sì che le media query CSS scelgano il layout mobile. Impostando esplicitamente **la larghezza dello schermo** e **l'altezza dello schermo**, controlli quali regole CSS vengono applicate.

## Passo 3: Specifica una stringa user‑agent personalizzata

Alcune pagine web forniscono contenuti diversi in base all'header user‑agent. Per **specificare il user agent** basta impostarlo nella configurazione del sandbox:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Perché usare un user agent personalizzato?*  
Una stringa personalizzata può bypassare il rilevamento dei bot, attivare funzionalità solo per desktop, o testare come un sito si comporta per una specifica versione del browser. Il motore Aspose inoltra questo valore con ogni richiesta HTTP effettuata durante il caricamento di risorse esterne (CSS, immagini, script).

## Passo 4: Carica il documento HTML all'interno del sandbox

Ora che il sandbox è completamente configurato, carica il file HTML. Il costruttore che accetta un percorso file e un `SandboxConfiguration` applica automaticamente tutte le impostazioni che abbiamo definito.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Se devi caricare da un URL remoto, sostituisci il percorso del file con la stringa URL—Aspose.HTML rispetterà comunque il **user agent personalizzato impostato** e le **dimensioni dello schermo**.

## Passo 5: Salva l'output elaborato

Dopo che il documento ha terminato il caricamento, puoi salvarlo in qualsiasi formato supportato. Qui scriviamo un file HTML sandboxed che riflette eventuali modifiche al DOM causate dalle impostazioni personalizzate.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

Il file salvato conterrà lo stesso markup, ma gli script che hanno interrogato `navigator.userAgent` o ispezionato `window.innerWidth` vedranno ora i valori che hai fornito.

## Esempio completo e eseguibile

Unendo tutti i passaggi ottieni un programma autonomo che puoi copiare, incollare ed eseguire.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Output previsto

Eseguendo il programma viene creato `sandboxed_output.html`. Se lo apri in un browser e ispezioni `navigator.userAgent` tramite la console, vedrai **AsposeHTML/1.0**. Allo stesso modo, `window.innerWidth` restituirà **1024**, confermando che le **dimensioni dello schermo impostate** hanno funzionato come previsto.

## Domande comuni e gestione dei casi limite

| Question | Answer |
|----------|--------|
| **Cosa succede se la pagina carica risorse aggiuntive da un dominio diverso?** | Il sandbox inoltra il **user agent personalizzato** con ogni richiesta, ma le politiche cross‑origin rimangono valide. Usa `sandboxConfig.setAllowCrossDomain(true)` se devi allentare tali restrizioni. |
| **Posso cambiare le dimensioni dello schermo dopo che il documento è stato caricato?** | No. Le dimensioni dello schermo vengono lette durante il passaggio di layout iniziale. Per renderizzare con una dimensione diversa, crea una nuova `SandboxConfiguration` e ricarica il documento. |
| **Devo chiamare `document.close()`?** | `HTMLDocument` implementa `AutoCloseable`. Usare un blocco try‑with‑resources garantisce una corretta pulizia, ma chiamare esplicitamente `close()` è opzionale negli script semplici. |
| **In che modo questo differisce dall'impostare un user‑agent in un client HTTP?** | Impostare il user‑agent sul sandbox influisce su **tutte** le richieste di risorse effettuate dal motore HTML, non solo sul recupero iniziale dell'HTML. Questo imita più fedelmente un browser reale. |
| **Il sandbox è sicuro per HTML non attendibile?** | Sì. Il sandbox isola l'accesso al file system e limita le chiamate di rete secondo la configurazione, riducendo il rischio che script malevoli influenzino la tua JVM host. |

## Consigli professionali

* **Riutilizza le configurazioni** – Se renderizzi molte pagine con la stessa viewport, crea un unico `SandboxConfiguration` e riutilizzalo per evitare l'overhead di creazione degli oggetti.
* **Debug con logging** – Abilita il logging di Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) per vedere quali risorse sono state recuperate con il user‑agent personalizzato.
* **Combina con le media query CSS** – Regolando **la larghezza dello schermo** puoi testare come il tuo design responsive si comporta su tablet, telefoni o grandi desktop senza aprire un browser reale.

## Conclusione

Ora sai come **impostare un user agent personalizzato** e **impostare le dimensioni dello schermo** quando renderizzi HTML con Aspose.HTML per Java. Configurando un sandbox, isoli l'ambiente, controlli la viewport e garantisci che le risorse esterne vedano gli header esatti che specifichi. Questa tecnica è essenziale per testare layout responsive, bypassare blocchi anti‑bot o riprodurre funzionalità solo desktop in pipeline automatizzate.

Successivamente, potresti esplorare **come impostare cookie personalizzati** o **catturare screenshot renderizzati** usando l'API di rendering di Aspose.HTML—entrambi i concetti si basano sullo stesso modello di configurazione sandbox che hai appena padroneggiato.

Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Rendering ad alta DPI in Java – Cattura screenshot di pagine web con User Agent personalizzato](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [Come caricare HTML, impostare DPI del dispositivo e leggere il colore di sfondo](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Creare file HTML Java e configurare il servizio di rete (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}