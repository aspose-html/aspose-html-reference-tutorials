---
category: general
date: 2026-02-14
description: Come impostare i DPI per la conversione da SVG a PNG usando Java. Esporta
  PNG ad alta risoluzione, impara a convertire SVG in PNG e utilizza una libreria
  Java per la conversione di immagini.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: it
og_description: Come impostare i DPI per la conversione da SVG a PNG usando Java.
  Questa guida ti mostra come esportare PNG ad alta risoluzione e utilizzare una libreria
  Java di conversione immagini.
og_title: Come impostare i DPI durante la conversione da SVG a PNG con Java
tags:
- java
- image-conversion
- svg
- png
title: Come impostare i DPI durante la conversione da SVG a PNG con Java
url: /it/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare i DPI durante la conversione da SVG a PNG con Java

Ti sei mai chiesto **come impostare i DPI** per una conversione SVG‑to‑PNG in modo che il risultato sia nitido su un poster pronto per la stampa? Non sei il solo. In molti progetti—pensa a volantini di marketing, mock‑up UI o diagrammi tecnici—ottenere un PNG ad alta risoluzione da un SVG è imprescindibile.  

In questo tutorial vedremo passo passo **come convertire SVG in PNG**, **esportare PNG ad alta risoluzione** e, soprattutto, controllare i DPI usando la libreria Aspose.HTML per Java. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi applicazione Java, sia essa uno strumento desktop o un servizio backend.

## Cosa ti serve

- **Java 8+** (il codice si compila con qualsiasi JDK recente)
- **Aspose.HTML for Java** JAR (disponibili su Maven Central o sul sito Aspose)
- Un file SVG che desideri rasterizzare  
- Un pizzico di curiosità—nulla più.

Se usi Maven, aggiungi la dipendenza mostrata nella sezione successiva; altrimenti scarica i JAR manualmente e aggiungili al classpath.

## Passo 1: Aggiungi la libreria di conversione immagini Java

Prima di tutto, il tuo progetto ha bisogno della **libreria di conversione immagini Java** che sappia leggere SVG e scrivere PNG. Aspose.HTML è una scelta solida perché gestisce CSS, font e funzionalità vettoriali complesse fin da subito.

