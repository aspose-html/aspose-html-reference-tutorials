---
category: general
date: 2026-09-10
description: Scopri come utilizzare HtmlSaveOptions in C# per controllare gli stili
  dei web‑font e salvare file HTML con Aspose.HTML. Include un esempio di codice completo
  e consigli pratici.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use htmlsaveoptions
- Aspose HTML library
- WebFontStyle flags
- HTMLDocument conversion
- C# save HTML
- Aspose.Html SaveOptions
language: it
lastmod: 2026-09-10
og_description: Come utilizzare HtmlSaveOptions in C# per abilitare gli stili di carattere
  web in grassetto e corsivo durante il salvataggio di HTML con Aspose.HTML. Segui
  l'esempio completo e i consigli delle migliori pratiche.
og_image_alt: Screenshot showing how to use HtmlSaveOptions to save an HTML file in
  C#
og_title: Come utilizzare HtmlSaveOptions in C# con Aspose.HTML – guida passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  headline: How to use HtmlSaveOptions in C# with Aspose.HTML
  type: TechArticle
- description: Learn how to use HtmlSaveOptions in C# to control web‑font styles and
    save HTML files with Aspose.HTML. Full code example and practical tips included.
  name: How to use HtmlSaveOptions in C# with Aspose.HTML
  steps:
  - name: Why configure WebFontStyle?
    text: 'When you export an HTML document, Aspose.HTML can embed web fonts that
      match the original styling. By setting `WebFontStyle`, you tell the exporter
      which font variants to include. This reduces the final file size when you only
      need specific styles and guarantees that the rendered output matches the '
  - name: 5.1 Controlling CSS embedding
    text: 'You can decide whether to embed CSS inline, keep external links, or embed
      everything:'
  - name: 5.2 Saving to a specific encoding
    text: '```csharp saveOptions.Encoding = Encoding.UTF8; ```'
  - name: 5.3 Handling large documents
    text: 'For very large HTML files, consider streaming the output to avoid high
      memory consumption:'
  - name: 5.4 Error handling best practice
    text: 'Wrap the entire workflow in a try‑catch block and log the exception details.
      This ensures that any I/O or parsing errors are captured:'
  - name: Expected console output
    text: '``` HTML saved successfully to ''YOUR_DIRECTORY/output.html''. ```'
  type: HowTo
tags:
- Aspose.HTML
- C#
- HTML processing
title: Come utilizzare HtmlSaveOptions in C# con Aspose.HTML
url: /it/net/working-with-html-documents/how-to-use-htmlsaveoptions-in-c-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare HtmlSaveOptions in C# con Aspose.HTML

Se hai bisogno di controllare come Aspose.HTML salva un documento HTML, **imparare a usare HtmlSaveOptions è fondamentale**. Questo tutorial ti mostra passo‑passo come utilizzare HtmlSaveOptions per abilitare gli stili di web‑font in grassetto e corsivo durante il salvataggio di un documento.

La libreria Aspose HTML fornisce un'API ricca per caricare, manipolare ed esportare contenuti HTML. Alla fine di questa guida sarai in grado di:

* Caricare un file HTML esistente in un `HTMLDocument`.
* Configurare `HtmlSaveOptions` per applicare flag specifici di `WebFontStyle`.
* Salvare il documento modificato in una nuova posizione o in uno stream.
* Estendere la soluzione per altri stili di font, CSS personalizzato e gestione degli errori.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o versioni successive installate.
* Una licenza valida per **Aspose.HTML for .NET** (la versione di prova gratuita funziona per questo esempio).
* Visual Studio 2022 (o qualsiasi IDE C#) per compilare ed eseguire il codice.

Non sono richiesti pacchetti NuGet aggiuntivi oltre a `Aspose.HTML`.

## Passo 1: Configurare il progetto e importare i namespace

Crea un nuovo progetto **Console App** e aggiungi il pacchetto NuGet Aspose.HTML:

```bash
dotnet add package Aspose.HTML
```

Quindi, nella parte superiore di `Program.cs`, importa i namespace richiesti:

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
```

Questi namespace espongono i tipi `HTMLDocument`, `HtmlSaveOptions` e `WebFontStyle` che utilizzerai durante tutto il tutorial.

## Passo 2: Caricare il documento HTML di origine

La prima operazione è leggere l'HTML che desideri elaborare. Sostituisci `"YOUR_DIRECTORY/input.html"` con il percorso reale del tuo file.

```csharp
// Load the source HTML document from disk
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html");
```

`HTMLDocument` analizza il markup, costruisce un albero DOM e lo rende pronto per la manipolazione. Se il file non esiste, viene generata un'eccezione, quindi potresti voler avvolgere questa chiamata in un blocco try‑catch per il codice di produzione.

## Passo 3: Creare e configurare HtmlSaveOptions

`HtmlSaveOptions` ti consente di perfezionare il processo di salvataggio. Per abilitare gli stili di web‑font in grassetto e corsivo, combina i flag `WebFontStyle` corrispondenti usando l'operatore OR bitwise (`|`).

```csharp
// Create a new HtmlSaveOptions instance
HtmlSaveOptions saveOptions = new HtmlSaveOptions();

// Enable bold and italic web‑font styles (equivalent to the old FontStyle flags)
saveOptions.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

### Perché configurare WebFontStyle?

Quando esporti un documento HTML, Aspose.HTML può incorporare i web font che corrispondono allo stile originale. Impostando `WebFontStyle`, indichi all'esportatore quali varianti di font includere. Questo riduce la dimensione finale del file quando ti servono solo stili specifici e garantisce che l'output renderizzato corrisponda alla sorgente.

#### Varianti comuni

| Stile desiderato | Flag `WebFontStyle` corrispondente |
|------------------|------------------------------------|
| Normale (regolare) | `WebFontStyle.Regular` |
| Grassetto | `WebFontStyle.Bold` |
| Corsivo | `WebFontStyle.Italic` |
| Grassetto + Corsivo | `WebFontStyle.Bold | WebFontStyle.Italic` |
| Tutte le varianti | `WebFontStyle.All` |

Puoi combinare qualsiasi combinazione che si adatti al tuo scenario.

## Passo 4: Salvare il documento con le opzioni configurate

Ora scrivi il documento in un nuovo file. Il metodo `Save` accetta il percorso di destinazione e l'istanza `HtmlSaveOptions` che hai preparato.

```csharp
// Save the processed HTML using the configured options
document.Save("YOUR_DIRECTORY/output.html", saveOptions);
```

Se devi scrivere su uno stream di memoria (ad esempio per inviare il file via HTTP), usa la sovraccarico che accetta un oggetto `Stream`:

```csharp
using (var stream = new MemoryStream())
{
    document.Save(stream, saveOptions);
    // Reset the position to read the content later
    stream.Position = 0;
    // Example: return the stream from a Web API endpoint
}
```

## Passo 5: Verificare il risultato

Apri `output.html` in un browser o ispeziona il file con un editor di testo. Dovresti vedere che il blocco `<style>` ora contiene regole `@font-face` sia per le varianti in grassetto sia per quelle in corsivo di tutti i web font referenziati nel documento originale.

**Snippet di output previsto:**

```html
<link rel="stylesheet" href="fonts/Roboto-Bold.woff2" type="font/woff2">
<link rel="stylesheet" href="fonts/Roboto-Italic.woff2" type="font/woff2">
```

Se l'HTML originale referenziava una famiglia di font che aveva solo un peso regolare, Aspose.HTML includerà solo quel file, rispettando la configurazione `WebFontStyle`.

## Avanzato: Utilizzare HtmlSaveOptions con funzionalità aggiuntive

### 5.1 Controllare l'incorporamento CSS

Puoi decidere se incorporare il CSS inline, mantenere i link esterni o incorporare tutto:

```csharp
saveOptions.CssSavingMode = CssSavingMode.EmbedAllCss;
```

### 5.2 Salvataggio con una codifica specifica

```csharp
saveOptions.Encoding = Encoding.UTF8;
```

### 5.3 Gestione di documenti di grandi dimensioni

Per file HTML molto grandi, considera lo streaming dell'output per evitare un consumo elevato di memoria:

```csharp
using (FileStream fs = new FileStream("large_output.html", FileMode.Create, FileAccess.Write))
{
    document.Save(fs, saveOptions);
}
```

### 5.4 Migliori pratiche per la gestione degli errori

Avvolgi l'intero flusso di lavoro in un blocco try‑catch e registra i dettagli dell'eccezione. Questo garantisce che eventuali errori di I/O o di parsing vengano catturati:

```csharp
try
{
    // Load, configure, and save as shown earlier
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error processing HTML: {ex.Message}");
}
```

## Suggerimento professionale: Riutilizzare HtmlSaveOptions per più salvataggi

Se devi salvare diversi documenti con la stessa configurazione di stile dei font, crea un'unica istanza `HtmlSaveOptions` e riutilizzala. Questo riduce l'overhead di allocazione degli oggetti e garantisce un output coerente.

```csharp
HtmlSaveOptions sharedOptions = new HtmlSaveOptions
{
    WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
    CssSavingMode = CssSavingMode.EmbedAllCss
};

foreach (var file in Directory.GetFiles("input_folder", "*.html"))
{
    HTMLDocument doc = new HTMLDocument(file);
    string outputPath = Path.Combine("output_folder", Path.GetFileName(file));
    doc.Save(outputPath, sharedOptions);
}
```

## Esempio completo eseguibile

Di seguito trovi il programma completo che incorpora tutti i passaggi discussi. Copialo in `Program.cs` ed eseguilo dopo aver adeguato i percorsi dei file.

```csharp
using System;
using System.IO;
using System.Text;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath = "YOUR_DIRECTORY/input.html";
        string outputPath = "YOUR_DIRECTORY/output.html";

        try
        {
            // Step 1: Load the source HTML document
            HTMLDocument document = new HTMLDocument(inputPath);

            // Step 2: Create HtmlSaveOptions and enable bold + italic web‑font styles
            HtmlSaveOptions saveOptions = new HtmlSaveOptions
            {
                WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic,
                // Optional: embed all CSS and use UTF‑8 encoding
                CssSavingMode = CssSavingMode.EmbedAllCss,
                Encoding = Encoding.UTF8
            };

            // Step 3: Save the document with the configured options
            document.Save(outputPath, saveOptions);

            Console.WriteLine($"HTML saved successfully to '{outputPath}'.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Output console previsto

```
HTML saved successfully to 'YOUR_DIRECTORY/output.html'.
```

Apri il `output.html` generato per confermare che gli stili di web‑font in grassetto e corsivo sono presenti.

## Conclusione

Ora sai **come utilizzare HtmlSaveOptions** per controllare l'incorporamento dei web‑font, la gestione del CSS e la codifica quando salvi HTML con la libreria Aspose HTML in C#. Configurando i flag `WebFontStyle` puoi personalizzare l'output includendo solo le varianti di font di cui hai bisogno, migliorando le prestazioni e riducendo la dimensione del file.

Da qui puoi esplorare altre proprietà di `HtmlSaveOptions` come `ImageSavingMode`, `JavaScriptSavingMode`, o combinare più opzioni per pipeline di conversione complesse. Sperimenta il salvataggio su stream per API web, o integra il flusso di lavoro in un sistema più ampio di generazione di documenti.

---


## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come salvare HTML con Aspose.Html – Guida completa C#](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [Come usare Aspose per renderizzare HTML in PNG in C#](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-in-c/)
- [Come usare Aspose per renderizzare HTML in PNG – Guida passo‑passo](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}