---
category: general
date: 2026-10-21
description: Scopri come salvare HTML come ZIP usando Aspose.HTML, convertire HTML
  in ZIP e rimuovere le risorse per un pacchetto pulito.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save html as zip
- convert html to zip
- how to omit resources
- how to strip resources
- create html zip
language: it
lastmod: 2026-10-21
og_description: Salva HTML come ZIP con Aspose.HTML, scopri come convertire HTML in
  ZIP e rimuovere le risorse per un archivio leggero.
og_image_alt: Screenshot showing the save html as zip process with resources omitted
og_title: Salva HTML come ZIP con Aspose.HTML – ometti le risorse in un solo passaggio
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to save HTML as ZIP using Aspose.HTML, convert HTML to ZIP,
    and strip resources for a clean package.
  headline: How to save HTML as ZIP with Aspose.HTML and omit resources
  type: TechArticle
tags:
- Aspose.HTML
- C#
- ZIP archive
- HTML conversion
- Resource handling
title: Come salvare HTML come ZIP con Aspose.HTML e omettere le risorse
url: /it/net/html-extensions-and-conversions/how-to-save-html-as-zip-with-aspose-html-and-omit-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come salvare HTML come ZIP con Aspose.HTML e omettere le risorse

Se hai bisogno di **salvare HTML come ZIP** rimuovendo i file esterni, questa guida mostra una soluzione completa, pronta all'uso. Alla fine del tutorial sarai in grado di **convertire HTML in ZIP**, controllare quali risorse vengono mantenute e produrre un archivio pulito che contiene solo il markup di base.

Molti scenari di automazione web richiedono di impacchettare una pagina per uso offline, allegato email o archiviazione. Includere immagini, font o script spesso gonfia l'archivio inutilmente. I passaggi seguenti spiegano **come omettere le risorse** e **come rimuovere le risorse** dall'output, così il ZIP risultante rimane leggero.

## Prerequisiti

- .NET 6.0 o versioni successive installato  
- Una licenza Aspose.HTML per .NET (o una valutazione gratuita)  
- Un ambiente di sviluppo C# di base (Visual Studio, VS Code o Rider)

Non sono necessari pacchetti NuGet aggiuntivi oltre a `Aspose.Html`.

## Passo 1: Creare un gestore di risorse personalizzato

Il cuore di **come omettere le risorse** risiede in una sottoclasse di `ResourceHandler`. Aspose.HTML chiama questo gestore per ogni risorsa esterna (immagini, CSS, script). Restituendo uno stream vuoto, si indica al convertitore di ignorare la risorsa.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

/// <summary>
/// Prevents external resources from being written to the output package.
/// </summary>
class CustomResourceHandler : ResourceHandler
{
    public override Stream HandleResource(ResourceInfo info)
    {
        // Returning an empty MemoryStream strips the resource from the ZIP.
        return new MemoryStream();
    }
}
```

**Perché è importante:** Il comportamento predefinito copia ogni file collegato nel ZIP, il che può raddoppiare o triplicare la dimensione del file. Sovrascrivere `HandleResource` ti offre un controllo fine senza modificare l'HTML originale.

## Passo 2: Caricare il documento HTML

Carica il file sorgente con `HTMLDocument`. Il costruttore accetta un percorso file, un URL o uno stream. In questo esempio leggiamo un file locale chiamato `input.html`.

```csharp
// Load the source HTML file from the local file system.
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

Se il tuo HTML risiede in memoria o proviene da una richiesta web, puoi passare invece un `MemoryStream` o una stringa URL. L'API funziona allo stesso modo.

## Passo 3: Configurare le opzioni di salvataggio

Crea un'istanza di `HtmlSaveOptions` e assegna il gestore personalizzato creato nel Passo 1. Questo indica ad Aspose.HTML di utilizzare il gestore ogni volta che incontra una risorsa.

```csharp
// Prepare save options and attach the custom resource handler.
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // The ResourceHandler property is what enables resource stripping.
    ResourceHandler = new CustomResourceHandler()
};
```

Puoi anche regolare altre opzioni qui, come `CompressImages = false` se desideri mantenere i dati delle immagini ma comunque omettere le altre risorse. L'esempio mantiene le impostazioni di compressione predefinite.

## Passo 4: Salvare il documento come archivio ZIP

Infine, invoca `Save` con il percorso di destinazione e le opzioni configurate. Il file di output sarà un `.zip` che contiene `index.html` (o il nome file originale) e **nessuna risorsa esterna**.

```csharp
// Save the HTML document as a ZIP file. The archive will contain only the HTML markup.
document.Save("YOUR_DIRECTORY/output.zip", saveOptions);
```

### Risultato atteso

