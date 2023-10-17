---
title: Erstellen eines Dokuments in .NET mit Aspose.HTML
linktitle: Erstellen eines Dokuments in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Entfesseln Sie die Leistungsfähigkeit von Aspose.HTML für .NET. Erfahren Sie, wie Sie mit Leichtigkeit HTML- und SVG-Dokumente erstellen, bearbeiten und optimieren. Entdecken Sie Schritt-für-Schritt-Beispiele und FAQs.
type: docs
weight: 14
url: /de/net/html-document-manipulation/creating-a-document/
---

In der sich ständig weiterentwickelnden Welt der Webentwicklung ist es wichtig, immer einen Schritt voraus zu sein. Aspose.HTML für .NET bietet Entwicklern ein robustes Toolkit für die Arbeit mit HTML-Dokumenten. Ganz gleich, ob Sie bei Null anfangen, aus einer Datei laden, von einer URL abrufen oder SVG-Dokumente bearbeiten, diese Bibliothek bietet die Vielseitigkeit, die Sie brauchen.

In dieser Schritt-für-Schritt-Anleitung befassen wir uns mit den Grundlagen der Verwendung von Aspose.HTML für .NET und stellen sicher, dass Sie für den Einsatz dieses leistungsstarken Tools in Ihren Webentwicklungsprojekten bestens gerüstet sind. Bevor wir uns mit den Details befassen, gehen wir die Voraussetzungen und die notwendigen Namespaces durch, um Ihre Reise in Gang zu bringen.

## Voraussetzungen

Um diesem Tutorial erfolgreich zu folgen und die Leistungsfähigkeit von Aspose.HTML für .NET zu nutzen, benötigen Sie die folgenden Voraussetzungen:

- Ein Windows-Computer mit installiertem .NET Framework oder .NET Core.
- Ein Code-Editor wie Visual Studio.
- Grundkenntnisse der C#-Programmierung.

Nachdem Sie nun alle Voraussetzungen geschaffen haben, können wir beginnen.

## Namespaces importieren

Bevor Sie Aspose.HTML für .NET verwenden, müssen Sie die erforderlichen Namespaces importieren. Diese Namespaces enthalten Klassen und Methoden, die für die Arbeit mit HTML-Dokumenten unerlässlich sind. Nachfolgend finden Sie eine Liste der Namespaces, die Sie importieren sollten:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Nachdem diese Namespaces importiert wurden, können Sie nun in die Schritt-für-Schritt-Beispiele eintauchen.

## Erstellen eines HTML-Dokuments von Grund auf

### Schritt 1: Initialisieren Sie ein leeres HTML-Dokument

```csharp
// Initialisieren Sie ein leeres HTML-Dokument.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Erstellen Sie ein Textelement und fügen Sie es dem Dokument hinzu
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Speichern Sie das Dokument auf der Festplatte.
    document.Save("document.html");
}
```

In diesem Beispiel erstellen wir zunächst ein leeres HTML-Dokument und fügen ein „Hello World!“ hinzu. Text dazu. Anschließend speichern wir das Dokument in einer Datei.

## Erstellen eines HTML-Dokuments aus einer Datei

### Schritt 1: Bereiten Sie eine Datei „document.html“ vor

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Schritt 2: Aus einer „document.html“-Datei laden

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Schreiben Sie den Dokumentinhalt in den Ausgabestream.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Hier bereiten wir eine Datei mit „Hello World!“ vor. Inhalt und laden Sie ihn dann als HTML-Dokument. Wir drucken den Inhalt des Dokuments auf der Konsole aus.

## Erstellen eines HTML-Dokuments aus einer URL

### Schritt 1: Laden Sie ein Dokument von einer Webseite

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Schreiben Sie den Dokumentinhalt in den Ausgabestream.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

In diesem Beispiel laden wir ein HTML-Dokument direkt von einer Webseite und zeigen dessen Inhalt an.

## Erstellen eines HTML-Dokuments aus einem String

### Schritt 1: Bereiten Sie einen HTML-Code vor

```csharp
var html_code = "<p>Hello World!</p>";
```

### Schritt 2: Dokument aus der String-Variablen initialisieren

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Speichern Sie das Dokument auf der Festplatte.
    document.Save("document.html");
}
```

Hier erstellen wir ein HTML-Dokument aus einer String-Variablen und speichern es in einer Datei.

## Erstellen eines HTML-Dokuments aus einem MemoryStream

### Schritt 1: Erstellen Sie ein Speicherstreamobjekt

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Schreiben Sie den HTML-Code in das Speicherobjekt
    sw.Write("<p>Hello World!</p>");
    // Stellen Sie die Position auf den Anfang ein
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Dokument aus dem Speicherstrom initialisieren
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Speichern Sie das Dokument auf der Festplatte.
        document.Save("document.html");
    }
}
```

