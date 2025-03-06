---
title: Web Scraping in .NET mit Aspose.HTML
linktitle: Web Scraping in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie HTML-Dokumente in .NET mit Aspose.HTML bearbeiten. Navigieren, filtern, abfragen und wählen Sie Elemente effektiv aus, um die Webentwicklung zu verbessern.
weight: 13
url: /de/net/advanced-features/web-scraping/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Web Scraping in .NET mit Aspose.HTML


Im heutigen digitalen Zeitalter ist das Bearbeiten und Extrahieren von Informationen aus HTML-Dokumenten eine alltägliche Aufgabe für Entwickler. Aspose.HTML für .NET ist ein leistungsstarkes Tool, das die HTML-Verarbeitung und -Bearbeitung in .NET-Anwendungen vereinfacht. In diesem Tutorial werden wir verschiedene Aspekte von Aspose.HTML für .NET untersuchen, darunter Voraussetzungen, Namespaces und schrittweise Beispiele, die Ihnen helfen, das volle Potenzial von Aspose.HTML auszuschöpfen.

## Voraussetzungen

Bevor Sie in die Welt von Aspose.HTML für .NET eintauchen, benötigen Sie einige Voraussetzungen:

1. Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine funktionierende Entwicklungsumgebung mit Visual Studio oder einer anderen kompatiblen IDE für die .NET-Entwicklung eingerichtet haben.

