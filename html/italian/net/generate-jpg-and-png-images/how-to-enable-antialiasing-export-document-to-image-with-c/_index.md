---
category: general
date: 2026-04-06
description: Scopri come abilitare l'antialiasing, impostare larghezza e altezza dell'immagine
  e salvare il documento come PNG in C# – una guida rapida per esportare il documento
  in immagine.
draft: false
keywords:
- how to enable antialiasing
- save document as png
- set image width
- set image height
- export document to image
language: it
og_description: Come abilitare l'antialiasing quando esporti un documento in un'immagine.
  Questa guida ti mostra come impostare la larghezza dell'immagine, impostare l'altezza
  dell'immagine e salvare il documento come PNG.
og_title: Come abilitare l'antialiasing – Esporta il documento in immagine
tags:
- C#
- ImageRendering
- Antialiasing
title: Come abilitare l'antialiasing – Esportare il documento in immagine con C#
url: /it/net/generate-jpg-and-png-images/how-to-enable-antialiasing-export-document-to-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare l'anti-aliasing – Esportare un documento in immagine in C#

Ti sei mai chiesto **come abilitare l'anti-aliasing** mentre trasformi un documento in un'immagine? Forse hai provato una rapida chiamata `Save` e il risultato è apparso frastagliato, soprattutto sulle linee diagonali. La buona notizia è che non serve essere un mago della grafica—bastano poche righe di C# e le opzioni corrette.

In questo tutorial vedremo come impostare la larghezza dell'immagine, l'altezza dell'immagine e, infine, **salvare il documento come PNG** così potrai **esportare il documento in immagine** con bordi morbidi. Alla fine avrai uno snippet pronto all'uso che produce un PNG nitido 800 × 600 con l'anti-aliasing attivato.

## Prerequisiti

- .NET 6.0 o versioni successive (il codice funziona anche su .NET Framework 4.7+)  
- Un riferimento a una libreria di rendering che supporti `ImageRenderingOptions` (ad es., Aspose.Words, Syncfusion o qualsiasi API che esponga proprietà simili)  
- Una conoscenza di base della sintassi C#  

Nessuna configurazione complessa—basta aggiungere il pacchetto NuGet e sei pronto.

## Passo 1: Installa la libreria di rendering

Per prima cosa, aggiungi il pacchetto al tuo progetto. Se usi Aspose.Words, esegui:

```bash
dotnet add package Aspose.Words
```

> **Suggerimento:** Mantieni la versione della libreria aggiornata; l'ultima release (a partire da aprile 2026) aggiunge ottimizzazioni di prestazioni per l'anti-aliasing.

## Passo 2: Crea l'oggetto Document

Carica o crea il documento che desideri renderizzare. Ecco un esempio minimale che costruisce un documento di una pagina con un semplice paragrafo:

```csharp
using Aspose.Words;
using Aspose.Words.Rendering;

// Create a new blank document
Document doc = new Document();

// Add a paragraph with some text
Paragraph para = new Paragraph(doc);
Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
para.AppendChild(run);
doc.FirstSection.Body.AppendChild(para);
```

La classe `Document` è il punto di ingresso; tutto ciò che renderizzi proviene da essa. Nei progetti reali probabilmente caricherai un file .docx esistente:

```csharp
// Document doc = new Document("input.docx");
```

## Passo 3: Definisci le opzioni di rendering (larghezza, altezza, anti-aliasing)

Ora rispondiamo alla domanda principale: **come abilitare l'anti-aliasing**. L'oggetto `ImageRenderingOptions` ti permette di attivare la levigatura e controllare le dimensioni.

```csharp
// Step 3: Define rendering options (size and antialiasing)
ImageRenderingOptions imageOptions = new ImageRenderingOptions
{
    // Set the desired output size
    Width = 800,               // set image width
    Height = 600,              // set image height

    // Turn on antialiasing for smoother edges
    UseAntialiasing = true
};
```

Nota i commenti: menzionano esplicitamente **set image width**, **set image height** e **UseAntialiasing**—i tre parametri che contano di più quando vuoi un PNG curato.

### Perché l'anti-aliasing è importante

Senza anti-aliasing, le linee diagonali e le curve appaiono a gradini perché il renderer tratta ogni pixel come acceso o spento. Attivandolo, i pixel di bordo vengono mescolati, producendo un'attenuazione visiva che imita ciò che vedi in un editor fotografico. Il compromesso è un leggero aumento del tempo di elaborazione, ma per la maggior parte delle esportazioni orientate all'interfaccia utente è trascurabile.

## Passo 4: Salva il documento come PNG (esporta il documento in immagine)

