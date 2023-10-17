---
title: Konvertieren Sie HTML in MHTML in .NET mit Aspose.HTML
linktitle: Konvertieren Sie HTML in MHTML in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Konvertieren Sie HTML in MHTML in .NET mit Aspose.HTML – Eine Schritt-für-Schritt-Anleitung für die effiziente Archivierung von Webinhalten. Erfahren Sie, wie Sie mit Aspose.HTML für .NET MHTML-Archive erstellen.
type: docs
weight: 19
url: /de/net/html-extensions-and-conversions/convert-html-to-mhtml/
---

In der Welt der Webentwicklung ist eine effiziente Dokumentenkonvertierung von entscheidender Bedeutung. Die Bibliothek Aspose.HTML für .NET ist ein leistungsstarkes Tool, das die Konvertierung von HTML-Dokumenten in verschiedene Formate, einschließlich MHTML, vereinfacht. MHTML, kurz für „MIME HTML“, ist ein Webseitenarchivformat, mit dem Sie eine Webseite und ihre Ressourcen in einer einzigen Datei speichern können. In dieser Schritt-für-Schritt-Anleitung führen wir Sie durch den Prozess der Konvertierung eines HTML-Dokuments in MHTML mit Aspose.HTML für .NET.

## Voraussetzungen

Bevor wir mit dem Konvertierungsprozess beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

