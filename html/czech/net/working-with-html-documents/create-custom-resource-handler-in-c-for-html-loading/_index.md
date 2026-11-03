---
category: general
date: 2026-08-15
description: Vytvořte vlastní obslužný program zdrojů v C# pro správu HTML zdrojů,
  jako jsou obrázky a CSS. Naučte se HTMLLoadOptions, paměťové proudy a načítání HTMLDocumentu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create custom resource handler
- C# resource handler
- HTMLLoadOptions
- HTMLDocument loading
- memory stream for resources
language: cs
lastmod: 2026-08-15
og_description: Vytvořte vlastní obslužný program zdrojů v C# pro řízení způsobu streamování
  HTML zdrojů. Tento tutoriál ukazuje nastavení HTMLLoadOptions, práci s paměťovým
  streamem a načítání HTMLDocument s vlastní logikou.
og_image_alt: Screenshot of C# code defining a custom resource handler class for HTML
  loading
og_title: Vytvořte vlastní manipulátor zdrojů v C# – kompletní průvodce správou HTML
  zdrojů
schemas:
- author: GroupDocs
  dateModified: '2026-08-15'
  description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  headline: Create custom resource handler in C# for HTML loading
  type: TechArticle
- description: Create custom resource handler in C# to manage HTML resources like
    images and CSS. Learn HTMLLoadOptions, memory streams, and HTMLDocument loading.
  name: Create custom resource handler in C# for HTML loading
  steps:
  - name: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
    text: '**Create a custom resource handler** by subclassing `ResourceHandler`.'
  - name: Configure `HTMLLoadOptions` to use the handler.
    text: Configure `HTMLLoadOptions` to use the handler.
  - name: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
    text: Load an HTML file with `HTMLDocument` while the handler supplies a stream
      for each resource.
  - name: (Optional) Store received resources to disk for verification.
    text: (Optional) Store received resources to disk for verification.
  type: HowTo
tags:
- C#
- HTML
- resource handling
title: Vytvořte vlastní obslužný program zdrojů v C# pro načítání HTML
url: /cs/net/working-with-html-documents/create-custom-resource-handler-in-c-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte vlastní manipulátor zdrojů v C# pro načítání HTML

Pokud potřebujete **vytvořit vlastní manipulátor zdrojů** pro soubory HTML, tento průvodce vám přesně ukáže, jak na to. Naučíte se zachytávat obrázky, CSS a další aktiva při načítání HTML dokumentu pomocí `HTMLLoadOptions` a paměťového proudu.

Tutoriál pokrývá vše potřebné k implementaci znovupoužitelného manipulátoru, nastavení možností načítání a ověření, že zdroje jsou zachyceny správně. Není potřeba žádná externí dokumentace – stačí kód níže a vysvětlení.

## Požadavky

- .NET 6.0 nebo novější
- Základní znalost C#
- Odkaz na knihovnu pro zpracování HTML, která poskytuje `HTMLDocument`, `HtmlLoadOptions` a `ResourceHandler` (např. GroupDocs.Viewer pro .NET)

## Přehled řešení

Budeme:

1. **Vytvořit vlastní manipulátor zdrojů** podtříděním `ResourceHandler`.
2. Nastavit `HTMLLoadOptions` tak, aby používal manipulátor.
3. Načíst soubor HTML pomocí `HTMLDocument`, zatímco manipulátor poskytuje proud pro každý zdroj.
4. (Volitelné) Uložit získané zdroje na disk pro ověření.

Každý krok obsahuje kompletní zdrojový kód a odůvodnění.

## Krok 1: Definujte třídu vlastního manipulátoru zdrojů

Vytvoření vlastního manipulátoru znamená přepsání metody `HandleResource`, aby knihovna mohla zapisovat bajty zdroje do proudu, který ovládáte. Použití `MemoryStream` udržuje data v paměti, což je ideální pro testování nebo další zpracování.

