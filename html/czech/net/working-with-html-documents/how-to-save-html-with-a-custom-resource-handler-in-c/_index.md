---
category: general
date: 2026-11-20
description: Naučte se, jak ukládat HTML pomocí vlastního ResourceHandleru v C# a
  také ukládat HTML do zip archivů pomocí stručného, produkčně připraveného kódu.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save html
- save html to zip
- custom ResourceHandler C#
- HtmlAgilityPack save example
- stream based HTML export
language: cs
lastmod: 2026-11-20
og_description: Jak uložit HTML pomocí vlastního ResourceHandleru v C# a volitelně
  uložit HTML do zip souborů – kompletní, spustitelný návod pro vývojáře .NET.
og_image_alt: Diagram showing how to save HTML with a custom ResourceHandler and zip
  the output
og_title: Jak uložit HTML pomocí vlastního manipulátoru zdrojů v C#
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  headline: How to save HTML with a custom resource handler in C#
  type: TechArticle
- description: Learn how to save HTML using a custom ResourceHandler in C# and also
    save HTML to zip archives with concise, production‑ready code.
  name: How to save HTML with a custom resource handler in C#
  steps:
  - name: What if I need multiple HTML files in the same zip?
    text: 'Create a new entry for each call to `HandleResource`. The `resourceName`
      argument typically contains the filename, so you can use it directly:'
  - name: How to handle large documents without exhausting memory?
    text: Replace `MemoryStream` with a `FileStream` that points to a temporary file.
      The handler then returns the file stream, and you can later delete the file
      after the zip is created.
  - name: Does this approach work with .NET Core on Linux?
    text: Yes. All APIs used (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) are
      cross‑platform. Ensure the target framework is at least .NET 6 for best compatibility.
  - name: Can I encrypt the zip archive?
    text: '`ZipArchive` supports password‑based encryption only through third‑party
      libraries (e.g., `SharpZipLib`). If encryption is required, wrap the output
      bytes with a library that provides AES encryption before sending them to the
      client.'
  type: HowTo
tags:
- C#
- HTML
- file I/O
title: Jak uložit HTML pomocí vlastního zpracovatele zdrojů v C#
url: /cs/net/working-with-html-documents/how-to-save-html-with-a-custom-resource-handler-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak uložit HTML pomocí vlastního resource handleru v C#

Pokud potřebujete vědět **jak uložit HTML** z řetězce v paměti nebo z parsovaného dokumentu, tento průvodce ukazuje kompletní řešení. Použití vlastního `ResourceHandler` vám umožní řídit cílový stream, což znamená, že můžete **uložit HTML do zip** archivů, aniž byste zapisovali dočasné soubory.

Uvidíte, proč je `ResourceHandler` upřednostňován před starším přístupem `IOutputStorage`, jak jej nastavit a jak jej rozšířit pro zip kompresi. Na konci tohoto tutoriálu můžete vložit kód do libovolného projektu .NET 6+ a přizpůsobit jej svým vlastním požadavkům na úložiště.

## Co vytvoříte

* Minimální `ResourceHandler`, který vrací `MemoryStream`.
* `HtmlDocument` vytvořený pomocí **HtmlAgilityPack**.
* Volání `doc.Save`, které zapisuje HTML do streamu poskytnutého handlerem.
* Volitelný obal, který komprimuje výsledné HTML do zip souboru.

Požadavky:

* .NET 6 SDK nebo novější.
* NuGet balíček `HtmlAgilityPack` (`dotnet add package HtmlAgilityPack`).
* Základní znalost C# streamů.

## Krok 1: Vytvořte vlastní resource handler (primární způsob, jak **uložit html**)

`ResourceHandler` základní třída (dostupná od verze 24.2 viewer SDK) definuje jedinou abstraktní metodu `HandleResource`. Implementací této metody získáte plnou kontrolu nad tím, kam se HTML zapisuje.