- `output.zip` → contiene un unico file `index.html`.  
- Tutte le immagini, i file CSS e i riferimenti JavaScript sono omessi, perché il gestore personalizzato ha restituito uno stream vuoto per ciascuno.

Puoi verificare l'archivio aprendolo con qualsiasi visualizzatore ZIP. La pagina HTML continuerà a fare riferimento agli URL originali, ma quei file non sono presenti nell'archivio, mantenendo il pacchetto minimale.

## Esempio completo, eseguibile

Di seguito trovi il programma completo che puoi copiare, incollare ed eseguire. Sostituisci `YOUR_DIRECTORY` con un percorso di cartella reale sul tuo computer.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Converters;

class Program
{
    static void Main()
    {
        // Step 1: Define a custom resource handler to control how external resources are saved.
        class CustomResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // Returning an empty stream strips the resource from the ZIP output.
                return new MemoryStream();
            }
        }

        // Step 2: Load an HTML document from a file.
        string inputPath = "YOUR_DIRECTORY/input.html";
        HTMLDocument document = new HTMLDocument(inputPath);

        // Step 3: Create HTML save options and assign the custom handler.
        HtmlSaveOptions saveOptions = new HtmlSaveOptions
        {
            ResourceHandler = new CustomResourceHandler()
        };

        // Step 4: Save the document as a ZIP archive containing the HTML and (now omitted) resources.
        string outputPath = "YOUR_DIRECTORY/output.zip";
        document.Save(outputPath, saveOptions);

        Console.WriteLine($"HTML has been saved as ZIP at: {outputPath}");
    }
}
```

Eseguendo questo programma si genera il file ZIP descritto in precedenza. Ora puoi distribuire la pagina HTML senza includere risorse inutili.

## Variazioni comuni e casi limite

| Scenario | Adjustment |
|----------|------------|
| **Mantieni le immagini ma elimina CSS/JS** | In `CustomResourceHandler`, ispeziona `info.MimeType`. Restituisci un `MemoryStream` solo per `text/css` e `application/javascript`. |
| **Preserva i font esterni** | Restituisci lo stream originale per i tipi MIME `font/woff2`, altrimenti restituisci uno stream vuoto. |
| **Genera un ZIP con un nome di entry personalizzato** | Usa il sovraccarico di `HtmlSaveOptions` `Save(string path, SaveOptions options, string entryName)` per specificare un nome file radice diverso. |
| **Converti più file HTML in un unico ZIP** | Itera su ogni file, crea un `HTMLDocument` separato e aggiungi ciascuno allo stesso `ZipArchive` manualmente usando `System.IO.Compression`. |

Queste variazioni illustrano **come rimuovere le risorse** in modo selettivo, offrendoti il pieno controllo sulla dimensione finale dell'archivio.

## Consigli professionali

- **Convalida il risultato**: Dopo il salvataggio, apri il ZIP e carica `index.html` in un browser. Le risorse mancanti appariranno come link interrotti, confermando che il gestore ha funzionato.  
- **Prestazioni**: Restituire un `MemoryStream` vuoto è poco costoso, ma se hai migliaia di risorse, considera di memorizzare nella cache la decisione (ad es., un `HashSet<string>` di tipi MIME da saltare).  
- **Licenza**: La versione di valutazione gratuita di Aspose.HTML aggiunge un commento watermark all'interno dell'HTML. Distribuisci una versione con licenza per rimuoverlo in produzione.

## Conclusione

Ora sai come **salvare HTML come ZIP**, **convertire HTML in ZIP** e **rimuovere le risorse** usando Aspose.HTML per .NET. Implementando un `ResourceHandler` personalizzato, puoi omettere i file indesiderati e mantenere l'archivio leggero. Sperimenta con la logica del gestore per conservare solo le risorse di cui hai realmente bisogno e integra questo modello in pipeline di automazione più ampie.

---

**Passi successivi**

- Esplora altre funzionalità di `HtmlSaveOptions` come `EmbedImages` per incorporare le immagini direttamente nell'HTML.  
- Combina questo approccio con `Aspose.PDF` per convertire lo stesso HTML in PDF dopo aver creato il ZIP.  
- Esamina scenari lato server in cui generi il ZIP su richiesta e lo trasmetti a un client senza scriverlo su disco.  

Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come usare ZipArchive – Salva HTML e risorse in un file ZIP](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [Come salvare HTML in C# – Gestori di risorse personalizzati e ZIP](/html/english/net/working-with-html-documents/how-to-save-html-in-c-custom-resource-handlers-zip/)
- [Come salvare HTML come ZIP in C# – Guida completa Aspose.HTML](/html/english/net/html-extensions-and-conversions/how-to-save-html-as-zip-in-c-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}