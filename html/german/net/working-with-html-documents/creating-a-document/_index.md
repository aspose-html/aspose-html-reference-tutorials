---
title: Erstellen eines HTML-Dokuments in .NET mit Aspose.HTML
linktitle: Erstellen eines HTML-Dokuments in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie mit Aspose.HTML HTML-Dokumente in .NET erstellen, von Grund auf oder aus URLs. Ein umfassendes Tutorial für Webentwickler.
weight: 10
url: /de/net/working-with-html-documents/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen eines HTML-Dokuments in .NET mit Aspose.HTML


Im Bereich der Webentwicklung und Datenmanipulation ist ein leistungsstarkes Tool zum Erstellen, Ändern und Arbeiten mit HTML-Dokumenten unverzichtbar. Aspose.HTML für .NET ist ein solches Tool, das Ihre HTML-bezogenen Aufgaben vereinfachen kann. In diesem umfassenden Tutorial erfahren Sie Schritt für Schritt, wie Sie mit Aspose.HTML für .NET HTML-Dokumente erstellen. Bevor wir uns in die Beispiele vertiefen, wollen wir einige Voraussetzungen besprechen.

## Voraussetzungen

Bevor Sie sich auf diese Reise begeben, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem System installiert ist.

2. Aspose.HTML für .NET: Laden Sie die Aspose.HTML für .NET-Bibliothek herunter und installieren Sie sie. Den Download-Link finden Sie[Hier](https://releases.aspose.com/html/net/).

3. Grundkenntnisse in C#: Machen Sie sich mit den Grundlagen der Programmiersprache C# vertraut.

Nachdem wir nun die Voraussetzungen erfüllt haben, beginnen wir mit der Erstellung von HTML-Dokumenten.

## Namespaces importieren

Zunächst müssen Sie die erforderlichen Namespaces importieren, um Aspose.HTML in Ihrem C#-Projekt verwenden zu können. Fügen Sie Ihrer Codedatei die folgenden using-Direktiven hinzu:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## Erstellen eines SVG-Dokuments

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        // Führen Sie hier Aktionen am SVG-Dokument aus ...
    }
}
```

 In diesem Beispiel erstellen wir ein SVG-Dokument, indem wir den SVG-Inhalt und eine Basis-URL angeben.`SVGDocument` Mit der Klasse von Aspose.HTML für .NET können Sie SVG-Dokumente mühelos bearbeiten.

## Erstellen eines HTML-Dokuments von Grund auf

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // Führen Sie hier Aktionen am HTML-Dokument aus ...
    }
}
```

 Dieses Beispiel zeigt, wie man ein HTML-Dokument von Grund auf neu erstellt.`HTMLDocument`Klasse bietet eine leere Leinwand für Ihren HTML-Inhalt.

## Erstellen eines HTML-Dokuments aus einer lokalen Datei

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // Führen Sie hier Aktionen am HTML-Dokument aus ...
    }
}
```

 Wenn Sie eine vorhandene HTML-Datei auf Ihrem lokalen System haben, können Sie diese mit dem`HTMLDocument` Klasse, wie in diesem Beispiel gezeigt.

## Erstellen eines HTML-Dokuments aus einer Remote-URL

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://Ihre.site.com/"))
    {
        // Führen Sie hier Aktionen am HTML-Dokument aus ...
    }
}
```

Manchmal müssen Sie mit HTML-Inhalten arbeiten, die auf einem Remote-Server gehostet werden. Dieses Beispiel zeigt, wie Sie aus einer Remote-URL ein HTML-Dokument erstellen.

## Erstellen eines HTML-Dokuments aus einer Remote-URL (Alternative)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://Ihre.site.com/")))
    {
        // Führen Sie hier Aktionen am HTML-Dokument aus ...
    }
}
```

Dieser alternative Ansatz zeigt auch, wie mit einem anderen Konstruktor ein HTML-Dokument aus einer Remote-URL erstellt wird.

## Erstellen eines HTML-Dokuments aus HTML-Inhalten

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        // Führen Sie hier Aktionen am HTML-Dokument aus ...
    }
}
```

Wenn Sie HTML-Inhalte im String-Format haben, können Sie damit ein HTML-Dokument erstellen, wie in diesem Beispiel gezeigt.

## Erstellen eines HTML-Dokuments aus einem Stream

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            // Führen Sie hier Aktionen am HTML-Dokument aus ...
        }
    }
}
```

In diesem Beispiel zeigen wir, wie man aus Daten in einem Speicherstream ein HTML-Dokument erstellt. Dies kann nützlich sein, wenn Sie HTML-Inhalte in einem Stream haben und diese bearbeiten möchten.

## Abschluss

Aspose.HTML für .NET bietet einen leistungsstarken Satz von Tools zum Erstellen und Arbeiten mit HTML-Dokumenten in Ihren .NET-Anwendungen. Mit den in diesem Tutorial bereitgestellten Beispielen können Sie problemlos mit dem Erstellen von HTML-Dokumenten beginnen, egal ob von Grund auf, mit lokalen Dateien, Remote-URLs oder mit vorhandenem HTML-Inhalt.

 Haben Sie Fragen oder benötigen Sie Hilfe? Besuchen Sie das Aspose.HTML-Community-Forum für Unterstützung unter[https://forum.aspose.com/](https://forum.aspose.com/).

## FAQs

### F1: Ist die Nutzung von Aspose.HTML für .NET kostenlos?
 A1: Aspose.HTML für .NET bietet eine kostenlose Testversion an, für die volle Nutzung müssen Sie jedoch eine Lizenz erwerben. Weitere Einzelheiten finden Sie unter[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### F2: Wie kann ich eine temporäre Lizenz für Aspose.HTML für .NET erhalten?
 A2: Wenn Sie eine temporäre Lizenz benötigen, können Sie diese erhalten bei[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### F3: Wo finde ich Dokumentation für Aspose.HTML für .NET?
A3: Die Dokumentation finden Sie unter[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### F4: Gibt es andere Aspose-Bibliotheken für die .NET-Entwicklung?
 A4: Ja, Aspose bietet eine Reihe von Bibliotheken für verschiedene Dateiformate und Dokumentbearbeitungsaufgaben. Schauen Sie sich ihre Angebote an unter[https://products.aspose.com/](https://products.aspose.com/).

### F5: Kann ich Aspose.HTML für .NET in meinen Webanwendungen verwenden?
A5: Ja, Aspose.HTML für .NET ist mit Webanwendungen kompatibel und somit eine vielseitige Wahl sowohl für Desktop- als auch für webbasierte Projekte.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
