---
category: general
date: 2026-03-29
description: Scopri come utilizzare ZipArchive in C# per convertire HTML in ZIP, salvare
  HTML in ZIP e comprimere le immagini HTML—tutto in un unico tutorial chiaro.
draft: false
keywords:
- how to use ziparchive
- convert html to zip
- save html to zip
- create zip archive c#
- compress html images
language: it
og_description: Scopri come utilizzare ZipArchive in C# per convertire HTML in ZIP,
  salvare HTML in ZIP e comprimere le immagini HTML con un esempio completo e funzionante.
og_title: Come usare ZipArchive – Salva HTML e risorse in un file ZIP
tags:
- C#
- .NET
- Aspose.Html
- ZipArchive
title: Come utilizzare ZipArchive – Salva HTML e risorse in un file ZIP
url: /it/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare ZipArchive – Salvare HTML e risorse in un file ZIP

Ti sei mai chiesto **come usare ZipArchive** per raggruppare una pagina HTML insieme alle sue immagini, CSS e altri asset? Non sei solo. Molti sviluppatori si trovano in difficoltà quando devono distribuire un pacchetto HTML autonomo, soprattutto quando la pagina fa riferimento a risorse esterne. La buona notizia? Con poche righe di C# e Aspose.HTML puoi **convertire HTML in ZIP**, **salvare HTML in ZIP** e persino **comprimere le immagini HTML** senza uscire dal tuo IDE.

In questo tutorial percorreremo l’intero processo—dalla creazione di un semplice `HTMLDocument` alla gestione di ogni risorsa collegata tramite un `ResourceHandler` personalizzato. Alla fine avrai un file ZIP pronto all’uso che potrai inserire in qualsiasi server web o allegare a un’email. Nessuno script esterno, nessuna copia manuale—solo puro .NET.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- **.NET 6+** (o .NET Framework 4.6+). Le API utilizzate fanno parte di `System.IO.Compression`.
- **Aspose.HTML for .NET** installato (pacchetto NuGet `Aspose.Html`).
- Una conoscenza di base della sintassi C#.
- Un IDE come Visual Studio o VS Code.

Tutto qui. Nessun tool aggiuntivo, nessuna utility zip di terze parti. Pronto? Iniziamo.

## Passo 1: Configurare il progetto e aggiungere le dipendenze

Crea un nuovo progetto console:

```bash
dotnet new console -n HtmlToZipDemo
cd HtmlToZipDemo
dotnet add package Aspose.Html
```

Il pacchetto `Aspose.Html` ci fornisce la classe `HTMLDocument` e la classe base `ResourceHandler` che estenderemo più avanti. Lo spazio dei nomi integrato `System.IO.Compression` fornisce `ZipArchive` e `ZipArchiveEntry`.

> **Suggerimento:** Se punti a .NET 6, puoi usare le dichiarazioni top‑level per mantenere il metodo `Main` più pulito. Il codice qui sotto utilizza una classe `Program` classica per maggiore chiarezza.

## Passo 2: Creare un Resource Handler personalizzato