### 1. Aspose.HTML für .NET-Bibliothek

 Sie müssen die Aspose.HTML für .NET-Bibliothek installiert haben. Wenn Sie dies noch nicht getan haben, können Sie es von der Website herunterladen[Hier](https://releases.aspose.com/html/net/). Befolgen Sie die Installationsanweisungen auf der Website.

### 2. Beispiel-HTML-Dokument

Um die Konvertierung durchzuführen, benötigen Sie ein HTML-Dokument, mit dem Sie arbeiten können. Stellen Sie sicher, dass Sie eine Beispiel-HTML-Datei bereit haben. Sie können Ihr eigenes HTML-Dokument verwenden oder ein Beispiel von herunterladen[Aspose.HTML-Dokumentation](https://reference.aspose.com/html/net/).

Nachdem Sie nun die Voraussetzungen geschaffen haben, können wir mit der Konvertierung fortfahren.

## Namespace importieren

Zunächst müssen Sie die erforderlichen Namespaces in Ihren C#-Code importieren. Dies ist für den Zugriff auf die von der Aspose.HTML-Bibliothek bereitgestellten Klassen und Methoden unerlässlich.

### Importieren Sie den erforderlichen Namespace

```csharp
using Aspose.Html;
```

Nachdem Sie nun den erforderlichen Namespace importiert haben, können Sie mit dem eigentlichen Konvertierungsprozess fortfahren.

Der Übersichtlichkeit halber unterteilen wir die Konvertierung eines HTML-Dokuments in MHTML in mehrere Schritte.

## Laden Sie das HTML-Dokument

```csharp
string dataDir = "Your Data Directory"; // Geben Sie Ihr Datenverzeichnis an
HTMLDocument htmlDocument = new HTMLDocument(dataDir + "input.html"); // Laden Sie das HTML-Dokument
```

In diesem Schritt geben Sie den Pfad zu Ihrem HTML-Dokument an. Aspose.HTML lädt die HTML-Datei und macht sie für die Konvertierung bereit.

## Initialisieren Sie MHTMLSaveOptions

```csharp
MHTMLSaveOptions options = new MHTMLSaveOptions();
```

 Hier initialisieren Sie die`MHTMLSaveOptions` Klasse, die Optionen für die MHTML-Konvertierung bereitstellt.

## Legen Sie Regeln für die Ressourcenhandhabung fest

```csharp
options.ResourceHandlingOptions.MaxHandlingDepth = 1;
```

Sie können Regeln für die Ressourcenhandhabung basierend auf Ihren Anforderungen festlegen. In diesem Beispiel begrenzen wir die maximale Verarbeitungstiefe auf 1, was bedeutet, dass nur das Haupt-HTML-Dokument und seine unmittelbaren Ressourcen in die MHTML-Datei aufgenommen werden.

## Geben Sie den Ausgabepfad an

```csharp
string outputMHTML = dataDir + "HTMLtoMHTML_Output.mht"; // Geben Sie den Pfad der Ausgabedatei an
```

In diesem Schritt geben Sie den Pfad für die resultierende MHTML-Datei an. Hier wird das konvertierte MHTML-Dokument gespeichert.

## Führen Sie die Konvertierung durch

```csharp
Converter.ConvertHTML(htmlDocument, options, outputMHTML);
```

 Jetzt ist es an der Zeit, das HTML-Dokument in MHTML zu konvertieren. Der`ConvertHTML` Die Methode verwendet das geladene HTML-Dokument, die von Ihnen festgelegten Optionen und den Pfad der Ausgabedatei als Parameter.

Glückwunsch! Sie haben ein HTML-Dokument mit Aspose.HTML für .NET erfolgreich in MHTML konvertiert. Sie können nun über den angegebenen Ausgabepfad auf die MHTML-Datei zugreifen.

## Abschluss

Die effiziente Konvertierung von HTML-Dokumenten in das MHTML-Format ist eine wertvolle Fähigkeit für Webentwickler und Inhaltsersteller. Aspose.HTML für .NET vereinfacht diesen Prozess und macht ihn zugänglich und benutzerfreundlich. Wenn Sie der oben beschriebenen Schritt-für-Schritt-Anleitung folgen, können Sie mühelos MHTML-Archive Ihrer Webinhalte erstellen.

Lassen Sie uns nun einige häufig gestellte Fragen (FAQs) beantworten, um weitere Klarheit zu diesem Thema zu schaffen.

## FAQs

### Was ist MHTML und warum wird es verwendet?

MHTML, kurz für „MIME HTML“, ist ein Webseitenarchivformat, mit dem Sie eine Webseite und ihre Ressourcen in einer einzigen Datei speichern können. Es wird häufig zum Archivieren von Webinhalten, zum Teilen von Webseiten als einzelne Dateien und zum Sicherstellen, dass alle Ressourcen (Bilder, Stylesheets usw.) enthalten sind, auch wenn sie auf verschiedenen Servern gehostet werden, verwendet.

### Kann ich die Ressourcenverwaltung bei der Konvertierung in MHTML anpassen?

 Ja, du kannst. Wie im Beispiel gezeigt, können Sie mit dem Ressourcenhandhabungsregeln festlegen`ResourceHandlingOptions` des`MHTMLSaveOptions`Klasse. Sie können die Tiefe steuern, in der Ressourcen in die MHTML-Datei einbezogen werden.

### Wo finde ich weitere Ressourcen und Dokumentation für Aspose.HTML für .NET?

 Sie können die erkunden[Aspose.HTML-Dokumentation](https://reference.aspose.com/html/net/) für ausführliche Informationen, Tutorials und API-Referenzen. Darüber hinaus ist die[Aspose.HTML-Forum](https://forum.aspose.com/) ist ein großartiger Ort, um Hilfe zu suchen und alle Probleme oder Fragen zu besprechen, die Sie möglicherweise haben.

### Gibt es eine kostenlose Testversion für Aspose.HTML für .NET?

 Ja, Sie können eine kostenlose Testversion von Aspose.HTML für .NET erhalten, indem Sie hier klicken[dieser Link](https://releases.aspose.com/). Mit der Testversion können Sie die Funktionen der Bibliothek erkunden, bevor Sie einen Kauf tätigen.

### Wie erhalte ich eine temporäre Lizenz für Aspose.HTML für .NET?

 Wenn Sie eine temporäre Lizenz benötigen, können Sie diese bei der erhalten[Aspose.Purchase-Website](https://purchase.aspose.com/temporary-license/). Mit dieser temporären Lizenz erhalten Sie für einen begrenzten Zeitraum Zugriff auf die volle Funktionalität der Bibliothek.

