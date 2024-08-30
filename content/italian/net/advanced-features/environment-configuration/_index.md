---
title: Configurazione dell'ambiente in .NET con Aspose.HTML
linktitle: Configurazione dell'ambiente in .NET
second_title: Aspose.HTML API di manipolazione HTML .NET
description: Scopri come lavorare con documenti HTML in .NET usando Aspose.HTML per attività come gestione script, stili personalizzati, controllo esecuzione JavaScript e altro. Questo tutorial completo fornisce esempi passo dopo passo e FAQ per iniziare.
type: docs
weight: 10
url: /it/net/advanced-features/environment-configuration/
---

Nel mondo digitale odierno, creare e manipolare documenti HTML è un compito fondamentale per molti sviluppatori. Che tu stia creando un'applicazione web o che tu debba convertire HTML in altri formati come PDF o immagini, Aspose.HTML per .NET è uno strumento potente da avere nel tuo kit di strumenti. In questo tutorial, esploreremo vari aspetti di Aspose.HTML per .NET, inclusi prerequisiti, importazione di namespace ed esempi passo dopo passo con spiegazioni dettagliate.

## Prerequisiti

Prima di addentrarci nell'uso di Aspose.HTML per .NET, è necessario assicurarsi di disporre dei seguenti prerequisiti:

1. Visual Studio: assicurati di avere Visual Studio installato sul tuo computer di sviluppo. Aspose.HTML per .NET è progettato per funzionare senza problemi con Visual Studio.

2.  Aspose.HTML per .NET: puoi scaricare la libreria Aspose.HTML per .NET dal sito web. Usa il seguente link per accedere alla pagina di download:[Scarica Aspose.HTML per .NET](https://releases.aspose.com/html/net/).

3.  Installazione e licenza: dopo aver scaricato la libreria, segui le istruzioni di installazione fornite nella documentazione. Potresti anche aver bisogno di una licenza valida per usare alcune delle funzionalità avanzate. Puoi ottenere una licenza dal sito web Aspose:[Acquista la licenza Aspose.HTML](https://purchase.aspose.com/buy).

4.  Prova gratuita: se vuoi provare Aspose.HTML prima di acquistare una licenza, puoi ottenere una versione di prova gratuita da questo link:[Prova gratuita di Aspose.HTML](https://releases.aspose.com/).

Ora che hai i prerequisiti necessari, passiamo alla sezione successiva in cui importeremo gli spazi dei nomi richiesti.

## Importazione degli spazi dei nomi

Per lavorare efficacemente con Aspose.HTML per .NET, dovrai importare gli spazi dei nomi appropriati nel tuo progetto. Di seguito, elencheremo gli spazi dei nomi di cui hai bisogno per gli esempi che tratteremo:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Una volta importati questi namespace, è possibile accedere alle funzionalità fornite da Aspose.HTML per .NET.

## Disabilita l'esecuzione degli script

Iniziamo con un esempio di base di disattivazione dell'esecuzione di script all'interno di un documento HTML e conversione in PDF. Segui questi passaggi:

1. Crea un frammento di codice HTML e salvalo in un file denominato "document.html".

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Inizializza la configurazione di Aspose.HTML, contrassegnando 'script' come risorsa non attendibile.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Inizializza un documento HTML con la configurazione specificata
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Convertire HTML in PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

In questo esempio, abbiamo impedito l'esecuzione di script all'interno del documento HTML, garantendo la sicurezza durante la conversione in PDF. Ora, passiamo all'esempio successivo.

## Specificare il foglio di stile utente

A volte, potresti voler applicare stili personalizzati agli elementi all'interno di un documento HTML. Ecco come puoi farlo usando Aspose.HTML per .NET:

1. Crea un frammento di codice HTML e salvalo in un file denominato "document.html".

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  Imposta un colore personalizzato per il`<span>` elemento che utilizza un foglio di stile utente.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Inizializza un documento HTML con la configurazione specificata
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Convertire HTML in PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 In questo esempio, abbiamo applicato uno stile personalizzato al`<span>` elemento, impostando il colore del testo su verde. Aspose.HTML per .NET consente di manipolare gli stili con facilità.

## Timeout di esecuzione di JavaScript

Quando si ha a che fare con codice JavaScript potenzialmente dispendioso in termini di tempo, è essenziale impostare un timeout per impedire l'esecuzione indefinita. Ecco come puoi farlo:

1. Crea un frammento di codice HTML con un ciclo infinito e salvalo in un file denominato "document.html".

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Imposta un timeout di esecuzione JavaScript a 10 secondi.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // Inizializza un documento HTML con la configurazione specificata
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Attendi che tutti gli script siano terminati/annullati e converti HTML in PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

In questo esempio, abbiamo limitato il tempo di esecuzione di JavaScript a 10 secondi, assicurandoci che lo script non venga eseguito indefinitamente, il che potrebbe causare potenziali problemi di prestazioni.

## Gestore messaggi personalizzato

A volte, potresti dover gestire messaggi di errore o risorse mancanti quando carichi un documento HTML. Ecco un esempio di come creare un gestore di messaggi personalizzato:

1. Crea un frammento di codice HTML con un riferimento al file immagine mancante e salvalo in un file denominato "document.html".

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. Aggiungere un gestore dei messaggi di errore al servizio di rete per registrare le richieste non riuscite.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // Inizializza un documento HTML con la configurazione specificata
    // Durante il caricamento del documento, l'applicazione proverà a caricare l'immagine e vedremo il risultato di questa operazione nella console.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Convertire HTML in PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

In questo esempio, abbiamo aggiunto un gestore di messaggi personalizzato (`LogMessageHandler`) per registrare informazioni sulle richieste non riuscite. Ciò può essere particolarmente utile per il debug e la gestione delle risorse mancanti in modo elegante.

## Conclusione

Aspose.HTML per .NET è una libreria versatile che consente agli sviluppatori di lavorare in modo efficiente con i documenti HTML. In questo tutorial, abbiamo trattato concetti essenziali e fornito esempi passo-passo per attività comuni, tra cui gestione degli script, personalizzazione dei fogli di stile, controllo dell'esecuzione di JavaScript e gestione dei messaggi personalizzati.

Seguendo i passaggi descritti in questo tutorial, potrai sfruttare la potenza di Aspose.HTML per .NET per creare, manipolare e convertire documenti HTML nelle tue applicazioni .NET in tutta sicurezza.

## Domande frequenti

### D1: Posso utilizzare Aspose.HTML per .NET senza acquistare una licenza?

R1: Sì, puoi provare Aspose.HTML per .NET con una versione di prova gratuita, ma alcune funzionalità avanzate potrebbero richiedere una licenza valida.

### D2: Come posso ottenere una licenza per Aspose.HTML per .NET?

 A2: Puoi acquistare una licenza dal sito web di Aspose:[Acquista la licenza Aspose.HTML](https://purchase.aspose.com/buy).

### D3: In quali formati posso convertire i documenti HTML utilizzando Aspose.HTML per .NET?

A3: Aspose.HTML per .NET supporta la conversione in vari formati, tra cui PDF, immagini e altro ancora.

### D4: Esiste una community o un forum di supporto per Aspose.HTML per .NET?

 A4: Sì, puoi trovare aiuto e supporto sui forum di Aspose:[Forum di supporto Aspose.HTML](https://forum.aspose.com/).

### D5: Aspose.HTML per .NET fornisce documentazione e tutorial?

 A5: Sì, puoi accedere alla documentazione qui:[Documentazione di Aspose.HTML per .NET](https://reference.aspose.com/html/net/).