---
title: Salvataggio di un documento in .NET con Aspose.HTML
linktitle: Salvataggio di un documento in .NET
second_title: Aspose.HTML API di manipolazione HTML .NET
description: Sblocca la potenza di Aspose.HTML per .NET con la nostra guida passo-passo. Impara a creare, manipolare e convertire documenti HTML e SVG
weight: 16
url: /it/net/html-document-manipulation/saving-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salvataggio di un documento in .NET con Aspose.HTML


Nell'era digitale odierna, creare e manipolare documenti HTML e SVG è essenziale per molti sviluppatori software e aziende. Aspose.HTML per .NET è una potente libreria che semplifica queste attività, offrendo varie funzionalità per lavorare con HTML, SVG e altro. In questa guida completa, approfondiremo gli elementi essenziali di Aspose.HTML per .NET, suddividendo ogni esempio in passaggi facili da seguire. Che tu sia uno sviluppatore esperto o alle prime armi, troverai questa guida preziosa per sfruttare le capacità di Aspose.HTML.

## Prerequisiti

Prima di intraprendere questo viaggio, assicuriamoci di avere tutto ciò di cui hai bisogno:

- Ambiente di sviluppo: assicurati di avere Visual Studio o qualsiasi altro ambiente di sviluppo .NET installato sul tuo computer.

- Aspose.HTML per .NET: devi procurarti la libreria Aspose.HTML per .NET. Puoi scaricarla da[Qui](https://releases.aspose.com/html/net/).

- Conoscenza di C#: la familiarità con il linguaggio di programmazione C# è utile ma non obbligatoria. Questa guida è progettata per essere adatta ai principianti.

## Importa spazio dei nomi

Per iniziare a usare Aspose.HTML per .NET, dovrai importare i namespace necessari nel tuo progetto. Nel tuo codice C#, includi il seguente namespace:

### Passaggio 1: importare lo spazio dei nomi Aspose.HTML
```csharp
using Aspose.Html;
```

Questo spazio dei nomi ti garantirà l'accesso a varie funzionalità di manipolazione HTML e SVG.

## HTML in file

### Passaggio 1: inizializzare un documento HTML vuoto
```csharp
// Inizializza un documento HTML vuoto.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Crea un elemento di testo e aggiungilo al documento
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Salvare l'HTML nel file sul disco.
    document.Save("document.html");
}
```

In questo esempio, creiamo un documento HTML e aggiungiamo un semplice testo "Hello World!". Quindi salviamo l'HTML in un file sul disco.

## HTML senza file collegato

### Passaggio 1: preparare un semplice file HTML
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Qui creiamo un file HTML di base con un collegamento di ancoraggio a un altro file.

### Passaggio 2: caricare 'document.html' nella memoria
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Crea istanza Opzioni di salvataggio
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Impostare la profondità di gestione massima su 0 per tagliare i file HTML collegati.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Salva il documento
    document.Save(@".\html-to-file-example\document.html", options);
}
```

In questo esempio, carichiamo un documento HTML nella memoria, impostiamo la profondità di gestione massima per tagliare i file collegati e salviamo il documento. 

## Da HTML a MHTML

### Passaggio 1: preparare un semplice file HTML
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Proprio come nell'esempio 2, creiamo un file HTML di base con un collegamento di ancoraggio a un altro file.

### Passaggio 2: caricare 'document.html' nella memoria e salvare come MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Salva il documento come MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Qui carichiamo il documento HTML nella memoria e lo salviamo in formato MHTML.

## Da HTML a Markdown

### Passaggio 1: preparare un codice HTML
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 In questo passaggio, definiamo un frammento di codice HTML contenente un`<H2>` elemento.

### Passaggio 2: inizializzare il documento dal codice HTML e salvarlo come Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Salvare il documento come file Markdown.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Creiamo un documento HTML dal frammento di codice e lo salviamo come file Markdown.

## SVG in file

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

### Passaggio 2: inizializzare un documento SVG dal codice e salvarlo su disco
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Salvare il file SVG sul disco
    document.Save("document.svg");
}
```

In questa fase creiamo un documento SVG dal codice e lo salviamo come file SVG.

## Conclusione

Aspose.HTML per .NET è una libreria versatile che semplifica la gestione dei documenti HTML e SVG nelle applicazioni .NET. In questa guida, abbiamo trattato cinque esempi essenziali, suddividendoli in istruzioni dettagliate. Che tu stia creando, manipolando o convertendo documenti, Aspose.HTML ti copre. Seguendo questi passaggi, sei sulla buona strada per padroneggiare questo potente strumento.

## Domande frequenti

### D1: Che cos'è Aspose.HTML per .NET?

A1: Aspose.HTML per .NET è una libreria .NET che fornisce un'ampia gamma di funzionalità per lavorare con documenti HTML e SVG, tra cui creazione, manipolazione e conversione.

### D2: Dove posso scaricare Aspose.HTML per .NET?

 A2: Puoi scaricare Aspose.HTML per .NET da[Qui](https://releases.aspose.com/html/net/).

### D3: Aspose.HTML per .NET è adatto ai principianti?

A3: Sì, Aspose.HTML per .NET può essere utilizzato sia da principianti che da sviluppatori esperti. Gli esempi in questa guida sono progettati per essere adatti ai principianti.

### D4: Posso convertire HTML in altri formati utilizzando Aspose.HTML per .NET?

A4: Sì, Aspose.HTML per .NET supporta la conversione in vari formati, tra cui MHTML e Markdown, come mostrato negli esempi.

### D5: Dove posso ottenere supporto per Aspose.HTML per .NET?

 A5: Puoi trovare supporto e risposte alle tue domande nel forum della community Aspose.HTML[Qui](https://forum.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
