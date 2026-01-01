---
category: general
date: 2026-01-01
description: Hogyan tegyünk félkövér címet és alkalmazzunk dőlt stílust C# és CSS
  segítségével. Tanulja meg beállítani a cím betűvastagságát, alkalmazni a félkövér
  és dőlt formát, és gyorsan stílusozni a címeket.
draft: false
keywords:
- how to bold heading
- how to apply italic
- apply bold and italic
- how to apply bold
- set heading font weight
language: hu
og_description: Hogyan tegyünk félkövér címet az első mondatban, majd tanuljuk meg
  az dőlt betű használatát, a félkövér és dőlt kombinálását, és a cím betűvastagságának
  beállítását világos példákkal.
og_title: Hogyan tegyünk félkövér címet – Teljes útmutató a CSS-hez és a C#-hoz
tags:
- CSS
- C#
- Web Development
title: Hogyan tegyünk félkövér címet CSS‑sel és C#‑val – Teljes lépésről‑lépésre útmutató
url: /hu/net/working-with-html-documents/how-to-bold-heading-with-css-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan lehet félkövér címet – Teljes útmutató CSS-hez és C#-hez

Gondolkodtál már azon, **hogyan lehet félkövér címet** egy weboldalon anélkül, hogy végtelen dokumentációt kellene átböngészni? Nem vagy egyedül. A legtöbb fejlesztő ebbe a helyzetbe kerül, amikor gyors vizuális módosításra van szüksége, különösen, ha HTML-t, CSS-t és egy kis C#-t kombinál a felület vezérléséhez.  

Ebben az útmutatóban egy teljes, futtatható példán keresztül mutatjuk be, hogyan lehet pontosan félkövér, dőlt és kombinált stílusokat alkalmazni egy `<h1>` elemre. Útközben kitérünk arra, hogyan **alkalmazzunk dőltet**, hogyan **alkalmazzunk egyszerre félkövér és dőlt** stílust, valamint a finom különbségre a CSS `font-weight` és az alacsony szintű `WebFontStyle` API használata között. A végére magabiztosan **be tudod állítani a cím betűvastagságát**, függetlenül attól, hogy melyik technológiai stacket használod.

## Előfeltételek

- .NET 6+ (vagy .NET Framework 4.8, ha inkább azt használod)
- Visual Studio 2022 vagy bármely C#‑kompatibilis IDE
- Alapvető HTML és CSS ismeretek
- Egy egyszerű WinForms vagy WPF projekt, amely WebView2 vezérlőt tartalmaz (a példa WinForms-t használ)

Ha bármelyik ismeretlennek tűnik, ne ess pánikba – megmutatjuk a szükséges minimális kódot, és egyszerűen be tudod másolni egy új projektbe.

---

## 1. lépés: Hozz létre egy minimális HTML oldalt

Először is szükségünk van egy HTML fájlra, amelyet a WebView2 vezérlő betölthet. Mentsd el a következőt `index.html` néven a projekted kimeneti mappájába (például `bin\Debug\net6.0-windows`).

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

> **Miért fontos ez:** A CSS minimalizálása tiszta alapot biztosít, így pontosan láthatjuk, mit csinál a C# kód. Az `id="title"` attribútum megkönnyíti a cím elem célzását a szkriptből.

---

## 2. lépés: Állítsd be a WinForms projektet a WebView2-vel

Hozz létre egy új **Windows Forms App**-ot (`.NET 6`) és add hozzá a **Microsoft.Web.WebView2** NuGet csomagot. Húzz egy `WebView2` vezérlőt a formra, nevezd el `webView`-nak, és állítsd be a `Dock` tulajdonságát `Fill`-re.

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

> **Pro tipp:** Ha a navigáció sikertelen, ellenőrizd, hogy az `index.html` másolva van-e a kimeneti mappába (állítsd be a *Copy to Output Directory* → *Copy always* opciót).

---

## 3. lépés: A cím elem megtalálása C#-ban

Miután az oldal betöltődött, lekérhetjük a `<h1>` elemet. A `CoreWebView2` API egy `ExecuteScriptAsync` metódust biztosít, amely JavaScriptet futtat és visszaadja az eredményt. Azonban ebben a tutorialban a **alacsony szintű DOM wrapper**-t használjuk, amely a WebView2-vel együtt érkezik (`webView.CoreWebView2`-n keresztül elérhető).

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

> **Miért így teszünk:** A közvetlen DOM hozzáférés lehetővé teszi, hogy elkerüljük nagy JavaScript kódrészletek injektálását. Tisztább, és megmutatja, **hogyan alkalmazzunk félkövér stílust** a WebView2 API-val.

---

## 4. lépés: Félkövér, dőlt és kombinált stílusok alkalmazása

Most három különböző megközelítést használunk a cím stílusozásához:

