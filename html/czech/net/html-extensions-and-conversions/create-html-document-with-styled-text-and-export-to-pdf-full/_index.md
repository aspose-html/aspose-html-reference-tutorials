---
category: general
date: 2025-12-29
description: Vytvořte HTML dokument v C# a naučte se nastavit rodinu písma, velikost
  písma, poté uložte HTML jako PDF nebo převeďte HTML na PDF pomocí Aspose.HTML.
draft: false
keywords:
- create html document
- set font family
- set font size
- save html as pdf
- convert html to pdf
language: cs
og_description: Vytvořte HTML dokument v C# a okamžitě zjistěte, jak nastavit rodinu
  písma, velikost písma, poté uložte HTML jako PDF nebo převádějte HTML do PDF pomocí
  Aspose.HTML.
og_title: Vytvořit HTML dokument – stylovaný text a export do PDF
tags:
- aspnet
- csharp
- pdf-generation
title: Vytvořte HTML dokument se stylovaným textem a exportujte do PDF – kompletní
  průvodce
url: /cs/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření HTML dokumentu se stylovaným textem a export do PDF

Už jste někdy potřebovali **vytvořit HTML dokument** za běhu a převést jej do PDF, aniž byste opustili svůj C# kód? Možná budujete reporting engine, generátor faktur nebo jen rychlý náhled pro uživatele. Dobrá zpráva je, že to můžete udělat v několika řádcích pomocí Aspose.HTML a získáte plnou kontrolu nad rodinou písma, velikostí písma a dokonce i tučným‑kurzivním stylováním.

V tomto tutoriálu projdeme celý proces – od vytvoření HTML dokumentu v paměti až po uložení jako PDF soubor. Na konci budete přesně vědět, jak **nastavit rodinu písma**, **nastavit velikost písma** a **uložit HTML jako PDF** (alias **převést HTML do PDF**) s čistým, připraveným k nasazení kódem.

## Co budete potřebovat

- .NET 6+ (API funguje jak s .NET Core, tak s .NET Framework)  
- NuGet balíček Aspose.HTML pro .NET (`Aspose.Html`) – nainstalujte pomocí `dotnet add package Aspose.Html`  
- Složka na disku, kam může být vygenerované PDF zapsáno  

Žádné extra HTML šablony, žádné externí konvertory, jen čistý C#.

![ilustrace vytvoření HTML dokumentu](/images/create-html-document.png){alt="příklad vytvoření HTML dokumentu"}

## Krok 1: Vytvoření HTML dokumentu

Nejprve potřebujeme prázdný objekt HTML dokumentu. Představte si ho jako čisté plátno, na které později namalujete svůj stylovaný odstavec.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;
using Aspose.Html.Saving;

// Step 1 – initialize a new HTML document in memory
HTMLDocument htmlDocument = new HTMLDocument();

// Grab a reference to the <body> element for later use
HTMLBodyElement body = htmlDocument.Body;
```

**Proč je to důležité:** `HTMLDocument` vám poskytuje strukturu podobnou DOM, kterou můžete programově manipulovat. Nemusíte se dotýkat surových řetězců nebo souborových operací až do samotného konce.

## Krok 2: Přidání odstavce a nastavení rodiny písma a velikosti písma

Nyní vytvoříme element `<p>`, vložíme do něj text a explicitně definujeme rodinu písma a velikost. Zde vstupují klíčová slova **set font family** a **set font size**.

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

**Tip:** Pokud potřebujete bezpečnou zálohu pro web, můžete zadat seznam oddělený čárkou, např. `"Arial, Helvetica, sans-serif"`; prohlížeč (nebo Aspose) vybere první dostupné písmo.

## Krok 3: Použití tučného a kurzivního stylu pomocí příznaků WebFontStyle

Aspose.HTML poskytuje užitečné enum `WebFontStyle`, které umožňuje kombinovat styly pomocí bitového OR. Uděláme text zároveň tučný **i** kurzivní.

```csharp
// Step 3 – apply bold and italic using WebFontStyle flags
paragraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

**Co se děje pod kapotou?** Vlastnost `FontStyle` se překládá na CSS deklarace `font-weight` a `font-style`. OR‑ováním příznaků se vyhneme psaní dvou samostatných řádků CSS.

## Krok 4: Převod HTML do PDF (Uložení HTML jako PDF)

Poslední krok je samotný převod. Jediným voláním `Save` Aspose.HTML vykreslí DOM a zapíše PDF soubor na disk. Tím splníme požadavky **save html as pdf** i **convert html to pdf**.

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

**Očekávaný výsledek:** Otevřete `styled.pdf` a uvidíte jediný odstavec s textem „Bold & Italic text“ v 18‑px Arial, vykreslený tučně a kurzívou. Rozměry PDF odpovídají standardnímu formátu A4 a text je výběrný – díky vektorovému vykreslení.

## Kompletní funkční příklad

Sestavením všech částí dohromady získáte kompletní, připravený program:

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

### Spuštění kódu

1. Nainstalujte NuGet balíček Aspose.HTML:  
   ```bash
   dotnet add package Aspose.Html
   ```
2. Nahraďte `C:\Temp\styled.pdf` složkou, do které máte právo zapisovat.  
3. Sestavte a spusťte: `dotnet run`.  

Měli byste vidět zprávu v konzoli potvrzující umístění souboru a PDF bude obsahovat stylovaný odstavec.

## Často kladené otázky a okrajové případy

- **Co když potřebuji vlastní webové písmo?**  
  Načtěte písmo pomocí `HTMLFontFaceRule` nebo odkažte na vzdálený `@font-face` CSS soubor před vytvořením odstavce.

- **Mohu přidat obrázky před převodem?**  
  Rozhodně. Použijte `HTMLImageElement img = (HTMLImageElement)htmlDocument.CreateElement("img");` a nastavte `img.Source` na lokální cestu nebo data URI.

- **Co s PDF o více stránkách?**  
  Přidejte více elementů (tabulky, divy atd.) a Aspose.HTML automaticky stránkuje, když obsah přesáhne výšku stránky.

- **Existuje způsob, jak ovládat metadata PDF?**  
  Předávejte instanci `PdfSaveOptions` a nastavte vlastnosti jako `Author`, `Title` nebo `PdfAConformanceLevel`.

## Shrnutí

Probrali jsme, jak **vytvořit HTML dokument** v C#, **nastavit rodinu písma**, **nastavit velikost písma**, aplikovat tučné‑kurzivní styly a nakonec **uložit HTML jako PDF** – tedy **převést HTML do PDF** pomocí Aspose.HTML. Tento úryvek je dostatečně stručný, aby šel vložit do jakéhokoli .NET projektu, a zároveň kompletní, aby sloužil jako pevný základ pro složitější reportingové scénáře.

## Další kroky

- Experimentujte s CSS třídami pro opakovaně použitelné styly.  
- Kombinujte více odstavců, tabulek a obrázků pro bohatší PDF dokumenty.  
- Prozkoumejte PDF/A kompatibilitu, pokud potřebujete archivní úroveň dokumentů.  

Klidně upravujte písmo, velikost nebo barvy – neexistuje žádný limit, co můžete programově generovat. Šťastné kódování a ať se vaše PDF vždy vykreslí přesně tak, jak si představujete!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}