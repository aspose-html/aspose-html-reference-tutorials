---
title: Konvertieren Sie EPUB in .NET mit Aspose.HTML in ein Bild
linktitle: Konvertieren Sie EPUB in .NET in ein Bild
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie mit Aspose.HTML für .NET EPUB in Bilder konvertieren. Schritt-für-Schritt-Anleitung mit Codebeispielen und anpassbaren Optionen.
weight: 11
url: /de/net/html-extensions-and-conversions/convert-epub-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertieren Sie EPUB in .NET mit Aspose.HTML in ein Bild


Im heutigen digitalen Zeitalter ist die Fähigkeit, verschiedene Dokumentformate zu bearbeiten und zu konvertieren, eine wertvolle Fähigkeit. Aspose.HTML für .NET ist ein leistungsstarkes Tool, mit dem Entwickler mühelos mit HTML- und EPUB-Dokumenten arbeiten können. In diesem Tutorial tauchen wir in die Welt von Aspose.HTML für .NET ein und führen Sie durch den Prozess der Konvertierung von EPUB-Dokumenten in verschiedene Bildformate. Wir unterteilen jedes Beispiel in mehrere Schritte und erklären dabei jeden Schritt.

## Voraussetzungen

Bevor wir in die Welt von Aspose.HTML für .NET eintauchen, sollten Sie sicherstellen, dass die folgenden Voraussetzungen erfüllt sind:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem System installiert ist. Sie können es von der Website herunterladen.

