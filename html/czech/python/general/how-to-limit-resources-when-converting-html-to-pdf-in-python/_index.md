---
category: general
date: 2026-08-15
description: Jak omezit zdroje při převodu HTML na PDF pomocí Pythonu. Naučte se exportovat
  HTML do PDF s řízenou hloubkou zdrojů.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to limit resources
- convert html to pdf
- export html to pdf
- save html as pdf
- how to convert html
language: cs
lastmod: 2026-08-15
og_description: Jak omezit zdroje při převodu HTML na PDF v Pythonu. Tento průvodce
  vám ukáže, jak bezpečně exportovat HTML do PDF omezením hloubky propojených zdrojů.
og_image_alt: Screenshot of Python code converting an HTML file to a PDF with limited
  resource handling
og_title: Jak omezit zdroje při převodu HTML na PDF v Pythonu
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: How to limit resources while converting HTML to PDF using Python. Learn
    to export HTML to PDF with controlled resource depth.
  headline: How to limit resources when converting HTML to PDF in Python
  type: TechArticle
tags:
- HTML to PDF
- Python
- Resource handling
title: Jak omezit zdroje při převodu HTML na PDF v Pythonu
url: /cs/python/general/how-to-limit-resources-when-converting-html-to-pdf-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak omezit zdroje při převodu HTML na PDF v Pythonu

Pokud potřebujete **jak omezit zdroje** během převodu HTML‑to‑PDF, tento průvodce poskytuje kompletní, připravené řešení. Nastavením správy zdrojů zabráníte načítání hlubokých odkazů, stahování velkých obrázků nebo nekonečnému spouštění skriptů, což udržuje převod rychlý a předvídatelný.

Také se naučíte, jak **převést HTML na PDF**, **exportovat HTML do PDF** a **uložit HTML jako PDF** pomocí jediného, dobře strukturovaného skriptu. Nepotřebujete žádnou externí dokumentaci – stačí postupovat podle níže uvedených kroků.

## Co budete potřebovat

* Python 3.9 nebo novější  
* `aspose.html` package (the library that provides `HTMLDocument`, `ResourceHandlingOptions`, and `PdfSaveOptions`) → *balíček `aspose.html` (knihovna, která poskytuje `HTMLDocument`, `ResourceHandlingOptions` a `PdfSaveOptions`)*
* An HTML file you want to convert (e.g., `big_page.html`) → *HTML soubor, který chcete převést (např. `big_page.html`)*  

Mít tyto předpoklady nainstalované zajišťuje, že kód poběží bez dalších konfigurací.

## Krok 1: Nainstalujte balíček Aspose.HTML

```bash
pip install aspose-html
```

Balíček `aspose-html` poskytuje třídy používané pro načítání, konfiguraci a ukládání dokumentů. Jednorázová instalace pokryje všechny následné importy.

## Krok 2: Načtěte HTML dokument, který chcete převést

```python
from aspose.html import HTMLDocument

# Load the source HTML file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

`HTMLDocument` parsuje soubor a vytvoří DOM v paměti. Tento objekt je vstupním bodem pro jakýkoli převod, ať už plánujete **převést HTML na PDF** nebo jej zobrazit v prohlížeči.

## Krok 3: Nakonfigurujte správu zdrojů (jak omezit zdroje)

```python
from aspose.html.drawing import ResourceHandlingOptions

# Create a resource handling options object
res_opts = ResourceHandlingOptions()
# Limit the depth of linked resources to three levels
res_opts.max_handling_depth = 3
```

Nastavení `max_handling_depth` říká enginu, aby po třech skocích přestal sledovat odkazy. To je jádro **jak omezit zdroje**: hlubší zdroje jsou ignorovány, čímž se zabrání nekontrolovaným síťovým požadavkům nebo obrovské spotřebě paměti. Hodnotu upravte podle bezpečnostních či výkonnostních požadavků vašeho projektu.

### Proč omezovat zdroje?

* **Bezpečnost** – Zabraňuje načítání externích skriptů, které by mohly spustit nechtěný kód.  
* **Výkon** – Snižuje spotřebu šířky pásma a CPU času, když zdrojová stránka odkazuje na mnoho obrázků nebo stylových souborů.  
* **Předvídatelnost** – Zajišťuje, že převod skončí v předem známém časovém rámci.

## Krok 4: Připojte možnosti zdrojů k nastavení ukládání PDF

```python
from aspose.html.saving import PdfSaveOptions

