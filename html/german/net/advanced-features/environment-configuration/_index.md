---
title: Umgebungskonfiguration in .NET mit Aspose.HTML
linktitle: Umgebungskonfiguration in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie mit Aspose.HTML mit HTML-Dokumenten in .NET für Aufgaben wie Skriptverwaltung, benutzerdefinierte Stile, JavaScript-Ausführungssteuerung und mehr arbeiten. Dieses umfassende Tutorial bietet schrittweise Beispiele und FAQs, um Ihnen den Einstieg zu erleichtern.
weight: 10
url: /de/net/advanced-features/environment-configuration/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Umgebungskonfiguration in .NET mit Aspose.HTML


In der heutigen digitalen Welt ist das Erstellen und Bearbeiten von HTML-Dokumenten für viele Entwickler eine grundlegende Aufgabe. Egal, ob Sie eine Webanwendung erstellen oder HTML in andere Formate wie PDF oder Bilder konvertieren müssen, Aspose.HTML für .NET ist ein leistungsstarkes Tool, das in Ihrem Toolkit nicht fehlen darf. In diesem Tutorial werden wir verschiedene Aspekte von Aspose.HTML für .NET untersuchen, darunter Voraussetzungen, Importieren von Namespaces und schrittweise Beispiele mit detaillierten Erklärungen.

## Voraussetzungen

Bevor wir uns mit der Verwendung von Aspose.HTML für .NET befassen, müssen Sie sicherstellen, dass die folgenden Voraussetzungen erfüllt sind:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Entwicklungscomputer installiert ist. Aspose.HTML für .NET ist für die nahtlose Zusammenarbeit mit Visual Studio konzipiert.

