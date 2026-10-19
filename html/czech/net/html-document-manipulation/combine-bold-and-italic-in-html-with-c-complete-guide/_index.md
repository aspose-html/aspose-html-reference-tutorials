---
category: general
date: 2026-04-01
description: Kombinujte tučný a kurzívní text v HTML pomocí C#. Naučte se, jak upravit
  styl písma v HTML, uložit upravené HTML a změnit styl písma v C# během několika
  jednoduchých kroků.
draft: false
keywords:
- combine bold and italic
- save modified html
- modify html font style
- change font style c#
language: cs
og_description: Kombinujte tučný a kurzívní text v HTML pomocí C#. Tento průvodce
  ukazuje, jak upravit styl písma v HTML, uložit upravené HTML a rychle změnit styl
  písma v C#.
og_title: Kombinujte tučný a kurzívní text v HTML pomocí C# – krok za krokem
tags:
- C#
- Aspose.Html
- HTML manipulation
title: Kombinace tučného a kurzívy v HTML pomocí C# – Kompletní průvodce
url: /cs/net/html-document-manipulation/combine-bold-and-italic-in-html-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kombinace tučného a kurzívního textu v HTML s C# – Kompletní průvodce

Už jste někdy potřebovali **zkombinovat tučný a kurzívní** text v HTML úryvku, ale nebyli jste si jisti, jak to udělat programově? Nejste v tom sami — mnoho vývojářů narazí na tento problém při generování dynamických e‑mailů nebo reportů. Dobrou zprávou je, že s několika řádky C# a knihovnou Aspose.HTML můžete aplikovat kombinovaný styl tučné‑a‑kurzívní písmo na libovolný dokument a následně **uložit upravené HTML** pro pozdější použití.

V tomto tutoriálu projdeme celý proces: načtení malého HTML fragmentu, **úpravu stylu písma v HTML**, aplikaci efektu **kombinace tučného a kurzívního**, a nakonec **uložení upraveného HTML** na disk. Na konci budete přesně vědět, jak **změnit styl písma v C#** — bez zbytečného prohrabávání se v nejasné dokumentaci.

## Co budete potřebovat

- .NET 6 nebo novější (kód funguje i na .NET Core)  
- Aspose.HTML pro .NET — můžete jej získat z NuGet (`Install-Package Aspose.HTML`)  
- Textový editor nebo IDE (Visual Studio, VS Code, Rider — co vám vyhovuje)  

Žádné další závislosti. Pokud už máte projekt, stačí přidat NuGet balíček a můžete začít.

