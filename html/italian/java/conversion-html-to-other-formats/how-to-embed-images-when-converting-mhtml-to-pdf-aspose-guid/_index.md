---
category: general
date: 2026-03-29
description: Come incorporare le immagini durante la conversione da MHTML a PDF con
  Aspose HTML. Riduci le dimensioni del file PDF e padroneggia le tecniche di conversione
  da Aspose HTML a PDF in pochi minuti.
draft: false
keywords:
- how to embed images
- convert mhtml to pdf
- reduce pdf file size
- aspose html to pdf
- reduce pdf size
language: it
og_description: Come incorporare le immagini durante la conversione da MHTML a PDF
  con Aspose HTML. Scopri come ridurre le dimensioni del file PDF e sfruttare al massimo
  Aspose HTML to PDF.
og_title: Come incorporare le immagini durante la conversione da MHTML a PDF – Guida
  Aspose
tags:
- Aspose
- Java
- PDF
- MHTML
title: Come incorporare le immagini durante la conversione da MHTML a PDF – Guida
  Aspose
url: /it/java/conversion-html-to-other-formats/how-to-embed-images-when-converting-mhtml-to-pdf-aspose-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come incorporare le immagini durante la conversione da MHTML a PDF – Guida Aspose

Ti sei mai chiesto **come incorporare le immagini** durante una conversione da MHTML a PDF e mantenere il file risultante leggero? Non sei l'unico. Molti sviluppatori si trovano in difficoltà quando i loro PDF crescono perché ogni risorsa—font, script, persino piccole icone—viene inserita al loro interno. La buona notizia? Con Aspose.HTML per Java puoi indicare al convertitore di incorporare **solo le immagini**, lasciando tutto il resto come riferimenti esterni. Questa singola modifica riduce spesso le dimensioni del PDF in modo drastico.

In questo tutorial vedremo come convertire un report MHTML in PDF, concentrandoci su **come incorporare le immagini**, e aggiungeremo alcuni consigli extra per **ridurre le dimensioni del file PDF**. Alla fine avrai una classe Java pronta all'uso, comprenderai perché è importante incorporare solo le immagini e saprai dove andare se in seguito dovrai incorporare font o altre risorse. Niente scorciatoie vaghe tipo “vedi la documentazione” — solo una soluzione completa, pronta da copiare e incollare.

## Cosa imparerai

- Le chiamate API esatte necessarie per **convertire MHTML in PDF** con Aspose.HTML.
- Come configurare `PdfConversionOptions` affinché il convertitore **incorpori solo le immagini**.
- Perché incorporare solo le immagini aiuta a **ridurre le dimensioni del PDF** e quando potresti volere un'impostazione diversa.
- Un esempio Java completo e eseguibile che puoi inserire in qualsiasi progetto Maven/Gradle.
- Problemi comuni (risorse mancanti, percorsi file errati) e soluzioni rapide.

### Prerequisiti