Con le opzioni pronte, finalmente **salviamo il documento come PNG**. Il metodo `Save` accetta il percorso del file e le opzioni appena configurate.

```csharp
// Step 4: Render the document to a PNG file using the configured options
doc.Save("output.png", imageOptions);
```

Fatto—il tuo documento è ora un PNG 800 × 600 con anti-aliasing applicato. Se apri `output.png` vedrai testo pulito, linee morbide e nessun artefatto frastagliato.

### Verifica del risultato

Puoi controllare rapidamente il file in qualsiasi visualizzatore di immagini. Cerca:

- Dimensioni corrette (800 × 600)  
- Nessun bordo a gradini visibile sul testo o su eventuali forme  
- Uno sfondo trasparente se il documento non conteneva un colore di sfondo (la maggior parte delle librerie usa il bianco come predefinito)

Se l'immagine appare frastagliata, ricontrolla che `UseAntialiasing = true` non sia stato sovrascritto altrove.

## Passo 5: Casi particolari e varianti

### Cambiare il formato di output

Vuoi un JPEG invece di PNG? Cambia semplicemente l'estensione del file e, opzionalmente, regola la compressione:

```csharp
imageOptions.JpegQuality = 90; // only works for JPEG output
doc.Save("output.jpg", imageOptions);
```

### Esportare più pagine

Quando il documento di origine ha diverse pagine, il renderer crea file immagine separati per pagina per impostazione predefinita. Puoi iterare sulle pagine:

```csharp
for (int i = 0; i < doc.PageCount; i++)
{
    string fileName = $"page_{i + 1}.png";
    doc.Save(fileName, imageOptions);
}
```

### Salvare su uno stream (ad es., risposta HTTP)

Se stai costruendo un'API web, potresti voler restituire direttamente il PNG:

```csharp
using (MemoryStream ms = new MemoryStream())
{
    doc.Save(ms, imageOptions);
    ms.Position = 0;
    // Return ms as FileResult in ASP.NET Core
}
```

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per il copia‑incolla, che incorpora tutti i passaggi discussi:

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Rendering;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a document
        Document doc = new Document();
        Paragraph para = new Paragraph(doc);
        Run run = new Run(doc, "Hello, world! This text will be rendered as an image.");
        para.AppendChild(run);
        doc.FirstSection.Body.AppendChild(para);

        // 2️⃣ Define rendering options (size and antialiasing)
        ImageRenderingOptions imageOptions = new ImageRenderingOptions
        {
            Width = 800,               // set image width
            Height = 600,              // set image height
            UseAntialiasing = true     // how to enable antialiasing
        };

        // 3️⃣ Export document to image (save document as PNG)
        doc.Save("output.png", imageOptions);

        Console.WriteLine("Image saved as output.png with antialiasing enabled.");
    }
}
```

Eseguendo questo programma otterrai `output.png` nella cartella dell'eseguibile. Aprilo e vedrai un PNG morbido 800 × 600—esattamente ciò che ci eravamo prefissati.

## Domande frequenti e risoluzione problemi

- **E se l'immagine appare sfocata?**  
  La sfocatura può verificarsi quando ingrandisci una pagina di origine piccola. Mantieni la dimensione della pagina di origine vicina a quella target, oppure aumenta la DPI tramite `imageOptions.Resolution` (ad es., `Resolution = 300`).

- **Funziona su .NET Framework?**  
  Sì. La stessa API è disponibile nel framework classico; basta referenziare il DLL appropriato.

- **Posso controllare il colore di sfondo?**  
  Assolutamente. Imposta `imageOptions.BackgroundColor = System.Drawing.Color.Transparent;` prima di salvare.

- **L'anti-aliasing è accelerato dall'hardware?**  
  La maggior parte delle librerie esegue l'anti-aliasing in software. Se ti serve l'accelerazione GPU, cerca un motore di rendering che lo supporti esplicitamente.

## Conclusione

Abbiamo coperto **come abilitare l'anti-aliasing** quando **esporti un documento in immagine**, illustrato **set image width** e **set image height**, e mostrato i passaggi esatti per **salvare il documento come PNG**. Lo snippet sopra è pronto per la produzione e ora puoi adattarlo a JPEG, PDF multi‑pagina o persino trasmettere l'immagine direttamente a un client.

Successivamente potresti esplorare l'aggiunta di filigrane, la regolazione della DPI per output di stampa di alta qualità, o l'integrazione di questa logica in un endpoint ASP.NET Core. Gli stessi principi valgono—basta sostituire il percorso del file con uno stream di risposta.

Buona programmazione e goditi quelle immagini nitide e anti‑aliased! 

![Rendered PNG with antialiasing enabled](output.png "PNG renderizzato con anti-aliasing abilitato")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}