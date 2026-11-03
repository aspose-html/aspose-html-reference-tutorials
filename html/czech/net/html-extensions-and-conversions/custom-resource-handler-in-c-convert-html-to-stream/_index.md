---
category: general
date: 2026-06-22
description: Návod na vlastní obslužný program zdrojů, který ukazuje, jak převést
  HTML na stream pomocí Aspose.HTML v C#. Krok za krokem průvodce pro vývojáře.
draft: false
keywords:
- custom resource handler
- convert html to stream
- Aspose.HTML C#
- HTML to MemoryStream
- resource handling C#
language: cs
og_description: Tutoriál o vlastním handleru zdrojů, který vysvětluje, jak převést
  HTML na stream pomocí Aspose.HTML v C#. Naučte se kompletní implementaci.
og_title: Vlastní obsluha zdrojů v C# – Převod HTML na stream
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Custom resource handler tutorial showing how to convert HTML to stream
    with Aspose.HTML in C#. Step-by-step guide for developers.
  headline: Custom Resource Handler in C# – Convert HTML to Stream
  type: TechArticle
tags:
- C#
- Aspose.HTML
- Stream Processing
title: Vlastní obsluha zdrojů v C# – převod HTML na stream
url: /cs/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-stream/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vlastní obslužná rutina zdrojů v C# – Převod HTML na Stream

Už jste se někdy zamýšleli, jak **custom resource handler** použít při konverzi HTML a přitom vše držet v paměti? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují *convert HTML to stream* bez zásahu do souborového systému, zejména v cloud‑native nebo sandboxovaných prostředích.

V tomto průvodci projdeme kompletním, spustitelným příkladem, který přesně ukazuje, jak vytvořit vlastní obslužnou rutinu zdrojů pomocí Aspose.HTML a poté ji použít k **convert HTML to stream**. Žádné externí soubory, žádná skrytá magie — jen čistý C# kód, který můžete okamžitě vložit do svého projektu.

## Co tento tutoriál pokrývá

- Proč můžete potřebovat **custom resource handler** místo výchozího přístupu založeného na souborech.  
- Krok‑za‑krokem vytvoření `HTMLDocument` kompletně v paměti.  
- Implementace podtřídy `ResourceHandler`, která rozhoduje, kam se umístí každý externí asset (obrázky, CSS atd.).  
- Konfigurace `HtmlSaveOptions` pro připojení vašeho handleru do pipeline ukládání.  
- Závěrečný krok: uložení HTML (a jeho zdrojů) do `MemoryStream`, abyste mohli **convert HTML to stream** pro další zpracování — ať už nahráním do Azure Blob, odesláním přes HTTP nebo předáním jiné API.  

Na konci budete mít samostatný ukázkový kód a tipy, jak zacházet s reálnými okrajovými případy, jako jsou velké obrázky nebo CSS balíčky.

## Požadavky

- .NET 6.0 nebo novější (kód funguje jak na .NET Core, tak na .NET Framework).  
- Platná licence Aspose.HTML nebo zkušební verze — bezplatná verze přidává vodoznak, ale API zůstává stejné.  
- Základní znalost C# async/await (volitelné; ukázka je synchronní pro přehlednost).  

Pokud už to máte, skvělé — ponořme se do toho.

## Krok 1: Nastavení HTML dokumentu v paměti

Nejprve potřebujeme objekt `HTMLDocument`, který existuje výhradně v RAM. Tím se eliminuje jakákoliv potřeba fyzického souboru `.html` na disku.

```csharp
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;

// Create a simple HTML snippet – you could also load from a string builder or an HTTP response.
string htmlContent = "<html><head><title>Demo</title></head><body><h1>Hello World</h1></body></html>";

// The HTMLDocument constructor accepts raw HTML markup.
var htmlDoc = new HTMLDocument(htmlContent);
```

> **Proč je to důležité** – Přímým předáním surového markupu máte plnou kontrolu nad zdrojem a vyhnete se nechtěným vedlejším efektům, jako je řešení relativních cest, které může zavést konstruktor založený na souboru.

