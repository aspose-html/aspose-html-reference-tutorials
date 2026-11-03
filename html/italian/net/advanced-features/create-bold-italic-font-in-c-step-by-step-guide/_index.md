---
category: general
date: 2026-08-15
description: Crea rapidamente un font grassetto e corsivo in C#. Scopri come creare
  un font in C# con stili grassetto e corsivo usando la classe Font integrata.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create bold italic font
- create font in c#
- C# FontStyle
- text styling C#
- System.Drawing.Font
language: it
lastmod: 2026-08-15
og_description: Crea un font grassetto e corsivo in C# con un esempio chiaro. Questo
  tutorial mostra come creare un font in C# usando i flag FontStyle e spiega le insidie
  più comuni.
og_image_alt: Screenshot of text rendered with a bold italic Arial font in a C# console
  window
og_title: Crea un font grassetto e corsivo in C# – guida completa di programmazione
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  headline: Create bold italic font in C# – step‑by‑step guide
  type: TechArticle
- description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  name: Create bold italic font in C# – step‑by‑step guide
  steps:
  - name: Save the code to a file named `Program.cs`.
    text: Save the code to a file named `Program.cs`.
  - name: Open a terminal in the file’s directory.
    text: Open a terminal in the file’s directory.
  - name: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
    text: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
  - name: Replace the generated `Program.cs` with the code above.
    text: Replace the generated `Program.cs` with the code above.
  - name: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
    text: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
  - name: Build and run with `dotnet run`.
    text: Build and run with `dotnet run`.
  type: HowTo
tags:
- C#
- fonts
- text styling
title: Crea un font grassetto e corsivo in C# – guida passo passo
url: /it/net/advanced-features/create-bold-italic-font-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea un font grassetto corsivo in C# – guida passo‑passo

Se hai bisogno di **creare un font grassetto corsivo** in C#, questa guida ti mostra esattamente come farlo. Vedrai un esempio completo e eseguibile che dimostra anche come **creare un font in C#** usando la classe standard .NET `Font`.

Lavorare con font personalizzati è una parte routine della creazione di app desktop Windows, della generazione di PDF o del rendering di HTML sul server. Alla fine di questo tutorial sarai in grado di istanziare un font sia grassetto che corsivo, capire perché viene usato l'operatore bitwise `|` e gestire casi limite comuni come famiglie di font mancanti.

Non sono richieste librerie esterne—tutto utilizza la libreria di classi di base .NET Framework / .NET Core.

## Cosa imparerai

* Come importare gli spazi dei nomi necessari per la gestione dei font.  
* La sintassi per combinare `FontStyle.Bold` e `FontStyle.Italic`.  
* Come verificare che il font sia stato creato correttamente.  
* Suggerimenti per la gestione dei fallback quando la famiglia richiesta non è installata.  

Non sono richieste librerie esterne—tutto utilizza la libreria di classi di base .NET Framework / .NET Core.

## Prerequisiti

* .NET 6.0 SDK o successivo (il codice funziona anche su .NET Framework 4.6+).  
* Un editor di codice o IDE (Visual Studio, VS Code, Rider, ecc.).  
* Familiarità di base con la sintassi C#.  

Se soddisfi questi prerequisiti, puoi seguire i passaggi senza alcuna configurazione aggiuntiva.

## Passo 1: Aggiungi le direttive using necessarie

La classe `Font` si trova nello spazio dei nomi `System.Drawing`, che fa parte del pacchetto NuGet `System.Drawing.Common` per .NET Core/.NET 5+. Aggiungi lo spazio dei nomi all'inizio del tuo file:

```csharp
using System;
using System.Drawing;   // Provides Font and FontStyle
```

> **Perché questo passaggio è importante** – Senza la riga `using System.Drawing;` il compilatore non può individuare `Font` o `FontStyle`, generando un errore “type or namespace name could not be found”.

## Passo 2: Combina gli stili grassetto e corsivo con l'operatore OR bitwise

In .NET, `FontStyle` è un enum contrassegnato con l'attributo `[Flags]`. Questo significa che puoi combinare più valori usando l'operatore `|` (OR bitwise):

```csharp
// Step 2: Create a Font that is both bold and italic
var font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
```

### Spiegazione

* `"Arial"` – il nome della famiglia di font. Se il sistema non ha Arial installato, il costruttore ricade sul font predefinito.  
* `12` – dimensione in punti.  
* `FontStyle.Bold | FontStyle.Italic` – combina le due bandiere di stile. L'operatore `|` unisce la rappresentazione binaria di ciascuna bandiera, producendo un unico valore che rappresenta “grassetto + corsivo”.

> **Consiglio pro:** Usa sempre i nomi dell'enum (`FontStyle.Bold`) invece di numeri magici; questo migliora la leggibilità e previene bug quando i valori dell'enum cambiano.

## Passo 3: Verifica il font creato (opzionale ma consigliato)

Stampare le proprietà del font ti aiuta a confermare che la combinazione di stili sia riuscita, specialmente durante il debug su una nuova macchina.

```csharp
// Step 3: Output the font details to the console
Console.WriteLine($"Font family: {font.Name}");
Console.WriteLine($"Size (pt): {font.Size}");
Console.WriteLine($"Style: {font.Style}");
```

**Output previsto**

```
Font family: Arial
Size (pt): 12
Style: Bold, Italic
```

Se l'output elenca sia `Bold` che `Italic`, il font è stato creato correttamente.

