---
title: Převeďte EPUB na obrázek v .NET pomocí Aspose.HTML
linktitle: Převést EPUB na obrázek v .NET
second_title: Aspose.HTML .NET API pro manipulaci s HTML
description: Přečtěte si, jak převést EPUB na obrázky pomocí Aspose.HTML pro .NET. Výukový program krok za krokem s příklady kódu a přizpůsobitelnými možnostmi.
weight: 11
url: /cs/net/html-extensions-and-conversions/convert-epub-to-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převeďte EPUB na obrázek v .NET pomocí Aspose.HTML


dnešní digitální době je schopnost manipulovat a převádět různé formáty dokumentů cennou dovedností. Aspose.HTML for .NET je výkonný nástroj, který umožňuje vývojářům bez námahy pracovat s dokumenty HTML a EPUB. V tomto tutoriálu se ponoříme do světa Aspose.HTML pro .NET a provedeme vás procesem převodu dokumentů EPUB do různých obrazových formátů. Každý příklad rozdělíme do několika kroků a každý krok vysvětlíme.

## Předpoklady

Než se ponoříme do světa Aspose.HTML pro .NET, měli byste se ujistit, že máte splněny následující předpoklady:

1. Visual Studio: Ujistěte se, že máte v systému nainstalované Visual Studio. Můžete si jej stáhnout z webu.

2.  Aspose.HTML pro .NET: Knihovnu můžete získat z webu Aspose[zde](https://releases.aspose.com/html/net/).

3. Váš datový adresář: Připravte si adresář, kam uložíte soubory EPUB a kam se budou ukládat výstupní obrázky.

4. Základní znalost C#: Pro pochopení a implementaci příkladů kódu uvedených v tomto tutoriálu je nezbytná znalost programování C#.

## Import nezbytných jmenných prostorů

Než začneme pracovat s Aspose.HTML pro .NET, musíte do kódu C# importovat požadované jmenné prostory. Tyto jmenné prostory poskytují přístup k funkcím Aspose.HTML for .NET.

```csharp
using Aspose.Html.Converters;
using Aspose.Html.Saving;
using Aspose.Html.Rendering.Image;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
using System.IO;
using System.Drawing;
using System.Collections.Generic;
```

Nyní, když máme předpoklady a jmenné prostory, přejděme k příkladům krok za krokem.

## Převod EPUB do JPEG

```csharp
    string dataDir = "Your Data Directory";
    // Otevřete existující soubor EPUB ke čtení.
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        // Chcete-li převést soubor EPUB na obrázek, zavolejte metodu ConvertEPUB.
        Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), "output.jpg");
    }
```
### Kroky

1. Zadejte cestu k souboru EPUB v proměnné dataDir.
2. Otevřete soubor EPUB pro čtení pomocí FileStream.
3. Zavolejte metodu ConvertEPUB, předejte stream EPUB, ImageSaveOptions určující výstupní formát (JPEG) a název výstupního souboru ("output.jpg").
5. Soubor EPUB se převede na obrázek JPEG.

tomto příkladu otevřeme soubor EPUB, přečteme jeho obsah a převedeme jej do formátu obrázku JPEG. Výstupní obrázek se uloží jako "output.jpg."

## Převod EPUB do PNG

Pomocí podobných struktur kódu můžete snadno převádět soubory EPUB do různých obrazových formátů, jako jsou PNG, BMP, GIF a TIFF. Zde je příklad převodu do PNG:

```csharp

    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Png);
        Converter.ConvertEPUB(stream, options, "output.png");
    }

```
### Kroky
1. Otevřete soubor EPUB pro čtení pomocí FileStream.
2. Inicializujte objekt ImageSaveOptions s požadovaným výstupním formátem (v tomto případě PNG).
3. Zavolejte metodu ConvertEPUB, předejte stream EPUB, možnosti uložení obrázku a název výstupního souboru.
4. Soubor EPUB se převede do zadaného formátu obrázku.

## Zadejte možnosti uložení obrázku

Výstup obrázku můžete přizpůsobit zadáním voleb, jako je velikost stránky a barva pozadí. Zde je příklad:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        var options = new ImageSaveOptions(ImageFormat.Jpeg)
        {
            PageSetup =
            {
                AnyPage = new Page()
                {
                    Size = new Size(Length.FromPixels(3000), Length.FromPixels(1000))
                }
            },
            BackgroundColor = Color.AliceBlue,
        };
        Converter.ConvertEPUB(stream, options, "output.jpg");
    }
