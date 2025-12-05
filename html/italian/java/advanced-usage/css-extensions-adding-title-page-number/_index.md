---
date: 2025-12-05
description: Scopri come impostare i margini delle pagine HTML in Java usando Aspose.HTML
  e aggiungere numeri di pagina e titoli ai tuoi documenti.
language: it
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Come impostare i margini della pagina HTML in Java con Aspose.HTML
url: /java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare i margini di una pagina HTML in Java con Aspose.HTML

In questo tutorial scoprirai **come impostare i margini di una pagina HTML in stile Java** utilizzando Aspose.HTML per Java. Ti guideremo nella creazione di margini personalizzati, nell'inserimento dei numeri di pagina e nell'aggiunta di un titolo al documento—tutto con codice chiaro, passo‑per‑passo, pronto per essere copiato nel tuo progetto.

## Risposte rapide
- **Quale libreria è necessaria?** Aspose.HTML per Java  
- **Posso controllare i margini programmaticamente?** Sì, tramite una regola CSS `@page` nel foglio di stile utente  
- **Quali formati di output supportano i margini?** XPS, PDF e altri formati raster  
- **È necessaria una licenza per la produzione?** È richiesta una licenza valida di Aspose.HTML per l'uso non‑trial  
- **È compatibile con Java 11+?** Assolutamente – la libreria funziona con le versioni moderne di Java  

## Che cosa significa “Impostare i margini di una pagina HTML in Java”?
Impostare i margini di una pagina HTML in Java significa configurare il motore di rendering (fornito da Aspose.HTML) per applicare le proprietà CSS della pagina‑box prima che il documento venga convertito in un formato stampabile come XPS o PDF. Definendo una regola `@page` personalizzata, controlli l'area stampabile, i numeri di pagina e il contenuto di intestazione/piè di pagina.

## Perché usare Aspose.HTML per il controllo dei margini?
- **Layout preciso** – CSS `@page` ti offre un controllo pixel‑perfect sui margini, intestazioni e piè di pagina.  
- **Coerenza tra formati** – Le stesse definizioni di margine funzionano per XPS, PDF e uscite immagine.  
- **Nessuna dipendenza dal browser** – Il rendering avviene lato server, quindi non è necessario un browser headless.  

## Prerequisiti

Prima di iniziare, assicurati di avere i seguenti prerequisiti:

1. **Ambiente di sviluppo Java** – JDK 11 o successivo installato.  
2. **Aspose.HTML per Java** – Scarica e installa la libreria da [qui](https://releases.aspose.com/html/java/).  

## Importare i pacchetti

Per cominciare, importa le classi necessarie di Aspose.HTML:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Come impostare i margini di una pagina HTML in Java – Guida passo‑per‑passo

### Passo 1: Inizializzare la configurazione e definire i margini personalizzati

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

In questo blocco creiamo un oggetto `Configuration`, otteniamo il servizio `IUserAgentService` e iniettiamo una regola CSS `@page` che definisce i margini, un contatore di pagina in basso‑a‑destra e un titolo del documento al centro‑alto.

### Passo 2: Creare il documento HTML

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Qui istanziamo un `HTMLDocument` con un semplice frammento “Hello World”. La stessa configurazione del Passo 1 viene applicata, così i margini personalizzati vengono rispettati al momento del rendering.

### Passo 3: Renderizzare in un file XPS (o qualsiasi output supportato)

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Questo passo crea un `XpsDevice` che scrive le pagine renderizzate in `output.xps`. I margini, i numeri di pagina e il titolo definiti in precedenza appariranno nel file finale.

## Problemi comuni e suggerimenti

- **I margini non cambiano** – Assicurati che la regola `@page` non venga sovrascritta da altri fogli di stile. La chiamata `setUserStyleSheet` la impone con la massima priorità.  
- **I numeri di pagina mostrano “NaN”** – Verifica di utilizzare Aspose.HTML versione 23.10 o successiva; le versioni precedenti non includono la funzione `currentPageNumber()`.  
- **Il file di output è vuoto** – Controlla che il percorso `Resources.output` sia risolto correttamente e che tu abbia i permessi di scrittura.  

## Domande frequenti

### Q1: Cos'è Aspose.HTML per Java?

**A:** Aspose.HTML per Java è una libreria Java che fornisce potenti strumenti per lavorare con documenti HTML in applicazioni Java, inclusi conversione, rendering e manipolazione.

### Q2: Posso personalizzare ulteriormente i margini della pagina?

**A:** Sì, modifica semplicemente il CSS all'interno di `setUserStyleSheet`. Puoi cambiare qualsiasi valore `margin-*` o aggiungere ulteriori box `@top-*` / `@bottom-*`.

### Q3: Come posso aggiungere più contenuto al documento HTML?

**A:** Sostituisci la stringa in `new HTMLDocument("<div>Hello World!!!</div>", …)` con il tuo markup HTML, oppure carica un file esterno usando il costruttore `HTMLDocument(String url, …)`.

### Q4: Aspose.HTML per Java è compatibile con altri formati di documento?

**A:** Assolutamente. Lo stesso `HTMLDocument` può essere renderizzato in PDF, XPS, immagini o anche EPUB cambiando il dispositivo di output (ad es., `PdfDevice`, `PngDevice`).

### Q5: È necessaria una licenza per usare Aspose.HTML per Java?

**A:** Sì, è richiesta una licenza per l'uso in produzione. Puoi ottenere una versione trial o acquistare una licenza da [qui](https://purchase.aspose.com/buy) o [qui](https://releases.aspose.com/).

### Q6: Come impostare margini diversi per pagine dispari e pari?

**A:** Usa le pseudo‑classi `@page :left` e `@page :right` nel tuo foglio di stile per definire margini distinti per le pagine di sinistra (pari) e di destra (dispari).

### Q7: Posso incorporare font personalizzati nel documento renderizzato?

**A:** Sì. Aggiungi regole `@font-face` al foglio di stile utente e fai riferimento ai font nel tuo contenuto HTML.

## Conclusione

Ora hai imparato **come impostare i margini di una pagina HTML in Java** usando Aspose.HTML, e sai aggiungere numeri di pagina e un titolo per rendere i tuoi documenti professionali. Sentiti libero di sperimentare con box `@page` aggiuntivi, font personalizzati o formati di output diversi per soddisfare le esigenze del tuo progetto.

Se incontri difficoltà, la documentazione ufficiale di [Aspose.HTML per Java](https://reference.aspose.com/html/java/) e il [forum di supporto Aspose](https://forum.aspose.com/) sono ottime risorse per ottenere aiuto.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Ultimo aggiornamento:** 2025-12-05  
**Testato con:** Aspose.HTML per Java 23.12  
**Autore:** Aspose  

---