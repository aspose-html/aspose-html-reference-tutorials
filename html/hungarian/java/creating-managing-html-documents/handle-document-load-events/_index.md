---
date: 2026-04-23
description: Ismerje meg, hogyan lehet lekérni a külső HTML-t és megvárni a dokumentum
  betöltését az Aspose.HTML for Java használatával ebben a lépésről‑lépésre útmutatóban.
keywords:
- get outer html
- wait for document load
- java html processing
- navigate html document
- aspose html example
linktitle: Dokumentumbetöltési események kezelése az Aspose.HTML-ben
second_title: Java HTML Processing with Aspose.HTML
title: Külső HTML lekérése és betöltési események kezelése az Aspose.HTML for Java-ban
url: /hu/java/creating-managing-html-documents/handle-document-load-events/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Külső HTML lekérése és betöltési események kezelése az Aspose.HTML for Java-ban

## Bevezetés
Amikor **get outer html**-t kell lekérned egy távoli oldalról, és azonnal reagálni szeretnél, amint a dokumentum befejezi a betöltést, a dokumentum betöltési események kezelése elengedhetetlen. Java-ban az Aspose.HTML tiszta API-t biztosít, amellyel navigálhatsz egy URL-re, és figyelheted az `OnLoad` eseményt, így biztonságosan hozzáférhetsz a HTML-hez, amikor az készen áll. Ez a tutorial végigvezet a teljes folyamaton – a környezet beállításától a betöltött oldal külső HTML-jének kiírásáig – hogy bármely web‑központú Java alkalmazásba integrálhasd.

## Gyors válaszok
- **Mi jelent a “get outer html”?** Visszaadja a dokumentum gyökérelem teljes HTML jelölését.  
- **Melyik könyvtár kezeli a betöltési eseményeket?** Az Aspose.HTML for Java biztosítja az `OnLoad` eseményt.  
- **Szükségem van licencre a teszteléshez?** Elérhető egy ingyenes próba; a gyártási környezethez kereskedelmi licenc szükséges.  
- **Hogyan várhatok a dokumentum betöltésére?** Használd az `OnLoad` kezelőt vagy egy egyszerű alvást demo célokra.  
- **Ez a megközelítés aszinkron‑biztonságos?** Igen, az esemény a dokumentum betöltése után aktiválódik, biztosítva, hogy a HTML készen áll.

## Mi az a “get outer html”?
`document.getDocumentElement().getOuterHTML()` visszaadja a dokumentum gyökérelem teljes HTML karakterláncát, beleértve a nyitó és záró címkéket. Ez akkor hasznos, ha a nyers jelölésre van szükség további feldolgozáshoz, tároláshoz vagy átalakításhoz.

## Miért használjuk az Aspose.HTML for Java-t?
- **Robusztus HTML elemzés** böngésző motor használata nélkül.  
- **Esemény‑vezérelt modell** lehetővé teszi, hogy pontosan akkor reagálj, amikor a dokumentum készen áll.  
- **Kereszt‑platform** támogatás Windows, Linux és macOS rendszerekhez.  
- **Gazdag API** navigációhoz, manipulációhoz és PDF, kép stb. konvertáláshoz.

## Előfeltételek
Mielőtt belemerülnénk a kódba, győződj meg róla, hogy a következőkkel rendelkezel:

1. **Java Development Kit (JDK)** – Telepítsd a [Oracle weboldaláról](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html).  
2. **Aspose.HTML for Java** – Töltsd le a legújabb JAR-t az [Aspose kiadási oldaláról](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse vagy bármely kedvelt szerkesztő.  
4. **Alap Java ismeretek** – Az osztályok, metódusok és eseménykezelés megértése.  
5. **Internetkapcsolat** – A példa egy online HTML oldalt tölt be.

Miután minden készen áll, már csak a kódolásra van szükséged!

## Lépés‑ről‑lépésre útmutató

### 1. lépés: HTML dokumentum inicializálása
Először hozz létre egy `HTMLDocument` példányt. Emellett beállítunk egy `AtomicBoolean`-t a betöltési állapot nyomon követésére.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument();
java.util.concurrent.atomic.AtomicBoolean isLoading = new java.util.concurrent.atomic.AtomicBoolean(false);
```

### 2. lépés: Feliratkozás az **OnLoad** eseményre
Csatolj egy kezelőt, amely a `isLoading` jelzőt megfordítja, amint a dokumentum befejezi a betöltést. Itt tudjuk meg, hogy biztonságosan meghívhatjuk a **get outer html**-t.

```java
document.OnLoad.add(new DOMEventHandler() {
    @Override
    public void invoke(Object o, Event event) {
        isLoading.set(true);
    }
});
```

### 3. lépés: Navigálás a dokumentumhoz (HTML betöltése URL-ről)
Add meg a `HTMLDocument`-nek, melyik oldalt kell lekérnie. Ebben a példában egy nyilvános Aspose dokumentációs oldalt töltünk be.

```java
document.navigate("https://docs.aspose.com/html/net/creating-a-document/document.html");
```

### 4. lépés: Várakozás a dokumentum betöltésére
Egy távoli oldal betöltése aszinkron. Demonstrációs célra pár másodpercre szüneteltetjük a szálat; a gyártásban a `OnLoad` jelzőre vagy egy kifinomultabb szinkronizációs technikára támaszkodnál.

```java
Thread.sleep(5000);
```

### 5. lépés: A betöltött dokumentum elérése és **Get Outer HTML**
Most, hogy a `isLoading` igaz, lekérheted a dokumentum gyökérelem teljes jelölését.

```java
System.out.println("outerHTML = " + document.getDocumentElement().getOuterHTML());
```

A konzolon meg kell jelennie a betöltött oldal teljes HTML-jének.

## Gyakori problémák és megoldások
| Issue | Reason | Fix |
|-------|--------|-----|
| **`isLoading` sosem lesz igaz** | Az `OnLoad` kezelő nem lett csatolva a `navigate()` előtt | Csatold a kezelőt **a `navigate()` hívása előtt**. |
| **`NullPointerException` a `getDocumentElement()`-nél** | A dokumentum nem volt teljesen betöltve a hozzáféréskor | Használj megfelelő várakozási mechanizmust (pl. ciklus `isLoading.get()`-on vagy `CountDownLatch`). |
| **SSLHandshakeException** HTTPS URL-ek betöltésekor | Hiányzó megbízható tanúsítványok | Add hozzá a megfelelő tanúsítványt a Java kulcstáradhoz vagy használd a `-Djsse.enableSNIExtension=false` beállítást. |
| **Lassú betöltés időtúllépést okoz** | Nagy oldal vagy hálózati késleltetés | Növeld a szünet időtartamát vagy valósíts meg egy időtúllépés‑érzékeny hallgatót. |

## Gyakran Ismételt Kérdések

**Q: Mi az az Aspose.HTML for Java?**  
A: Az Aspose.HTML for Java egy könyvtár, amely lehetővé teszi a fejlesztők számára, hogy HTML dokumentumokat hozzanak létre, manipuláljanak és konvertáljanak Java alkalmazásokban.

**Q: Hogyan tölthetem le az Aspose.HTML for Java-t?**  
A: Letöltheted a [Aspose kiadási oldaláról](https://releases.aspose.com/html/java/).

**Q: Használhatom ingyen az Aspose.HTML-t?**  
A: Igen, ingyen kipróbálhatod az Aspose.HTML-t, ha letöltesz egy próbaverziót a [Aspose weboldaláról](https://releases.aspose.com/).

**Q: Van elérhető támogatás az Aspose.HTML-hez?**  
A: Igen, támogatást találsz és kérdéseket tehetsz fel a [Aspose fórumon](https://forum.aspose.com/c/html/29).

**Q: Hogyan szerezhetek ideiglenes licencet az Aspose.HTML-hez?**  
A: Ideiglenes licencet kérhetsz a [Aspose ideiglenes licenc oldalán](https://purchase.aspose.com/temporary-license/).

---

**Utolsó frissítés:** 2026-04-23  
**Tesztelve:** Aspose.HTML for Java 24.11  
**Szerző:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}