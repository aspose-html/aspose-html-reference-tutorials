---
title: Rendern Sie HTML als PNG in .NET mit Aspose.HTML
linktitle: Rendern Sie HTML als PNG in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie mit Aspose.HTML für .NET arbeiten. Bearbeiten Sie HTML, konvertieren Sie es in verschiedene Formate und mehr. Tauchen Sie ein in dieses umfassende Tutorial!
type: docs
weight: 10
url: /de/net/rendering-html-documents/render-html-as-png/
---

In diesem Tutorial tauchen wir in die Welt von Aspose.HTML für .NET ein, einem leistungsstarken Tool für die programmgesteuerte Arbeit mit HTML-Dokumenten. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst in die Welt der .NET-Programmierung einsteigen, dieses Tutorial führt Sie durch die Grundlagen von Aspose.HTML, vom Importieren von Namespaces bis zum Aufschlüsseln praktischer Beispiele.

## Einführung

Aspose.HTML für .NET ist eine vielseitige Bibliothek, mit der Entwickler HTML-Dokumente mühelos bearbeiten können. Ob Sie HTML in andere Formate konvertieren, Daten aus HTML-Dokumenten extrahieren oder dynamische HTML-Inhalte erstellen müssen, Aspose.HTML bietet alles. In diesem Tutorial werden wir seine Funktionen Schritt für Schritt erkunden.

## Voraussetzungen

Bevor wir uns in die Codebeispiele vertiefen, müssen einige Voraussetzungen erfüllt sein:

1. Visual Studio: Stellen Sie sicher, dass Sie Visual Studio installiert haben, da wir .NET-Code schreiben werden.

2.  Aspose.HTML für .NET: Laden Sie die Aspose.HTML für .NET-Bibliothek herunter und installieren Sie sie von[dieser Link](https://releases.aspose.com/html/net/) Sie können zwischen der kostenlosen Testversion oder dem Kauf einer Lizenz wählen.[Hier](https://purchase.aspose.com/buy).

3. .NET Framework oder .NET Core: Stellen Sie sicher, dass auf Ihrem Entwicklungscomputer je nach Projektanforderungen entweder das .NET Framework oder .NET Core installiert ist.

4. Ein Code-Editor: Sie können Visual Studio oder einen anderen Code-Editor Ihrer Wahl verwenden.

## Namespaces importieren

Um mit Aspose.HTML für .NET zu beginnen, müssen wir zunächst die erforderlichen Namespaces importieren. Öffnen Sie Ihr Projekt in Visual Studio, erstellen Sie eine neue C#-Klasse und importieren Sie die folgenden Namespaces:

```csharp
using Aspose.Html;
using Aspose.Html.Converters;
using Aspose.Html.Rendering;
using Aspose.Html.Rendering.Image;
```

Diese Namespaces bieten Zugriff auf verschiedene Klassen und Methoden, die für die programmgesteuerte Arbeit mit HTML-Dokumenten erforderlich sind.

## HTML als PNG rendern – Beispiel

Schauen wir uns das von Ihnen bereitgestellte Codebeispiel genauer an und unterteilen es in mehrere Schritte:

```csharp
// Rendern Sie HTML als PNG in .NET mit Aspose.HTML
string dataDir = "Your Data Directory";

// Schritt 1: Erstellen Sie ein HTML-Dokumentobjekt
using (var document = new Aspose.Html.HTMLDocument("<style>p { color: green; }</style><p>my first paragraph</p>", @"c:\work\"))
{
    // Schritt 2: Erstellen Sie einen HTML-Renderer
    using (HtmlRenderer renderer = new HtmlRenderer())
    using (ImageDevice device = new ImageDevice(dataDir + @"document_out.png"))
    {
        // Schritt 3: Rendern Sie das HTML-Dokument in PNG
        renderer.Render(device, document);
    }
}
```

### Schritt 1: Erstellen Sie ein HTML-Dokumentobjekt

 In diesem Schritt erstellen wir eine`HTMLDocument` Objekt, das ein HTML-Dokument darstellt. Sie können den HTML-Inhalt als Zeichenfolge an den Konstruktor übergeben und auch den Basispfad zum Auflösen relativer Pfade angeben.

### Schritt 2: Erstellen Sie einen HTML-Renderer

 Hier erstellen wir eine`HtmlRenderer` Objekt. Dies ist die Kernkomponente, die für die Darstellung von HTML-Inhalten verantwortlich ist. 

### Schritt 3: Rendern Sie das HTML-Dokument in PNG

 Zum Schluss rendern wir das HTML-Dokument in ein PNG-Bild mit dem`HtmlRenderer` und ein`ImageDevice` . Das resultierende PNG-Bild wird im angegebenen`dataDir`.

## Abschluss

In diesem Tutorial haben wir Ihnen Aspose.HTML für .NET vorgestellt und eine Aufschlüsselung des Beispielcodes bereitgestellt. Dies ist nur der Anfang dessen, was Sie mit dieser leistungsstarken Bibliothek erreichen können. Sie können die umfangreiche Dokumentation erkunden[Hier](https://reference.aspose.com/html/net/) und greifen Sie auf zusätzliche Ressourcen und Support zu auf der[Aspose-Foren](https://forum.aspose.com/).

Wenn Sie Fragen haben oder Hilfe zu Aspose.HTML für .NET benötigen, können Sie sich gerne an die Aspose-Community wenden oder die Dokumentation für weitere Anleitungen zu Rate ziehen.

## Häufig gestellte Fragen (FAQs)

### Was ist Aspose.HTML für .NET?
   Aspose.HTML für .NET ist eine Bibliothek, die es Entwicklern ermöglicht, HTML-Dokumente programmgesteuert in .NET-Anwendungen zu bearbeiten und zu konvertieren.

### Wie kann ich eine temporäre Lizenz für Aspose.HTML für .NET erhalten?
    Sie können eine temporäre Lizenz für Aspose.HTML für .NET erhalten[Hier](https://purchase.aspose.com/temporary-license/).

### Kann ich HTML mit Aspose.HTML für .NET in andere Formate konvertieren?
   Ja, Aspose.HTML für .NET bietet verschiedene Konverter zum Konvertieren von HTML in Formate wie PDF, XPS und Bilder.

### Gibt es eine kostenlose Testversion für Aspose.HTML für .NET?
    Ja, Sie können eine kostenlose Testversion von Aspose.HTML für .NET herunterladen[Hier](https://releases.aspose.com/).

### Wo finde ich weitere Tutorials und Dokumentationen?
   Sie finden umfassende Dokumentationen und Tutorials auf der[Aspose.HTML für .NET-Dokumentationsseite](https://reference.aspose.com/html/net/).