---
category: general
date: 2025-12-29
description: Come comprimere HTML in C# rapidamente usando Aspose.HTML – salva HTML
  in zip con un ZipResourceHandler personalizzato. Impara passo‑passo.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: it
og_description: Come comprimere HTML in zip in C# rapidamente usando Aspose.HTML.
  Segui questa guida per salvare HTML in zip e creare un archivio zip con gestione
  personalizzata delle risorse.
og_title: Come comprimere HTML in C# – Salva HTML in Zip
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: Come comprimere HTML in C# – Salvare HTML in un file zip
url: /it/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come comprimere HTML in C# – Salvare HTML in zip

Comprimere HTML in C# è una necessità comune quando vuoi impacchettare pagine web per l'uso offline. Che tu stia raggruppando una singola pagina con le sue immagini o esportando un intero sito, **salvare HTML in zip** mantiene tutto ordinato e portatile. In questo tutorial percorreremo una soluzione completa, pronta‑da‑eseguire, che non solo comprime il markup HTML ma trasmette anche ogni risorsa referenziata direttamente nell'archivio.

Imparerai a:

* Creare un archivio zip programmaticamente con `System.IO.Compression` di .NET.
* Inserire un `ResourceHandler` personalizzato in Aspose.HTML affinché le risorse fluiscano direttamente nel zip.
* Gestire casi particolari come file zip esistenti e asset binari di grandi dimensioni.

Nessun tool esterno richiesto—solo C#, Aspose.HTML e poche righe di codice.

## Di cosa avrai bisogno

Prima di immergerci, assicurati di avere:

* **.NET 6+** (il codice funziona anche su .NET Framework 4.6.2 e versioni successive).
* **Aspose.HTML for .NET** – puoi scaricare una prova gratuita dal sito di Aspose o usare una copia con licenza.
* Un ambiente di sviluppo (Visual Studio, VS Code, Rider—quello che preferisci).

Tutto qui. Nessun pacchetto NuGet aggiuntivo oltre a `System.IO.Compression` (incluso in .NET) e `Aspose.HTML`.

## Passo 1: Configurare il progetto e le importazioni

Crea un nuovo progetto console (o inserisci il codice in uno esistente). Aggiungi le direttive `using` richieste nella parte superiore del file:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Suggerimento:** Se usi Visual Studio, l'IDE suggerirà di aggiungere il pacchetto NuGet mancante per `Aspose.Html`. Accetta e sei pronto per partire.

## Passo 2: Implementare un ZipResourceHandler personalizzato

Aspose.HTML chiama un `ResourceHandler` ogni volta che deve scrivere una risorsa (come un'immagine, un file CSS o uno script). Sovrascrivendo `HandleResource`, possiamo decidere esattamente dove finisce ogni risorsa. Il gestore qui sotto crea una voce zip che rispecchia il percorso logico della risorsa, poi restituisce uno stream scrivibile che punta direttamente a quella voce.

```csharp
/// <summary>
/// Streams each HTML resource straight into a ZipArchive entry.
/// </summary>
class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;

    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        // Ensure the entry's directory structure exists inside the zip.
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        // The returned stream writes directly into the zip entry.
        return entry.Open();
    }
}
```

**Perché è importante:**  
Invece di scrivere le risorse in una cartella temporanea e poi comprimere la cartella, questo gestore trasmette i dati al volo, riducendo I/O su disco e mantenendo basso l'uso di memoria. Garantisce inoltre che la gerarchia interna del zip corrisponda ai percorsi relativi dell'HTML, come si aspetta il browser quando si decomprime e si apre la pagina.

## Passo 3: Preparare l'archivio zip

Ora apriremo (o creeremo) il file zip di destinazione. Il flag `FileMode.Create` sovrascrive eventuali file esistenti—perfetto per build ripetibili. Se preferisci preservare un archivio esistente, passa a `FileMode.OpenOrCreate` e gestisci le voci duplicate di conseguenza.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Caso particolare:** Se il processo si arresta prima che il blocco `using` rilasci l'archivio, potresti ritrovarti con un zip corrotto. Eseguire il codice all'interno di un `try/catch` e cancellare il file parzialmente creato in caso di errore è una semplice precauzione.

## Passo 4: Costruire il documento HTML con una risorsa incorporata

Per dimostrazione, creeremo una piccola pagina HTML che fa riferimento a un'immagine chiamata `image.png`. In uno scenario reale caricheresti l'HTML da un file o da una stringa proveniente da un database.

```csharp
// Sample HTML containing an <img> tag.
// Aspose.HTML will ask the ResourceHandler for "image.png".
string htmlContent = @"
<html>
<head><title>Sample Zip</title></head>
<body>
    <h1>Hello, zipped world!</h1>
    <img src='image.png' alt='Demo image'>
</body>
</html>";

// Create the document from the string.
var html = new HTMLDocument(htmlContent);
```

Se hai file immagine reali su disco, puoi aggiungerli manualmente al zip prima di salvare l'HTML, oppure lasciare che Aspose.HTML li recuperi tramite il gestore (ad esempio da un URL). Il gestore che abbiamo scritto funziona sia per percorsi locali sia per URL remoti.

## Passo 5: Configurare le opzioni di salvataggio per usare il ZipResourceHandler

Ora indichiamo ad Aspose.HTML di utilizzare il nostro gestore personalizzato quando scrive le risorse. La classe `HTMLSaveOptions` permette anche di specificare il nome del file di output all'interno del zip (per impostazione predefinita è `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Passo 6: Salvare il documento – Tutto fluisce nel zip

Infine, invochiamo `Save`. Aspose.HTML analizza il markup, individua il tag `<img>`, chiama `HandleResource` per `image.png` e scrive sia il file HTML sia l'immagine nello stesso archivio zip.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

Quando i blocchi `using` terminano, il `ZipArchive` finalizza il file, rendendolo pronto per la distribuzione.

### Esempio completo funzionante

Di seguito trovi l'intero programma assemblato. Copialo in `Program.cs` ed eseguilo—non servono ulteriori modifiche.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;

class ZipResourceHandler : ResourceHandler
{
    private readonly ZipArchive _zip;
    public ZipResourceHandler(ZipArchive zip) => _zip = zip;

    public override Stream HandleResource(ResourceInfo resourceInfo)
    {
        var entry = _zip.CreateEntry(resourceInfo.Path, CompressionLevel.Optimal);
        return entry.Open();
    }
}

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare the zip file.
        string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");
        Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);
        using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
        using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);

        // 2️⃣ Build a simple HTML document with an image reference.
        string htmlContent = @"
        <html>
        <head><title>Sample Zip</title></head>
        <body>
            <h1>Hello, zipped world!</h1>
            <img src='image.png' alt='Demo image'>
        </body>
        </html>";
        var html = new HTMLDocument(htmlContent);

        // 3️⃣ Set save options to stream resources into the zip.
        var saveOptions = new HTMLSaveOptions
        {
            OutputFileName = "index.html",
            OutputStorage = new ZipResourceHandler(zip)
        };

        // 4️⃣ Save – everything ends up in output.zip.
        html.Save(saveOptions);
        Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
    }
}
```

**Risultato atteso:** Dopo l'esecuzione, `output.zip` contiene due voci:

```
index.html
image.png
```

Se decomprimi il file e apri `index.html` in un browser, l'immagine viene visualizzata correttamente perché il percorso relativo è preservato.

## Domande frequenti

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}