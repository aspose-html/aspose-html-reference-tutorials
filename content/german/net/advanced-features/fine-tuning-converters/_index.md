---
title: Feinabstimmung von Konvertern in .NET mit Aspose.HTML
linktitle: Feinabstimmung von Konvertern in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie mit Aspose.HTML für .NET HTML in PDF, XPS und Bilder konvertieren. Schritt-für-Schritt-Anleitung mit Codebeispielen und FAQs.
type: docs
weight: 16
url: /de/net/advanced-features/fine-tuning-converters/
---

## Einführung

Aspose.HTML für .NET ist eine leistungsstarke Bibliothek, die es Entwicklern ermöglicht, HTML-Dokumente in verschiedenen Formaten zu bearbeiten und zu konvertieren. Unabhängig davon, ob Sie HTML in PDF, XPS oder Bilder konvertieren oder andere HTML-bezogene Aufgaben ausführen müssen, bietet Aspose.HTML eine Reihe robuster Tools, die Sie bei der Erledigung Ihrer Aufgabe unterstützen.

In diesem Tutorial werden wir einige wesentliche Funktionen von Aspose.HTML für .NET untersuchen und für jedes Beispiel Schritt-für-Schritt-Erklärungen bereitstellen. Am Ende dieses Tutorials verfügen Sie über ein solides Verständnis für die Verwendung von Aspose.HTML für .NET in Ihren .NET-Anwendungen.

## Voraussetzungen

Bevor wir uns mit den Beispielen befassen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

