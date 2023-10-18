---
title: Creazione di un documento in .NET con Aspose.HTML
linktitle: Creazione di un documento in .NET
second_title: Aspose.HTML .NET API di manipolazione HTML
description: Scatena la potenza di Aspose.HTML per .NET. Impara a creare, manipolare e ottimizzare documenti HTML e SVG con facilità. Esplora esempi passo passo e domande frequenti.
type: docs
weight: 14
url: /it/net/html-document-manipulation/creating-a-document/
---

Nel mondo in continua evoluzione dello sviluppo web, rimanere al passo con i tempi è essenziale. Aspose.HTML per .NET fornisce agli sviluppatori un robusto toolkit per lavorare con documenti HTML. Che tu stia iniziando da zero, caricando da un file, estraendo da un URL o gestendo documenti SVG, questa libreria offre la versatilità di cui hai bisogno.

In questa guida passo passo, approfondiremo i fondamenti dell'utilizzo di Aspose.HTML per .NET, assicurandoci che tu sia ben attrezzato per utilizzare questo potente strumento nei tuoi progetti di sviluppo web. Prima di immergerci nei dettagli, esaminiamo i prerequisiti e gli spazi dei nomi necessari per iniziare il tuo viaggio.

## Prerequisiti

Per seguire con successo questo tutorial e sfruttare la potenza di Aspose.HTML per .NET, avrai bisogno dei seguenti prerequisiti:

- Un computer Windows con .NET Framework o .NET Core installato.
- Un editor di codice come Visual Studio.
- Conoscenza base della programmazione C#.

Ora che hai definito i prerequisiti, iniziamo.

## Importazione di spazi dei nomi

Prima di iniziare a utilizzare Aspose.HTML per .NET, è necessario importare gli spazi dei nomi necessari. Questi spazi dei nomi contengono classi e metodi vitali per lavorare con i documenti HTML. Di seguito è riportato un elenco degli spazi dei nomi che dovresti importare:

```csharp
using Aspose.Html;
using Aspose.Html.Dom.Svg;
```

Una volta importati questi spazi dei nomi, sei ora pronto per immergerti negli esempi passo passo.

## Creare un documento HTML da zero

### Passaggio 1: inizializza un documento HTML vuoto

```csharp
// Inizializza un documento HTML vuoto.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Crea un elemento di testo e aggiungilo al documento
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Salvare il documento su disco.
    document.Save("document.html");
}
```

In questo esempio, iniziamo creando un documento HTML vuoto e aggiungendo un messaggio "Hello World!" mandagli un SMS. Salviamo quindi il documento in un file.

## Creazione di un documento HTML da un file

### Passaggio 1: preparare un file "document.html".

```csharp
System.IO.File.WriteAllText("document.html", "Hello World!");
```

### Passaggio 2: carica da un file "document.html".

