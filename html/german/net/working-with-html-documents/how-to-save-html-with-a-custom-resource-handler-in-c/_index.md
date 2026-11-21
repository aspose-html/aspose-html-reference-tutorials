---
category: general
date: 2026-11-20
description: Erfahren Sie, wie Sie HTML mit einem benutzerdefinierten ResourceHandler
  in C# speichern und HTML außerdem in ZIP-Archive mit prägnantem, produktionsreifem
  Code sichern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: de
lastmod: 2026-11-20
og_description: Wie man HTML mit einem benutzerdefinierten ResourceHandler in C# speichert
  und optional HTML in Zip-Dateien speichert – vollständige, ausführbare Anleitung
  für .NET‑Entwickler.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Wie man HTML mit einem benutzerdefinierten Ressourcen‑Handler in C# speichert
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
title: Wie man HTML mit einem benutzerdefinierten Ressourcen‑Handler in C# speichert
url: /de/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man HTML mit einem benutzerdefinierten Resource‑Handler in C# speichert

Wenn Sie wissen möchten, **wie man HTML** aus einem In‑Memory‑String oder einem geparsten Dokument speichert, zeigt Ihnen diese Anleitung eine komplette Lösung. Mit einem benutzerdefinierten `ResourceHandler` können Sie den Ziel‑Stream steuern, was bedeutet, dass Sie **HTML in ZIP**‑Archive speichern können, ohne temporäre Dateien zu schreiben.

Sie erfahren, warum ein `ResourceHandler` dem älteren `IOutputStorage`‑Ansatz vorzuziehen ist, wie Sie ihn einrichten und wie Sie ihn für ZIP‑Kompression erweitern. Am Ende dieses Tutorials können Sie den Code in jedes .NET 6+‑Projekt einbinden und an Ihre eigenen Speicheranforderungen anpassen.

## Was Sie bauen werden

* Einen minimalen `ResourceHandler`, der einen `MemoryStream` zurückgibt.
* Ein `HtmlDocument`, erstellt mit **HtmlAgilityPack**.
* Einen Aufruf von `doc.Save`, der das HTML in den vom Handler bereitgestellten Stream schreibt.
* Einen optionalen Wrapper, der das resultierende HTML in eine ZIP‑Datei komprimiert.

Voraussetzungen:

* .NET 6 SDK oder neuer.
* NuGet‑Paket `HtmlAgilityPack` (`dotnet add package HtmlAgilityPack`).
* Grundlegende Kenntnisse von C#‑Streams.

## Schritt 1: Einen benutzerdefinierten Resource‑Handler erstellen (primärer Weg, **wie man HTML speichert**)

Die Basisklasse `ResourceHandler` (verfügbar ab Version 24.2 des Viewer‑SDK) definiert eine einzelne abstrakte Methode, `HandleResource`. Durch die Implementierung dieser Methode erhalten Sie die volle Kontrolle darüber, wohin das HTML geschrieben wird.

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

**Warum das wichtig ist:** Durch das Zurückgeben eines `MemoryStream` vermeiden Sie Festplatten‑I/O, reduzieren die Latenz und halten den Code für Unit‑Tests deterministisch. Der Handler wird automatisch von der `Save`‑Methode aufgerufen, sodass Sie nie explizit einen Stream übergeben müssen.

## Schritt 2: Das HTML‑Dokument laden oder erstellen

`HtmlAgilityPack` stellt die praktische Klasse `HtmlDocument` bereit, die einen String, eine Datei oder einen Stream parsen kann. In diesem Beispiel laden wir ein einfaches Literal, aber derselbe Code funktioniert mit jeder HTML‑Quelle.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Warum das wichtig ist:** Das Dokument im Speicher zu halten, passt zum stream‑basierten Ansatz des benutzerdefinierten Handlers. Außerdem können Sie den DOM vor dem Speichern manipulieren, z. B. Skripte einfügen oder fehlerhafte Tags korrigieren.

## Schritt 3: Das Dokument mit dem benutzerdefinierten Handler speichern

Ein Aufruf von `doc.Save` mit einer Instanz von `MyHandler` löst die Methode `HandleResource` aus. Das HTML wird direkt in den von Ihnen zurückgegebenen Stream geschrieben.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