![Screenshot showing combined bold and italic text in a browser – combine bold and italic](https://example.com/combine-bold-italic.png)

*Alternativní text obrázku: kombinace tučného a kurzívního*

## Krok 1: Načtení HTML úryvku a vytvoření dokumentu

Nejprve potřebujeme objekt `Aspose.Html.Document`, který představuje HTML, se kterým chceme pracovat. Níže uvedený úryvek načte malý fragment obsahující značky `<b>` a `<i>`.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;

// The raw HTML we’ll transform
string htmlContent = "<html><body><b>Bold</b> <i>Italic</i></body></html>";

// Create a Document instance from the string
Document document = new Document(htmlContent);
```

**Proč je to důležité:**  
Vytvoření `Document` vám poskytne plnohodnotný model podobný DOM, takže můžete manipulovat se styly přesně tak, jako by to dělal prohlížeč. Navíc připraví objekt na pozdější uložení, což je nezbytné, když chcete **uložit upravené HTML**.

## Krok 2: Kombinace tučného a kurzívního stylu písma

Nyní přichází jádro tutoriálu — aplikace stylu, který je najednou tučný **i** kurzívní. Aspose.HTML poskytuje výčtový typ `WebFontStyle` a člen `BoldItalic` je zkratkou pro `FontStyle.Bold | FontStyle.Italic`.

```csharp
// Retrieve the default viewport style (covers the whole document)
var defaultStyle = document.DefaultViewPort.Style;

// Apply the combined bold‑and‑italic style
defaultStyle.FontStyle = WebFontStyle.BoldItalic; // same as FontStyle.Bold | FontStyle.Italic
```

**Vysvětlení:**  
`DefaultViewPort.Style` je globální CSS pravidlo, které ovlivňuje každý prvek, pokud není přepsáno. Nastavením `FontStyle` na `BoldItalic` zajistíme, že **úprava stylu písma v HTML** bude aplikována jednotně, aniž bychom museli zasahovat do každé značky `<b>` nebo `<i>` zvlášť.

> *Tip:* Pokud chcete, aby byl tučný ‑ kurzívní styl aplikován jen na určité elementy, vyberte je pomocí `document.QuerySelectorAll("p.special")` a nastavením stylu na každý uzel místo globálního viewportu.

## Krok 3: Ověření změny (volitelné, ale užitečné)

Než něco zapíšete na disk, je dobré se podívat na výsledný markup. Můžete vypsat HTML do konzole nebo debug okna:

```csharp
// Output the transformed HTML for quick verification
string transformedHtml = document.ToString();
Console.WriteLine(transformedHtml);
```

Měli byste vidět blok `<style>` vložený do `<head>`, který vynutí, aby celé tělo renderovalo s `font-weight: bold; font-style: italic;`. Tím se potvrzuje, že operace **kombinace tučného a kurzívního** byla úspěšná.

## Krok 4: Uložení upraveného HTML

Nakonec uložíme aktualizovaný dokument. Metoda `Save` automaticky zapíše dobře formovaný HTML soubor a zachová všechny externí zdroje, které jste mohli přidat.

```csharp
// Choose an output path that makes sense for your project
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.html");

// Save the document – this is the “save modified html” step
document.Save(outputPath);
Console.WriteLine($"Modified HTML saved to: {outputPath}");
```

**Co získáte:**  
Soubor `output.html`, který po otevření v libovolném prohlížeči zobrazí původní text **jak tučný, tak kurzívní**. To je konkrétní výsledek **změny stylu písma v C#** pomocí Aspose.HTML.

## Krok 5: Běžné varianty a okrajové případy

### a) Cílení jen na konkrétní elementy

Pokud potřebujete **upravit styl písma v HTML** jen pro podmnožinu — například všechny odstavce s třídou `highlight` — použijte selektor:

```csharp
var highlights = document.QuerySelectorAll("p.highlight");
foreach (var node in highlights)
{
    node.Style.FontStyle = WebFontStyle.BoldItalic;
}
```

### b) Zachování původních značek `<b>` / `<i>`

Někdy chcete zachovat původní značky pro sémantiku, ale stále aplikovat kombinovaný styl. V takovém případě přidejte CSS třídu místo přepisování globálního stylu:

```csharp
// Add a CSS class to the head
var style = document.CreateElement("style");
style.InnerHtml = ".bold-italic { font-weight: bold; font-style: italic; }";
document.Head.AppendChild(style);

// Apply the class to the body (or any element you like)
document.Body.ClassName = "bold-italic";
```

### c) Uložení s jiným kódováním

Aspose.HTML standardně používá UTF‑8, ale můžete specifikovat jiné kódování, pokud to vyžaduje váš downstream systém:

```csharp
var saveOptions = new HtmlSaveOptions()
{
    Encoding = System.Text.Encoding.ASCII // or any other Encoding
};
document.Save("output-ascii.html", saveOptions);
```

## Kompletní funkční příklad

Když spojíme vše dohromady, získáte samostatný program, který můžete zkopírovat a vložit do konzolové aplikace:

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the HTML snippet
        string htmlContent = "<html><body><b>Bold</b> <i>Italic</i></body></html>";
        Document document = new Document(htmlContent);

        // 2️⃣ Apply combined bold‑and‑italic style
        var defaultStyle = document.DefaultViewPort.Style;
        defaultStyle.FontStyle = WebFontStyle.BoldItalic; // combine bold and italic

        // 3️⃣ (Optional) Verify by printing to console
        Console.WriteLine("Transformed HTML:");
        Console.WriteLine(document.ToString());

        // 4️⃣ Save the modified HTML
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.html");
        document.Save(outputPath);
        Console.WriteLine($"✅ Modified HTML saved to: {outputPath}");
    }
}
```

**Očekávaný výstup:**  
Po otevření `output.html` v prohlížeči uvidíte slova „Bold Italic“ zobrazená **jak tučně, tak kurzívně**. Konzole také vypíše vygenerované HTML, kde je vidět `<style>` tag vynucující kombinovaný styl.

## Závěr

Nyní víte, jak **kombinovat tučný a kurzívní** text v HTML dokumentu pomocí C#. Načtením HTML do `Aspose.Html.Document`, nastavením `WebFontStyle.BoldItalic` na výchozí viewport a následným **uložením upraveného HTML** máte čisté, opakovatelné řešení pro jakýkoli automatizační úkol. Ať už potřebujete **upravit styl písma v HTML** globálně, cílit na konkrétní uzly, nebo **změnit styl písma v C#** pro web‑mail šablonu, platí stejná pravidla.

Co dál? Vyzkoušejte další hodnoty `WebFontStyle` — `Underline`, `StrikeThrough` nebo vlastní CSS třídy — a rozšiřte tak svůj stylovací nástrojový set. Můžete také prozkoumat funkce Aspose.HTML pro práci s obrázky nebo konverzi do PDF, abyste ze stejného stylovaného dokumentu během okamžiku vytvořili PDF.

Máte otázky nebo obtížný okrajový případ? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}