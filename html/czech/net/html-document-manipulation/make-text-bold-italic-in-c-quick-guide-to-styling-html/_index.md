---
category: general
date: 2026-02-13
description: Programově vytvořte tučný a kurzívní text v C#. Naučte se používat GetElementsByTagName,
  nastavit styl písma, načíst HTML dokument a získat první odstavec.
draft: false
keywords:
- make text bold italic
- use getelementsbytagname
- set font style programmatically
- load html document c#
- get first paragraph element
language: cs
og_description: Okamžitě vytvořte tučný a kurzívní text v C#. Tento tutoriál ukazuje,
  jak použít GetElementsByTagName, programově nastavit styl písma, načíst HTML dokument
  a získat první odstavec.
og_title: Ztučte a kurzivujte text v C# – Rychlé, stylování založené na kódu
tags:
- C#
- Aspose.Html
- HTML manipulation
title: Ztučte a kurzivujte text v C# – Rychlý průvodce stylováním HTML
url: /cs/net/html-document-manipulation/make-text-bold-italic-in-c-quick-guide-to-styling-html/
---

are placeholders but not fenced code blocks. The requirement says preserve code blocks fenced. There are none besides placeholders. So fine.

Make sure we didn't miss any text.

Let's produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ztučte a kurzívu text v C# – Rychlý průvodce stylováním HTML

Už jste někdy potřebovali **ztučit a kurzívu text** v HTML souboru z C# aplikace? Nejste sami; je to častý požadavek při generování reportů, e‑mailů nebo dynamických webových útržků. Dobrá zpráva? Můžete to dosáhnout během několika řádků pomocí Aspose.HTML.

V tomto tutoriálu vás provedeme načtením HTML dokumentu, vyhledáním prvního elementu `<p>` pomocí `GetElementsByTagName` a následným **nastavením stylu písma programově**, aby se text stal zároveň tučným a kurzívou. Na konci budete mít kompletní spustitelný úryvek a pevné pochopení podkladového API.

## Co budete potřebovat

- **Aspose.HTML for .NET** (jakákoli aktuální verze; API, které používáme, funguje s .NET 6+)
- Základní vývojové prostředí C# (Visual Studio, Rider nebo VS Code)
- HTML soubor pojmenovaný `sample.html` umístěný ve složce, kterou ovládáte  
  (odkazujeme na něj pomocí `YOUR_DIRECTORY/sample.html`)

Žádné další NuGet balíčky nejsou potřeba kromě Aspose.HTML a kód běží na Windows, Linuxu nebo macOS.

---

## Krok 1: Načtení HTML dokumentu v C#

První věc, kterou musíte udělat, je načíst HTML soubor do paměti. Třída `HtmlDocument` z Aspose.HTML provádí těžkou práci.

```csharp
using Aspose.Html;
using Aspose.Html.Drawing;

// Replace YOUR_DIRECTORY with the actual path where sample.html lives
string htmlPath = Path.Combine("YOUR_DIRECTORY", "sample.html");

// Load the HTML document from the file system
HtmlDocument htmlDoc = new HtmlDocument(htmlPath);
```

**Proč je to důležité:**  
Načtení dokumentu vám poskytne objektový model podobný DOM, který můžete dotazovat a měnit. Je to základ pro jakoukoli následnou práci se stylem.

> **Tip:** Pokud soubor nemusí existovat, zabalte načítání do `try/catch` a ošetřete `FileNotFoundException` elegantně.

---

## Krok 2: Vyhledání prvního elementu `<p>` pomocí `GetElementsByTagName`

Pro změnu stylu konkrétního odstavce potřebujeme odkaz na tento uzel. `GetElementsByTagName` vrací živou kolekci; získání první položky je jednoduché.

```csharp
// Get all <p> elements and pick the first one
var paragraphs = htmlDoc.GetElementsByTagName("p");

// Safety check – ensure at least one <p> exists
if (paragraphs.Length == 0)
{
    Console.WriteLine("No <p> elements found in the document.");
    return;
}

// This is the element we will style
var firstParagraph = paragraphs[0];
```

**Proč použít `GetElementsByTagName`?**  
Jedná se o známou metodu podle standardu DOM, která funguje bez ohledu na složitost dokumentu. Můžete také použít CSS selektory, ale `GetElementsByTagName` je naprosto jasná pro „získat první element odstavce“.

---

## Krok 3: Použití kombinovaného tučného a kurzívního stylu pomocí `WebFontStyle`

Aspose.HTML poskytuje výčtový typ `WebFontStyle`, který umožňuje bitové kombinování stylů. Pro ztučení a kurzívu textu **bold italic** použijeme bitový OR obou příznaků.

```csharp
// Apply both Bold and Italic styles at once
firstParagraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;
```

Pod povrchem to nastaví odpovídající CSS `font-weight: bold; font-style: italic;`. Výčet zajišťuje typovou bezpečnost kódu a eliminuje chyby v řetězcích.

## Krok 4: Uložení upraveného dokumentu (volitelné)

Pokud potřebujete změny uložit, jednoduše zavolejte `Save`. Můžete výstup uložit do jiného HTML souboru nebo dokonce do PDF, podle vašich následných potřeb.

