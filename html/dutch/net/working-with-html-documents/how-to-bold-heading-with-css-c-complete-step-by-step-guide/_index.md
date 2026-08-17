---
category: general
date: 2026-01-01
description: Hoe een kop vet maken en cursieve stijl toepassen met C# en CSS. Leer
  de lettergewicht van een kop instellen, vet en cursief toepassen, en koppen snel
  stijlen.
draft: false
keywords:
- how to bold heading
- how to apply italic
- apply bold and italic
- how to apply bold
- set heading font weight
language: nl
og_description: Hoe je een kop vet maakt in de eerste zin, vervolgens leert om cursief
  toe te passen, vet en cursief te combineren, en de letterdikte van de kop in te
  stellen met duidelijke voorbeelden.
og_title: Hoe een koptekst vet maken – Volledige gids voor CSS & C#
tags:
- CSS
- C#
- Web Development
title: Hoe een koptekst vet maken met CSS & C# – Complete stap‑voor‑stap gids
url: /nl/net/working-with-html-documents/how-to-bold-heading-with-css-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Kop Vet Maken – Volledige Gids voor CSS & C#

Heb je je ooit afgevraagd **hoe je een kop vet maakt** op een webpagina zonder eindeloos door documentatie te graven? Je bent niet de enige. De meeste ontwikkelaars lopen tegen dit probleem aan wanneer ze snel een visuele aanpassing nodig hebben, vooral wanneer ze HTML, CSS en een beetje C# combineren om de UI aan te sturen.  

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat je precies laat zien hoe je vet, cursief en gecombineerde stijlen toepast op een `<h1>`-element. Onderweg behandelen we ook **hoe je cursief toepast**, hoe je **vet en cursief samen toepast**, en het subtiele verschil tussen het gebruik van CSS `font-weight` versus de low‑level `WebFontStyle` API. Aan het einde kun je **de lettertypegewicht van een kop instellen** met vertrouwen, ongeacht welke stack je gebruikt.

## Vereisten

- .NET 6+ (of .NET Framework 4.8 als je dat liever hebt)
- Visual Studio 2022 of een C#‑compatibele IDE
- Basiskennis van HTML en CSS
- Een eenvoudig WinForms- of WPF-project dat een WebView2‑control host (het voorbeeld gebruikt WinForms)

Als een van deze je onbekend voorkomt, geen paniek – we wijzen je op de minimale code die je nodig hebt, en je kunt deze direct kopiëren‑plakken in een nieuw project.

---

## Stap 1: Maak een Minimale HTML-pagina

Eerst hebben we een HTML‑bestand nodig dat de WebView2‑control kan laden. Sla het volgende op als `index.html` in de output‑map van je project (bijv. `bin\Debug\net6.0-windows`).

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

> **Waarom dit belangrijk is:** Het minimalistisch houden van de CSS geeft ons een schone basis zodat we precies kunnen zien wat de C#‑code doet. Het `id="title"`‑attribuut maakt het eenvoudig om de kop vanuit het script te targeten.

---

## Stap 2: Zet het WinForms‑project op met WebView2

Maak een nieuwe **Windows Forms App** (`.NET 6`) aan en voeg het **Microsoft.Web.WebView2** NuGet‑pakket toe. Sleep een `WebView2`‑control naar het formulier, noem deze `webView`, en stel de `Dock`‑eigenschap in op `Fill`.

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

> **Pro tip:** Als de navigatie mislukt, controleer dan dubbel of `index.html` naar de output‑map is gekopieerd (stel *Copy to Output Directory* → *Copy always* in).

---

## Stap 3: Zoek het Kop‑element in C#

Zodra de pagina is geladen, kunnen we het `<h1>`‑element pakken. De `CoreWebView2`‑API biedt een `ExecuteScriptAsync`‑methode die JavaScript uitvoert en het resultaat retourneert. Voor dit tutorialdoel gebruiken we echter de **low‑level DOM‑wrapper** die met WebView2 wordt geleverd (beschikbaar via `webView.CoreWebView2`).

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

> **Waarom we dit doen:** Directe DOM‑toegang laat ons grote JavaScript‑blobs injecteren vermijden. Het is schoner en toont **hoe je vet toepast** met de WebView2‑API.

---

## Stap 4: Pas Vet, Cursief en Gecombineerde Stijlen toe

Nu gebruiken we drie verschillende benaderingen om de kop te stijlen:

