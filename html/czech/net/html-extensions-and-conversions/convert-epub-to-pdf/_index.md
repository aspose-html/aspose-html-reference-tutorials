---
title: Převeďte EPUB do PDF v .NET pomocí Aspose.HTML
linktitle: Převeďte EPUB do PDF v .NET
second_title: Aspose.HTML .NET API pro manipulaci s HTML
description: Přečtěte si, jak převést EPUB do PDF pomocí Aspose.HTML pro .NET. Tento podrobný průvodce obsahuje možnosti přizpůsobení, často kladené dotazy a další pro bezproblémový převod dokumentů.
type: docs
weight: 12
url: /cs/net/html-extensions-and-conversions/convert-epub-to-pdf/
---

V tomto tutoriálu prozkoumáme, jak používat Aspose.HTML pro .NET k převodu souborů EPUB do PDF. Aspose.HTML je výkonná knihovna .NET, která poskytuje různé funkce pro práci s dokumenty HTML a EPUB. Pokryjeme předpoklady, importujeme potřebné jmenné prostory a rozebereme několik příkladů, přičemž každý krok podrobně vysvětlíme.

## Předpoklady

Než začnete, ujistěte se, že máte splněny následující předpoklady:

1. Aspose.HTML for .NET: Ujistěte se, že máte v projektu .NET nainstalovaný Aspose.HTML for .NET. Můžete si jej stáhnout z[zde](https://releases.aspose.com/html/net/).

2. Váš datový adresář: Budete potřebovat datový adresář, kde jsou uloženy vaše soubory EPUB.

Nyní se pojďme ponořit do procesu převodu EPUB do PDF pomocí Aspose.HTML pro .NET krok za krokem.

## Převést EPUB do PDF

### Krok 1: Inicializujte svůj projekt

Ujistěte se, že máte nastaven projekt .NET a je nainstalován Aspose.HTML for .NET.

### Krok 2: Importujte požadované jmenné prostory

Do souboru kódu C# importujte potřebné jmenné prostory:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
```

### Krok 3: Otevřete soubor EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Pokračujte dalším krokem...
}
```

-  Nahradit`"Your Data Directory"` se skutečným adresářem, kde se nachází váš soubor EPUB.
- Tento kód otevře soubor EPUB pro čtení.

### Krok 4: Nastavte možnosti PDF a proveďte převod

```csharp
var options = new PdfSaveOptions();
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Vytvořte instanci`PdfSaveOptions` specifikovat nastavení převodu PDF.
-  Použijte`Converter.ConvertEPUB` metoda pro převod EPUB do PDF s danými možnostmi.
- Uložte výsledné PDF jako „output.pdf“.

## Zadejte možnosti uložení PDF

### Krok 1: Inicializujte svůj projekt

Ujistěte se, že máte nastaven projekt .NET a nainstalovaný Aspose.HTML for .NET.

### Krok 2: Importujte požadované jmenné prostory

Importujte potřebné jmenné prostory do kódu C#:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
using Aspose.Html.Drawing;
```

### Krok 3: Otevřete soubor EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Pokračujte dalším krokem...
}
```

-  Nahradit`"Your Data Directory"` se skutečným adresářem vašeho souboru EPUB.
- Otevřete soubor EPUB pro čtení.

### Krok 4: Přizpůsobte možnosti PDF

```csharp
var options = new PdfSaveOptions()
{
    PageSetup = { AnyPage = new Page() { Size = Size.FromPixels(3000, 1000) } },
    BackgroundColor = System.Drawing.Color.AliceBlue
};
```

-  Vytvořte instanci`PdfSaveOptions` a upravte jej podle svých požadavků.
- V tomto příkladu nastavíme velikost stránky na šířku 3000 pixelů a výšku 1000 pixelů a barvu pozadí na Alice Blue.

### Krok 5: Proveďte konverzi

```csharp
Converter.ConvertEPUB(stream, options, "output.pdf");
```

-  Použijte`Converter.ConvertEPUB` metoda pro převod EPUB do PDF s vlastními možnostmi.
- Uložte výsledné PDF jako „output.pdf“.

## Použít vlastního poskytovatele streamu

### Krok 1: Inicializujte svůj projekt

Nastavte projekt .NET a nainstalujte Aspose.HTML pro .NET.

### Krok 2: Importujte požadované jmenné prostory

Do kódu C# importujte potřebné jmenné prostory:

```csharp
using Aspose.Html.Saving;
using Aspose.Html.Converters;
using Aspose.Html.IO;
```

### Krok 3: Otevřete soubor EPUB

```csharp
string dataDir = "Your Data Directory";
using (var stream = System.IO.File.OpenRead(dataDir + "input.epub"))
{
    // Pokračujte dalším krokem...
}
```

-  Nahradit`"Your Data Directory"` se skutečným adresářem vašeho souboru EPUB.
- Otevřete soubor EPUB pro čtení.

### Krok 4: Použijte vlastního poskytovatele streamu

```csharp
using (var streamProvider = new MemoryStreamProvider())
{
    Converter.ConvertEPUB(stream, new PdfSaveOptions(), streamProvider);

    // Pokračujte dalším krokem...
}
```

-  Vytvořte a`MemoryStreamProvider` spravovat výsledek převodu jako paměťový proud.
-  Použijte`Converter.ConvertEPUB` metoda s vlastním poskytovatelem streamu.

### Krok 5: Uložte výsledek

```csharp
var memory = streamProvider.Streams.First();
memory.Seek(0, System.IO.SeekOrigin.Begin);

