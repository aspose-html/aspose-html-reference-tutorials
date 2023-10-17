---
title: Konvertieren Sie EPUB in XPS in .NET mit Aspose.HTML
linktitle: Konvertieren Sie EPUB in XPS in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie EPUB in XPS in .NET mit Aspose.HTML für .NET konvertieren. Befolgen Sie unsere Schritt-für-Schritt-Anleitung für mühelose Konvertierungen.
type: docs
weight: 13
url: /de/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Suchen Sie nach einer nahtlosen Möglichkeit, EPUB-Dateien in Ihren .NET-Anwendungen in das XPS-Format zu konvertieren? Aspose.HTML für .NET bietet eine leistungsstarke Lösung, um dies mühelos zu erreichen. In dieser Schritt-für-Schritt-Anleitung führen wir Sie durch den Prozess der Konvertierung von EPUB in XPS mit Aspose.HTML. Lass uns anfangen!

## Voraussetzungen

Bevor Sie mit der Konvertierung von EPUB in XPS beginnen, müssen Sie sicherstellen, dass die folgenden Voraussetzungen erfüllt sind:

### 1. Aspose.HTML für .NET-Bibliothek

 Stellen Sie sicher, dass in Ihrem Projekt die Aspose.HTML für .NET-Bibliothek installiert ist. Wenn Sie dies noch nicht getan haben, können Sie es bei erhalten[Aspose.HTML für .NET-Downloadseite](https://releases.aspose.com/html/net/).

### 2. Geben Sie die EPUB-Datei ein

Sie benötigen eine EPUB-Datei, die Sie in XPS konvertieren möchten. Stellen Sie sicher, dass Ihnen eine EPUB-Datei zur Konvertierung zur Verfügung steht.

### 3. .NET-Entwicklungsumgebung

In diesem Handbuch wird davon ausgegangen, dass auf Ihrem Computer eine funktionierende .NET-Entwicklungsumgebung eingerichtet ist.

## Namespace importieren

Zunächst sollten Sie den erforderlichen Namespace für Aspose.HTML importieren:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Konvertieren Sie EPUB in XPS

Lassen Sie uns den Prozess der Konvertierung einer EPUB-Datei in das XPS-Format in mehrere Schritte unterteilen.

### Schritt 1.1: Öffnen Sie die EPUB-Datei

Öffnen Sie zunächst die vorhandene EPUB-Datei zum Lesen mit einem FileStream:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Fahren Sie mit dem Konvertierungsprozess fort
}
```

### Schritt 1.2: Erstellen Sie XpsSaveOptions

Erstellen Sie eine Instanz von XpsSaveOptions. Dieser Schritt ist für die Konfiguration der XPS-Ausgabe von entscheidender Bedeutung:

```csharp
var options = new XpsSaveOptions();
```

### Schritt 1.3: EPUB in XPS konvertieren

Rufen wir nun die ConvertEPUB-Methode auf, um EPUB in XPS zu konvertieren:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Geben Sie benutzerdefinierte XPS-Optionen an

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

Rufen Sie nun die ConvertEPUB-Methode auf, um EPUB mit den benutzerdefinierten Optionen in XPS zu konvertieren:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Verwenden Sie einen benutzerdefinierten Stream-Anbieter

In diesem Schritt konvertieren wir EPUB mithilfe eines benutzerdefinierten Stream-Anbieters in XPS, sodass Sie die resultierenden Daten bearbeiten können.

### Schritt 3.1: Erstellen Sie einen MemoryStreamProvider

Erstellen Sie eine Instanz von MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Fahren Sie mit dem Konvertierungsprozess fort
}
```

### Schritt 3.2: Konvertieren Sie EPUB in XPS mit Stream Provider

Konvertieren Sie EPUB in XPS mithilfe des MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Schritt 3.3: Auf das Ergebnis zugreifen und es speichern

Rufen Sie den Speicherstream mit den konvertierten Daten ab und speichern Sie ihn in einer Ausgabedatei:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Quellcode der Klasse MemoryStreamProvider

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Liste der MemoryStream-Objekte, die während der Dokumentwiedergabe erstellt wurden
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Diese Methode wird aufgerufen, wenn nur ein Ausgabestream erforderlich ist, beispielsweise für XPS-, PDF- oder TIFF-Formate.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Diese Methode wird aufgerufen, wenn die Erstellung mehrerer Ausgabestreams erforderlich ist. Zum Beispiel beim Rendern von HTML in eine Liste der Bilddateien (JPG, PNG usw.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Hier können Sie den mit Daten gefüllten Stream freigeben und beispielsweise auf die Festplatte spülen
            }
            public void Dispose()
            {
                // Ressourcen freisetzen
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Glückwunsch! Sie haben eine EPUB-Datei mit Aspose.HTML für .NET erfolgreich in das XPS-Format konvertiert.

## Abschluss

In diesem umfassenden Tutorial haben wir untersucht, wie Sie Aspose.HTML für .NET nutzen können, um EPUB-Dateien mit verschiedenen Anpassungsoptionen in das XPS-Format zu konvertieren. Unabhängig davon, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, Aspose.HTML vereinfacht den Prozess und ermöglicht Ihnen die problemlose Konvertierung von EPUB in XPS.

 Haben Sie Fragen oder sind Probleme aufgetreten? Besuche die[Aspose.HTML-Dokumentation](https://reference.aspose.com/html/net/) für weitere Einblicke oder suchen Sie Hilfe bei der[Aspose.HTML-Community-Forum](https://forum.aspose.com/).

## Häufig gestellte Fragen

### Was ist Aspose.HTML für .NET?
Aspose.HTML für .NET ist eine leistungsstarke Bibliothek, die Entwicklern die Arbeit mit HTML-, EPUB- und XPS-Dokumenten in .NET-Anwendungen ermöglicht.

### Wo kann ich Aspose.HTML für .NET herunterladen?
 Sie können Aspose.HTML für .NET von herunterladen[Download-Seite](https://releases.aspose.com/html/net/).

### Gibt es eine kostenlose Testversion für Aspose.HTML für .NET?
 Ja, Sie können eine kostenlose Testversion von erhalten[Hier](https://releases.aspose.com/).

### Wie kann ich eine temporäre Lizenz für Aspose.HTML für .NET erhalten?
 Um eine temporäre Lizenz zu erhalten, besuchen Sie die[temporäre Lizenzseite](https://purchase.aspose.com/temporary-license/).

### Wo finde ich weitere Tutorials und Dokumentation für Aspose.HTML für .NET?
Entdecken Sie eine große Auswahl an Tutorials und ausführlicher Dokumentation zum Thema[Aspose.HTML-Dokumentation](https://reference.aspose.com/html/net/) Seite.