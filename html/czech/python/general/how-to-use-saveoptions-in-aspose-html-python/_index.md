---
category: general
date: 2026-07-27
description: Jak použít SaveOptions v Aspose.HTML (Python) k převodu velké HTML stránky
  a efektivnímu zpracování zdrojů.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: cs
lastmod: 2026-07-27
og_description: Jak použít SaveOptions v Aspose.HTML (Python) vám umožní převést velkou
  HTML stránku a zároveň aplikovat správu zdrojů pro čisté a rychlé výsledky.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Jak používat SaveOptions v Aspose.HTML – Průvodce pro Python
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Jak použít SaveOptions v Aspose.HTML (Python)
url: /cs/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat SaveOptions v Aspose.HTML (Python)

Jak používat SaveOptions v Aspose.HTML pro Python je otázka, kterou si klade mnoho vývojářů při práci s obrovskými HTML soubory. Pokud potřebujete **převést velkou HTML stránku** a zároveň mít pevnou kontrolu nad **aplikací správy zdrojů**, jste na správném místě.  

V tomto tutoriálu projdeme reálný scénář: vezmeme objemnou HTML stránku, omezíme, jak hluboko se mají načítat vnořené zdroje, a nakonec výsledek uložíme (nebo převedeme) s naprosto jasnou kontrolou. Žádné vágní odkazy, jen kompletní, spustitelný příklad, který můžete dnes zkopírovat a vložit do svého projektu.

> **Pro tip:** `SaveOptions` v Aspose.HTML funguje nejen pro ukládání zpět do HTML, ale také pro převod do PDF, PNG nebo dokonce DOCX. Stejný vzor, který níže popisujeme, platí pro všechny tyto formáty.

---

## Co budete potřebovat

- **Python 3.8+** (kód používá typové nápovědy, ale běží na jakékoli aktuální verzi)  
- **Aspose.HTML for Python via .NET** – nainstalujte pomocí `pip install aspose-html`  
- **Velký HTML soubor**, který chcete zmenšit nebo transformovat (v příkladu se používá `big_page.html`)  
- Přiměřené množství volného místa na disku pro výstupní soubor  

To je vše — žádné další knihovny, žádné těžkopádné nástroje pro sestavování.

---

## Jak používat SaveOptions s možnostmi správy zdrojů

Toto je podstata věci. Vytvoříme instanci `SaveOptions`, připojíme objekt `ResourceHandlingOptions`, který říká Aspose.HTML, jak hluboko má sledovat propojené zdroje, a poté vše předáme metodě `save` dokumentu.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Proč to funguje:**  
- `HTMLDocument` načte původní soubor a parsuje každý `<img>`, `<link>`, `<script>` atd.  
- `ResourceHandlingOptions.max_handling_depth` říká enginu, aby po třech úrovních vnoření přestal sledovat další zdroje — ideální pro zamezení nekonečných smyček na stránkách, které vkládají jiné stránky.  
- `SaveOptions` je nosič, který přenáší jak výstupní formát (standardně HTML), tak pravidla správy zdrojů.  
- Nakonec `doc.save` zapíše nový soubor s aplikovanými pravidly.

Když spustíte skript, uvidíte nový soubor na `big_page_processed.html`. Otevřete jej v prohlížeči; všimnete si, že všechny obrázky, styly a skripty do třetí úrovně vnoření jsou stále přítomny, zatímco hlubší odkazy byly odstraněny. To dramaticky snižuje velikost souboru, aniž by se narušilo základní rozložení stránky — právě to, co potřebujete, když **převádíte velkou HTML stránku** pro offline použití nebo e‑mailové doručení.

---

## Efektivní převod velké HTML stránky

Pokud je vaším cílem *převést velkou HTML stránku* na úspornější verzi, výše uvedený úryvek už provádí většinu těžké práce. Můžete však chtít změnit výstupní formát úplně. Aspose.HTML to umožňuje jedním řádkem:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Stačí nahradit vlastnost `format` hodnotou `"PNG"`, `"JPEG"` nebo `"DOCX"` a máte kompletní převodní řetězec. Stejná pravidla **aplikace správy zdrojů** zůstávají zachována, takže výsledné PDF neobsahuje každý externí CSS soubor z původního webu — pouze ty, které spadají do tříúrovňové hloubky, kterou jste definovali.

---

## Aplikace správy zdrojů na vnořené zdroje

Ponořme se trochu hlouběji do **aplikace správy zdrojů**. Předpokládejme, že vaše HTML obsahuje stylový list, který sám importuje další stylové listy, z nichž každý načítá obrázky. Bez omezení hloubky by Aspose.HTML mohl sledovat řetězec donekonečna, což by nafoukl paměť a využití CPU.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Hloubka 0** – Žádné externí zdroje nejsou načteny; získáte kostru HTML bez jakýchkoli doplňků.  
- **Hloubka 1** – Jsou zahrnuty pouze zdroje první úrovně (přímé `<img>` tagy, okamžité CSS soubory).  
- **Hloubka 2+** – Respektuje se hlubší vnoření, užitečné pro složité stránky, kde styly závisí na dalších stylech.

Vyberte hloubku, která odpovídá vašemu scénáři **převodu velké HTML stránky**. Pro e‑mailové newslettery stačí často hloubka 1. Pro lokální archiv poskytuje hloubka 3 (jako v hlavním příkladu) pěknou rovnováhu.

---

## Kompletní funkční příklad – od začátku do konce

Níže je samostatný skript, který můžete umístit do souboru s názvem `process_html.py`. Obsahuje ošetření chyb, logování a malý pomocník, který vypíše úsporu velikosti, kterou jste dosáhli.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Očekávaný výstup (konzole):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Otevřete zpracovaný soubor; uvidíte úspornější stránku, která stále vypadá jako originál. Pokud změníte `fmt` na `"PDF"`, konzole zobrazí velikost PDF souboru a můžete jej otevřít v libovolném PDF prohlížeči.

---

## Často kladené otázky a okrajové případy

- **Co když stránka odkazuje na zdroje přes HTTPS, které vyžadují autentizaci?**  
  Aspose.HTML následuje přesměrování, ale automaticky neodesílá přihlašovací údaje. Můžete si tyto assety předem stáhnout nebo použít vlastní `WebRequest` handler (mimo rozsah tohoto návodu).

- **Mohu zachovat inline CSS a přitom odstranit externí soubory?**  
  Ano — nastavte `resource_options.max_handling_depth = 0`. Tím se přeskočí externí soubory, ale jakékoli `<style>` bloky zůstanou nedotčeny.

- **Co s velmi velkými obrázky, které stále zvětšují výstup?**  
  Po uložení můžete provést druhý průchod pomocí Pillow a obrázky zmenšit, nebo nechat Aspose.HTML použít vestavěné možnosti komprese obrázků (použijte `save_options.image_quality`).

- **Je limit hloubky aplikován na každý typ zdroje zvlášť?**  
  Limit je globální napříč všemi typy zdrojů (obrázky, skripty, styly). Pokud potřebujete jemnější kontrolu, musíte po načtení dokumentu ručně filtrovat zdroje.

---

## Závěr

Nyní máte pevné pochopení **jak používat SaveOptions** v Aspose.HTML


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [Jak převést HTML do PDF v Javě – Použití Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Jak převést HTML do MHTML s Aspose.HTML pro Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [Jak použít Aspose k renderování HTML do PNG – Krok za krokem](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}