```
### Kroky

1.  Zadejte cestu k souboru EPUB v`dataDir` variabilní.
2.  Otevřete soubor EPUB pro čtení pomocí a`FileStream`.
3.  Vytvořit`ImageSaveOptions` objekt a zadejte požadovaný výstupní formát (JPEG).
4. V případě potřeby přizpůsobte velikost stránky a barvu pozadí.
5.  Zavolejte na`ConvertEPUB`způsob, předávání toku EPUB, možnosti uložení obrázku a název výstupního souboru.
6. Soubor EPUB se převede na obrázek se zadanými možnostmi.

## Zadejte vlastního poskytovatele streamu

Pokud potřebujete manipulovat s výstupním proudem, můžete použít vlastního poskytovatele streamu. Zde je příklad:

```csharp
    string dataDir = "Your Data Directory";
    using (var stream = File.OpenRead(Path.Combine(dataDir, "input.epub")))
    {
        using (var streamProvider = new MemoryStreamProvider())
        {
            Converter.ConvertEPUB(stream, new ImageSaveOptions(ImageFormat.Jpeg), streamProvider);
            
            for (int i = 0; i < streamProvider.Streams.Count; i++)
            {
                var memory = streamProvider.Streams[i];
                memory.Seek(0, SeekOrigin.Begin);
                
                using (FileStream fs = File.Create($"page_{i + 1}.jpg"))
                {
                    memory.CopyTo(fs);
                }
            }
        }
    }

```
Zdrojový kód třídy MemoryStreamProvider.

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

### Kroky
1.  Zadejte cestu k souboru EPUB v`dataDir` variabilní.
2.  Otevřete soubor EPUB pro čtení pomocí a`FileStream`.
3.  Vytvořte a`MemoryStreamProvider` pro zpracování vlastních výstupních proudů.
4.  Zavolejte na`ConvertEPUB` způsob, předávání streamu EPUB, možností uložení obrázku (JPEG) a vlastního poskytovatele streamu.
5. Procházejte toky paměti ve vlastním poskytovateli a ukládejte je do jednotlivých souborů.
6. Tento příklad vám umožňuje podle potřeby manipulovat a ukládat více výstupních proudů.

## Závěr

Aspose.HTML for .NET je všestranná knihovna, která zjednodušuje práci s dokumenty EPUB a HTML. Díky možnosti převádět dokumenty EPUB do různých obrazových formátů a přizpůsobitelným možnostem nabízí širokou škálu aplikací pro vývojáře.

---

## Často kladené otázky

### 1. Kde si mohu stáhnout Aspose.HTML pro .NET?

 Aspose.HTML pro .NET si můžete stáhnout ze stránky vydání[zde](https://releases.aspose.com/html/net/).

### 2. Jak mohu získat dočasnou licenci pro Aspose.HTML pro .NET?

 Chcete-li získat dočasnou licenci, navštivte stránku dočasné licence[zde](https://purchase.aspose.com/temporary-license/).

### 3. Kde najdu další podporu pro Aspose.HTML pro .NET?

 V případě jakýchkoli dotazů nebo problémů můžete požádat o pomoc komunitu Aspose na fóru podpory[zde](https://forum.aspose.com/).

### 4. Mohu převést dokumenty EPUB do jiných formátů, jako je PDF nebo XPS?

Ano, Aspose.HTML for .NET můžete použít k převodu dokumentů EPUB do různých formátů, včetně PDF a XPS.

### 5. Je Aspose.HTML for .NET vhodný pro malé i velké projekty?

Absolutně! Aspose.HTML for .NET je navržen tak, aby byl škálovatelný, takže je skvělou volbou pro projekty všech velikostí.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
