---
category: general
date: 2026-05-31
description: Vytvořte instanci ResourceHandlingOptions pro řízení načítání HTML zdrojů.
  Naučte se, jak omezit hloubku zdrojů a načíst HTMLDocument s vlastními možnostmi.
draft: false
keywords:
- create resourcehandlingoptions instance
- limit resource depth
- HTMLDocument options
- resource loading configuration
- python html parsing
language: cs
og_description: Vytvořte instanci ResourceHandlingOptions pro řízení načítání HTML
  zdrojů. Tento návod ukazuje, jak nastavit maximální hloubku zpracování a načíst
  HTMLDocument s vlastními možnostmi.
og_title: Vytvořit instanci ResourceHandlingOptions pro načítání HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create ResourceHandlingOptions instance to control HTML resource loading.
    Learn how to limit resource depth and load an HTMLDocument with custom options.
  headline: Create ResourceHandlingOptions Instance for HTML Loading
  type: TechArticle
tags:
- Python
- HTML parsing
- Resource handling
title: Vytvořit instanci ResourceHandlingOptions pro načítání HTML
url: /cs/python/general/create-resourcehandlingoptions-instance-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření instance ResourceHandlingOptions pro načítání HTML

Už jste se někdy zamýšleli, jak **vytvořit instanci ResourceHandlingOptions**, aby se vám obrovská HTML stránka nerozpadla na parseru? Nejste v tom sami — velké dokumenty s vnořenými skripty, rámy nebo zahrnutími mohou rychle proměnit jednoduché stahování v noční můru.  

V tomto tutoriálu projdeme přesně kroky, jak vytvořit objekt `ResourceHandlingOptions`, omezit úroveň vnoření a předat jej do `HTMLDocument`. Na konci budete mít čistý, opakovatelný vzor pro **konfiguraci načítání zdrojů**, který funguje s jakýmkoli obrovským HTML souborem.

## Co se naučíte

- Proč je instance `ResourceHandlingOptions` důležitá při parsování masivních stránek.  
- Jak **omezit hloubku zdrojů**, aby se zabránilo nekonečné rekurzi.  
- Přesná syntaxe pro načtení `HTMLDocument` s vašimi vlastními možnostmi.  
- Kompletní, spustitelný příklad, který můžete dnes vložit do svého projektu.  

**Požadavky:** Python 3.8+, knihovna `htmlparser`, která poskytuje `HTMLDocument` a `ResourceHandlingOptions`. Žádné další závislosti nejsou potřeba.

---

## Krok 1: Vytvoření instance ResourceHandlingOptions

Prvním, co potřebujete, je čerstvý objekt `ResourceHandlingOptions`. Představte si jej jako ovládací panel pro každý externí zdroj, na který může parser narazit — skripty, obrázky, iframe, co jen chcete.

```python
# Step 1: Initialize the options object
options = ResourceHandlingOptions()
```

> **Proč je to důležité:** Bez explicitní instance se parser vrátí k výchozím nastavením, což často znamená „načíst vše“. Pro obrovské stránky může toto výchozí nastavení spotřebovat gigabajty paměti a zastavit váš skript.

---

## Krok 2: Omezení hloubky zdrojů

Dále řekneme možnostem, jak hluboko jsme ochotni jít. Nastavení `max_handling_depth` na 5 například zastaví parser po pěti úrovních vnořených zdrojů. Upravit číslo podle vašeho konkrétního případu.

```python
# Step 2: Cap the nesting depth (e.g., stop after 5 levels)
options.max_handling_depth = 5
```

> **Tip:** Pokud vás zajímá jen obsah nejvyšší úrovně, hloubka 1 nebo 2 je obvykle dostačující a výrazně zrychlí zpracování.

---

## Krok 3: Načtení HTML dokumentu s možnostmi

Nyní předáme nakonfigurované `options` do `HTMLDocument`. Konstruktor přijímá cestu k souboru (nebo URL) a objekt možností, což vám poskytuje detailní kontrolu nad tím, co se načte.

