---
category: general
date: 2026-07-15
description: Vytvořte PDF z HTML pomocí Pythonu. Naučte se, jak rychle převést HTML
  na PDF pomocí jednoduchého skriptu a jasných kroků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: cs
lastmod: 2026-07-15
og_description: Vytvořte PDF z HTML pomocí Pythonu. Tento průvodce vám ukáže, jak
  převést HTML na PDF, uložit HTML jako PDF a efektivně pracovat s prostředky.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Vytvořte PDF z HTML v Pythonu – Praktický tutoriál
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: Vytvořte PDF z HTML v Pythonu – Tutoriál HTML do PDF v Pythonu
url: /cs/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření PDF z HTML v Pythonu – Kompletní tutoriál

Už jste někdy potřebovali **vytvořit PDF z HTML**, ale nebyli jste si jisti, kterou knihovnu Pythonu zvolit? Nejste v tom sami — mnoho vývojářů narazí na tento problém, když se snaží převést webovou zprávu, fakturu nebo marketingovou stránku na tisknutelné PDF.  

Dobrou zprávou je, že s pouhými několika řádky kódu můžete **spolehlivě převést HTML na PDF**, a skript funguje na Windows, macOS i Linuxu. V tomto průvodci projdeme kompletním, spustitelným příkladem, vysvětlíme, proč je každý krok důležitý, a ukážeme vám, jak **uložit HTML jako PDF** bez zbytečných nedostatků.

---

## Co se naučíte

- Nainstalovat správný Python balíček pro konverzi HTML‑na‑PDF.  
- Načíst HTML soubor s vlastními možnostmi zpracování zdrojů (aby se předešlo nekonečným importům CSS).  
- Vygenerovat čistý PDF soubor na disku.  
- Řešit běžné okrajové případy, jako jsou externí obrázky, relativní cesty a velké dokumenty.  

Na konci tohoto **HTML‑to‑PDF tutoriálu** budete mít znovupoužitelnou funkci, kterou můžete vložit do libovolného projektu.

---

## Předpoklady

- Python 3.9+ (kód funguje i s 3.8, ale 3.9+ poskytuje nejnovější funkce `pathlib`).  
- Základní znalost příkazové řádky a virtuálních prostředí.  
- HTML soubor, který chcete převést na PDF — každá statická stránka bude stačit.

> **Pro tip:** Pokud používáte virtuální prostředí, aktivujte jej před instalací knihovny; tím udržíte svůj globální Python v pořádku.

---

## Krok 1 – Instalace WeasyPrint (engine za konverzí)

WeasyPrint je čistě Pythonová knihovna, která renderuje HTML a CSS do PDF. Zvládá většinu moderních webových funkcí a poskytuje vám detailní kontrolu nad načítáním zdrojů.

```bash
pip install weasyprint
```

Spuštěním výše uvedeného příkazu se stáhnou `cairocffi`, `tinycss2` a několik dalších závislostí. Pokud narazíte na chybu související s `cairo` na Windows, stáhněte si předkompilované balíčky z [WeasyPrint webu](https://weasyprint.org/docs/install/).

---

## Krok 2 – Připravte malý pomocník pro správu zdrojů

Když načítáte HTML dokument, který odkazuje na externí styly nebo obrázky, knihovna bude následovat tyto odkazy. V některých případech to vede k hlubokému vnoření nebo dokonce k nekonečným smyčkám (např. CSS soubor, který `@import`uje sám sebe). Abychom udrželi věci přehledné, omezujeme hloubku zpracování zdrojů.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

Třída výše není vyžadována WeasyPrint, ale napodobuje vzor, který jste viděli v původním úryvku, a poskytuje vám háček pro zastavení nekontrolovaných importů. Uvidíte ji použít v dalším kroku.

---

## Krok 3 – Načtěte HTML dokument pomocí vlastních možností

Nyní skutečně načteme HTML soubor. Třída `HTML` přijímá argument `base_url`, který nastavíme na adresář obsahující zdrojový soubor — tím umožníme fungování relativních odkazů bez webového serveru.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Proč je to důležité:** Pokud vaše HTML načítá řetězec CSS souborů, každý `@import` spustí další načtení. Ochrana hloubky zabraňuje, aby skript vymkl kontrole.

---

## Krok 4 – Uložte zpracovaný dokument jako PDF

S objektem `HTML` v ruce je generování PDF jedním řádkem. Navíc předáváme jednoduchý CSS útržek, který vynutí čistou velikost stránky (A4) a přidá malý okraj — klidně si ho upravte.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Volání `write_pdf` streamuje PDF na disk, takže získáte soubor připravený ke sdílení.

---

## Krok 5 – Sestavte vše dohromady

Níže je kompaktní skript, který můžete zkopírovat do `convert.py`. Nahraďte zástupné cesty svými skutečnými adresáři.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Očekávaný výstup** — po spuštění `python convert.py` byste měli vidět:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Otevřete vygenerovaný soubor v libovolném PDF prohlížeči; uvidíte původní rozložení stránky, CSS styly a obrázky (pokud byly dostupné z HTML souboru).  

Pokud zjistíte chybějící obrázky, dvakrát zkontrolujte, že jejich atributy `src` jsou buď absolutní URL, nebo relativní cesty, které existují pod `YOUR_DIRECTORY`.

---

## Časté otázky a řešení okrajových případů

| Otázka | Odpověď |
|----------|--------|
| *Co když moje HTML odkazuje na externí fonty?* | WeasyPrint stáhne soubory fontů automaticky, ale můžete chtít povolit (whitelist) domény, abyste se vyhnuli dlouhým načítacím časům. |
| *Mohu převést řetězec HTML místo souboru?* | Ano — použijte `HTML(string=my_html_string)` a vynechte `base_url` nebo jej nastavte na dočasnou složku. |
| *Jak mohu řídit metadata PDF (název, autor)?* | Předávejte slovník `metadata` funkci `write_pdf`, např. `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Na Linuxu dostávám „cairo‑cffi error“. * | Nejprve nainstalujte systémový balíček `libcairo2-dev` (`apt-get install libcairo2-dev` na Debian/Ubuntu) před instalací WeasyPrint pomocí pip. |

---

## Závěr

Právě jsme **vytvořili PDF z HTML** pomocí čistého Python workflow, pokryli mechaniku **konverze HTML na PDF** a ukázali vám, jak **uložit HTML jako PDF** s robustní správou zdrojů. Skript je dostatečně malý na to, aby se dal vložit do CI pipeline, a zároveň dostatečně flexibilní na rozšíření o vlastní záhlaví, patičky nebo vodoznaky.

Další kroky, které můžete prozkoumat:

- Použijte knihovnu **html to pdf python** `pdfkit` pro přístup založený na wkhtmltopdf (dobré pro starší CSS).  
- Přidejte CLI rozhraní s `argparse`, aby skript přijímal vstupní/výstupní argumenty.  
- Generujte PDF za běhu uvnitř Flask nebo FastAPI endpointu pro on‑demand reporty.  

Klidně experimentujte, rozbíjejte věci a pak se vraťte k tomuto průvodci pro rychlé osvěžení. Pokud narazíte na problémy, dokumentace WeasyPrint a komunitní fóra jsou vynikající zdroje.

Šťastné kódování a užijte si převod těch webových stránek na elegantní PDF!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Převod HTML na PDF s Aspose.HTML – Kompletní průvodce manipulací](/html/english/)
- [Převod HTML na PDF v .NET s Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Vytvoření PDF z HTML – C# krok za krokem průvodce](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}