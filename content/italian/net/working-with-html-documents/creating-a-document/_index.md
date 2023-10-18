---
title: Creazione di un documento HTML in .NET con Aspose.HTML
linktitle: Creazione di un documento HTML in .NET
second_title: Aspose.HTML .NET API di manipolazione HTML
description: Scopri come creare documenti HTML in .NET utilizzando Aspose.HTML, da zero o da URL. Un tutorial completo per gli sviluppatori web.
type: docs
weight: 10
url: /it/net/working-with-html-documents/creating-a-document/
---

Nel campo dello sviluppo web e della manipolazione dei dati, è indispensabile disporre di un potente strumento per creare, modificare e lavorare con documenti HTML. Aspose.HTML per .NET è uno di questi strumenti che può semplificare le attività relative all'HTML. In questo tutorial completo, esploreremo come creare documenti HTML utilizzando Aspose.HTML per .NET passo dopo passo. Prima di immergerci negli esempi, esaminiamo alcuni prerequisiti.

## Prerequisiti

Prima di intraprendere questo viaggio, assicurati di possedere i seguenti prerequisiti:

1. Visual Studio: assicurati di avere Visual Studio installato sul tuo sistema.

2.  Aspose.HTML per .NET: scarica e installa la libreria Aspose.HTML per .NET. È possibile trovare il collegamento per il download[Qui](https://releases.aspose.com/html/net/).

3. Conoscenza di base di C#: familiarizza con le nozioni di base del linguaggio di programmazione C#.

Ora che abbiamo coperto i prerequisiti, iniziamo con la creazione di documenti HTML.

## Importazione di spazi dei nomi

Innanzitutto, devi importare gli spazi dei nomi necessari per utilizzare Aspose.HTML nel tuo progetto C#. Aggiungi le seguenti direttive using al tuo file di codice:

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
        // Esegui azioni sul documento SVG qui...
    }
}
```

 In questo esempio, creiamo un documento SVG fornendo il contenuto SVG e un URL di base. IL`SVGDocument`La classe Aspose.HTML per .NET ti consente di manipolare i documenti SVG senza sforzo.

## Creare un documento HTML da zero

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // Esegui azioni sul documento HTML qui...
    }
}
```

 Questo esempio dimostra come creare un documento HTML da zero. IL`HTMLDocument` La classe fornisce una tela vuota per il tuo contenuto HTML.

## Creazione di un documento HTML da un file locale

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // Esegui azioni sul documento HTML qui...
    }
}
```

 Se hai un file HTML esistente sul tuo sistema locale, puoi caricarlo utilizzando il file`HTMLDocument` classe, come mostrato in questo esempio.

## Creazione di un documento HTML da un URL remoto

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://tuo.sito.com/"))
    {
        // Esegui azioni sul documento HTML qui...
    }
}
```

A volte potrebbe essere necessario lavorare con contenuto HTML ospitato su un server remoto. Questo esempio dimostra come creare un documento HTML da un URL remoto.

## Creazione di un documento HTML da un URL remoto (alternativa)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://tuo.sito.com/")))
    {
        // Esegui azioni sul documento HTML qui...
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
        // Esegui azioni sul documento HTML qui...
    }
}
```

Se disponi di contenuto HTML in formato stringa, puoi creare un documento HTML con esso, come dimostrato in questo esempio.

## Creazione di un documento HTML da uno stream

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
            // Esegui azioni sul documento HTML qui...
        }
    }
}
```

In questo esempio mostriamo come creare un documento HTML dai dati in un flusso di memoria. Ciò può essere utile quando hai contenuto HTML in uno stream e desideri manipolarlo.

## Conclusione

Aspose.HTML per .NET fornisce un potente set di strumenti per creare e lavorare con documenti HTML nelle applicazioni .NET. Con gli esempi forniti in questo tutorial, puoi iniziare facilmente a creare documenti HTML, da zero, file locali, URL remoti o contenuto HTML esistente.

 Hai domande o hai bisogno di assistenza? Visita il forum della comunità Aspose.HTML per supporto all'indirizzo[https://forum.aspose.com/](https://forum.aspose.com/).

## Domande frequenti

### Q1: Aspose.HTML per .NET è gratuito?
 A1: Aspose.HTML per .NET offre una prova gratuita, ma per l'utilizzo completo sarà necessario acquistare una licenza. Puoi trovare maggiori dettagli su[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### Q2: Come posso ottenere una licenza temporanea per Aspose.HTML per .NET?
R2: Se hai bisogno di una licenza temporanea, puoi ottenerne una su[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### Q3: Dove posso trovare la documentazione per Aspose.HTML per .NET?
 R3: La documentazione è reperibile all'indirizzo[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### Q4: Esistono altre librerie Aspose per lo sviluppo .NET?
 R4: Sì, Aspose fornisce una gamma di librerie per vari formati di file e attività di manipolazione dei documenti. Controlla le loro offerte su[https://prodotti.aspose.com/](https://products.aspose.com/).

### Q5: posso utilizzare Aspose.HTML per .NET nelle mie applicazioni web?
A5: Sì, Aspose.HTML per .NET è compatibile con le applicazioni web, rendendolo una scelta versatile sia per progetti desktop che basati sul web.
