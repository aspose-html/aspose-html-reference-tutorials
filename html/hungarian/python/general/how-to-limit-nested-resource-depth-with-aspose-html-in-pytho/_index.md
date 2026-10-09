---
category: general
date: 2026-10-09
description: Tanulja meg, hogyan korlátozhatja a beágyazott erőforrások mélységét
  az Aspose.HTML ResourceHandlingOptions használatával Pythonban. Szabályozza a max_handling_depth
  értékét a biztonságos HTML konverzió érdekében.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit nested resource depth
- Aspose.HTML ResourceHandlingOptions
- Python resource handling
- max_handling_depth
- nested HTML resources
language: hu
lastmod: 2026-10-09
og_description: Korlátozza a beágyazott erőforrások mélységét az Aspose.HTML ResourceHandlingOptions
  használatával Pythonban. Állítsa be a max_handling_depth értéket, hogy megvédje
  HTML konverziós munkafolyamatát.
og_image_alt: Screenshot showing limit nested resource depth setting in Python
og_title: Hogyan korlátozhatja a beágyazott erőforrások mélységét az Aspose.HTML használatával
  Pythonban
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  headline: How to limit nested resource depth with Aspose.HTML in Python
  type: TechArticle
- description: Learn to limit nested resource depth using Aspose.HTML ResourceHandlingOptions
    in Python. Control max_handling_depth for safe HTML conversion.
  name: How to limit nested resource depth with Aspose.HTML in Python
  steps:
  - name: What the setting does
    text: '- **Depth 0** – The root HTML document is processed, but no external resources
      are fetched. - **Depth 1** – Direct resources referenced by the root (e.g.,
      `<img src="...">`, `<link href="...">`) are fetched. - **Depth 2** – Resources
      referenced by the first‑level resources (e.g., CSS files that impo'
  - name: Using the options with a converter
    text: After configuring the depth limit, pass the `resource_options` object to
      the `HtmlConverter` (or any Aspose.HTML API that accepts `ResourceHandlingOptions`).
  - name: 1. Disabling depth limiting entirely
    text: Set the property to a very high number (e.g., `sys.maxsize`) or `None` if
      you want unrestricted handling. Use this only when you trust the source HTML.
  - name: 2. Handling missing resources
    text: When the depth limit stops a resource from being fetched, Aspose.HTML logs
      a warning but continues. You can capture these warnings by attaching a custom
      logger to the converter if you need audit trails.
  - name: 3. Combining with other resource options
    text: '`ResourceHandlingOptions` also offers `allow_external_resources`, `download_timeout`,
      and `max_resource_size`. Pairing a depth limit with a size limit provides a
      robust safety net.'
  - name: 4. Testing the limit
    text: Create a test HTML hierarchy with nested `<iframe>` tags or CSS `@import`
      statements to verify that your depth limit behaves as expected before deploying
      to production.
  type: HowTo
tags:
- Aspose.HTML
- Python
- HTML conversion
- Resource handling
title: Hogyan korlátozhatja a beágyazott erőforrások mélységét az Aspose.HTML használatával
  Pythonban
url: /hu/python/general/how-to-limit-nested-resource-depth-with-aspose-html-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan korlátozhatja a beágyazott erőforrások mélységét az Aspose.HTML használatával Pythonban

## Előfeltételek

- Python 3.8 vagy újabb telepítve  
- Az `aspose.html` csomag (`pip install aspose-html`)  
- Alapvető ismeretek az Aspose.HTML konverziós munkafolyamatáról  

Ezek az egyetlen függőségek a lenti példákhoz.

## 1. lépés: Importálja a **ResourceHandlingOptions** osztályt

Az első lépés, hogy behozza a `ResourceHandlingOptions` osztályt a szkriptjébe. Ez az osztály csoportosítja az összes beállítást, amely befolyásolja, hogyan kerülnek lekérdezésre és feldolgozásra a külső erőforrások (képek, CSS, szkriptek stb.) a konverzió során.

```python
# Step 1: Import the ResourceHandlingOptions class
from aspose.html import ResourceHandlingOptions
```

**Miért fontos:**  
A `ResourceHandlingOptions` elkülöníti az erőforrás‑kapcsolódó beállításokat a többi konverziós opciótól, lehetővé téve, hogy finomhangolja a beágyazott erőforrások kezelését anélkül, hogy befolyásolná a renderelést vagy a kimeneti formátumot.

## 2. lépés: Hozzon létre egy példányt a beállítási objektumból

Példányosítsa a `ResourceHandlingOptions`‑t, hogy módosíthassa a tulajdonságait. Az alapértelmezett példány korlátlan beágyazást engedélyez, ami teljesítményproblémákat vagy akár verem túlcsordulást is okozhat rosszul megírt oldalak esetén.

```python
# Step 2: Create an instance of the options object
resource_options = ResourceHandlingOptions()
```

**Pro tipp:**  
Ha ugyanazt a mélységkorlátot sok konverzióban szeretné újrahasználni, tárolja a konfigurált objektumot egy modul‑szintű változóban, hogy elkerülje annak újra‑létrehozását minden alkalommal.

## 3. lépés: Állítsa be a **max_handling_depth** értékét a beágyazott erőforrások mélységének korlátozásához

Rendelje hozzá a `max_handling_depth` tulajdonságot a maximálisan engedélyezett beágyazott szintek számához. Ebben a példában a **3** szint után állunk le, de választhat bármilyen egész számot, amely megfelel az Ön helyzetének.

```python
# Step 3: Limit the depth of nested resource handling (stop after 3 levels)
resource_options.max_handling_depth = 3
```

### Mit csinál a beállítás

- **Depth 0** – A gyökér HTML dokumentum feldolgozásra kerül, de külső erőforrások nem kerülnek lekérdezésre.  
- **Depth 1** – A gyökér által közvetlenül hivatkozott erőforrások (pl. `<img src="...">`, `<link href="...">`) lekérdezésre kerülnek.  
- **Depth 2** – Az első szintű erőforrások által hivatkozott erőforrások (pl. más CSS‑t importáló CSS‑fájlok) lekérdezésre kerülnek.  
- **Depth 3** – A folyamat a harmadszintű erőforrások kezelése után leáll. A további beágyazott hivatkozások figyelmen kívül maradnak.

A `max_handling_depth` beállítás megvédi az alkalmazását a következőktől:

| Kockázat | Hogyan segít a korlát |
|------|----------------------|
| **Végtelen rekurzió** körkörös hivatkozások miatt | A konverter a meghatározott mélység után leáll, megszakítva a ciklust. |
| **Túlzott hálózati forgalom**, amikor egy oldal tucatnyi láncolt stíluslapot tölt be | Csak az első néhány szint kerül letöltésre, csökkentve a sávszélességet. |
| **Memória túlcsordulás** hatalmas erőforrásfák betöltésekor | Kevesebb objektum jön létre, így a memóriahasználat előre látható marad. |

### A beállítások használata egy konverterrel

A mélységkorlát beállítása után adja át a `resource_options` objektumot a `HtmlConverter`‑nek (vagy bármely Aspose.HTML API‑nak, amely elfogadja a `ResourceHandlingOptions`‑t).

```python
from aspose.html import HtmlConverter, SaveFormat

# Create a converter with the resource handling options
converter = HtmlConverter(resource_options)

# Convert a sample HTML file to PDF while respecting the depth limit
converter.convert("sample.html", "output.pdf", SaveFormat.PDF)

print("Conversion completed with max_handling_depth =", resource_options.max_handling_depth)
```

**Várható kimenet**

```
Conversion completed with max_handling_depth = 3
```

Ha a forrás HTML a harmadik szintet meghaladó erőforrásokat tartalmaz, azok kihagyásra kerülnek a PDF‑ből, és a konverzió továbbra is gyorsan befejeződik.

## Szélsőséges esetek és gyakori variációk

### 1. A mélységkorlátozás teljes letiltása

Állítsa a tulajdonságot egy nagyon magas számra (pl. `sys.maxsize`) vagy `None`‑ra, ha korlátlan kezelést szeretne. Ezt csak akkor használja, ha megbízik a forrás HTML‑ben.

```python
import sys
resource_options.max_handling_depth = sys.maxsize  # effectively unlimited
```

### 2. Hiányzó erőforrások kezelése

Amikor a mélységkorlát megakadályozza egy erőforrás lekérdezését, az Aspose.HTML figyelmeztetést naplóz, de folytatja. Ezeket a figyelmeztetéseket egy egyedi naplózó csatolásával a konverterhez rögzítheti, ha audit nyomokra van szüksége.

### 3. Kombinálás más erőforrás-beállításokkal

A `ResourceHandlingOptions` továbbá kínálja az `allow_external_resources`, `download_timeout` és `max_resource_size` beállításokat. A mélységkorlát és egy méretkorlát párosítása erős biztonsági hálót nyújt.

```python
resource_options.allow_external_resources = True
resource_options.max_resource_size = 5 * 1024 * 1024  # 5 MiB per resource
```

### 4. A korlát tesztelése

Hozzon létre egy teszt HTML hierarchiát beágyazott `<iframe>` címkékkel vagy CSS `@import` utasításokkal, hogy ellenőrizze, a mélységkorlát a várt módon működik-e, mielőtt éles környezetbe helyezné.

## Gyakorlati tippek (E‑E‑A‑T)

- **Érvényesítse a bemeneti URL‑eket** a konverzió előtt, hogy elkerülje a felesleges hálózati hívásokat.  
- **Naplózza a ténylegesen elért mélységet** (`converter.handling_depth_reached`) a felügyelethez.  
- **Használja újra ugyanazt a `ResourceHandlingOptions`‑t** több konverzió során, hogy a konfiguráció konzisztens maradjon.  
- **Profilozza a teljesítményt** a mélység változtatásakor; az alacsonyabb korlát általában felgyorsítja a konverziót, de elhagyhat szükséges eszközöket.  

## Összegzés

Most már tudja, hogyan **korlátozhatja a beágyazott erőforrások mélységét** az Aspose.HTML Python használatakor a `ResourceHandlingOptions` `max_handling_depth` tulajdonságának beállításával. Ez az egyetlen beállítás védi a konverziós csővezetékét a szabadon futó rekurziótól, a túlzott hálózati használattól és a memóriahullámoktól, miközben finomhangolt irányítást biztosít a erőforrásfák feldolgozásának mélysége felett.

Készen áll a további felfedezésre? Próbálja meg kombinálni a mélységkorlátot a `max_resource_size`‑szel, hogy teljesen megerősített HTML‑PDF konverziós munkafolyamatot hozzon létre, vagy olvassa el útmutatónkat a **Aspose.HTML erőforráskezelésről** a `allow_external_resources` és a timeout kezelés mélyebb megértéséhez.

--- 

*Image illustrating the depth‑limit setting (optional):*  
![Képernyőfelvétel, amely a beágyazott erőforrások mélységkorlát beállítását mutatja Pythonban](placeholder.png "beágyazott erőforrások mélységkorlát beállítása")

## Mit érdemes legközelebb megtanulni?

A következő oktatóanyagok szorosan kapcsolódó témákat fednek le, amelyek a jelen útmutatóban bemutatott technikákra épülnek. Minden forrás tartalmaz teljes, működő kódrészleteket lépésről‑lépésre magyarázatokkal, hogy segítsen elsajátítani további API‑funkciókat és alternatív megvalósítási megközelítéseket saját projektjeiben.

- [Egyéni erőforráskezelő az Aspose HTML‑ben – Mentés streambe útmutató](/html/english/net/advanced-features/custom-resource-handler-in-aspose-html-save-to-stream-guide/)
- [HTML mentése C#‑ben – Teljes útmutató egy egyéni erőforráskezelő használatával](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Üzenetkezelés és hálózatkezelés az Aspose.HTML‑ben Java számára](/html/english/java/message-handling-networking/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}