1. **CSS `font-weight`** – de meest voorkomende manier, die voldoet aan de **set heading font weight**‑vereiste.
2. **CSS `font-style`** – hoe je **cursief toepast**.
3. **`WebFontStyle`‑vlaggen** – een low‑level alternatief dat ons **vet en cursief tegelijk toepast**.

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

> **Uitleg:**  
> • `fontWeight = '700'` vertelt de browser om de tekst weer te geven met een **vet** gewicht.  
> • `fontStyle = 'italic'` kantelt de tekens, wat voldoet aan de **how to apply italic**‑vraag.  
> • De gecommentarieerde regel laat zien hoe je *zou* `WebFontStyle` vanuit C# kunt instellen als je een wrapper hebt die de enum blootlegt. In een real‑world scenario zou je een C#‑methode aanroepen op het `heading`‑object, bijv. `heading.Font.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;`.

Om de low‑level API vanuit C# daadwerkelijk aan te roepen, heb je een COM‑interop wrapper nodig. Hier is een minimaal voorbeeld, ervan uitgaande dat je een referentie hebt naar de `Microsoft.Web.WebView2.Wpf`‑namespace:

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

> **Conclusie:** Als je vertrouwd bent met het WebView2 COM‑model, geeft de vlag‑benadering je fijnmazige controle. Anders is de CSS‑route meer dan voldoende en werkt deze in alle browsers.

---

## Stap 5: Alles Samenvoegen – Volledig Werkend Voorbeeld

Hieronder staat een enkel `MainForm.cs`‑bestand dat compileert en draait. Het laadt de HTML en stijlt de kop zodra de navigatie voltooid is.

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

### Verwachte Output

Wanneer je de app uitvoert, toont het venster:

- **“Dynamic Heading”** weergegeven in **vet** (gewicht 700) en **cursief**.
- De omringende alinea blijft ongewijzigd.
- Als je het element inspecteert (Ctrl + Shift + I), zie je de inline‑stijlen toegepast.

---

## Veelgestelde Vragen & Randgevallen

### 1️⃣ *Wat als de kop al een class heeft?*  
Je kunt een class toevoegen via `classList.add('my‑bold‑italic')` en de stijlen in een stylesheet definiëren, of de inline‑stijlen blijven gebruiken zoals getoond. Inline‑stijlen winnen wanneer je een snelle, eenmalige wijziging nodig hebt.

### 2️⃣ *Respecteren alle browsers `font-weight: 700`?*  
Ja, 700 komt overeen met het **Bold**‑gewicht in de CSS‑specificatie. Als de lettertypefamilie geen vette variant biedt, zal de browser er een synthetiseren, wat iets wazig kan lijken. Daarom wordt aangeraden een lettertypefamilie met een echte vette variant te gebruiken (bijv. Arial).

### 3️⃣ *Kan ik de overgang van normaal naar vet animeren?*  
Zeker. Voeg een CSS‑transition toe:

```css
h1 {
    transition: font-weight 0.3s ease, font-style 0.3s ease;
}
```

### 4️⃣ *Hoe zit het met toegankelijkheid?*  
Vet en cursief zijn visuele aanwijzingen, geen semantische. Voor schermlezers kun je overwegen `aria-label` toe te voegen of een juiste kophiërarchie te gebruiken (`<h1>` → `<h2>`) om belangrijkheid over te brengen.

---

## Pro Tips & Valkuilen

- **Pro tip:** Houd je CSS in een apart bestand en gebruik C# alleen om classes te toggelen. Dit maakt de UI‑logica schoner en makkelijker te onderhouden.
- **Let op:** Het overschrijven van user‑agent stijlen. Sommige browsers passen standaard `font-weight: bold` toe op `<strong>`‑tags; vermijd het combineren van die stijlen met handmatige styling tenzij je dat wilt.
- **Prestatienota:** Inline‑stijlwijzigingen zijn goedkoop, maar als je van plan bent tientallen elementen te stijlen, batch ze dan in één script‑aanroep om round‑trips te verminderen.

## Conclusie

We hebben alles behandeld wat je moet weten over **hoe je een kop vet maakt** en **hoe je cursief toepast**, plus de truc om **vet en cursief samen toe te passen** en **de lettertypegewicht van een kop in te stellen** programmatically vanuit C#. Door een kleine HTML‑pagina, een WinForms WebView2‑host en een handvol `ExecuteScriptAsync`‑aanroepen te gebruiken,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}