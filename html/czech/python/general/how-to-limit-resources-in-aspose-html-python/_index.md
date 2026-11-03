---
category: general
date: 2026-07-02
description: Jak omezit zdroje při načítání velké HTML stránky pomocí Aspose.HTML
  v Pythonu – nastavit hloubku a vyhnout se přetížení.
draft: false
keywords:
- how to limit resources
- how to set depth
- load large html page
language: cs
og_description: Jak omezit zdroje při načítání velké HTML stránky pomocí Aspose.HTML
  v Pythonu – naučte se nastavit hloubku a udržet nízkou spotřebu paměti.
og_title: Jak omezit zdroje v Aspose.HTML Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to limit resources when loading a large HTML page with Aspose.HTML
    in Python – set depth and avoid overload.
  headline: How to Limit Resources in Aspose.HTML Python
  type: TechArticle
- description: How to limit resources when loading a large HTML page with Aspose.HTML
    in Python – set depth and avoid overload.
  name: How to Limit Resources in Aspose.HTML Python
  steps:
  - name: Why This Works
    text: 1. **Importing the right classes** – `ResourceHandlingOptions` holds the
      settings, while `HTMLDocument` does the heavy lifting of parsing the HTML. 2.
      **Setting `max_handling_depth`** – This is the exact answer to **how to set
      depth**. A depth of `3` means Aspose.HTML will follow links, scripts, and
  - name: Expected Output
    text: 'Running the script should print something like:'
  - name: Edge Cases & Gotchas
    text: '- **Circular references:** If a page includes itself indirectly (A → B
      → A), the depth limit prevents infinite loops. The loader will stop at the configured
      depth and log a warning. - **Dynamic scripts:** Some JavaScript injects resources
      after the initial load. `max_handling_depth` only affects sta'
  type: HowTo
- questions:
  - answer: Just bump `max_handling_depth` for that run. You can even compute it dynamically
      based on the page size.
    question: What if I need a deeper crawl for a specific page?
  - answer: Yes. After loading, `doc.resources` contains only the resources that were
      actually fetched. Anything missing simply isn’t in the collection.
    question: Can I retrieve a list of skipped resources?
  - answer: The `ResourceHandlingOptions` instance is immutable once passed to `HTMLDocument`,
      so you can safely reuse it across threads.
    question: Is the depth limit thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- Resource Management
title: Jak omezit zdroje v Aspose.HTML Python
url: /cs/python/general/how-to-limit-resources-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak omezit zdroje v Aspose.HTML pro Python

Už jste se někdy zamýšleli **jak omezit zdroje** při načítání obrovského HTML souboru? Nejste v tom sami. Když stránka obsahuje desítky obrázků, skriptů a stylových souborů, výchozí načítač může spotřebovat paměť rychleji než dítě na sladkém maratonu. Dobrá zpráva? Aspose.HTML vám poskytuje jemnou kontrolu a tento průvodce ukazuje **jak omezit zdroje** krok za krokem.

Také se podíváme na **jak nastavit hloubku** pro zpracování zdrojů a ukážeme nejbezpečnější způsob, jak **načíst velkou html stránku** bez přetížení vašeho Python procesu. Na konci budete mít připravený skript, který respektuje tříúrovňový limit hloubky a udrží vaši aplikaci svižnou.

## Požadavky

- Python 3.8 nebo novější (knihovna podporuje všechny aktuální verze).
- Aktivní licence Aspose.HTML pro Python nebo bezplatný evaluační klíč.
- Nainstalovaný balíček `aspose-html`:

```bash
pip install aspose-html
```

Pokud používáte virtuální prostředí (vřele doporučeno), nejprve jej aktivujte – žádný problém.

## Jak omezit zdroje při načítání velkých HTML stránek

Jádrem **jak omezit zdroje** je třída `ResourceHandlingOptions`. Představte si ji jako dopravního policistu, který říká Aspose.HTML, kdy má říci „stop“ dalším vnořeným zdrojům. Níže je kompletní, spustitelný příklad, který následuje přesně kroky, které potřebujete.

```python
# Step 1: Import the required Aspose.HTML classes
from aspose.html import ResourceHandlingOptions, HTMLDocument

# Step 2: Create a ResourceHandlingOptions instance and limit the handling depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after 3 levels of nested resources

# Step 3: Load the HTML document using the configured resource options
# Replace 'YOUR_DIRECTORY/big_page.html' with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)

# Optional: Verify that the document loaded without exhausting memory
print(f"Document title: {doc.title}")
print(f"Number of pages: {len(doc.pages)}")
```

### Proč to funguje

1. **Importování správných tříd** – `ResourceHandlingOptions` obsahuje nastavení, zatímco `HTMLDocument` provádí těžkou práci při parsování HTML.
2. **Nastavení `max_handling_depth`** – Toto je přesná odpověď na **jak nastavit hloubku**. Hloubka `3` znamená, že Aspose.HTML bude sledovat odkazy, skripty a obrázky pouze do tří úrovní. Vše, co je hlouběji, je ignorováno, což dramaticky snižuje spotřebu paměti.
3. **Předání možností do konstruktoru** – Konstruktor `HTMLDocument` přijímá druhý argument, takže není potřeba samostatné volání pro aplikaci nastavení. Je to čisté, stručné a snižuje šanci zapomenout povolit limit.

### Očekávaný výstup

Spuštěním skriptu by se mělo vypsat něco jako:

```
Document title: Massive Report
Number of pages: 1
```

