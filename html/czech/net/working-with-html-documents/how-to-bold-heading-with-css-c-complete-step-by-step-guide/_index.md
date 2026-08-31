---
category: general
date: 2026-01-01
description: Jak zvýraznit nadpis tučným písmem a použít kurzívu pomocí C# a CSS.
  Naučte se nastavit tloušťku písma nadpisu, použít tučné a kurzívní písmo a rychle
  stylovat nadpisy.
draft: false
keywords:
- how to bold heading
- how to apply italic
- apply bold and italic
- how to apply bold
- set heading font weight
language: cs
og_description: Jak zvýraznit nadpis tučným písmem v první větě, pak se naučit použít
  kurzívu, kombinovat tučné a kurzívu a nastavit tloušťku písma nadpisu s jasnými
  příklady.
og_title: Jak ztučnit nadpis – Kompletní průvodce pro CSS a C#
tags:
- CSS
- C#
- Web Development
title: Jak zvýraznit nadpis tučným písmem pomocí CSS a C# – Kompletní krok za krokem
  průvodce
url: /cs/net/working-with-html-documents/how-to-bold-heading-with-css-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak tučnit nadpis – Kompletní průvodce pro CSS & C#

Už jste se někdy zamýšleli **jak tučnit nadpis** na webové stránce, aniž byste prohrabávali nekonečné dokumentace? Nejste v tom sami. Většina vývojářů narazí na tento problém, když potřebují rychlou vizuální úpravu, zejména když kombinují HTML, CSS a trochu C# pro ovládání UI.  

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který vám přesně ukáže, jak použít tučné, kurzívní a kombinované styly na element `<h1>`. Během toho se také podíváme na **jak použít kurzívu**, jak **použít tučné a kurzívu** dohromady a na jemný rozdíl mezi použitím CSS `font-weight` a nízkoúrovňovým `WebFontStyle` API. Na konci budete schopni **nastavit tloušťku písma nadpisu** s jistotou, bez ohledu na to, jaký stack používáte.

## Předpoklady

- .NET 6+ (nebo .NET Framework 4.8, pokud dáváte přednost)
- Visual Studio 2022 nebo jakékoli IDE kompatibilní s C#
- Základní znalosti HTML a CSS
- Jednoduchý projekt WinForms nebo WPF, který hostuje kontrolu WebView2 (příklad používá WinForms)

Pokud vám některý z nich není známý, nepanikařte – ukážeme vám minimální kód, který potřebujete, a můžete jej zkopírovat a vložit přímo do nového projektu.

---

## Krok 1: Vytvořte minimální HTML stránku

Nejprve potřebujeme HTML soubor, který může načíst kontrola WebView2. Uložte následující jako `index.html` do výstupní složky vašeho projektu (např. `bin\Debug\net6.0-windows`).

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

> **Proč je to důležité:** Udržení CSS na minimu nám dává čistý základ, takže můžeme přesně vidět, co C# kód dělá. Atribut `id="title"` usnadňuje cílení na nadpis ze skriptu.

---

## Krok 2: Nastavte projekt WinForms s WebView2

Vytvořte novou **Windows Forms App** (`.NET 6`) a přidejte balíček NuGet **Microsoft.Web.WebView2**. Přetáhněte kontrolu `WebView2` na formulář, pojmenujte ji `webView` a nastavte její vlastnost `Dock` na `Fill`.

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

> **Pro tip:** Pokud navigace selže, zkontrolujte, že `index.html` je zkopírován do výstupní složky (nastavte *Copy to Output Directory* → *Copy always*).

---

## Krok 3: Najděte element nadpisu v C#

Jakmile se stránka načte, můžeme zachytit element `<h1>`. API `CoreWebView2` poskytuje metodu `ExecuteScriptAsync`, která spouští JavaScript a vrací výsledek. Pro účely tohoto tutoriálu však použijeme **nízkoúrovňový DOM wrapper**, který je součástí WebView2 (dostupný přes `webView.CoreWebView2`).

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

> **Proč to děláme:** Přímý přístup k DOM nám umožňuje vyhnout se vkládání velkých JavaScriptových bloků. Je to čistší a ukazuje **jak použít tučné** pomocí WebView2 API.

---

## Krok 4: Použijte tučné, kurzívní a kombinované styly