using (System.IO.FileStream fs = System.IO.File.Create("output.pdf"))
{
    memory.CopyTo(fs);
}
```

- Přístup k paměťovému proudu obsahujícímu převedená data.
- Nastavte pozici streamu na začátek.
- Vytvořte výstupní soubor PDF a zkopírujte do něj obsah z paměťového toku.

### Zdrojový kód třídy MemoryStreamProvider. 

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
Nyní jste se naučili, jak převádět soubory EPUB do PDF pomocí Aspose.HTML for .NET s různými možnostmi a možnostmi přizpůsobení. Aspose.HTML zjednodušuje proces a poskytuje flexibilitu a kontrolu nad konverzí vašich dokumentů.

## Závěr

Aspose.HTML for .NET je všestranný nástroj pro převod souborů EPUB do PDF, který nabízí možnosti přizpůsobení pro přizpůsobení výsledného dokumentu PDF vašim potřebám. Ať už požadujete jednoduché konverze nebo pokročilé přizpůsobení, Aspose.HTML vás pokryje.

 Pokud jste to ještě neudělali, můžete si stáhnout Aspose.HTML pro .NET z webu[webové stránky](https://releases.aspose.com/html/net/) a začněte jej používat ve svých aplikacích .NET ještě dnes.

---

## Nejčastější dotazy

### Je Aspose.HTML pro .NET zdarma k použití?
    Aspose.HTML for .NET je komerční produkt, ale je k dispozici bezplatná zkušební verze[zde](https://releases.aspose.com/).

### Mohu upravit vzhled převedeného PDF?
   Ano, vzhled PDF si můžete přizpůsobit úpravou voleb, jako je velikost stránky a barva pozadí, jak je znázorněno v příkladu 2.

### Jak mohu získat podporu pro Aspose.HTML pro .NET?
    Podporu a zdroje najdete na[Fórum Aspose.HTML](https://forum.aspose.com/).

### Existují další formáty, které mohu převést pomocí Aspose.HTML pro .NET?
   Ano, Aspose.HTML for .NET podporuje různé formáty dokumentů, včetně HTML, EPUB a dalších.

### Je Aspose.HTML for ..NET vhodný pro konverzi dokumentů ve velkém měřítku?
   Aspose.HTML for .NET je navržen tak, aby efektivně zvládal převody dokumentů ve velkém měřítku, takže je vhodný pro širokou škálu aplikací.