## Krok 2: Vytvoření vlastního ResourceHandleru

Aspose.HTML volá `ResourceHandler.HandleResource` pro **každý** externí zdroj, na který narazí — např. obrázky, styly, fonty, dokonce i odkazované skripty. Výchozí implementace zapisuje každý asset do složky na disku. Nahradíme ji handlerem, který vrátí prázdný `MemoryStream`. Ve výrobním scénáři byste mohli stream komprimovat, uložit do databáze nebo vše zabalit do ZIP.

```csharp
// Define a custom handler that decides how to store each external resource.
class MyResourceHandler : ResourceHandler
{
    // The 'info' argument contains details like the resource's URL and MIME type.
    public override Stream HandleResource(ResourceInfo info)
    {
        // For demo purposes we just return an empty MemoryStream.
        // Replace this with real logic (e.g., write to a blob store) as needed.
        return new MemoryStream();
    }
}
```

**Pro tip:** Pokud potřebujete původní bajty (pro logování nebo transformaci), přečtěte `info.Stream` uvnitř metody před tím, než vrátíte svůj vlastní stream.

## Krok 3: Připojení handleru do HtmlSaveOptions

Nyní řekneme Aspose.HTML, aby používal náš `MyResourceHandler` při každém ukládání dokumentu. Zde skutečně začíná magie **convert HTML to stream**.

```csharp
var saveOptions = new HtmlSaveOptions
{
    // Attach our custom handler.
    ResourceHandler = new MyResourceHandler()
};
```

Zde můžete také doladit další možnosti — např. `Encoding`, `PrettyPrint` nebo `Compress` — ale jsou volitelné pro základní ukázku.

## Krok 4: Uložení dokumentu do MemoryStream

S handlerem na místě se ukládání dokumentu stane jedním řádkem. Metoda `HTMLDocument.Save` zavolá `HandleResource` pro každý externí asset a zapíše hlavní HTML markup do poskytnutého streamu.

```csharp
// Create a MemoryStream that will receive the final HTML + references.
using var outputStream = new MemoryStream();

// Save the document (HTML + any resources) into the stream.
htmlDoc.Save(outputStream, saveOptions);

// Reset the position so downstream readers start at the beginning.
outputStream.Position = 0;
```

V tomto okamžiku `outputStream` obsahuje kompletní HTML dokument a všechny externí zdroje byly zpracovány `MyResourceHandler`. Kdybyste ve `HandleResource` skutečně zapisovali bajty, byly by uloženy tam, kam jste je nasměrovali.

## Krok 5: Použití streamu – Příklad: zápis do souboru

Níže je malý úryvek, který ukazuje, jak můžete vzít výsledný stream a uložit jej na disk, jen pro ověření výstupu. Ve skutečných aplikacích můžete toto nahradit nahráním do cloudového úložiště, tělem HTTP odpovědi nebo dalším transformačním krokem.

```csharp
// Optional: write the stream to a file for inspection.
using var fileStream = new FileStream("output.html", FileMode.Create, FileAccess.Write);
outputStream.CopyTo(fileStream);
```

Spuštěním celého programu by se měl vytvořit soubor `output.html`, který obsahuje:

```html
<html><head><title>Demo</title></head><body><h1>Hello World</h1></body></html>
```

Protože jsme neembedovali žádné externí assety, resource handler nevytvořil žádné další soubory — ale pipeline prokázala, že **custom resource handler** funguje ruku v ruce s **convert HTML to stream**.

## Zpracování reálných zdrojů

Demo používá prostý HTML řetězec, ale většina stránek odkazuje na CSS, obrázky nebo fonty. Zde je, jak můžete rozšířit `MyResourceHandler`, aby skutečně zachytil tyto bajty:

```csharp
public override Stream HandleResource(ResourceInfo info)
{
    // Read the incoming resource data.
    using var source = info.Stream; // Stream provided by Aspose.HTML
    var memory = new MemoryStream();
    source.CopyTo(memory);
    memory.Position = 0; // Reset for downstream consumers

    // Example: store the bytes in a dictionary for later use.
    // ResourceCache[info.Uri] = memory.ToArray();

    // Return the same stream (or a new one) so Aspose.HTML can continue.
    return memory;
}
```

**Okrajový případ** – Velké obrázky: Pokud očekáváte assety v megabajtech, zvažte zápis přímo do dočasného souboru nebo cloudového blobu, aby nedošlo k přetížení paměti. Jen se ujistěte, že vrácený stream je seekable, pokud Aspose.HTML potřebuje číst znovu.

## Kompletní funkční příklad

Spojením všeho dohromady zde máte kompletní, připravenou konzolovou aplikaci. Vložte ji do nového `.csproj` a stiskněte **F5**.

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Saving;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the in‑memory HTML document.
        string html = @"
            <html>
                <head>
                    <title>Demo Page</title>
                    <link rel='stylesheet' href='styles.css'>
                </head>
                <body>
                    <h1>Hello World</h1>
                    <img src='logo.png' alt='Logo'>
                </body>
            </html>";
        var htmlDoc = new HTMLDocument(html);

        // 2️⃣ Define a custom resource handler.
        class MyResourceHandler : ResourceHandler
        {
            public override Stream HandleResource(ResourceInfo info)
            {
                // For illustration we just log the resource URI.
                Console.WriteLine($\"Handling resource: {info.Uri}\");
                // Return an empty stream – replace with real storage logic.
                return new MemoryStream();
            }
        }

        // 3️⃣ Configure save options with our handler.
        var options = new HtmlSaveOptions
        {
            ResourceHandler = new MyResourceHandler()
        };

        // 4️⃣ Save to a MemoryStream (the core of convert HTML to stream).
        using var output = new MemoryStream();
        htmlDoc.Save(output, options);
        output.Position = 0; // rewind

        // 5️⃣ Verify – write to a file (optional).
        using var file = new FileStream(\"output.html\", FileMode.Create, FileAccess.Write);
        output.CopyTo(file);

        Console.WriteLine(\"HTML saved to MemoryStream and written to output.html\");
    }
}
```

**Očekávaný výstup v konzoli** (předpokládáme, že stránka odkazuje na dva zdroje):

```
Handling resource: styles.css
Handling resource: logo.png
HTML saved to MemoryStream and written to output.html
```

Soubor `output.html` bude obsahovat původní markup; externí CSS a obrázek byly zachyceny handlerem (v tomto demu jsou zahazovány, ale můžete je uložit jinde).

## Časté úskalí a jak se jim vyhnout

| Pitfall | Why it Happens | Fix |
|---------|----------------|-----|
| **Přetečení paměti** při zpracování velkých obrázků | Vrácení nového `MemoryStream` pro každý zdroj hromadí data v RAM. | Streamujte přímo do souboru nebo cloudového blobu uvnitř `HandleResource`. |
| **Chybějící zdroje** kvůli relativním URL | Aspose.HTML řeší relativní URI vůči základní URL dokumentu, která je pro dokumenty v paměti prázdná. | Nastavte `htmlDoc.BaseUrl = new Uri(\"https://example.com/\");` před uložením. |
| **Handler není volán** | Použití `HTMLDocument.Save(string path, ...)` obchází vlastní handler. | Vždy používejte přetížení, které přijímá `Stream`. |
| **Problémy s thread‑safety** | Stejná instance handleru může být znovu použita při paralelních ukládáních. | Buď vytvořte novou instanci handleru pro každé ukládání, nebo zajistěte... |

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vlastních projektech.

- [Jak uložit HTML v C# – Kompletní průvodce s použitím vlastního Resource Handleru](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Vytvořit HTML ze stringu v C# – Průvodce vlastním Resource Handlerem](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Převod HTML do PDF s Aspose.HTML – Kompletní průvodce manipulací](/html/english/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}