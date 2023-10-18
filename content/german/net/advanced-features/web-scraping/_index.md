---
title: Web Scraping in .NET mit Aspose.HTML
linktitle: Web Scraping in .NET
second_title: Aspose.HTML .NET HTML-Manipulations-API
description: Erfahren Sie, wie Sie HTML-Dokumente in .NET mit Aspose.HTML bearbeiten. Navigieren, filtern, fragen Sie ab und wählen Sie Elemente effektiv aus, um die Webentwicklung zu verbessern.
type: docs
weight: 13
url: /de/net/advanced-features/web-scraping/
---

Im heutigen digitalen Zeitalter ist das Bearbeiten und Extrahieren von Informationen aus HTML-Dokumenten eine häufige Aufgabe für Entwickler. Aspose.HTML für .NET ist ein leistungsstarkes Tool, das die HTML-Verarbeitung und -Manipulation in .NET-Anwendungen vereinfacht. In diesem Tutorial befassen wir uns mit verschiedenen Aspekten von Aspose.HTML für .NET, einschließlich Voraussetzungen, Namespaces und Schritt-für-Schritt-Beispielen, damit Sie das volle Potenzial nutzen können.

## Voraussetzungen

Bevor Sie in die Welt von Aspose.HTML für .NET eintauchen, benötigen Sie einige Voraussetzungen:

1. Entwicklungsumgebung: Stellen Sie sicher, dass Sie über eine funktionierende Entwicklungsumgebung mit Visual Studio oder einer anderen kompatiblen IDE für die .NET-Entwicklung verfügen.

2.  Aspose.HTML für .NET: Laden Sie die Aspose.HTML für .NET-Bibliothek von herunter und installieren Sie sie[Download-Link](https://releases.aspose.com/html/net/). Sie können je nach Bedarf zwischen der kostenlosen Testversion oder einer lizenzierten Version wählen.

3. Grundlegende HTML-Kenntnisse: Vertrautheit mit HTML-Strukturen und -Elementen ist für die effektive Nutzung von Aspose.HTML für .NET unerlässlich.

## Namensräume importieren

Zunächst müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. Diese Namespaces bieten Zugriff auf die Aspose.HTML für .NET-Klassen und -Funktionen:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Nachdem die Voraussetzungen erfüllt und Namespaces importiert sind, wollen wir einige wichtige Beispiele Schritt für Schritt aufschlüsseln, um zu veranschaulichen, wie Aspose.HTML für .NET effektiv verwendet werden kann.

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
        // Rufen Sie den Verweis auf das erste untergeordnete Element (erste SPAN) des BODY ab
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Ausgabe: Hallo

        // Rufen Sie den Verweis auf den Leerraum zwischen HTML-Elementen ab
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Ausgabe: ' '

        // Rufen Sie den Verweis auf das zweite SPAN-Element ab
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Ausgabe: Welt!
    }
}
```

 In diesem Beispiel erstellen wir ein HTML-Dokument, greifen auf sein erstes untergeordnetes Dokument zu (a`SPAN` Element), das Leerzeichen zwischen Elementen und das zweite`SPAN` Element, das die grundlegende Navigation demonstriert.

## Verwenden von Knotenfiltern

Mit Knotenfiltern können Sie bestimmte Elemente innerhalb eines HTML-Dokuments selektiv verarbeiten.

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

 Dieses Beispiel zeigt, wie Sie einen benutzerdefinierten Knotenfilter verwenden, um bestimmte Elemente zu extrahieren (in diesem Fall`IMG` Elemente) aus dem HTML-Dokument.

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
        // Werten Sie einen XPath-Ausdruck aus, um bestimmte Elemente auszuwählen
        var result = document.Evaluate("//*[@class='happy']//span",
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

Dieses Beispiel zeigt die Verwendung von XPath-Abfragen, um Elemente im HTML-Dokument basierend auf ihren Attributen und ihrer Struktur zu finden.

## CSS-Selektoren

CSS-Selektoren bieten eine alternative Möglichkeit, Elemente in einem HTML-Dokument auszuwählen, ähnlich wie CSS-Stylesheets auf Elemente abzielen.

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
        
        // Durchlaufen Sie die resultierende Liste der Elemente
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Ausgabe: Hallo
            // Ausgabe: Welt!
        }
    }
}
```

Hier zeigen wir, wie Sie CSS-Selektoren verwenden, um auf bestimmte Elemente im HTML-Dokument abzuzielen.

Mit diesen Beispielen haben Sie ein grundlegendes Verständnis für das Navigieren, Filtern, Abfragen und Auswählen von Elementen in HTML-Dokumenten mit Aspose.HTML für .NET erlangt.

## Abschluss

 Aspose.HTML für .NET ist eine vielseitige Bibliothek, die .NET-Entwicklern die effiziente Arbeit mit HTML-Dokumenten ermöglicht. Mit seinen leistungsstarken Funktionen zum Navigieren, Filtern, Abfragen und Auswählen von Elementen können Sie verschiedene HTML-Verarbeitungsaufgaben nahtlos erledigen. Indem Sie diesem Tutorial folgen und die Dokumentation unter erkunden[Aspose.HTML für .NET-Dokumentation](https://reference.aspose.com/html/net/)können Sie das volle Potenzial dieses Tools für Ihre .NET-Anwendungen nutzen.

## FAQs

### Q1. Ist die Nutzung von Aspose.HTML für .NET kostenlos?

A1: Aspose.HTML für .NET bietet eine kostenlose Testversion, für den Produktionseinsatz müssen Sie jedoch eine Lizenz erwerben. Lizenzdetails und Optionen finden Sie unter[Aspose.HTML-Kauf](https://purchase.aspose.com/buy).

### Q2. Wie kann ich eine temporäre Lizenz für Aspose.HTML für .NET erhalten?

 A2: Eine temporäre Lizenz zu Testzwecken erhalten Sie bei[Temporäre Aspose.HTML-Lizenz](https://purchase.aspose.com/temporary-license/).

### Q3. Wo kann ich Hilfe oder Unterstützung für Aspose.HTML für .NET suchen?

 A3: Wenn Sie auf Probleme stoßen oder Fragen haben, können Sie die besuchen[Aspose.HTML-Forum](https://forum.aspose.com/) für Hilfe und gemeinschaftliche Unterstützung.

### Q4. Gibt es zusätzliche Ressourcen zum Erlernen von Aspose.HTML für .NET?

 A4: Neben diesem Tutorial können Sie weitere Tutorials und Dokumentationen zum Thema erkunden[Aspose.HTML für .NET-Dokumentationsseite](https://reference.aspose.com/html/net/).

### F5. Ist Aspose.HTML für .NET mit den neuesten .NET-Versionen kompatibel?

A5: Aspose.HTML für .NET wird regelmäßig aktualisiert, um die Kompatibilität mit den neuesten .NET-Versionen und -Technologien sicherzustellen.