---
category: general
date: 2026-03-25
description: Scopri come disabilitare l'anti‑aliasing durante la conversione da HTML
  a PNG, garantendo un rendering pixel‑perfect. Include i passaggi per rendere l'HTML
  come immagine, salvare l'HTML come PNG e creare PNG dall'HTML.
draft: false
keywords:
- how to disable antialiasing
- convert html to png
- render html as image
- save html as png
- create png from html
language: it
og_description: Scopri il metodo passo‑passo per disabilitare l'antialiasing durante
  la conversione da HTML a PNG, garantendoti un output immagine pixel‑perfetto ogni
  volta.
og_title: Come disabilitare l'antialiasing nella conversione da HTML a PNG
tags:
- Aspose.HTML
- C#
- Image Rendering
title: Come disabilitare l'antialiasing durante la conversione da HTML a PNG
url: /it/net/generate-jpg-and-png-images/how-to-disable-antialiasing-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come disabilitare l'anti-aliasing durante la conversione da HTML a PNG

Ti sei mai chiesto **come disabilitare l'anti-aliasing** in modo che la tua conversione da HTML‑to‑PNG abbia esattamente l'aspetto del markup originale? Forse stai creando un generatore di miniature per componenti UI e i bordi sfocati compromettono la fedeltà visiva. Non sei solo: molti sviluppatori incontrano questo ostacolo quando cercano di **convertire HTML in PNG** per screenshot pixel‑perfect.

In questo tutorial percorreremo l'intero processo di **rendering di HTML come immagine**, modificando la pipeline di rendering per disattivare l'anti-aliasing, e infine **salvare HTML come PNG** usando Aspose.HTML per .NET. Alla fine avrai uno snippet pronto all'uso che crea un PNG nitido da qualsiasi file HTML, e comprenderai perché disabilitare l'anti-aliasing è importante in alcuni scenari sensibili al design.

## Cosa ti serve

- **.NET 6.0** o versioni successive (il codice funziona anche su .NET Framework 4.6+).  
- Pacchetto NuGet **Aspose.HTML for .NET** (`Aspose.HTML`).  
- Un semplice file `input.html` che desideri rasterizzare.  
- Qualsiasi IDE ti piaccia—Visual Studio, Rider, o anche VS Code con l'estensione C#.

Non sono necessarie librerie native aggiuntive o strumenti esterni; Aspose.HTML gestisce tutto internamente.

## Passo 1: Installa Aspose.HTML

La prima cosa di cui hai bisogno è la libreria Aspose.HTML. Apri il terminale (o la Package Manager Console) ed esegui:

```bash
dotnet add package Aspose.HTML
```

Oppure, se preferisci l'interfaccia UI di NuGet, cerca **Aspose.HTML** e fai clic su *Install*. Questo pacchetto include un potente motore di rendering in grado di generare PNG, JPEG, BMP e altro.

> **Suggerimento professionale:** Usa l'ultima versione stabile (a partire da marzo 2026 è la 23.12) per beneficiare delle correzioni di bug relative al rendering delle immagini e al controllo dell'anti-aliasing.

## Passo 2: Carica il documento HTML

Una volta installato il pacchetto, puoi caricare l'HTML che desideri trasformare. La classe `HTMLDocument` astrae il DOM e ti consente di manipolarlo prima del rendering, se necessario.

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Image;

// Path to your source HTML file
string inputPath = Path.Combine(Environment.CurrentDirectory, "input.html");

// Create a new HTMLDocument instance
HTMLDocument htmlDoc = new HTMLDocument(inputPath);
```

> **Perché è importante:** Caricare prima il documento ti dà la possibilità di iniettare CSS o correggere URL relativi prima della fase di rasterizzazione. Inoltre isola il rendering dal file system, rendendo il codice più facile da testare.

## Passo 3: Configura ImageSaveOptions e disattiva l'anti-aliasing

Ecco il nocciolo del tutorial: disabilitare l'anti-aliasing. Aspose.HTML espone `ImageRenderingOptions` dove è possibile attivare/disattivare `UseAntialiasing`. Impostandolo su `false` il motore renderizza ogni pixel esattamente come definito dalle forme vettoriali, producendo un **PNG pixel‑perfect**.

```csharp
// Create ImageSaveOptions for PNG output
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.Png)
{
    // Attach rendering options
    ImageRenderingOptions = new ImageRenderingOptions
    {
        // Disable antialiasing for a crisp raster image
        UseAntialiasing = false
    }
};
```

### Cosa fa realmente l'anti-aliasing

L'anti-aliasing leviga i bordi delle forme mescolando i colori dei pixel vicini. Sebbene sia ottimo per fotografie o grafiche complesse, può sfocare elementi UI nitidi (pensa a icone o testo a piccole dimensioni). Disabilitarlo garantisce che ogni linea rimanga affilata come un rasoio—esattamente ciò di cui hai bisogno quando **crei PNG da HTML** per test UI o documentazione.

## Passo 4: Renderizza e salva il PNG

Ora che le opzioni sono impostate, chiama `Save` sul `HTMLDocument`. Il metodo accetta il percorso di output e le `ImageSaveOptions` precedentemente configurate.

```csharp
// Destination path for the PNG file
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.png");

