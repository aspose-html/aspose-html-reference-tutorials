---
title: Web Scraping in .NET con Aspose.HTML
linktitle: Web Scraping in .NET
second_title: Aspose.Slides API di manipolazione HTML .NET
description: Impara a manipolare documenti HTML in .NET con Aspose.HTML. Naviga, filtra, interroga e seleziona gli elementi in modo efficace per uno sviluppo web avanzato.
type: docs
weight: 13
url: /it/net/advanced-features/web-scraping/
---

Nell'era digitale di oggi, manipolare ed estrarre informazioni dai documenti HTML è un compito comune per gli sviluppatori. Aspose.HTML per .NET è un potente strumento che semplifica l'elaborazione e la manipolazione dell'HTML nelle applicazioni .NET. In questo tutorial esploreremo vari aspetti di Aspose.HTML per .NET, inclusi prerequisiti, spazi dei nomi ed esempi passo passo per aiutarti a sfruttare tutto il suo potenziale.

## Prerequisiti

Prima di immergerti nel mondo di Aspose.HTML per .NET, avrai bisogno di alcuni prerequisiti:

1. Ambiente di sviluppo: assicurati di disporre di un ambiente di sviluppo funzionante configurato con Visual Studio o qualsiasi altro IDE compatibile per lo sviluppo .NET.

2.  Aspose.HTML per .NET: scarica e installa la libreria Aspose.HTML per .NET da[Link per scaricare](https://releases.aspose.com/html/net/). Puoi scegliere tra la versione di prova gratuita o quella con licenza in base alle tue esigenze.

3. Conoscenza di base di HTML: la familiarità con la struttura e gli elementi HTML è essenziale per utilizzare in modo efficace Aspose.HTML per .NET.

## Importazione di spazi dei nomi

Per iniziare, devi importare gli spazi dei nomi necessari nel tuo progetto C#. Questi spazi dei nomi forniscono l'accesso alle classi e funzionalità Aspose.HTML per .NET:

```csharp
using Aspose.Html;
using Aspose.Html.Dom;
using Aspose.Html.XPath;
using Aspose.Html.Css;
```

Con i prerequisiti in atto e gli spazi dei nomi importati, analizziamo passo dopo passo alcuni esempi chiave per illustrare come utilizzare Aspose.HTML per .NET in modo efficace.

## Navigazione attraverso HTML

In questo esempio navigheremo attraverso un documento HTML e accederemo ai suoi elementi passo dopo passo.

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

        //Ottieni il riferimento allo spazio bianco tra gli elementi HTML
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Produzione: ' '

        // Ottieni il riferimento al secondo elemento SPAN
        element = element.NextSibling;
        Console.WriteLine(element.TextContent); // Uscita: Mondo!
    }
}
```

 In questo esempio creiamo un documento HTML, accediamo al suo primo figlio (a`SPAN` element), lo spazio bianco tra gli elementi e il secondo`SPAN` elemento, che mostra la navigazione di base.

## Utilizzo dei filtri dei nodi

I filtri dei nodi consentono di elaborare selettivamente elementi specifici all'interno di un documento HTML.

```csharp
public static void NodeFilterUsageExample()
{
    // Preparare un codice HTML
    var code = @"
        <p>Hello</p>
        <img src='image1.png'>
        <img src='image2.png'>
        <p>World!</p>";
    
    // Inizializza un documento in base al codice preparato
    using (var document = new HTMLDocument(code, "."))
    {
        // Crea un TreeWalker con un filtro personalizzato per gli elementi dell'immagine
        using (var iterator = document.CreateTreeWalker(document, NodeFilter.SHOW_ALL, new OnlyImageFilter()))
        {
            while (iterator.NextNode() != null)
            {
                var image = (HTMLImageElement)iterator.CurrentNode;
                Console.WriteLine(image.Src);
                // Risultato: immagine1.png
                // Risultato: immagine2.png
            }
        }
    }
}
```

 Questo esempio dimostra come utilizzare un filtro del nodo personalizzato per estrarre elementi specifici (in questo caso,`IMG` elementi) dal documento HTML.

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
    
    // Inizializza un documento in base al codice preparato
    using (var document = new HTMLDocument(code, "."))
    {
        // Valuta un'espressione XPath per selezionare elementi specifici
        var result = document.Evaluate("//*[@class='happy']//span",
                                        document,
                                        null,
                                        XPathResultType.Any,
                                        null);
        
        // Iterare sui nodi risultanti
        for (Node node; (node = result.IterateNext()) != null;)
        {
            Console.WriteLine(node.TextContent);
            // Uscita: Ciao
            // Uscita: Mondo!
        }
    }
}
```

