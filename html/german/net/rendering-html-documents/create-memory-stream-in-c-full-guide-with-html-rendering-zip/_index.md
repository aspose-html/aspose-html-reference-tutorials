---
category: general
date: 2026-03-31
description: Erstelle einen MemoryStream in C# und lerne, HTML in PNG zu rendern,
  einen benutzerdefinierten Ressourcen‑Handler zu verwenden, HTML in ein ZIP zu speichern
  und die Schriftart programmgesteuert festzulegen – alles in einem Tutorial.
draft: false
keywords:
- create memory stream
- render html to png
- custom resource handler
- save html to zip
- set font style programmatically
language: de
og_description: Erstelle einen Memory‑Stream in C# und rendere HTML sofort zu PNG,
  verwende benutzerdefinierte Ressourcen‑Handler, speichere HTML in ein ZIP‑Archiv
  und setze den Schriftstil programmgesteuert.
og_title: Memory Stream in C# erstellen – Vollständiger Programmierleitfaden
tags:
- C#
- HTML rendering
- Streams
- ZIP archives
- Image processing
title: Memory-Stream in C# erstellen – Vollständige Anleitung mit HTML-Rendering und
  ZIP-Export
url: /de/net/rendering-html-documents/create-memory-stream-in-c-full-guide-with-html-rendering-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memory Stream in C# erstellen – Vollständiger Leitfaden mit HTML-Rendering & ZIP-Export

Haben Sie sich jemals gefragt, wie man **Memory Stream erstellen** in C# und dann ein HTML‑Dokument in ein PNG‑Bild, eine ZIP‑Datei umwandelt oder sogar die Schriftart zur Laufzeit ändert? Sie sind nicht allein. Viele Entwickler stoßen an Grenzen, wenn sie eine In‑Memory‑Darstellung eines Dokuments benötigen, aber das Dateisystem nicht berühren wollen.

In diesem Tutorial führen wir Sie durch eine vollständige End‑to‑End‑Lösung: Wir bauen einen benutzerdefinierten Resource‑Handler, leiten HTML in einen `MemoryStream`, zippen dasselbe Dokument und rendern es schließlich zu einem Bild mit Antialiasing. Am Ende können Sie **HTML zu PNG rendern**, **HTML zu ZIP speichern** und **Schriftstil programmgesteuert setzen**, ohne jemals temporäre Dateien auf die Festplatte zu schreiben.

## Voraussetzungen

- .NET 6.0 oder höher (die API-Oberfläche ist über aktuelle Versionen hinweg stabil).  
- Ein Verweis auf eine HTML‑zu‑Image‑Bibliothek, die `HTMLDocument`, `ImageRenderer` und verwandte Typen bereitstellt – zum Beispiel **HtmlRenderer.Core** (ersetzen Sie dies durch das tatsächlich von Ihnen genutzte Paket).  
- Grundlegende Vertrautheit mit Streams, `using`‑Anweisungen und C#‑objektorientierten Mustern.

> **Pro Tipp:** Wenn Sie Visual Studio verwenden, aktivieren Sie **nullable reference types** (`<Nullable>enable</Nullable>`), um subtile Fehler frühzeitig zu erkennen.

## Schritt 1: Erstellen eines Memory Streams mit einem benutzerdefinierten Resource Handler

Das erste, was wir benötigen, ist ein Handler, der der HTML‑Engine sagt, *wo* jede Ressource (Bilder, CSS usw.) geschrieben werden soll. Durch das Erben von `ResourceHandler` können wir jede Ausgabe in einen einzigen `MemoryStream` leiten.

```csharp
using System;
using System.IO;

// Step 1: Define a handler that writes resources to an in‑memory stream
class MemoryResourceHandler : ResourceHandler
{
    // The stream lives for the whole lifetime of the handler
    public MemoryStream OutputStream = new MemoryStream();

    // The engine calls this for every resource it needs to write
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}
```

**Warum das wichtig ist:**  
Ein `MemoryStream` existiert vollständig im RAM, das bedeutet kein Festplatten‑I/O, was perfekt für Hochleistungs‑Szenarien wie Web‑Services oder Unit‑Tests ist. Der Handler hält zudem die API zufrieden, da die Engine für jede Ressource einen `Stream` erwartet.

## Schritt 2: Laden des HTML‑Dokuments und Speichern in den Memory Stream

Jetzt laden wir eine vorhandene HTML‑Datei (oder einen String) und weisen sie an, unseren `MemoryResourceHandler` zu verwenden. Nach dem Aufruf von `Save` enthält `OutputStream` die vollständige HTML‑Nutzlast.

