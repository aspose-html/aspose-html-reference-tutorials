---
title: Regola le dimensioni della pagina PDF con Aspose.HTML per Java
linktitle: Regolazione delle dimensioni della pagina PDF
second_title: Elaborazione HTML Java con Aspose.HTML
description: Scopri come adattare le dimensioni delle pagine PDF con Aspose.HTML per Java. Crea PDF di alta qualità da HTML senza sforzo. Controlla le dimensioni delle pagine in modo efficace.
type: docs
weight: 15
url: /it/java/advanced-usage/adjust-pdf-page-size/
---

Nell'era digitale odierna, la necessità di generare PDF di alta qualità da contenuti HTML è in aumento. Aspose.HTML per Java è una potente libreria Java che consente di convertire documenti HTML in formato PDF senza sforzo. In questo tutorial, ci concentreremo sulla regolazione delle dimensioni della pagina durante la conversione di HTML in PDF utilizzando Aspose.HTML per Java.

## Prerequisiti

Prima di iniziare, assicurati di avere i seguenti prerequisiti:

- Ambiente di sviluppo Java: assicurati di avere installato Java Development Kit (JDK) sul tuo sistema.
-  Aspose.HTML per Java: è necessario scaricare e installare Aspose.HTML per Java dal sito Web[Qui](https://releases.aspose.com/html/java/).
- Documento HTML: dovresti avere un documento HTML pronto per la conversione. In caso contrario, creane uno o usa un file HTML esistente.

## Importa pacchetti

Per iniziare, devi importare i pacchetti necessari per lavorare con Aspose.HTML per Java. Il seguente frammento di codice mostra come farlo:

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

Ora che hai soddisfatto i prerequisiti e hai importato i pacchetti necessari, suddividiamo il processo di regolazione delle dimensioni della pagina PDF in più passaggi:

## Fase 1: lettura del contenuto HTML

Per prima cosa, devi leggere il contenuto HTML che vuoi convertire in PDF. In questo esempio, leggeremo l'HTML da un file denominato "FirstFile.html".

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Fase 2: Scrittura di contenuti HTML

Successivamente, scriverai il contenuto HTML in un file denominato "FirstFileOut.html".

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Aggiungi stili HTML o contenuti personalizzati qui
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

## Fase 3: rendering HTML in PDF

Ora, renderizzerai il contenuto HTML in un file PDF. Ci occuperemo di due scenari: uno in cui la dimensione della pagina non è adattata alla larghezza del contenuto e un altro in cui è adattata.

### Dimensioni della pagina non regolate

In questo scenario, la dimensione della pagina è impostata su una larghezza e un'altezza fisse, il che potrebbe comportare il ritaglio del contenuto se supera queste dimensioni.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Crea un'istanza HTMLDocument dal file HTML
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Imposta le opzioni di rendering PDF
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Renderizza l'output
pdf_renderer.render(device, html_document);
```

### Dimensioni della pagina adattate alla larghezza del contenuto

In questo scenario, la dimensione della pagina viene regolata in base alla larghezza del contenuto.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

//Renderizza l'output
pdf_renderer.render(device, html_document);
```

## Conclusione

In questo tutorial, abbiamo esplorato come regolare le dimensioni della pagina PDF quando si converte HTML in PDF usando Aspose.HTML per Java. Hai appreso i prerequisiti, importato i pacchetti richiesti e seguito una guida passo passo per raggiungere questo obiettivo. Con Aspose.HTML per Java, puoi facilmente controllare le dimensioni della pagina dei tuoi PDF generati, assicurandoti che il tuo contenuto venga visualizzato come previsto.

 Sentiti libero di sperimentare diverse dimensioni di pagina e impostazioni per soddisfare le tue esigenze specifiche. Se riscontri problemi o hai altre domande, non esitare a chiedere assistenza al[Documentazione di Aspose.HTML per Java](https://reference.aspose.com/html/java/) o il[Forum di supporto Aspose](https://forum.aspose.com/).

## Domande frequenti

### D1: Che cos'è Aspose.HTML per Java?

A1: Aspose.HTML per Java è una libreria Java che consente di lavorare con documenti HTML, manipolarli, convertirli e renderli in vari formati, incluso PDF.

### D2: Come posso modificare le dimensioni della pagina PDF quando converto HTML in PDF con Aspose.HTML per Java?

 A2: È possibile regolare le dimensioni della pagina PDF utilizzando`PageSetup` classe e impostazione del`AdjustToWidestPage` proprietà a`true` o `falso, a seconda delle esigenze.

### D3: Posso personalizzare lo stile del contenuto HTML prima di convertirlo in PDF?

R3: Sì, puoi personalizzare lo stile aggiungendo elementi CSS e HTML al tuo contenuto HTML prima di convertirlo in PDF, come mostrato nel tutorial.

### D4: Dove posso trovare la documentazione per Aspose.HTML per Java?

 A4: Puoi fare riferimento alla documentazione[Qui](https://reference.aspose.com/html/java/) per informazioni ed esempi completi.

### D5: È disponibile una versione di prova gratuita di Aspose.HTML per Java?

 A5: Sì, puoi accedere a una prova gratuita di Aspose.HTML per Java da[questo collegamento](https://releases.aspose.com/).