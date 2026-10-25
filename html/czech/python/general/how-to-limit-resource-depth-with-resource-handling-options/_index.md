---
category: general
date: 2026-10-25
description: Naučte se, jak omezit hloubku zdrojů a použít jejich zpracování při ukládání
  velkých HTML souborů pomocí Pythonu. Postupujte podle tohoto krok‑za‑krokem průvodce
  pro spolehlivé výsledky.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit resource depth
- apply resource handling
- HTML document processing
- save options Python
- resource handling options
language: cs
lastmod: 2026-10-25
og_description: Omezte hloubku zdrojů a použijte zpracování zdrojů při ukládání HTML
  pomocí Pythonu. Tento tutoriál ukazuje kompletní, spustitelné řešení.
og_image_alt: Screenshot illustrating limit resource depth in a Python script
og_title: Omezte hloubku zdrojů při aplikaci správy zdrojů – průvodce Pythonem
schemas:
- author: GroupDocs
  dateModified: '2026-10-25'
  description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  headline: How to limit resource depth with resource handling options
  type: TechArticle
- description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  name: How to limit resource depth with resource handling options
  steps:
  - name: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
    text: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
  - name: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
    text: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
  - name: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
    text: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
  type: HowTo
tags:
- Python
- HTML
- File handling
title: Jak omezit hloubku zdroje pomocí možností správy zdrojů
url: /cs/python/general/how-to-limit-resource-depth-with-resource-handling-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak omezit hloubku zdrojů pomocí možností zpracování zdrojů

Pokud potřebujete **omezit hloubku zdrojů** při zpracování obrovského HTML souboru, tento návod vám ukáže, jak na to. Na konci tutoriálu také zjistíte, jak **použít zpracování zdrojů**, aby operace ukládání respektovala limit hloubky a zabránila nekontrolovanému zpracování.

Velké HTML stránky často obsahují mnoho externích zdrojů — obrázky, skripty, styly a vnořené iframe. Bez limitu hloubky může parser sledovat každý odkaz, což dramaticky zvyšuje spotřebu paměti a dobu zpracování. Technika popsaná zde udržuje operaci rychlou a předvídatelnou.

## Předpoklady

Než začnete, ujistěte se, že máte:

* Python 3.9+ nainstalovaný.
* Knihovnu `groupdocs-viewer` (nebo podobnou knihovnu pro zpracování HTML) dostupnou přes `pip install groupdocs-viewer`.
* Ukázkový HTML soubor (`big_page.html`) umístěný v známém adresáři.
* Oprávnění k zápisu do výstupního adresáře.

Tyto položky zajistí, že kód poběží bez další konfigurace.

## Krok 1: Načtěte zdrojový HTML dokument

Prvním krokem je vytvořit instanci `HTMLDocument`, která ukazuje na původní soubor. Objekt představuje celou HTML strukturu a později vám umožní nastavit možnosti ukládání.

```python
# Step 1: Load the source HTML document
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

*Proč je to důležité*: Načtení souboru jednou poskytne knihovně jediný vstupní bod pro všechny následné operace. Také ověří, že soubor existuje, a v případě špatné cesty vyvolá chybu již na začátku.

## Krok 2: Vytvořte možnosti zpracování zdrojů a omezte hloubku zpracování

`ResourceHandlingOptions` vám umožňuje řídit, jak hluboko bude knihovna procházet propojené zdroje. Nastavením `max_handling_depth` na nízké číslo (např. 5) řeknete enginu, aby po pěti úrovních vnoření přestal sledovat odkazy.

```python
# Step 2: Create resource handling options and limit the processing depth
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 5  # Restricts handling to 5 levels deep
```

*Proč je to důležité*: **Omezením hloubky zdrojů** zabráníte parseru stahovat každý obrázek, skript nebo iframe, který může být odkazován nepřímo. Tím se sníží síťový provoz a zatížení paměti, zejména u stránek, které vkládají obsah třetích stran.

## Krok 3: Připojte možnosti zdrojů k možnostem ukládání

`SaveOptions` shromažďuje všechna nastavení, která ovlivňují výstupní soubor. Přiřazením `resource_handling_options` **aplikujete zpracování zdrojů** na nadcházející operaci ukládání.

```python
# Step 3: Attach the resource options to the save options
save_opts = SaveOptions()
save_opts.resource_handling_options = resource_opts
```

*Proč je to důležité*: Objekt `save_opts` funguje jako kontejner pro více příznaků (komprese, formát atd.). Přidání `resource_handling_options` zajistí, že limit hloubky bude během fáze zápisu dodržen.

## Krok 4: Uložte dokument s aplikovaným omezením zpracování zdrojů

Nakonec zavolejte `doc.save()` s nakonfigurovaným `save_opts`. Výstupní soubor bude obsahovat jen zdroje, které spadají do definované hloubky.

```python
# Step 4: Save the document with the limited resource handling applied
doc.save("YOUR_DIRECTORY/big_page_limited.html", save_opts)
```

**Očekávaný výsledek**:  
Nový soubor `big_page_limited.html` se objeví v `YOUR_DIRECTORY`. Otevřete jej v prohlížeči; uvidíte původní rozvržení, ale všechny zdroje nad úrovní pěti úrovní vnoření budou vynechány. Stránka se načte rychleji a spotřebuje mnohem méně paměti.

## Ověřte uložené HTML

Po uložení je dobré zkontrolovat, že byl limit hloubky respektován.

```python
# Verify that the saved file exists and its size is reasonable
import os