// Render the HTML and write the PNG file
htmlDoc.Save(outputPath, saveOptions);
```

Eseguendo il codice sopra verrà generato `output.png` accanto al tuo eseguibile. Aprilo con qualsiasi visualizzatore di immagini—dovresti vedere una resa nitida, senza anti-aliasing, di `input.html`.

### Risultato atteso

| Prima (Anti-aliasing attivo) | Dopo (Anti-aliasing disattivato) |
|--------------------------|--------------------------|
| ![Output con anti-aliasing](antialiased.png "come disabilitare l'anti-aliasing esempio con bordi sfocati") | ![Output pixel‑perfect](pixelperfect.png "come disabilitare l'anti-aliasing esempio con bordi nitidi") |

*L'immagine a sinistra mostra il rendering predefinito con anti-aliasing, mentre l'immagine a destra dimostra il risultato nitido dopo aver disabilitato l'anti-aliasing.*

> **Nota:** Gli screenshot sopra sono segnaposto; sostituiscili con i tuoi file quando pubblichi.

## Passo 5: Verifica l'output programmaticamente (opzionale)

Se hai bisogno di garantire che il PNG soddisfi determinati criteri (ad esempio dimensioni esatte o profondità di colore), puoi ispezionarlo usando `System.Drawing` o `SixLabors.ImageSharp`. Ecco un rapido controllo con `ImageSharp`:

```csharp
using SixLabors.ImageSharp;
using SixLabors.ImageSharp.PixelFormats;

using (Image<Rgba32> img = Image.Load<Rgba32>(outputPath))
{
    Console.WriteLine($"Width: {img.Width}px, Height: {img.Height}px");
    // Verify that the image has no blended pixels (simple heuristic)
    // You could compare a few pixel values against expected RGBA values.
}
```

Questo passaggio aggiuntivo è utile quando automatizzi la generazione di PNG in una pipeline CI e devi garantire la coerenza.

## Casi limite e domande frequenti

### E se il mio HTML utilizza risorse esterne?

Se l'HTML fa riferimento a CSS, font o immagini tramite URL relativi, assicurati che l'URL base di `HTMLDocument` punti alla cartella contenente tali risorse:

```csharp
HTMLDocument htmlDoc = new HTMLDocument(inputPath, new Uri("file:///" + Path.GetDirectoryName(inputPath) + "/"));
```

### Posso modificare DPI o dimensione dell'immagine?

Assolutamente. `ImageRenderingOptions` ti permette anche di impostare `Resolution` (punti per pollice) e `Width`/`Height`:

```csharp
saveOptions.ImageRenderingOptions.Resolution = 300; // High‑resolution PNG
saveOptions.ImageRenderingOptions.Width = 800;      // Desired pixel width
saveOptions.ImageRenderingOptions.Height = 600;     // Desired pixel height
```

Ricorda solo che aumentare il DPI senza scalare il viewport può produrre un file più grande con la stessa dimensione visiva.

### Disabilitare l'anti-aliasing influisce sulla leggibilità del testo?

Per la maggior parte dei font moderni, disattivare l'anti-aliasing può rendere il testo piccolo irregolare. Se hai bisogno di testo nitido **e** bordi lisci, considera di renderizzare a una risoluzione più alta e poi ridimensionare con un algoritmo di ricampionamento di alta qualità. Questo trucco preserva la leggibilità mantenendo il controllo sulla griglia finale dei pixel.

### Questo approccio è cross‑platform?

Sì. Aspose.HTML è puro .NET e funziona su Windows, Linux e macOS. L'unica sfumatura specifica della piattaforma è la disponibilità dei font di sistema; potresti dover incorporare font personalizzati nel tuo HTML o installarli sulla macchina di destinazione.

## Esempio completo funzionante

Di seguito trovi il programma completo e autonomo che puoi copiare e incollare in un'applicazione console. Include tutte le istruzioni `using` necessarie, la gestione degli errori e i commenti.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Rendering.Image;

namespace HtmlToPngDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // -------------------------------------------------
                // 1️⃣ Define input and output paths
                // -------------------------------------------------
                string inputHtml = Path.Combine(Environment.CurrentDirectory, "input.html");
                string outputPng = Path.Combine(Environment.CurrentDirectory, "output.png");

                // -------------------------------------------------
                // 2️⃣ Load the HTML document
                // -------------------------------------------------
                // BaseUri ensures relative resources resolve correctly
                var htmlDoc = new HTMLDocument(inputHtml, new Uri("file:///" + Path.GetDirectoryName(inputHtml) + "/"));

                // -------------------------------------------------
                // 3️⃣ Configure rendering options – disable antialiasing
                // -------------------------------------------------
                var saveOptions = new ImageSaveOptions(SaveFormat.Png)
                {
                    ImageRenderingOptions = new ImageRenderingOptions
                    {
                        UseAntialiasing = false,   // 👈 The key line for pixel‑perfect output
                        // Optional: set resolution or size here
                    }
                };

                // -------------------------------------------------
                // 4️⃣ Render and save the PNG
                // -------------------------------------------------
                htmlDoc.Save(outputPng, saveOptions);
                Console.WriteLine($"✅ PNG created at: {outputPng}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
            }
        }
    }
}
```

Esegui il programma e vedrai apparire **output.png** accanto all'eseguibile. Aprilo—nessun bordo sfocato, solo una copia raster pura del tuo HTML.

## Conclusione

Abbiamo coperto **come disabilitare l'anti-aliasing** quando **converti HTML in PNG**, esaminato ogni passaggio di configurazione e fornito un esempio completo e eseguibile che **renderizza HTML come immagine**, **salva HTML come PNG**, e ti permette di **creare PNG da HTML** con fedeltà pixel‑perfect.

Se vuoi andare oltre, prova a sperimentare con diversi formati immagine (JPEG, BMP), esplora trucchi di scaling vettore‑a‑raster, o integra questo snippet in un servizio web che genera miniature al volo. Gli stessi principi valgono sia che tu stia costruendo un generatore di documentazione, uno strumento di test di regressione visiva o un esportatore di grafici dinamici.

Hai altre domande su curiosità del rendering o sulle funzionalità di Aspose.HTML? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}