-  Aspose.HTML für .NET: Sie sollten die Aspose.HTML für .NET-Bibliothek installiert haben. Sie können es hier herunterladen[Download-Link](https://releases.aspose.com/html/net/).

- Temporäre Lizenz (optional): Wenn Sie keine gültige Lizenz haben, können Sie bei uns eine temporäre Lizenz erhalten[Hier](https://purchase.aspose.com/temporary-license/).

Lassen Sie uns nun einige häufige Anwendungsfälle mit Aspose.HTML für .NET untersuchen.

## Namespaces importieren

Beginnen Sie in Ihrem C#-Code mit dem Importieren der erforderlichen Namespaces:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Konvertieren Sie HTML in PDF

### Schritt 1: HTML-Code vorbereiten

```csharp
var code = @"<span>Hello World!!</span>";
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Schritt 3: PDF-Gerät erstellen und Ausgabedatei angeben

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Schritt 4: HTML in PDF rendern

```csharp
document.RenderTo(device);
```

In diesem Beispiel wird ein HTML-Snippet in ein PDF-Dokument konvertiert. Sie können den HTML-Code und die Ausgabedatei nach Bedarf anpassen.

## Legen Sie die benutzerdefinierte Seitengröße fest

### Schritt 1: HTML-Code vorbereiten

```csharp
var code = @"<span>Hello World!!</span>";
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Schritt 3: Erstellen Sie PDF-Rendering-Optionen

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Schritt 4: PDF-Gerät erstellen und Optionen und Ausgabedatei angeben

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Schritt 5: HTML in PDF rendern

```csharp
document.RenderTo(device);
```

Dieses Beispiel zeigt, wie Sie eine benutzerdefinierte Seitengröße für das resultierende PDF-Dokument festlegen.

## Passen Sie die Auflösung an

### Schritt 1: HTML-Code vorbereiten und in einer Datei speichern

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Schritt 3: Erstellen Sie PDF-Rendering-Optionen für niedrige Auflösung

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Schritt 4: PDF-Gerät erstellen und Optionen und Ausgabedatei für niedrige Auflösung angeben

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Schritt 5: Rendern Sie HTML für eine niedrige Auflösung in PDF

```csharp
document.RenderTo(device);
```

### Schritt 6: Erstellen Sie PDF-Renderingoptionen für hohe Auflösung

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Schritt 7: PDF-Gerät erstellen und Optionen und Ausgabedatei für hohe Auflösung festlegen

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Schritt 8: Rendern Sie HTML für eine hohe Auflösung in PDF

```csharp
document.RenderTo(device);
```

Dieses Beispiel veranschaulicht, wie die Auflösung beim Rendern von HTML in PDF angepasst wird, wobei sowohl Bildschirme mit niedriger als auch hoher Auflösung berücksichtigt werden.

## Geben Sie die Hintergrundfarbe an

### Schritt 1: HTML-Code vorbereiten und in einer Datei speichern

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Schritt 3: Initialisieren Sie die PDF-Rendering-Optionen mit der Hintergrundfarbe

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Schritt 4: PDF-Gerät erstellen und Optionen und Ausgabedatei angeben

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Schritt 5: HTML in PDF rendern

```csharp
document.RenderTo(device);
```

Dieses Beispiel zeigt, wie Sie beim Konvertieren von HTML in PDF eine Hintergrundfarbe angeben.

## Legen Sie die Seitengrößen für die linke und rechte Seite fest

### Schritt 1: HTML-Code vorbereiten

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Schritt 3: Erstellen Sie PDF-Rendering-Optionen mit linken und rechten Seitengrößen

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Schritt 4: PDF-Gerät erstellen und Optionen und Ausgabedatei angeben

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Schritt 5: HTML in PDF rendern

```csharp
document.RenderTo(device);
```

Dieses Beispiel zeigt, wie Sie beim Konvertieren von HTML in PDF unterschiedliche Seitengrößen für die linke und rechte Seite festlegen.

## Passen Sie die Seitengröße an den Inhalt an

### Schritt 1: HTML-Code vorbereiten

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Schritt 3: Erstellen Sie PDF-Rendering-Optionen

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Schritt 4: PDF-Gerät erstellen und Optionen und Ausgabedatei angeben

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Schritt 5: HTML in PDF rendern

```csharp
document.RenderTo(device);
```

Dieses Beispiel zeigt, wie Sie beim Konvertieren von HTML in PDF die Seitengröße an den breitesten Inhalt anpassen.

## Geben Sie PDF-Berechtigungen an

### Schritt 1: HTML-Code vorbereiten

```csharp
var code = @"<div>Hello World!!</div>";
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Schritt 3: Erstellen Sie PDF-Rendering-Optionen mit Berechtigungen

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Schritt 4: PDF-Gerät erstellen und Optionen und Ausgabedatei angeben

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Schritt 5: HTML in PDF rendern

```csharp
document.RenderTo(device);
```

Dieses Beispiel zeigt, wie Sie Berechtigungen und Verschlüsselung beim Konvertieren von HTML in eine geschützte PDF-Datei festlegen.

## Geben Sie bildspezifische Optionen an

### Schritt 1: HTML-Code vorbereiten

```csharp
var code = @"<div>Hello World!!</div>";
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Schritt 3: Erstellen Sie Bildwiedergabeoptionen

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Schritt 4: Bildgerät erstellen und Optionen und Ausgabedatei angeben

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Schritt 5: HTML in Bild rendern

```csharp
document.RenderTo(device);
```

Dieses Beispiel zeigt, wie HTML mit bestimmten Rendering-Optionen wie Format, Auflösung und Glättungsmodus in ein Bild konvertiert wird.

## Geben Sie XPS-Rendering-Optionen an

### Schritt 1: HTML-Code vorbereiten

```csharp
var code = @"<span>Hello World!!</span>";
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Schritt 3: Erstellen Sie XPS-Rendering-Optionen mit Seitengröße

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Schritt 4: XPS-Gerät erstellen und Optionen und Ausgabedatei angeben

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Schritt 5: HTML in XPS rendern

```csharp
document.RenderTo(device);
```

Dieses Beispiel zeigt, wie man HTML mit benutzerdefinierten Seitengrößen- und Rendering-Optionen in XPS konvertiert.

## Kombinieren Sie mehrere HTML-Dokumente zu PDF

### Schritt 1: HTML-Code für mehrere Dokumente vorbereiten

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Schritt 2: Erstellen Sie HTML-Dokumente zum Zusammenführen

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Schritt 3: HTML-Renderer initialisieren

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Schritt 4: Erstellen Sie ein PDF-Gerät für die zusammengeführte Ausgabe

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Schritt 5: HTML-Dokumente in PDF zusammenführen

```csharp
renderer.Render(device, document1, document2, document3);
```

Dieses Beispiel zeigt, wie Sie mit Aspose.HTML für .NET mehrere HTML-Dokumente in einer einzigen PDF-Datei kombinieren.

## Legen Sie das Rendering-Timeout fest

### Schritt 1: HTML-Code mit JavaScript vorbereiten

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Schritt 3: HTML-Renderer initialisieren

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Schritt 4: PDF-Gerät erstellen und Rendering-Timeout festlegen

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Schritt 5: HTML mit Timeout in PDF rendern

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Dieses Beispiel zeigt, wie man beim Konvertieren von HTML in PDF ein Rendering-Timeout festlegt, was bei der Arbeit mit dynamischen Inhalten oder lang laufenden Skripten nützlich sein kann.

## Abschluss

Aspose.HTML für .NET ist eine vielseitige Bibliothek, die Entwicklern die effiziente Arbeit mit HTML-Dokumenten ermöglicht. In diesem Tutorial haben wir verschiedene Beispiele behandelt, von einfachen HTML-zu-PDF-Konvertierungen bis hin zu erweiterten Funktionen wie benutzerdefinierten Seitengrößen, Auflösungen und Berechtigungen. Wenn Sie diese Beispiele befolgen, können Sie das volle Potenzial von Aspose.HTML für .NET in Ihren .NET-Anwendungen nutzen.

 Wenn Sie Fragen haben oder weitere Hilfe benötigen, besuchen Sie bitte die[Aspose.HTML-Forum](https://forum.aspose.com/) für Unterstützung und Anleitung.

## FAQs

### Q1. Was ist Aspose.HTML für .NET?
   
A1: Aspose.HTML für .NET ist eine .NET-Bibliothek, die es Entwicklern ermöglicht, HTML-Dokumente programmgesteuert zu bearbeiten und zu konvertieren. Es bietet zahlreiche Funktionen für die Arbeit mit HTML-Inhalten, darunter HTML in PDF, XPS und Bildkonvertierung sowie erweiterte Rendering-Optionen.

### Q2. Wo kann ich Aspose.HTML für .NET herunterladen?

 A2: Sie können Aspose.HTML für .NET von herunterladen[Download-Link](https://releases.aspose.com/html/net/).

### Q3. Benötige ich eine Lizenz, um Aspose.HTML für .NET zu verwenden?

A3: Während Sie Aspose.HTML für .NET ohne Lizenz verwenden können, wird empfohlen, eine Lizenz für die Produktionsnutzung zu erwerben, um alle Funktionen freizuschalten und etwaige Wasserzeichen oder Einschränkungen zu entfernen.

### Q4. Wie kann ich meine mit Aspose.HTML für .NET generierten PDF-Dateien schützen?

A4: Sie können PDF-Berechtigungen und Verschlüsselungseinstellungen angeben, wenn Sie HTML mit Aspose.HTML für .NET in PDF rendern. Dadurch können Sie steuern, wer auf die resultierenden PDF-Dateien zugreifen und diese ändern kann.

### F5. Kann ich HTML in andere Formate wie XPS oder Bilder konvertieren?

A5: Ja, Aspose.HTML für .NET unterstützt die Konvertierung von HTML in verschiedene Formate, einschließlich PDF, XPS und Bilder (z. B. JPEG). Sie können die Konvertierungseinstellungen an Ihre spezifischen Anforderungen anpassen.