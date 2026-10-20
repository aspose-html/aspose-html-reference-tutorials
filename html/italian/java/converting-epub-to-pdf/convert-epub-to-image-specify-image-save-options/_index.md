---
date: 2026-03-24
description: 'Scopri come impostare il colore di sfondo dell''immagine, la dimensione
  personalizzata della pagina e convertire EPUB in immagine usando Aspose.HTML per
  Java. #JavaDevelopment #WebDevelopment #DocumentConversion'
linktitle: Specifying Image Save Options for EPUB to Image Conversion
second_title: Java HTML Processing with Aspose.HTML
title: Imposta il colore di sfondo dell'immagine per la conversione da EPUB a immagine
url: /it/java/converting-epub-to-pdf/convert-epub-to-image-specify-image-save-options/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta il colore di sfondo dell'immagine per la conversione da EPUB a immagine

Nei moderni flussi di lavoro web e documentali, **Aspose.HTML for Java** ti offre la possibilità di convertire e‑book come EPUB in immagini raster mantenendo il pieno controllo sull'output visivo. Utilizzando l'opzione **set image background color** insieme a una **custom page size**, puoi produrre immagini che corrispondono perfettamente ai componenti UI, ai layout di stampa o a qualsiasi requisito di elaborazione successiva. In questa guida percorreremo l'intero processo — dai prerequisiti alla conversione finale — così potrai **convert EPUB to image** con sicurezza.

## Risposte rapide
- **Che cosa influenza la “custom page size”?** Definisce la larghezza e l'altezza dell'immagine generata in pixel.  
- **In quale formato posso convertire EPUB?** Qualsiasi formato immagine supportato da `ImageSaveOptions`, come JPEG, PNG o BMP.  
- **Come imposto un colore di sfondo dell'immagine?** Usa `options.setBackgroundColor(Color.getAliceBlue())` (o qualsiasi altro `Color`).  
- **È necessaria una licenza per lo sviluppo?** Una versione di prova gratuita è sufficiente per la valutazione; è richiesta una licenza commerciale per la produzione.  
- **Quale versione di Java è richiesta?** Java 8 o superiore con la libreria Aspose.HTML for Java.

## Che cos'è “set image background color”?
Impostare il colore di sfondo dell'immagine indica al motore di rendering quale colore utilizzare per riempire la tela prima di disegnare il contenuto della pagina. Questo è particolarmente utile quando l'EPUB di origine contiene elementi trasparenti o quando si desidera uno sfondo uniforme per tutte le pagine.

## Come impostare il colore di sfondo dell'immagine e la dimensione personalizzata della pagina in Java?
Di seguito scomponiamo i passaggi da seguire. Ogni passaggio include una breve spiegazione seguita dallo snippet di codice esatto da utilizzare (il codice stesso rimane invariato rispetto al tutorial originale).

