---
title: Uložení dokumentu v .NET pomocí Aspose.HTML
linktitle: Uložení dokumentu v .NET
second_title: Aspose.HTML .NET API pro manipulaci s HTML
description: Odemkněte sílu Aspose.HTML pro .NET pomocí našeho podrobného průvodce. Naučte se vytvářet, manipulovat a převádět dokumenty HTML a SVG
type: docs
weight: 16
url: /cs/net/html-document-manipulation/saving-a-document/
---

V dnešní digitální době je vytváření a manipulace s dokumenty HTML a SVG zásadní pro mnoho softwarových vývojářů a firem. Aspose.HTML for .NET je výkonná knihovna, která tyto úkoly zjednodušuje a nabízí různé funkce pro práci s HTML, SVG a dalšími. V tomto obsáhlém průvodci se ponoříme do základů Aspose.HTML pro .NET a rozdělíme každý příklad do snadno srozumitelných kroků. Ať už jste zkušený vývojář nebo teprve začínáte, tento průvodce je pro vás neocenitelným pomocníkem při využití možností Aspose.HTML.

## Předpoklady

Než se vydáme na tuto cestu, ujistěte se, že máte vše, co potřebujete:

- Vývojové prostředí: Ujistěte se, že máte v počítači nainstalované Visual Studio nebo jiné vývojové prostředí .NET.

- Aspose.HTML for .NET: Potřebujete získat knihovnu Aspose.HTML for .NET. Můžete si jej stáhnout z[tady](https://releases.aspose.com/html/net/).

- Znalost C#: Znalost programovacího jazyka C# je výhodou, ale není podmínkou. Tato příručka je navržena tak, aby byla vhodná pro začátečníky.

## Import jmenného prostoru

Chcete-li začít používat Aspose.HTML pro .NET, budete muset do svého projektu importovat potřebné jmenné prostory. Do kódu C# zahrňte následující jmenný prostor:

### Krok 1: Import jmenného prostoru Aspose.HTML
```csharp
using Aspose.Html;
```

Tento jmenný prostor vám umožní přístup k různým možnostem manipulace s HTML a SVG.

## HTML do souboru

### Krok 1: Inicializujte prázdný dokument HTML
```csharp
// Inicializujte prázdný dokument HTML.
using (var document = new Aspose.Html.HTMLDocument())
{
    // Vytvořte textový prvek a přidejte jej do dokumentu
    var text = document.CreateTextNode("Hello World!");
    document.Body.AppendChild(text);
    // Uložte HTML do souboru na disk.
    document.Save("document.html");
}
```

V tomto příkladu vytvoříme dokument HTML a přidáme jednoduché "Ahoj světe!" text k tomu. HTML pak uložíme do souboru na disk.

## HTML bez propojeného souboru

### Krok 1: Připravte jednoduchý soubor HTML
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Zde vytvoříme základní HTML soubor s kotvícím odkazem na jiný soubor.

### Krok 2: Načtěte 'document.html' do paměti
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Vytvořit instanci Možnosti uložení
    var options = new Aspose.Html.Saving.HTMLSaveOptions();
    //Chcete-li oříznout propojené soubory HTML, nastavte maximální hloubku zpracování na 0.
    options.ResourceHandlingOptions.MaxHandlingDepth = 0;
    // Uložte dokument
    document.Save(@".\html-to-file-example\document.html", options);
}
```

V tomto příkladu načteme dokument HTML do paměti, nastavíme maximální hloubku zpracování pro oříznutí propojených souborů a dokument uložíme. 

## HTML na MHTML

### Krok 1: Připravte jednoduchý soubor HTML
```csharp
System.IO.File.WriteAllText("document.html", "<p>Hello World!</p>" +
                                             "<a href='linked.html'>linked file</a>");
```

Stejně jako v příkladu 2 vytvoříme základní HTML soubor s kotvícím odkazem na jiný soubor.

### Krok 2: Načtěte 'document.html' do paměti a uložte jako MHTML
```csharp
using (var document = new Aspose.Html.HTMLDocument("document.html"))
{
    // Uložte dokument jako MHTML
    document.Save(@".\html-to-file-example\document.mht", Aspose.Html.Saving.HTMLSaveFormat.MHTML);
}
```

Zde načteme HTML dokument do paměti a uložíme jej ve formátu MHTML.

## HTML do Markdown

### Krok 1: Připravte HTML kód
```csharp
var html_code = "<H2>Hello World!</H2>";
```

 V tomto kroku definujeme fragment kódu HTML obsahující`<H2>` živel.

### Krok 2: Inicializujte dokument z kódu HTML a uložte jej jako Markdown
```csharp
using (var document = new Aspose.Html.HTMLDocument(html_code, "."))
{
    // Uložte dokument jako soubor Markdown.
    document.Save("document.md", Aspose.Html.Saving.HTMLSaveFormat.Markdown);
}
```

Z fragmentu kódu vytvoříme dokument HTML a uložíme jej jako soubor Markdown.

## SVG do souboru

### Krok 1: Připravte si SVG kód
```csharp
var code = @"
    <svg xmlns='http://www.w3.org/2000/svg' height='80' width='300'>
        <g fill='none'>
            <path stroke='red' d='M5 20 l215 0' />
            <path stroke='black' d='M5 40 l215 0' />
            <path stroke='blue' d='M5 60 l215 0' />
        </g>
    </svg>";
```

Zde vytvoříme kód SVG, který vykreslí jednoduchou barevnou grafiku.

### Krok 2: Inicializujte dokument SVG z kódu a uložte na disk
```csharp
using (var document = new Aspose.Html.Dom.Svg.SVGDocument(code, "."))
{
    // Uložte soubor SVG na disk
    document.Save("document.svg");
}
```

V tomto kroku vytvoříme z kódu dokument SVG a uložíme jej jako soubor SVG.

## Závěr

Aspose.HTML for .NET je všestranná knihovna, která zjednodušuje práci s dokumenty HTML a SVG ve vašich aplikacích .NET. V této příručce jsme probrali pět základních příkladů a každý rozdělili do podrobných pokynů. Ať už vytváříte, manipulujete nebo převádíte dokumenty, Aspose.HTML vás pokryje. Dodržováním těchto kroků jste na dobré cestě k ovládnutí tohoto mocného nástroje.

## FAQ

### Q1: Co je Aspose.HTML pro .NET?

Odpověď 1: Aspose.HTML for .NET je knihovna .NET, která poskytuje širokou škálu funkcí pro práci s dokumenty HTML a SVG, včetně vytváření, manipulace a převodu.

### Q2: Kde mohu stáhnout Aspose.HTML pro .NET?

 A2: Aspose.HTML pro .NET si můžete stáhnout z[tady](https://releases.aspose.com/html/net/).

### Q3: Je Aspose.HTML pro .NET vhodný pro začátečníky?

A3: Ano, Aspose.HTML pro .NET mohou používat začátečníci i zkušení vývojáři. Příklady v této příručce jsou navrženy tak, aby byly vhodné pro začátečníky.

### Q4: Mohu převést HTML do jiných formátů pomocí Aspose.HTML pro .NET?

Odpověď 4: Ano, Aspose.HTML for .NET podporuje převod do různých formátů, včetně MHTML a Markdown, jak je znázorněno v příkladech.

### Q5: Kde mohu získat podporu pro Aspose.HTML pro .NET?

 Odpověď 5: Podporu a odpovědi na své otázky můžete najít na fóru komunity Aspose.HTML[tady](https://forum.aspose.com/).