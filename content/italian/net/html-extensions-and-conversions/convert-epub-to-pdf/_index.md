---
title: Converti EPUB in PDF in .NET con Aspose.HTML
linktitle: Converti EPUB in PDF in .NET
second_title: Aspose.HTML .NET API di manipolazione HTML
description: Scopri come convertire EPUB in PDF utilizzando Aspose.HTML per .NET. Questa guida passo passo copre le opzioni di personalizzazione, le domande frequenti e altro ancora per una conversione fluida dei documenti.
type: docs
weight: 12
url: /it/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

In questo tutorial esploreremo come utilizzare Aspose.HTML per .NET per convertire file EPUB in PDF. Aspose.HTML è una potente libreria .NET che fornisce varie funzionalità per lavorare con documenti HTML ed EPUB. Tratteremo i prerequisiti, importeremo gli spazi dei nomi necessari e analizzeremo più esempi, spiegando ogni passaggio in dettaglio.

## Prerequisiti

Prima di iniziare, assicurati di disporre dei seguenti prerequisiti:

1. Aspose.HTML per .NET: assicurati di avere Aspose.HTML per .NET installato nel tuo progetto .NET. Puoi scaricarlo da[Qui](https://releases.aspose.com/html/net/).

2. La tua directory di dati: avrai bisogno di una directory di dati in cui sono archiviati i tuoi file EPUB.

Ora, tuffiamoci nel processo passo passo di conversione da EPUB a PDF utilizzando Aspose.HTML per .NET.

## Converti EPUB in PDF

### Passaggio 1: inizializza il tuo progetto

Assicurati di avere un progetto .NET configurato e che Aspose.HTML per .NET sia installato.

### Passaggio 2: importa gli spazi dei nomi richiesti

Nel file di codice C#, importa gli spazi dei nomi necessari:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Passaggio 3: apri il file EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continua al passaggio successivo...
}
```

-  Sostituire`"Your Data Directory"` con la directory effettiva in cui si trova il file EPUB.
- Questo codice apre il file EPUB per la lettura.

### Passaggio 4: imposta le opzioni PDF ed esegui la conversione

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Crea un'istanza di`PdfSaveOptions` per specificare le impostazioni di conversione PDF.
-  Usa il`Converter.ConvertEPUB` metodo per convertire l'EPUB in PDF con le opzioni fornite.
- Salva il PDF risultante come "output.pdf".

## Specificare le opzioni di salvataggio del PDF

### Passaggio 1: inizializza il tuo progetto

Assicurati di avere un progetto .NET configurato e Aspose.HTML per .NET installato.

### Passaggio 2: importa gli spazi dei nomi richiesti

Importa gli spazi dei nomi necessari nel tuo codice C#:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Passaggio 3: apri il file EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continua al passaggio successivo...
}
```

-  Sostituire`"Your Data Directory"` con la directory effettiva del tuo file EPUB.
- Apri il file EPUB per la lettura.

### Passaggio 4: personalizza le opzioni PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Crea un'istanza di`PdfSaveOptions` e personalizzalo secondo le tue esigenze.
- In questo esempio, impostiamo la dimensione della pagina su 3000 pixel di larghezza e 1000 pixel di altezza e il colore di sfondo su Alice Blue.

### Passaggio 5: eseguire la conversione

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Usa il`Converter.ConvertEPUB` metodo per convertire EPUB in PDF con le opzioni personalizzate.
- Salva il PDF risultante come "output.pdf".

## Utilizza provider di streaming personalizzato

### Passaggio 1: inizializza il tuo progetto

Configura un progetto .NET e installa Aspose.HTML per .NET.

### Passaggio 2: importa gli spazi dei nomi richiesti

Nel codice C# importa gli spazi dei nomi necessari:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Passaggio 3: apri il file EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Continua al passaggio successivo...
}
```

-  Sostituire`"Your Data Directory"` con la directory effettiva del tuo file EPUB.
- Apri il file EPUB per la lettura.

### Passaggio 4: utilizzare un provider di streaming personalizzato

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Continua al passaggio successivo...
}
```

-  Creare un`MemoryStreamProvider` per gestire il risultato della conversione come flusso di memoria.
-  Usa il`Converter.ConvertEPUB` metodo con il provider di streaming personalizzato.

### Passaggio 5: salva il risultato

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Accedi al flusso di memoria contenente i dati convertiti.
- Imposta la posizione del flusso all'inizio.
- Crea un file PDF di output e copia il contenuto dal flusso di memoria su di esso.

### Codice sorgente della classe MemoryStreamProvider. 

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
Ora hai imparato come convertire file EPUB in PDF utilizzando Aspose.HTML per .NET con varie opzioni e possibilità di personalizzazione. Aspose.HTML semplifica il processo, fornendo flessibilità e controllo sulla conversione del documento.

## Conclusione

Aspose.HTML per .NET è uno strumento versatile per convertire file EPUB in PDF, offrendo opzioni di personalizzazione per adattare il documento PDF risultante alle tue esigenze. Se hai bisogno di conversioni semplici o di personalizzazione avanzata, Aspose.HTML ti copre.

 Se non lo hai già fatto, puoi scaricare Aspose.HTML per .NET da[sito web](https://releases.aspose.com/html/net/) e inizia a utilizzarlo nelle tue applicazioni .NET oggi stesso.

---

## Domande frequenti

### Aspose.HTML per .NET è gratuito?
    Aspose.HTML per .NET è un prodotto commerciale, ma è disponibile una prova gratuita[Qui](https://releases.aspose.com/).

### Posso personalizzare l'aspetto del PDF convertito?
   Sì, puoi personalizzare l'aspetto del PDF regolando opzioni come la dimensione della pagina e il colore dello sfondo, come mostrato nell'esempio 2.

### Come posso ottenere supporto per Aspose.HTML per .NET?
    Puoi trovare supporto e risorse su[Forum Aspose.HTML](https://forum.aspose.com/).

### Ci sono altri formati che posso convertire con Aspose.HTML per .NET?
   Sì, Aspose.HTML per .NET supporta vari formati di documenti, inclusi HTML, EPUB e altri.

### Aspose.HTML per ..NET è adatto per la conversione di documenti su larga scala?
   Aspose.HTML per .NET è progettato per gestire in modo efficiente conversioni di documenti su larga scala, rendendolo adatto a un'ampia gamma di applicazioni.