Questo esempio mostra l'uso delle query XPath per individuare gli elementi nel documento HTML in base ai loro attributi e alla loro struttura.

## Selettori CSS

I selettori CSS forniscono un modo alternativo per selezionare gli elementi in un documento HTML, in modo simile al modo in cui i fogli di stile CSS prendono di mira gli elementi.

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
    
    // Inizializza un documento in base al codice preparato
    using (var document = new HTMLDocument(code, "."))
    {
        // Utilizza un selettore CSS per estrarre elementi in base alla classe e alla gerarchia
        var elements = document.QuerySelectorAll(".happy span");
        
        // Iterare sull'elenco di elementi risultante
        foreach (HTMLElement element in elements)
        {
            Console.WriteLine(element.InnerHTML);
            // Uscita: Ciao
            // Uscita: Mondo!
        }
    }
}
```

Qui, dimostriamo come utilizzare i selettori CSS per indirizzare elementi specifici nel documento HTML.

Con questi esempi, hai acquisito una conoscenza fondamentale di come navigare, filtrare, eseguire query e selezionare elementi nei documenti HTML utilizzando Aspose.HTML per .NET.

## Conclusione

Aspose.HTML per .NET è una libreria versatile che consente agli sviluppatori .NET di lavorare in modo efficiente con documenti HTML. Con le sue potenti funzionalità per la navigazione, il filtraggio, l'esecuzione di query e la selezione di elementi, puoi gestire varie attività di elaborazione HTML senza problemi. Seguendo questo tutorial ed esplorando la documentazione all'indirizzo[Aspose.HTML per la documentazione .NET](https://reference.aspose.com/html/net/), puoi sfruttare tutto il potenziale di questo strumento per le tue applicazioni .NET.

## Domande frequenti

### Q1. Aspose.HTML per .NET è gratuito?

 A1: Aspose.HTML per .NET offre una versione di prova gratuita, ma per l'utilizzo in produzione sarà necessario acquistare una licenza. Puoi trovare i dettagli e le opzioni di licenza su[Aspose.HTML Acquisto](https://purchase.aspose.com/buy).

### Q2. Come posso ottenere una licenza temporanea per Aspose.HTML per .NET?

 R2: È possibile ottenere una licenza temporanea a scopo di test da[Licenza temporanea Aspose.HTML](https://purchase.aspose.com/temporary-license/).

### Q3. Dove posso cercare aiuto o supporto per Aspose.HTML per .NET?

 R3: Se riscontri problemi o hai domande, puoi visitare il[Aspose.HTML Forum](https://forum.aspose.com/) per l'assistenza e il sostegno della comunità.

### Q4. Esistono risorse aggiuntive per l'apprendimento di Aspose.HTML per .NET?

 R4: Oltre a questo tutorial, puoi esplorare altri tutorial e documentazione su[Aspose.HTML per la pagina della documentazione .NET](https://reference.aspose.com/html/net/).

### Q5. Aspose.HTML per .NET è compatibile con le ultime versioni di .NET?

A5: Aspose.HTML per .NET viene regolarmente aggiornato per garantire la compatibilità con le ultime versioni e tecnologie di .NET.