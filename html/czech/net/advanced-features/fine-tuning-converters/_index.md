---
title: Jemné ladění konvertorů v .NET pomocí Aspose.HTML
linktitle: Jemné ladění převodníků v .NET
second_title: Aspose.HTML .NET API pro manipulaci s HTML
description: Naučte se převádět HTML do PDF, XPS a obrázků pomocí Aspose.HTML pro .NET. Výukový program krok za krokem s příklady kódu a často kladenými dotazy.
weight: 16
url: /cs/net/advanced-features/fine-tuning-converters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jemné ladění konvertorů v .NET pomocí Aspose.HTML


## Zavedení

Aspose.HTML for .NET je výkonná knihovna, která umožňuje vývojářům manipulovat a převádět HTML dokumenty v různých formátech. Ať už potřebujete převést HTML na PDF, XPS nebo obrázky nebo provádět jiné úkoly související s HTML, Aspose.HTML poskytuje robustní sadu nástrojů, které vám pomohou dokončit práci.

tomto tutoriálu prozkoumáme některé základní funkce Aspose.HTML pro .NET a poskytneme vysvětlení krok za krokem pro každý příklad. Na konci tohoto tutoriálu budete dobře rozumět tomu, jak používat Aspose.HTML pro .NET ve vašich aplikacích .NET.

## Předpoklady

Než se vrhneme na příklady, ujistěte se, že máte splněny následující předpoklady:

-  Aspose.HTML for .NET: Měli byste mít nainstalovanou knihovnu Aspose.HTML for .NET. Můžete si jej stáhnout z[odkaz ke stažení](https://releases.aspose.com/html/net/).

-  Dočasná licence (volitelné): Pokud nemáte platnou licenci, můžete získat dočasnou licenci od[zde](https://purchase.aspose.com/temporary-license/).

Nyní se podívejme na některé běžné případy použití s Aspose.HTML pro .NET.

## Importovat jmenné prostory

V kódu C# začněte importováním potřebných jmenných prostorů:

```csharp
using Aspose.Html;
using Aspose.Html.Rendering.Pdf;
using Aspose.Html.Rendering.Image;
using Aspose.Html.Rendering.Xps;
using Aspose.Html.Rendering.Pdf.Encryption;
using Aspose.Html.Drawing;
```

## Převést HTML do PDF

### Krok 1: Připravte HTML kód

```csharp
var code = @"<span>Hello World!!</span>";
```

### Krok 2: Inicializujte dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Vytvořte zařízení PDF a zadejte výstupní soubor

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Krok 4: Vykreslení HTML do PDF

```csharp
document.RenderTo(device);
```

Tento příklad převede úryvek HTML na dokument PDF. HTML kód a výstupní soubor můžete přizpůsobit podle potřeby.

## Nastavte vlastní velikost stránky

### Krok 1: Připravte HTML kód

```csharp
var code = @"<span>Hello World!!</span>";
```

### Krok 2: Inicializujte dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Vytvořte možnosti vykreslování PDF

```csharp
var options = new PdfRenderingOptions()
{
    PageSetup =
    {
        AnyPage = new Page(
            new Size(
                Length.FromInches(5),
                Length.FromInches(2)))
    }
};
```

### Krok 4: Vytvořte zařízení PDF a zadejte možnosti a výstupní soubor

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Vykreslení HTML do PDF

```csharp
document.RenderTo(device);
```

Tento příklad ukazuje, jak nastavit vlastní velikost stránky pro výsledný dokument PDF.

## Upravit rozlišení

### Krok 1: Připravte HTML kód a uložte do souboru

```csharp
var code = @"
    <style>
    p
    { 
        background: blue; 
    }
    @media(min-resolution: 300dpi)
    {
        p 
        { 
            /* high-resolution screen color */
            background: green
        }
    }
    </style>
    <p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Krok 2: Inicializujte dokument HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Krok 3: Vytvořte možnosti vykreslování PDF pro nízké rozlišení

```csharp
var options = new PdfRenderingOptions()
{
    HorizontalResolution = 50,
    VerticalResolution = 50
};
```

### Krok 4: Vytvořte zařízení PDF a zadejte možnosti a výstupní soubor pro nízké rozlišení

```csharp
using (var device = new PdfDevice(options, "output_resolution_50.pdf"))
```

### Krok 5: Vykreslení HTML do PDF pro nízké rozlišení

```csharp
document.RenderTo(device);
```

### Krok 6: Vytvořte možnosti vykreslování PDF pro vysoké rozlišení

```csharp
options = new PdfRenderingOptions()
{
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

### Krok 7: Vytvořte zařízení PDF a zadejte možnosti a výstupní soubor pro vysoké rozlišení

```csharp
using (var device = new PdfDevice(options, "output_resolution_300.pdf"))
```

### Krok 8: Vykreslení HTML do PDF pro vysoké rozlišení

```csharp
document.RenderTo(device);
```

Tento příklad ukazuje, jak upravit rozlišení při vykreslování HTML do PDF s ohledem na obrazovky s nízkým i vysokým rozlišením.

## Určete barvu pozadí

### Krok 1: Připravte HTML kód a uložte do souboru

```csharp
var code = @"<p>Hello World!!</p>";
System.IO.File.WriteAllText("document.html", code);
```

### Krok 2: Inicializujte dokument HTML

```csharp
using (var document = new HTMLDocument("document.html"))
```

### Krok 3: Inicializujte možnosti vykreslování PDF pomocí barvy pozadí

```csharp
var options = new PdfRenderingOptions()
{
    BackgroundColor = System.Drawing.Color.Cyan
};
```

### Krok 4: Vytvořte zařízení PDF a zadejte možnosti a výstupní soubor

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Vykreslení HTML do PDF

```csharp
document.RenderTo(device);
```

Tento příklad ukazuje, jak určit barvu pozadí při převodu HTML do PDF.

## Nastavte velikost levé a pravé stránky

### Krok 1: Připravte HTML kód

```csharp
var code = @"<style>div { page-break-after: always; }</style>
    <div>First Page</div>
    <div>Second Page</div>
    <div>Third Page</div>
    <div>Fourth Page</div>";
```

### Krok 2: Inicializujte dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Vytvořte možnosti vykreslování PDF s velikostí levé a pravé stránky

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.SetLeftRightPage(
    new Page(new Size(400, 200)),
    new Page(new Size(400, 100))
);
```

### Krok 4: Vytvořte zařízení PDF a zadejte možnosti a výstupní soubor

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Vykreslení HTML do PDF

```csharp
document.RenderTo(device);
```

Tento příklad ukazuje, jak nastavit různé velikosti stránek pro levou a pravou stránku při převodu HTML do PDF.

## Upravte velikost stránky podle obsahu

### Krok 1: Připravte HTML kód

```csharp
var code = @"<style>
    div { page-break-after: always; }
</style>
<div style='border: 1px solid red; width: 400px'>First Page</div>
<div style='border: 1px solid red; width: 600px'>Second Page</div>";
```

### Krok 2: Inicializujte dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Vytvořte možnosti vykreslování PDF

```csharp
var options = new PdfRenderingOptions();
options.PageSetup.AnyPage = new Page(new Size(500, 200));
options.PageSetup.AdjustToWidestPage = true;
```

### Krok 4: Vytvořte zařízení PDF a zadejte možnosti a výstupní soubor

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Vykreslení HTML do PDF

```csharp
document.RenderTo(device);
```

Tento příklad ukazuje, jak upravit velikost stránky na nejširší obsah při převodu HTML do PDF.

## Zadejte oprávnění PDF

### Krok 1: Připravte HTML kód

```csharp
var code = @"<div>Hello World!!</div>";
```

### Krok 2: Inicializujte dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Vytvořte možnosti vykreslování PDF s oprávněními

```csharp
var options = new PdfRenderingOptions();
options.Encryption = new PdfEncryptionInfo(
    "user_pwd",
    "owner_pwd",
    PdfPermissions.PrintDocument,
    PdfEncryptionAlgorithm.RC4_128
);
```

### Krok 4: Vytvořte zařízení PDF a zadejte možnosti a výstupní soubor

```csharp
using (var device = new PdfDevice(options, "output.pdf"))
```

### Krok 5: Vykreslení HTML do PDF

```csharp
document.RenderTo(device);
```

Tento příklad ukazuje, jak určit oprávnění a šifrování při převodu HTML do chráněného PDF.

## Zadejte možnosti specifické pro obrázek

### Krok 1: Připravte HTML kód

```csharp
var code = @"<div>Hello World!!</div>";
```

### Krok 2: Inicializujte dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Vytvořte možnosti vykreslování obrázků

```csharp
var options = new ImageRenderingOptions()
{
    Format = ImageFormat.Jpeg,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.None,
    VerticalResolution = Resolution.FromDotsPerInch(75),
    HorizontalResolution = Resolution.FromDotsPerInch(75),
};
```

### Krok 4: Vytvořte obrazové zařízení a zadejte možnosti a výstupní soubor

```csharp
using (var device = new ImageDevice(options, "output.jpg"))
```

### Krok 5: Vykreslení HTML na obrázek

```csharp
document.RenderTo(device);
```

Tento příklad ukazuje, jak převést HTML na obrázek se specifickými možnostmi vykreslování, jako je formát, rozlišení a režim vyhlazování.

## Zadejte možnosti vykreslování XPS

### Krok 1: Připravte HTML kód

```csharp
var code = @"<span>Hello World!!</span>";
```

### Krok 2: Inicializujte dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Vytvořte možnosti vykreslování XPS s velikostí stránky

```csharp
var options = new XpsRenderingOptions();
options.PageSetup.AnyPage = new Page(
    new Size(
        Length.FromInches(5),
        Length.FromInches(2)
    )
);
```

### Krok 4: Vytvořte zařízení XPS a zadejte možnosti a výstupní soubor

```csharp
using (var device = new XpsDevice(options, "output.xps"))
```

### Krok 5: Vykreslení HTML do XPS

```csharp
document.RenderTo(device);
```

Tento příklad ukazuje, jak převést HTML na XPS s vlastní velikostí stránky a možnostmi vykreslování.

## Kombinujte více dokumentů HTML do PDF

### Krok 1: Připravte HTML kód pro více dokumentů

```csharp
var code1 = @"<br><span style='color: green'>Hello World!!</span>";
var code2 = @"<br><span style='color: blue'>Hello World!!</span>";
var code3 = @"<br><span style='color: red'>Hello World!!</span>";
```

### Krok 2: Vytvořte dokumenty HTML ke sloučení

```csharp
using (var document1 = new HTMLDocument(code1, "."))
using (var document2 = new HTMLDocument(code2, "."))
using (var document3 = new HTMLDocument(code3, "."))
```

### Krok 3: Inicializujte HTML Renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Krok 4: Vytvořte zařízení PDF pro sloučený výstup

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Krok 5: Sloučení HTML dokumentů do PDF

```csharp
renderer.Render(device, document1, document2, document3);
```

Tento příklad ukazuje, jak zkombinovat více dokumentů HTML do jednoho souboru PDF pomocí Aspose.HTML for .NET.

## Nastavte časový limit vykreslování

### Krok 1: Připravte HTML kód pomocí JavaScriptu

```csharp
var code = @"
    <script>
        var count = 0;
        setInterval(function()
        {
            var element = document.createElement('div');
            var message = (++count) + '. ' + 'Hello World!!';
            var text = document.createTextNode(message);
            element.appendChild(text);
            document.body.appendChild(element);
        }, 1000);
    </script>";
```

### Krok 2: Inicializujte dokument HTML

```csharp
using (var document = new HTMLDocument(code, "."))
```

### Krok 3: Inicializujte HTML Renderer

```csharp
using (HTMLRenderer renderer = new HTMLRenderer())
```

### Krok 4: Vytvořte zařízení PDF a nastavte časový limit vykreslování

```csharp
using (var device = new PdfDevice("output.pdf"))
```

### Krok 5: Vykreslení HTML do PDF s časovým limitem

```csharp
renderer.Render(device, TimeSpan.FromSeconds(5), document);
```

Tento příklad ukazuje, jak nastavit časový limit vykreslování při převodu HTML do PDF, což může být užitečné při práci s dynamickým obsahem nebo dlouho běžícími skripty.

## Závěr

Aspose.HTML for .NET je všestranná knihovna, která umožňuje vývojářům efektivně pracovat s dokumenty HTML. V tomto tutoriálu jsme probrali různé příklady, od základních převodů HTML do PDF až po pokročilejší funkce, jako jsou vlastní velikosti stránek, rozlišení a oprávnění. Podle těchto příkladů můžete využít plný potenciál Aspose.HTML pro .NET ve svých aplikacích .NET.

 Pokud máte nějaké dotazy nebo potřebujete další pomoc, neváhejte a navštivte[Fórum Aspose.HTML](https://forum.aspose.com/) za podporu a vedení.

## FAQ

### Q1. Co je Aspose.HTML pro .NET?
   
A1: Aspose.HTML for .NET je knihovna .NET, která umožňuje vývojářům manipulovat a převádět dokumenty HTML programově. Nabízí širokou škálu funkcí pro práci s obsahem HTML, včetně HTML do PDF, XPS a převodu obrázků, stejně jako pokročilé možnosti vykreslování.

### Q2. Kde si mohu stáhnout Aspose.HTML pro .NET?

 A2: Aspose.HTML pro .NET si můžete stáhnout z[odkaz ke stažení](https://releases.aspose.com/html/net/).

### Q3. Potřebuji licenci k používání Aspose.HTML pro .NET?

Odpověď 3: Aspose.HTML pro .NET můžete používat bez licence, ale pro odemknutí všech funkcí a odstranění všech vodoznaků nebo omezení se doporučuje získat licenci pro produkční použití.

### Q4. Jak mohu chránit své soubory PDF generované pomocí Aspose.HTML pro .NET?

Odpověď 4: Při vykreslování HTML do PDF pomocí Aspose.HTML for .NET můžete zadat oprávnění PDF a nastavení šifrování. To vám umožňuje řídit, kdo může přistupovat k výsledným souborům PDF a upravovat je.

### Q5. Mohu převést HTML do jiných formátů, jako je XPS nebo obrázky?

Odpověď 5: Ano, Aspose.HTML for .NET podporuje převod HTML do různých formátů, včetně PDF, XPS a obrázků (např. JPEG). Nastavení převodu můžete upravit tak, aby vyhovovalo vašim konkrétním požadavkům.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
