---
category: general
date: 2026-02-16
description: Jak načíst HTML v Javě, nastavit DPI zařízení, definovat virtuální velikost
  obrazovky a přečíst vypočtenou barvu pozadí libovolného prvku.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: cs
og_description: Jak načíst HTML v Javě, nastavit DPI zařízení, definovat virtuální
  velikost obrazovky a přečíst vypočtenou barvu pozadí libovolného prvku.
og_title: Jak načíst HTML, nastavit DPI zařízení a přečíst barvu pozadí
tags:
- Aspose.HTML
- Java
title: Jak načíst HTML, nastavit DPI zařízení a přečíst barvu pozadí
url: /cs/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak načíst HTML, nastavit DPI zařízení a přečíst barvu pozadí

Už jste se někdy zamýšleli **jak načíst html** v Java aplikaci a poté prozkoumat styly stránky? Nejste v tom sami — vývojáři často potřebují vykreslit webovou stránku mimo obrazovku, získat finální hodnoty CSS a použít je pro konverzi do PDF, snímky obrazovky nebo dokonce automatizované testy.  

V tomto průvodci projdeme přesně to: načteme soubor HTML, **nastavíme DPI zařízení**, definujeme **virtuální velikost obrazovky** a nakonec **přečteme barvu pozadí** z elementu `<body>`. Na konci budete mít plně spustitelný úryvek, který vytiskne **vypočtenou barvu pozadí** — žádná magie, jen čistá Java.

## Co budete potřebovat

Než se pustíme dál, ujistěte se, že máte:

* Java 17 nebo novější (kód funguje s libovolnou aktuální JDK).  
* Aspose.HTML pro Java 23.9 nebo novější — stáhněte JAR z webu Aspose nebo jej přidejte přes Maven.  
* Jednoduchý HTML soubor (např. `responsive.html`), který v CSS definuje barvu pozadí.

To je vše — žádné další frameworky, žádné ovladače prohlížeče. Připravení? Pojďme na to.

![Diagram illustrating how to load html and extract computed styles](/images/load-html-diagram.png){alt="Diagram ukazující, jak načíst html a získat vypočtené styly"}

## Krok 1: Jak načíst HTML a nakonfigurovat možnosti vykreslování

První věc, kterou uděláte, je vytvořit objekt `HtmlLoadOptions`. Tento objekt říká Aspose.HTML **jak načíst html** — včetně rozměrů virtuální obrazovky a DPI, které chcete emulovat.

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

**Proč je to důležité:**  
Nastavení virtuální velikosti obrazovky zajišťuje, že media queries jako `@media (max-width: 600px)` se chovají, jako by stránka byla vykreslena na skutečném monitoru. DPI ovlivňuje, jak jsou jednotky CSS `px` mapovány na fyzické pixely — klíčové, když později generujete obrázky nebo PDF.

## Krok 2: Načtení HTML souboru pomocí nakonfigurovaných možností

Nyní skutečně načteme soubor. Všimněte si, že předáváme stejný `loadOptions`, který jsme právě nastavili.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Pokud soubor není nalezen, Aspose vyhodí jasnou `FileNotFoundException`. V produkci můžete tento kód obalit do try‑catch a přejít na výchozí HTML řetězec.

## Krok 3: Nastavení virtuální velikosti obrazovky a DPI zařízení (explicitně)

I když jsme výše již zavolali `setScreenSize` a `setDeviceDpi`, stojí za to zdůraznit, že **set virtual screen size** a **set device dpi** lze upravit kdykoli před vykreslením. Například můžete zvýšit DPI pro vysoce rozlišené snímky obrazovky:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Nezapomeňte znovu načíst dokument, pokud tato nastavení změníte po prvním načtení — Aspose je po vytvoření `Document` považuje za neměnné.

## Krok 4: Přečtení barvy pozadí a získání vypočtené barvy pozadí

S dokumentem v paměti můžete dotazovat vypočtený styl libovolného elementu. Zde se zaměřujeme na tag `<body>`, ale stejný postup funguje i pro `<div>`, `<p>` nebo dokonce pseudo‑elementy.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Co uvidíte:** Pokud `responsive.html` obsahuje `body { background: #ff5722; }`, konzole vytiskne něco jako:

```
Computed background color: rgba(255,87,34,1)
```

To je výsledek **get computed background color** — Aspose vyřeší všechny cascade pravidla CSS, media queries a dokonce deklarace `!important`, než vrátí finální hodnotu.

## Kompletní funkční příklad

Spojením všech částí získáte kompletní, připravený program ke zkopírování:

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

### Očekávaný výstup

```
Computed background color: rgba(255,255,255,1)
```

*(Přesné hodnoty RGBA závisí na CSS ve vašem HTML souboru.)*

## Časté úskalí a tipy profesionálů

* **Chybí nastavení DPI?** Aspose ve výchozím nastavení používá 96 DPI, což může rozmazat snímky ve vysokém rozlišení. Vždy jej nastavte explicitně, pokud potřebujete ostrý výstup.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}