```csharp
using System;
using System.IO;
using GroupDocs.Viewer.Handler;   // Adjust namespace to match your library

namespace HtmlResourceDemo
{
    /// <summary>
    /// Provides a memory stream for each HTML resource (images, CSS, etc.).
    /// </summary>
    public class MyHandler : ResourceHandler
    {
        /// <summary>
        /// Called by the viewer for every external resource referenced in the HTML.
        /// </summary>
        /// <param name="info">Information about the resource (name, MIME type, etc.).</param>
        /// <returns>A writable stream that receives the resource data.</returns>
        public override Stream HandleResource(ResourceInfo info)
        {
            // A fresh MemoryStream ensures the viewer can write the resource bytes.
            // You could replace this with a FileStream to save directly to disk.
            return new MemoryStream();
        }
    }
}
```

**Proč je to důležité:**  
Přepsání `HandleResource` vám dává úplnou kontrolu nad tím, kam data zdroje směřují. Pokud později potřebujete kešovat obrázky, transformovat CSS nebo logovat využití zdrojů, můžete `MemoryStream` nahradit libovolnou vlastní implementací proudu.

## Krok 2: Nastavte `HTMLLoadOptions` pro použití manipulátoru

`HTMLLoadOptions` vám umožňuje připojit manipulátor do načítacího řetězce. Nastavením vlastnosti `ResourceHandler` řeknete prohlížeči, aby volal `MyHandler` pro každý externí asset.

```csharp
using GroupDocs.Viewer.Options;   // Namespace for HtmlLoadOptions

// ...

var loadOptions = new HtmlLoadOptions
{
    // Attach the custom handler defined in Step 1
    ResourceHandler = new MyHandler()
};
```

**Proč je to důležité:**  
Bez přiřazení `ResourceHandler` by prohlížeč zapisoval zdroje do výchozího umístění (často do dočasné složky). Specifikací vlastního manipulátoru **vytvoříte vlastní manipulátor zdrojů**, který odpovídá strategii ukládání vaší aplikace.

## Krok 3: Načtěte HTML dokument s nakonfigurovanými možnostmi

Nyní načtěte soubor HTML. Prohlížeč zavolá `MyHandler.HandleResource` pro každý zdroj, na který narazí.

```csharp
using GroupDocs.Viewer;           // Namespace for HTMLDocument

// Path to the source HTML file
string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");

// Load the document using the custom load options
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);
```

V tomto okamžiku je HTML obsah parsován a všechny externí zdroje byly streamovány do paměťových bufferů poskytnutých `MyHandler`.

## Krok 4 (volitelné): Přístup k zachyceným zdrojům

Pokud potřebujete zdroje prohlédnout nebo uložit, můžete upravit `MyHandler`, aby ukládal každý `MemoryStream` do slovníku s klíčem podle názvu zdroje.

```csharp
public class MyHandler : ResourceHandler
{
    // Stores streams for later retrieval
    public Dictionary<string, MemoryStream> Resources { get; } = new();

    public override Stream HandleResource(ResourceInfo info)
    {
        var stream = new MemoryStream();
        Resources[info.Name] = stream;
        return stream;
    }
}
```

Po načtení můžete iterovat přes `handler.Resources` a každý zapsat na disk:

```csharp
var handler = new MyHandler();
var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };
HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions);

// Save each captured resource
foreach (var kvp in handler.Resources)
{
    string fileName = Path.Combine("output_resources", kvp.Key);
    File.WriteAllBytes(fileName, kvp.Value.ToArray());
    Console.WriteLine($"Saved resource: {fileName}");
}
```

**Proč je to důležité:**  
Ukládání zdrojů umožňuje následné zpracování, jako je optimalizace obrázků, minifikace CSS nebo archivace. Také poskytuje hmatatelné ověření, že logika **vytvořit vlastní manipulátor zdrojů** funguje podle očekávání.

## Krok 5: Vyčištění

Jak `HTMLDocument`, tak i všechny proudy by měly být uvolněny (disposed), aby se uvolnily neřízené zdroje.

```csharp
doc.Dispose();                     // Releases internal buffers
foreach (var stream in handler.Resources.Values)
{
    stream.Dispose();              // Flushes and releases memory
}
```

## Kompletní spustitelný příklad

