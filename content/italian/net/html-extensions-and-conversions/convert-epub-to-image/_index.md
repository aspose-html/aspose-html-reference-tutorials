---
title: Converti EPUB in immagine in .NET con Aspose.HTML
linktitle: Converti EPUB in immagine in .NET
second_title: Aspose.HTML .NET API di manipolazione HTML
description: Scopri come convertire EPUB in immagini utilizzando Aspose.HTML per .NET. Tutorial passo passo con esempi di codice e opzioni personalizzabili.
type: docs
weight: 11
url: /it/net/html-extensions-and-conversions/convert-epub-to-image/
---

Nell'era digitale di oggi, la capacità di manipolare e convertire vari formati di documenti è un'abilità preziosa. Aspose.HTML per .NET è un potente strumento che consente agli sviluppatori di lavorare con documenti HTML ed EPUB senza sforzo. In questo tutorial, approfondiremo il mondo di Aspose.HTML per .NET e ti guideremo attraverso il processo di conversione dei documenti EPUB in vari formati di immagine. Suddivideremo ogni esempio in più passaggi, spiegando ogni passaggio lungo il percorso.

## Prerequisiti

Prima di immergerci nel mondo di Aspose.HTML per .NET, dovresti assicurarti di disporre dei seguenti prerequisiti:

1. Visual Studio: assicurati di avere Visual Studio installato sul tuo sistema. Puoi scaricarlo dal sito web.

2.  Aspose.HTML per .NET: è possibile ottenere la libreria dal sito Web Aspose[Qui](https://releases.aspose.com/html/net/).

3. La tua directory dei dati: prepara una directory in cui memorizzi i tuoi file EPUB e dove verranno salvate le immagini di output.

4. Conoscenza di base di C#: la familiarità con la programmazione C# è essenziale per comprendere e implementare gli esempi di codice forniti in questo tutorial.

## Importazione degli spazi dei nomi necessari

Prima di iniziare a lavorare con Aspose.HTML per .NET, è necessario importare gli spazi dei nomi richiesti nel codice C#. Questi spazi dei nomi forniscono l'accesso alle funzionalità Aspose.HTML per .NET.

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

Ora che abbiamo i prerequisiti e gli spazi dei nomi, passiamo agli esempi passo passo.

## Conversione di EPUB in JPEG

```csharp
    string dataDir = "Your Data Directory";
    // Apri un file EPUB esistente per la lettura.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // Chiama il metodo ConvertEPUB per convertire il file EPUB in immagine.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Passi

1. Fornisci il percorso del tuo file EPUB nella variabile dataDir.
2. Apri il file EPUB per la lettura utilizzando FileStream.
3. Chiama il metodo ConvertEPUB, passando il flusso EPUB, un ImageSaveOptions che specifica il formato di output (JPEG) e il nome del file di output ("output.jpg").
5. Il file EPUB viene convertito in un'immagine JPEG.

In questo esempio, apriamo un file EPUB, ne leggiamo il contenuto e lo convertiamo in un formato immagine JPEG. L'immagine di output viene salvata come "output.jpg".

## Conversione di EPUB in PNG

Puoi convertire facilmente file EPUB in vari formati immagine come PNG, BMP, GIF e TIFF utilizzando strutture di codice simili. Ecco un esempio per la conversione in PNG:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### Passi
1. Apri il file EPUB per la lettura utilizzando FileStream.
2. Inizializza un oggetto ImageSaveOptions con il formato di output desiderato (in questo caso, PNG).
3. Chiama il metodo ConvertEPUB, passando il flusso EPUB, le opzioni di salvataggio dell'immagine e il nome del file di output.
4. Il file EPUB viene convertito nel formato immagine specificato.

## Specificare le opzioni di salvataggio dell'immagine

Puoi personalizzare l'output dell'immagine specificando opzioni come la dimensione della pagina e il colore dello sfondo. Ecco un esempio:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### Passi

1.  Fornisci il percorso del tuo file EPUB nel file`dataDir` variabile.
2.  Apri il file EPUB per la lettura utilizzando a`FileStream`.
3.  Creare un`ImageSaveOptions` oggetto e specificare il formato di output desiderato (JPEG).
4. Personalizza le dimensioni della pagina e il colore dello sfondo, se necessario.
5.  Chiama il`ConvertEPUB`metodo, passando il flusso EPUB, le opzioni di salvataggio dell'immagine e il nome del file di output.
6. Il file EPUB viene convertito in un'immagine con le opzioni specificate.

## Specifica un provider di streaming personalizzato

Se è necessario manipolare il flusso di output, è possibile utilizzare un provider di flusso personalizzato. Ecco un esempio:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
Codice sorgente della classe MemoryStreamProvider.

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Elenco degli oggetti MemoryStream creati durante il rendering del documento
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Questo metodo viene chiamato quando è richiesto un unico flusso di output, ad esempio per i formati XPS, PDF o TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Questo metodo viene chiamato quando è richiesta la creazione di più flussi di output. Ad esempio durante il rendering dell'HTML nell'elenco dei file immagine (JPG, PNG, ecc.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Qui puoi rilasciare il flusso pieno di dati e, ad esempio, scaricarlo sul disco rigido
            }
            public void Dispose()
            {
                // Rilascio di risorse
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```

### Passi
1.  Fornisci il percorso del tuo file EPUB nel file`dataDir` variabile.
2.  Apri il file EPUB per la lettura utilizzando a`FileStream`.
3.  Creare un`MemoryStreamProvider` per gestire flussi di output personalizzati.
4.  Chiama il`ConvertEPUB` metodo, passando il flusso EPUB, le opzioni di salvataggio dell'immagine (JPEG) e il provider di flusso personalizzato.
5. Scorrere i flussi di memoria nel provider personalizzato, salvarli in singoli file.
6. Questo esempio consente di manipolare e salvare più flussi di output secondo necessità.

## Conclusione

Aspose.HTML per .NET è una libreria versatile che semplifica il lavoro con documenti EPUB e HTML. Con la possibilità di convertire documenti EPUB in vari formati immagine e opzioni personalizzabili, offre un'ampia gamma di applicazioni per gli sviluppatori.

---

## Domande frequenti

### 1. Dove posso scaricare Aspose.HTML per .NET?

 È possibile scaricare Aspose.HTML per .NET dalla pagina delle versioni[Qui](https://releases.aspose.com/html/net/).

### 2. Come posso ottenere una licenza temporanea per Aspose.HTML per .NET?

 Per ottenere una licenza temporanea, visitare la pagina della licenza temporanea[Qui](https://purchase.aspose.com/temporary-license/).

### 3. Dove posso trovare ulteriore supporto per Aspose.HTML per .NET?

 Per qualsiasi domanda o problema, puoi chiedere assistenza alla comunità Aspose sul forum di supporto[Qui](https://forum.aspose.com/).

### 4. Posso convertire documenti EPUB in altri formati come PDF o XPS?

Sì, puoi utilizzare Aspose.HTML per .NET per convertire documenti EPUB in vari formati, inclusi PDF e XPS.

### 5. Aspose.HTML per .NET è adatto sia a progetti su piccola che su larga scala?

Assolutamente! Aspose.HTML per .NET è progettato per essere scalabile, rendendolo un'ottima scelta per progetti di tutte le dimensioni.