output_path = "YOUR_DIRECTORY/big_page_limited.html"
if os.path.isfile(output_path):
    size_kb = os.path.getsize(output_path) / 1024
    print(f"Saved file size: {size_kb:.2f} KB")
else:
    raise FileNotFoundError("The limited HTML file was not created.")
```

Pokud je velikost výrazně menší než originál (který může mít stovky kilobajtů), nastavení **limit resource depth** fungovalo podle očekávání.

## Časté problémy a jak se jim vyhnout

| Příznak | Příčina | Řešení |
|---------|---------|--------|
| Žádná změna velikosti souboru | `max_handling_depth` ponechán na výchozí (neomezený) | Explicitně nastavte `resource_opts.max_handling_depth` na hodnotu < ∞ |
| Chybějící obrázky na stránce | Zdroje byly hlubší než limit | Zvyšte hloubku nebo přesuňte kritické zdroje do mělké úrovně |
| `PermissionError` při ukládání | Výstupní adresář je jen pro čtení | Vyberte zapisovatelný adresář nebo upravte oprávnění OS |
| Neočekávaná výjimka `ResourceHandlingException` | Neslučitelnost verzí knihovny | Aktualizujte na nejnovější verzi `groupdocs-viewer` (`pip install --upgrade groupdocs-viewer`) |

**Tip od profíka**: Začněte s hloubkou 3 pro velmi velké stránky a postupně ji zvyšujte, dokud vizuální věrnost nesplní vaše požadavky.

## Okrajové případy, na které můžete narazit

1. **Dynamický obsah načítaný pomocí JavaScriptu** – Parser vidí jen statické HTML. Pokud vaše stránka spoléhá na skripty, které vkládají další zdroje, ty nebudou započítány do limitu hloubky. Zvažte předzpracování stránky pomocí headless prohlížeče před aplikací limitu.
2. **Cyklické reference** – Některé stránky obsahují iframe, které odkazují zpět na stejnou stránku. Počítadlo hloubky zabraňuje nekonečným smyčkám, ale můžete stále vidět částečně vykreslené sekce. Upravte `max_handling_depth` nebo ručně vyloučte problematické rámy.
3. **Smíšené protokoly (http/https)** – Pokud zdroje používají různé schémata, knihovna je může považovat za samostatné domény. Limit hloubky se stále aplikuje napříč protokoly, ale síťová oprávnění se mohou lišit. Ujistěte se, že vaše prostředí povoluje oba.

## Další kroky: pokročilé zpracování zdrojů

Nyní, když umíte **omezit hloubku zdrojů** a **aplikovat zpracování zdrojů**, můžete zkusit:

* **Vlastní filtry** – Použijte `resource_opts.resource_filter` k přeskočení konkrétních typů souborů (např. velkých videí).
* **Nastavení komprese** – Kombinujte `SaveOptions` s `compression_level` pro další zmenšení výstupu.
* **Dávkové zpracování** – Procházejte adresář HTML souborů a aplikujte stejný limit hloubky na každý z nich.

Tyto rozšíření vám umožní vytvořit kompletní pipeline optimalizace HTML pro rozsáhlé dokumentové workflow.

## Závěr

Naučili jste se, jak **omezit hloubku zdrojů** a **aplikovat zpracování zdrojů** při ukládání velkého HTML dokumentu v Pythonu. Konfigurací `ResourceHandlingOptions` a jejich připojením k `SaveOptions` získáte jemnou kontrolu nad tím, kolik vnořených zdrojů bude zpracováno, což vede k rychlejšímu ukládání a menším výstupním souborům. Experimentujte s různými hodnotami hloubky a dalšími `SaveOptions`, abyste chování přizpůsobili potřebám svého projektu.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, která vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vlastních projektech.

- [How to Set max_handling_depth in Aspose.HTML Python – Complete Guide](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [Create resource handling options and load an HTML document in Python](/html/english/python/general/create-resource-handling-options-and-load-an-html-document-i/)
- [How to Save HTML with Controlled Depth – Step‑by‑Step Python Guide](/html/english/python/general/how-to-save-html-with-controlled-depth-step-by-step-python-g/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}