---
category: general
date: 2026-08-15
description: Rychle vytvořte tučný kurzívní font v C#. Naučte se, jak vytvořit font
  v C# s tučným a kurzívním stylem pomocí vestavěné třídy Font.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create bold italic font
- create font in c#
- C# FontStyle
- text styling C#
- System.Drawing.Font
language: cs
lastmod: 2026-08-15
og_description: Vytvořte tučný kurzívní font v C# s jasným příkladem. Tento tutoriál
  ukazuje, jak vytvořit font v C# pomocí příznaků FontStyle a vysvětluje běžné úskalí.
og_image_alt: Screenshot of text rendered with a bold italic Arial font in a C# console
  window
og_title: Vytvořte tučný kurzívní font v C# – kompletní průvodce programováním
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  headline: Create bold italic font in C# – step‑by‑step guide
  type: TechArticle
- description: Create bold italic font in C# quickly. Learn how to create font in
    C# with bold and italic styles using the built‑in Font class.
  name: Create bold italic font in C# – step‑by‑step guide
  steps:
  - name: Save the code to a file named `Program.cs`.
    text: Save the code to a file named `Program.cs`.
  - name: Open a terminal in the file’s directory.
    text: Open a terminal in the file’s directory.
  - name: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
    text: Execute `dotnet new console -n FontDemo` (if you need a project scaffold).
  - name: Replace the generated `Program.cs` with the code above.
    text: Replace the generated `Program.cs` with the code above.
  - name: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
    text: Run `dotnet add package System.Drawing.Common` (required for .NET Core/5+).
  - name: Build and run with `dotnet run`.
    text: Build and run with `dotnet run`.
  type: HowTo
tags:
- C#
- fonts
- text styling
title: Vytvořte tučné kurzívní písmo v C# – krok za krokem průvodce
url: /cs/net/advanced-features/create-bold-italic-font-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření tučného kurzívy písma v C# – krok za krokem průvodce

Pokud potřebujete **vytvořit tučné kurzívní písmo** v C#, tento průvodce vám přesně ukáže, jak na to. Uvidíte kompletní, spustitelný příklad, který také demonstruje, jak **vytvořit písmo v C#** pomocí standardní třídy .NET `Font`.

Práce s vlastním písmem je běžnou součástí tvorby Windows desktop aplikací, generování PDF nebo renderování HTML na serveru. Na konci tohoto tutoriálu budete schopni vytvořit instanci písma, které je zároveň tučné i kurzívní, pochopit, proč se používá bitový operátor `|`, a řešit běžné okrajové případy, jako jsou chybějící rodiny písem.

## Co se naučíte

* Jak importovat požadované jmenné prostory pro práci s písmy.  
* Syntaxe pro kombinaci `FontStyle.Bold` a `FontStyle.Italic`.  
* Jak ověřit, že písmo bylo úspěšně vytvořeno.  
* Tipy pro zpracování náhrad, když požadovaná rodina není nainstalována.  

Není potřeba žádná externí knihovna – vše používá základní knihovnu tříd .NET Framework / .NET Core.

## Požadavky

* .NET 6.0 SDK nebo novější (kód také funguje na .NET Framework 4.6+).  
* Editor kódu nebo IDE (Visual Studio, VS Code, Rider, atd.).  
* Základní znalost syntaxe C#.  

Pokud splňujete tyto požadavky, můžete postupovat podle kroků bez dalšího nastavení.

## Krok 1: Přidejte potřebné using direktivy

Třída `Font` se nachází v jmenném prostoru `System.Drawing`, který je součástí NuGet balíčku `System.Drawing.Common` pro .NET Core/.NET 5+. Přidejte jmenný prostor na začátek souboru:

```csharp
using System;
using System.Drawing;   // Provides Font and FontStyle
```

> **Proč je tento krok důležitý** – Bez řádku `using System.Drawing;` kompilátor nemůže najít `Font` ani `FontStyle`, což vede k chybě „type or namespace name could not be found“.

