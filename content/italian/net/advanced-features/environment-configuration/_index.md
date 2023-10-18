---
title: Configurazione dell'ambiente in .NET con Aspose.HTML
linktitle: Configurazione dell'ambiente in .NET
second_title: Aspose.HTML .NET API di manipolazione HTML
description: Scopri come lavorare con documenti HTML in .NET utilizzando Aspose.HTML per attività come la gestione degli script, stili personalizzati, controllo dell'esecuzione JavaScript e altro ancora. Questo tutorial completo fornisce esempi passo passo e domande frequenti per iniziare.
type: docs
weight: 10
url: /it/net/advanced-features/environment-configuration/
---

Nel mondo digitale di oggi, creare e manipolare documenti HTML è un compito fondamentale per molti sviluppatori. Che tu stia creando un'applicazione Web o abbia bisogno di convertire HTML in altri formati come PDF o immagini, Aspose.HTML per .NET è un potente strumento da avere nel tuo toolkit. In questo tutorial esploreremo vari aspetti di Aspose.HTML per .NET, inclusi prerequisiti, importazione di spazi dei nomi ed esempi passo passo con spiegazioni dettagliate.

## Prerequisiti

Prima di approfondire l'utilizzo di Aspose.HTML per .NET, dovrai assicurarti di disporre dei seguenti prerequisiti:

1. Visual Studio: assicurati di avere Visual Studio installato nel computer di sviluppo. Aspose.HTML per .NET è progettato per funzionare perfettamente con Visual Studio.