```csharp
using System.IO;

// Assume the HTML file lives under YOUR_DIRECTORY
HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

// Instantiate the memory handler
MemoryResourceHandler memoryHandler = new MemoryResourceHandler();

// Save the document – all resources flow into the same MemoryStream
htmlDoc.Save(memoryHandler);
```

An diesem Punkt befindet sich die Position des Streams am Ende, daher müssen wir ihn zurückspulen, bevor wir den Inhalt lesen können.

```csharp
// Reset the stream position to the beginning
memoryHandler.OutputStream.Position = 0;

// Quick verification (optional)
// string htmlContent = new StreamReader(memoryHandler.OutputStream).ReadToEnd();
// Console.WriteLine(htmlContent);
```

**Hinweis:** Die obige `ReadToEnd`‑Zeile ist auskommentiert, weil Sie in einem Produktionsszenario den Stream wahrscheinlich an eine andere Komponente weitergeben würden, anstatt ihn auszugeben.

## Schritt 3: Zippen des gleichen HTMLs mit einem benutzerdefinierten ZIP‑Resource‑Handler

Manchmal müssen Sie das HTML zusammen mit seinen Ressourcen ausliefern. Ein zweiter benutzerdefinierter Handler kann für jede Ressource on the fly einen ZIP‑Eintrag erstellen.

```csharp
using System.IO.Compression;

// Step 4: Define a handler that writes each resource into a ZIP archive
class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;

    public ZipResourceHandler(string zipPath)
    {
        // Open (or create) the archive in write mode
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);
    }

    // The engine calls this for each resource; we create a ZIP entry with the same name
    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    // Proper disposal of the underlying ZipArchive
    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}
```

Jetzt verwenden wir dieselbe `htmlDoc`‑Instanz erneut und schreiben sie in eine ZIP‑Datei.

```csharp
// Step 5: Save the HTML document into a ZIP file
using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
{
    htmlDoc.Save(zipHandler);
}
```

**Hinweis für Sonderfälle:** Wenn das HTML dasselbe Bild mehrfach referenziert, wird der ZIP‑Handler doppelte Einträge erzeugen. Um das zu vermeiden, könnten Sie ein `HashSet<string>` mit bereits hinzugefügten Namen führen und stattdessen den Stream des bestehenden Eintrags zurückgeben.

## Schritt 4: Programmgesteuertes Setzen des Schriftstils im Standard‑Stylesheet

Das Aussehen des Dokuments zu ändern, ohne das Quell‑HTML zu berühren, ist oft praktisch – zum Beispiel beim Erzeugen einer PDF‑Vorschau mit einer fetten Überschrift. Die Bibliothek stellt ein `DefaultViewStyleSheet` bereit, das Sie anpassen können.

```csharp
// Step 6: Apply bold and italic styling to the default view stylesheet
htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

Sie können beliebige Flags aus `WebFontStyle` kombinieren. Die Änderung ist sofort wirksam und beeinflusst nachfolgende Render‑ oder Speicher‑Vorgänge.

## Schritt 5: Rendern des HTML‑Dokuments zu einem PNG‑Bild

Zum Schluss wandeln wir das HTML in ein Rasterbild um. Durch Aktivieren von Antialiasing und Hinting erhalten wir scharfen Text und glatte Kanten.

```csharp
using System.Drawing; // For ImageRenderingOptions if needed

// Step 7: Render the document to an image with antialiasing and hinting
var renderingOptions = new ImageRenderingOptions
{
    UseAntialiasing = true,
    UseHinting = true
};

