---
category: general
date: 2026-08-19
description: Vytvořte možnosti zpracování zdrojů v Pythonu a naučte se, jak načíst
  HTML dokument, dokonce i velkou HTML stránku, pomocí Aspose.HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to load html document
- load large html page
language: cs
lastmod: 2026-08-19
og_description: Vytvořte možnosti správy zdrojů v Pythonu a podívejte se, jak načíst
  HTML dokument, včetně velkých HTML stránek, pomocí Aspose.HTML.
og_image_alt: Screenshot of Python code that creates resource handling options and
  loads a large HTML page
og_title: Vytvořte možnosti správy zdrojů a načtěte HTML dokument – průvodce Pythonem
schemas:
- author: Aspose
  dateModified: '2026-08-19'
  description: Create resource handling options in Python and learn how to load an
    HTML document, even a large HTML page, with Aspose.HTML.
  headline: Create resource handling options and load an HTML document in Python
  type: TechArticle
- description: Create resource handling options in Python and learn how to load an
    HTML document, even a large HTML page, with Aspose.HTML.
  name: Create resource handling options and load an HTML document in Python
  steps:
  - name: Verify that the page loaded successfully
    text: 'A quick way to confirm that the document is ready is to print the number
      of child nodes in the root element:'
  - name: 1. Missing resources
    text: 'When a linked CSS or JS file is unavailable, Aspose.HTML silently skips
      it but logs a warning. To capture these warnings, enable logging:'
  - name: 2. Circular references
    text: Even with a depth limit, circular references can cause the parser to waste
      time. If you notice unusually long load times, consider reducing `max_handling_depth`
      to `2` or `1`.
  - name: 3. Very large pages (> 10 MB)
    text: 'For extremely large pages, increase Python’s recursion limit **only if**
      you have verified that the depth is safe:'
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML processing
title: Vytvořte možnosti zpracování zdrojů a načtěte HTML dokument v Pythonu
url: /cs/python/general/create-resource-handling-options-and-load-an-html-document-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvořte možnosti zpracování zdrojů a načtěte HTML dokument v Pythonu

Pokud potřebujete **vytvořit možnosti zpracování zdrojů** pro import HTML, tento návod vám přesně ukáže, jak na to. Ať už pracujete s menší stránkou nebo s *velkou HTML stránkou*, která načítá mnoho externích zdrojů, níže uvedené kroky vám umožní řídit hloubku, vyhnout se kruhovým odkazům a udržet předvídatelnou spotřebu paměti.

V tomto tutoriálu se naučíte **jak načíst soubory HTML dokumentu** pomocí Aspose.HTML pro Python, nakonfigurovat maximální hloubku zpracování a ověřit, že se stránka načte, aniž by vyčerpala zdroje. Přístup funguje pro jakýkoli HTML zdroj, od jednoduchých statických souborů po složité stránky, které odkazují na desítky skriptů, stylových listů a obrázků.

## Co budete potřebovat

- Python 3.8 nebo novější nainstalovaný.  
- Balíček `aspose-html` (nainstalujte pomocí `pip install aspose-html`).  
- Lokální HTML soubor (např. `big_page.html`), který chcete otestovat.  
- Základní znalost Pythonu a načítání HTML zdrojů.  

Tyto předpoklady zajišťují, že kód běží beze změn na Windows, macOS nebo Linuxu.

## Krok 1: Vytvořte možnosti zpracování zdrojů

Prvním krokem je **vytvořit možnosti zpracování zdrojů**. Tento objekt říká Aspose.HTML, jak zacházet s propojenými zdroji (CSS, JS, obrázky) při parsování dokumentu.

```python
# Step 1: Import the Aspose.HTML library
from aspose.html import *

# Step 2: Instantiate the options container
# This is where we will configure resource handling behavior.
resource_options = ResourceHandlingOptions()
```

> **Proč je to důležité:** Bez explicitních možností Aspose.HTML následuje každý odkaz, na který narazí, což může vést k nekonečné rekurzi na stránkách, které se navzájem odkazují. Vytvořením objektu možností získáte detailní kontrolu nad procesem importu.

## Krok 2: Omezte hloubku zpracování

Aby se zabránilo nekontrolovaným síťovým voláním, nastavte maximální hloubku. Hloubka `3` je bezpečná výchozí hodnota pro většinu webů, umožňující hlavní stránku a dvě úrovně vnořených zdrojů.

```python
# Step 3: Limit the depth to three levels
resource_options.max_handling_depth = 3
```

- **Hloubka 1** – samotný HTML soubor.  
- **Hloubka 2** – zdroje přímo odkazované HTML (např. značky `<link>` nebo `<script>`).  
- **Hloubka 3** – zdroje odkazované těmito prvními úrovněmi aktiv (např. importy CSS uvnitř stylového listu).  

Nastavení `max_handling_depth` zastaví parser po třech skocích, což je zvláště užitečné, když **načítáte velké HTML stránky**, které obsahují mnoho knihoven třetích stran.

## Krok 3: Načtěte HTML dokument (jak načíst html dokument)

Nyní, když jsou možnosti připravené, můžete **načíst HTML dokument**. Předávejte nakonfigurované `resource_options` konstruktoru `HTMLDocument`.

```python
# Step 4: Load the HTML document using the configured options
doc = HTMLDocument(
    "YOUR_DIRECTORY/big_page.html",
    resource_handling_options=resource_options
)
```

