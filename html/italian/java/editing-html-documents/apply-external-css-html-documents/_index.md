---
title: Applicare CSS esterni ai documenti HTML in Aspose.HTML per Java
linktitle: Applicare CSS esterni ai documenti HTML in Aspose.HTML per Java
second_title: Elaborazione HTML Java con Aspose.HTML
description: Scopri come applicare CSS esterni ai documenti HTML usando Aspose.HTML per Java! Segui questa guida passo passo per un tutorial completo.
weight: 12
url: /it/java/editing-html-documents/apply-external-css-html-documents/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applicare CSS esterni ai documenti HTML in Aspose.HTML per Java

## Introduzione
Quando si lavora con documenti HTML, applicare stili può fare la differenza nella presentazione e nell'esperienza utente. Se ti stai tuffando in Java e vuoi imparare come applicare stili CSS esterni ai tuoi documenti HTML usando la libreria Aspose.HTML, sei nel posto giusto! Questa guida mira a illuminare il processo passo dopo passo, rendendolo facile anche per coloro che potrebbero essere nuovi a Java o CSS.
## Prerequisiti
Prima di immergerti nel codice, ecco alcune cose che devi sapere:
### 1. Kit di sviluppo Java (JDK)
 Assicurati di avere JDK installato sulla tua macchina. Puoi scaricare l'ultima versione da[Sito web Java di Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
### 2. Aspose.HTML per Java
Dovrai aver configurato Aspose.HTML per Java. Se non lo hai ancora fatto, vai su[Pagina di download di Aspose](https://releases.aspose.com/html/java/) e prendi la biblioteca.
### 3. Un IDE o un editor di testo
Scegli un ambiente di sviluppo integrato (IDE) come IntelliJ IDEA, Eclipse o anche un semplice editor di testo per scrivere il tuo codice Java.
### 4. Conoscenza di base di Java
La familiarità con la programmazione Java e con le basi del CSS ti aiuterà sicuramente a seguire il corso con maggiore facilità.
## Importa pacchetti
Una volta impostato tutto, il passo successivo è importare i pacchetti necessari nel tuo progetto Java. Ecco cosa ti serve:
```java
import com.aspose.html.HTMLDocument;
```
Queste importazioni ti consentiranno di manipolare documenti HTML e di convertirli in formati diversi, come ad esempio PDF.

Suddivideremo il nostro tutorial in passaggi gestibili. Ogni passaggio ti guiderà attraverso il processo di applicazione di stili CSS esterni a un documento HTML utilizzando Aspose.HTML per Java.
## Passaggio 1: creare un documento HTML
Per prima cosa, dobbiamo creare il nostro documento HTML. Inizieremo definendo il contenuto con una semplice struttura HTML.
```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
HTMLDocument document = new HTMLDocument(content, ".");
```

 Qui abbiamo definito una struttura HTML di base, che include un`<div>` con due paragrafi. Il`HTMLDocument` La classe viene utilizzata per creare una rappresentazione del documento del nostro contenuto HTML.
## Passaggio 2: creare un elemento di stile
 Successivamente, creeremo un`style` elemento per contenere le nostre regole CSS.
```java
Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;} \n" +
        ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

 Utilizzando il`createElement` metodo di`HTMLDocument` , creiamo un nuovo`<style>` elemento e impostarne il contenuto per includere le nostre definizioni CSS per due classi:`frame1` E`frame2`Queste classi definiscono margini, spaziatura, dimensioni, colori di sfondo, famiglie di font e colori del testo.
## Passaggio 3: aggiungere lo stile all'intestazione del documento
Ora che abbiamo il nostro CSS al suo posto, dobbiamo aggiungere il nostro elemento di stile alla testa del documento.
```java
Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

 Recuperiamo la testa del documento e aggiungiamo il nostro appena creato`style` elemento. Questa azione integra efficacemente il nostro CSS nel documento HTML, consentendogli di definire lo stile del nostro contenuto HTML.
## Passaggio 4: applicare le classi agli elementi HTML
Successivamente applicheremo le classi CSS definite in precedenza agli elementi del paragrafo.
```java
HTMLElement paragraph = (HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

Qui, accediamo al primo e all'ultimo elemento del paragrafo nel documento e assegniamo loro le classi CSS che abbiamo creato. Questa assegnazione assicura che aderiscano agli stili definiti nel nostro CSS.
## Passaggio 5: impostare proprietà di stile aggiuntive
Per migliorare ulteriormente l'aspetto, imposteremo proprietà di stile aggiuntive per i nostri paragrafi.
```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

In questa fase, stiamo perfezionando i nostri stili. La dimensione del carattere del primo paragrafo viene aumentata e centrata, mentre vengono definiti il colore, la dimensione del carattere e la famiglia di caratteri dell'ultimo paragrafo. Questa rifinitura è fondamentale per la leggibilità e l'attrattiva estetica.
## Passaggio 6: Salvare il documento HTML
Una volta applicati gli stili, è il momento di salvare il documento HTML.
```java
document.save("edit-internal-css.html");
```

 Qui utilizziamo il`save` metodo del`HTMLDocument` classe per scrivere il contenuto HTML modificato in un file, preservando così stili e modifiche.
## Passaggio 7: convertire il documento in PDF
Infine, trasformiamo il documento in formato PDF per l'output.
```java
PdfDevice device = new PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

 Utilizzando il`PdfDevice` classe, abbiamo impostato il rendering del nostro documento HTML in un PDF. Questo passaggio è fondamentale quando si desidera condividere il documento formattato in un formato universalmente accessibile.
## Conclusione
Ed ecco fatto: applicare CSS esterni a documenti HTML usando Aspose.HTML per Java è semplice e gratificante! Con solo poche righe di codice, puoi trasformare testo normale in documenti visivamente accattivanti e con uno stile professionale. Quindi, che tu stia progettando per uso personale, creando report o sviluppando contenuti web, capire come manipolare HTML e CSS in Java è una potente abilità da avere nel tuo kit di strumenti.
## Domande frequenti
### Che cos'è Aspose.HTML per Java?
Aspose.HTML per Java è una potente libreria che consente agli sviluppatori di lavorare con documenti HTML nelle applicazioni Java, offrendo una vasta gamma di funzionalità, dalla manipolazione HTML al rendering.
### Ho bisogno di una connessione Internet per utilizzare Aspose.HTML?
No, una volta scaricati i file di libreria necessari, puoi utilizzare Aspose.HTML offline.
### Posso applicare più file CSS a un documento HTML?
 Sì, puoi crearne più di uno`<link>` elementi e aggiungerli all'intestazione del documento per vari file CSS.
### C'è differenza tra CSS interno ed esterno?
Sì! Il CSS interno è definito all'interno di un documento HTML, mentre il CSS esterno è inserito in un file separato e collegato al documento.
### Come posso ottenere supporto per Aspose.HTML per Java?
 Puoi accedere al supporto della comunità tramite[Forum di Aspose](https://forum.aspose.com/c/html/29) per qualsiasi domanda o problema che potresti incontrare.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
