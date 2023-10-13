---
title: Umgebungskonfiguration in .NET mit Aspose.HTML
linktitle: Umgebungskonfiguration in .NET
second_title: Aspose.Slides .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie mit HTML-Dokumenten in .NET arbeiten und Aspose.HTML für Aufgaben wie Skriptverwaltung, benutzerdefinierte Stile, JavaScript-Ausführungssteuerung und mehr verwenden. Dieses umfassende Tutorial bietet Schritt-für-Schritt-Beispiele und FAQs, um Ihnen den Einstieg zu erleichtern.
type: docs
weight: 10
url: /de/net/advanced-features/environment-configuration/
---

In der heutigen digitalen Welt ist die Erstellung und Bearbeitung von HTML-Dokumenten für viele Entwickler eine grundlegende Aufgabe. Unabhängig davon, ob Sie eine Webanwendung erstellen oder HTML in andere Formate wie PDF oder Bilder konvertieren müssen, ist Aspose.HTML für .NET ein leistungsstarkes Tool, das Sie in Ihrem Toolkit haben sollten. In diesem Tutorial untersuchen wir verschiedene Aspekte von Aspose.HTML für .NET, einschließlich Voraussetzungen, Importieren von Namespaces und Schritt-für-Schritt-Beispielen mit detaillierten Erklärungen.

## Voraussetzungen

Bevor wir uns mit der Verwendung von Aspose.HTML für .NET befassen, müssen Sie sicherstellen, dass die folgenden Voraussetzungen erfüllt sind:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Entwicklungscomputer installiert ist. Aspose.HTML für .NET ist für die nahtlose Zusammenarbeit mit Visual Studio konzipiert.

