---
category: general
date: 2026-09-26
description: Převod HTML na Markdown pomocí Pythonu, extrakce odkazů z HTML a uložení
  HTML jako Markdown. Naučte se, jak převádět HTML krok za krokem.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: cs
lastmod: 2026-09-26
og_description: Převod HTML na Markdown pomocí Pythonu, extrahování odkazů z HTML
  a ukládání HTML jako Markdown. Postupujte podle tohoto kompletního průvodce.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: Převod HTML na Markdown v Pythonu – extrahovat odkazy a odstavce
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: Převod HTML na Markdown v Pythonu – snadno extrahujte odkazy a odstavce
url: /cs/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod HTML na Markdown v Pythonu – snadné získávání odkazů a odstavců

Pokud potřebujete **convert HTML to Markdown** a zachovat jen užitečné části, tento průvodce vám ukáže, jak to provést pomocí několika řádků Pythonu. Ať už scrapujete blogové příspěvky, archivujete dokumentaci nebo čistíte těla e‑mailů, naučíte se spolehlivý způsob, jak extract links from HTML a save HTML as Markdown.

Tutoriál pokrývá vše od instalace požadovaného balíčku až po zpracování okrajových případů, jako jsou prázdné `<a>` značky nebo vnořené odstavce. Na konci budete mít připravený skript, který **converts HTML to Markdown**, extracts links from HTML a dokonce extracts paragraphs from HTML, když je potřebujete.

---

## Požadavky

* Python 3.8 nebo novější nainstalovaný  
* Přístup k Python balíčku `groupdocs-conversion` (knihovna, která poskytuje `HTMLDocument`, `MarkdownSaveOptions` a `Converter`)  
* Místní HTML soubor, který chcete zpracovat (např. `article.html`)

Knihovnu můžete nainstalovat pomocí pip:

```bash
pip install groupdocs-conversion
```

> **Tip:** Použijte virtuální prostředí (`python -m venv venv`), aby byly závislosti izolované.

---

## Krok 1: Načtení zdrojového HTML dokumentu

Prvním krokem je vytvořit objekt `HTMLDocument`, který ukazuje na váš zdrojový soubor. Tento objekt abstrahuje surové HTML a poskytuje konvertoru čistý vstupní bod.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Proč je to důležité:* Načtení dokumentu tímto způsobem umožňuje knihovně jednorázově parsovat DOM, takže následné operace (jako extracting links nebo extracting paragraphs) jsou rychlé a paměťově úsporné.

---

## Krok 2: Vytvoření Markdown možností uložení a výběr požadovaných funkcí

`MarkdownSaveOptions` vám umožňuje rozhodnout, které HTML elementy přežijí konverzi. Příznak `features` používá bitový OR k kombinaci možností.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Proč je to důležité:* Specifikací `LINKS` a `PARAGRAPHS` **extract links from HTML** a **extract paragraphs from HTML**, zatímco vše ostatní (styly, skripty, obrázky) je zahozeno. Pokud později potřebujete jen odkazy, nahraďte `MarkdownFeatures.PARAGRAPHS` hodnotou `0` (nebo ji vynechejte).

---

## Krok 3: Převod HTML na Markdown pomocí nakonfigurovaných možností

Nyní zavolejte statickou metodu `convert_html`, předáte zdrojový dokument, cílovou cestu a možnosti, které jste právě vytvořili.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Proč je to důležité:* Konverze probíhá v jednom průchodu, aplikujíc filtr funkcí, který jste definovali. Výsledný soubor (`article_links.md`) obsahuje jen odkazy a odstavce ve formátu Markdown, což je přesně to, co potřebujete, když chcete **save HTML as Markdown** pro následné zpracování.

---

## Kompletní skript – vše dohromady

Níže je kompletní, spustitelný skript, který můžete zkopírovat a vložit do souboru pojmenovaného `html_to_md.py`. Přizpůsobte cesty tak, aby odpovídaly vašemu prostředí.

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### Očekávaný výstup

Spuštěním skriptu se vygeneruje soubor podobný následujícímu (přesný obsah závisí na zdrojovém HTML):

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Objeví se jen text odkazu a text odstavce; všechny ostatní HTML elementy jsou odstraněny.

---

## Extrahování jen odkazů nebo jen odstavců (pokročilé varianty)

Někdy potřebujete **how to convert HTML** do souboru Markdown, který obsahuje jen jeden typ elementu.

### 1. Extrahování jen odkazů

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Extrahování jen odstavců

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Obě varianty znovu používají stejný volání `convert_html`, takže nemusíte psát samostatnou konverzní logiku.

---

## Zpracování okrajových případů

| Situation                               | Recommended fix |
|----------------------------------------|-----------------|
| HTML soubor obsahuje prázdné `<a>` značky    | Konvertor automaticky přeskočí prázdné odkazy. Pokud vidíte osamělé `[]()` položky, nastavte `md_options.removeEmptyLinks = True`. |
| Vnořené odstavce (`<p>` uvnitř `<div>`) | Knihovna vyrovná vnořené odstavce, zachovává pořadí textu. Není potřeba žádný další kód. |
| Ne‑ASCII znaky v názvech odkazů    | Ujistěte se, že váš Python soubor je uložen s kódováním UTF‑8 a otevřete výstupní soubor s `encoding="utf-8"`, pokud jej budete později číst. |
| Velmi velké HTML soubory (≥ 50 MB)        | Zpracovávejte soubor po částech pomocí `HTMLDocument(stream=io.BytesIO(...))`, abyste se vyhnuli načtení celého souboru do paměti. |

---

## Často kladené otázky

**Q: Funguje to s HTML fragmenty (bez kořenové značky `<html>`)?**  
A: Ano. `HTMLDocument` přijímá jakýkoli dobře formovaný fragment; konvertor s ním zachází jako s tělem dokumentu.

**Q: Mohu zachovat obrázky jako Markdown syntaxi pro obrázky?**  
A: Přidejte `MarkdownFeatures.IMAGES` do příznaku `features`:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**Q: Jak převést mnoho souborů v adresáři?**  
A: Zabalte `convert_html_to_markdown` do smyčky, která prochází adresář pomocí `os.listdir` nebo `pathlib.Path.rglob("*.html")`.

---

## Závěr

Nyní víte, jak **convert HTML to Markdown** v Pythonu a zároveň selektivně **extract links from HTML** a **extract paragraphs from HTML**. Skript ukazuje standardní postup – načíst dokument, nakonfigurovat `MarkdownSaveOptions` a spustit `Converter.convert_html`. S několika úpravami můžete také **save HTML as Markdown** obsahující jen odkazy, jen odstavce nebo plnou věrnou reprezentaci.

Dále můžete zkoumat:

* Přidání `MarkdownFeatures.HEADINGS` pro zachování názvů sekcí.  
* Použití výsledného Markdownu jako vstupu pro statické generátory stránek jako MkDocs nebo Hugo.  
* Automatizace hromadných konverzí pro celou dokumentační repozitář.

Šťastné převádění!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Převod HTML na Markdown v .NET s Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Převod HTML na Markdown v Aspose.HTML pro Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Jak nastavit offset při převodu HTML na Markdown v Javě](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}