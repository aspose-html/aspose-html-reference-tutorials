---
title: Salvataggio di un documento in .NET con Aspose.HTML
linktitle: Salvare un documento in .NET
second_title: Aspose.Slides API di manipolazione HTML .NET
description: Sblocca la potenza di Aspose.HTML per .NET con la nostra guida passo passo. Impara a creare, manipolare e convertire documenti HTML e SVG
type: docs
weight: 16
url: /it/net/html-document-manipulation/saving-a-document/
---

Nell'era digitale di oggi, la creazione e la manipolazione di documenti HTML e SVG è essenziale per molti sviluppatori di software e aziende. Aspose.HTML per .NET è una potente libreria che semplifica queste attività, offrendo varie funzionalità per lavorare con HTML, SVG e altro. In questa guida completa, approfondiremo gli elementi essenziali di Aspose.HTML per .NET, suddividendo ogni esempio in passaggi facili da seguire. Che tu sia uno sviluppatore esperto o che tu abbia appena iniziato, troverai questa guida preziosa per sfruttare le funzionalità di Aspose.HTML.

## Prerequisiti

Prima di intraprendere questo viaggio, assicuriamoci di avere tutto ciò di cui hai bisogno:

- Ambiente di sviluppo: assicurati di avere Visual Studio o qualsiasi altro ambiente di sviluppo .NET installato sul tuo computer.

-  Aspose.HTML per .NET: è necessario ottenere la libreria Aspose.HTML per .NET. Puoi scaricarlo da[Qui](https://releases.aspose.com/html/net/).

- Conoscenza di C#: la familiarità con il linguaggio di programmazione C# è utile ma non obbligatoria. Questa guida è progettata per essere adatta ai principianti.

## Importa spazio dei nomi

Per iniziare a utilizzare Aspose.HTML per .NET, dovrai importare gli spazi dei nomi necessari nel tuo progetto. Nel codice C#, includi il seguente spazio dei nomi:

### Passaggio 1: importare lo spazio dei nomi Aspose.HTML
```csharp
using Aspose.Html;
```

Questo spazio dei nomi ti garantirà l'accesso a varie funzionalità di manipolazione HTML e SVG.

## HTML su file

### Passaggio 1: inizializza un documento HTML vuoto
```csharp
// Inizializza un documento HTML vuoto.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Crea un elemento di testo e aggiungilo al documento
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Salvare l'HTML nel file su disco.
    document.Save("document.html");
}
```

In questo esempio creiamo un documento HTML e aggiungiamo un semplice "Hello World!" mandagli un SMS. Quindi salviamo l'HTML in un file sul disco.

## HTML senza file collegato

### Passaggio 1: preparare un semplice file HTML
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Qui creiamo un file HTML di base con un collegamento di ancoraggio a un altro file.

### Passaggio 2: carica "document.html" in memoria
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Crea un'istanza di opzioni di salvataggio
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    // Imposta la profondità di gestione massima su 0 per tagliare i file HTML collegati.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Salva il documento
    document.Save(@".\html-to-file-example\document.html", options);
}
```

In questo esempio, carichiamo un documento HTML in memoria, impostiamo la massima profondità di gestione per tagliare i file collegati e salviamo il documento. 

## Da HTML a MHTML

### Passaggio 1: preparare un semplice file HTML
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Proprio come nell'esempio 2, creiamo un file HTML di base con un collegamento di ancoraggio a un altro file.

### Passaggio 2: carica "document.html" in memoria e salva come MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Salva il documento come MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Qui carichiamo il documento HTML in memoria e lo salviamo in formato MHTML.

## HTML per Markdown

### Passaggio 1: preparare un codice HTML
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 In questo passaggio definiamo uno snippet di codice HTML contenente un file`<H2>` elemento.

### Passaggio 2: inizializza il documento dal codice HTML e salva come Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Salva il documento come file Markdown.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Creiamo un documento HTML dallo snippet di codice e lo salviamo come file Markdown.

## SVG su file

### Passaggio 1: preparare un codice SVG
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' altezza='80' larghezza='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Qui creiamo un codice SVG che disegna una grafica semplice e colorata.

### Passaggio 2: inizializza un documento SVG dal codice e salva su disco
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Salva il file SVG sul disco
    document.Save("document.svg");
}
```

In questo passaggio creiamo un documento SVG dal codice e lo salviamo come file SVG.

## Conclusione

Aspose.HTML per .NET è una libreria versatile che semplifica la gestione dei documenti HTML e SVG nelle applicazioni .NET. In questa guida abbiamo trattato cinque esempi essenziali, suddividendoli ciascuno in istruzioni passo passo. Che tu stia creando, manipolando o convertendo documenti, Aspose.HTML ti copre. Seguendo questi passaggi, sei sulla buona strada per padroneggiare questo potente strumento.

## Domande frequenti

### Q1: Cos'è Aspose.HTML per .NET?

A1: Aspose.HTML per .NET è una libreria .NET che fornisce un'ampia gamma di funzionalità per lavorare con documenti HTML e SVG, inclusa la creazione, la manipolazione e la conversione.

### Q2: Dove posso scaricare Aspose.HTML per .NET?

 A2: È possibile scaricare Aspose.HTML per .NET da[Qui](https://releases.aspose.com/html/net/).

### Q3: Aspose.HTML per .NET è adatto ai principianti?

A3: Sì, Aspose.HTML per .NET può essere utilizzato sia dai principianti che dagli sviluppatori esperti. Gli esempi in questa guida sono progettati per essere adatti ai principianti.

### Q4: Posso convertire HTML in altri formati utilizzando Aspose.HTML per .NET?

A4: Sì, Aspose.HTML per .NET supporta la conversione in vari formati, inclusi MHTML e Markdown, come mostrato negli esempi.

### Q5: Dove posso ottenere supporto per Aspose.HTML per .NET?

 R5: Puoi trovare supporto e risposte alle tue domande nel forum della community Aspose.HTML[Qui](https://forum.aspose.com/).