```python
# Step 3: Parse the HTML file using the configured options
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
```

> **Co uvidíte:** Parser načte `big_page.html`, ale jakýkoli zdroj, který by způsobil překročení hloubky 5, bude tiše ignorován. To zabraňuje nekontrolované rekurzi a udržuje předvídatelnou spotřebu paměti.

---

## Krok 4: Ověření výsledku (volitelné, ale užitečné)

Je dobrým zvykem zkontrolovat, že se dokument načetl podle očekávání. Níže je rychlá kontrola, která vypíše počet úspěšně zpracovaných zdrojů.

```python
# Step 4: Quick verification
print(f"Handled resources: {len(doc.resources)}")
print(f"Document title: {doc.title}")
```

**Očekávaný výstup** (vaše čísla se budou lišit podle vstupního souboru):

```
Handled resources: 12
Document title: Example Large Page
```

Pokud je počet výrazně nižší, než jste očekávali, možná budete muset zvýšit `max_handling_depth` nebo upravit jiné vlastnosti `ResourceHandlingOptions`.

---

## Běžné varianty a okrajové případy

| Situace | Úprava |
|-----------|------------|
| **Potřebujete ignorovat jen obrázky** | Set `options.ignore_images = True`. |
| **Skripty způsobují timeouty** | Use `options.max_script_execution_time = 2` (seconds). |
| **Parsování vzdálené URL místo souboru** | Pass the URL string to `HTMLDocument` just like a file path. |
| **Chcete vlastní logger** | Assign `options.logger = my_logger` before loading. |

Tyto úpravy jsou součástí nástroje **HTMLDocument options** a umožňují vám jemně doladit **konfiguraci načítání zdrojů** bez přepisování parseru.

---

## Kompletní funkční příklad

Spojením všech částí získáte samostatný skript, který můžete spustit hned teď. Uložte jej jako `parse_big_page.py` a spusťte pomocí `python parse_big_page.py`.

```python
# parse_big_page.py
from htmlparser import HTMLDocument, ResourceHandlingOptions

def main():
    # 1️⃣ Create the options instance
    options = ResourceHandlingOptions()
    
    # 2️⃣ Limit how deep we go into nested resources
    options.max_handling_depth = 5
    
    # Optional: ignore images to speed things up
    # options.ignore_images = True
    
    # 3️⃣ Load the document with our custom options
    doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
    
    # 4️⃣ Verify the load
    print(f"Handled resources: {len(doc.resources)}")
    print(f"Document title: {doc.title}")

if __name__ == "__main__":
    main()
```

Spusťte jej a měli byste vidět vytištěný počet zdrojů a název, což potvrzuje, že jste úspěšně **vytvořili instanci ResourceHandlingOptions** a použili ji.

---

## Závěr

Právě jsme vám ukázali, jak **vytvořit instanci ResourceHandlingOptions**, omezit úroveň vnoření a předat ji do `HTMLDocument`. Tento vzor vám poskytuje spolehlivou **konfiguraci načítání zdrojů** pro jakýkoli velký HTML soubor, což udržuje vaše Python HTML parsování rychlé a šetrné k paměti.

Jste připraveni na další krok? Vyzkoušejte změnit limit hloubky, přepnout `ignore_images`, nebo integrovat vlastní logger — každá úprava vás naučí více o **HTMLDocument options** a o tom, jak spolupracují s vaším datovým kanálem.  

Pokud se vám tento průvodce hodil, neváhejte jej sdílet, dát hvězdičku repozitáři nebo zanechat komentář s vlastními tipy. Šťastné parsování!

## Co byste se měli naučit dál?

- [Vytvořit HTML ze stringu v C# – Průvodce vlastním manipulátorem zdrojů](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Jak uložit HTML v C# – Kompletní průvodce s použitím vlastního manipulátoru zdrojů](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Vytvořit Stream Provider v .NET s Aspose.HTML](/html/english/net/advanced-features/create-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}