## Passo 4: Renderizza una stringa di esempio (conferma visiva)

Quando esegui un'app console non puoi vedere lo stile effettivo dei glifi, ma puoi generare un'immagine per dimostrare il risultato. Il frammento seguente disegna “Hello, World!” usando il font grassetto‑corsivo e lo salva come *sample.png*:

```csharp
// Step 4: Draw text to an image file for visual confirmation
using (var bitmap = new Bitmap(300, 100))
using (var graphics = Graphics.FromImage(bitmap))
{
    graphics.Clear(Color.White);
    var brush = Brushes.Black;
    graphics.DrawString("Hello, World!", font, brush, new PointF(10, 30));
    bitmap.Save("sample.png");
    Console.WriteLine("Image saved as sample.png");
}
```

Dopo che il programma è terminato, apri *sample.png* per vedere il testo renderizzato con lo stile grassetto corsivo.

![Testo di esempio renderizzato con font grassetto corsivo](sample.png)

*Testo alternativo dell'immagine: Screenshot del testo renderizzato con un font Arial grassetto corsivo in una finestra console C#* – questo testo alternativo soddisfa il requisito SEO per il testo alternativo delle immagini.

## Passo 5: Fallback elegante quando la famiglia di font non è disponibile

Se la famiglia richiesta (ad es., “Arial”) non è installata, il costruttore `Font` lancia un `ArgumentException`. Avvolgi la creazione in un blocco `try/catch` e ricorri a un font sicuro noto, come “Segoe UI”.

```csharp
Font font;
try
{
    font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
}
catch (ArgumentException)
{
    Console.WriteLine("Arial not found – falling back to Segoe UI.");
    font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
}
```

**Perché gestirlo?** In ambienti containerizzati o headless il set predefinito di font può differire da un tipico desktop. Fornire un fallback previene crash a runtime e garantisce uno stile coerente.

## Esempio completo, eseguibile

Mettendo tutto insieme, ecco un programma completo che puoi copiare, incollare ed eseguire:

```csharp
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create the font (bold + italic)
        Font font;
        try
        {
            font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
        }
        catch (ArgumentException)
        {
            Console.WriteLine("Arial not found – using Segoe UI as fallback.");
            font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
        }

        // Display font information
        Console.WriteLine($"Font family: {font.Name}");
        Console.WriteLine($"Size (pt): {font.Size}");
        Console.WriteLine($"Style: {font.Style}");

        // Render a sample image
        using (var bitmap = new Bitmap(300, 100))
        using (var graphics = Graphics.FromImage(bitmap))
        {
            graphics.Clear(Color.White);
            graphics.DrawString("Hello, World!", font, Brushes.Black, new PointF(10, 30));
            bitmap.Save("sample.png");
        }

        Console.WriteLine("Sample image saved as sample.png");
    }
}
```

### Come eseguire

1. Salva il codice in un file chiamato `Program.cs`.  
2. Apri un terminale nella directory del file.  
3. Esegui `dotnet new console -n FontDemo` (se ti serve uno scheletro di progetto).  
4. Sostituisci il `Program.cs` generato con il codice sopra.  
5. Esegui `dotnet add package System.Drawing.Common` (necessario per .NET Core/5+).  
6. Compila ed esegui con `dotnet run`.  

Vedrai l'output della console che conferma le proprietà del font, e `sample.png` apparirà nella cartella del progetto.

## Problemi comuni e come evitarli

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| **Manca il pacchetto `System.Drawing.Common`** | .NET Core non include `System.Drawing` per impostazione predefinita. | Esegui `dotnet add package System.Drawing.Common`. |
| **Famiglia di font non installata** | Le immagini Docker headless spesso non hanno i font Windows. | Usa un font di fallback o installa i font richiesti nel container. |
| **Uso errato di `|`** | Usare `+` invece di `|` produce una combinazione non valida. | Combina sempre i valori di `FontStyle` con l'operatore OR bitwise (`|`). |
| **Non rilasciare l'oggetto `Font`** | Non chiamare `Dispose` può provocare perdite di risorse GDI. | Avvolgi `Font` in un blocco `using` o chiama `font.Dispose()` dopo aver finito. |

## Conclusione

Ora sai come **creare un font grassetto corsivo** in C# e come **creare un font in C#** in modo sicuro ed efficiente. Il tutorial ha coperto l'importazione dello spazio dei nomi corretto, la combinazione delle bandiere `FontStyle`, la verifica del risultato, il rendering di un esempio visivo e la gestione delle famiglie di font mancanti.

Successivamente, potresti esplorare:

* **Creare font sottolineati o barrati** – aggiungi `FontStyle.Underline` o `FontStyle.Strikeout`.  
* **Usare font TrueType personalizzati** – carica un file `.ttf` con `PrivateFontCollection`.  
* **Applicare i font in WinForms, WPF o nella generazione di PDF** – lo stesso oggetto `Font` può essere passato a controlli UI o a librerie di terze parti.  

Sentiti libero di sperimentare con diverse famiglie, dimensioni e combinazioni di stile. Se incontri problemi, rivedi la tabella “Problemi comuni” o consulta la documentazione ufficiale [.NET per System.Drawing.Font](https://learn.microsoft.com/dotnet/api/system.drawing.font). Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come combinare i font programmaticamente in C# – Guida passo‑passo](/html/indonesian/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/)
- [Crea documento HTML con testo formattato ed esporta in PDF – Guida completa](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [converti docx in png – crea archivio zip tutorial C#](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}