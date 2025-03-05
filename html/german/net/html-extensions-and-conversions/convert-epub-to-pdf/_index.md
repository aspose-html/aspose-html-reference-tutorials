---
title: Konvertieren Sie EPUB in .NET mit Aspose.HTML in PDF
linktitle: Konvertieren Sie EPUB in .NET in PDF
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie mit Aspose.HTML für .NET EPUB in PDF konvertieren. Diese Schritt-für-Schritt-Anleitung umfasst Anpassungsoptionen, FAQs und mehr für eine nahtlose Dokumentkonvertierung.
type: docs
weight: 12
url: /de/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

In diesem Tutorial erfahren Sie, wie Sie mit Aspose.HTML für .NET EPUB-Dateien in PDF konvertieren. Aspose.HTML ist eine leistungsstarke .NET-Bibliothek, die verschiedene Funktionen für die Arbeit mit HTML- und EPUB-Dokumenten bietet. Wir behandeln die Voraussetzungen, importieren die erforderlichen Namespaces und analysieren mehrere Beispiele, wobei wir jeden Schritt im Detail erklären.

## Voraussetzungen

Stellen Sie zunächst sicher, dass die folgenden Voraussetzungen erfüllt sind:

1. Aspose.HTML für .NET: Stellen Sie sicher, dass Sie Aspose.HTML für .NET in Ihrem .NET-Projekt installiert haben. Sie können es herunterladen von[Hier](https://releases.aspose.com/html/net/).

2. Ihr Datenverzeichnis: Sie benötigen ein Datenverzeichnis, in dem Ihre EPUB-Dateien gespeichert sind.

Lassen Sie uns nun Schritt für Schritt in den Prozess der Konvertierung von EPUB in PDF mit Aspose.HTML für .NET eintauchen.

## Konvertieren Sie EPUB in PDF

### Schritt 1: Initialisieren Sie Ihr Projekt

Stellen Sie sicher, dass Sie ein .NET-Projekt eingerichtet und Aspose.HTML für .NET installiert haben.

### Schritt 2: Erforderliche Namespaces importieren

Importieren Sie in Ihre C#-Codedatei die erforderlichen Namespaces:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Schritt 3: Öffnen Sie die EPUB-Datei

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Fahren Sie mit dem nächsten Schritt fort ...
}
```

-  Ersetzen`"Your Data Directory"` durch das tatsächliche Verzeichnis, in dem sich Ihre EPUB-Datei befindet.
- Dieser Code öffnet die EPUB-Datei zum Lesen.

### Schritt 4: PDF-Optionen festlegen und Konvertierung durchführen

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Erstellen Sie eine Instanz von`PdfSaveOptions` um PDF-Konvertierungseinstellungen festzulegen.
-  Verwenden Sie die`Converter.ConvertEPUB` Methode zum Konvertieren von EPUB in PDF mit den angegebenen Optionen.
- Speichern Sie das resultierende PDF als „output.pdf“.

## PDF-Speicheroptionen festlegen

### Schritt 1: Initialisieren Sie Ihr Projekt

Stellen Sie sicher, dass Sie ein .NET-Projekt eingerichtet und Aspose.HTML für .NET installiert haben.

### Schritt 2: Erforderliche Namespaces importieren

Importieren Sie die erforderlichen Namespaces in Ihren C#-Code:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Schritt 3: Öffnen Sie die EPUB-Datei

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Fahren Sie mit dem nächsten Schritt fort ...
}
```

-  Ersetzen`"Your Data Directory"` durch das tatsächliche Verzeichnis Ihrer EPUB-Datei.
- Öffnen Sie die EPUB-Datei zum Lesen.

### Schritt 4: PDF-Optionen anpassen

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Erstellen Sie eine Instanz von`PdfSaveOptions` und passen Sie es Ihren Anforderungen entsprechend an.
- In diesem Beispiel haben wir die Seitengröße auf 3000 Pixel Breite und 1000 Pixel Höhe und die Hintergrundfarbe auf Alice Blue eingestellt.

