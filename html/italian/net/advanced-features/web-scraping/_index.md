---
title: Web Scraping in .NET con Aspose.HTML
linktitle: Web scraping in .NET
second_title: Aspose.HTML API di manipolazione HTML .NET
description: Impara a manipolare documenti HTML in .NET con Aspose.HTML. Naviga, filtra, interroga e seleziona elementi in modo efficace per uno sviluppo web avanzato.
type: docs
weight: 13
url: /it/net/advanced-features/web-scraping/
---

Nell'era digitale odierna, manipolare ed estrarre informazioni da documenti HTML è un compito comune per gli sviluppatori. Aspose.HTML per .NET è un potente strumento che semplifica l'elaborazione e la manipolazione HTML nelle applicazioni .NET. In questo tutorial, esploreremo vari aspetti di Aspose.HTML per .NET, inclusi prerequisiti, namespace ed esempi passo dopo passo per aiutarti a sfruttarne appieno il potenziale.

## Prerequisiti

Prima di immergerti nel mondo di Aspose.HTML per .NET, sono necessari alcuni prerequisiti:

1. Ambiente di sviluppo: assicurati di disporre di un ambiente di sviluppo funzionante configurato con Visual Studio o qualsiasi altro IDE compatibile per lo sviluppo .NET.

2.  Aspose.HTML per .NET: Scarica e installa la libreria Aspose.HTML per .NET da[collegamento per il download](https://releases.aspose.com/html/net/)Puoi scegliere tra la versione di prova gratuita o quella con licenza in base alle tue esigenze.

3. Conoscenza di base dell'HTML: la familiarità con la struttura e gli elementi HTML è essenziale per utilizzare in modo efficace Aspose.HTML per .NET.

## Importazione di namespace

Per iniziare, devi importare i namespace necessari nel tuo progetto C#. Questi namespace forniscono accesso alle classi e alle funzionalità di Aspose.HTML per .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Una volta soddisfatti i prerequisiti e importati gli spazi dei nomi, analizziamo passo dopo passo alcuni esempi chiave per illustrare come utilizzare in modo efficace Aspose.HTML per .NET.

## Navigazione in HTML

In questo esempio, navigheremo attraverso un documento HTML e accederemo ai suoi elementi passo dopo passo.

```csharp
public static void NavigateThroughHTML()
{
    // Preparare un codice HTML
    var html_code = "<span>Hello</span> <span>World!</span>";
    
    // Inizializza un documento dal codice preparato
    using (var document = new HTMLDocument(html_code, "."))
    {
        // Ottieni il riferimento al primo figlio (primo SPAN) del BODY
        var element = document.Body.FirstChild;
        Console.WriteLine(element.TextContent); // Uscita: Ciao

        // Ottieni il riferimento allo spazio vuoto tra gli elementi HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Produzione: ' '

        // Ottieni il riferimento al secondo elemento SPAN
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Risultato: Mondo!
    }
}
```

 In questo esempio, creiamo un documento HTML, accediamo al suo primo figlio (un`SPAN` elemento), lo spazio vuoto tra gli elementi e il secondo`SPAN` elemento che illustra la navigazione di base.

## Utilizzo dei filtri dei nodi

I filtri dei nodi consentono di elaborare in modo selettivo elementi specifici all'interno di un documento HTML.

```csharp
public static void NodeFilterUsageExample()
{
    // Preparare un codice HTML
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Inizializzare un documento in base al codice preparato
    using (var document = new HTMLDocument(code, "."))
    {
        // Crea un TreeWalker con un filtro personalizzato per gli elementi dell'immagine
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Risultato: image1.png
                // Risultato: image2.png
            }
        }
    }
}
```

 Questo esempio mostra come utilizzare un filtro nodo personalizzato per estrarre elementi specifici (in questo caso,`IMG` elementi) dal documento HTML.

## Query XPath

Le query XPath consentono di cercare elementi in un documento HTML in base a criteri specifici.

```csharp
public static void XPathQueryUsageExample()
{
    // Preparare un codice HTML
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
    
    // Inizializzare un documento in base al codice preparato
    using (var document = new HTMLDocument(code, "."))
    {
        // Valutare un'espressione XPath per selezionare elementi specifici
        var result = document.Evaluate("//*[@class='happy']//intervallo",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Eseguire l'iterazione sui nodi risultanti
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Uscita: Ciao
            // Risultato: Mondo!
        }
    }
}
```

Questo esempio illustra l'uso delle query XPath per individuare gli elementi nel documento HTML in base ai loro attributi e alla loro struttura.

## Selettori CSS

I selettori CSS forniscono un metodo alternativo per selezionare gli elementi in un documento HTML, in modo simile al modo in cui i fogli di stile CSS indirizzano gli elementi.

```csharp
public static void CSSSelectorUsageExample()
{
    // Preparare un codice HTML
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
    
    // Inizializzare un documento in base al codice preparato
    using (var document = new HTMLDocument(code, "."))
    {
        //Utilizzare un selettore CSS per estrarre gli elementi in base alla classe e alla gerarchia
        var elements = document.QuerySelectorAll(".happy span");
        
        // Eseguire l'iterazione sull'elenco risultante degli elementi
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Uscita: Ciao
            // Risultato: Mondo!
        }
    }
}
```

In questo articolo mostreremo come utilizzare i selettori CSS per selezionare elementi specifici nel documento HTML.

Grazie a questi esempi, avrai acquisito le nozioni fondamentali su come navigare, filtrare, interrogare e selezionare elementi nei documenti HTML utilizzando Aspose.HTML per .NET.

## Conclusione

 Aspose.HTML per .NET è una libreria versatile che consente agli sviluppatori .NET di lavorare in modo efficiente con i documenti HTML. Grazie alle sue potenti funzionalità per la navigazione, il filtraggio, l'interrogazione e la selezione di elementi, puoi gestire senza problemi varie attività di elaborazione HTML. Seguendo questo tutorial ed esplorando la documentazione su[Documentazione di Aspose.HTML per .NET](https://reference.aspose.com/html/net/)puoi sfruttare appieno il potenziale di questo strumento per le tue applicazioni .NET.

## Domande frequenti

### D1. Aspose.HTML per .NET è gratuito?

A1: Aspose.HTML per .NET offre una versione di prova gratuita, ma per l'uso in produzione, dovrai acquistare una licenza. Puoi trovare i dettagli e le opzioni di licenza su[Acquisto Aspose.HTML](https://purchase.aspose.com/buy).

### D2. Come posso ottenere una licenza temporanea per Aspose.HTML per .NET?

 A2: È possibile ottenere una licenza temporanea per scopi di prova da[Licenza temporanea Aspose.HTML](https://purchase.aspose.com/temporary-license/).

### D3. Dove posso cercare aiuto o supporto per Aspose.HTML per .NET?

 A3: Se riscontri problemi o hai domande, puoi visitare il[Forum di Aspose.HTML](https://forum.aspose.com/) per assistenza e supporto alla comunità.

### D4. Esistono risorse aggiuntive per apprendere Aspose.HTML per .NET?

 A4: Insieme a questo tutorial, puoi esplorare altri tutorial e documentazione su[Pagina di documentazione di Aspose.HTML per .NET](https://reference.aspose.com/html/net/).

### D5. Aspose.HTML per .NET è compatibile con le ultime versioni di .NET?

A5: Aspose.HTML per .NET viene aggiornato regolarmente per garantire la compatibilità con le ultime versioni e tecnologie .NET.