2.  Aspose.HTML per .NET: è possibile scaricare la libreria Aspose.HTML per .NET dal sito Web. Utilizzare il seguente collegamento per accedere alla pagina di download:[Scarica Aspose.HTML per .NET](https://releases.aspose.com/html/net/).

3. Installazione e licenza: dopo aver scaricato la libreria, seguire le istruzioni di installazione fornite nella documentazione. Potrebbe anche essere necessaria una licenza valida per utilizzare alcune delle funzionalità avanzate. È possibile ottenere una licenza dal sito Web Aspose:[Acquista la licenza Aspose.HTML](https://purchase.aspose.com/buy).

4.  Prova gratuita: se vuoi provare Aspose.HTML prima di acquistare una licenza, puoi ottenere una versione di prova gratuita da questo link:[Prova gratuita di Aspose.HTML](https://releases.aspose.com/).

Ora che disponi dei prerequisiti necessari, procediamo alla sezione successiva in cui importeremo gli spazi dei nomi richiesti.

## Importa spazi dei nomi

Per lavorare in modo efficace con Aspose.HTML per .NET, dovrai importare gli spazi dei nomi appropriati nel tuo progetto. Di seguito elencheremo gli spazi dei nomi necessari per gli esempi che tratteremo:

```csharp
using Aspose.Html;
using Aspose.Html.Configuration;
using Aspose.Html.Sandbox;
using Aspose.Html.Services;
using Aspose.Html.Saving;
using System;
using System.IO;
```

Con questi spazi dei nomi importati, è possibile accedere alle funzionalità fornite da Aspose.HTML per .NET.

## Disabilita l'esecuzione degli script

Cominciamo con un esempio base di disabilitazione dell'esecuzione di script all'interno di un documento HTML e di conversione in PDF. Segui questi passi:

1. Crea uno snippet di codice HTML e salvalo in un file denominato "document.html".

```csharp
var code = "<span>Hello World!!</span> " +
           "<script>document.write('Have a nice day!');</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Inizializza la configurazione Aspose.HTML, contrassegnando gli "script" come risorse non attendibili.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    configuration.Security |= Aspose.Html.Sandbox.Scripts;
    
    // Inizializza un documento HTML con la configurazione specificata
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Converti HTML in PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

In questo esempio, abbiamo impedito l'esecuzione di script all'interno del documento HTML, garantendone la sicurezza durante la conversione in PDF. Ora passiamo all'esempio successivo.

## Specificare il foglio di stile dell'utente

A volte potresti voler applicare stili personalizzati agli elementi all'interno di un documento HTML. Ecco come puoi farlo utilizzando Aspose.HTML per .NET:

1. Crea uno snippet di codice HTML e salvalo in un file denominato "document.html".

```csharp
var code = @"<span>Hello World!!!</span>";
System.IO.File.WriteAllText("document.html", code);
```

2.  Imposta un colore personalizzato per`<span>` elemento utilizzando un foglio di stile utente.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var userAgent = configuration.GetService<Aspose.Html.Services.IUserAgentService>();
    userAgent.UserStyleSheet = "span { color: green; }";
    
    // Inizializza un documento HTML con la configurazione specificata
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Converti HTML in PDF
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.PdfSaveOptions(), "output.pdf");
    }
}
```

 In questo esempio, abbiamo applicato uno stile personalizzato al file`<span>`elemento, impostando il colore del testo su verde. Aspose.HTML per .NET ti consente di manipolare gli stili con facilità.

## Timeout di esecuzione JavaScript

Quando si ha a che fare con codice JavaScript potenzialmente dispendioso in termini di tempo, è essenziale impostare un timeout per impedire l'esecuzione indefinita. Ecco come puoi farlo:

1. Crea uno snippet di codice HTML con un ciclo infinito e salvalo in un file denominato "document.html".

```csharp
var code = @"<script>while(true){}</script>";
System.IO.File.WriteAllText("document.html", code);
```

2. Imposta un timeout di esecuzione JavaScript su 10 secondi.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var runtime = configuration.GetService<Aspose.Html.Services.IRuntimeService>();
    runtime.JavaScriptTimeout = TimeSpan.FromSeconds(10);
    
    // Inizializza un documento HTML con la configurazione specificata
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Attendi fino al completamento/annullamento di tutti gli script e converti l'HTML in PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

In questo esempio, abbiamo limitato il tempo di esecuzione di JavaScript a 10 secondi, garantendo che lo script non venga eseguito indefinitamente, il che potrebbe causare problemi di prestazioni.

## Gestore di messaggi personalizzato

A volte potrebbe essere necessario gestire messaggi di errore o risorse mancanti durante il caricamento di un documento HTML. Ecco un esempio di come creare un gestore di messaggi personalizzato:

1. Crea uno snippet di codice HTML con un riferimento al file immagine mancante e salvalo in un file denominato "document.html".

```csharp
var code = @"<img src='missing.jpg'>";
System.IO.File.WriteAllText("document.html", code);
```

2. Aggiungi un gestore di messaggi di errore al servizio di rete per registrare le richieste non riuscite.

```csharp
using (var configuration = new Aspose.Html.Configuration())
{
    var network = configuration.GetService<Aspose.Html.Services.INetworkService>();
    network.MessageHandlers.Add(new LogMessageHandler());
    
    // Inizializza un documento HTML con la configurazione specificata
    // Durante il caricamento del documento, l'applicazione tenterà di caricare l'immagine e vedremo il risultato di questa operazione nella console.
    using (var document = new Aspose.Html.HTMLDocument("document.html", configuration))
    {
        // Converti HTML in PNG
        Aspose.Html.Converters.Converter.ConvertHTML(document, new Aspose.Html.Saving.ImageSaveOptions(), "output.png");
    }
}
```

In questo esempio abbiamo aggiunto un gestore di messaggi personalizzato (`LogMessageHandler`) per registrare informazioni sulle richieste non riuscite. Ciò può essere particolarmente utile per eseguire il debug e gestire con garbo le risorse mancanti.

## Conclusione

Aspose.HTML per .NET è una libreria versatile che consente agli sviluppatori di lavorare in modo efficiente con i documenti HTML. In questo tutorial abbiamo trattato concetti essenziali e fornito esempi passo passo per attività comuni, tra cui la gestione degli script, la personalizzazione dei fogli di stile, il controllo dell'esecuzione di JavaScript e la gestione dei messaggi personalizzati.

Seguendo i passaggi descritti in questo tutorial, puoi sfruttare la potenza di Aspose.HTML per .NET per creare, manipolare e convertire documenti HTML nelle tue applicazioni .NET in tutta sicurezza.

## Domande frequenti

### Q1: posso utilizzare Aspose.HTML per .NET senza acquistare una licenza?

A1: Sì, puoi provare Aspose.HTML per .NET con una versione di prova gratuita, ma alcune funzionalità avanzate potrebbero richiedere una licenza valida.

### Q2: Come posso ottenere una licenza per Aspose.HTML per .NET?

 A2: È possibile acquistare una licenza dal sito Web Aspose:[Acquista la licenza Aspose.HTML](https://purchase.aspose.com/buy).

### Q3: In quali formati posso convertire i documenti HTML utilizzando Aspose.HTML per .NET?

A3: Aspose.HTML per .NET supporta la conversione in vari formati, inclusi PDF, immagini e altro.

### Q4: esiste una community o un forum di supporto per Aspose.HTML per .NET?

 R4: Sì, puoi trovare aiuto e supporto sui forum Aspose:[Forum di supporto Aspose.HTML](https://forum.aspose.com/).

### Q5: Aspose.HTML per .NET fornisce documentazione ed esercitazioni?

 R5: Sì, puoi accedere alla documentazione qui:[Aspose.HTML per la documentazione .NET](https://reference.aspose.com/html/net/).