2.  Aspose.HTML für .NET: Laden Sie die Aspose.HTML für .NET-Bibliothek herunter und installieren Sie sie von der[Downloadlink](https://releases.aspose.com/html/net/). Sie können je nach Bedarf zwischen der kostenlosen Testversion oder einer lizenzierten Version wählen.

3. Grundlegende HTML-Kenntnisse: Um Aspose.HTML für .NET effektiv nutzen zu können, sind Kenntnisse der HTML-Struktur und -Elemente unerlässlich.

## Namespaces importieren

Zu Beginn müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. Diese Namespaces bieten Zugriff auf die Aspose.HTML für .NET-Klassen und -Funktionen:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Nachdem die Voraussetzungen erfüllt und die Namespaces importiert sind, wollen wir nun einige wichtige Beispiele Schritt für Schritt aufschlüsseln, um zu veranschaulichen, wie Aspose.HTML für .NET effektiv verwendet wird.

## Navigieren durch HTML

In diesem Beispiel navigieren wir durch ein HTML-Dokument und greifen Schritt für Schritt auf seine Elemente zu.

```csharp
public static void NavigateThroughHTML()
{
    // Bereiten Sie einen HTML-Code vor
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Initialisieren Sie ein Dokument aus dem vorbereiteten Code
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Holen Sie sich den Verweis auf das erste Kind (erster SPAN) des BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Ausgabe: Hallo

        // Holen Sie sich den Verweis auf das Leerzeichen zwischen HTML-Elementen
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Ausgabe: ' '

        // Holen Sie sich den Verweis auf das zweite SPAN-Element
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Ausgabe: Welt!
    }
}
```

 In diesem Beispiel erstellen wir ein HTML-Dokument, greifen auf dessen erstes untergeordnetes Dokument zu (ein`SPAN` Element), das Leerzeichen zwischen den Elementen und das zweite`SPAN` Element, das die grundlegende Navigation demonstriert.

## Verwenden von Knotenfiltern

Knotenfilter ermöglichen Ihnen die selektive Verarbeitung bestimmter Elemente in einem HTML-Dokument.

```csharp
public static void NodeFilterUsageExample()
{
    // Bereiten Sie einen HTML-Code vor
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Initialisieren Sie ein Dokument basierend auf dem vorbereiteten Code
    using (var document = new HTMLDocument(code, "."))
    {
        // Erstellen Sie einen TreeWalker mit einem benutzerdefinierten Filter für Bildelemente
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Ausgabe: image1.png
                // Ausgabe: image2.png
            }
        }
    }
}
```

 Dieses Beispiel zeigt, wie Sie mit einem benutzerdefinierten Knotenfilter bestimmte Elemente extrahieren können (in diesem Fall`IMG` Elemente) aus dem HTML-Dokument.

## XPath-Abfragen

Mit XPath-Abfragen können Sie anhand bestimmter Kriterien nach Elementen in einem HTML-Dokument suchen.

```csharp
public static void XPathQueryUsageExample()
{
    // Bereiten Sie einen HTML-Code vor
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello!</span>
            </div>
        </div>
        <p class='happy'>
            <span>World</span>
        </p>
    ";
    
    // Initialisieren Sie ein Dokument basierend auf dem vorbereiteten Code
    using (var document = new HTMLDocument(code, "."))
    {
        // Auswerten eines XPath-Ausdrucks zum Auswählen bestimmter Elemente
        var result = document.Evaluate("//*[@class='glücklich']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Iterieren Sie über die resultierenden Knoten
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Ausgabe: Hallo
            // Ausgabe: Welt!
        }
    }
}
```

Dieses Beispiel zeigt die Verwendung von XPath-Abfragen, um Elemente im HTML-Dokument anhand ihrer Attribute und Struktur zu lokalisieren.

## CSS-Selektoren

CSS-Selektoren bieten eine alternative Möglichkeit, Elemente in einem HTML-Dokument auszuwählen, ähnlich der Art und Weise, wie CSS-Stylesheets Elemente ansprechen.

```csharp
public static void CSSSelectorUsageExample()
{
    // Bereiten Sie einen HTML-Code vor
    var code = @"
        <div class='happy'>
            <div>
                <span>Hello</span>
            </div>
        </div>
        <p class='happy'>
            <span>World!</span>
        </p>
    ";
    
    // Initialisieren Sie ein Dokument basierend auf dem vorbereiteten Code
    using (var document = new HTMLDocument(code, "."))
    {
        //Verwenden Sie einen CSS-Selektor, um Elemente basierend auf Klasse und Hierarchie zu extrahieren
        var elements = document.QuerySelectorAll(".happy span");
        
        // Iterieren Sie über die resultierende Liste der Elemente
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Ausgabe: Hallo
            // Ausgabe: Welt!
        }
    }
}
```

Hier zeigen wir, wie Sie CSS-Selektoren verwenden, um bestimmte Elemente im HTML-Dokument anzusprechen.

Mit diesen Beispielen haben Sie ein grundlegendes Verständnis für die Navigation, Filterung, Abfrage und Auswahl von Elementen in HTML-Dokumenten mit Aspose.HTML für .NET gewonnen.

## Abschluss

 Aspose.HTML für .NET ist eine vielseitige Bibliothek, die .NET-Entwicklern die effiziente Arbeit mit HTML-Dokumenten ermöglicht. Mit seinen leistungsstarken Funktionen zum Navigieren, Filtern, Abfragen und Auswählen von Elementen können Sie verschiedene HTML-Verarbeitungsaufgaben nahtlos erledigen. Indem Sie diesem Tutorial folgen und die Dokumentation unter[Aspose.HTML für .NET-Dokumentation](https://reference.aspose.com/html/net/)können Sie das volle Potenzial dieses Tools für Ihre .NET-Anwendungen freisetzen.

## Häufig gestellte Fragen

### F1. Ist die Nutzung von Aspose.HTML für .NET kostenlos?

A1: Aspose.HTML für .NET bietet eine kostenlose Testversion, für den produktiven Einsatz müssen Sie jedoch eine Lizenz erwerben. Lizenzdetails und -optionen finden Sie unter[Aspose.HTML Kauf](https://purchase.aspose.com/buy).

### F2. Wie kann ich eine temporäre Lizenz für Aspose.HTML für .NET erhalten?

 A2: Eine temporäre Lizenz zu Testzwecken erhalten Sie bei[Aspose.HTML Temporäre Lizenz](https://purchase.aspose.com/temporary-license/).

### F3. Wo kann ich Hilfe oder Support für Aspose.HTML für .NET erhalten?

 A3: Wenn Sie auf Probleme stoßen oder Fragen haben, können Sie die[Aspose.HTML Forum](https://forum.aspose.com/) für Hilfe und Unterstützung durch die Gemeinschaft.

### F4. Gibt es zusätzliche Ressourcen zum Erlernen von Aspose.HTML für .NET?

 A4: Neben diesem Tutorial können Sie weitere Tutorials und Dokumentationen zum[Aspose.HTML für .NET-Dokumentationsseite](https://reference.aspose.com/html/net/).

### F5. Ist Aspose.HTML für .NET mit den neuesten .NET-Versionen kompatibel?

A5: Aspose.HTML für .NET wird regelmäßig aktualisiert, um die Kompatibilität mit den neuesten .NET-Versionen und -Technologien sicherzustellen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
