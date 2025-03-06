---
title: Speichern eines Dokuments in .NET mit Aspose.HTML
linktitle: Speichern eines Dokuments in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Entfesseln Sie die Leistungsfähigkeit von Aspose.HTML für .NET mit unserer Schritt-für-Schritt-Anleitung. Lernen Sie, HTML- und SVG-Dokumente zu erstellen, zu bearbeiten und zu konvertieren
weight: 16
url: /de/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Speichern eines Dokuments in .NET mit Aspose.HTML


Im heutigen digitalen Zeitalter ist das Erstellen und Bearbeiten von HTML- und SVG-Dokumenten für viele Softwareentwickler und Unternehmen unverzichtbar. Aspose.HTML für .NET ist eine leistungsstarke Bibliothek, die diese Aufgaben vereinfacht und verschiedene Funktionen für die Arbeit mit HTML, SVG und mehr bietet. In diesem umfassenden Handbuch tauchen wir in die Grundlagen von Aspose.HTML für .NET ein und unterteilen jedes Beispiel in leicht verständliche Schritte. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, dieses Handbuch wird Ihnen bei der Nutzung der Funktionen von Aspose.HTML von unschätzbarem Wert sein.

## Voraussetzungen

Bevor wir uns auf diese Reise begeben, stellen wir sicher, dass Sie alles haben, was Sie brauchen:

- Entwicklungsumgebung: Stellen Sie sicher, dass Visual Studio oder eine andere .NET-Entwicklungsumgebung auf Ihrem Computer installiert ist.

- Aspose.HTML für .NET: Sie müssen die Bibliothek Aspose.HTML für .NET herunterladen. Sie können sie hier herunterladen:[Hier](https://releases.aspose.com/html/net/).

- Kenntnisse in C#: Kenntnisse in der Programmiersprache C# sind von Vorteil, aber nicht zwingend erforderlich. Dieses Handbuch ist anfängerfreundlich gestaltet.

## Namespace importieren

Um Aspose.HTML für .NET zu verwenden, müssen Sie die erforderlichen Namespaces in Ihr Projekt importieren. Fügen Sie in Ihren C#-Code den folgenden Namespace ein:

### Schritt 1: Aspose.HTML-Namespace importieren
```csharp
using Aspose.Html;
```

Dieser Namespace gewährt Ihnen Zugriff auf verschiedene HTML- und SVG-Bearbeitungsfunktionen.

## HTML in Datei

### Schritt 1: Initialisieren Sie ein leeres HTML-Dokument
```csharp
// Initialisieren Sie ein leeres HTML-Dokument.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Erstellen Sie ein Textelement und fügen Sie es dem Dokument hinzu
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Speichern Sie das HTML in der Datei auf der Festplatte.
    document.Save("document.html");
}
```

In diesem Beispiel erstellen wir ein HTML-Dokument und fügen einen einfachen „Hallo Welt!“-Text hinzu. Anschließend speichern wir das HTML in einer Datei auf der Festplatte.

## HTML ohne verknüpfte Datei

### Schritt 1: Bereiten Sie eine einfache HTML-Datei vor
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Hier erstellen wir eine einfache HTML-Datei mit einem Ankerlink zu einer anderen Datei.

### Schritt 2: Laden Sie „document.html“ in den Speicher
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Instanz „Save Options“ erstellen
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Setzen Sie die maximale Verarbeitungstiefe auf 0, um verknüpfte HTML-Dateien abzuschneiden.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Speichern des Dokuments
    document.Save(@".\html-to-file-example\document.html", options);
}
```

In diesem Beispiel laden wir ein HTML-Dokument in den Speicher, legen die maximale Verarbeitungstiefe fest, um verknüpfte Dateien abzuschneiden, und speichern das Dokument. 

## HTML zu MHTML

### Schritt 1: Bereiten Sie eine einfache HTML-Datei vor
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Genau wie in Beispiel 2 erstellen wir eine einfache HTML-Datei mit einem Ankerlink zu einer anderen Datei.

### Schritt 2: Laden Sie „document.html“ in den Speicher und speichern Sie es als MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Speichern Sie das Dokument als MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Hier laden wir das HTML-Dokument in den Speicher und speichern es im MHTML-Format.

## HTML zu Markdown

### Schritt 1: Bereiten Sie einen HTML-Code vor
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 In diesem Schritt definieren wir einen HTML-Codeausschnitt mit einem`<H2>` Element.

### Schritt 2: Dokument aus HTML-Code initialisieren und als Markdown speichern
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Speichern Sie das Dokument als Markdown-Datei.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Aus dem Code-Schnipsel erstellen wir ein HTML-Dokument und speichern es als Markdown-Datei ab.

## SVG in Datei

### Schritt 1: Bereiten Sie einen SVG-Code vor
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' Höhe='80' Breite='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Hier erstellen wir einen SVG-Code, der eine einfache, farbenfrohe Grafik zeichnet.

### Schritt 2: Initialisieren Sie ein SVG-Dokument aus dem Code und speichern Sie es auf der Festplatte
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Speichern Sie die SVG-Datei auf der Festplatte
    document.Save("document.svg");
}
```

In diesem Schritt erstellen wir aus dem Code ein SVG-Dokument und speichern es als SVG-Datei.

## Abschluss

Aspose.HTML für .NET ist eine vielseitige Bibliothek, die die Handhabung von HTML- und SVG-Dokumenten in Ihren .NET-Anwendungen vereinfacht. In diesem Handbuch haben wir fünf wichtige Beispiele behandelt und jedes in schrittweise Anleitungen unterteilt. Egal, ob Sie Dokumente erstellen, bearbeiten oder konvertieren, Aspose.HTML bietet alles. Wenn Sie diese Schritte befolgen, sind Sie auf dem besten Weg, dieses leistungsstarke Tool zu beherrschen.

## Häufig gestellte Fragen

### F1: Was ist Aspose.HTML für .NET?

A1: Aspose.HTML für .NET ist eine .NET-Bibliothek, die eine breite Palette an Funktionen für die Arbeit mit HTML- und SVG-Dokumenten bietet, einschließlich Erstellung, Bearbeitung und Konvertierung.

### F2: Wo kann ich Aspose.HTML für .NET herunterladen?

 A2: Sie können Aspose.HTML für .NET herunterladen von[Hier](https://releases.aspose.com/html/net/).

### F3: Ist Aspose.HTML für .NET für Anfänger geeignet?

A3: Ja, Aspose.HTML für .NET kann sowohl von Anfängern als auch von erfahrenen Entwicklern verwendet werden. Die Beispiele in diesem Handbuch sind anfängerfreundlich gestaltet.

### F4: Kann ich HTML mit Aspose.HTML für .NET in andere Formate konvertieren?

A4: Ja, Aspose.HTML für .NET unterstützt die Konvertierung in verschiedene Formate, einschließlich MHTML und Markdown, wie in den Beispielen gezeigt.

### F5: Wo erhalte ich Support für Aspose.HTML für .NET?

 A5: Support und Antworten auf Ihre Fragen finden Sie im Aspose.HTML-Community-Forum[Hier](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
