---
category: general
date: 2026-08-09
description: Jak omezit zdroje při převodu HTML na PDF nebo Markdown. Naučte se exportovat
  PDF, extrahovat odkazy z HTML a řídit hloubku zdrojů.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to limit resources
- convert html to pdf
- convert html to markdown
- extract links from html
- how to export pdf
language: cs
lastmod: 2026-08-09
og_description: Jak omezit zdroje při konverzi HTML na PDF nebo Markdown. Tento průvodce
  vám ukáže, jak exportovat PDF, extrahovat odkazy z HTML a udržet zpracování zdrojů
  povrchní.
og_image_alt: Screenshot showing how to limit resources in HTML conversion script
og_title: Jak omezit zdroje pro konverzi HTML na PDF a HTML na Markdown
schemas:
- author: GroupDocs
  dateModified: '2026-08-09'
  description: How to limit resources while converting HTML to PDF or Markdown. Learn
    to export PDF, extract links from HTML, and control resource depth.
  headline: How to limit resources for HTML to PDF and Markdown
  type: TechArticle
tags:
- HTML conversion
- PDF export
- Markdown generation
- Resource handling
title: Jak omezit zdroje pro převod HTML na PDF a Markdown
url: /cs/python/general/how-to-limit-resources-for-html-to-pdf-and-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak omezit zdroje při převodu HTML na PDF a Markdown

Pokud potřebujete **jak omezit zdroje** během rozsáhlého převodu HTML, tento průvodce vám ukáže kompletní řešení. Nastavením možností pro zpracování zdrojů zabráníte hlubokému stahování externích souborů, udržíte nízkou spotřebu paměti a přesto získáte přesný výstup ve formátu PDF i Markdown.

Také se naučíte, jak **convert html to pdf**, jak **convert html to markdown**, jak **extract links from html**, a nejlepší způsob, **how to export pdf** ze stejného zdrojového dokumentu. Kromě GroupDocs.Conversion SDK není potřeba žádný externí nástroj.

## Co dosáhnete

* Omezit zpracování externích zdrojů na bezpečnou hloubku.  
* Vygenerovat PDF soubor z velké HTML zprávy.  
* Vytvořit Markdown soubor ve stylu Git, který obsahuje pouze odkazy a odstavce.  
* Ověřit, že export PDF byl úspěšný a že Markdown soubor obsahuje očekávané odkazy.

### Požadavky

* Python 3.8+ (kód používá typově anotovaný Python).  
* Nainstalovaný balíček `groupdocs-conversion` (`pip install groupdocs-conversion`).  
* Velký HTML soubor (např. `big_report.html`) umístěný v zapisovatelném adresáři.  

---

## Jak omezit zdroje při převodu HTML

Řízení počtu úrovní externích zdrojů (obrázky, CSS, skripty), které konvertor sleduje, je zásadní pro výkon i bezpečnost. Třída `ResourceHandlingOptions` vám umožňuje nastavit maximální hloubku zpracování. Hloubka **3** znamená, že konvertor bude sledovat odkazy až do třetí úrovně a poté se zastaví, čímž zabrání nekonečným síťovým voláním.

```python
from groupdocs.conversion import ResourceHandlingOptions, HTMLDocument, Converter, MarkdownSaveOptions

# Step 1: Create a ResourceHandlingOptions instance and cap the depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3  # limit external resource traversal
```

*Proč je to důležité*: Velké zprávy často odkazují na mnoho externích aktiv. Bez omezení hloubky by konvertor mohl zkusit stáhnout každý propojený skript nebo obrázek, což by vyčerpalo šířku pásma i paměť. Nastavení `max_handling_depth` na 3 vyvažuje úplnost a bezpečnost.

---

## Převod HTML na PDF s řízenou hloubkou zdrojů

Jakmile jsou možnosti zdrojů připravené, načtěte HTML dokument s těmito možnostmi a spusťte převod do PDF. Metoda `Converter.convert_html` detekuje výstupní formát podle přípony souboru.

```python
# Step 2: Load the HTML document with the resource options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_report.html", resource_options)

# Step 3: Convert the HTML document to PDF
Converter.convert_html(html_doc, "YOUR_DIRECTORY/big_report.pdf")
```

*Proč to funguje*: Konstruktor `HTMLDocument` přijímá argument `ResourceHandlingOptions`, což zajišťuje, že stejný limit hloubky se použije i při generování PDF. SDK automaticky vykreslí rozvržení stránky, vloží povolené obrázky a vytvoří vysoce věrné PDF.

**Očekávaný výstup**: `big_report.pdf` se objeví v `YOUR_DIRECTORY`. Otevřete jej v libovolném prohlížeči PDF a ověřte, že obrázky, tabulky a text jsou správně vykresleny, zatímco externí zdroje nad hloubkou 3 jsou vynechány.

---

## Připravte možnosti uložení Markdown pro extrakci odkazů

