---
title: Ottimizzazione dei convertitori in .NET con Aspose.HTML
linktitle: Ottimizzazione dei convertitori in .NET
second_title: Aspose.HTML API di manipolazione HTML .NET
description: Scopri come convertire HTML in PDF, XPS e immagini con Aspose.HTML per .NET. Esercitazione dettagliata con esempi di codice e FAQ.
weight: 16
url: /it/net/advanced-features/fine-tuning-converters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ottimizzazione dei convertitori in .NET con Aspose.HTML


## Introduzione

Aspose.HTML per .NET è una potente libreria che consente agli sviluppatori di manipolare e convertire documenti HTML in vari formati. Che tu debba convertire HTML in PDF, XPS o immagini, o eseguire altre attività correlate a HTML, Aspose.HTML fornisce un robusto set di strumenti per aiutarti a portare a termine il lavoro.

In questo tutorial, esploreremo alcune funzionalità essenziali di Aspose.HTML per .NET e forniremo spiegazioni passo dopo passo per ogni esempio. Alla fine di questo tutorial, avrai una solida comprensione di come usare Aspose.HTML per .NET nelle tue applicazioni .NET.

## Prerequisiti

Prima di addentrarci negli esempi, assicurati di avere i seguenti prerequisiti:

-  Aspose.HTML per .NET: dovresti avere installata la libreria Aspose.HTML per .NET. Puoi scaricarla da[collegamento per il download](https://releases.aspose.com/html/net/).

-  Licenza temporanea (facoltativa): se non si dispone di una licenza valida, è possibile ottenere una licenza temporanea da[Qui](https://purchase.aspose.com/temporary-license/).

Ora esploriamo alcuni casi d'uso comuni con Aspose.HTML per .NET.

## Importazione degli spazi dei nomi

Nel codice C#, inizia importando gli spazi dei nomi necessari:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Convertire HTML in PDF

### Passaggio 1: preparare il codice HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Passaggio 2: inizializzare il documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passaggio 3: creare un dispositivo PDF e specificare il file di output

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Passaggio 4: Trasformare l'HTML in PDF

```csharp
document.RenderTo(device);
```

Questo esempio converte uno snippet HTML in un documento PDF. Puoi personalizzare il codice HTML e il file di output in base alle tue esigenze.

## Imposta dimensione pagina personalizzata

### Passaggio 1: preparare il codice HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Passaggio 2: inizializzare il documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passaggio 3: creare opzioni di rendering PDF

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Passaggio 4: creare un dispositivo PDF e specificare le opzioni e il file di output

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Passaggio 5: Trasformare l'HTML in PDF

```csharp
document.RenderTo(device);
```

Questo esempio mostra come impostare una dimensione di pagina personalizzata per il documento PDF risultante.

## Regola la risoluzione

### Passaggio 1: preparare il codice HTML e salvarlo nel file

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Passaggio 2: inizializzare il documento HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Passaggio 3: creare opzioni di rendering PDF per bassa risoluzione

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Passaggio 4: creare un dispositivo PDF e specificare le opzioni e il file di output per la bassa risoluzione

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Passaggio 5: rendering di HTML in PDF per bassa risoluzione

```csharp
document.RenderTo(device);
```

### Passaggio 6: creare opzioni di rendering PDF per alta risoluzione

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Passaggio 7: creare un dispositivo PDF e specificare le opzioni e il file di output per l'alta risoluzione

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Passaggio 8: rendering di HTML in PDF per alta risoluzione

```csharp
document.RenderTo(device);
```

Questo esempio illustra come regolare la risoluzione durante il rendering di HTML in PDF, tenendo conto sia degli schermi a bassa che di quelli ad alta risoluzione.

## Specificare il colore di sfondo

### Passaggio 1: preparare il codice HTML e salvarlo nel file

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Passaggio 2: inizializzare il documento HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Passaggio 3: inizializzare le opzioni di rendering PDF con il colore di sfondo

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Passaggio 4: creare un dispositivo PDF e specificare le opzioni e il file di output

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Passaggio 5: Trasformare l'HTML in PDF

```csharp
document.RenderTo(device);
```

Questo esempio mostra come specificare un colore di sfondo durante la conversione di HTML in PDF.

## Imposta le dimensioni della pagina sinistra e destra

### Passaggio 1: preparare il codice HTML

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Passaggio 2: inizializzare il documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passaggio 3: creare opzioni di rendering PDF con dimensioni di pagina sinistra e destra

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Passaggio 4: creare un dispositivo PDF e specificare le opzioni e il file di output

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Passaggio 5: Trasformare l'HTML in PDF

```csharp
document.RenderTo(device);
```

Questo esempio mostra come impostare dimensioni di pagina diverse per la pagina sinistra e quella destra durante la conversione di HTML in PDF.

## Adatta le dimensioni della pagina al contenuto

### Passaggio 1: preparare il codice HTML

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Passaggio 2: inizializzare il documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passaggio 3: creare opzioni di rendering PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Passaggio 4: creare un dispositivo PDF e specificare le opzioni e il file di output

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Passaggio 5: Trasformare l'HTML in PDF

```csharp
document.RenderTo(device);
```

Questo esempio mostra come adattare le dimensioni della pagina al contenuto più ampio durante la conversione di HTML in PDF.

## Specificare le autorizzazioni PDF

### Passaggio 1: preparare il codice HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Passaggio 2: inizializzare il documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passaggio 3: creare opzioni di rendering PDF con autorizzazioni

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Passaggio 4: creare un dispositivo PDF e specificare le opzioni e il file di output

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Passaggio 5: Trasformare l'HTML in PDF

```csharp
document.RenderTo(device);
```

Questo esempio mostra come specificare autorizzazioni e crittografia durante la conversione di HTML in un PDF protetto.

## Specificare le opzioni specifiche dell'immagine

### Passaggio 1: preparare il codice HTML

```csharp
var code = @"<div>Hello World!!</div>";
```

### Passaggio 2: inizializzare il documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passaggio 3: creare opzioni di rendering delle immagini

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Passaggio 4: creare il dispositivo immagine e specificare le opzioni e il file di output

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Passaggio 5: rendering dell'HTML in immagine

```csharp
document.RenderTo(device);
```

Questo esempio mostra come convertire l'HTML in un'immagine con opzioni di rendering specifiche, come formato, risoluzione e modalità di levigatura.

## Specificare le opzioni di rendering XPS

### Passaggio 1: preparare il codice HTML

```csharp
var code = @"<span>Hello World!!</span>";
```

### Passaggio 2: inizializzare il documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passaggio 3: creare opzioni di rendering XPS con dimensioni di pagina

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Passaggio 4: creare un dispositivo XPS e specificare le opzioni e il file di output

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Passaggio 5: rendering HTML in XPS

```csharp
document.RenderTo(device);
```

Questo esempio mostra come convertire HTML in XPS con dimensioni di pagina e opzioni di rendering personalizzate.

## Combina più documenti HTML in PDF

### Passaggio 1: preparare il codice HTML per più documenti

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Passaggio 2: creare documenti HTML da unire

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Passaggio 3: inizializzare il renderer HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Passaggio 4: creare un dispositivo PDF per l'output unito

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Passaggio 5: unire i documenti HTML in PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

Questo esempio mostra come combinare più documenti HTML in un unico file PDF utilizzando Aspose.HTML per .NET.

## Imposta timeout di rendering

### Passaggio 1: preparare il codice HTML con JavaScript

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Passaggio 2: inizializzare il documento HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Passaggio 3: inizializzare il renderer HTML

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Passaggio 4: creare un dispositivo PDF e impostare il timeout di rendering

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Passaggio 5: rendering di HTML in PDF con timeout

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Questo esempio mostra come impostare un timeout di rendering durante la conversione di HTML in PDF, il che può essere utile quando si ha a che fare con contenuti dinamici o script di lunga durata.

## Conclusione

Aspose.HTML per .NET è una libreria versatile che consente agli sviluppatori di lavorare in modo efficiente con i documenti HTML. In questo tutorial, abbiamo trattato vari esempi, dalle conversioni di base da HTML a PDF a funzionalità più avanzate come dimensioni di pagina personalizzate, risoluzioni e permessi. Seguendo questi esempi, puoi sfruttare appieno il potenziale di Aspose.HTML per .NET nelle tue applicazioni .NET.

 Se hai domande o hai bisogno di ulteriore assistenza, non esitare a visitare il[Forum di Aspose.HTML](https://forum.aspose.com/) per supporto e guida.

## Domande frequenti

### D1. Che cos'è Aspose.HTML per .NET?
   
A1: Aspose.HTML per .NET è una libreria .NET che consente agli sviluppatori di manipolare e convertire i documenti HTML a livello di programmazione. Offre un'ampia gamma di funzionalità per lavorare con contenuti HTML, tra cui HTML in PDF, XPS e conversione di immagini, nonché opzioni di rendering avanzate.

### D2. Dove posso scaricare Aspose.HTML per .NET?

 A2: Puoi scaricare Aspose.HTML per .NET da[collegamento per il download](https://releases.aspose.com/html/net/).

### D3. Ho bisogno di una licenza per utilizzare Aspose.HTML per .NET?

R3: Sebbene sia possibile utilizzare Aspose.HTML per .NET senza licenza, si consiglia di ottenere una licenza per l'uso in produzione per sbloccare tutte le funzionalità e rimuovere eventuali filigrane o limitazioni.

### D4. Come posso proteggere i miei file PDF generati con Aspose.HTML per .NET?

A4: È possibile specificare le autorizzazioni PDF e le impostazioni di crittografia quando si esegue il rendering di HTML in PDF utilizzando Aspose.HTML per .NET. Ciò consente di controllare chi può accedere e modificare i file PDF risultanti.

### D5. Posso convertire l'HTML in altri formati come XPS o immagini?

A5: Sì, Aspose.HTML per .NET supporta la conversione di HTML in vari formati, tra cui PDF, XPS e immagini (ad esempio, JPEG). Puoi personalizzare le impostazioni di conversione per soddisfare i tuoi requisiti specifici.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
