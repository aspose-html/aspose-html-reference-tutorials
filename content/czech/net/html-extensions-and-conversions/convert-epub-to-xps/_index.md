---
title: Převeďte EPUB na XPS v .NET pomocí Aspose.HTML
linktitle: Převeďte EPUB na XPS v .NET
second_title: Aspose.HTML .NET API pro manipulaci s HTML
description: Přečtěte si, jak převést EPUB na XPS v .NET pomocí Aspose.HTML pro .NET. Postupujte podle našeho průvodce krok za krokem pro snadné konverze.
type: docs
weight: 13
url: /cs/net/html-extensions-and-conversions/convert-epub-to-xps/
---

Hledáte bezproblémový způsob převodu souborů EPUB do formátu XPS ve vašich aplikacích .NET? Aspose.HTML for .NET poskytuje výkonné řešení, jak toho dosáhnout bez námahy. V tomto podrobném průvodci vás provedeme procesem převodu EPUB na XPS pomocí Aspose.HTML. Začněme!

## Předpoklady

Než se ponoříte do procesu převodu EPUB na XPS, musíte se ujistit, že máte splněny následující předpoklady:

### 1. Aspose.HTML for .NET Library

 Ujistěte se, že máte v projektu nainstalovanou knihovnu Aspose.HTML for .NET. Pokud jste tak neučinili, můžete jej získat z[Aspose.HTML for .NET Download page](https://releases.aspose.com/html/net/).

### 2. Zadejte soubor EPUB

Budete potřebovat soubor EPUB, který chcete převést na XPS. Ujistěte se, že máte k dispozici soubor EPUB pro převod.

### 3. Vývojové prostředí .NET

Tato příručka předpokládá, že máte na svém počítači nastaveno funkční vývojové prostředí .NET.

## Import jmenného prostoru

Pro začátek byste měli importovat potřebný jmenný prostor pro Aspose.HTML:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.Drawing;
```

## Převést EPUB na XPS

Pojďme si proces převodu souboru EPUB do formátu XPS rozdělit do několika kroků.

### Krok 1.1: Otevřete soubor EPUB

Nejprve otevřete existující soubor EPUB pro čtení pomocí FileStreamu:

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Pokračujte v procesu převodu
}
```

### Krok 1.2: Vytvořte XpsSaveOptions

Vytvořte instanci XpsSaveOptions. Tento krok je zásadní pro konfiguraci výstupu XPS:

```csharp
var options = new XpsSaveOptions();
```

### Krok 1.3: Převeďte EPUB na XPS

Nyní zavolejte metodu ConvertEPUB pro převod EPUB na XPS:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Zadejte vlastní možnosti XPS

Výstup XPS můžete dále přizpůsobit zadáním vlastních možností, jako je velikost stránky a barva pozadí.

### Krok 2.1: Vlastní velikost stránky a barva pozadí

Vytvořte instanci XpsSaveOptions s vlastní velikostí stránky a barvou pozadí:

```csharp
var options = new XpsSaveOptions()
{
    PageSetup =
    {
        AnyPage = new Page()
        {
            Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
        }
    },
    BackgroundColor = System.Drawing.Color.AliceBlue,
};
```

### Krok 2.2: Převeďte EPUB na XPS pomocí vlastních možností

Nyní zavolejte metodu ConvertEPUB pro převod EPUB na XPS s vlastními možnostmi:

```csharp
ConvertEPUB(stream, options, "output.xps");
```

## Použít vlastního poskytovatele streamu

V tomto kroku převedeme EPUB na XPS pomocí vlastního poskytovatele streamu, což vám umožní manipulovat s výslednými daty.

### Krok 3.1: Vytvořte MemoryStreamProvider

Vytvořte instanci MemoryStreamProvider:

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    // Pokračujte v procesu převodu
}
```

### Krok 3.2: Převeďte EPUB na XPS pomocí poskytovatele streamu

Převeďte EPUB na XPS pomocí MemoryStreamProvider:

```csharp
ConvertEPUB(stream, new XpsSaveOptions(), streamProvider);
```

### Krok 3.3: Přístup a uložení výsledku

Načtěte tok paměti obsahující převedená data a uložte jej do výstupního souboru:

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.xps"))
{
    memory.CopyTo(fs);
}
```

### Zdrojový kód třídy MemoryStreamProvider

```csharp
class MemoryStreamProvider : Aspose.Html.IO.ICreateStreamProvider
        {
            // Seznam objektů MemoryStream vytvořených během vykreslování dokumentu
            public List<System.IO.MemoryStream> Streams { get; } = new List<System.IO.MemoryStream>();
            public System.IO.Stream GetStream(string name, string extension)
            {
                // Tato metoda se volá, když je vyžadován pouze jeden výstupní proud, například pro formáty XPS, PDF nebo TIFF.
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public System.IO.Stream GetStream(string name, string extension, int page)
            {
                // Tato metoda se volá, když je vyžadováno vytvoření více výstupních toků. Například při vykreslování HTML na seznam obrazových souborů (JPG, PNG atd.)
                System.IO.MemoryStream result = new System.IO.MemoryStream();
                Streams.Add(result);
                return result;
            }
            public void ReleaseStream(System.IO.Stream stream)
            {
                // Zde můžete uvolnit proud naplněný daty a například jej vyprázdnit na pevný disk
            }
            public void Dispose()
            {
                // Uvolnění zdrojů
                foreach (var stream in Streams)
                    stream.Dispose();
            }
        }
```
Gratulujeme! Úspěšně jste převedli soubor EPUB do formátu XPS pomocí Aspose.HTML pro .NET.

## Závěr

V tomto komplexním tutoriálu jsme prozkoumali, jak využít Aspose.HTML pro .NET k převodu souborů EPUB do formátu XPS s různými možnostmi přizpůsobení. Ať už jste zkušený vývojář nebo teprve začínáte, Aspose.HTML tento proces zjednodušuje a umožňuje vám snadno zpracovávat převody EPUB na XPS.

 Máte nějaké dotazy nebo jste narazili na problémy? Podívejte se na[Dokumentace Aspose.HTML](https://reference.aspose.com/html/net/) pro více informací nebo požádejte o pomoc[Fórum komunity Aspose.HTML](https://forum.aspose.com/).

## Často kladené otázky

### Co je Aspose.HTML pro .NET?
Aspose.HTML for .NET je výkonná knihovna, která umožňuje vývojářům pracovat s dokumenty HTML, EPUB a XPS v aplikacích .NET.

### Kde si mohu stáhnout Aspose.HTML pro .NET?
 Aspose.HTML pro .NET si můžete stáhnout z[stránka ke stažení](https://releases.aspose.com/html/net/).

### Je k dispozici bezplatná zkušební verze pro Aspose.HTML pro .NET?
 Ano, můžete získat bezplatnou zkušební verzi od[tady](https://releases.aspose.com/).

### Jak mohu získat dočasnou licenci pro Aspose.HTML pro .NET?
 Chcete-li získat dočasnou licenci, navštivte[dočasná licenční stránka](https://purchase.aspose.com/temporary-license/).

### Kde najdu další návody a dokumentaci pro Aspose.HTML pro .NET?
 Prozkoumejte širokou škálu výukových programů a podrobné dokumentace na[Dokumentace Aspose.HTML](https://reference.aspose.com/html/net/) strana.