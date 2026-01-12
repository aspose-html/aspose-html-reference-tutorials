---
category: general
date: 2025-12-29
description: Crea un documento HTML in C# e impara come impostare la famiglia di caratteri,
  impostare la dimensione del carattere, quindi salva l'HTML come PDF o converti l'HTML
  in PDF usando Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: it
og_description: Crea un documento HTML in C# e visualizza subito come impostare la
  famiglia di caratteri, impostare la dimensione del carattere, quindi salva l'HTML
  come PDF o converti l'HTML in PDF con Aspose.HTML.
og_title: Crea documento HTML – Testo formattato ed esportazione PDF
tags:
- aspnet
- csharp
- pdf-generation
title: Crea documento HTML con testo formattato ed esporta in PDF – Guida completa
url: /it/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un documento HTML con testo formattato ed esportalo in PDF

Hai mai dovuto **creare un documento HTML** al volo e trasformarlo in PDF senza uscire dal tuo codice C#? Forse stai costruendo un motore di report, un generatore di fatture, o semplicemente un'anteprima rapida per gli utenti. La buona notizia è che puoi farlo in poche righe usando Aspose.HTML, ottenendo il pieno controllo su famiglia di caratteri, dimensione del carattere e persino lo stile grassetto‑corsivo.

In questo tutorial percorreremo l’intero processo — dalla creazione di un documento HTML in memoria al salvataggio come file PDF. Alla fine saprai esattamente come **impostare la famiglia di caratteri**, **impostare la dimensione del carattere** e **salvare HTML come PDF** (cioè **convertire HTML in PDF**) con un esempio di codice pulito e pronto per la produzione.

## Cosa ti serve

- .NET 6+ (l’API funziona sia con .NET Core sia con .NET Framework)  
- Pacchetto NuGet Aspose.HTML per .NET (`Aspose.Html`) – installalo con `dotnet add package Aspose.Html`  
- Una cartella su disco dove poter scrivere il PDF generato  

Nessun modello HTML aggiuntivo, nessun convertitore esterno, solo puro C#.

![illustrazione creazione documento html](/images/create-html-document.png){alt="esempio di creazione documento html"}

## Passo 1: Crea il documento HTML

Per prima cosa, abbiamo bisogno di un oggetto documento HTML vuoto. Pensalo come una tela fresca su cui dipingerai più tardi il tuo paragrafo formattato.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Perché è importante:** `HTMLDocument` ti fornisce una struttura simile al DOM che puoi manipolare programmaticamente. Non è necessario toccare stringhe grezze o I/O di file fino all’ultimo passaggio.

## Passo 2: Aggiungi un paragrafo e imposta famiglia di caratteri e dimensione

Ora creeremo un elemento `<p>`, inseriremo del testo e definiremo esplicitamente la famiglia di caratteri e la dimensione. È qui che entrano in gioco le parole chiave **set font family** e **set font size**.

```csharp
// Step 2 – create a <p> element with some sample text
HtmlElement paragraph = htmlDocument.CreateElement("p");
paragraph.InnerHtml = "Bold & Italic text";

// Define the base font style
paragraph.Style.FontFamily = "Arial";   // set font family
paragraph.Style.FontSize = "18px";      // set font size

// Attach the paragraph to the document body
body.AppendChild(paragraph);
```

**Consiglio professionale:** Se ti serve un fallback web‑safe, puoi fornire una lista separata da virgole come `"Arial, Helvetica, sans-serif"`; il browser (o Aspose) sceglierà il primo font disponibile.

## Passo 3: Applica lo stile Grassetto e Corsivo con i flag WebFontStyle

Aspose.HTML espone un comodo enum `WebFontStyle` che ti permette di combinare gli stili con un OR bitwise. Facciamo in modo che il testo sia sia grassetto **che** corsivo.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Cosa succede dietro le quinte?** La proprietà `FontStyle` si traduce in dichiarazioni CSS `font-weight` e `font-style`. Unendo i flag evitiamo di scrivere due righe separate di CSS.

