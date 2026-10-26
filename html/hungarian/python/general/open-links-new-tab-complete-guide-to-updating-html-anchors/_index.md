---
category: general
date: 2026-07-05
description: Nyisd meg a linkeket új lapon Python segítségével – tanuld meg, hogyan
  adhatod hozzá a target="_blank" attribútumot, módosíthatod a link célját, használhatod
  az attribútumot tartalmazó szelektort, és könnyedén mentheted a módosított HTML-t.
draft: false
keywords:
- open links new tab
- add target blank
- change link target
- attribute contains selector
- save modified html
language: hu
og_description: Nyissa meg a linkeket új lapon gyorsan. Ez az útmutató bemutatja,
  hogyan adhatunk hozzá target='_blank' attribútumot, hogyan változtathatjuk meg a
  link célját, és hogyan menthetjük el a módosított HTML-t Python segítségével.
og_title: Linkek megnyitása új lapon – Lépésről lépésre HTML frissítési útmutató
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
title: Linkek megnyitása új lapon – Teljes útmutató a HTML horgonyok frissítéséhez
url: /hu/python/general/open-links-new-tab-complete-guide-to-updating-html-anchors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Linkek új lapon megnyitása – Teljes útmutató a HTML horgonyok frissítéséhez

Valaha szükséged volt **linkek új lapon megnyitására** egy statikus HTML oldalon, de nem tudtad, hol kezdjed? Nem vagy egyedül. Sok fejlesztő szembesül ezzel a problémával, amikor régi oldalakat tisztít vagy hozzáférhetőségi módosításokat végez. Ebben az útmutatóban egy gyakorlati megoldáson keresztül vezetünk, amely **hozzáadja a target blank-et**, **megváltoztatja a hivatkozás célját**, és biztonságosan **elmenti a módosított html-t** – minde néhány Python sorral.

Megmutatjuk, hogyan használj **attribútum tartalmazó szelektort**, így csak azokat a horgonyokat módosítod, amelyek valóban érdekelnek (például minden *example.com*-ra mutató hivatkozást). A végére egy újrahasználható szkriptet kapsz, amelyet bármely projektbe beilleszthetsz, legyen az nagy vagy kicsi.

## Mit fogsz megtanulni

- HTML fájlt betölteni egy manipulálható dokumentumobjektumba.  
- `<a>` elemek kiválasztása, amelyek `href` attribútuma egy adott részletet tartalmaz.  
- **target blank hozzáadása** és a `rel="noopener"` attribútum beállítása a biztonság javítása érdekében.  
- **Módosított html mentése** vissza a lemezre formázás elvesztése nélkül.  

Nincsenek külső függőségek a szabványos könyvtár és a **beautifulsoup4** (egy apró telepítés) kivételével. Ha már más elemzőt használsz, a koncepciók közvetlenül átültethetők.

---

## Előfeltételek

- Python 3.8+ telepítve a gépeden.  
- Alapvető ismeretek a HTML és a Python terén.  
- `beautifulsoup4` csomag (`pip install beautifulsoup4`).  

Ennyi—nincs szükség nehéz keretrendszerekre.

---

## 1. lépés: HTML dokumentum betöltése

Először is: be kell olvasnunk a forrásfájlt, és átadni a BeautifulSoup-nak. Gondolj rá úgy, mint egy üres vászonra, ahol új attribútumokat rajzolhatsz.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Path to the original HTML file
html_path = Path("YOUR_DIRECTORY/links.html")

# Read the file content
with html_path.open(encoding="utf-8") as f:
    soup = BeautifulSoup(f, "html.parser")
```

> **Miért fontos:** A `Path` használata kódként OS‑függetlenné teszi, és a `html.parser` beépített, így egyszerű feladatokhoz nem szükséges extra elemző.

---

## 2. lépés: Attribútum tartalmazó szelektor használata a megfelelő hivatkozások megtalálásához

Csak azokat a horgonyokat akarjuk módosítani, amelyek *example.com*-ra mutatnak. A `a[href*='example.com']` CSS szelektor pontosan ezt teszi – a `*=` azt jelenti, hogy „tartalmaz”. A BeautifulSoup `select` metódusa érti ezt a szintaxist.

```python
# Find all <a> tags whose href contains 'example.com'
selector = "a[href*='example.com']"
anchor_elements = soup.select(selector)
```

> **Pro tipp:** Ha kis- és nagybetű érzéketlen egyezésre van szükség, válts egy kis ciklusra, amely ellenőrzi: `if 'example.com' in a.get('href', '').lower()`.

Most a `anchor_elements` tartalmazza az összes érdekes hivatkozást, készen a következő átalakításra.

---

## 3. lépés: Hivatkozás céljának módosítása – Target Blank hozzáadása és a link biztonságossá tétele

Egy link új lapon való megnyitása olyan egyszerű, mint a `target="_blank"` beállítása. A modern böngészők azonban azt javasolják, hogy adjuk hozzá a `rel="noopener"` (vagy `noreferrer`) attribútumot, hogy megakadályozzuk az újonnan megnyitott oldal hozzáférését az eredeti ablakhoz a `window.opener` segítségével. Ez a kis biztonsági trükk megállíthatja a phishing támadásokat.

```python
for anchor in anchor_elements:
    # Open in a new tab
    anchor['target'] = "_blank"          # add target blank
    # Harden security
    anchor['rel'] = "noopener"           # prevent access to the opener page