new ImageRenderer(renderingOptions).Render(htmlDoc, "YOUR_DIRECTORY/out.png");
```

**Was Sie sehen werden:** Eine PNG‑Datei namens `out.png` im Verzeichnis `YOUR_DIRECTORY`, die exakt so aussieht, wie der Browser das HTML rendern würde, jedoch mit dem zuvor gesetzten fett‑kursiven Stil.

![Screenshot der Memory Stream-Erstellung](placeholder-image.png "Beispiel für Memory Stream-Erstellung")

*Der Alt‑Text des Bildes enthält das Haupt‑Keyword, um SEO zu erfüllen.*

## Häufige Fragen & Stolperfallen

| Frage | Antwort |
|----------|--------|
| **Kann ich dasselbe `HTMLDocument` nach dem Speichern in ein ZIP wiederverwenden?** | Ja. Das Dokumentobjekt bleibt im Speicher; Sie können `Save` mehrfach mit unterschiedlichen Handlern aufrufen. |
| **Was ist, wenn das HTML große Binär‑Assets enthält?** | Der `MemoryStream` wächst entsprechend. Bei sehr großen Dateien sollten Sie in Erwägung ziehen, direkt in eine Datei zu streamen oder einen `BufferedStream` zu verwenden. |
| **Muss ich `Dispose` auf `MemoryResourceHandler` aufrufen?** | Nicht zwingend erforderlich, da er nur einen `MemoryStream` hält, der beim Garbage‑Collect des Handlers freigegeben wird. Dennoch ist das Aufrufen von `Dispose` eine gute Gewohnheit. |
| **Wie ändere ich das Bildformat (z. B. JPEG anstelle von PNG)?** | Übergeben Sie eine andere Dateierweiterung an `ImageRenderer.Render` oder verwenden Sie `ImageRenderer.RenderToBitmap` und speichern Sie anschließend mit `bitmap.Save("out.jpg", ImageFormat.Jpeg)`. |
| **Ist der ZIP‑Handler thread‑sicher?** | Nein. `ZipArchive` ist nicht thread‑sicher, daher sollten Sie den Zugriff serialisieren oder für jeden Thread einen separaten Handler erstellen. |

## Vollständiges funktionierendes Beispiel

Unten finden Sie ein einzelnes, sofort kopier‑und‑einfügbares Programm, das jeden besprochenen Schritt demonstriert. Ersetzen Sie `YOUR_DIRECTORY` durch einen echten Pfad auf Ihrem Rechner.

```csharp
// FullExample.cs
using System;
using System.IO;
using System.IO.Compression;

// Assume these types come from your HTML rendering library
using HtmlRendering; // placeholder namespace

class MemoryResourceHandler : ResourceHandler
{
    public MemoryStream OutputStream = new MemoryStream();
    public override Stream HandleResource(ResourceInfo info) => OutputStream;
}

class ZipResourceHandler : ResourceHandler, IDisposable
{
    private readonly ZipArchive _zipArchive;
    public ZipResourceHandler(string zipPath) =>
        _zipArchive = ZipFile.Open(zipPath, ZipArchiveMode.Create);

    public override Stream HandleResource(ResourceInfo info) =>
        _zipArchive.CreateEntry(info.Name).Open();

    protected override void Dispose(bool disposing)
    {
        if (disposing) _zipArchive.Dispose();
        base.Dispose(disposing);
    }

    public void Dispose() => Dispose(true);
}

class Program
{
    static void Main()
    {
        // 1️⃣ Load HTML
        var htmlDoc = new HTMLDocument("YOUR_DIRECTORY/sample.html");

        // 2️⃣ Write to a memory stream
        var memHandler = new MemoryResourceHandler();
        htmlDoc.Save(memHandler);
        memHandler.OutputStream.Position = 0;
        // Optional: verify content
        // Console.WriteLine(new StreamReader(memHandler.OutputStream).ReadToEnd());

        // 3️⃣ Zip the same document
        using (var zipHandler = new ZipResourceHandler("YOUR_DIRECTORY/output.zip"))
        {
            htmlDoc.Save(zipHandler);
        }

        // 4️⃣ Change font style programmatically
        htmlDoc.DefaultViewStyleSheet.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 5️⃣ Render to PNG with antialiasing & hinting
        var renderOpts = new ImageRenderingOptions
        {
            UseAntialiasing = true,
            UseHinting = true
        };
        new ImageRenderer(renderOpts).Render(htmlDoc, "YOUR_DIRECTORY/out.png");

        Console.WriteLine("All operations completed successfully.");
    }
}
```

Wenn Sie dieses Programm ausführen, erhalten Sie drei Artefakte:

1. **In‑memory HTML** gespeichert in `memHandler.OutputStream`.  
2. **`output.zip`** enthält das HTML und alle verknüpften Ressourcen.  
3. **`out.png`** – ein gerendertes Bild, das den fett‑kursiven Stil berücksichtigt.

## Fazit

Wir haben gezeigt, wie man **Memory Stream** in C# erstellt und nahtlos mit HTML‑Rendering, ZIP‑Archivierung und Bildgenerierung integriert. Die zentrale Erkenntnis ist, dass ein einzelnes `HTMLDocument` auf mehrere Arten gespeichert werden kann – in einen `MemoryStream`, ein ZIP‑Archiv oder eine PNG‑Datei – einfach durch Austausch des `ResourceHandler`.

Wenn Sie bereit sind, weiterzugehen, probieren Sie:

- **Rendern zu PDF** mit einem PDF‑Renderer, der einen `Stream` akzeptiert.  
- **Komprimieren des Memory Streams** vor dem Senden über ein Netzwerk (z. B. `GZipStream`).  
- **Mehrere HTML‑Seiten kombinieren** zu einem ZIP für den Massenausexport.

Fühlen Sie sich frei zu experimentieren und zögern Sie nicht, einen Kommentar zu hinterlassen, falls Sie auf ein Problem stoßen. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}