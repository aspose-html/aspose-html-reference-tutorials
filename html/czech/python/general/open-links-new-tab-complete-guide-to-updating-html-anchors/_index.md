---
category: general
date: 2026-07-05
description: Otevřete odkazy v novém panelu pomocí Pythonu – naučte se přidat target='_blank',
  změnit cíl odkazu, použít selektor obsahující atribut a snadno uložit upravený HTML.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: cs
og_description: Rychle otevřete odkazy v novém panelu. Tento tutoriál ukazuje, jak
  přidat target='_blank', změnit cíl odkazu a uložit upravený HTML pomocí Pythonu.
og_title: Otevřít odkazy v novém panelu – krok za krokem průvodce aktualizací HTML
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  headline: Open Links New Tab – Complete Guide to Updating HTML Anchors
  type: TechArticle
- description: Open links new tab using Python – learn how to add target blank, change
    link target, use attribute contains selector, and save modified html effortlessly.
  name: Open Links New Tab – Complete Guide to Updating HTML Anchors
  steps:
  - name: Expected Result
    text: 'Suppose `links.html` originally contained:'
  - name: What if a link already has a `rel` attribute?
    text: 'Our loop overwrites it with `"noopener"`. If you need to preserve existing
      values (e.g., `"nofollow"`), concatenate instead:'
  - name: How to handle multiple domains?
    text: 'Just expand the selector list:'
  - name: Does `prettify()` change the original HTML structure?
    text: It re‑indents but doesn’t alter tag order or attribute values. If you must
      keep the exact original whitespace, replace `prettify()` with `str(soup)` as
      mentioned earlier.
  type: HowTo
tags:
- HTML manipulation
- Python
- web automation
title: Otevřít odkazy v novém panelu – Kompletní průvodce aktualizací HTML kotvy
url: /cs/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Open Links New Tab – Kompletní průvodce aktualizací HTML odkazů

Už jste někdy potřebovali **open links new tab** na statické HTML stránce, ale nevedeli ste, kde začít? Nejste v tom sami. Mnoho vývojářů narazí na tento problém při úklidu starých stránek nebo při přidávání přístupových úprav. V tomto tutoriálu vás provedeme praktickým řešením, které **adds target blank**, **changes link target** a bezpečně **saves modified html** – vše pomocí několika řádků Pythonu.

Ukážeme si také, jak použít **attribute contains selector**, abyste se dotkli jen těch odkazů, na kterých vám opravdu záleží (například každého odkazu směřujícího na *example.com*). Na konci budete mít znovupoužitelný skript, který můžete vložit do jakéhokoli projektu, ať už je velký nebo malý.

## Co se naučíte

- Načíst HTML soubor do manipulovatelného dokumentového objektu.  
- Vybrat `<a>` elementy, jejichž atribut `href` obsahuje konkrétní podřetězec.  
- **Add target blank** a nastavit atribut `rel="noopener"` pro zvýšení bezpečnosti.  
- **Save modified html** zpět na disk bez ztráty formátování.  

Žádné externí závislosti kromě standardní knihovny a **beautifulsoup4** (malá instalace). Pokud už používáte jiný parser, koncepty se přenášejí přímo.

---

## Předpoklady

- Python 3.8+ nainstalovaný na vašem počítači.  
- Základní znalost HTML a Pythonu.  
- Balíček `beautifulsoup4` (`pip install beautifulsoup4`).  

To je vše – žádné těžké frameworky nejsou potřeba.

---

## Krok 1: Načtení HTML dokumentu

Nejprve musíme přečíst zdrojový soubor a předat ho BeautifulSoup. Představte si to jako otevření prázdného plátna, kde můžete kreslit nové atributy.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Proč je to důležité:** Použití `Path` udržuje kód OS‑agnostický a `html.parser` je vestavěný, takže pro jednoduché úkoly nepotřebujete další parsery.

---

## Krok 2: Použití Attribute Contains Selector pro nalezení správných odkazů

Chceme zasáhnout jen kotvy, které ukazují na *example.com*. CSS selektor `a[href*='example.com']` dělá přesně to – `*=` znamená „obsahuje“. Metoda `select` v BeautifulSoup rozumí této syntaxi.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Tip:** Pokud potřebujete shodu bez ohledu na velikost písmen, přepněte na malou smyčku, která kontroluje `if 'example.com' in a.get('href', '').lower()`.

Nyní `anchor_elements` obsahuje všechny odkazy, na které nám záleží, připravené na další transformaci.

---

## Krok 3: Změna cíle odkazu – Add Target Blank a zabezpečení odkazu