## Passo 4: Converti l'HTML in PDF (Salva HTML come PDF)

L’ultimo passo è la conversione vera e propria. Con una singola chiamata a `Save`, Aspose.HTML rende il DOM e scrive un file PDF su disco. Questo soddisfa sia i requisiti **save html as pdf** sia **convert html to pdf**.

```csharp
// Step 4 – save the HTML document as a PDF file
string outputPath = @"C:\Temp\styled.pdf";
htmlDocument.Save(outputPath, new PDFSaveOptions());

// Optional: open the PDF automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Risultato atteso:** Apri `styled.pdf` e vedrai un unico paragrafo con il testo “Bold & Italic text” in Arial 18 px, reso in grassetto e corsivo. Le dimensioni del PDF corrispondono a una pagina A4 standard, e il testo è selezionabile — grazie al rendering vettoriale.

## Esempio completo funzionante

Mettendo tutto insieme, ecco il programma completo, pronto per l’esecuzione:

```csharp
using System;
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new HTML document
        HTMLDocument htmlDocument = new HTMLDocument();
        HTMLBodyElement body = htmlDocument.Body;

        // 2️⃣ Add a styled paragraph
        HtmlElement paragraph = htmlDocument.CreateElement("p");
        paragraph.InnerHtml = "Bold & Italic text";

        // Set font family and size
        paragraph.Style.FontFamily = "Arial";
        paragraph.Style.FontSize = "18px";

        // 3️⃣ Apply bold + italic
        paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // Append to body
        body.AppendChild(paragraph);

        // 4️⃣ Save as PDF (convert HTML to PDF)
        string outputFile = @"C:\Temp\styled.pdf";
        htmlDocument.Save(outputFile, new PDFSaveOptions());

        Console.WriteLine($"PDF generated at: {outputFile}");
    }
}
```

### Esecuzione del codice

1. Installa il pacchetto NuGet Aspose.HTML:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Sostituisci `C:\Temp\styled.pdf` con una cartella in cui hai i permessi di scrittura.  
3. Compila ed esegui: `dotnet run`.  

Dovresti vedere un messaggio nella console che conferma la posizione del file, e il PDF conterrà il paragrafo formattato.

## Domande frequenti e casi particolari

- **E se ho bisogno di un font web personalizzato?**  
  Carica il font con `HTMLFontFaceRule` o riferisci un file CSS remoto `@font-face` prima di creare il paragrafo.

- **Posso aggiungere immagini prima della conversione?**  
  Assolutamente. Usa `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` e imposta `img.Source` a un percorso locale o a un data URI.

- **Cosa succede con PDF multi‑pagina?**  
  Aggiungi più elementi (tabelle, div, ecc.) e Aspose.HTML paginerà automaticamente quando il contenuto supera l’altezza della pagina.

- **È possibile controllare i metadati del PDF?**  
  Passa un’istanza di `PdfSaveOptions` e imposta proprietà come `Author`, `Title` o `PdfAConformanceLevel`.

## Riepilogo

Abbiamo visto come **creare un documento HTML** in C#, **impostare la famiglia di caratteri**, **impostare la dimensione del carattere**, applic stili grassetto‑corsivo e infine **salvare HTML come PDF** — ovvero **convertire HTML in PDF** con Aspose.HTML. Lo snippet è sufficientemente breve da poterlo inserire in qualsiasi progetto .NET, ma anche abbastanza completo da fungere da solida base per scenari di reporting più complessi.

## Prossimi passi

- Sperimenta con classi CSS per stili riutilizzabili.  
- Combina più paragrafi, tabelle e immagini per creare PDF più ricchi.  
- Esplora la conformità PDF/A se ti servono documenti di livello archivistico.  

Sentiti libero di modificare font, dimensione o colori — non ci sono limiti a ciò che puoi generare programmaticamente. Buon coding, e che i tuoi PDF vengano sempre renderizzati esattamente come li immagini!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}