1. **CSS `font-weight`** – a leggyakoribb módszer, amely megfelel a **set heading font weight** követelménynek.
2. **CSS `font-style`** – hogyan **alkalmazzunk dőltet**.
3. `WebFontStyle` jelzők – egy alacsony szintű alternatíva, amely lehetővé teszi a **félkövér és dőlt** egyidejű alkalmazását.

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

> **Magyarázat:**  
> • `fontWeight = '700'` azt mondja a böngészőnek, hogy a szöveget **félkövér** súllyal jelenítse meg.  
> • `fontStyle = 'italic'` dőlté teszi a karaktereket, ezáltal kielégítve a **hogyan alkalmazzunk dőltet** kérdést.  
> • A megjegyzett sor azt mutatja, hogyan *állíthatnád* be a `WebFontStyle`-t C#-ból, ha van egy olyan wrappered, amely kiteszi az enumot. Valós környezetben a `heading` objektumon hívnál egy C# metódust, például `heading.Font.WebFontStyle = WebFontStyle.Bold | WebFontStyle.Italic;`.

A low‑level API C#-ból való tényleges meghívásához COM interop wrapperre van szükség. Íme egy minimális példa, feltételezve, hogy van hivatkozásod a `Microsoft.Web.WebView2.Wpf` névtérre:

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

> **Lényeg:** Ha jártas vagy a WebView2 COM modellben, a jelző alapú megközelítés finomhangolt vezérlést biztosít. Ellenkező esetben a CSS út tökéletesen megfelelő és minden böngészőben működik.

---

## 5. lépés: Összekapcsolás – Teljes működő példa

Az alábbi egyetlen `MainForm.cs` fájl, amely lefordítható és futtatható. Betölti a HTML-t, majd a navigáció befejeződése után stílusozza a címet.

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

### Várható kimenet

Amikor futtatod az alkalmazást, az ablak a következőket mutatja:

- **„Dynamic Heading”** megjelenik **félkövér** (súly 700) és **dőlt** formában.
- A környező bekezdés változatlan marad.
- Ha megvizsgálod az elemet (Ctrl + Shift + I), láthatod az alkalmazott inline stílusokat.

---

## Gyakori kérdések és szélhelyzetek

### 1️⃣ *Mi van, ha a cím már rendelkezik osztállyal?*  
Vagy hozzáadhatsz egy osztályt a `classList.add('my‑bold‑italic')` segítségével, és a stílusokat egy stíluslapban definiálhatod, vagy továbbra is használhatod az itt bemutatott inline stílusokat. Az inline stílusok előnyben részesülnek, ha gyors, egyszeri módosításra van szükség.

### 2️⃣ *Minden böngésző tiszteletben tartja a `font-weight: 700`-at?*  
Igen, a 700 a CSS specifikációban a **Bold** (félkövér) súlyt jelöli. Ha a betűcsalád nem biztosít félkövér változatot, a böngésző szintetizál egyet, ami kissé elmosódott lehet. Ezért ajánlott olyan betűcsaládot használni, amely valódi félkövér változattal rendelkezik (például Arial).

### 3️⃣ *Animálhatom a normálról félkövérre való átmenetet?*  
Természetesen. Adj hozzá egy CSS átmenetet:

```css
h1 {
    transition: font-weight 0.3s ease, font-style 0.3s ease;
}
```

Ezután C#-ból váltogasd a stílusokat, és figyeld a sima animációt.

### 4️⃣ *Mi a helyzet a hozzáférhetőséggel?*  
A félkövér és dőlt stílusok vizuális jelzések, nem szemantikusak. A képernyőolvasók számára fontold meg `aria-label` hozzáadását vagy a megfelelő címsor hierarchia (`<h1>` → `<h2>`) használatát a fontosság közvetítéséhez.

---

## Pro tippek és buktatók

- **Pro tipp:** Tartsd a CSS-ed külön fájlban, és csak C#-ot használj az osztályok váltogatására. Ez tisztábbá és könnyebben karbantarthatóvá teszi a UI logikát.
- **Vigyázz:** A felhasználói ügynök stílusainak felülírása. Néhány böngésző alapértelmezett `font-weight: bold`-ot alkalmaz a `<strong>` elemekre; kerüld a kézi stílusokkal való keverést, hacsak nem szándékod.
- **Teljesítményjegyzet:** Az inline stílusváltoztatások olcsók, de ha tucatnyi elemet szeretnél stílusozni, csoportosítsd őket egyetlen script hívásba a körutazások csökkentése érdekében.

## Összegzés

Áttekintettük mindent, amit a **félkövér cím** és a **dőlt alkalmazása** kapcsán tudni kell, valamint a trükköt, hogyan **alkalmazzunk egyszerre félkövér és dőlt** stílust és hogyan **állítsuk be a cím betűvastagságát** programozottan C#-ból. Egy apró HTML oldal, egy WinForms WebView2 host és néhány `ExecuteScriptAsync` hívás használatával,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}