> **Vysvětlení:** Třída `HTMLDocument` načte soubor, vyřeší zdroje podle limitu hloubky a vytvoří DOM, který můžete dotazovat nebo renderovat. Pokud soubor neexistuje nebo je cesta špatná, Aspose.HTML vyvolá `FileNotFoundError`.

### Ověřte, že se stránka načetla úspěšně

Rychlý způsob, jak potvrdit, že je dokument připraven, je vypsat počet podřízených uzlů v kořenovém elementu:

```python
print(f"Root has {len(doc.root.child_nodes)} child nodes.")
```

Pokud výstup ukazuje nenulový počet, parser byl úspěšný. Pro *velkou HTML stránku* můžete také chtít zkontrolovat počet externích zdrojů, které byly skutečně staženy:

```python
fetched = doc.resource_handling_options.fetched_resources
print(f"Fetched {len(fetched)} external resources (max depth = {resource_options.max_handling_depth}).")
```

## Řešení okrajových případů a běžných úskalí

### 1. Chybějící zdroje

Když je propojený CSS nebo JS soubor nedostupný, Aspose.HTML jej tiše přeskočí, ale zaznamená varování. Pro zachycení těchto varování povolte logování:

```python
import logging
logging.basicConfig(level=logging.WARNING)
```

### 2. Kruhové reference

I když je nastaven limit hloubky, kruhové reference mohou způsobit ztrátu času parseru. Pokud zaznamenáte neobvykle dlouhé načítání, zvažte snížení `max_handling_depth` na `2` nebo `1`.

### 3. Velmi velké stránky (> 10 MB)

Pro extrémně velké stránky zvyšte limit rekurze v Pythonu **pouze pokud** jste ověřili, že hloubka je bezpečná:

```python
import sys
sys.setrecursionlimit(2000)  # optional, use with caution
```

Nicméně doporučený přístup je udržet hloubku nízkou a nechat možnosti filtrovat zbytečné assety.

## Kompletní spustitelný příklad

Níže je kompletní skript, který můžete zkopírovat a vložit do souboru pojmenovaného `load_html.py`. Upravit cestu k souboru tak, aby ukazovala na váš vlastní HTML soubor.

```python
# load_html.py
# Demonstrates how to create resource handling options,
# limit handling depth, and load a large HTML page with Aspose.HTML.

from aspose.html import *
import logging
import sys

# Optional: show warnings about missing resources
logging.basicConfig(level=logging.WARNING)

def main():
    # 1️⃣ Create and configure resource handling options
    resource_options = ResourceHandlingOptions()
    resource_options.max_handling_depth = 3  # limit to three levels

    # 2️⃣ Load the HTML document using the options
    html_path = "YOUR_DIRECTORY/big_page.html"  # <-- replace with your file
    doc = HTMLDocument(html_path, resource_handling_options=resource_options)

    # 3️⃣ Verify the load
    print(f"Root has {len(doc.root.child_nodes)} child nodes.")
    fetched = doc.resource_handling_options.fetched_resources
    print(f"Fetched {len(fetched)} external resources (max depth = {resource_options.max_handling_depth}).")

    # Optional: increase recursion limit for huge documents (use with care)
    # sys.setrecursionlimit(2000)

if __name__ == "__main__":
    main()
```

Spuštění skriptu:

```bash
python load_html.py
```

**Očekávaný výstup** (příklad pro středně velkou stránku):

```
Root has 12 child nodes.
Fetched 8 external resources (max depth = 3).
```

Pro skutečně masivní stránku budou čísla vyšší, ale skript i nadále bude respektovat nastavený limit hloubky.

## Nejlepší postupy a další kroky

- **Znovupoužití možností:** Pokud zpracováváte mnoho stránek najednou, vytvořte jedinou instanci `ResourceHandlingOptions` a znovu ji použijte, abyste se vyhnuli zbytečnému vytváření objektů.  
- **Kombinujte s renderováním:** Po načtení můžete DOM renderovat do PDF, obrázku nebo dokonce sanitizovaného HTML řetězce pomocí `HTMLRenderer` z Aspose.HTML.  
- **Prozkoumejte další možnosti:** `ResourceHandlingOptions` vám také umožňuje definovat vlastní download handlery, nastavit časové limity nebo whitelist/blacklist domény. To je užitečné, když potřebujete **načíst velké HTML stránky** z nedůvěryhodných zdrojů.

## Závěr

Nyní víte, jak **vytvořit možnosti zpracování zdrojů**, nakonfigurovat bezpečnou hloubku a **načíst HTML dokument**—včetně *velkých HTML stránek*—s Aspose.HTML pro Python. Omezením hloubky zpracování chráníte svou aplikaci před nekontrolovanými síťovými požadavky a zároveň získáte nezbytné zdroje potřebné pro přesné vykreslení.

Neváhejte experimentovat s různými hodnotami hloubky, vlastními download handlery nebo integrovat načtený DOM do následných zpracovatelských pipeline, jako je generování PDF nebo analýza obsahu. Šťastné programování!

## What Should You Learn Next?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak renderovat HTML – Kompletní průvodce s vlastním handlerem zdrojů](/html/english/net/rendering-html-documents/how-to-render-html-complete-guide-with-custom-resource-handl/)
- [Načíst HTML pomocí URL v .NET s Aspose.HTML](/html/english/net/html-document-manipulation/load-html-using-url/)
- [Načíst HTML pomocí vzdáleného serveru v .NET s Aspose.HTML](/html/english/net/html-document-manipulation/load-html-using-remote-server/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}