- Java 8 o versioni successive installate.
- Maven o Gradle per gestire le dipendenze (mostreremo lo snippet Maven).
- Libreria Aspose.HTML per Java (puoi scaricare una prova gratuita dal sito di Aspose).
- Un file MHTML che desideri trasformare in PDF (l'esempio utilizza `report.mhtml`).

> **Consiglio professionale:** mantieni il tuo MHTML e il PDF di output nella stessa cartella durante i test; i percorsi relativi mantengono le cose ordinate.

---

## Passo 1 – Aggiungi Aspose.HTML al tuo progetto

Se utilizzi Maven, incolla quanto segue nel tuo `pom.xml`. La versione mostrata è l'ultima a marzo 2026; controlla il repository di Aspose per versioni più recenti.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Per Gradle, l'equivalente è:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

Una volta risolta la dipendenza, sei pronto a importare le classi di cui avremo bisogno.

## Passo 2 – Crea le opzioni di conversione e imposta la modalità di incorporamento

Il cuore di **come incorporare le immagini** risiede in `PdfConversionOptions`. Per impostazione predefinita Aspose incorpora *tutte* le risorse (font, CSS, immagini). Cambieremo questo valore in `EMBED_IMAGES_ONLY`.

```java
// Step 2: Prepare conversion options – embed only images
PdfConversionOptions options = new PdfConversionOptions();
options.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);
```

Perché è importante? Immagina un report aziendale che fa riferimento a un font corporativo memorizzato su una condivisione di rete. Incorporare quel font gonfia il PDF di centinaia di kilobyte anche se il visualizzatore può recuperarlo da remoto. Incorporando solo le immagini, il PDF mantiene la fedeltà visiva necessaria rimanendo leggero.

## Passo 3 – Esegui la conversione

Ora chiamiamo `Converter.convert`, passando il percorso MHTML di origine, il percorso PDF di destinazione e le opzioni appena configurate.

```java
// Step 3: Convert MHTML to PDF using the options above
String sourcePath = "YOUR_DIRECTORY/report.mhtml";
String targetPath = "YOUR_DIRECTORY/report.pdf";

Converter.convert(sourcePath, targetPath, options);
```

Se tutto è collegato correttamente, vedrai comparire un `report.pdf` accanto al tuo file MHTML. Aprilo: ogni immagine del report originale dovrebbe essere presente, mentre font e CSS rimangono riferimenti esterni.

## Passo 4 – Verifica la riduzione delle dimensioni del PDF

Un rapido controllo di coerenza aiuta a confermare che hai effettivamente **ridotto le dimensioni del PDF**. Confronta la dimensione del file prima e dopo aver cambiato la modalità di incorporamento:

```java
File before = new File("YOUR_DIRECTORY/report_full.pdf"); // generated with default settings
File after  = new File(targetPath); // our image‑only PDF

System.out.println("Full embed size: " + before.length() / 1024 + " KB");
System.out.println("Images‑only size: " + after.length() / 1024 + " KB");
```

Nella maggior parte dei casi vedrai una diminuzione del 30‑70 % a seconda di quanti font o file CSS erano originariamente incorporati. È un vantaggio notevole per chi distribuisce PDF sul web o li archivia in un bucket cloud.

## Passo 5 – Esempio completo e eseguibile

Di seguito trovi l'intera classe Java che puoi copiare nel tuo IDE. Sostituisci `YOUR_DIRECTORY` con il percorso reale della cartella dove si trova `report.mhtml`.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.converters.ResourceEmbeddingMode;

import java.io.File;

public class MhtmlToPdf {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define source and destination ----------
        String sourcePath = "YOUR_DIRECTORY/report.mhtml";
        String targetPath = "YOUR_DIRECTORY/report.pdf";

        // ---------- Step 2: Set conversion options (embed only images) ----------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);

        // ---------- Step 3: Run the conversion ----------
        Converter.convert(sourcePath, targetPath, conversionOptions);
        System.out.println("Conversion complete! PDF saved to: " + targetPath);

        // ---------- Step 4: (Optional) Show size reduction ----------
        File outputPdf = new File(targetPath);
        System.out.println("Resulting PDF size: " + outputPdf.length() / 1024 + " KB");
    }
}
```

**Output previsto** (sulla console):

```
Conversion complete! PDF saved to: YOUR_DIRECTORY/report.pdf
Resulting PDF size: 842 KB
```

Apri `report.pdf` in qualsiasi visualizzatore; dovresti vedere tutte le immagini originali renderizzate correttamente. Se noti immagini mancanti, verifica che gli URL delle immagini nel MHTML siano assoluti o che i file siano raggiungibili dalla macchina di conversione.

## Domande comuni e gestione dei casi limite

### Cosa succede se *devo* incorporare i font?

Passa `ResourceEmbeddingMode` a `EMBED_ALL` o `EMBED_FONTS_ONLY`. L'enumerazione offre quattro scelte:

| Modalità                | Cosa viene incorporato |
|--------------------------|------------------------|
| `EMBED_ALL`              | Immagini, font, CSS |
| `EMBED_IMAGES_ONLY`      | Solo le immagini (impostazione predefinita) |
| `EMBED_FONTS_ONLY`       | Solo i font |
| `EMBED_NONE`             | Niente (solo riferimenti esterni) |

### Il mio MHTML contiene CSS esterno che influisce sul layout—il PDF sarà rotto?

Poiché non stiamo incorporando il CSS, il convertitore lo scaricherà comunque durante la conversione. Se il CSS è ospitato su un intranet a cui il server di conversione non può accedere, il layout potrebbe tornare ai valori predefiniti. In questi casi, incorpora il CSS (`EMBED_ALL`) oppure copia il foglio di stile localmente e modifica il MHTML per puntare al file locale.

### Posso elaborare in batch una cartella di file MHTML?

Assolutamente sì. Avvolgi la logica di conversione in un ciclo che itera su `File.listFiles()` e modifica il nome del file di destinazione di conseguenza. Ricorda solo di riutilizzare una singola istanza di `PdfConversionOptions` per migliorare le prestazioni.

### E per quanto riguarda il consumo di memoria per documenti enormi?

Aspose.HTML trasmette in streaming il contenuto, quindi l'uso della memoria rimane contenuto. Tuttavia, immagini molto grandi possono comunque provocare picchi. Se incontri un `OutOfMemoryError`, considera di ridurre la risoluzione delle immagini prima di incorporarle — Aspose offre `ImageConversionOptions` per questo, ma è un argomento per un altro tutorial.

## Conclusione

Ora sai **come incorporare le immagini** quando converti MHTML in PDF con Aspose.HTML, e hai visto perché questa piccola impostazione può **ridurre drasticamente le dimensioni del PDF**. L'esempio Java completo, pronto da copiare e incollare, dimostra l'intero flusso — dall'aggiunta della dipendenza Maven alla stampa della dimensione finale del file.

Da qui potresti:

- Sperimentare con `EMBED_FONTS_ONLY` se i tuoi PDF devono essere completamente autonomi.
- Automatizzare le conversioni batch per un'intera cartella di report.
- Combinare questa tecnica con le API di ottimizzazione PDF di Aspose per file ancora più piccoli.

Che tu stia costruendo un servizio di reporting, una pipeline email‑to‑PDF, o semplicemente pulendo pagine web archiviate, controllare cosa viene incorporato è una leva fondamentale per prestazioni e costi. Provalo, regola le opzioni e lascia che i tuoi PDF rimangano il più snelli possibile.

*Buon coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}