```csharp
// Save the updated HTML to a new file
string outputPath = Path.Combine("YOUR_DIRECTORY", "sample_modified.html");
htmlDoc.Save(outputPath);

Console.WriteLine($"Document saved to {outputPath}");
```

**Výsledek, který uvidíte:**  
Otevřete `sample_modified.html` v libovolném prohlížeči a první odstavec se zobrazí **tučně a kurzívou**. Veškerý ostatní obsah zůstane nedotčený.

---

## Kompletní funkční příklad

Spojením všeho dohromady zde máte kompletní program, který můžete zkopírovat a vložit do konzolové aplikace:

```csharp
using System;
using System.IO;
using Aspose.Html;
using Aspose.Html.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the HTML document
        string htmlPath = Path.Combine("YOUR_DIRECTORY", "sample.html");
        HtmlDocument htmlDoc = new HtmlDocument(htmlPath);

        // 2️⃣ Locate the first <p> element
        var paragraphs = htmlDoc.GetElementsByTagName("p");
        if (paragraphs.Length == 0)
        {
            Console.WriteLine("No <p> elements found.");
            return;
        }
        var firstParagraph = paragraphs[0];

        // 3️⃣ Make text bold italic
        firstParagraph.Style.FontStyle = WebFontStyle.Bold | WebFontStyle.Italic;

        // 4️⃣ Save the result (optional)
        string outputPath = Path.Combine("YOUR_DIRECTORY", "sample_modified.html");
        htmlDoc.Save(outputPath);

        Console.WriteLine($"Successfully made text bold italic and saved to {outputPath}");
    }
}
```

**Očekávaný výstup v konzoli:**

```
Successfully made text bold italic and saved to YOUR_DIRECTORY\sample_modified.html
```

Otevřete uložený soubor a ověřte, že první odstavec nyní vypadá takto:

> *Toto je první odstavec – měl by být **bold italic**.*

---

## Často kladené otázky a okrajové případy

### Co když HTML neobsahuje žádné tagy `<p>`?

Bezpečnostní kontrola v Kroku 2 již vypíše přátelskou zprávu a ukončí se. V produkci můžete místo ukončení vytvořit nový element `<p>`.

### Můžu stylovat více odstavců najednou?

Určitě. Projděte `paragraphs` ve smyčce a aplikujte stejný `FontStyle`:

```csharp
foreach (var p in paragraphs)
{
    p.Style.FontWeight = FontWeight.Bold;
    p.Style.FontStyle = FontStyle.Italic;
}
```

### Jak kombinovat jiné styly, například podtržení?

`WebFontStyle` pokrývá pouze tloušťku a sklon. Pro podtržení nastavíte CSS vlastnost `text-decoration`:

```csharp
firstParagraph.Style.TextDecoration = TextDecoration.Underline;
```

### Funguje to s HTML5 tagy jako `<section>`?

`GetElementsByTagName` funguje s libovolným názvem tagu, takže můžete cílit na `<section>`, `<div>` nebo vlastní tagy stejně snadno.

### Je změna viditelná v prohlížečích, které nepodporují CSS?

Protože API zapisuje standardní CSS vlastnosti, jakýkoli moderní prohlížeč vykreslí tučně‑kurzívní styl správně. Starší prohlížeče, které ignorují `font-weight` nebo `font-style`, jsou vzácné a mimo rozsah většiny .NET projektů.

---

## Pro tipy a běžné úskalí

- **Nezapomeňte na importy jmenných prostorů.** Chybějící `using Aspose.Html.Drawing;` vede k chybě kompilace pro `WebFontStyle`.
- **Zpracování cest:** Použijte `Path.Combine`, abyste se vyhnuli pevně zakódovaným oddělovačům; udržuje kód multiplatformní.
- **Výkon:** U velkých dokumentů používejte `GetElementsByTagName` střídmě. Pokud potřebujete jen první odstavec, můžete po jeho nalezení smyčku ukončit.
- **Formát ukládání:** Pokud později potřebujete PDF, nahraďte `htmlDoc.Save(outputPath);` za `htmlDoc.Save(outputPath, SaveFormat.Pdf);` (vyžaduje PDF add‑on).

---

## Závěr

Nyní víte, jak **ztučit a kurzívu text** v HTML souboru pomocí C#. Načtením dokumentu, použitím `GetElementsByTagName` k **získání prvního elementu odstavce** a **nastavením stylu písma programově** získáte detailní kontrolu nad libovolným HTML obsahem.  

Od tady můžete experimentovat s dalšími možnostmi stylování, zpracovávat více uzlů nebo dokonce převést stylovaný HTML do PDF pro účely reportování. Stejný vzor – načíst, najít, stylovat, uložit – platí prakticky pro jakýkoli úkol manipulace s DOM v Aspose.HTML.

Máte další otázky ohledně manipulace s HTML v C#? Neváhejte prozkoumat související témata jako *load html document c#*, *use GetElementsByTagName* nebo *set font style programmatically* pro podrobnější pohled. Šťastné kódování!

![příklad ztučněného a kurzívního textu](image.png "Snímek obrazovky ukazující odstavec zobrazený tučně a kurzívou po aplikaci stylu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}