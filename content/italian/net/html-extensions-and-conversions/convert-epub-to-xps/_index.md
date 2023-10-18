---
title: Converti EPUB in XPS in .NET con Aspose.HTML
linktitle: Converti EPUB in XPS in .NET
second_title: Aspose.HTML .NET API di manipolazione HTML
description: Scopri come convertire EPUB in XPS in .NET utilizzando Aspose.HTML per .NET. Segui la nostra guida passo passo per conversioni senza sforzo.
type: docs
weight: 13
url: /it/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Stai cercando un modo semplice per convertire i file EPUB in formato XPS nelle tue applicazioni .NET? Aspose.HTML per .NET fornisce una potente soluzione per raggiungere questo obiettivo senza sforzo. In questa guida passo passo ti guideremo attraverso il processo di conversione da EPUB a XPS utilizzando Aspose.HTML. Iniziamo!

## Prerequisiti

Prima di immergerti nel processo di conversione da EPUB a XPS, dovrai assicurarti di disporre dei seguenti prerequisiti:

### 1. Aspose.HTML per la libreria .NET

 Assicurati di avere la libreria Aspose.HTML per .NET installata nel tuo progetto. Se non lo hai fatto, puoi ottenerlo da[Pagina di download di Aspose.HTML per .NET](https://releases.aspose.com/html/net/).

### 2. Inserisci il file EPUB

Avrai bisogno di un file EPUB che desideri convertire in XPS. Assicurati di avere un file EPUB disponibile per la conversione.

### 3. Ambiente di sviluppo .NET

Questa guida presuppone che tu abbia un ambiente di sviluppo .NET funzionante configurato sul tuo computer.

## Importa spazio dei nomi

Per iniziare, dovresti importare lo spazio dei nomi necessario per Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Converti EPUB in XPS

Analizziamo il processo di conversione di un file EPUB nel formato XPS in più passaggi.

### Passaggio 1.1: apri il file EPUB

Innanzitutto, apri il file EPUB esistente per la lettura utilizzando FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continuare con il processo di conversione
}
```

### Passaggio 1.2: creare XpsSaveOptions

Crea un'istanza di XpsSaveOptions. Questo passaggio è fondamentale per configurare l'output XPS:

```csharp
var options = new XpsSaveOptions();
```

### Passaggio 1.3: converti EPUB in XPS

Ora chiamiamo il metodo ConvertEPUB per convertire l'EPUB in XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Specificare le opzioni XPS personalizzate

È possibile personalizzare ulteriormente l'output XPS specificando opzioni personalizzate come le dimensioni della pagina e il colore dello sfondo.

### Passaggio 2.1: dimensioni della pagina personalizzate e colore di sfondo

Crea un'istanza di XpsSaveOptions con dimensioni di pagina e colore di sfondo personalizzati:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Passaggio 2.2: converti EPUB in XPS con opzioni personalizzate

Ora chiama il metodo ConvertEPUB per convertire l'EPUB in XPS con le opzioni personalizzate:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Utilizza provider di streaming personalizzato

In questo passaggio, convertiremo EPUB in XPS utilizzando un provider di streaming personalizzato, consentendoti di manipolare i dati risultanti.

### Passaggio 3.1: creare un MemoryStreamProvider

Crea un'istanza di MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Continuare con il processo di conversione
}
```

### Passaggio 3.2: converti EPUB in XPS con Stream Provider

Converti EPUB in XPS utilizzando MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Passaggio 3.3: accesso e salvataggio dei risultati

Recupera il flusso di memoria contenente i dati convertiti e salvalo in un file di output:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Codice sorgente della classe MemoryStreamProvider

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
Congratulazioni! Hai convertito con successo un file EPUB in formato XPS utilizzando Aspose.HTML per .NET.

## Conclusione

In questo tutorial completo, abbiamo esplorato come sfruttare Aspose.HTML per .NET per convertire file EPUB in formato XPS con varie opzioni di personalizzazione. Che tu sia uno sviluppatore esperto o che tu abbia appena iniziato, Aspose.HTML semplifica il processo, permettendoti di gestire facilmente le conversioni da EPUB a XPS.

 Hai domande o hai riscontrato problemi? Dai un'occhiata a[Documentazione Aspose.HTML](https://reference.aspose.com/html/net/) per ulteriori approfondimenti o chiedere aiuto al[Forum della comunità Aspose.HTML](https://forum.aspose.com/).

## Domande frequenti

### Cos'è Aspose.HTML per .NET?
Aspose.HTML per .NET è una potente libreria che consente agli sviluppatori di lavorare con documenti HTML, EPUB e XPS nelle applicazioni .NET.

### Dove posso scaricare Aspose.HTML per .NET?
 È possibile scaricare Aspose.HTML per .NET da[pagina di download](https://releases.aspose.com/html/net/).

### È disponibile una prova gratuita per Aspose.HTML per .NET?
 Sì, puoi ottenere una prova gratuita da[Qui](https://releases.aspose.com/).

### Come posso ottenere una licenza temporanea per Aspose.HTML per .NET?
 Per ottenere una licenza temporanea, visitare il[pagina della licenza temporanea](https://purchase.aspose.com/temporary-license/).

### Dove posso trovare ulteriori tutorial e documentazione per Aspose.HTML per .NET?
 Esplora un'ampia gamma di tutorial e documentazione dettagliata su[Documentazione Aspose.HTML](https://reference.aspose.com/html/net/) pagina.