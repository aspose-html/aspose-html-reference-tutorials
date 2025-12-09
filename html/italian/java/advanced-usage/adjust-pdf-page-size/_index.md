---
date: 2025-12-01
description: Scopri come regolare le dimensioni della pagina PDF, convertire HTML
  in PDF e generare PDF da HTML usando Aspose.HTML per Java. Controlla facilmente
  le dimensioni della pagina.
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Regola le dimensioni della pagina PDF con Aspose.HTML per Java
url: /it/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Regola la dimensione della pagina PDF con Aspose.HTML per Java

La generazione di PDF da HTML è una esigenza comune per report, fatture e e‑book. Quando **regoli la dimensione della pagina PDF** ti assicuri che il documento finale corrisponda al layout che hai progettato in HTML. In questo tutorial imparerai a renderizzare HTML come PDF, impostare dimensioni personalizzate e controllare se la pagina si espande automaticamente al contenuto più largo. Seguiremo un esempio completo e pratico usando Aspose.HTML per Java.

## Risposte rapide
- **Che cosa significa “regolare la dimensione della pagina PDF”?** Consente di definire larghezza e altezza di ogni pagina PDF o di far sì che il renderer adatti automaticamente l'elemento più largo.  
- **Quale libreria viene utilizzata?** Aspose.HTML per Java (ultima versione).  
- **Ho bisogno di una licenza?** Una versione di prova gratuita è sufficiente per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **Posso modificare le dimensioni programmaticamente?** Sì – usa `PageSetup` e la proprietà `AdjustToWidestPage`.  
- **È compatibile con Java 8+?** Assolutamente – l'API funziona con qualsiasi JDK 8 o successivo.

## Che cosa è “regolare la dimensione della pagina PDF”?
Regolare la dimensione della pagina PDF significa configurare le dimensioni di ogni pagina che il renderer HTML crea. Puoi impostare una dimensione fissa (ad es., A4, Letter) o lasciare che il renderer calcoli la larghezza ottimale in base al contenuto. Questo ti offre un controllo preciso su layout, paginazione e fedeltà visiva.

## Perché regolare la dimensione della pagina PDF durante la conversione da HTML a PDF?
- **Preservare l'intento del design:** Evita che il contenuto venga tagliato o allungato.  
- **Ottimizzare per la stampa:** Abbina la dimensione della carta richiesta dai processi successivi.  
- **Migliorare la leggibilità:** Evita spazi bianchi eccessivi o testo troppo compresso.  
- **Documenti dinamici:** Adatta automaticamente tabelle o immagini larghe senza calcoli manuali.

## Prerequisiti
Prima di iniziare, assicurati di avere:

- **Java Development Kit (JDK) 8 o superiore** installato sulla tua macchina.  
- **Aspose.HTML per Java** – scarica l'ultimo JAR dalla [pagina di rilascio ufficiale](https://releases.aspose.com/html/java/).  
- **Un file HTML** che desideri convertire (useremo `FirstFile.html` nell'esempio).  

## Importa i pacchetti
Per prima cosa, importa le classi di cui avremo bisogno. Il blocco di codice qui sotto è invariato rispetto al tutorial originale.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## Passo 1: Leggi il contenuto HTML
Leggiamo il file HTML sorgente usando un `FileInputStream`. Questo passaggio prepara il markup grezzo per la successiva manipolazione.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Passo 2: Scrivi (e opzionalmente arricchisci) l'HTML
Qui copiamo l'HTML originale in un nuovo file e iniettiamo alcuni stili inline per dimostrare come lo styling influisce sull'output PDF. Sentiti libero di sostituire il CSS di esempio con il tuo.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Passo 3: Renderizza HTML in PDF – Due scenari
Ora vedremo come **generare PDF da HTML** con due diverse strategie di dimensione della pagina.

### 3.1 Dimensione della pagina NON regolata alla larghezza del contenuto
In questo caso fissiamo le dimensioni della pagina (100 × 100 punti). Se qualche elemento supera questi limiti, verrà ritagliato.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 Dimensione della pagina REGOLATA alla larghezza del contenuto
Qui abilitiamo `AdjustToWidestPage`, così il renderer espande automaticamente la larghezza della pagina per accogliere l'elemento più largo mantenendo l'altezza fissa.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## Come impostare le dimensioni PDF (come cambiare la dimensione della pagina PDF) nel codice
L'oggetto `PageSetup` è la chiave:

- `setAnyPage(Page page)`: definisce la larghezza × altezza di base.  
- `setAdjustToWidestPage(boolean)`: attiva/disattiva l'allargamento automatico.  

Regolando queste due proprietà puoi **impostare le dimensioni PDF** per qualsiasi scenario, sia che tu abbia bisogno di una pagina A4 statica o di una larghezza dinamica che segue il layout HTML.

## Problemi comuni e consigli
| Problema | Perché succede | Soluzione |
|-------|----------------|-----|
| Il contenuto viene tagliato | La dimensione fissa è troppo piccola | Aumenta i valori di `Size` o abilita `AdjustToWidestPage`. |
| Il testo appare sfocato | Il DPI di rendering predefinito è basso | Usa `PdfRenderingOptions.setResolution(int dpi)` per aumentare la qualità. |
| Gli stili sono mancanti | CSS esterno non caricato | Incorpora il CSS inline o usa `HTMLDocument.setBaseUrl()` per puntare alla cartella dei fogli di stile. |
| File HTML di grandi dimensioni causano OutOfMemoryError | Il renderer carica l'intero documento in memoria | Elabora il documento a blocchi o aumenta l'heap JVM (`-Xmx`). |

## Domande frequenti

**Q: Che cos'è Aspose.HTML per Java?**  
A: È una libreria Java che consente di creare, modificare e renderizzare documenti HTML, inclusa la conversione in PDF, PNG e altri formati.

**Q: Come posso regolare la dimensione della pagina PDF durante la conversione da HTML a PDF con Aspose.HTML per Java?**  
A: Usa la classe `PageSetup` e imposta `AdjustToWidestPage` su `true` (dimensione automatica) o `false` (dimensione fissa). Quindi assegna la `Size` desiderata tramite `new Page(new Size(width, height))`.

**Q: Posso personalizzare lo styling del contenuto HTML prima di convertirlo in PDF?**  
A: Sì – puoi iniettare CSS, modificare il DOM o usare fogli di stile esterni. Il tutorial dimostra l'iniezione di CSS inline.

**Q: Dove posso trovare la documentazione per Aspose.HTML per Java?**  
A: Documentazione completa è disponibile [qui](https://reference.aspose.com/html/java/).

**Q: È disponibile una versione di prova gratuita per Aspose.HTML per Java?**  
A: Assolutamente – scarica una versione di prova dalla [pagina di rilascio](https://releases.aspose.com/html/java/).

## Conclusione
Ora sai come **regolare la dimensione della pagina PDF**, **renderizzare HTML come PDF** e **impostare dimensioni PDF personalizzate** usando Aspose.HTML per Java. Sperimenta con diverse dimensioni di pagina, impostazioni DPI e modifiche CSS per perfezionare l'output per il tuo caso d'uso specifico. Se incontri difficoltà, consulta la documentazione ufficiale o i forum di supporto di Aspose.

---

**Last Updated:** 2025-12-01  
**Tested With:** Aspose.HTML for Java 24.12 (latest)  
**Author:** Aspose  
**Related Resources:** [Riferimento API](https://reference.aspose.com/html/java/) | [Scarica versione di prova gratuita](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}