```csharp
using System.IO;

/// <summary>
/// Handles the output stream for each HTML resource.
/// Returning a MemoryStream keeps everything in memory, which is ideal for further processing
/// such as zipping or sending over a network.
/// </summary>
class MyHandler : ResourceHandler
{
    public override Stream HandleResource(string resourceName)
    {
        // You could inspect resourceName to decide between file, memory, or zip entry.
        return new MemoryStream();
    }
}
```

**Proč je to důležité:** Vrácením `MemoryStream` se vyhnete diskovému I/O, snížíte latenci a kód zůstane deterministický pro jednotkové testy. Handler je volán automaticky metodou `Save`, takže nikdy nemusíte explicitně předávat stream.

## Krok 2: Načtěte nebo vytvořte HTML dokument

`HtmlAgilityPack` poskytuje pohodlnou třídu `HtmlDocument`, která dokáže parsovat řetězec, soubor nebo stream. V tomto příkladu načteme jednoduchý literál, ale stejný kód funguje s libovolným HTML zdrojem.

```csharp
using HtmlAgilityPack;

/// <summary>
/// Builds a basic HTML document in memory. Replace the string with your own markup
/// or load it from an external source.
/// </summary>
HtmlDocument doc = new HtmlDocument();
doc.LoadHtml("<html><body>Hello World</body></html>");
```

**Proč je to důležité:** Udržení dokumentu v paměti souzní se stream‑based přístupem vlastního handleru. Také vám to umožní manipulovat s DOM před uložením, například vkládat skripty nebo opravovat špatně formátované tagy.

## Krok 3: Uložte dokument pomocí vlastního handleru

Volání `doc.Save` s instancí `MyHandler` spustí metodu `HandleResource`. HTML je zapsáno přímo do streamu, který jste vrátili.

```csharp
// Save the HTML; the handler provides the output stream.
doc.Save(new MyHandler());
```

Po dokončení `Save` obsahuje `MemoryStream` uvnitř `MyHandler` serializované HTML. Můžete jej získat takto:

```csharp
// Cast the handler back to access the stream (if you kept a reference)
MyHandler handler = new MyHandler();
doc.Save(handler);

// Reset position to read from the beginning.
handler.HandleResource("").Seek(0, SeekOrigin.Begin);
using var reader = new StreamReader(handler.HandleResource(""));
string htmlOutput = reader.ReadToEnd();
System.Console.WriteLine(htmlOutput);
```

**Výsledek:** Konzole vypíše přesně HTML, které jste předali do `LoadHtml`. To dokazuje, že nyní rozumíte **jak uložit HTML** pomocí vlastního handleru.

## Krok 4: Rozšíření handleru pro **uložení HTML do zip**

Pokud chcete HTML archivovat, upravte `MyHandler`, aby zapisoval do `ZipArchiveEntry`. .NET jmenný prostor `System.IO.Compression` to usnadňuje.

```csharp
using System.IO.Compression;

/// <summary>
/// Writes the HTML into a zip entry named "document.html".
/// The zip archive is created in memory and can be saved to a file or sent over HTTP.
/// </summary>
class ZipHtmlHandler : ResourceHandler, IDisposable
{
    private readonly MemoryStream _zipStream = new();
    private readonly ZipArchive _archive;

    public ZipHtmlHandler()
    {
        // Initialise the zip archive in create mode.
        _archive = new ZipArchive(_zipStream, ZipArchiveMode.Create, leaveOpen: true);
    }

    public override Stream HandleResource(string resourceName)
    {
        // Create a zip entry for the HTML file.
        var entry = _archive.CreateEntry("document.html", CompressionLevel.Optimal);
        return entry.Open(); // Returns a stream that writes directly into the zip entry.
    }

    /// <summary>
    /// Finalises the zip archive and returns the raw bytes.
    /// </summary>
    public byte[] GetZipBytes()
    {
        // Ensure all entries are flushed.
        _archive.Dispose();
        return _zipStream.ToArray();
    }

    public void Dispose()
    {
        _archive?.Dispose();
        _zipStream?.Dispose();
    }
}
```

