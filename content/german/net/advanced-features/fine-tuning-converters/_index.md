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

Aspose.HTML für .NET ist eine leistungsstarke Bibliothek, mit der Entwickler HTML-Dokumente in verschiedenen Formaten bearbeiten und konvertieren können. Ob Sie HTML in PDF, XPS oder Bilder konvertieren oder andere HTML-bezogene Aufgaben ausführen müssen, Aspose.HTML bietet einen robusten Satz von Tools, die Ihnen dabei helfen, die Arbeit zu erledigen.

In diesem Tutorial werden wir einige wesentliche Funktionen von Aspose.HTML für .NET untersuchen und für jedes Beispiel schrittweise Erklärungen bereitstellen. Am Ende dieses Tutorials verfügen Sie über ein solides Verständnis für die Verwendung von Aspose.HTML für .NET in Ihren .NET-Anwendungen.

## Voraussetzungen

Bevor wir uns in die Beispiele vertiefen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

-  Aspose.HTML für .NET: Sie sollten die Bibliothek Aspose.HTML für .NET installiert haben. Sie können sie von der[Downloadlink](https://releases.aspose.com/html/net/).

-  Temporäre Lizenz (optional): Wenn Sie keine gültige Lizenz haben, können Sie eine temporäre Lizenz erhalten von[Hier](https://purchase.aspose.com/temporary-license/).

Sehen wir uns nun einige gängige Anwendungsfälle mit Aspose.HTML für .NET an.

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

Dieses Beispiel konvertiert einen HTML-Ausschnitt in ein PDF-Dokument. Sie können den HTML-Code und die Ausgabedatei nach Bedarf anpassen.

## Benutzerdefinierte Seitengröße festlegen

### Schritt 1: HTML-Code vorbereiten

```csharp
var code = @"<span>Hello World!!</span>";
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Schritt 3: PDF-Rendering-Optionen erstellen

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

Dieses Beispiel zeigt, wie eine benutzerdefinierte Seitengröße für das resultierende PDF-Dokument festgelegt wird.

## Auflösung anpassen

### Schritt 1: HTML-Code vorbereiten und in Datei speichern

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

### Schritt 3: Erstellen Sie PDF-Rendering-Optionen für niedrige Auflösungen

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Schritt 4: PDF-Gerät erstellen und Optionen und Ausgabedatei für niedrige Auflösung festlegen

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Schritt 5: HTML in PDF für niedrige Auflösung rendern

```csharp
document.RenderTo(device);
```

### Schritt 6: Erstellen Sie PDF-Rendering-Optionen für hohe Auflösung

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

### Schritt 8: HTML in PDF für hohe Auflösung rendern

```csharp
document.RenderTo(device);
```

Dieses Beispiel veranschaulicht, wie die Auflösung beim Rendern von HTML in PDF angepasst wird, wobei sowohl Bildschirme mit niedriger als auch mit hoher Auflösung berücksichtigt werden.

## Hintergrundfarbe festlegen

### Schritt 1: HTML-Code vorbereiten und in Datei speichern

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Schritt 3: PDF-Rendering-Optionen mit Hintergrundfarbe initialisieren

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

## Festlegen der linken und rechten Seitengröße

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

## Seitengröße dem Inhalt anpassen

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

### Schritt 3: PDF-Rendering-Optionen erstellen

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

Dieses Beispiel zeigt, wie Sie bei der Konvertierung von HTML in PDF die Seitengröße an den breitesten Inhalt anpassen.

## PDF-Berechtigungen festlegen

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

Dieses Beispiel zeigt, wie Sie beim Konvertieren von HTML in ein geschütztes PDF Berechtigungen und Verschlüsselung angeben.

## Bildspezifische Optionen festlegen

### Schritt 1: HTML-Code vorbereiten

```csharp
var code = @"<div>Hello World!!</div>";
```

### Schritt 2: HTML-Dokument initialisieren

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Schritt 3: Bild-Rendering-Optionen erstellen

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Schritt 4: Image-Gerät erstellen und Optionen und Ausgabedatei angeben

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Schritt 5: HTML in Bild rendern

```csharp
document.RenderTo(device);
```

Dieses Beispiel zeigt, wie HTML mit bestimmten Rendering-Optionen wie Format, Auflösung und Glättungsmodus in ein Bild konvertiert wird.

## XPS-Rendering-Optionen festlegen

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

Dieses Beispiel zeigt, wie HTML mit benutzerdefinierter Seitengröße und Rendering-Optionen in XPS konvertiert wird.

## Mehrere HTML-Dokumente zu PDF zusammenführen

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

### Schritt 4: PDF-Gerät für zusammengeführte Ausgabe erstellen

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Schritt 5: HTML-Dokumente in PDF zusammenführen

```csharp
renderer.Render(device, document1, document2, document3);
```

Dieses Beispiel zeigt, wie mehrere HTML-Dokumente mit Aspose.HTML für .NET zu einer einzigen PDF-Datei kombiniert werden.

## Rendering-Timeout festlegen

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

Dieses Beispiel zeigt, wie Sie beim Konvertieren von HTML in PDF ein Rendering-Timeout festlegen, was beim Umgang mit dynamischen Inhalten oder Skripts mit langer Laufzeit nützlich sein kann.

## Abschluss

Aspose.HTML für .NET ist eine vielseitige Bibliothek, die Entwicklern die effiziente Arbeit mit HTML-Dokumenten ermöglicht. In diesem Tutorial haben wir verschiedene Beispiele behandelt, von einfachen HTML-zu-PDF-Konvertierungen bis hin zu erweiterten Funktionen wie benutzerdefinierten Seitengrößen, Auflösungen und Berechtigungen. Indem Sie diese Beispiele befolgen, können Sie das volle Potenzial von Aspose.HTML für .NET in Ihren .NET-Anwendungen nutzen.

 Wenn Sie Fragen haben oder weitere Hilfe benötigen, besuchen Sie bitte die[Aspose.HTML Forum](https://forum.aspose.com/) für Unterstützung und Anleitung.

## Häufig gestellte Fragen

### F1. Was ist Aspose.HTML für .NET?
   
A1: Aspose.HTML für .NET ist eine .NET-Bibliothek, mit der Entwickler HTML-Dokumente programmgesteuert bearbeiten und konvertieren können. Sie bietet eine breite Palette an Funktionen für die Arbeit mit HTML-Inhalten, darunter HTML-zu-PDF-, XPS- und Bildkonvertierung sowie erweiterte Rendering-Optionen.

### F2. Wo kann ich Aspose.HTML für .NET herunterladen?

 A2: Sie können Aspose.HTML für .NET herunterladen von der[Downloadlink](https://releases.aspose.com/html/net/).

### F3. Benötige ich eine Lizenz, um Aspose.HTML für .NET zu verwenden?

A3: Obwohl Sie Aspose.HTML für .NET ohne Lizenz verwenden können, wird empfohlen, für die Produktionsnutzung eine Lizenz zu erwerben, um alle Funktionen freizuschalten und sämtliche Wasserzeichen oder Einschränkungen zu entfernen.

### F4. Wie kann ich meine mit Aspose.HTML für .NET erstellten PDF-Dateien schützen?

A4: Sie können PDF-Berechtigungen und Verschlüsselungseinstellungen angeben, wenn Sie HTML mit Aspose.HTML für .NET in PDF rendern. Auf diese Weise können Sie steuern, wer auf die resultierenden PDF-Dateien zugreifen und diese ändern kann.

### F5. Kann ich HTML in andere Formate wie XPS oder Bilder konvertieren?

A5: Ja, Aspose.HTML für .NET unterstützt die Konvertierung von HTML in verschiedene Formate, darunter PDF, XPS und Bilder (z. B. JPEG). Sie können die Konvertierungseinstellungen an Ihre spezifischen Anforderungen anpassen.