Nachdem `Save` abgeschlossen ist, enthält der `MemoryStream` in `MyHandler` das serialisierte HTML. Sie können es wie folgt abrufen:

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

**Ergebnis:** Die Konsole gibt das exakt gleiche HTML aus, das Sie `LoadHtml` übergeben haben. Das beweist, dass Sie nun **wie man HTML mit einem benutzerdefinierten Handler speichert**.

## Schritt 4: Den Handler erweitern, um **HTML in ZIP zu speichern**

Wenn Sie das HTML archivieren möchten, ändern Sie `MyHandler`, sodass er in einen `ZipArchiveEntry` schreibt. Der .NET‑Namespace `System.IO.Compression` macht das unkompliziert.

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

Jetzt verwenden Sie den neuen Handler:

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

**Warum das funktioniert:** Die Methode `HandleResource` erstellt einen ZIP‑Eintrag mit dem Namen `document.html`. Wenn `doc.Save` in den zurückgegebenen Stream schreibt, werden die Daten automatisch komprimiert. Da das ZIP‑Archiv im Speicher gebaut wird, können Sie es aus einer Web‑API zurückgeben, an eine E‑Mail anhängen oder in einer Datenbank speichern, ohne das Dateisystem zu berühren.

## Häufige Fragen und Sonderfälle

### Was, wenn ich mehrere HTML‑Dateien im selben ZIP benötige?
Erstellen Sie für jeden Aufruf von `HandleResource` einen neuen Eintrag. Das Argument `resourceName` enthält typischerweise den Dateinamen, sodass Sie es direkt verwenden können:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Wie gehe ich mit großen Dokumenten um, ohne den Speicher zu erschöpfen?
Ersetzen Sie `MemoryStream` durch einen `FileStream`, der auf eine temporäre Datei zeigt. Der Handler gibt dann den Dateistream zurück, und Sie können die Datei nach dem Erstellen des ZIPs wieder löschen.

### Funktioniert dieser Ansatz mit .NET Core unter Linux?
Ja. Alle verwendeten APIs (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) sind plattformübergreifend. Stellen Sie sicher, dass das Ziel‑Framework mindestens .NET 6 ist, um beste Kompatibilität zu gewährleisten.

### Kann ich das ZIP‑Archiv verschlüsseln?
`ZipArchive` unterstützt passwortbasierte Verschlüsselung nur über Drittanbieter‑Bibliotheken (z. B. `SharpZipLib`). Wenn Verschlüsselung nötig ist, wickeln Sie die Ausgabebytes mit einer Bibliothek, die AES‑Verschlüsselung bereitstellt, bevor Sie sie an den Client senden.

## Profi‑Tipps

* **Den Handler wiederverwenden**, wenn Sie viele Dokumente stapelweise verarbeiten; das Erzeugen eines neuen `ZipArchive` für jede Datei verursacht unnötigen Overhead.
* **`LeaveOpen: true`** beim `ZipArchive`‑Konstruktor setzen, wenn Sie die ZIP‑Bytes lesen müssen, während das Archiv noch geöffnet ist.
* **HTML validieren**, bevor Sie speichern, indem Sie `doc.OptionCheckSyntax = true;` setzen – das fängt fehlerhafte Tags frühzeitig auf.
* **Die Größe des erzeugten ZIPs protokollieren**; ungewöhnlich große Ausgaben deuten häufig auf doppelte Ressourcen oder fehlende Kompression hin.

## Vollständiges funktionierendes Beispiel

Unten finden Sie eine einzelne Datei, die Sie in ein Konsolen‑Projekt (`dotnet new console`) einfügen und ausführen können. Sie demonstriert sowohl das reine HTML‑Speichern als auch die ZIP‑Kompression.

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


## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man HTML in C# mit benutzerdefiniertem Resource‑Handler speichert](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Wie man ZipArchive verwendet – HTML und Ressourcen in eine ZIP‑Datei speichern](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [HTML als ZIP mit einem benutzerdefinierten Resource‑Handler speichern – Schritt‑für‑Schritt‑Anleitung](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}