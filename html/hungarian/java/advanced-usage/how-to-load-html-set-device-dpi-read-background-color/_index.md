---
category: general
date: 2026-02-16
description: Hogyan töltsünk be HTML-t Java-ban, állítsuk be az eszköz DPI-jét, definiáljunk
  egy virtuális képernyőméretet, és olvassuk ki bármely elem számított háttérszínét.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: hu
og_description: Hogyan töltsünk be HTML-t Java-ban, állítsuk be az eszköz DPI-jét,
  definiáljunk egy virtuális képernyőméretet, és olvassuk ki bármely elem kiszámított
  háttérszínét.
og_title: HTML betöltése, eszköz DPI beállítása és háttérszín kiolvasása
tags:
- Aspose.HTML
- Java
title: Hogyan töltsünk be HTML-t, állítsuk be az eszköz DPI-jét és olvassuk ki a háttérszínt
url: /hu/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

image URL, we left unchanged.

Check any shortcodes: we left unchanged.

Check any other markdown: headings, lists.

Make sure we didn't translate the placeholder {{CODE_BLOCK_X}}. Good.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan töltsünk be HTML-t, állítsuk be az eszköz DPI-ját és olvassuk ki a háttérszínt

Gondolkodtál már azon, **hogyan töltsünk be html-t** egy Java alkalmazásban, majd ellenőrizzük az oldal stílusait? Nem vagy egyedül – a fejlesztők gyakran szükségük van arra, hogy egy weboldalt képernyőn kívül rendereljenek, megszerezzék a végső CSS értékeket, és ezeket PDF konvertáláshoz, képernyőképekhez vagy akár automatizált tesztekhez használják.  

Ebben az útmutatóban pontosan ezt fogjuk végigjárni: betöltünk egy HTML fájlt, **beállítjuk az eszköz DPI-ját**, meghatározunk egy **virtuális képernyőméretet**, és végül **kiolvassuk a háttérszínt** a `<body>` elemből. A végére egy teljesen futtatható kódrészletet kapsz, amely kiírja a **kiszámított háttérszínt** – nincs rejtély, csak tiszta Java.

## Amire szükséged lesz

* Java 17 vagy újabb (a kód bármely friss JDK-val működik).  
* Aspose.HTML for Java 23.9 vagy későbbi – töltsd le a JAR-t az Aspose oldaláról, vagy add hozzá Maven‑en keresztül.  
* Egy egyszerű HTML fájl (például `responsive.html`), amely CSS‑ben meghatározott háttérszínt tartalmaz.

Ennyi – nincs extra keretrendszer, nincs böngésző‑driver. Készen állsz? Kezdjünk bele.

![Diagram, amely bemutatja a HTML betöltését és a kiszámított stílusok kinyerését](/images/load-html-diagram.png){alt="Diagram, amely bemutatja a HTML betöltését és a kiszámított stílusok kinyerését"}

## 1. lépés: HTML betöltése és a renderelési beállítások konfigurálása

Az első dolog, amit teszel, egy `HtmlLoadOptions` objektum létrehozása. Ez az objektum megmondja az Aspose.HTML‑nek, **hogyan töltse be a html‑t** – beleértve a virtuális képernyő méreteit és a kívánt DPI‑t.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Miért fontos:**  
A virtuális képernyőméret beállítása biztosítja, hogy a `@media (max-width: 600px)`‑hez hasonló média lekérdezések úgy viselkedjenek, mintha az oldal egy valódi monitoron lenne renderelve. A DPI befolyásolja, hogy a CSS `px` egységek hogyan térnek át a fizikai pixelekre – ez kulcsfontosságú, amikor később képeket vagy PDF‑eket generálsz.

## 2. lépés: HTML fájl betöltése a konfigurált beállításokkal

Most ténylegesen betöltjük a fájlt. Vedd észre, hogy ugyanazt a `loadOptions`‑t adjuk át, amelyet épp konfiguráltunk.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Ha a fájl nem található, az Aspose egy egyértelmű `FileNotFoundException`‑t dob. Éles környezetben érdemes ezt try‑catch‑ben kezelni, és egy alapértelmezett HTML karakterláncra visszaesni.

## 3. lépés: Virtuális képernyőméret és eszköz DPI beállítása (explicit módon)

Bár már meghívtuk a `setScreenSize` és a `setDeviceDpi` metódusokat fent, érdemes kiemelni, hogy a **set virtual screen size** és a **set device dpi** bármikor módosítható a renderelés előtt. Például növelheted a DPI‑t a nagy felbontású képernyőképekhez:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Ne feledd, hogy ha ezeket a beállításokat az első betöltés után módosítod, újra be kell tölteni a dokumentumot – az Aspose a `Document` létrehozása után immutábilisnak tekinti őket.

## 4. lépés: Háttérszín kiolvasása és a kiszámított háttérszín lekérése

A dokumentum memóriában van, így lekérdezheted bármely elem kiszámított stílusát. Itt a `<body>` elemre koncentrálunk, de ugyanaz a módszer működik `<div>`, `<p>` vagy akár pseudo‑elemek esetén is.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Ami megjelenik:** Ha a `responsive.html` tartalmazza a `body { background: #ff5722; }` szabályt, a konzol valami ilyesmit ír ki:

```
Computed background color: rgba(255,87,34,1)
```

Ez a **get computed background color** eredmény – az Aspose minden CSS kaszkád szabályt, média lekérdezést és még a `!important` deklarációkat is felold, mielőtt visszaadná a végső értéket.

## Teljes működő példa

Összegezve, itt a teljes, másolásra és beillesztésre kész program:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Várt kimenet

```
Computed background color: rgba(255,255,255,1)
```

*(A pontos RGBA értékek a HTML fájlod CSS‑étől függenek.)*

## Gyakori hibák és profi tippek

* **Hiányzó DPI beállítás?** Az Aspose alapértelmezés szerint 96 DPI‑t használ, ami elmosódott magas felbontású képernyőképeket eredményezhet. Mindig állítsd be explicit módon, ha éles kimenetre van szükséged.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}