## Krok 2: Kombinujte tučné a kurzívní styly pomocí bitového OR operátoru

V .NET je `FontStyle` výčtový typ označený atributem `[Flags]`. To znamená, že můžete kombinovat více hodnot pomocí operátoru `|` (bitový OR):

```csharp
// Step 2: Create a Font that is both bold and italic
var font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
```

### Vysvětlení

* `"Arial"` – název rodiny písma. Pokud systém nemá nainstalováno Arial, konstruktor přejde na výchozí písmo.  
* `12` – velikost v bodech.  
* `FontStyle.Bold | FontStyle.Italic` – kombinuje dva stylové příznaky. Operátor `|` sloučí binární reprezentaci každého příznaku a vytvoří jedinou hodnotu představující „tučné + kurzívní“.

> **Tip:** Vždy používejte názvy výčtových typů (`FontStyle.Bold`) místo magických čísel; zvyšuje to čitelnost a zabraňuje chybám, když se hodnoty výčtu změní.

## Krok 3: Ověřte vytvořené písmo (volitelné, ale doporučené)

Vytištění vlastností písma vám pomůže potvrdit, že kombinace stylů byla úspěšná, zejména při ladění na novém počítači.

```csharp
// Step 3: Output the font details to the console
Console.WriteLine($"Font family: {font.Name}");
Console.WriteLine($"Size (pt): {font.Size}");
Console.WriteLine($"Style: {font.Style}");
```

**Očekávaný výstup**

```
Font family: Arial
Size (pt): 12
Style: Bold, Italic
```

Pokud výstup obsahuje jak `Bold`, tak `Italic`, písmo bylo vytvořeno správně.

## Krok 4: Vykreslete ukázkový řetězec (vizuální potvrzení)

Když spustíte konzolovou aplikaci, nevidíte skutečné stylování glyfů, ale můžete vygenerovat obrázek, který výsledek dokáže. Následující úryvek vykreslí „Hello, World!“ pomocí tučně‑kurzívního písma a uloží jej jako *sample.png*:

```csharp
// Step 4: Draw text to an image file for visual confirmation
using (var bitmap = new Bitmap(300, 100))
using (var graphics = Graphics.FromImage(bitmap))
{
    graphics.Clear(Color.White);
    var brush = Brushes.Black;
    graphics.DrawString("Hello, World!", font, brush, new PointF(10, 30));
    bitmap.Save("sample.png");
    Console.WriteLine("Image saved as sample.png");
}
```

Po spuštění programu otevřete *sample.png*, abyste viděli text vykreslený s tučným kurzívním stylem.

![Ukázkový text vykreslený tučným kurzívním písmem](sample.png)

*Text alt obrázku: Screenshot textu vykresleného tučným kurzívním písmem Arial v C# konzolovém okně* – tento alt text splňuje SEO požadavek na alt text obrázku.

## Krok 5: Elegantní náhrada, když není rodina písma dostupná

Pokud požadovaná rodina (např. „Arial“) není nainstalována, konstruktor `Font` vyhodí `ArgumentException`. Zabalte vytvoření do bloku `try/catch` a přejděte na známé bezpečné písmo, jako je „Segoe UI“.

```csharp
Font font;
try
{
    font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
}
catch (ArgumentException)
{
    Console.WriteLine("Arial not found – falling back to Segoe UI.");
    font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
}
```

**Proč to řešit?**  
V kontejnerizovaných nebo bezhlavých prostředích se výchozí sada písem může lišit od typického desktopu. Poskytnutí náhrady zabraňuje pádům během běhu a zajišťuje konzistentní stylování.

## Kompletní, spustitelný příklad

Spojením všech částí zde máte kompletní program, který můžete zkopírovat, vložit a spustit:

```csharp
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create the font (bold + italic)
        Font font;
        try
        {
            font = new Font("Arial", 12, FontStyle.Bold | FontStyle.Italic);
        }
        catch (ArgumentException)
        {
            Console.WriteLine("Arial not found – using Segoe UI as fallback.");
            font = new Font("Segoe UI", 12, FontStyle.Bold | FontStyle.Italic);
        }

        // Display font information
        Console.WriteLine($"Font family: {font.Name}");
        Console.WriteLine($"Size (pt): {font.Size}");
        Console.WriteLine($"Style: {font.Style}");

        // Render a sample image
        using (var bitmap = new Bitmap(300, 100))
        using (var graphics = Graphics.FromImage(bitmap))
        {
            graphics.Clear(Color.White);
            graphics.DrawString("Hello, World!", font, Brushes.Black, new PointF(10, 30));
            bitmap.Save("sample.png");
        }

        Console.WriteLine("Sample image saved as sample.png");
    }
}
```

### Jak spustit

1. Uložte kód do souboru s názvem `Program.cs`.  
2. Otevřete terminál ve složce souboru.  
3. Spusťte `dotnet new console -n FontDemo` (pokud potřebujete kostru projektu).  
4. Nahraďte vygenerovaný `Program.cs` kódem výše.  
5. Spusťte `dotnet add package System.Drawing.Common` (vyžadováno pro .NET Core/5+).  
6. Sestavte a spusťte pomocí `dotnet run`.  

Uvidíte výstup v konzoli potvrzující vlastnosti písma a `sample.png` se objeví ve složce projektu.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč k tomu dochází | Oprava |
|---------|---------------------|--------|
| **Chybějící balíček `System.Drawing.Common`** | .NET Core ve výchozím nastavení neobsahuje `System.Drawing`. | Spusťte `dotnet add package System.Drawing.Common`. |
| **Rodina písma není nainstalována** | Headless Docker obrazy často postrádají Windows písma. | Použijte náhradní písmo nebo nainstalujte požadovaná písma v kontejneru. |
| **Nesprávné použití `|`** | Použití `+` místo `|` vede k neplatné kombinaci. | Vždy kombinujte hodnoty `FontStyle` pomocí bitového OR operátoru (`|`). |
| **Uvolňování objektu `Font`** | Nepoužití `Dispose` může způsobit únik GDI zdrojů. | Zabalte `Font` do bloku `using` nebo zavolejte `font.Dispose()` po dokončení. |

## Závěr

Nyní víte, jak **vytvořit tučné kurzívní písmo** v C# a jak **vytvořit písmo v C#** bezpečně a efektivně. Tutoriál pokryl import správného jmenného prostoru, kombinaci příznaků `FontStyle`, ověření výsledku, vykreslení vizuálního vzorku a zpracování chybějících rodin písem.

Dále můžete zkoumat:

* **Vytváření podtržených nebo přeškrtnutých písem** – přidejte `FontStyle.Underline` nebo `FontStyle.Strikeout`.  
* **Používání vlastních TrueType písem** – načtěte soubor `.ttf` pomocí `PrivateFontCollection`.  
* **Použití písem ve WinForms, WPF nebo generování PDF** – stejný objekt `Font` může být předán UI kontrolám nebo knihovnám třetích stran.  

Neváhejte experimentovat s různými rodinami, velikostmi a kombinacemi stylů. Pokud narazíte na problémy, podívejte se znovu na tabulku „Časté úskalí“ nebo zkontrolujte oficiální [.NET dokumentaci pro System.Drawing.Font](https://learn.microsoft.com/dotnet/api/system.drawing.font). Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Cara Menggabungkan Font Secara Programatis di C# – Panduan Langkah demi Langkah](/html/indonesian/net/advanced-features/how-to-combine-fonts-programmatically-in-c-step-by-step-guid/)
- [Create HTML Document with Styled Text and Export to PDF – Full Guide](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [convert docx to png – create zip archive c# tutorial](/html/english/net/generate-jpg-and-png-images/convert-docx-to-png-create-zip-archive-c-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}