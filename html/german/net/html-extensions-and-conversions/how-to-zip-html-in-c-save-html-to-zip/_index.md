---
category: general
date: 2025-12-29
description: Wie man HTML in C# schnell mit Aspose.HTML zippt – HTML in ein Zip‑Archiv
  mit einem benutzerdefinierten ZipResourceHandler speichern. Schritt für Schritt
  lernen.
draft: false
keywords:
- how to zip html
- save html to zip
- create zip archive c#
- Aspose HTML zip
- C# resource handling
language: de
og_description: Wie man HTML in C# schnell mit Aspose.HTML zippt. Folgen Sie dieser
  Anleitung, um HTML in ein Zip zu speichern und ein Zip‑Archiv mit benutzerdefinierter
  Ressourcenverwaltung zu erstellen.
og_title: Wie man HTML in C# zippt – HTML in ein Zip‑Archiv speichern
tags:
- C#
- Aspose.HTML
- ZipArchive
- File I/O
title: HTML in C# zippen – HTML in ein Zip‑Archiv speichern
url: /de/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man HTML in C# zippt – HTML in ein Zip speichern

HTML in C# zu zippen ist ein häufiges Bedürfnis, wenn Sie Webseiten für die Offline‑Nutzung paketieren möchten. Egal, ob Sie eine einzelne Seite mit ihren Bildern bündeln oder eine komplette Site exportieren, **HTML in ein Zip speichern** hält alles ordentlich und portabel. In diesem Tutorial führen wir Sie durch eine vollständige, sofort lauffähige Lösung, die nicht nur das HTML‑Markup zippt, sondern auch jede referenzierte Ressource direkt in das Archiv streamt.

Sie lernen, wie man:

* Ein ZIP‑Archiv programmgesteuert mit .NETs `System.IO.Compression` erstellt.
* Einen benutzerdefinierten `ResourceHandler` in Aspose.HTML einbindet, sodass Ressourcen direkt in das ZIP fließen.
* Randfälle wie vorhandene ZIP‑Dateien und große Binär‑Assets behandelt.

Keine externen Tools erforderlich – nur C#, Aspose.HTML und ein paar Code‑Zeilen.

## Was Sie benötigen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* **.NET 6+** (der Code funktioniert auch mit .NET Framework 4.6.2 und höher).
* **Aspose.HTML für .NET** – Sie können eine kostenlose Testversion von der Aspose‑Website herunterladen oder eine lizenzierte Kopie verwenden.
* Eine Entwicklungsumgebung (Visual Studio, VS Code, Rider – ganz wie Sie möchten).

Das war’s. Keine zusätzlichen NuGet‑Pakete außer `System.IO.Compression` (in .NET enthalten) und `Aspose.HTML`.

## Schritt 1: Projekt einrichten und Imports

Erstellen Sie ein neues Konsolenprojekt (oder fügen Sie den Code in ein bestehendes ein). Fügen Sie die erforderlichen `using`‑Direktiven am Anfang Ihrer Datei hinzu:

```csharp
using System;
using System.IO;
using System.IO.Compression;
using Aspose.Html;
using Aspose.Html.Saving;
```

> **Pro‑Tipp:** Wenn Sie Visual Studio verwenden, schlägt die IDE vor, das fehlende NuGet‑Paket für `Aspose.Html` hinzuzufügen. Akzeptieren Sie es, und Sie können loslegen.

## Schritt 2: Einen benutzerdefinierten ZipResourceHandler implementieren

Aspose.HTML ruft einen `ResourceHandler` auf, wann immer es eine Ressource (wie ein Bild, eine CSS‑Datei oder ein Skript) schreiben muss. Durch Überschreiben von `HandleResource` können wir genau bestimmen, wohin jede Ressource gelangt. Der untenstehende Handler erstellt einen ZIP‑Eintrag, der den logischen Pfad der Ressource widerspiegelt, und gibt dann einen beschreibbaren Stream zurück, der direkt auf diesen Eintrag zeigt.

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