2.  Aspose.HTML für .NET: Sie können die Bibliothek von der Aspose-Website beziehen[Hier](https://releases.aspose.com/html/net/).

3. Ihr Datenverzeichnis: Bereiten Sie ein Verzeichnis vor, in dem Sie Ihre EPUB-Dateien speichern und in dem die Ausgabebilder gespeichert werden.

4. Grundkenntnisse in C#: Um die in diesem Tutorial bereitgestellten Codebeispiele zu verstehen und umzusetzen, sind Kenntnisse in der C#-Programmierung unerlässlich.

## Erforderliche Namespaces importieren

Bevor wir mit der Arbeit mit Aspose.HTML für .NET beginnen, müssen Sie die erforderlichen Namespaces in Ihren C#-Code importieren. Diese Namespaces bieten Zugriff auf die Funktionen von Aspose.HTML für .NET.

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

Nachdem wir nun die Voraussetzungen und Namespaces eingerichtet haben, können wir mit den schrittweisen Beispielen fortfahren.

## Konvertieren von EPUB in JPEG

```csharp
    string dataDir = "Your Data Directory";
    // Öffnen Sie eine vorhandene EPUB-Datei zum Lesen.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // Rufen Sie die Methode ConvertEPUB auf, um die EPUB-Datei in ein Bild zu konvertieren.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Vorgehensweise

1. Geben Sie den Pfad zu Ihrer EPUB-Datei in der Variable „dataDir“ an.
2. Öffnen Sie die EPUB-Datei zum Lesen mithilfe eines FileStream.
3. Rufen Sie die Methode ConvertEPUB auf und übergeben Sie den EPUB-Stream, eine ImageSaveOptions, die das Ausgabeformat (JPEG) angibt, und den Namen der Ausgabedatei („output.jpg“).
5. Die EPUB-Datei wird in ein JPEG-Bild konvertiert.

In diesem Beispiel öffnen wir eine EPUB-Datei, lesen ihren Inhalt und konvertieren sie in ein JPEG-Bildformat. Das Ausgabebild wird als „output.jpg“ gespeichert.

## Konvertieren von EPUB in PNG

Sie können EPUB-Dateien mithilfe ähnlicher Codestrukturen problemlos in verschiedene Bildformate wie PNG, BMP, GIF und TIFF konvertieren. Hier ist ein Beispiel für die Konvertierung in PNG:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### Vorgehensweise
1. Öffnen Sie die EPUB-Datei zum Lesen mithilfe eines FileStream.
2. Initialisieren Sie ein ImageSaveOptions-Objekt mit dem gewünschten Ausgabeformat (in diesem Fall PNG).
3. Rufen Sie die Methode ConvertEPUB auf und übergeben Sie den EPUB-Stream, die Optionen zum Speichern des Bilds und den Namen der Ausgabedatei.
4. Die EPUB-Datei wird in das angegebene Bildformat konvertiert.

## Festlegen von Optionen zum Speichern von Bildern

Sie können die Bildausgabe anpassen, indem Sie Optionen wie Seitengröße und Hintergrundfarbe angeben. Hier ist ein Beispiel:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### Vorgehensweise

1.  Geben Sie den Pfad zu Ihrer EPUB-Datei im`dataDir` Variable.
2.  Öffnen Sie die EPUB-Datei zum Lesen mit einem`FileStream`.
3.  Erstellen Sie ein`ImageSaveOptions` Objekt und geben Sie das gewünschte Ausgabeformat (JPEG) an.
4. Passen Sie bei Bedarf die Seitengröße und Hintergrundfarbe an.
5.  Rufen Sie die`ConvertEPUB`Methode, bei der der EPUB-Stream, die Optionen zum Speichern des Bilds und der Name der Ausgabedatei übergeben werden.
6. Die EPUB-Datei wird mit den angegebenen Optionen in ein Bild konvertiert.

## Angeben eines benutzerdefinierten Stream-Anbieters

Wenn Sie den Ausgabestream bearbeiten müssen, können Sie einen benutzerdefinierten Stream-Provider verwenden. Hier ist ein Beispiel:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
Quellcode der MemoryStreamProvider-Klasse.

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

### Vorgehensweise
1.  Geben Sie den Pfad zu Ihrer EPUB-Datei im`dataDir` Variable.
2.  Öffnen Sie die EPUB-Datei zum Lesen mit einem`FileStream`.
3.  Erstellen Sie ein`MemoryStreamProvider` um benutzerdefinierte Ausgabeströme zu verarbeiten.
4.  Rufen Sie die`ConvertEPUB` Methode, wobei der EPUB-Stream, die Bildspeicheroptionen (JPEG) und der benutzerdefinierte Stream-Anbieter übergeben werden.
5. Iterieren Sie durch die Speicherströme im benutzerdefinierten Anbieter und speichern Sie sie in einzelnen Dateien.
6. Mit diesem Beispiel können Sie mehrere Ausgabeströme nach Bedarf bearbeiten und speichern.

## Abschluss

Aspose.HTML für .NET ist eine vielseitige Bibliothek, die die Arbeit mit EPUB- und HTML-Dokumenten vereinfacht. Mit der Möglichkeit, EPUB-Dokumente in verschiedene Bildformate und anpassbare Optionen zu konvertieren, bietet es Entwicklern ein breites Anwendungsspektrum.

---

## Häufig gestellte Fragen

### 1. Wo kann ich Aspose.HTML für .NET herunterladen?

 Sie können Aspose.HTML für .NET von der Releases-Seite herunterladen.[Hier](https://releases.aspose.com/html/net/).

### 2. Wie kann ich eine temporäre Lizenz für Aspose.HTML für .NET erhalten?

 Um eine temporäre Lizenz zu erhalten, besuchen Sie die Seite mit den temporären Lizenzen.[Hier](https://purchase.aspose.com/temporary-license/).

### 3. Wo finde ich zusätzliche Unterstützung für Aspose.HTML für .NET?

 Bei Fragen oder Problemen können Sie sich an die Aspose-Community im Support-Forum wenden.[Hier](https://forum.aspose.com/).

### 4. Kann ich EPUB-Dokumente in andere Formate wie PDF oder XPS konvertieren?

Ja, Sie können Aspose.HTML für .NET verwenden, um EPUB-Dokumente in verschiedene Formate zu konvertieren, darunter PDF und XPS.

### 5. Ist Aspose.HTML für .NET sowohl für kleine als auch für große Projekte geeignet?

Auf jeden Fall! Aspose.HTML für .NET ist skalierbar und damit eine hervorragende Wahl für Projekte jeder Größe.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
