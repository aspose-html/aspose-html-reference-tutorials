---
title: Creazione di un documento HTML in .NET con Aspose.HTML
linktitle: Creazione di un documento HTML in .NET
second_title: Aspose.HTML API di manipolazione HTML .NET
description: Scopri come creare documenti HTML in .NET usando Aspose.HTML, da zero o da URL. Un tutorial completo per sviluppatori web.
weight: 10
url: /it/net/working-with-html-documents/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creazione di un documento HTML in .NET con Aspose.HTML


Nel regno dello sviluppo web e della manipolazione dei dati, avere uno strumento potente per creare, modificare e lavorare con documenti HTML è indispensabile. Aspose.HTML per .NET è uno di questi strumenti che può semplificare le tue attività correlate a HTML. In questo tutorial completo, esploreremo passo dopo passo come creare documenti HTML usando Aspose.HTML per .NET. Prima di immergerci negli esempi, esaminiamo alcuni prerequisiti.

## Prerequisiti

Prima di intraprendere questo viaggio, assicurati di disporre dei seguenti prerequisiti:

1. Visual Studio: assicurati di aver installato Visual Studio sul tuo sistema.

2. Aspose.HTML per .NET: Scarica e installa la libreria Aspose.HTML per .NET. Puoi trovare il link per il download[Qui](https://releases.aspose.com/html/net/).

3. Conoscenza di base di C#: familiarizzare con le basi del linguaggio di programmazione C#.

Ora che abbiamo chiarito i prerequisiti, possiamo iniziare a creare documenti HTML.

## Importazione di namespace

Innanzitutto, devi importare i namespace necessari per usare Aspose.HTML nel tuo progetto C#. Aggiungi le seguenti direttive using al tuo file di codice:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## Creazione di un documento SVG

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        // Esegui qui le azioni sul documento SVG...
    }
}
```

 In questo esempio, creiamo un documento SVG fornendo il contenuto SVG e un URL di base.`SVGDocument` La classe di Aspose.HTML per .NET consente di manipolare documenti SVG senza sforzo.

## Creare un documento HTML da zero

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // Esegui qui le azioni sul documento HTML...
    }
}
```

 Questo esempio dimostra come creare un documento HTML da zero.`HTMLDocument`fornisce una tela bianca per il tuo contenuto HTML.

## Creazione di un documento HTML da un file locale

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // Esegui qui le azioni sul documento HTML...
    }
}
```

 Se hai un file HTML esistente sul tuo sistema locale, puoi caricarlo utilizzando`HTMLDocument` classe, come mostrato in questo esempio.

## Creazione di un documento HTML da un URL remoto

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://tuo.sito.com/"))
    {
        // Esegui qui le azioni sul documento HTML...
    }
}
```

A volte, potresti dover lavorare con contenuti HTML ospitati su un server remoto. Questo esempio mostra come creare un documento HTML da un URL remoto.

## Creazione di un documento HTML da un URL remoto (alternativa)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://tuo.sito.com/")))
    {
        // Esegui qui le azioni sul documento HTML...
    }
}
```

Questo approccio alternativo mostra anche come creare un documento HTML da un URL remoto utilizzando un costruttore diverso.

## Creazione di un documento HTML da contenuto HTML

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        // Esegui qui le azioni sul documento HTML...
    }
}
```

Se si dispone di contenuto HTML in formato stringa, è possibile creare un documento HTML con esso, come illustrato in questo esempio.

## Creazione di un documento HTML da un flusso

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
            // Esegui qui le azioni sul documento HTML...
        }
    }
}
```

In questo esempio, mostriamo come creare un documento HTML da dati in un flusso di memoria. Questo può essere utile quando hai del contenuto HTML in un flusso e vuoi manipolarlo.

## Conclusione

Aspose.HTML per .NET fornisce un potente set di strumenti per creare e lavorare con documenti HTML nelle tue applicazioni .NET. Con gli esempi forniti in questo tutorial, puoi facilmente iniziare a creare documenti HTML, sia da zero, file locali, URL remoti o contenuti HTML esistenti.

 Hai domande o hai bisogno di assistenza? Visita il forum della community Aspose.HTML per ricevere supporto all'indirizzo[https://forum.aspose.com/](https://forum.aspose.com/).

## Domande frequenti

### D1: Aspose.HTML per .NET è gratuito?
 A1: Aspose.HTML per .NET offre una prova gratuita, ma per un utilizzo completo, dovrai acquistare una licenza. Puoi trovare maggiori dettagli su[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### D2: Come posso ottenere una licenza temporanea per Aspose.HTML per .NET?
 A2: Se hai bisogno di una licenza temporanea, puoi ottenerne una presso[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### D3: Dove posso trovare la documentazione per Aspose.HTML per .NET?
A3: La documentazione può essere trovata su[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### D4: Esistono altre librerie Aspose per lo sviluppo .NET?
 A4: Sì, Aspose fornisce una gamma di librerie per vari formati di file e attività di manipolazione di documenti. Dai un'occhiata alle loro offerte su[https://products.aspose.com/](https://products.aspose.com/).

### D5: Posso usare Aspose.HTML per .NET nelle mie applicazioni web?
R5: Sì, Aspose.HTML per .NET è compatibile con le applicazioni web, il che lo rende una scelta versatile sia per progetti desktop che basati sul web.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