### Schritt 5: Konvertierung durchführen

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Verwenden Sie die`Converter.ConvertEPUB` Methode zum Konvertieren von EPUB in PDF mit benutzerdefinierten Optionen.
- Speichern Sie das resultierende PDF als „output.pdf“.

## Benutzerdefinierten Stream-Anbieter verwenden

### Schritt 1: Initialisieren Sie Ihr Projekt

Richten Sie ein .NET-Projekt ein und installieren Sie Aspose.HTML für .NET.

### Schritt 2: Erforderliche Namespaces importieren

Importieren Sie in Ihren C#-Code die erforderlichen Namespaces:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Schritt 3: Öffnen Sie die EPUB-Datei

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Fahren Sie mit dem nächsten Schritt fort ...
}
```

-  Ersetzen`"Your Data Directory"` durch das tatsächliche Verzeichnis Ihrer EPUB-Datei.
- Öffnen Sie die EPUB-Datei zum Lesen.

### Schritt 4: Verwenden Sie einen benutzerdefinierten Stream-Anbieter

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Fahren Sie mit dem nächsten Schritt fort ...
}
```

-  Erstellen Sie ein`MemoryStreamProvider` um das Konvertierungsergebnis als Speicherstrom zu verwalten.
-  Verwenden Sie die`Converter.ConvertEPUB` Methode mit dem benutzerdefinierten Stream-Anbieter.

### Schritt 5: Speichern Sie das Ergebnis

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Greifen Sie auf den Speicherstream zu, der die konvertierten Daten enthält.
- Setzt die Streamposition auf den Anfang.
- Erstellen Sie eine PDF-Ausgabedatei und kopieren Sie den Inhalt aus dem Speicherstream dorthin.

### Quellcode der Klasse MemoryStreamProvider. 

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
Jetzt haben Sie gelernt, wie Sie EPUB-Dateien mit Aspose.HTML für .NET mit verschiedenen Optionen und Anpassungsmöglichkeiten in PDF konvertieren. Aspose.HTML vereinfacht den Prozess und bietet Flexibilität und Kontrolle über Ihre Dokumentkonvertierung.

## Abschluss

Aspose.HTML für .NET ist ein vielseitiges Tool zum Konvertieren von EPUB-Dateien in PDF und bietet Anpassungsoptionen, um das resultierende PDF-Dokument an Ihre Bedürfnisse anzupassen. Egal, ob Sie einfache Konvertierungen oder erweiterte Anpassungen benötigen, Aspose.HTML bietet alles.

 Wenn Sie es noch nicht getan haben, können Sie Aspose.HTML für .NET von der[Webseite](https://releases.aspose.com/html/net/) und beginnen Sie noch heute, es in Ihren .NET-Anwendungen zu verwenden.

---

## FAQs

### Ist die Nutzung von Aspose.HTML für .NET kostenlos?
    Aspose.HTML für .NET ist ein kommerzielles Produkt, aber eine kostenlose Testversion ist verfügbar[Hier](https://releases.aspose.com/).

### Kann ich das Erscheinungsbild der konvertierten PDF-Datei anpassen?
   Ja, Sie können das Erscheinungsbild der PDF-Datei anpassen, indem Sie Optionen wie Seitengröße und Hintergrundfarbe anpassen, wie in Beispiel 2 gezeigt.

### Wie erhalte ich Support für Aspose.HTML für .NET?
    Unterstützung und Ressourcen finden Sie auf der[Aspose.HTML-Forum](https://forum.aspose.com/).

### Gibt es andere Formate, die ich mit Aspose.HTML für .NET konvertieren kann?
   Ja, Aspose.HTML für .NET unterstützt verschiedene Dokumentformate, darunter HTML, EPUB und mehr.

### Ist Aspose.HTML für ..NET für die Konvertierung von Dokumenten im großen Maßstab geeignet?
   Aspose.HTML für .NET ist für die effiziente Handhabung umfangreicher Dokumentkonvertierungen konzipiert und eignet sich daher für ein breites Anwendungsspektrum.