### Prerequisiti
1. **Java Development Environment** – JDK 8 o più recente installato.  
2. **Aspose.HTML for Java** – Scarica la libreria dal sito ufficiale [here](https://releases.aspose.com/html/java/).  
3. **A Code Editor** – IntelliJ IDEA, Eclipse, VS Code o qualsiasi IDE tu preferisca.  
4. **Basic Java Knowledge** – Familiarità con la sintassi Java e la configurazione del progetto.  
5. **Enthusiasm** – Pronto a esplorare la custom page size e le altre opzioni di salvataggio immagine.

Ora che sei pronto, passiamo all'implementazione.

## Importa i pacchetti

Per prima cosa, importa le classi necessarie per il rendering e la conversione.

### Passo 1: Importa le classi Aspose.HTML

```java
import com.aspose.html.saving.ImageSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
```

Queste importazioni ti danno accesso a `ImageSaveOptions`, agli oggetti di layout della pagina e all'utilità `Converter`.

## Analisi dell'esempio: Conversione da EPUB a immagine

Di seguito trovi una guida passo‑passo su **come convertire EPUB** applicando una **custom page size** e un'opzione **set image background color**.

### Passo 2: Apri il file EPUB

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
```

Il `FileInputStream` legge l'EPUB di origine. Sostituisci `"input.epub"` con il percorso del tuo file.

### Passo 3: Inizializza ImageSaveOptions con Custom Page Size

```java
ImageSaveOptions options = new ImageSaveOptions(ImageFormat.Jpeg);
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
Size size = new Size(Length.fromPixels(3000), Length.fromPixels(1000));
anyPage.setSize(size);
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Custom Page Size**: `Size` viene creata con una larghezza di 3000 px e un'altezza di 1000 px. Regola questi valori per soddisfare le esigenze del tuo layout.  
- **Set Image Background Color**: `Color.getAliceBlue()` riempie la tela con uno sfondo azzurro chiaro; puoi sostituirlo con qualsiasi `Color` preferisci, ad esempio `Color.getTransparent()` per la trasparenza PNG.  

### Passo 4: Converti EPUB in immagine

```java
Converter.convertEPUB(fileInputStream, options, Resources.output("output.jpg"));
```

Il metodo `convertEPUB` esegue la conversione utilizzando le `options` configurate. Il risultato viene salvato come `output.jpg`.

> **Consiglio professionale:** Se hai bisogno di una **conversione epub to png**, istanzia `ImageSaveOptions` con `ImageFormat.Png` invece di `ImageFormat.Jpeg`.

Congratulazioni! Hai convertito con successo **convert epub to image** controllando le dimensioni della pagina e il colore di sfondo.

## Come impostare la dimensione della pagina (custom page size java) – approfondimento
Se ti serve una dimensione della pagina diversa per ogni EPUB, puoi calcolare le dimensioni in modo dinamico basandoti sul CSS o sui metadati del contenuto. L'oggetto `PageSetup` può essere riutilizzato in più conversioni; basta regolare il `Size` prima di ogni chiamata a `Converter.convertEPUB`.

## Problemi comuni e soluzioni

| Problema | Motivo | Soluzione |
|----------|--------|-----------|
| L'immagine di output è ritagliata | Custom page size più piccola del contenuto | Aumenta larghezza/altezza in `Size` o abilita `options.setFitToPage(true)`. |
| Lo sfondo appare nero | Colore non impostato o formato non supportato | Assicurati che `options.setBackgroundColor(...)` sia chiamato prima della conversione. |
| Conversione fallita con `NullPointerException` | File `Resources.input` mancante | Verifica il percorso e che il file EPUB esista. |

## Domande frequenti (FAQ)

### 1. Dove posso trovare la documentazione di Aspose.HTML per Java?
Puoi accedere alla documentazione [here](https://reference.aspose.com/html/java/). Fornisce informazioni complete ed esempi per aiutarti a iniziare.

### 2. È disponibile una versione di prova gratuita di Aspose.HTML per Java?
Sì, puoi scaricare una versione di prova gratuita [here](https://releases.aspose.com/). Ti consente di esplorare le funzionalità della libreria prima di effettuare un acquisto.

### 3. Come posso ottenere una licenza temporanea per Aspose.HTML per Java?
Se ti serve una licenza temporanea, puoi ottenerla [here](https://purchase.aspose.com/temporary-license/).

### 4. Aspose.HTML per Java può gestire altre conversioni di documenti?
Sì, Aspose.HTML per Java supporta varie conversioni, inclusi HTML → PDF, HTML → image e altro.

### 5. Aspose.HTML per Java è adatto sia ai principianti che agli sviluppatori esperti?
Assolutamente! I principianti possono iniziare con esempi semplici, mentre gli utenti avanzati possono sfruttare l'intera API per flussi di lavoro complessi.

**Domande aggiuntive**

**Q: Posso convertire più pagine EPUB in immagini separate?**  
A: Sì. Usa un ciclo sugli indici delle pagine, regola `options.setPageSetup(pageSetup)` per ogni pagina e chiama ripetutamente `Converter.convertEPUB`.

**Q: Come modifico la qualità dell'immagine per l'output JPEG?**  
A: Imposta `options.setQuality(90)` (valore 0‑100) prima di avviare la conversione.

**Q: La libreria supporta sfondi trasparenti?**  
A: Per l'output PNG, puoi usare `options.setBackgroundColor(Color.getTransparent())`.

## Argomenti correlati che potresti esplorare
- **How to convert EPUB to PNG** – passa a `ImageFormat.Png` e opzionalmente imposta uno sfondo trasparente.  
- **Batch converting multiple EPUB files** – itera su una cartella di EPUB e riutilizza la stessa istanza di `ImageSaveOptions`.  
- **Optimizing image size for web** – usa `options.setQuality()` e `options.setResolution()` per bilanciare la fedeltà visiva e la dimensione del file.

## Conclusione

Aspose.HTML for Java ti offre un controllo granulare sulle conversioni da EPUB a immagine. Configurando **custom page size**, **set image background color** e altre `ImageSaveOptions`, puoi produrre immagini che corrispondono perfettamente ai requisiti visivi del tuo progetto. Sentiti libero di sperimentare con formati diversi, dimensioni e colori di sfondo, ed esplorare le capacità più ampie di Aspose.HTML per Java nelle tue applicazioni.

Hai domande o hai bisogno di assistenza? Rivolgiti alla [Aspose.HTML community](https://forum.aspose.com/) per supporto.

---

**Ultimo aggiornamento:** 2026-03-24  
**Testato con:** Aspose.HTML for Java 24.12  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}