```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Scrivere il contenuto del documento nel flusso di output.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Qui prepariamo un file con "Hello World!" contenuto e quindi caricarlo come documento HTML. Stampiamo il contenuto del documento sulla console.

## Creazione di un documento HTML da un URL

### Passaggio 1: carica un documento da una pagina web

```csharp
using (var document = new Aspose.Html.HTMLDocument("https://html.spec.whatwg.org/multipage/introduction.html"))
{
    // Scrivere il contenuto del documento nel flusso di output.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

In questo esempio, carichiamo un documento HTML direttamente da una pagina web e ne visualizziamo il contenuto.

## Creazione di un documento HTML da una stringa

### Passaggio 1: preparare un codice HTML

```csharp
var html_code = "<p>Hello World!</p>";
```

### Passaggio 2: inizializza il documento dalla variabile stringa

```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Salvare il documento su disco.
    document.Save("document.html");
}
```

Qui creiamo un documento HTML da una variabile stringa e lo salviamo in un file.

## Creazione di un documento HTML da un MemoryStream

### Passaggio 1: creare un oggetto flusso di memoria

```csharp
using (var mem = new System.IO.MemoryStream())
using (var sw = new System.IO.StreamWriter(mem))
{
    // Scrivi il codice HTML nell'oggetto memoria
    sw.Write("<p>Hello World!</p>");
    // Imposta la posizione all'inizio
    sw.Flush();
    mem.Seek(0, System.IO.SeekOrigin.Begin);
    // Inizializza il documento dal flusso di memoria
    using (var document = new Aspose.Html.HTMLDocument(mem, "."))
    {
        // Salvare il documento su disco.
        document.Save("document.html");
    }
}
```

In questo esempio creiamo un documento HTML da un flusso di memoria e lo salviamo in un file.

## Lavorare con documenti SVG

### Passaggio 1: inizializza il documento SVG da una stringa

```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "."))
{
    // Scrivere il contenuto del documento nel flusso di output.
    Console.WriteLine(document.DocumentElement.OuterHTML);
}
```

Qui creiamo e visualizziamo un documento SVG da una stringa.

## Caricamento di un documento HTML in modo asincrono

### Passaggio 1: crea l'istanza del documento HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Passaggio 2: iscriviti all'evento "ReadyStateChange".

```csharp
document.OnReadyStateChange += (sender, @event) =>
{
    //Controlla il valore della proprietà "ReadyState".
    if (document.ReadyState == "complete")
    {
        Console.WriteLine(document.DocumentElement.OuterHTML);
        Console.WriteLine("Loading is completed. Press any key to continue...");
    }
};
```

### Passaggio 3: navigare in modo asincrono nell'URI specificato

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

In questo esempio, carichiamo un documento HTML in modo asincrono e gestiamo l'evento "ReadyStateChange" per visualizzare il contenuto al termine del caricamento.

## Gestione dell'evento "OnLoad".

### Passaggio 1: crea l'istanza del documento HTML

```csharp
var document = new Aspose.Html.HTMLDocument();
```

### Passaggio 2: iscriviti all'evento "OnLoad".

```csharp
document.OnLoad += (sender, @event) =>
{
    Console.WriteLine(document.DocumentElement.OuterHTML);
    Console.WriteLine("Loading is completed. Press any key to continue...");
};
```

### Passaggio 3: navigare in modo asincrono nell'URI specificato

```csharp
document.Navigate("https://html.spec.whatwg.org/multipage/introduction.html");
Console.WriteLine("Waiting for loading...");
Console.ReadLine();
```

Questo esempio dimostra il caricamento di un documento HTML in modo asincrono e la gestione dell'evento "OnLoad" per visualizzare il contenuto al termine.

## Insomma

Nel dinamico mondo dello sviluppo web, avere gli strumenti giusti a propria disposizione è fondamentale. Aspose.HTML per .NET ti fornisce i mezzi per creare, manipolare ed elaborare documenti HTML e SVG in modo efficiente. Questa guida completa ti ha guidato attraverso gli elementi essenziali, assicurandoti di poter sfruttare la potenza di Aspose.HTML per .NET nei tuoi progetti.

## Domande frequenti

### Q1: Cos'è Aspose.HTML per .NET?

A1: Aspose.HTML per .NET è una potente libreria .NET che consente agli sviluppatori di lavorare con documenti HTML e SVG. Fornisce un'ampia gamma di funzionalità, dalla creazione di documenti da zero all'analisi e alla manipolazione di file HTML e SVG esistenti.

### Q2: posso utilizzare Aspose.HTML per .NET con .NET Core?

A2: Sì, Aspose.HTML per .NET è compatibile sia con .NET Framework che con .NET Core, rendendolo una scelta versatile per le moderne applicazioni .NET.

### Q3: Aspose.HTML per .NET è adatto per il web scraping e l'analisi?

A3: Assolutamente! Aspose.HTML per .NET è una scelta eccellente per attività di web scraping e parsing, grazie alla sua capacità di caricare documenti HTML da URL e stringhe. Puoi estrarre dati, eseguire analisi e altro ancora.

### Q4: Come posso accedere al supporto per Aspose.HTML per .NET?

 A4: Se riscontri problemi o hai domande durante l'utilizzo di Aspose.HTML per .NET, puoi visitare il[Aspose Forum](https://forum.aspose.com/) per il supporto e l'assistenza della comunità e degli esperti Aspose.

### A5: Dove posso trovare la documentazione dettagliata e le opzioni di download?

R5: Per la documentazione completa e l'accesso alle opzioni di download, è possibile fare riferimento ai seguenti collegamenti:

- [Documentazione](https://reference.aspose.com/html/net/)
- [Scaricamento](https://releases.aspose.com/html/net/)
- [Acquistare](https://purchase.aspose.com/buy)
- [Prova gratuita](https://releases.aspose.com/)
- [Licenza temporanea](https://purchase.aspose.com/temporary-license/)