**Warum das wichtig ist:**  
Anstatt Ressourcen in einen temporären Ordner zu schreiben und anschließend den Ordner zu zippen, streamt dieser Handler Daten on‑the‑fly, spart Festplatten‑I/O und hält den Speicherverbrauch niedrig. Außerdem stellt er sicher, dass die interne Ordnerhierarchie des ZIPs den relativen Pfaden des HTML entspricht, was Browser beim Entpacken und Öffnen der Seite erwarten.

## Schritt 3: Das ZIP‑Archiv vorbereiten

Jetzt öffnen (oder erstellen) wir die Ziel‑ZIP‑Datei. Das Flag `FileMode.Create` überschreibt jede vorhandene Datei – ideal für wiederholbare Builds. Wenn Sie ein bestehendes Archiv erhalten möchten, wechseln Sie zu `FileMode.OpenOrCreate` und behandeln Sie doppelte Einträge entsprechend.

```csharp
string zipPath = Path.Combine(Environment.CurrentDirectory, "output.zip");

// Ensure the directory exists (useful if you run the code from a nested folder)
Directory.CreateDirectory(Path.GetDirectoryName(zipPath)!);

using var zipStream = new FileStream(zipPath, FileMode.Create, FileAccess.ReadWrite);
using var zip = new ZipArchive(zipStream, ZipArchiveMode.Create, leaveOpen: false);
```

> **Randfall:** Wenn der Prozess abstürzt, bevor der `using`‑Block das Archiv freigibt, kann ein beschädigtes ZIP entstehen. Das Ausführen des Codes innerhalb eines try/catch und das Löschen der teilweise erstellten Datei bei einem Fehler ist ein einfacher Schutz.

## Schritt 4: Das HTML‑Dokument mit einer eingebetteten Ressource erstellen

Zur Demonstration erstellen wir eine kleine HTML‑Seite, die ein Bild mit dem Namen `image.png` referenziert. In einem realen Szenario würden Sie HTML aus einer Datei oder einem String aus einer Datenbank laden.

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

Wenn Sie tatsächliche Bilddateien auf der Festplatte haben, können Sie diese vor dem Speichern des HTML manuell zum ZIP hinzufügen oder Aspose.HTML sie über den Handler (z. B. von einer URL) holen lassen. Der von uns geschriebene Handler funktioniert sowohl für lokale Pfade als auch für entfernte URLs.

## Schritt 5: Speichereinstellungen konfigurieren, um den ZipResourceHandler zu verwenden

Jetzt teilen wir Aspose.HTML mit, unseren benutzerdefinierten Handler beim Schreiben von Ressourcen zu verwenden. Die Klasse `HTMLSaveOptions` ermöglicht zudem, den Ausgabedateinamen innerhalb des ZIPs festzulegen (standardmäßig ist es `index.html`).

```csharp
var saveOptions = new HTMLSaveOptions
{
    // The HTML file itself will be saved as "index.html" inside the zip.
    OutputFileName = "index.html",
    // Plug in our handler so resources go straight into the archive.
    OutputStorage = new ZipResourceHandler(zip)
};
```

## Schritt 6: Dokument speichern – Alles wird in das ZIP gestreamt

Zum Schluss rufen Sie `Save` auf. Aspose.HTML analysiert das Markup, findet das `<img>`‑Tag, ruft `HandleResource` für `image.png` auf und schreibt sowohl die HTML‑Datei als auch das Bild in dasselbe ZIP‑Archiv.

```csharp
html.Save(saveOptions);
Console.WriteLine($"HTML and its resources have been zipped to: {zipPath}");
```

Wenn die `using`‑Blöcke beendet werden, finalisiert das `ZipArchive` die Datei, sodass sie bereit für die Verteilung ist.

### Vollständiges funktionierendes Beispiel

Unten finden Sie das gesamte Programm zusammengefügt. Kopieren Sie es in `Program.cs` und führen Sie es aus – weitere Änderungen sind nicht nötig.

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

**Erwartetes Ergebnis:** Nach der Ausführung enthält `output.zip` zwei Einträge:

```
index.html
image.png
```

Wenn Sie die Datei entpacken und `index.html` in einem Browser öffnen, wird das Bild korrekt angezeigt, da der relative Pfad erhalten bleibt.

## Häufig gestellte Fragen

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}