2.  Aspose.HTML für .NET: Sie können die Bibliothek Aspose.HTML für .NET von der Website herunterladen. Verwenden Sie den folgenden Link, um auf die Download-Seite zuzugreifen:[Laden Sie Aspose.HTML für .NET herunter](https://releases.aspose.com/html/net/).

3.  Installation und Lizenz: Folgen Sie nach dem Herunterladen der Bibliothek den Installationsanweisungen in der Dokumentation. Möglicherweise benötigen Sie auch eine gültige Lizenz, um einige der erweiterten Funktionen nutzen zu können. Sie können eine Lizenz von der Aspose-Website erhalten:[Kaufen Sie eine Aspose.HTML-Lizenz](https://purchase.aspose.com/buy).

4.  Kostenlose Testversion: Wenn Sie Aspose.HTML vor dem Kauf einer Lizenz ausprobieren möchten, können Sie unter diesem Link eine kostenlose Testversion erhalten:[Kostenlose Testversion von Aspose.HTML](https://releases.aspose.com/).

Nachdem Sie nun über die erforderlichen Voraussetzungen verfügen, fahren wir mit dem nächsten Abschnitt fort, in dem wir die erforderlichen Namespaces importieren.

## Namespaces importieren

Um effektiv mit Aspose.HTML für .NET arbeiten zu können, müssen Sie die entsprechenden Namespaces in Ihr Projekt importieren. Im Folgenden listen wir die Namespaces auf, die Sie für die Beispiele benötigen, die wir behandeln:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Mit diesen importierten Namespaces können Sie auf die von Aspose.HTML für .NET bereitgestellte Funktionalität zugreifen.

## Skriptausführung deaktivieren

Beginnen wir mit einem einfachen Beispiel für die Deaktivierung der Skriptausführung in einem HTML-Dokument und dessen Konvertierung in ein PDF. Führen Sie die folgenden Schritte aus:

1. Erstellen Sie einen HTML-Codeausschnitt und speichern Sie ihn in einer Datei mit dem Namen „document.html“.

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

In diesem Beispiel haben wir die Ausführung von Skripten im HTML-Dokument verhindert und so die Sicherheit bei der Konvertierung in ein PDF gewährleistet. Fahren wir nun mit dem nächsten Beispiel fort.

## Benutzer-Stylesheet angeben

Manchmal möchten Sie benutzerdefinierte Stile auf Elemente in einem HTML-Dokument anwenden. So können Sie dies mit Aspose.HTML für .NET tun:

1. Erstellen Sie einen HTML-Codeausschnitt und speichern Sie ihn in einer Datei mit dem Namen „document.html“.

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  Legen Sie eine benutzerdefinierte Farbe fest für`<span>` Element mithilfe eines Benutzer-Stylesheets.

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

 In diesem Beispiel haben wir einen benutzerdefinierten Stil angewendet auf die`<span>` Element, indem die Textfarbe auf Grün gesetzt wird. Mit Aspose.HTML für .NET können Sie Stile ganz einfach bearbeiten.

## JavaScript-Ausführungstimeout

Beim Umgang mit potenziell zeitaufwändigem JavaScript-Code ist es wichtig, ein Timeout festzulegen, um eine unbegrenzte Ausführung zu verhindern. So können Sie das tun:

1. Erstellen Sie einen HTML-Codeausschnitt mit einer Endlosschleife und speichern Sie ihn in einer Datei mit dem Namen „document.html“.

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Legen Sie für die JavaScript-Ausführung ein Timeout von 10 Sekunden fest.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // Initialisieren Sie ein HTML-Dokument mit der angegebenen Konfiguration
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Warten Sie, bis alle Skripte abgeschlossen/abgebrochen sind und konvertieren Sie HTML in PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

In diesem Beispiel haben wir die JavaScript-Ausführungszeit auf 10 Sekunden begrenzt, um sicherzustellen, dass das Skript nicht unbegrenzt ausgeführt wird, was möglicherweise zu Leistungsproblemen führen könnte.

## Benutzerdefinierter Nachrichtenhandler

Manchmal müssen Sie beim Laden eines HTML-Dokuments Fehlermeldungen oder fehlende Ressourcen verarbeiten. Hier ist ein Beispiel für die Erstellung eines benutzerdefinierten Nachrichtenhandlers:

1. Erstellen Sie einen HTML-Codeausschnitt mit einer fehlenden Bilddateireferenz und speichern Sie ihn in einer Datei mit dem Namen „document.html“.

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
    // Während das Dokument geladen wird, versucht die Anwendung, das Bild zu laden, und wir sehen das Ergebnis dieses Vorgangs in der Konsole.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Konvertieren Sie HTML in PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

In diesem Beispiel haben wir einen benutzerdefinierten Nachrichtenhandler hinzugefügt (`LogMessageHandler`), um Informationen zu fehlgeschlagenen Anfragen zu protokollieren. Dies kann insbesondere beim Debuggen und beim ordnungsgemäßen Umgang mit fehlenden Ressourcen nützlich sein.

## Abschluss

Aspose.HTML für .NET ist eine vielseitige Bibliothek, die Entwicklern die effiziente Arbeit mit HTML-Dokumenten ermöglicht. In diesem Tutorial haben wir wichtige Konzepte behandelt und schrittweise Beispiele für gängige Aufgaben bereitgestellt, darunter Skriptverwaltung, Stylesheet-Anpassung, JavaScript-Ausführungskontrolle und benutzerdefinierte Nachrichtenverarbeitung.

Indem Sie die in diesem Tutorial beschriebenen Schritte befolgen, können Sie die Leistungsfähigkeit von Aspose.HTML für .NET nutzen, um HTML-Dokumente in Ihren .NET-Anwendungen sicher zu erstellen, zu bearbeiten und zu konvertieren.

## Häufig gestellte Fragen

### F1: Kann ich Aspose.HTML für .NET verwenden, ohne eine Lizenz zu erwerben?

A1: Ja, Sie können Aspose.HTML für .NET mit einer kostenlosen Testversion ausprobieren, aber für einige erweiterte Funktionen ist möglicherweise eine gültige Lizenz erforderlich.

### F2: Wie kann ich eine Lizenz für Aspose.HTML für .NET erhalten?

 A2: Sie können eine Lizenz von der Aspose-Website erwerben:[Kaufen Sie eine Aspose.HTML-Lizenz](https://purchase.aspose.com/buy).

### F3: In welche Formate kann ich HTML-Dokumente mit Aspose.HTML für .NET konvertieren?

A3: Aspose.HTML für .NET unterstützt die Konvertierung in verschiedene Formate, darunter PDF, Bilder und mehr.

### F4: Gibt es eine Community oder ein Supportforum für Aspose.HTML für .NET?

 A4: Ja, Sie finden Hilfe und Unterstützung in den Aspose-Foren:[Aspose.HTML Support Forum](https://forum.aspose.com/).

### F5: Bietet Aspose.HTML für .NET Dokumentation und Tutorials?

 A5: Ja, Sie können hier auf die Dokumentation zugreifen:[Aspose.HTML für .NET-Dokumentation](https://reference.aspose.com/html/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