**Gli utenti Maven** possono incollare questo nel proprio `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Gli appassionati di Gradle** possono aggiungere:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Se preferisci il percorso manuale, scarica il JAR dalla pagina di download di Aspose e posizionalo in `libs/`, poi aggiungilo al percorso di compilazione del tuo IDE.

> **Pro tip:** Tieni d'occhio il numero di versione; le release più recenti spesso migliorano la gestione dei DPI e risolvono bug di casi limite.

## Passo 2: Crea le opzioni di conversione e imposta i DPI desiderati

Ora che la libreria è a disposizione, dobbiamo dirle *come* vogliamo che il PNG di output appaia. È qui che entra in gioco la parola chiave principale—**come impostare i DPI**. La classe `ImageConversionOptions` ti offre un controllo granulare sia sulla risoluzione orizzontale (`dpiX`) sia su quella verticale (`dpiY`).

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Perché 300 DPI? Per la maggior parte dei flussi di lavoro di stampa, 300 punti‑per‑pollice è considerata “qualità di stampa”. Se il tuo target è solo il web, puoi ridurli a 72 o 96 DPI per mantenere le dimensioni dei file contenute.

> **E se avessi bisogno di DPI diversi per larghezza e altezza?**  
> Cambia `setDpiX` e `setDpiY` in modo indipendente. La libreria rispetta valori non uniformi, utile per immagini anamorfiche.

## Passo 3: Esegui la conversione da SVG a PNG

Con le opzioni pronte, la conversione vera e propria è una singola chiamata statica. Useremo `java.nio.file.Paths` per mantenere la compatibilità tra piattaforme.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

Fatto—esegui il metodo `main` e troverai un PNG nitido a 300 DPI nella cartella `YOUR_DIRECTORY`. La libreria scala automaticamente la grafica vettoriale per corrispondere ai DPI specificati, preservando il rapporto d'aspetto e la nitidezza del testo.

## Passo 4: Verifica il risultato (opzionale ma consigliato)

Un rapido controllo di coerenza può salvarti da mal di testa in seguito. Apri il PNG generato in un visualizzatore d'immagini che mostri i metadati DPI (ad esempio Photoshop, GIMP o anche la scheda “Dettagli” di Esplora file di Windows). Dovresti vedere **300 DPI** elencati sia per la risoluzione orizzontale che verticale.

Se il file appare sfocato, ricontrolla:

1. Che l'SVG originale non sia a bassa risoluzione fin dall'inizio (i file vettoriali sono indipendenti dalla risoluzione, ma le immagini raster incorporate possono limitare la qualità).  
2. Che tu abbia effettivamente salvato il file dopo aver impostato i DPI—alcuni IDE mantengono nella cache build precedenti.  
3. Che le opzioni di conversione non siano state sovrascritte altrove nel tuo codice.

## Perché i DPI sono importanti per l'esportazione di PNG ad alta risoluzione

Potresti chiederti: “Perché preoccuparsi dei DPI? Il PNG è solo pixel?” La verità è che i DPI sono un *tag di metadati* che indica alle applicazioni a valle (soprattutto quelle orientate alla stampa) quanti pixel corrispondono a un pollice di spazio fisico. Se consegni un PNG 1200 × 800 a una stampante senza i DPI corretti, la stampante potrebbe assumere un valore predefinito (spesso 72 DPI) e ingrandire l'immagine, producendo un risultato sfocato.

Impostare correttamente i DPI è anche un vantaggio in termini di prestazioni: eviti di dover up‑scale le immagini raster in seguito, operazione computazionalmente costosa e degradante per la qualità.

## Casi limite e problemi comuni

| Situazione | Cosa controllare | Come risolvere |
|-----------|-------------------|----------------|
| **SVG contiene immagini bitmap incorporate** | La bitmap incorporata può essere a bassa risoluzione, causando un PNG finale pixelato anche a DPI alti. | Sostituisci la bitmap con una versione ad alta risoluzione o modifica l'SVG per fare riferimento a un'immagine esterna. |
| **Valori DPI molto alti (es. 1200 DPI)** | Il consumo di memoria aumenta; potresti incorrere in un `OutOfMemoryError`. | Aumenta la dimensione dell'heap JVM (`-Xmx2g`) o limita i DPI a un valore ragionevole per il tuo caso d'uso. |
| **Pixel non quadrati** | Alcuni display interpretano i DPI in modo diverso, provocando immagini allungate. | Assicurati che `setDpiX` sia uguale a `setDpiY` a meno che non ci sia una ragione specifica per differenziarli. |
| **Font mancanti** | Il testo nell'SVG potrebbe ricadere su un font predefinito, alterando il layout. | Incorpora i font nell'SVG o installa i font necessari sulla macchina di runtime. |

## Riepilogo veloce (in una frase)

Per **impostare i DPI** in una conversione SVG‑to‑PNG, crea un oggetto `ImageConversionOptions`, imposta `dpiX`/`dpiY` e chiama `Converter.convert` della libreria Aspose.HTML per Java.

## Prossimi passi e argomenti correlati

- **Elaborazione batch:** Scorri una directory di file SVG e applica le stesse impostazioni DPI.  
- **DPI dinamico:** Leggi un file di configurazione o un argomento da riga di comando per impostare i DPI a runtime.  
- **Librerie alternative:** Se non puoi usare Aspose, considera **Batik** (Apache) o **SVG Salamander**, anche se potrebbero richiedere codice aggiuntivo per gestire i DPI.  
- **Esportazione di PNG ad alta risoluzione** per risorse Android: combina questa tecnica con le cartelle `drawable‑hdpi`, `xhdpi`, ecc., di Android.

Sentiti libero di sperimentare—prova 72 DPI per miniature web, 600 DPI per stampe di grande formato, o anche 150 DPI come via di mezzo. Il codice rimane lo stesso; cambiano solo i numeri.

---

![come impostare i dpi](placeholder-image.png "Illustrazione dell'impostazione dei DPI nel flusso di conversione Java")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}