Otevření odkazu v novém panelu je tak jednoduché jako nastavit `target="_blank"`. Moderní prohlížeče však doporučují také přidat `rel="noopener"` (nebo `noreferrer`), aby nově otevřená stránka nemohla přistupovat k původnímu oknu přes `window.opener`. Tento malý bezpečnostní trik může zastavit phishingové útoky.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Proč používáme přímé přiřazení do slovníku:** Automaticky vytvoří atribut, pokud chybí, a přepíše ho, pokud už existuje – ideální pro operaci **change link target**.

---

## Krok 4: Uložení upraveného HTML zpět na disk

Poslední krok je zapsat aktualizovaný markup do nového souboru. Zachování originálu neporušeného vám umožní vrátit se zpět, pokud něco selže.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **Co dělá `prettify()`:** Formátuje HTML s pěkným odsazením, což usnadňuje čtení a porovnání souboru později. Pokud dáváte přednost původnímu whitespace, nahraďte `prettify()` výrazem `str(soup)`.

---

## Kompletní skript – Řešení jedním kliknutím

Níže je kompletní, připravený ke spuštění skript. Uložte jej jako `update_links.py` a spusťte `python update_links.py` z terminálu.

```python
#!/usr/bin/env python3
"""
Open Links New Tab – script that adds target blank,
sets rel="noopener", and saves modified html.
"""

from pathlib import Path
from bs4 import BeautifulSoup

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Load the HTML document
    # ------------------------------------------------------------------
    html_path = Path("YOUR_DIRECTORY/links.html")
    with html_path.open(encoding="utf-8") as f:
        soup = BeautifulSoup(f, "html.parser")

    # ------------------------------------------------------------------
    # 2️⃣ Select anchors with an attribute contains selector
    # ------------------------------------------------------------------
    selector = "a[href*='example.com']"
    anchors = soup.select(selector)

    # ------------------------------------------------------------------
    # 3️⃣ Change link target – add target blank & secure the link
    # ------------------------------------------------------------------
    for a in anchors:
        a['target'] = "_blank"          # add target blank
        a['rel'] = "noopener"           # prevent opener access

    # ------------------------------------------------------------------
    # 4️⃣ Save modified html to a new file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/links-updated.html")
    with output_path.open("w", encoding="utf-8") as f:
        f.write(soup.prettify())

    print(f"✅ Updated {len(anchors)} link(s) and saved to {output_path}")

if __name__ == "__main__":
    main()
```

### Očekávaný výsledek

Předpokládejme, že `links.html` původně obsahoval:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Po spuštění skriptu bude `links-updated.html` vypadat takto:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Pouze odkaz na *example.com* získal **add target blank** atributy, což dokazuje, že náš **attribute contains selector** fungoval přesně podle očekávání.

---

## Často kladené otázky a okrajové případy

### Co když odkaz už má atribut `rel`?

Naše smyčka jej přepíše na `"noopener"`. Pokud potřebujete zachovat existující hodnoty (např. `"nofollow"`), spojte je:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Jak řešit více domén?

Stačí rozšířit seznam selektorů:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### Mění `prettify()` původní strukturu HTML?

Přeformátuje odsazení, ale nemění pořadí tagů ani hodnoty atributů. Pokud musíte zachovat přesně původní whitespace, nahraďte `prettify()` výrazem `str(soup)` jak bylo zmíněno výše.

---

## Profesionální tipy pro produkčně připravené skripty

- **Záloha před přepsáním:** Přidejte krok kopírování (`shutil.copy`) pro bezpečné uchování originálního souboru.  
- **Logování místo print:** Použijte modul `logging` pro škálovatelné projekty.  
- **Dávkové zpracování:** Procházejte adresář pomocí `Path.rglob("*.html")` a aktualizujte mnoho souborů najednou.  

Tyto úpravy promění jednoduchý **open links new tab** skript na robustní nástroj pro jakýkoli workflow údržby webu.

---

## Závěr

Nyní máte solidní, znovupoužitelnou metodu pro **open links new tab** napříč libovolnou kolekcí statických HTML souborů. Využitím **attribute contains selector** můžete **change link target** přesně tam, kde to potřebujete, **add target blank** a **save modified html** bez ztráty formátování.

Vyzkoušejte to na testovací stránce, pak to rozšiřte na celý web. Potřebujete upravit selektor pro PDF, jiné domény nebo jiné typy souborů? Stačí změnit CSS řetězec – vše ostatní zůstane stejné.

Neváhejte zanechat komentář, pokud narazíte na nějaké problémy, nebo podělit se o to, jak jste skript rozšířili pro své vlastní projekty. Šťastné kódování a ať se všechny vaše kotvy otevřou přesně tam, kde chcete!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným krok‑za‑krokem vysvětlením, aby vám pomohl zvládnout další API funkce a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}