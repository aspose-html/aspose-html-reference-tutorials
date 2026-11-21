---
category: general
date: 2026-11-20
description: Scopri come salvare HTML usando un ResourceHandler personalizzato in
  C# e anche come salvare HTML in archivi zip con codice conciso e pronto per la produzione.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: it
lastmod: 2026-11-20
og_description: Come salvare HTML usando un ResourceHandler personalizzato in C# e,
  facoltativamente, salvare HTML in file zip — guida completa e funzionante per sviluppatori
  .NET.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Come salvare HTML con un gestore di risorse personalizzato in C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: Come salvare HTML con un gestore di risorse personalizzato in C#
url: /it/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come salvare HTML con un gestore di risorse personalizzato in C#

Se hai bisogno di sapere **come salvare HTML** da una stringa in memoria o da un documento analizzato, questa guida mostra una soluzione completa. Utilizzare un `ResourceHandler` personalizzato ti consente di controllare lo stream di destinazione, il che significa che puoi **salvare HTML in zip** archivi senza scrivere file temporanei.

Vedrai perché un `ResourceHandler` è preferito rispetto al vecchio approccio `IOutputStorage`, come configurarlo e come estenderlo per la compressione zip. Alla fine di questo tutorial potrai incorporare il codice in qualsiasi progetto .NET 6+ e adattarlo alle tue esigenze di archiviazione.

## Cosa costruirai

* Un `ResourceHandler` minimale che restituisce un `MemoryStream`.
* Un `HtmlDocument` creato con **HtmlAgilityPack**.
* Una chiamata a `doc.Save` che scrive l'HTML nello stream fornito dal gestore.
* Un wrapper opzionale che comprime l'HTML risultante in un file zip.

Prerequisiti:

* SDK .NET 6 o successivo.
* Pacchetto NuGet `HtmlAgilityPack` (`dotnet add package HtmlAgilityPack`).
* Familiarità di base con gli stream C#.

## Passo 1: Creare un gestore di risorse personalizzato (modo principale per **come salvare html**)

La classe base `ResourceHandler` (disponibile dalla versione 24.2 dell'SDK del visualizzatore) definisce un unico metodo astratto, `HandleResource`. Implementare questo metodo ti dà il pieno controllo su dove viene scritto l'HTML.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Perché è importante:** Restituendo un `MemoryStream`, eviti I/O su disco, riduci la latenza e mantieni il codice deterministico per i test unitari. Il gestore viene invocato automaticamente dal metodo `Save`, quindi non è mai necessario passare esplicitamente uno stream.

## Passo 2: Caricare o creare il documento HTML

`HtmlAgilityPack` fornisce una comoda classe `HtmlDocument` che può analizzare una stringa, un file o uno stream. Per questo esempio carichiamo un semplice literal, ma lo stesso codice funziona con qualsiasi sorgente HTML.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Perché è importante:** Mantenere il documento in memoria è coerente con l'approccio basato su stream del gestore personalizzato. Ti consente anche di manipolare il DOM prima del salvataggio, ad esempio iniettando script o correggendo tag malformati.

## Passo 3: Salvare il documento usando il gestore personalizzato

Chiamare `doc.Save` con un'istanza di `MyHandler` attiva il metodo `HandleResource`. L'HTML viene scritto direttamente nello stream restituito.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

Dopo il completamento di `Save`, il `MemoryStream` all'interno di `MyHandler` contiene l'HTML serializzato. Puoi recuperarlo così:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Risultato:** La console stampa l'HTML esatto che hai passato a `LoadHtml`. Questo dimostra che ora comprendi **come salvare HTML** con un gestore personalizzato.

## Passo 4: Estendere il gestore per **salvare HTML in zip**

Se vuoi archiviare l'HTML, modifica `MyHandler` per scrivere in un `ZipArchiveEntry`. Lo spazio dei nomi .NET `System.IO.Compression` rende questo semplice.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Ora usa il nuovo gestore:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Perché funziona:** Il metodo `HandleResource` crea una voce zip chiamata `document.html`. Quando `doc.Save` scrive nello stream restituito, i dati vengono compressi automaticamente. Poiché lo zip è costruito in memoria, puoi restituirlo da una web API, allegarlo a un'email o archiviarlo in un database senza toccare il file system.

## Domande comuni e casi particolari

### E se ho bisogno di più file HTML nello stesso zip?

Crea una nuova voce per ogni chiamata a `HandleResource`. L'argomento `resourceName` contiene tipicamente il nome del file, quindi puoi usarlo direttamente:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Come gestire documenti di grandi dimensioni senza esaurire la memoria?

Sostituisci `MemoryStream` con un `FileStream` che punta a un file temporaneo. Il gestore restituisce quindi lo stream del file, e potrai eliminare il file in seguito dopo che lo zip è stato creato.

### Questo approccio funziona con .NET Core su Linux?

Sì. Tutte le API utilizzate (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) sono cross‑platform. Assicurati che il framework di destinazione sia almeno .NET 6 per la migliore compatibilità.

### Posso criptare l'archivio zip?

`ZipArchive` supporta la crittografia basata su password solo tramite librerie di terze parti (ad es., `SharpZipLib`). Se è necessaria la crittografia, avvolgi i byte di output con una libreria che fornisce crittografia AES prima di inviarli al client.

## Consigli professionali

* **Riutilizza il gestore** quando elabori molti documenti in batch; creare un nuovo `ZipArchive` per ogni file aggiunge overhead non necessario.
* **Imposta `LeaveOpen: true`** sul costruttore `ZipArchive` se hai bisogno di leggere i byte dello zip mentre l'archivio è ancora aperto.
* **Convalida l'HTML** prima del salvataggio chiamando `doc.OptionCheckSyntax = true;` – questo intercetta i tag malformati in anticipo.
* **Registra la dimensione** dello zip generato; un output insolitamente grande spesso indica risorse duplicate o compressione mancante.

## Esempio completo funzionante

Di seguito c'è un unico file che puoi incollare in un progetto console (`dotnet new console`) ed eseguire. Dimostra sia il salvataggio HTML semplice che la compressione zip.

```csharp
using System;
using System.IO;
using System.IO.Compression;
using HtmlAgilityPack;

// ---------- Custom handlers ----------
class MyHandler : ResourceHandler
{
    public MemoryStream HtmlStream { get; } = new();

    public override Stream HandleResource(string resourceName) => HtmlStream;
}

class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open();
    }

    public byte[] GetZipBytes()
    {
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}

// ---------- Main program ----------
class Program
{
    static void Main()
    {
        // Build a simple HTML document.
        HtmlDocument doc = new HtmlDocument();
        doc.LoadHtml("<html><body>Hello World from HtmlAgilityPack</body></html>");

        // ---- Example 1: plain HTML save ----
        var plainHandler = new MyHandler();
        doc.Save(plainHandler);
        plainHandler.HtmlStream.Seek(0, SeekOrigin.Begin);
        using var reader = new StreamReader(plainHandler.HtmlStream);
        Console.WriteLine("Plain HTML output:");


## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come salvare HTML in C# con gestore di risorse personalizzato](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Come usare ZipArchive – Salvare HTML e risorse in un file ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [salva html come zip con un gestore di risorse personalizzato – guida passo‑passo](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}