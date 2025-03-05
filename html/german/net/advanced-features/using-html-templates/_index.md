---
title: Verwenden von HTML-Vorlagen in .NET mit Aspose.HTML
linktitle: Verwenden von HTML-Vorlagen in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie mit Aspose.HTML für .NET dynamisch HTML-Dokumente aus JSON-Daten generieren. Nutzen Sie die Leistungsfähigkeit der HTML-Manipulation in Ihren .NET-Anwendungen.
type: docs
weight: 17
url: /de/net/advanced-features/using-html-templates/
---

Wenn Sie mit HTML-Dokumenten und -Vorlagen in Ihren .NET-Anwendungen arbeiten möchten, sind Sie hier richtig! Aspose.HTML für .NET ist eine vielseitige Bibliothek, mit der Entwickler HTML-Dokumente und -Vorlagen mühelos bearbeiten können. In diesem Tutorial werden wir uns mit den Grundlagen der Verwendung von Aspose.HTML für .NET befassen, jeden Schritt aufschlüsseln und dabei eine klare Erklärung liefern.

## Voraussetzungen

Bevor wir uns mit den Einzelheiten von Aspose.HTML für .NET befassen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Sie können es von der Website herunterladen, falls Sie es noch nicht haben.

2.  Aspose.HTML für .NET: Sie müssen Aspose.HTML für .NET in Ihrem Visual Studio-Projekt installiert haben. Sie erhalten es von der[Dokumentation](https://reference.aspose.com/html/net/).

3. JSON-Daten: Bereiten Sie eine JSON-Datenquelle vor, die Sie zum Auffüllen Ihrer HTML-Vorlage verwenden möchten. Für dieses Tutorial verwenden wir die folgenden JSON-Daten:

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

## Namespaces importieren

Als Erstes importieren wir die erforderlichen Namespaces in Ihr .NET-Projekt:

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Loading;
```

Nachdem wir nun die Voraussetzungen abgedeckt und die erforderlichen Namespaces importiert haben, wollen wir jeden Schritt im Detail aufschlüsseln.

## Schritt 1: Vorbereiten einer JSON-Datenquelle

Beginnen Sie mit der Erstellung einer JSON-Datenquelle, die die Informationen enthält, die Sie in Ihre HTML-Vorlage einfügen möchten. In diesem Beispiel haben wir bereits eine JSON-Datenquelle vorbereitet, wie in den Voraussetzungen erwähnt. Speichern Sie sie in einer Datei, zum Beispiel „data-source.json“.

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

Dieser Codeausschnitt liest die JSON-Daten und schreibt sie in eine Datei mit dem Namen „data-source.json“.

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

## Schritt 3: HTML-Vorlage ausfüllen

 Rufen Sie abschließend die`Converter.ConvertTemplate` Methode, um Ihre HTML-Vorlage mit den Daten aus der JSON-Quelle zu füllen.

```csharp
Aspose.Html.Converters.Converter.ConvertTemplate(
"template.html", new Aspose.Html.Converters.TemplateData("data-source.json"), new Aspose.Html.Loading.TemplateLoadOptions(), "document.html"
);
```

Dieser Code nimmt die Datei „template.html“, ersetzt die Platzhalter durch die entsprechenden JSON-Werte und speichert das Ergebnis in „document.html“.

Herzlichen Glückwunsch! Sie haben die Leistung von Aspose.HTML für .NET erfolgreich genutzt, um HTML-Dokumente dynamisch aus JSON-Daten zu generieren.

## Abschluss

In diesem Tutorial haben wir die Grundlagen der Verwendung von Aspose.HTML für .NET zur dynamischen Erstellung von HTML-Dokumenten erkundet. Wir haben die Voraussetzungen behandelt, Namespaces importiert und jeden Schritt detailliert aufgeschlüsselt. Wenn Sie diese Schritte befolgen, können Sie die HTML-Dokumentenerstellung nahtlos in Ihre .NET-Anwendungen integrieren.

## Häufig gestellte Fragen

### F1. Was ist Aspose.HTML für .NET?

A1: Aspose.HTML für .NET ist eine leistungsstarke Bibliothek, die es .NET-Entwicklern ermöglicht, programmgesteuert mit HTML-Dokumenten und -Vorlagen zu arbeiten. Es vereinfacht Aufgaben wie die HTML-Generierung, -Konvertierung und -Bearbeitung.

### F2. Wo finde ich die Dokumentation für Aspose.HTML für .NET?

 A2: Sie können auf die Dokumentation für Aspose.HTML für .NET zugreifen[Hier](https://reference.aspose.com/html/net/). Es bietet umfassende Informationen, einschließlich API-Referenzen und Codebeispielen.

### F3. Wie kann ich Aspose.HTML für .NET herunterladen?

A3: Sie können Aspose.HTML für .NET von der Download-Seite herunterladen[Hier](https://releases.aspose.com/html/net/).

### F4. Gibt es eine kostenlose Testversion für Aspose.HTML für .NET?

 A4: Ja, Sie können Aspose.HTML für .NET ausprobieren, indem Sie die kostenlose Testversion von herunterladen[Hier](https://releases.aspose.com/).

### F5. Benötige ich eine temporäre Lizenz für Aspose.HTML für .NET?

 A5: Wenn Sie eine temporäre Lizenz für Evaluierungszwecke benötigen, erhalten Sie diese bei[Hier](https://purchase.aspose.com/temporary-license/).