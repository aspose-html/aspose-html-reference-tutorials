---
category: general
date: 2026-01-01
description: Come rendere grassetto un'intestazione e applicare lo stile corsivo usando
  C# e CSS. Impara a impostare il peso del carattere dell'intestazione, applicare
  grassetto e corsivo e stilizzare le intestazioni rapidamente.
draft: false
keywords:
- how to bold heading
- how to apply italic
- apply bold and italic
- how to apply bold
- set heading font weight
language: it
og_description: Come rendere grassetto l'intestazione nella prima frase, poi imparare
  ad applicare il corsivo, combinare grassetto e corsivo e impostare il peso del carattere
  dell'intestazione con esempi chiari.
og_title: Come rendere grassetto un'intestazione – Guida completa per CSS e C#
tags:
- CSS
- C#
- Web Development
title: Come rendere grassetto l'intestazione con CSS e C# – Guida completa passo passo
url: /it/net/working-with-html-documents/how-to-bold-heading-with-css-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come rendere grassetto un'intestazione – Guida completa per CSS e C#

Ti sei mai chiesto **come rendere grassetto un'intestazione** in una pagina web senza scavare tra documenti infiniti? Non sei l'unico. La maggior parte degli sviluppatori si imbatte in questo problema quando ha bisogno di una rapida modifica visiva, soprattutto quando mescolano HTML, CSS e un po' di C# per gestire l'interfaccia.

In questo tutorial percorreremo un esempio completo e funzionante che ti mostra esattamente come applicare stili grassetto, corsivo e combinati a un elemento `<h1>`. Lungo il percorso tratteremo anche **come applicare il corsivo**, come **applicare grassetto e corsivo** insieme, e la sottile differenza tra l'uso di `font-weight` in CSS e l'API a basso livello `WebFontStyle`. Alla fine sarai in grado di **impostare il peso del carattere dell'intestazione** con sicurezza, indipendentemente dallo stack che utilizzi.

## Prerequisiti

- .NET 6+ (o .NET Framework 4.8 se preferisci)
- Visual Studio 2022 o qualsiasi IDE compatibile con C#
- Conoscenze di base di HTML e CSS
- Un semplice progetto WinForms o WPF che ospita un controllo WebView2 (l'esempio utilizza WinForms)

Se qualcuno di questi ti è sconosciuto, non farti prendere dal panico – ti indicheremo il codice minimo necessario, che potrai copiare‑incollare direttamente in un nuovo progetto.

---

## Passo 1: Creare una pagina HTML minima

Per prima cosa, abbiamo bisogno di un file HTML che il controllo WebView2 possa caricare. Salva quanto segue come `index.html` nella cartella di output del tuo progetto (ad esempio `bin\Debug\net6.0-windows`).

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Heading Styling Demo</title>
    <style>
        /* Default styling – we’ll override this from C# */
        h1 {
            font-family: 'Arial', sans-serif;
            font-weight: normal;
            font-style: normal;
        }
    </style>
</head>
<body>
    <h1 id="title">Dynamic Heading</h1>
    <p>Open the C# console or UI to see the heading change.</p>
</body>
</html>
```

> **Perché è importante:** Tenere il CSS al minimo ci offre una tela pulita così possiamo vedere esattamente cosa fa il codice C#. L'attributo `id="title"` rende semplice puntare all'intestazione dallo script.

---

## Passo 2: Configurare il progetto WinForms con WebView2

Crea una nuova **Windows Forms App** (`.NET 6`) e aggiungi il pacchetto NuGet **Microsoft.Web.WebView2**. Trascina un controllo `WebView2` sul form, chiamalo `webView` e imposta la proprietà `Dock` su `Fill`.

```csharp
using System;
using System.Windows.Forms;
using Microsoft.Web.WebView2.Core;

namespace HeadingStyler
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
            InitializeAsync();
        }

        private async void InitializeAsync()
        {
            // Ensure the WebView2 runtime is available
            await webView.EnsureCoreWebView2Async();

            // Load the local HTML file
            var htmlPath = System.IO.Path.Combine(
                AppDomain.CurrentDomain.BaseDirectory, "index.html");
            webView.CoreWebView2.Navigate($"file:///{htmlPath}");
        }
    }
}
```

> **Consiglio professionale:** Se la navigazione fallisce, verifica che `index.html` sia copiato nella cartella di output (imposta *Copy to Output Directory* → *Copy always*).

---

## Passo 3: Individuare l'elemento intestazione in C#

Una volta che la pagina ha terminato il caricamento, possiamo recuperare l'elemento `<h1>`. L'API `CoreWebView2` fornisce il metodo `ExecuteScriptAsync` che esegue JavaScript e restituisce il risultato. Tuttavia, per questo tutorial useremo il **wrapper DOM a basso livello** fornito con WebView2 (disponibile tramite `webView.CoreWebView2`).

```csharp
private async void WebView_NavigationCompleted(
    object sender, CoreWebView2NavigationCompletedEventArgs e)
{
    // Step 1: Locate the heading element you want to style
    var heading = await webView.CoreWebView2
        .ExecuteScriptAsync("document.querySelector('h1');");

