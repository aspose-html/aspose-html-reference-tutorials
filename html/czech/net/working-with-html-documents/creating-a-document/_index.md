---
title: Vytvoření dokumentu HTML v .NET pomocí Aspose.HTML
linktitle: Vytvoření dokumentu HTML v .NET
second_title: Aspose.HTML .NET API pro manipulaci s HTML
description: Naučte se vytvářet HTML dokumenty v .NET pomocí Aspose.HTML, od začátku nebo z URL. Komplexní návod pro webové vývojáře.
weight: 10
url: /cs/net/working-with-html-documents/creating-a-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření dokumentu HTML v .NET pomocí Aspose.HTML


V oblasti vývoje webu a manipulace s daty je nezbytný výkonný nástroj pro vytváření, úpravy a práci s dokumenty HTML. Aspose.HTML for .NET je jedním z takových nástrojů, který může zjednodušit vaše úkoly související s HTML. V tomto komplexním tutoriálu prozkoumáme, jak krok za krokem vytvářet HTML dokumenty pomocí Aspose.HTML for .NET. Než se ponoříme do příkladů, pokryjeme některé předpoklady.

## Předpoklady

Než se vydáte na tuto cestu, ujistěte se, že máte splněny následující předpoklady:

1. Visual Studio: Ujistěte se, že máte v systému nainstalované Visual Studio.

2. Aspose.HTML for .NET: Stáhněte a nainstalujte knihovnu Aspose.HTML for .NET. Odkaz ke stažení najdete[zde](https://releases.aspose.com/html/net/).

3. Základní znalost C#: Seznamte se se základy programovacího jazyka C#.

Nyní, když máme pokryty předpoklady, začněme s vytvářením HTML dokumentů.

## Import jmenných prostorů

Nejprve musíte importovat potřebné jmenné prostory pro použití Aspose.HTML ve vašem projektu C#. Pomocí direktiv přidejte do souboru kódu následující:

```csharp
using Aspose.Html.Dom.Svg;
using Aspose.Html;
```

## Vytvoření dokumentu SVG

```csharp
static void CreateSVG()
{
    using (var document = new SVGDocument("<svg xmlns='http://www.w3.org/2000/svg'><circle cx='50' cy='50' r='40'/></svg>", "about:blank"))
    {
        // Zde provádějte akce s dokumentem SVG...
    }
}
```

 V tomto příkladu vytvoříme dokument SVG poskytnutím obsahu SVG a základní adresy URL. The`SVGDocument` třída z Aspose.HTML pro .NET vám umožňuje bez námahy manipulovat s dokumenty SVG.

## Vytvoření dokumentu HTML od nuly

```csharp
static void FromScratch()
{
    using (var document = new HTMLDocument())
    {
        // Zde provádějte akce s dokumentem HTML...
    }
}
```

 Tento příklad ukazuje, jak vytvořit dokument HTML od začátku. The`HTMLDocument`class poskytuje prázdné plátno pro váš obsah HTML.

## Vytvoření dokumentu HTML z místního souboru

```csharp
static void FromLocalFile()
{
    string dataDir = "Your Data Directory";
    using (var document = new HTMLDocument(dataDir + "input.html"))
    {
        // Zde provádějte akce s dokumentem HTML...
    }
}
```

 Pokud máte ve svém lokálním systému existující soubor HTML, můžete jej načíst pomocí`HTMLDocument` třídy, jak ukazuje tento příklad.

## Vytvoření dokumentu HTML ze vzdálené adresy URL

```csharp
static void FromRemoteURL()
{
    using (var document = new HTMLDocument("http://vase.stranky.com/"))
    {
        // Zde provádějte akce s dokumentem HTML...
    }
}
```

Někdy může být nutné pracovat s obsahem HTML hostovaným na vzdáleném serveru. Tento příklad ukazuje, jak vytvořit dokument HTML ze vzdálené adresy URL.

## Vytvoření dokumentu HTML ze vzdálené adresy URL (alternativa)

```csharp
static void FromRemoteURL1()
{
    using (var document = new HTMLDocument(new Url("http://vase.stranky.com/")))
    {
        // Zde provádějte akce s dokumentem HTML...
    }
}
```

Tento alternativní přístup také ukazuje, jak vytvořit dokument HTML ze vzdálené adresy URL pomocí jiného konstruktoru.

## Vytvoření dokumentu HTML z obsahu HTML

```csharp
static void FromHTML()
{
    using (var document = new HTMLDocument("<p>my first paragraph</p>", "."))
    {
        // Zde provádějte akce s dokumentem HTML...
    }
}
```

Pokud máte obsah HTML ve formátu řetězce, můžete s ním vytvořit dokument HTML, jak ukazuje tento příklad.

## Vytvoření dokumentu HTML ze streamu

```csharp
static void FromStream()
{
    using (MemoryStream mem = new MemoryStream())
    using (StreamWriter sw = new StreamWriter(mem))
    {
        sw.Write("<p>my first paragraph</p>");
        sw.Flush();
        mem.Seek(0, SeekOrigin.Begin);
        using (var document = new HTMLDocument(mem, "about:blank"))
        {
            // Zde provádějte akce s dokumentem HTML...
        }
    }
}
```

tomto příkladu si ukážeme, jak vytvořit dokument HTML z dat v toku paměti. To může být užitečné, když máte ve streamu obsah HTML a chcete s ním manipulovat.

## Závěr

Aspose.HTML for .NET poskytuje výkonnou sadu nástrojů pro vytváření a práci s dokumenty HTML ve vašich aplikacích .NET. Pomocí příkladů uvedených v tomto kurzu můžete snadno začít s vytvářením dokumentů HTML, ať už od začátku, místních souborů, vzdálených adres URL nebo existujícího obsahu HTML.

 Máte otázky nebo potřebujete pomoc? Navštivte fórum komunity Aspose.HTML pro podporu na adrese[https://forum.aspose.com/](https://forum.aspose.com/).

## Nejčastější dotazy

### Q1: Je Aspose.HTML pro .NET zdarma k použití?
 Odpověď 1: Aspose.HTML for .NET nabízí bezplatnou zkušební verzi, ale pro plné využití si budete muset zakoupit licenci. Více podrobností najdete na[https://purchase.aspose.com/buy](https://purchase.aspose.com/buy).

### Q2: Jak mohu získat dočasnou licenci pro Aspose.HTML pro .NET?
 A2: Pokud potřebujete dočasnou licenci, můžete ji získat na[https://purchase.aspose.com/temporary-license/](https://purchase.aspose.com/temporary-license/).

### Q3: Kde najdu dokumentaci pro Aspose.HTML pro .NET?
A3: Dokumentaci lze nalézt na[https://reference.aspose.com/html/net/](https://reference.aspose.com/html/net/).

### Q4: Existují nějaké další knihovny Aspose pro vývoj .NET?
 Odpověď 4: Ano, Aspose poskytuje řadu knihoven pro různé formáty souborů a úlohy manipulace s dokumenty. Podívejte se na jejich nabídku na[https://products.aspose.com/](https://products.aspose.com/).

### Q5: Mohu použít Aspose.HTML pro .NET ve svých webových aplikacích?
Odpověď 5: Ano, Aspose.HTML for .NET je kompatibilní s webovými aplikacemi, což z něj činí univerzální volbu pro desktopové i webové projekty.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