2.  Aspose.HTML für .NET: Sie können die Aspose.HTML für .NET-Bibliothek von der Website herunterladen. Über den folgenden Link gelangen Sie zur Download-Seite:[Laden Sie Aspose.HTML für .NET herunter](https://releases.aspose.com/html/net/).

3. Installation und Lizenz: Befolgen Sie nach dem Herunterladen der Bibliothek die Installationsanweisungen in der Dokumentation. Möglicherweise benötigen Sie auch eine gültige Lizenz, um einige der erweiterten Funktionen nutzen zu können. Eine Lizenz erhalten Sie auf der Aspose-Website:[Erwerben Sie die Aspose.HTML-Lizenz](https://purchase.aspose.com/buy).

4.  Kostenlose Testversion: Wenn Sie Aspose.HTML vor dem Kauf einer Lizenz ausprobieren möchten, können Sie über diesen Link eine kostenlose Testversion erhalten:[Kostenlose Aspose.HTML-Testversion](https://releases.aspose.com/).

Da Sie nun über die erforderlichen Voraussetzungen verfügen, fahren wir mit dem nächsten Abschnitt fort, in dem wir die erforderlichen Namespaces importieren.

## Namespaces importieren

Um effektiv mit Aspose.HTML für .NET arbeiten zu können, müssen Sie die entsprechenden Namespaces in Ihr Projekt importieren. Nachfolgend listen wir die Namespaces auf, die Sie für die von uns behandelten Beispiele benötigen:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Wenn diese Namespaces importiert sind, können Sie auf die von Aspose.HTML für .NET bereitgestellten Funktionen zugreifen.

## Deaktivieren Sie die Skriptausführung

Beginnen wir mit einem einfachen Beispiel für die Deaktivierung der Skriptausführung in einem HTML-Dokument und dessen Konvertierung in eine PDF-Datei. Folge diesen Schritten:

1. Erstellen Sie ein HTML-Code-Snippet und speichern Sie es in einer Datei mit dem Namen „document.html“.

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Initialisieren Sie die Aspose.HTML-Konfiguration und markieren Sie „Skripte“ als nicht vertrauenswürdige Ressource.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Initialisieren Sie ein HTML-Dokument mit der angegebenen Konfiguration
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konvertieren Sie HTML in PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

In diesem Beispiel haben wir die Ausführung von Skripten innerhalb des HTML-Dokuments verhindert und so die Sicherheit beim Konvertieren in ein PDF gewährleistet. Kommen wir nun zum nächsten Beispiel.

## Geben Sie das Benutzer-Stylesheet an

Manchmal möchten Sie möglicherweise benutzerdefinierte Stile auf Elemente in einem HTML-Dokument anwenden. So können Sie es mit Aspose.HTML für .NET tun:

1. Erstellen Sie ein HTML-Code-Snippet und speichern Sie es in einer Datei mit dem Namen „document.html“.

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  Legen Sie eine benutzerdefinierte Farbe für fest`<span>` Element mithilfe eines Benutzer-Stylesheets.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Initialisieren Sie ein HTML-Dokument mit der angegebenen Konfiguration
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konvertieren Sie HTML in PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 In diesem Beispiel haben wir einen benutzerdefinierten Stil auf angewendet`<span>`Element und setzt seine Textfarbe auf Grün. Aspose.HTML für .NET ermöglicht Ihnen die einfache Bearbeitung von Stilen.

## Zeitüberschreitung bei der JavaScript-Ausführung

Beim Umgang mit potenziell zeitaufwändigem JavaScript-Code ist es wichtig, ein Timeout festzulegen, um eine unbegrenzte Ausführung zu verhindern. So können Sie es machen:

1. Erstellen Sie ein HTML-Code-Snippet mit einer Endlosschleife und speichern Sie es in einer Datei mit dem Namen „document.html“.

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Legen Sie ein Zeitlimit für die JavaScript-Ausführung auf 10 Sekunden fest.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // Initialisieren Sie ein HTML-Dokument mit der angegebenen Konfiguration
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Warten Sie, bis alle Skripte abgeschlossen/abgebrochen sind, und konvertieren Sie HTML in PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

In diesem Beispiel haben wir die JavaScript-Ausführungszeit auf 10 Sekunden begrenzt, um sicherzustellen, dass das Skript nicht unbegrenzt ausgeführt wird, was möglicherweise zu Leistungsproblemen führen könnte.

## Benutzerdefinierter Nachrichtenhandler

Manchmal müssen Sie beim Laden eines HTML-Dokuments möglicherweise mit Fehlermeldungen oder fehlenden Ressourcen umgehen. Hier ist ein Beispiel für die Erstellung eines benutzerdefinierten Nachrichtenhandlers:

1. Erstellen Sie einen HTML-Codeausschnitt mit einem fehlenden Bilddateiverweis und speichern Sie ihn in einer Datei mit dem Namen „document.html“.

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. Fügen Sie dem Netzwerkdienst einen Fehlermeldungshandler hinzu, um fehlgeschlagene Anforderungen zu protokollieren.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // Initialisieren Sie ein HTML-Dokument mit der angegebenen Konfiguration
    // Während des Ladens des Dokuments versucht die Anwendung, das Bild zu laden, und das Ergebnis dieses Vorgangs wird in der Konsole angezeigt.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konvertieren Sie HTML in PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

In diesem Beispiel haben wir einen benutzerdefinierten Nachrichtenhandler hinzugefügt (`LogMessageHandler`), um Informationen über fehlgeschlagene Anfragen zu protokollieren. Dies kann besonders nützlich sein, um fehlende Ressourcen zu debuggen und ordnungsgemäß zu verwalten.

## Abschluss

Aspose.HTML für .NET ist eine vielseitige Bibliothek, die Entwicklern die effiziente Arbeit mit HTML-Dokumenten ermöglicht. In diesem Tutorial haben wir wesentliche Konzepte behandelt und Schritt-für-Schritt-Beispiele für häufige Aufgaben bereitgestellt, darunter Skriptverwaltung, Stylesheet-Anpassung, JavaScript-Ausführungssteuerung und benutzerdefinierte Nachrichtenverarbeitung.

Wenn Sie die in diesem Tutorial beschriebenen Schritte befolgen, können Sie die Leistungsfähigkeit von Aspose.HTML für .NET nutzen, um HTML-Dokumente in Ihren .NET-Anwendungen sicher zu erstellen, zu bearbeiten und zu konvertieren.

## FAQs

### F1: Kann ich Aspose.HTML für .NET verwenden, ohne eine Lizenz zu erwerben?

A1: Ja, Sie können Aspose.HTML für .NET mit einer kostenlosen Testversion testen, aber für einige erweiterte Funktionen ist möglicherweise eine gültige Lizenz erforderlich.

### F2: Wie kann ich eine Lizenz für Aspose.HTML für .NET erhalten?

 A2: Sie können eine Lizenz auf der Aspose-Website erwerben:[Erwerben Sie die Aspose.HTML-Lizenz](https://purchase.aspose.com/buy).

### F3: In welche Formate kann ich HTML-Dokumente mit Aspose.HTML für .NET konvertieren?

A3: Aspose.HTML für .NET unterstützt die Konvertierung in verschiedene Formate, einschließlich PDF, Bilder und mehr.

### F4: Gibt es eine Community oder ein Support-Forum für Aspose.HTML für .NET?

 A4: Ja, Hilfe und Unterstützung finden Sie in den Aspose-Foren:[Aspose.HTML-Supportforum](https://forum.aspose.com/).

### F5: Bietet Aspose.HTML für .NET Dokumentation und Tutorials?

 A5: Ja, Sie können hier auf die Dokumentation zugreifen:[Aspose.HTML für .NET-Dokumentation](https://reference.aspose.com/html/net/).