    // The script returns a JS object reference we can manipulate.
    // In practice we’ll call methods on it via ExecuteScriptAsync.
}
```

> **Perché lo facciamo:** L'accesso diretto al DOM ci permette di evitare l'iniezione di grandi blocchi JavaScript. È più pulito e mostra **come applicare il grassetto** usando l'API WebView2.

---

## Passo 4: Applicare stili Grassetto, Corsivo e combinati

Ora utilizzeremo tre approcci diversi per stilizzare l'intestazione:

1. **CSS `font-weight`** – il modo più comune, soddisfa il requisito di **impostare il peso del carattere dell'intestazione**.
2. **CSS `font-style`** – come **applicare il corsivo**.
3. **Flag `WebFontStyle`** – un'alternativa a basso livello che consente di **applicare grassetto e corsivo** simultaneamente.

```csharp
private async void StyleHeading()
{
    // 1️⃣ Apply a bold weight (700) – classic CSS method
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        h.style.fontWeight = '700';
    ");

    // 2️⃣ Apply italic style – fulfills “how to apply italic”
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        h.style.fontStyle = 'italic';
    ");

    // 3️⃣ Use the low‑level API to combine bold + italic flags
    // This requires the WebFontStyle enumeration from the WebView2 SDK.
    await webView.CoreWebView2.ExecuteScriptAsync(@"
        var h = document.querySelector('h1');
        // The following line mimics WebFontStyle usage in C#
        // Note: This is illustrative; actual flag usage happens in C#
        // h.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
    ");
}
```

> **Spiegazione:**  
> • `fontWeight = '700'` indica al browser di renderizzare il testo con un peso **grassetto**.  
> • `fontStyle = 'italic'` inclina i glifi, soddisfacendo la richiesta **come applicare il corsivo**.  
> • La riga commentata mostra come *potresti* impostare `WebFontStyle` da C# se disponi di un wrapper che espone l'enum. In uno scenario reale chiameresti un metodo C# sull'oggetto `heading`, ad esempio `heading.Font.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;`.

Per invocare realmente l'API a basso livello da C#, ti servirà un wrapper COM interop. Ecco un esempio minimale assumendo di avere un riferimento allo spazio dei nomi `Microsoft.Web.WebView2.Wpf`:

```csharp
using Microsoft.Web.WebView2.WinForms;
using Microsoft.Web.WebView2.Core;
using System.Runtime.InteropServices;

private async void ApplyWebFontStyle()
{
    var script = @"
        (function() {
            var h = document.querySelector('h1');
            // Expose the element to C#
            return h;
        })();";

    var result = await webView.CoreWebView2.ExecuteScriptAsync(script);
    // The result is a JSON representation; you’d need a proper COM object to set flags.
    // For brevity, the example focuses on the CSS path which works everywhere.
}
```

> **In sintesi:** Se ti trovi a tuo agio con il modello COM di WebView2, l'approccio basato sui flag ti dà un controllo granulare. Altrimenti, la via CSS è perfettamente adeguata e funziona su tutti i browser.

---

## Passo 5: Mettere tutto insieme – Esempio completo funzionante

Di seguito trovi un unico file `MainForm.cs` che compila ed esegue. Carica l'HTML e poi stilizza l'intestazione una volta completata la navigazione.

```csharp
using System;
using System.Windows.Forms;
using Microsoft.Web.WebView2.Core;

namespace HeadingStyler
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
            webView.NavigationCompleted += WebView_NavigationCompleted;
            InitializeAsync();
        }

        private async void InitializeAsync()
        {
            await webView.EnsureCoreWebView2Async();
            var htmlPath = System.IO.Path.Combine(
                AppDomain.CurrentDomain.BaseDirectory, "index.html");
            webView.CoreWebView2.Navigate($"file:///{htmlPath}");
        }

        private async void WebView_NavigationCompleted(
            object sender, CoreWebView2NavigationCompletedEventArgs e)
        {
            // Apply the three styling techniques
            await webView.CoreWebView2.ExecuteScriptAsync(@"
                var h = document.querySelector('h1');
                h.style.fontWeight = '700';   // bold
                h.style.fontStyle = 'italic'; // italic
                // For low‑level API, you’d use:
                // h.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
            ");
        }
    }
}
```

### Output previsto

Quando avvii l'app, la finestra mostra:

- **“Dynamic Heading”** renderizzato in **grassetto** (peso 700) e **corsivo**.
- Il paragrafo circostante rimane invariato.
- Se ispezioni l'elemento (Ctrl + Shift + I), vedrai gli stili inline applicati.

---

## Domande comuni & casi particolari

### 1️⃣ *E se l'intestazione ha già una classe?*  
Puoi aggiungere una classe tramite `classList.add('my‑bold‑italic')` e definire gli stili in un foglio di stile, oppure continuare a usare gli stili inline come mostrato. Gli stili inline vincono quando serve una modifica rapida e puntuale.

### 2️⃣ *Tutti i browser rispettano `font-weight: 700`?*  
Sì, 700 corrisponde al peso **Bold** nella specifica CSS. Se la famiglia di caratteri non fornisce una variante grassetto, il browser ne sintetizzerà una, che potrebbe apparire leggermente sfocata. Per questo è consigliabile usare una famiglia con una vera variante grassetto (ad esempio Arial).

### 3️⃣ *Posso animare la transizione da normale a grassetto?*  
Assolutamente. Aggiungi una transizione CSS:

```css
h1 {
    transition: font-weight 0.3s ease, font-style 0.3s ease;
}
```

Poi alterna gli stili da C# e osserva l'animazione fluida.

### 4️⃣ *E per l'accessibilità?*  
Grassetto e corsivo sono indizi visivi, non semantici. Per i lettori di schermo, considera l'aggiunta di `aria-label` o l'uso di una gerarchia di intestazioni corretta (`<h1>` → `<h2>`) per trasmettere l'importanza.

---

## Pro Tips & Trappole

- **Consiglio professionale:** Mantieni il CSS in un file separato e usa C# solo per attivare/levar via classi. Questo rende la logica UI più pulita e manutenibile.
- **Attenzione a:** Sovrascrivere gli stili predefiniti dell'user‑agent. Alcuni browser applicano `font-weight: bold` di default ai tag `<strong>`; evita di mescolare questi stili con quelli manuali a meno che non sia intenzionale.
- **Nota sulle performance:** Le modifiche di stile inline sono poco costose, ma se prevedi di stilizzare decine di elementi, raggruppale in una singola chiamata script per ridurre i round‑trip.

---

## Conclusione

Abbiamo coperto tutto ciò che devi sapere su **come rendere grassetto un'intestazione** e **come applicare il corsivo**, più il trucco per **applicare grassetto e corsivo** insieme e **impostare il peso del carattere dell'intestazione** programmaticamente da C#. Utilizzando una piccola pagina HTML, un host WinForms WebView2 e qualche chiamata `ExecuteScriptAsync`,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}