In diesem Beispiel erstellen wir ein HTML-Dokument aus einem Speicherstream und speichern es in einer Datei.

## Arbeiten mit SVG-Dokumenten

### Schritt 1: Initialisieren Sie das SVG-Dokument aus einer Zeichenfolge

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Schreiben Sie den Dokumentinhalt in den Ausgabestream.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Hier erstellen und zeigen wir ein SVG-Dokument aus einer Zeichenfolge an.

## Asynchrones Laden eines HTML-Dokuments

### Schritt 1: Erstellen Sie die Instanz des HTML-Dokuments

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Schritt 2: Abonnieren Sie das Ereignis „ReadyStateChange“.

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //Überprüfen Sie den Wert der Eigenschaft „ReadyState“.
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Schritt 3: Navigieren Sie asynchron zum angegebenen Uri

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

In diesem Beispiel laden wir ein HTML-Dokument asynchron und verarbeiten das Ereignis „ReadyStateChange“, um den Inhalt anzuzeigen, wenn der Ladevorgang abgeschlossen ist.

## Behandeln des „OnLoad“-Ereignisses

### Schritt 1: Erstellen Sie die Instanz des HTML-Dokuments

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Schritt 2: Abonnieren Sie das „OnLoad“-Event

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Schritt 3: Navigieren Sie asynchron zum angegebenen Uri

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Dieses Beispiel zeigt das asynchrone Laden eines HTML-Dokuments und die Verarbeitung des „OnLoad“-Ereignisses, um den Inhalt nach Abschluss anzuzeigen.

## Abschließend

In der dynamischen Welt der Webentwicklung ist es entscheidend, über die richtigen Tools zu verfügen. Aspose.HTML für .NET bietet Ihnen die Möglichkeit, HTML- und SVG-Dokumente effizient zu erstellen, zu bearbeiten und zu verarbeiten. Dieser umfassende Leitfaden hat Sie durch das Wesentliche geführt und sichergestellt, dass Sie die Leistungsfähigkeit von Aspose.HTML für .NET in Ihren Projekten nutzen können.

## FAQs

### F1: Was ist Aspose.HTML für .NET?

A1: Aspose.HTML für .NET ist eine leistungsstarke .NET-Bibliothek, die Entwicklern die Arbeit mit HTML- und SVG-Dokumenten ermöglicht. Es bietet eine breite Palette von Funktionen, von der Erstellung von Dokumenten bis hin zum Parsen und Bearbeiten vorhandener HTML- und SVG-Dateien.

### F2: Kann ich Aspose.HTML für .NET mit .NET Core verwenden?

A2: Ja, Aspose.HTML für .NET ist sowohl mit .NET Framework als auch mit .NET Core kompatibel, was es zu einer vielseitigen Wahl für moderne .NET-Anwendungen macht.

### F3: Ist Aspose.HTML für .NET für Web Scraping und Parsing geeignet?

A3: Auf jeden Fall! Aspose.HTML für .NET ist dank seiner Fähigkeit, HTML-Dokumente aus URLs und Zeichenfolgen zu laden, eine ausgezeichnete Wahl für Web-Scraping- und Parsing-Aufgaben. Sie können Daten extrahieren, Analysen durchführen und mehr.

### F4: Wie kann ich auf die Unterstützung für Aspose.HTML für .NET zugreifen?

 A4: Wenn Sie bei der Verwendung von Aspose.HTML für .NET auf Probleme stoßen oder Fragen haben, können Sie die besuchen[Aspose-Forum](https://forum.aspose.com/) für die Unterstützung und Unterstützung durch die Community und Aspose-Experten.

### A5: Wo finde ich ausführliche Dokumentation und Download-Optionen?

A5: Eine umfassende Dokumentation und Zugriff auf Download-Optionen finden Sie unter den folgenden Links:

- [Dokumentation](https://reference.aspose.com/html/net/)
- [Herunterladen](https://releases.aspose.com/html/net/)
- [Kaufen](https://purchase.aspose.com/buy)
- [Kostenlose Testphase](https://releases.aspose.com/)
- [Temporäre Lizenz](https://purchase.aspose.com/temporary-license/)