---
title: Verwenden von HTML-Vorlagen in .NET mit Aspose.HTML
linktitle: Verwendung von HTML-Vorlagen in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie Aspose.HTML für .NET verwenden, um HTML-Dokumente dynamisch aus JSON-Daten zu generieren. Nutzen Sie die Möglichkeiten der HTML-Manipulation in Ihren .NET-Anwendungen.
type: docs
weight: 17
url: /de/net/advanced-features/using-html-templates/
---

Wenn Sie in Ihren .NET-Anwendungen mit HTML-Dokumenten und -Vorlagen arbeiten möchten, sind Sie hier richtig! Aspose.HTML für .NET ist eine vielseitige Bibliothek, die Entwicklern die mühelose Bearbeitung von HTML-Dokumenten und -Vorlagen ermöglicht. In diesem Tutorial befassen wir uns mit den Grundlagen der Verwendung von Aspose.HTML für .NET, schlüsseln jeden Schritt auf und geben nebenbei eine klare Erklärung.

## Voraussetzungen

Bevor wir uns mit den Einzelheiten von Aspose.HTML für .NET befassen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Sie können es von der Website herunterladen, falls Sie es noch nicht haben.

2.  Aspose.HTML für .NET: Sie müssen Aspose.HTML für .NET in Ihrem Visual Studio-Projekt installiert haben. Sie können es bei der erhalten[Dokumentation](https://reference.aspose.com/html/net/).

3. JSON-Daten: Bereiten Sie eine JSON-Datenquelle vor, die Sie zum Füllen Ihrer HTML-Vorlage verwenden möchten. Für dieses Tutorial verwenden wir die folgenden JSON-Daten:

```json
{
    'FirstName': 'John',
    'LastName': 'Smith',
    'Address': {
        'City': 'Dallas',
        'Street': 'Austin rd.',
        'Number': '200'
    }
}
```

4. HTML-Vorlage: Erstellen Sie eine HTML-Vorlage, die Sie mit den JSON-Daten füllen möchten. Hier ist ein einfaches Beispiel:

```html
<table border=1>
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
```

## Namensräume importieren

Als Erstes importieren wir die erforderlichen Namespaces in Ihr .NET-Projekt:

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Loading;
```

Nachdem wir nun die Voraussetzungen abgedeckt und die erforderlichen Namespaces importiert haben, wollen wir jeden Schritt im Detail aufschlüsseln.

## Schritt 1: Bereiten Sie eine JSON-Datenquelle vor

Erstellen Sie zunächst eine JSON-Datenquelle, die die Informationen enthält, die Sie in Ihre HTML-Vorlage einfügen möchten. In diesem Beispiel haben wir bereits eine JSON-Datenquelle vorbereitet, wie in den Voraussetzungen erwähnt. Speichern Sie es in einer Datei, zum Beispiel „data-source.json“.

```csharp
var data = @"{
    'FirstName': 'John',
    'LastName': 'Smith',
    'Address': {
        'City': 'Dallas',
        'Street': 'Austin rd.',
        'Number': '200'
    }
}";
System.IO.File.WriteAllText("data-source.json", data);
```

Dieses Code-Snippet liest die JSON-Daten und schreibt sie in eine Datei mit dem Namen „data-source.json“.

## Schritt 2: Bereiten Sie eine HTML-Vorlage vor

Erstellen wir nun eine HTML-Vorlage, die Sie mit den JSON-Daten füllen möchten. Speichern Sie diese Vorlage in einer Datei, z. B. „template.html“.

```csharp
var template = @"
<table border=1>
    <tr>
        <th>Person</th>
        <th>Address</th>
    </tr>
    <tr>
        <td>{{FirstName}} {{LastName}}</td>
        <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
    </tr>
</table>
";
System.IO.File.WriteAllText("template.html", template);
```

 Diese HTML-Vorlage enthält Platzhalter wie`{{FirstName}}`, `{{LastName}}`, `{{Address.Street}}`, `{{Address.Number}}` Und`{{Address.City}}`, die wir durch die tatsächlichen Daten ersetzen.

## Schritt 3: Füllen Sie die HTML-Vorlage aus

 Rufen Sie abschließend die auf`Converter.ConvertTemplate` -Methode, um Ihre HTML-Vorlage mit den Daten aus der JSON-Quelle zu füllen.

```csharp
Aspose.Html.Converters.Converter.ConvertTemplate(
"template.html", new Aspose.Html.Converters.TemplateData("data-source.json"), new Aspose.Html.Loading.TemplateLoadOptions(), "document.html"
);
```

Dieser Code verwendet die Datei „template.html“, ersetzt die Platzhalter durch die entsprechenden JSON-Werte und speichert das Ergebnis in „document.html“.

Glückwunsch! Sie haben die Leistungsfähigkeit von Aspose.HTML für .NET erfolgreich genutzt, um HTML-Dokumente dynamisch aus JSON-Daten zu generieren.

## Abschluss

In diesem Tutorial haben wir die Grundlagen der Verwendung von Aspose.HTML für .NET zum dynamischen Erstellen von HTML-Dokumenten untersucht. Wir haben die Voraussetzungen, das Importieren von Namespaces und die detaillierte Aufschlüsselung der einzelnen Schritte behandelt. Wenn Sie diese Schritte befolgen, können Sie die HTML-Dokumentgenerierung nahtlos in Ihre .NET-Anwendungen integrieren.

## FAQs

### Q1. Was ist Aspose.HTML für .NET?

A1: Aspose.HTML für .NET ist eine leistungsstarke Bibliothek, die es .NET-Entwicklern ermöglicht, programmgesteuert mit HTML-Dokumenten und -Vorlagen zu arbeiten. Es vereinfacht Aufgaben wie die HTML-Generierung, -Konvertierung und -Bearbeitung.

### Q2. Wo finde ich die Dokumentation für Aspose.HTML für .NET?

 A2: Sie können auf die Dokumentation für Aspose.HTML für .NET zugreifen[Hier](https://reference.aspose.com/html/net/). Es bietet umfassende Informationen, einschließlich API-Referenzen und Codebeispiele.

### Q3. Wie kann ich Aspose.HTML für .NET herunterladen?

A3: Sie können Aspose.HTML für .NET von der Download-Seite herunterladen[Hier](https://releases.aspose.com/html/net/).

### Q4. Gibt es eine kostenlose Testversion für Aspose.HTML für .NET?

 A4: Ja, Sie können Aspose.HTML für .NET ausprobieren, indem Sie die kostenlose Testversion von herunterladen[Hier](https://releases.aspose.com/).

### F5. Benötige ich eine temporäre Lizenz für Aspose.HTML für .NET?

 A5: Wenn Sie zu Evaluierungszwecken eine temporäre Lizenz benötigen, können Sie diese bei erhalten[Hier](https://purchase.aspose.com/temporary-license/).