Nyní použijte nový handler:

```csharp
// Instantiate the zip‑aware handler.
using var zipHandler = new ZipHtmlHandler();

// Save HTML; it ends up inside the zip archive.
doc.Save(zipHandler);

// Retrieve the zip file as a byte array.
byte[] zipBytes = zipHandler.GetZipBytes();

// Optionally write the zip to disk for verification.
File.WriteAllBytes("output.zip", zipBytes);
System.Console.WriteLine("ZIP file created with size: " + zipBytes.Length);
```

**Proč to funguje:** Metoda `HandleResource` vytvoří zip položku s názvem `document.html`. Když `doc.Save` zapisuje do vráceného streamu, data jsou automaticky komprimována. Protože zip je vytvořen v paměti, můžete jej vrátit z webového API, připojit k e‑mailu nebo uložit do databáze, aniž byste se dotkli souborového systému.

## Časté otázky a okrajové případy

### Co když potřebuji více HTML souborů ve stejném zipu?

Vytvořte novou položku pro každé volání `HandleResource`. Argument `resourceName` obvykle obsahuje název souboru, takže jej můžete použít přímo:

```csharp
public override Stream HandleResource(string resourceName)
{
    var entry = _archive.CreateEntry(resourceName, CompressionLevel.Optimal);
    return entry.Open();
}
```

### Jak zacházet s velkými dokumenty, aniž by se vyčerpala paměť?

Nahraďte `MemoryStream` za `FileStream`, který ukazuje na dočasný soubor. Handler pak vrátí tento file stream a po vytvoření zipu můžete soubor později smazat.

### Funguje tento přístup s .NET Core na Linuxu?

Ano. Všechny použité API (`MemoryStream`, `ZipArchive`, `HtmlAgilityPack`) jsou multiplatformní. Ujistěte se, že cílový framework je alespoň .NET 6 pro nejlepší kompatibilitu.

### Můžu zip archiv zašifrovat?

`ZipArchive` podporuje šifrování založené na hesle pouze prostřednictvím knihoven třetích stran (např. `SharpZipLib`). Pokud je šifrování vyžadováno, zabalte výstupní bajty pomocí knihovny, která poskytuje AES šifrování, před odesláním klientovi.

## Profesionální tipy

* **Znovu použijte handler** při zpracování mnoha dokumentů ve skupině; vytvoření nového `ZipArchive` pro každý soubor přidává zbytečnou režii.
* **Nastavte `LeaveOpen: true`** v konstruktoru `ZipArchive`, pokud potřebujete číst bajty zipu, zatímco archiv je stále otevřený.
* **Validujte HTML** před uložením voláním `doc.OptionCheckSyntax = true;` – tím se včas zachytí špatně formátované tagy.
* **Zaznamenejte velikost** vytvořeného zipu; neobvykle velký výstup často naznačuje duplicitní zdroje nebo chybějící kompresi.

## Kompletní funkční příklad

Níže je jeden soubor, který můžete vložit do konzolového projektu (`dotnet new console`) a spustit. Ukazuje jak ukládání čistého HTML, tak kompresi do zipu.



## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Jak uložit HTML v C# s vlastním Resource Handlerem](/html/english/net/working-with-html-documents/how-to-save-html-in-c-with-custom-resource-handler/)
- [Jak použít ZipArchive – Uložit HTML a zdroje do ZIP souboru](/html/english/net/html-extensions-and-conversions/how-to-use-ziparchive-save-html-and-resources-to-a-zip-file/)
- [uložit html jako zip s vlastním resource handlerem – krok za krokem průvodce](/html/english/net/html-extensions-and-conversions/save-html-as-zip-with-a-custom-resource-handler-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}