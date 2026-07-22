---
category: general
date: 2026-07-21
description: Hozzon létre erőforrás‑kezelési beállításokat Pythonban, és tanulja meg,
  hogyan állíthatja be a maximális kezelési mélységet a HTML‑elemzéshez. Kövesse ezt
  a lépésről‑lépésre útmutatót a megbízható erőforrás‑kezeléshez.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: hu
lastmod: 2026-07-21
og_description: Hozzon létre erőforrás-kezelési beállításokat Pythonban, és azonnal
  lássa, hogyan állítható be a maximális kezelési mélység a biztonságos HTML-dokumentum
  betöltéséhez. Mesteri szintre fejlesztheti a technikát percek alatt.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Erőforrás‑kezelési lehetőségek létrehozása Pythonban – Teljes lépésről‑lépésre
  útmutató
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Erőforrás-kezelési opciók létrehozása Pythonban – Teljes útmutató
url: /hu/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erőforrás‑kezelési beállítások létrehozása Pythonban – Teljes útmutató

Gondolkodtál már azon, hogyan **hozz létre erőforrás‑kezelési beállításokat** egy hatalmas HTML‑oldalhoz anélkül, hogy a memóriád kifogyna? Nem vagy egyedül. Amikor egy óriási dokumentumot adsz egy elemzőnek, a beágyazott erőforrások, mint a frame‑ek, iframe‑ek vagy a hivatkozott CSS, gyorsan kicsúszhatnak az irányítás alól.  

A jó hír? Megmondhatod az elemzőnek, hogy egy bizonyos beágyazási szint után álljon le. Ebben az útmutatóban megmutatjuk, **hogyan állítsd be a maximális kezelési mélységet** és tartsd a programod válaszkésznek. Készen állsz? Merüljünk el benne.

## Mit fogsz megtanulni

- Miért fontos a beágyazási mélység korlátozása a teljesítmény és a biztonság szempontjából.  
- A pontos kód, amellyel **erőforrás‑kezelési beállításokat hozhatsz létre** a `ResourceHandlingOptions` osztály segítségével.  
- Hogyan konfiguráld a `max_handling_depth` értékét, hogy az elemző három szint után megálljon.  
- Tippek a szélsőséges esetek kezelésére, például körkörös hivatkozásokkal vagy hiányzó erőforrásokkal rendelkező dokumentumok esetén.  

Előzetes ismeretek a könyvtárról nem szükségesek – csak egy működő Python 3 telepítés és az alapvető fájl‑I/O ismerete.

## Előfeltételek

- Python 3.8+ (a könyvtár minden friss verzióval működik).  
- A `htmlparser` csomag, amely biztosítja a `HTMLDocument` és a `ResourceHandlingOptions` osztályokat.  
- Egy minta HTML‑fájl (`big_page.html`), amelyet egy olyan mappában helyeztél el, ahonnan hivatkozhatsz rá.  

Ha még nem telepítetted a csomagot, futtasd:

```bash
pip install htmlparser
```

Most, hogy az alapok rendben vannak, térjünk rá a lényegre.

## Erőforrás‑kezelési beállítások létrehozása – 1. lépés

Elsőként szükséged van egy `ResourceHandlingOptions` példányra. Gondolj rá úgy, mint egy szerszámkészletre, ahol beállíthatod a korlátokat és a szabályokat, amelyeket az elemzőnek követnie kell.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Miért fontos ez:**  
Amikor az elemző egy `<iframe>`‑et talál egy másik `<iframe>`‑en belül, általában a láncot örökké követi. A mélység `3`‑ra korlátozásával megakadályozod a szabadon futó rekurziót, amely egyébként RAM‑ot fogyaszthat vagy stack‑overflow‑t okozhat.  

> **Pro tipp:** Ha nem megbízható tartalmat (pl. felhasználók által feltöltött HTML‑t) elemzel, fontold meg a mélység `1`‑re vagy `2`‑re csökkentését a lehetséges támadások mérséklése érdekében.

## HTML‑dokumentum betöltése – 2. lépés

Miután az opciók objektuma készen áll, add át a `HTMLDocument`‑nek. A konstruktor tiszteletben tartja a most beállított `max_handling_depth` értéket.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**Mi történik a háttérben?**  
A `HTMLDocument` beolvassa a fájlt, felépíti a DOM‑fát, majd végigjárja az összes külső erőforrást (stíluslapok, szkriptek, képek). Amikor beágyazott erőforráshoz ér, ellenőrzi a `resource_options.max_handling_depth` értékét. Ha a határ elérve, az elemző figyelmeztetést naplóz és kihagyja a további beágyazást.  