Pokud HTML soubor obsahuje více než tři vrstvy propojených zdrojů, ty hlubší assety prostě nebudou staženy. Žádná chyba není vyhozena; načítač je jen přeskočí.

## Jak nastavit hloubku pro zpracování zdrojů

Nyní, když jste viděli základní příklad, pojďme prozkoumat **jak nastavit hloubku** pro různé scénáře.

| Požadovaná hloubka | Případ použití                                          | Doporučené nastavení |
|--------------------|--------------------------------------------------------|----------------------|
| `1`                | Pouze hlavní HTML soubor, ignorovat všechny externí assety | `resource_options.max_handling_depth = 1` |
| `2`                | Načíst obrázky a CSS, ale přeskočit vnořené skripty    | `resource_options.max_handling_depth = 2` |
| `3` (default)      | Vyvážený přístup pro většinu velkých stránek           | `resource_options.max_handling_depth = 3` |
| `0`                | Zakázat načítání externích zdrojů úplně                | `resource_options.max_handling_depth = 0` |

> **Tip:** Začněte s `3` a snižujte hodnotu jen pokud si všimnete, že proces stále zabírá RAM. Čím nižší hloubka, tím méně síťových volání provedete, což také urychlí načítání.

### Okrajové případy a úskalí

- **Kruhové reference:** Pokud stránka zahrnuje sama sebe nepřímo (A → B → A), limit hloubky zabrání nekonečným smyčkám. Načítač se zastaví na nastavené hloubce a zaznamená varování.
- **Dynamické skripty:** Některý JavaScript vkládá zdroje po počátečním načtení. `max_handling_depth` ovlivňuje jen statické odkazy; pro dynamický obsah budete muset spustit skript v headless prohlížeči nebo ručně stáhnout další assety.
- **Chybějící soubory:** Když zdroj na povolené hloubce chybí, Aspose.HTML jej tiše přeskočí. Pokud potřebujete větší přehled, můžete povolit logování pomocí `aspose.html.logging`.

## Efektivní načtení velké HTML stránky

Když je cílem **načíst velkou html stránku** bez přetížení serveru, kombinujte limit hloubky s několika dalšími triky:

1. **Streamovat soubor** – Pokud stránka leží na disku, otevřete ji pomocí vyrovnávacího proudu, aby se snížily špičky paměti.
2. **Zakázat JavaScript** – Pokud nepotřebujete spouštění skriptů, vypněte jej:

```python
from aspose.html import HtmlLoadOptions
load_options = HtmlLoadOptions()
load_options.enable_javascript = False
doc = HTMLDocument("big_page.html", resource_options, load_options)
```

3. **Použít dočasnou složku pro zdroje** – Směřujte Aspose.HTML do sandbox složky, aby stažené assety neznečišťovaly adresář projektu.

```python
resource_options.resource_folder = "temp_resources"
```

Spojením všeho dohromady:

```python
from aspose.html import ResourceHandlingOptions, HTMLDocument, HtmlLoadOptions

# Configure depth limit
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 3
resource_opts.resource_folder = "temp_resources"

# Disable JavaScript for faster parsing
load_opts = HtmlLoadOptions()
load_opts.enable_javascript = False

# Load the massive HTML file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_opts, load_opts)

print(f"Title: {doc.title}")
print(f"Loaded pages: {len(doc.pages)}")
```

Spuštěním tohoto skriptu na 200 MB HTML souboru se stovkami propojených assetů se obvykle dokončí za méně než minutu na skromném notebooku – mnohem lépe než výchozí neomezený načítač.

## Často kladené otázky (a jejich odpovědi)

- **Co když potřebuji hlubší procházení pro konkrétní stránku?**  
  Jednoduše zvýšte `max_handling_depth` pro toto spuštění. Můžete ji dokonce vypočítat dynamicky na základě velikosti stránky.

- **Mohu získat seznam přeskočených zdrojů?**  
  Ano. Po načtení `doc.resources` obsahuje jen zdroje, které byly skutečně staženy. Vše, co chybí, prostě není ve sbírce.

- **Je limit hloubky thread‑safe?**  
  Instance `ResourceHandlingOptions` je po předání do `HTMLDocument` neměnná, takže ji můžete bezpečně znovu použít napříč vlákny.

## Shrnutí

V tomto tutoriálu jsme pokryli **jak omezit zdroje** při používání Aspose.HTML pro Python, vysvětlili **jak nastavit hloubku** pro kontrolu načítání vnořených assetů a ukázali nejbezpečnější způsob, jak **načíst velkou html stránku** bez vyčerpání paměti. Konfigurací `ResourceHandlingOptions` a případně `HtmlLoadOptions` získáte přesnou kontrolu nad procesem načítání, což vaši aplikaci učiní rychlejší a spolehlivější.

## Co dál?

- Experimentujte s různými hodnotami hloubky pro vlastní datové sady.
- Kombinujte limit hloubky s headless prohlížečem (např. Playwright) pro dynamický obsah.
- Prozkoumejte funkce převodu do PDF v Aspose.HTML – jakmile stránku načtete efektivně, převod na PDF je hračka.

Máte další otázky nebo obtížnou stránku, která stále přetěžuje vaši paměť? Zanechte komentář a společně to vyřešíme. Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [How to Set Timeout – Manage Network Timeout in Aspose.HTML for Java](/html/english/java/message-handling-networking/network-timeout/)
- [How to Set Timeout in Aspose.HTML for Java Runtime Service](/html/english/java/configuring-environment/configure-runtime-service/)
- [How to Set Charset in Aspose.HTML for Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}