---
title: Konvertieren Sie EPUB in XPS in .NET mit Aspose.HTML
linktitle: Konvertieren Sie EPUB in XPS in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie mit Aspose.HTML für .NET EPUB in XPS in .NET konvertieren. Folgen Sie unserer Schritt-für-Schritt-Anleitung für mühelose Konvertierungen.
type: docs
weight: 13
url: /de/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Suchen Sie nach einer nahtlosen Möglichkeit, EPUB-Dateien in Ihren .NET-Anwendungen in das XPS-Format zu konvertieren? Aspose.HTML für .NET bietet eine leistungsstarke Lösung, um dies mühelos zu erreichen. In dieser Schritt-für-Schritt-Anleitung führen wir Sie durch den Prozess der Konvertierung von EPUB in XPS mit Aspose.HTML. Lassen Sie uns anfangen!

## Voraussetzungen

Bevor Sie mit der Konvertierung von EPUB in XPS beginnen, müssen Sie sicherstellen, dass die folgenden Voraussetzungen erfüllt sind:

### 1. Aspose.HTML für .NET-Bibliothek

 Stellen Sie sicher, dass Sie die Bibliothek Aspose.HTML für .NET in Ihrem Projekt installiert haben. Wenn Sie dies nicht getan haben, können Sie sie von der[Aspose.HTML für .NET Download-Seite](https://releases.aspose.com/html/net/).

### 2. EPUB-Datei eingeben

Sie benötigen eine EPUB-Datei, die Sie in XPS konvertieren möchten. Stellen Sie sicher, dass Ihnen eine EPUB-Datei zur Konvertierung zur Verfügung steht.

### 3. .NET-Entwicklungsumgebung

Diese Anleitung setzt voraus, dass auf Ihrem Computer eine funktionierende .NET-Entwicklungsumgebung eingerichtet ist.

## Namespace importieren

Zu Beginn sollten Sie den erforderlichen Namespace für Aspose.HTML importieren:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Konvertieren Sie EPUB in XPS

Lassen Sie uns den Prozess der Konvertierung einer EPUB-Datei in das XPS-Format in mehrere Schritte aufteilen.

### Schritt 1.1: Öffnen Sie die EPUB-Datei

Öffnen Sie zunächst die vorhandene EPUB-Datei zum Lesen mithilfe eines FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Fahren Sie mit dem Konvertierungsprozess fort
}
```

### Schritt 1.2: XpsSaveOptions erstellen

Erstellen Sie eine Instanz von XpsSaveOptions. Dieser Schritt ist für die Konfiguration der XPS-Ausgabe entscheidend:

```csharp
var options = new XpsSaveOptions();
```

### Schritt 1.3: EPUB in XPS konvertieren

Rufen wir nun die Methode ConvertEPUB auf, um EPUB in XPS zu konvertieren:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Angeben benutzerdefinierter XPS-Optionen

Sie können die XPS-Ausgabe weiter anpassen, indem Sie benutzerdefinierte Optionen wie Seitengröße und Hintergrundfarbe angeben.

### Schritt 2.1: Benutzerdefinierte Seitengröße und Hintergrundfarbe

Erstellen Sie eine Instanz von XpsSaveOptions mit benutzerdefinierter Seitengröße und Hintergrundfarbe:

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

### Schritt 2.2: Konvertieren Sie EPUB mit benutzerdefinierten Optionen in XPS

Rufen Sie jetzt die Methode ConvertEPUB auf, um EPUB mit den benutzerdefinierten Optionen in XPS zu konvertieren:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Benutzerdefinierten Stream-Anbieter verwenden

In diesem Schritt konvertieren wir EPUB mithilfe eines benutzerdefinierten Stream-Anbieters in XPS, sodass Sie die resultierenden Daten bearbeiten können.

### Schritt 3.1: Erstellen eines MemoryStreamProviders

Erstellen Sie eine Instanz von MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Fahren Sie mit dem Konvertierungsprozess fort
}
```

### Schritt 3.2: EPUB mit Stream Provider in XPS konvertieren

Konvertieren Sie EPUB mithilfe des MemoryStreamProviders in XPS:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Schritt 3.3: Ergebnis abrufen und speichern

Rufen Sie den Speicherstream mit den konvertierten Daten ab und speichern Sie ihn in einer Ausgabedatei:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Klasse MemoryStreamProvider Quellcode

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Liste der MemoryStream-Objekte, die während der Dokumentwiedergabe erstellt wurden
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Diese Methode wird aufgerufen, wenn nur ein Ausgabestream erforderlich ist, beispielsweise für die Formate XPS, PDF oder TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Diese Methode wird aufgerufen, wenn die Erstellung mehrerer Ausgabeströme erforderlich ist. Beispielsweise beim Rendern von HTML zur Liste der Bilddateien (JPG, PNG usw.).
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Hier können Sie den mit Daten gefüllten Stream freigeben und beispielsweise auf die Festplatte übertragen
            }
            public void Dispose()
            {
                // Ressourcen freigeben
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Herzlichen Glückwunsch! Sie haben eine EPUB-Datei mit Aspose.HTML für .NET erfolgreich in das XPS-Format konvertiert.

## Abschluss

In diesem umfassenden Tutorial haben wir untersucht, wie Sie Aspose.HTML für .NET nutzen können, um EPUB-Dateien mit verschiedenen Anpassungsoptionen in das XPS-Format zu konvertieren. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, Aspose.HTML vereinfacht den Prozess und ermöglicht Ihnen die problemlose Konvertierung von EPUB in XPS.

 Haben Sie Fragen oder sind Probleme aufgetreten? Schauen Sie sich die[Aspose.HTML Dokumentation](https://reference.aspose.com/html/net/) für weitere Einblicke oder Hilfe von der[Aspose.HTML Gemeinschaftsforum](https://forum.aspose.com/).

## Häufig gestellte Fragen

### Was ist Aspose.HTML für .NET?
Aspose.HTML für .NET ist eine leistungsstarke Bibliothek, die es Entwicklern ermöglicht, mit HTML-, EPUB- und XPS-Dokumenten in .NET-Anwendungen zu arbeiten.

### Wo kann ich Aspose.HTML für .NET herunterladen?
 Sie können Aspose.HTML für .NET herunterladen von der[Download-Seite](https://releases.aspose.com/html/net/).

### Gibt es eine kostenlose Testversion für Aspose.HTML für .NET?
 Ja, Sie können eine kostenlose Testversion erhalten von[Hier](https://releases.aspose.com/).

### Wie kann ich eine temporäre Lizenz für Aspose.HTML für .NET erhalten?
 Um eine temporäre Lizenz zu erhalten, besuchen Sie die[Seite mit der temporären Lizenz](https://purchase.aspose.com/temporary-license/).

### Wo finde ich weitere Tutorials und Dokumentationen für Aspose.HTML für .NET?
 Entdecken Sie eine große Auswahl an Tutorials und ausführlicher Dokumentation zum[Aspose.HTML Dokumentation](https://reference.aspose.com/html/net/) Seite.