Ez azt jelenti, hogy az első három réteghez teljesen használható DOM‑ot kapsz, a többit pedig biztonságosan figyelmen kívül hagyja.

## A konfiguráció ellenőrzése – 3. lépés

Mindig jó ötlet megerősíteni, hogy a beállítások életbe léptek. A `resource_options` objektum ki tudja adni a jelenlegi állapotát, így kiírhatod vagy egy tesztben ellenőrizheted.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

Ha az állítás sikeres, biztos lehetsz benne, hogy az elemző a futás során betartja a korlátot.

## Szélsőséges esetek kezelése

### Körkörös hivatkozások

Néhány régi oldal egy iframe‑et ágyaz be, amely visszautal az eredeti oldalra, így hurkot hozva létre. A `max_handling_depth` beállításával a hurok automatikusan megszakad a harmadik iteráció után. Ennek ellenére előfordulhat, hogy egy figyelmeztetést látsz a naplóban. A zajos napló elnémításához állítsd be a logger szintjét:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Hiányzó erőforrások

Ha egy beágyazott erőforrás betöltése sikertelen (404 vagy hálózati időtúllépés), az elemző alapértelmezés szerint kivételt dob. A betöltési hívást tedd egy `try/except` blokkba, hogy az alkalmazásod tovább fusson:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Mélység dinamikus módosítása

Előfordulhat, hogy a csővezeték különböző részein eltérő mélységekre van szükség. Mivel a `resource_options` egy módosítható objektum, a `max_handling_depth` értékét futás közben megváltoztathatod:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Csak ne felejtsd el visszaállítani az értéket, mielőtt ugyanazt az opciós példányt egy másik szálban újra felhasználnád.

## Teljes működő példa

Az alábbiakban egy komplett szkriptet találsz, amelyet egyszerűen másolj‑be, állítsd be a fájl‑utakat, és azonnal futtathatsz.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**Várható kimenet (ha a fájlok léteznek és helyesek):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

Ha egy fájlt nem lehet beolvasni, egy hibaüzenetet kapsz ahelyett, hogy a program összeomlana.

![Create resource handling options in Python](/images/resource-options.png){alt="Erőforrás‑kezelési beállítások létrehozása Pythonban"}

## Összefoglalás – Miért nagyszerű ez a megközelítés

- **Biztonság először:** A beágyazási mélység korlátozása megakadályozza a szabadon futó rekurziót és a memória‑túlcsordulást.  
- **Rugalmasság:** A `max_handling_depth` értékét futás közben módosíthatod különböző forgatókönyvekhez.  
- **Egyszerűség:** Néhány sor kóddal **erőforrás‑kezelési beállításokat hozhatsz létre**, és azonnal alkalmazhatod őket.  

Röviden, most már egy robusztus mintát birtokolsz arra, hogyan szabályozd, hogy az elemző milyen mélységben kövesse a külső erőforrásokat.

## Mi a következő lépés?

- Fedezd fel a `ResourceHandlingOptions` osztály további lehetőségeit – vannak flag‑ek a gyorsítótárazásra, időkorlát‑kezelésre és MIME‑típus szűrésre.  
- Kombináld a mélység‑korlátozást egy egyedi `UserAgent` karakterlánccal, hogy elkerüld a túl szigorú szerverek blokkolását.  
- Ha aszinkron I/O‑val dolgozol, nézd meg az `aiohtmlparser` változatot, amely ugyanazokat a beállításokat támogatja, de az `asyncio`‑val működik.  

Kísérletezz nyugodtan: állítsd a mélységet `0`‑ra, és figyeld, ahogy az elemző minden külső hivatkozást figyelmen kívül hagy. Ez egy praktikus rövidítés, ha csak a nyers HTML‑markupt szeretnéd.

Van kérdésed, vagy egy makacs oldal akadályoz? Írj egy megjegyzést alább, és szívesen segítek a beállítások finomhangolásában. Jó elemzést!

## Mit érdemes még megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás komplett, működő kódrészleteket és lépésről‑lépésre magyarázatokat tartalmaz, hogy elsajátíthasd a további API‑funkciókat, és alternatív megvalósítási megközelítéseket is felfedezhess a saját projektjeidben.

- [Create HTML from String in C# – Custom Resource Handler Guide](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create sandbox for HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}