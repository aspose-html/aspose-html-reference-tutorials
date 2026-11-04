---
category: general
date: 2026-08-15
description: Crea un gestore di risorse personalizzato in C# per gestire le risorse
  HTML come immagini e CSS. Impara HTMLLoadOptions, stream di memoria e caricamento
  di HTMLDocument.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: it
lastmod: 2026-08-15
og_description: Crea un gestore di risorse personalizzato in C# per controllare come
  le risorse HTML vengono trasmesse. Questo tutorial mostra la configurazione di HTMLLoadOptions,
  la gestione dello stream di memoria e il caricamento di HTMLDocument con logica
  personalizzata.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Crea gestore di risorse personalizzato in C# – guida completa per la gestione
  delle risorse HTML
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Crea gestore di risorse personalizzato in C# per il caricamento HTML
url: /it/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea gestore di risorse personalizzato in C# per il caricamento HTML

Se hai bisogno di **create custom resource handler** per file HTML, questa guida ti mostra esattamente come fare. Imparerai a intercettare immagini, CSS e altre risorse durante il caricamento di un documento HTML, usando `HTMLLoadOptions` e uno stream basato su memoria.

Il tutorial copre tutto il necessario per implementare un gestore riutilizzabile, configurare le opzioni di caricamento e verificare che le risorse siano catturate correttamente. Non è necessaria alcuna documentazione esterna—basta il codice qui sotto e le spiegazioni.

## Prerequisiti

- .NET 6.0 o versioni successive
- Familiarità di base con C#
- Un riferimento alla libreria di elaborazione HTML che fornisce `HTMLDocument`, `HtmlLoadOptions` e `ResourceHandler` (ad esempio, GroupDocs.Viewer per .NET)

## Panoramica della soluzione

Procederemo:

1. **Create a custom resource handler** creando una sottoclasse di `ResourceHandler`.
2. Configurare `HTMLLoadOptions` per utilizzare il gestore.
3. Caricare un file HTML con `HTMLDocument` mentre il gestore fornisce uno stream per ogni risorsa.
4. (Opzionale) Salvare le risorse ricevute su disco per la verifica.

Ogni passaggio include il codice sorgente completo e la motivazione dietro di esso.

## Passo 1: Definisci la classe del gestore di risorse personalizzato

Creare un gestore personalizzato significa sovrascrivere `HandleResource` in modo che la libreria possa scrivere i byte della risorsa su uno stream controllato da te. L'uso di un `MemoryStream` mantiene i dati in memoria, ideale per test o ulteriori elaborazioni.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Perché è importante:**  
Sovrascrivere `HandleResource` ti dà il controllo completo su dove vanno i dati della risorsa. Se in seguito dovessi memorizzare nella cache le immagini, trasformare il CSS o registrare l'uso delle risorse, puoi sostituire il `MemoryStream` con qualsiasi implementazione di stream personalizzata.

## Passo 2: Configura `HTMLLoadOptions` per utilizzare il gestore

`HTMLLoadOptions` ti consente di inserire il gestore nella pipeline di caricamento. Impostare la proprietà `ResourceHandler` indica al visualizzatore di invocare `MyHandler` per ogni risorsa esterna.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Perché è importante:**  
Senza assegnare `ResourceHandler`, il visualizzatore scriverebbe le risorse nella sua posizione predefinita (spesso una cartella temporanea). Specificando il tuo gestore, crei un comportamento di **create custom resource handler** che si allinea alla strategia di archiviazione della tua applicazione.

## Passo 3: Carica il documento HTML con le opzioni configurate

Ora carica il file HTML. Il visualizzatore chiamerà `MyHandler.HandleResource` per ogni risorsa che incontra.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

A questo punto il contenuto HTML è stato analizzato e tutte le risorse esterne sono state inviate nei buffer di memoria forniti da `MyHandler`.

## Passo 4 (opzionale): Accedi alle risorse catturate

Se hai bisogno di ispezionare o conservare le risorse, puoi modificare `MyHandler` per memorizzare ogni `MemoryStream` in un dizionario indicizzato dal nome della risorsa.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Dopo il caricamento, puoi iterare su `handler.Resources` e scrivere ciascuna su disco:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Perché è importante:**  
Memorizzare le risorse consente post‑processing come l'ottimizzazione delle immagini, la minificazione del CSS o l'archiviazione. Fornisce anche una verifica tangibile che la logica di **create custom resource handler** funzioni come previsto.

## Passo 5: Pulizia

Sia `HTMLDocument` che eventuali stream devono essere eliminati per liberare risorse non gestite.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Esempio completo eseguibile

Di seguito è riportato un programma autonomo che dimostra tutti i passaggi, dalla definizione della classe all'estrazione delle risorse.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Output previsto**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

La console elenca ogni risorsa che il visualizzatore ha inviato attraverso il tuo gestore personalizzato, confermando che il flusso di lavoro **create custom resource handler** è riuscito.

## Domande comuni e casi limite

| Domanda | Risposta |
|----------|--------|
| *Che succede se una risorsa è grande (ad esempio, immagine ad alta risoluzione)?* | Sostituire `MemoryStream` con un `FileStream` che punta a una cartella temporanea. Questo evita un consumo eccessivo di memoria. |
| *Posso filtrare le risorse per tipo?* | All'interno di `HandleResource`, ispeziona `info.MimeType` o `info.Extension` e restituisci `null` per i tipi indesiderati. Restituire `null` indica al visualizzatore di saltare la risorsa. |
| *È necessaria la sicurezza dei thread?* | Se la stessa istanza del gestore viene utilizzata in più caricamenti concorrenti, proteggi il dizionario `Resources` con un lock o usa una collezione concorrente. |
| *Come gestire URL relativi?* | `ResourceInfo` contiene l'URL originale; puoi combinarlo con il percorso base del file HTML per risolvere i riferimenti relativi prima di memorizzarli. |

## Conclusione

Ora sai come **create custom resource handler** in C# per il caricamento HTML, configurare `HTMLLoadOptions`, catturare le risorse trasmesse e pulire in modo responsabile. Questo modello ti offre il controllo completo sulla gestione delle risorse, consentendo scenari come l'elaborazione di immagini al volo, la riscrittura del CSS o l'archiviazione sicura.

Successivamente, esplora argomenti correlati come il **HTMLDocument loading** con diverse opzioni di rendering, o estendi il gestore a implementazioni di **C# resource handler** che scrivono direttamente su storage cloud. Sperimenta con il metodo `HandleResource` del gestore per adattarlo al flusso di lavoro delle risorse specifico del tuo progetto.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea HTML da stringa in C# – Guida al gestore di risorse personalizzato](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Gestore di risorse personalizzato in C# – Tutorial per convertire HTML in ZIP](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [Come salvare HTML in C# – Guida completa usando un gestore di risorse personalizzato](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}