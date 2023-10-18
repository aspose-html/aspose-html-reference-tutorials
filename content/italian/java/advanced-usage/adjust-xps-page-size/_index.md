---
title: Regola le dimensioni della pagina XPS con Aspose.HTML per Java
linktitle: Regolazione delle dimensioni della pagina XPS
second_title: Elaborazione HTML Java con Aspose.HTML
description: Scopri come regolare le dimensioni della pagina XPS con Aspose.HTML per Java. Controlla facilmente le dimensioni di output dei tuoi documenti XPS.
type: docs
weight: 16
url: /it/java/advanced-usage/adjust-xps-page-size/
---

In questo tutorial, ti guideremo attraverso il processo di regolazione delle dimensioni della pagina XPS utilizzando Aspose.HTML per Java. Questa potente libreria ti consente di manipolare documenti HTML e renderli in vari formati, incluso XPS. La regolazione delle dimensioni della pagina è essenziale quando è necessario controllare le dimensioni di output del documento XPS.

## Prerequisiti

Prima di iniziare, assicurati di disporre dei seguenti prerequisiti:

1. Ambiente di sviluppo Java: assicurati di avere Java Development Kit (JDK) installato sul tuo sistema.

2.  Libreria Aspose.HTML per Java: è necessario scaricare e includere la libreria Aspose.HTML per Java nel progetto Java. Puoi trovare la biblioteca[Qui](https://releases.aspose.com/html/java/).

3. File HTML di input: prepara un file HTML di cui desideri eseguire il rendering e per il quale regola le dimensioni della pagina XPS. Puoi utilizzare il tuo file HTML per questo tutorial.

## Importa pacchetti

Innanzitutto, devi importare i pacchetti necessari per lavorare con Aspose.HTML per Java. Includi questi pacchetti all'inizio della tua classe Java:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Passaggio 1: impostare il nome del file di input

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 In questo passaggio, leggiamo il file di input HTML utilizzando un file`FileInputStream`.

## Passaggio 2: crea un documento HTML e imposta gli stili

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Questo passaggio prevede la creazione di un file`HTMLDocument` e aggiungendo stili ad esso.

## Passaggio 3: crea opzioni di rendering XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Qui creiamo opzioni di rendering XPS per configurare il processo di rendering.

## Passaggio 4: regola le dimensioni della pagina

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Questo passaggio prevede l'impostazione delle dimensioni della pagina e la specifica se adattarla alla pagina più larga.

## Passaggio 5: rendering dell'output

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Nel passaggio finale, eseguiamo il rendering dell'output XPS utilizzando le opzioni configurate.

## Conclusione

In questo tutorial, ti abbiamo mostrato come regolare le dimensioni della pagina XPS utilizzando Aspose.HTML per Java. Puoi controllare le dimensioni di output dei tuoi documenti XPS, assicurandoti che soddisfino i tuoi requisiti specifici. Con il codice e i passaggi forniti, puoi facilmente implementare questa funzionalità nelle tue applicazioni Java.

 Se hai domande o hai bisogno di ulteriore assistenza, non esitare a visitare il[Aspose.HTML per la documentazione Java](https://reference.aspose.com/html/java/) o chiedi aiuto su[Aspose Forum](https://forum.aspose.com/).

## Domande frequenti

### Q1: Cos'è Aspose.HTML per Java?

A1: Aspose.HTML per Java è una libreria Java che consente agli sviluppatori di manipolare e convertire documenti HTML in vari formati, come XPS, PDF e immagini.

### Q2: Dove posso scaricare Aspose.HTML per Java?

 A2: È possibile scaricare la libreria Aspose.HTML per Java da[questo link](https://releases.aspose.com/html/java/).

### Q3: È disponibile una prova gratuita per Aspose.HTML per Java?

 A3: Sì, puoi ottenere una prova gratuita di Aspose.HTML per Java da[Qui](https://releases.aspose.com/).

### Q4: Come posso ottenere una licenza temporanea per Aspose.HTML per Java?

 A4: Per ottenere una licenza temporanea per Aspose.HTML per Java, visitare[questa pagina](https://purchase.aspose.com/temporary-license/).

### Q5: Posso ottenere supporto per Aspose.HTML per Java?

 R5: Sì, puoi chiedere aiuto e supporto alla comunità Aspose su[Aspose Forum](https://forum.aspose.com/).