Quando Aspose.HTML salva un documento, richiede a un `ResourceHandler` di fornire uno `Stream` per ogni file esterno (immagini, CSS, font, ecc.). Sovrascrivendo `HandleResource` possiamo indirizzare ogni risorsa direttamente in una voce zip.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Writes each HTML resource (image, CSS, etc.) directly into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        // Ensure a folder hierarchy inside the zip (optional but tidy)
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open(); // Aspose streams the content into this entry.
    }
}
```

**Perché è importante:** Invece di scrivere le risorse su disco prima di comprimerle, il gestore le trasmette direttamente, riducendo il carico I/O e garantendo che lo zip rimanga sincronizzato con il contenuto HTML.

## Passo 3: Costruire il documento HTML

Per dimostrazione, includeremo un piccolo frammento HTML che fa riferimento a un’immagine esterna chiamata `logo.png`. In un progetto reale potresti caricare l’HTML da un file o da un database.

```csharp
// Create a simple HTML document with an external image reference.
HTMLDocument htmlDocument = new HTMLDocument(
    "<html><body><h1>Welcome!</h1><img src='logo.png' alt='Demo logo'></body></html>"
);
```

Se devi **comprimere le immagini HTML**, assicurati semplicemente che il file immagine si trovi accanto all’eseguibile (o incorporalo come risorsa). Il `ZipResourceHandler` aggiungerà automaticamente l’immagine all’archivio.

## Passo 4: Aprire (o creare) il file ZIP e salvare

Ora uniamo tutto. Apriamo un `FileStream` per lo zip di output, istanziamo `ZipArchive` in modalità *Update* e passiamo il nostro handler personalizzato a `HTMLDocument.Save`.

```csharp
using (var fileStream = new FileStream("output.zip", FileMode.Create))
using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
{
    // Initialise the handler with the open ZipArchive.
    var zipHandler = new ZipResourceHandler(zipArchive);

    // Save the HTML document; the handler writes HTML, images, CSS, etc. into the zip.
    htmlDocument.Save(zipHandler);
}
```

Quando i blocchi `using` terminano, lo zip viene finalizzato e chiuso automaticamente. Lo `output.zip` risultante contiene:

- `index.html` (il documento HTML serializzato)
- `logo.png` (l’immagine referenziata nell’HTML)

Puoi verificare il contenuto aprendo lo zip con qualsiasi gestore di file.

## Passo 5: Verificare il risultato (opzionale)

È sempre una buona idea ricontrollare che lo zip funzioni correttamente. Ecco un breve snippet che puoi eseguire dopo il codice precedente per elencare le voci:

```csharp
using (var zip = ZipFile.OpenRead("output.zip"))
{
    Console.WriteLine("Contents of output.zip:");
    foreach (var entry in zip.Entries)
        Console.WriteLine($"- {entry.FullName} ({entry.Length} bytes)");
}
```

Dovresti vedere qualcosa di simile:

```
Contents of output.zip:
- index.html (1234 bytes)
- logo.png (45678 bytes)
```

Apri `index.html` dalla cartella estratta e vedrai l’immagine visualizzata correttamente—la prova che **salvare HTML in ZIP** ha funzionato come previsto.

## Varianti comuni e casi limite

### 1. Usare un nome di voce diverso per il file HTML

Per impostazione predefinita Aspose scrive l’HTML in `index.html`. Se ti serve un nome personalizzato, puoi impostare `htmlDocument.FileName` prima di salvare:

```csharp
htmlDocument.FileName = "myPage.html";
htmlDocument.Save(zipHandler);
```

### 2. Aggiungere file aggiuntivi manualmente

A volte vuoi includere file extra (ad esempio un README). Puoi aggiungerli direttamente al `ZipArchive` prima di chiamare `htmlDocument.Save`:

```csharp
var readme = zipArchive.CreateEntry("README.txt", CompressionLevel.Optimal);
using (var writer = new StreamWriter(readme.Open()))
{
    writer.WriteLine("This ZIP contains an HTML page generated with Aspose.HTML.");
}
```

### 3. Gestire immagini di grandi dimensioni in modo efficiente

Se il tuo HTML fa riferimento a immagini molto grandi, considera di ridimensionarle in anticipo per mantenere ragionevole la dimensione dello zip. Il pacchetto `System.Drawing.Common` può aiutare:

```csharp
// Example: Resize logo.png to a max width of 800px before zipping.
using (var img = System.Drawing.Image.FromFile("logo.png"))
{
    int maxWidth = 800;
    if (img.Width > maxWidth)
    {
        var ratio = (double)maxWidth / img.Width;
        var newHeight = (int)(img.Height * ratio);
        using var thumb = img.GetThumbnailImage(maxWidth, newHeight, () => false, IntPtr.Zero);
        thumb.Save("logo_resized.png");
    }
}
```

Poi punta il `<img src='logo_resized.png'>` nel tuo HTML.

## Esempio completo, eseguibile

Di seguito trovi il programma completo che puoi copiare‑incollare in `Program.cs`. Compila ed esegui così com’è, a condizione di aver installato il pacchetto NuGet Aspose.HTML.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Custom handler that streams each resource into a zip entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(ZipArchive zipArchive) => _zipArchive = zipArchive;

    public override Stream HandleResource(string resourceName, ResourceType resourceType)
    {
        var entry = _zipArchive.CreateEntry(resourceName, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Create an HTML document that references an external image.
        HTMLDocument htmlDocument = new HTMLDocument(
            "<html><head><title>Demo</title></head>" +
            "<body><h2>Hello, ZipArchive!</h2>" +
            "<img src='logo.png' alt='Demo logo'></body></html>"
        );

        // 2️⃣ Open (or create) the output zip file.
        using (var fileStream = new FileStream("output.zip", FileMode.Create))
        using (var zipArchive = new ZipArchive(fileStream, ZipArchiveMode.Update))
        {
            // 3️⃣ Initialise the custom handler.
            var zipHandler = new ZipResourceHandler(zipArchive);

            // 4️⃣ Save the HTML; resources get streamed into the zip.
            htmlDocument.Save(zipHandler);
        }

        Console.WriteLine("✅ HTML document and its resources have been saved to output.zip");
    }
}
```

**Output previsto:** la console stampa un messaggio di successo e `output.zip` appare nella cartella del progetto contenente `index.html` e `logo.png`.

## Domande frequenti

- **Funziona su .NET Core?**  
  Sì. `System.IO.Compression.ZipArchive` fa parte di .NET Standard, quindi lo stesso codice gira su .NET 5, .NET 6 e .NET 7.

- **E se devo **comprimere le immagini HTML** in modo più aggressivo?**  
  Puoi pre‑processare le immagini (ridimensionare, cambiare formato in WebP, ecc.) prima di aggiungerle allo zip. L’handler si limita a trasmettere i dati che riceve.

- **Posso criptare lo zip?**  
  `ZipArchive` supporta la crittografia AES solo tramite librerie di terze parti (ad esempio `SharpZipLib`). Se ti serve la crittografia, crea lo zip con quella libreria e poi passa lo stream ad Aspose come `ResourceHandler` personalizzato.

- **C’è modo di impostare una cartella radice dentro lo zip?**  
  Sì—anteponi un nome di cartella a `resourceName` dentro `HandleResource`, ad esempio `var entry = _zipArchive.CreateEntry($"site/{resourceName}", ...)`.

## Conclusione

Ora sai **come usare ZipArchive** in C# per **convertire HTML in ZIP**, **salvare HTML in ZIP** e **comprimere le immagini HTML** in un unico flusso di lavoro pulito. Estendendo `ResourceHandler` abbiamo evitato file temporanei e mantenuto il processo efficiente in termini di memoria. Il modello scala bene: basta posare lo zip generato su un server web, allegarlo a un’email o archiviarlo nel cloud.

Passi successivi che potresti esplorare:

- **Creare archivi ZIP programmaticamente** per intere cartelle di siti web (`create zip archive c#`).
- **Aggiungere conversioni PDF o DOCX** prima di comprimere per pacchetti di documentazione più ricchi.
- **Integrare con ASP.NET Core** per trasmettere lo zip direttamente al browser client (`FileStreamResult`).

Hai altre domande su come comprimere HTML, gestire i font o ottimizzare le dimensioni delle immagini? Lascia un commento o scrivimi su Stack Overflow. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}