# Create PDF save options and attach the resource handling configuration
pdf_opts = PdfSaveOptions()
pdf_opts.resource_handling_options = res_opts
```

`PdfSaveOptions` seskupuje všechny parametry pro finální export. Propojením `resource_handling_options` zajistíte, že krok **exportovat HTML do PDF** bude respektovat nastavený limit hloubky.

## Krok 5: Exportujte HTML do PDF (uložte HTML jako PDF)

```python
# Save the document as a PDF file using the configured options
doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_opts)
```

Volání `save` zapíše PDF na disk. Tento řádek demonstruje **jak převést HTML** do přenosného dokumentu při zachování omezení zdrojů. Výsledný soubor `big_page.pdf` obsahuje pouze zdroje v povolené hloubce.

## Krok 6: Ověřte vygenerované PDF

Otevřete `big_page.pdf` v libovolném PDF prohlížeči. Měli byste vidět původní rozvržení stránky, ale externí zdroje nad rámec tří skoků budou chybět. Pokud zaznamenáte chybějící obrázky nebo styly, zvažte zvýšení `max_handling_depth` nebo vložení těchto aktiv přímo do HTML.

### Běžný kontrolní seznam ověření

| Kontrola | Očekávaný výsledek |
|----------|--------------------|
| Text se zobrazuje správně | Veškerý textový obsah ze zdrojového HTML je přítomen |
| Základní obrázky se načtou | Obrázky odkazované do tří úrovní jsou viditelné |
| Žádné síťové volání po převodu | Použijte síťový monitor k potvrzení, že nejsou prováděny žádné další požadavky |

## Okrajové případy a praktické tipy

| Situace | Doporučené řešení |
|---------|-------------------|
| **Chybějící lokální soubor** | Zabalte vytvoření `HTMLDocument` do bloku `try/except FileNotFoundError` a zaznamenejte jasnou chybovou zprávu. |
| **Velmi velké obrázky** | Kombinujte `max_handling_depth` s `max_image_resolution` v `PdfSaveOptions` pro zmenšení příliš velkých grafik. |
| **Dynamický JavaScript obsah** | Nastavte `pdf_opts.enable_javascript = False`, pokud chcete čistý statický převod bez spouštění skriptů. |
| **Relativní URL** | Ujistěte se, že `doc.base_url` ukazuje na adresář obsahující HTML soubor, aby se relativní odkazy správně vyřešily. |

## Kompletní skript, který můžete zkopírovat a vložit

```python
# -------------------------------------------------------------
# Full example: limit resources while converting HTML to PDF
# -------------------------------------------------------------
# pip install aspose-html   # Run once before execution
# -------------------------------------------------------------

from aspose.html import HTMLDocument
from aspose.html.drawing import ResourceHandlingOptions
from aspose.html.saving import PdfSaveOptions

def convert_html_to_pdf(
    html_path: str,
    pdf_path: str,
    max_depth: int = 3
) -> None:
    """
    Converts an HTML file to PDF while limiting the depth of linked resources.

    Args:
        html_path: Path to the source .html file.
        pdf_path: Destination path for the generated .pdf file.
        max_depth: Maximum depth for resource handling (default = 3).
    """
    # Load the HTML document
    doc = HTMLDocument(html_path)

    # Configure resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = max_depth

    # Attach resource options to PDF save settings
    pdf_opts = PdfSaveOptions()
    pdf_opts.resource_handling_options = res_opts

    # Export HTML to PDF
    doc.save(pdf_path, pdf_opts)

if __name__ == "__main__":
    # Example usage
    convert_html_to_pdf(
        html_path="YOUR_DIRECTORY/big_page.html",
        pdf_path="YOUR_DIRECTORY/big_page.pdf",
        max_depth=3
    )
```

Spuštěním tohoto skriptu vznikne `big_page.pdf` ve stejném adresáři, přičemž se použije pravidlo **jak omezit zdroje**, které jste definovali. Funkce `convert_html_to_pdf` může být znovu použita ve větších projektech, což usnadňuje **uložit HTML jako PDF** s konzistentním nastavením.

## Závěr

Nyní už víte **jak omezit zdroje**, když **převádíte HTML na PDF** pomocí Pythonu. Tutoriál pokryl instalaci knihovny, načtení HTML, konfiguraci `ResourceHandlingOptions`, připojení těchto možností k `PdfSaveOptions` a nakonec **export HTML do PDF**. Kontrolou `max_handling_depth` chráníte aplikaci před nadměrným síťovým provozem a nepředvídatelnými časy převodu.

Dále prozkoumejte související témata, jako je **jak převést HTML** s vlastním CSS, vkládání fontů nebo hromadné generování PDF. Úpravou dalších `PdfSaveOptions` (např. velikost stránky, komprese) můžete doladit výstup pro faktury, zprávy nebo e‑knihy.

Neváhejte experimentovat s různými hodnotami hloubky, kombinovat tento přístup s headless prohlížeči nebo jej integrovat do webové služby, která na požádání vrací PDF. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Jak uložit HTML v C# – Kompletní průvodce s vlastním správcem zdrojů](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Vytvořit HTML dokument s formátovaným textem a exportovat do PDF – Kompletní průvodce](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [Převést HTML na PDF pomocí Aspose.HTML – Kompletní průvodce manipulací](/html/english/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}