```

> **Miért használunk közvetlen szótár‑hozzárendelést:** Automatikusan létrehozza az attribútumot, ha hiányzik, és felülírja, ha már létezik – tökéletes a **link céljának módosítása** művelethez.

---

## 4. lépés: Módosított HTML mentése vissza a lemezre

Az utolsó lépés a frissített markup egy új fájlba írása. Az eredeti érintetlen megtartása lehetővé teszi a visszaállítást, ha valami rosszul sül el.

```python
# Destination path for the updated HTML
output_path = Path("YOUR_DIRECTORY/links-updated.html")

# Write the prettified HTML (preserves indentation)
with output_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())
```

> **Mit csinál a `prettify()`:** Szép behúzással formázza a HTML-t, így a mentett fájl később könnyebben olvasható és összehasonlítható. Ha az eredeti szóközöket részesíted előnyben, cseréld a `prettify()`-t `str(soup)`-ra.

---

## Teljes szkript – egykattintásos megoldás

Az alábbiakban a teljes, azonnal futtatható szkript található. Mentsd el `update_links.py` néven, és futtasd a `python update_links.py` parancsot a terminálodból.

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

### Várható eredmény

Tegyük fel, hogy a `links.html` eredetileg a következőt tartalmazta:

```html
<a href="https://example.com/page1">Page 1</a>
<a href="https://other.com/home">Home</a>
```

A szkript futtatása után a `links-updated.html` így fog kinézni:

```html
<a href="https://example.com/page1" target="_blank" rel="noopener">Page 1</a>
<a href="https://other.com/home">Home</a>
```

Csak a *example.com*-ra mutató link kapta meg a **target blank hozzáadása** attribútumokat, ami azt mutatja, hogy a **attribútum tartalmazó szelektor** pontosan a kívánt módon működött.

---

## Gyakori kérdések és szélhelyzetek

### Mi van, ha egy link már rendelkezik `rel` attribútummal?

A ciklus felülírja `"noopener"` értékkel. Ha meg kell őrizned a meglévő értékeket (pl. `"nofollow"`), akkor összefűzheted őket:

```python
existing = a.get('rel', '')
a['rel'] = f"{existing} noopener".strip()
```

### Hogyan kezeljünk több domaint?

Egyszerűen bővítsd a szelektor listát:

```python
domains = ["example.com", "sample.org"]
selector = ",".join([f"a[href*='{d}']" for d in domains])
anchors = soup.select(selector)
```

### Módosítja a `prettify()` az eredeti HTML struktúrát?

Újra behúz, de nem változtatja meg a tagek sorrendjét vagy az attribútum értékeket. Ha pontosan az eredeti szóközöket kell megtartani, cseréld a `prettify()`-t `str(soup)`-ra, ahogy korábban említettük.

---

## Pro tippek a termelés‑kész szkriptekhez

- **Biztonsági mentés felülírás előtt:** Adj hozzá egy másolási lépést (`shutil.copy`), hogy az eredeti fájl biztonságban legyen.  
- **Naplózás a print helyett:** Használd a `logging` modult skálázható projektekhez.  
- **Kötegelt feldolgozás:** Használj ciklust egy könyvtáron a `Path.rglob("*.html")`-vel, hogy egy futtatásban sok fájlt frissíts.  

Ezek a finomítások egy egyszerű **linkek új lapon megnyitása** szkriptet robusztus eszközzé alakítanak bármely web‑karbantartási munkafolyamatban.

---

## Következtetés

Most már egy stabil, újrahasználható módszered van a **linkek új lapon megnyitására** bármely statikus HTML gyűjteményben. Az **attribútum tartalmazó szelektor** kihasználásával pontosan ott tudod **megváltoztatni a hivatkozás célját**, ahol szükséges, **target blank hozzáadása**, és **módosított html mentése** formázás elvesztése nélkül.

Próbáld ki egy tesztoldalon, majd skálázd fel az egész weboldalra. Szükség van a szelektor finomhangolására PDF-ekhez, vagy más domainekhez? Csak állítsd be a CSS karakterláncot – minden más változatlan marad.

Nyugodtan hagyj megjegyzést, ha valami furcsaságra bukkansz, vagy oszd meg, hogyan bővítetted a szkriptet a saját projektjeidben. Boldog kódolást, és legyen minden horgonyod pontosan ott, ahol szeretnéd!

## Mit érdemes legközelebb megtanulni?

A következő útmutatók szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás teljes, működő kódrészleteket tartalmaz lépésről‑lépésre magyarázatokkal, hogy elsajátíthasd a további API funkciókat és alternatív megvalósítási megközelítéseket a saját projektjeidben.

- [HTML szerkesztése Aspose.HTML for Java használatával](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [CSS hozzáadása – Inline CSS HTML dokumentumokhoz Aspose.HTML for Java-ban](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}