Když potřebujete lehkou reprezentaci HTML, je převod na Markdown ideální. Třída `MarkdownSaveOptions` vám umožňuje vybrat formátovač (Git‑flavoured) a zvolit, které funkce obsahu zachovat. V tomto tutoriálu zachováváme pouze **odkazy** a **odstavce**, což splňuje požadavek **extract links from html**.

```python
# Step 4: Configure MarkdownSaveOptions for link‑only output
markdown_options = MarkdownSaveOptions()
markdown_options.formatter = MarkdownSaveOptions.Formatter.GIT
markdown_options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

*Proč tyto příznaky*:  
* `Formatter.GIT` vytváří Markdown, který funguje bez problémů na GitHubu a GitLabu.  
* `Features.LINK | Features.PARAGRAPH` odstraňuje obrázky, tabulky a skripty, takže zůstane čistý seznam hyperodkazů a čitelných textových bloků.

---

## Převod HTML na Markdown pomocí nakonfigurovaných možností

Nyní spusťte převod se stejnou instancí `HTMLDocument`. Přetížená metoda `convert_html` přijímá objekt `MarkdownSaveOptions` následovaný cílovou cestou souboru.

```python
# Step 5: Convert the same HTML document to Markdown
Converter.convert_html(html_doc, markdown_options, "YOUR_DIRECTORY/big_report.md")
```

**Výsledek**: `big_report.md` obsahuje pouze odkazy a odstavce ve formátu Markdown. Otevřete soubor v libovolném editoru a uvidíte stručný seznam URL extrahovaných z původního HTML.

---

## Jak exportovat PDF a ověřit výsledky

Export PDF je již pokrytý v kroku 3, ale stojí za to potvrdit, že soubor byl správně zapsán a že omezení zdrojů fungovalo podle očekávání.

```python
import os

pdf_path = "YOUR_DIRECTORY/big_report.pdf"
md_path = "YOUR_DIRECTORY/big_report.md"

# Verify PDF existence and size
if os.path.isfile(pdf_path):
    print(f"PDF exported successfully – size: {os.path.getsize(pdf_path)} bytes")
else:
    raise FileNotFoundError("PDF export failed")

# Verify Markdown existence and preview first 5 lines
if os.path.isfile(md_path):
    print("Markdown export successful. First lines:")
    with open(md_path, "r", encoding="utf-8") as f:
        for _ in range(5):
            print(f.readline().strip())
else:
    raise FileNotFoundError("Markdown export failed")
```

*Proč je tato kontrola důležitá*: Kontrola velikosti souboru vám pomůže odhalit neobvykle malé PDF, které může naznačovat chybějící zdroje. Náhled Markdown potvrzuje, že byly zachovány pouze odkazy a odstavce, čímž se splňuje cíl **extract links from html**.

---

## Běžné varianty a řešení okrajových případů

| Situace | Doporučená úprava |
|-----------|-------------------|
| **HTML odkazuje hlouběji než 3 úrovně** | Zvyšte `max_handling_depth` na 5 nebo 7, ale sledujte využití paměti. |
| **Potřeba zachovat obrázky v Markdownu** | Přidejte `MarkdownSaveOptions.Features.IMAGE` do příznaku `features`. |
| **Generování jednostránkového PDF** | Nastavte `PDFSaveOptions.page_width` a `page_height` tak, aby odpovídaly obsahu, nebo použijte `pdf_options.split_into_pages = False`. |
| **Běh na serveru bez grafického rozhraní** | Ujistěte se, že jsou nainstalovány nativní závislosti SDK (`libcairo`, `libpango`), aby nedocházelo k chybám při vykreslování. |
| **Velké soubory způsobují timeout** | Zpracovávejte HTML po částech načítáním sekcí pomocí `HTMLDocument.load_range(start, end)`. |

**Tip**: Znovu použijte stejnou instanci `HTMLDocument` pro více převodů. SDK ukládá do mezipaměti parsovaný DOM, což snižuje čas CPU při následných exportech PDF nebo Markdown.

---

## Závěr

Nyní víte, **jak omezit zdroje** při **convert html to pdf** a **convert html to markdown**, jak **extract links from html**, a jak bezpečně provést kroky **how to export pdf**. Nastavením `ResourceHandlingOptions` a `MarkdownSaveOptions` řídíte hloubku externího stahování, udržujete výstup lehký a vytváříte spolehlivé artefakty pro následné zpracování.

Dále prozkoumejte pokročilé funkce, jako je **custom CSS injection**, **watermarking PDFs** nebo **batch converting multiple HTML files**. Tyto témata staví na stejných principech, které jsou zde popsány, a dále rozšiřují váš pipeline pro zpracování dokumentů.

---

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Use Aspose.HTML to Configure Fonts for HTML‑to‑PDF Java](/html/english/java/configuring-environment/configure-fonts/)
- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}