Nyní použijeme tři různé přístupy ke stylování nadpisu:

1. **CSS `font-weight`** – nejčastější způsob, splňující požadavek **nastavit tloušťku písma nadpisu**.
2. **CSS `font-style`** – jak **použít kurzívu**.
3. **`WebFontStyle` flags** – nízkoúrovňová alternativa, která nám umožní **použít tučné a kurzívu** současně.

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

> **Vysvětlení:**  
> • `fontWeight = '700'` říká prohlížeči, aby vykreslil text s **tučnou** vahou.  
> • `fontStyle = 'italic'` nakloní glyfy, čímž splňuje dotaz **jak použít kurzívu**.  
> • Komentovaná řádka ukazuje, jak byste *mohli* nastavit `WebFontStyle` z C#, pokud máte wrapper, který vystavuje enum. Ve skutečném scénáři byste zavolali C# metodu na objektu `heading`, např. `heading.Font.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;`.

Pro skutečné volání nízkoúrovňového API z C# byste potřebovali COM interop wrapper. Zde je minimální příklad za předpokladu, že máte referenci na jmenný prostor `Microsoft.Web.WebView2.Wpf`.

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

> **Závěr:** Pokud vám vyhovuje COM model WebView2, přístup s příznaky vám poskytne detailní kontrolu. Jinak je cesta přes CSS naprosto dostačující a funguje ve všech prohlížečích.

---

## Krok 5: Spojte vše dohromady – kompletní funkční příklad

Níže je jediný soubor `MainForm.cs`, který se zkompiluje a spustí. Načte HTML a poté styluje nadpis po dokončení navigace.

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

### Očekávaný výstup

Když spustíte aplikaci, okno zobrazí:

- **„Dynamic Heading“** vykreslený **tučně** (váha 700) a **kurzívou**.
- Okolní odstavec zůstane nezměněn.
- Pokud prozkoumáte element (Ctrl + Shift + I), uvidíte aplikované inline styly.

---

## Časté otázky a okrajové případy

### 1️⃣ *Co když už nadpis má třídu?*  
Můžete buď přidat třídu pomocí `classList.add('my‑bold‑italic')` a definovat styly v stylesheetu, nebo pokračovat s inline styly, jak je ukázáno. Inline styly vítězí, když potřebujete rychlou jednorázovou změnu.

### 2️⃣ *Respektují všechny prohlížeče `font-weight: 700`?*  
Ano, 700 odpovídá **Bold** váze v CSS specifikaci. Pokud daná rodina písem nenabízí tučnou variantu, prohlížeč ji syntetizuje, což může vypadat mírně rozmazaně. Proto se doporučuje použít rodinu písem s pravou tučnou variantou (např. Arial).

### 3️⃣ *Mohu animovat přechod z normálního na tučné?*  
Určitě. Přidejte CSS transition:

```css
h1 {
    transition: font-weight 0.3s ease, font-style 0.3s ease;
}
```

### 4️⃣ *Co s přístupností?*  
Tučné a kurzíva jsou vizuální nápovědy, ne sémantické. Pro čtečky obrazovky zvažte přidání `aria-label` nebo použití správné hierarchie nadpisů (`<h1>` → `<h2>`), aby se vyjádřila důležitost.

---

## Pro tipy a úskalí

- **Pro tip:** Udržujte CSS v samostatném souboru a používejte C# pouze k přepínání tříd. To dělá UI logiku čistší a snadněji udržovatelnou.
- **Dejte si pozor na:** Přepisování stylů uživatelského agenta. Některé prohlížeče aplikují výchozí `font-weight: bold` na tagy `<strong>`; vyhněte se jejich kombinaci s ručním stylingem, pokud to není zamýšlené.
- **Poznámka k výkonu:** Změny inline stylů jsou levné, ale pokud plánujete stylovat desítky elementů, seskupte je do jediného volání skriptu, aby se snížil počet round‑tripů.

---

## Závěr

Pokrývali jsme vše, co potřebujete vědět o **tom, jak tučnit nadpis** a **jak použít kurzívu**, plus trik, jak **použít tučné a kurzívu** dohromady a **nastavit tloušťku písma nadpisu** programově z C#. Použitím malé HTML stránky, hostitele WinForms WebView2 a několika volání `ExecuteScriptAsync`, 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}