Níže je samostatný program, který demonstruje všechny kroky od definice třídy po extrakci zdrojů.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Viewer;
using GroupDocs.Viewer.Handler;
using GroupDocs.Viewer.Options;

namespace HtmlResourceDemo
{
    public class MyHandler : ResourceHandler
    {
        public Dictionary<string, MemoryStream> Resources { get; } = new();

        public override Stream HandleResource(ResourceInfo info)
        {
            var stream = new MemoryStream();
            Resources[info.Name] = stream;
            return stream;
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Prepare paths
            string htmlPath = Path.Combine("YOUR_DIRECTORY", "input.html");
            string outputDir = Path.Combine("output_resources");
            Directory.CreateDirectory(outputDir);

            // 2️⃣ Create handler and load options
            var handler = new MyHandler();
            var loadOptions = new HtmlLoadOptions { ResourceHandler = handler };

            // 3️⃣ Load the HTML document
            using (HTMLDocument doc = new HTMLDocument(htmlPath, loadOptions))
            {
                // Document is now loaded; resources are in handler.Resources
            }

            // 4️⃣ Persist captured resources
            foreach (var kvp in handler.Resources)
            {
                string filePath = Path.Combine(outputDir, kvp.Key);
                File.WriteAllBytes(filePath, kvp.Value.ToArray());
                Console.WriteLine($"Saved: {filePath}");
            }

            // 5️⃣ Clean up streams
            foreach (var stream in handler.Resources.Values)
                stream.Dispose();

            Console.WriteLine("All resources processed.");
        }
    }
}
```

**Očekávaný výstup**

```
Saved: output_resources/logo.png
Saved: output_resources/styles.css
Saved: output_resources/banner.jpg
All resources processed.
```

Konzole vypíše každý zdroj, který prohlížeč streamoval přes váš vlastní manipulátor, což potvrzuje, že workflow **vytvořit vlastní manipulátor zdrojů** byl úspěšný.

## Časté otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| *Co když je zdroj velký (např. obrázek s vysokým rozlišením)?* | Nahraďte `MemoryStream` `FileStream`, který ukazuje na dočasnou složku. Tím se zabrání nadměrné spotřebě paměti. |
| *Mohu filtrovat zdroje podle typu?* | Uvnitř `HandleResource` zkontrolujte `info.MimeType` nebo `info.Extension` a vraťte `null` pro nechtěné typy. Vrácení `null` řekne prohlížeči, aby zdroj přeskočil. |
| *Je vyžadována bezpečnost vláken?* | Pokud je stejná instance manipulátoru používána při více souběžných načítáních, chraňte slovník `Resources` pomocí zámku nebo použijte souběžnou kolekci. |
| *Jak podpořit relativní URL?* | `ResourceInfo` obsahuje původní URL; můžete jej kombinovat se základní cestou HTML souboru k vyřešení relativních odkazů před uložením. |

## Závěr

Nyní víte, jak **vytvořit vlastní manipulátor zdrojů** v C# pro načítání HTML, nakonfigurovat `HTMLLoadOptions`, zachytit streamované assety a odpovědně uvolnit prostředky. Tento vzor vám dává plnou kontrolu nad správou zdrojů, umožňující scénáře jako zpracování obrázků za běhu, přepisování CSS nebo bezpečné ukládání.

Dále prozkoumejte související témata jako **načítání HTMLDocument** s různými možnostmi renderování, nebo rozšiřte manipulátor na implementace **C# resource handler**, které zapisují přímo do cloudového úložiště. Experimentujte s metodou `HandleResource` manipulátoru, aby odpovídala specifickému workflow zdrojů ve vašem projektu.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vytvořit HTML ze stringu v C# – Průvodce vlastním manipulátorem zdrojů](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Vlastní manipulátor zdrojů v C# – Tutoriál převodu HTML do ZIP](/html/english/net/html-extensions-and-conversions/custom-resource-handler-in-c-convert-html-to-zip-tutorial/)
- [Jak uložit HTML v C# – Kompletní průvodce s použitím vlastního manipulátoru zdrojů](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}