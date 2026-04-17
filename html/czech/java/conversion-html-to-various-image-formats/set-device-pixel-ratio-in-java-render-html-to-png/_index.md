---
category: general
date: 2026-03-14
description: Zjistěte, jak nastavit poměr pixelů zařízení v Javě a uložit webovou
  stránku jako PNG pomocí Aspose.HTML – kompletní průvodce konverzí HTML na PNG.
draft: false
keywords:
- set device pixel ratio
- save webpage as png
- how to render png
- html to png conversion
- java html to image
language: cs
og_description: Naučte se, jak v Javě nastavit poměr pixelů zařízení a uložit webovou
  stránku jako PNG pomocí Aspose.HTML, krok za krokem popisující převod HTML na PNG.
og_title: nastavit poměr pixelů zařízení v Javě – vykreslit HTML do PNG
tags:
- java
- aspose-html
- image-rendering
title: Nastavit poměr pixelů zařízení v Javě – renderovat HTML do PNG
url: /cs/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-render-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# nastavení poměru pixelů zařízení v Javě – Renderování HTML do PNG

Už jste někdy potřebovali **set device pixel ratio** při generování snímku webové stránky v Javě? Možná vytváříte službu pro náhledy na mobilních zařízeních, nebo jen chcete ostrý miniaturu, která vypadá správně na Retina displeji. Ať už je to jakkoli, jste na správném místě. V tomto tutoriálu projdeme celý proces **html to png conversion** a ukážeme vám přesně, jak **save webpage as png** pomocí knihovny Aspose.HTML.

Probereme vše od konfigurace sandboxu, který napodobuje viewport iPhonu, po načtení vzdálené HTML stránky a nakonec zápis výsledku na disk. Na konci budete vědět, **how to render png** soubory programově, a budete mít znovupoužitelný úryvek, který můžete vložit do jakéhokoli Java projektu, který potřebuje **java html to image** funkce.

## Co budete potřebovat

- **Java Development Kit (JDK) 8 or newer** – knihovna funguje s jakýmkoli aktuálním JDK.
- **Aspose.HTML for Java** – můžete získat nejnovější JAR z Aspose Maven repozitáře nebo stáhnout zip z oficiální stránky.
- **IDE** (IntelliJ IDEA, Eclipse nebo i VS Code) – cokoliv, co vám umožní kompilovat a spouštět Javu.
- Připojení k internetu, pokud plánujete načíst živou URL (příklad používá `https://example.com/mobile.html`).

To je vše. Nepotřebujete žádné další nástroje pro sestavení ani nativní binárky.

## Krok 1: Konfigurace sandboxu a nastavení poměru pixelů zařízení

Prvním krokem je vytvořit **Sandbox**, který se tváří jako mobilní zařízení. Zde skutečně **set device pixel ratio** tak, aby odpovídal obrazovce s vysokou hustotou pixelů (například 2× retina displej iPhonu).

```java
import com.aspose.html.rendering.SandboxOptions;

// Create sandbox options
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixel width of iPhone 6/7/8
sandboxOptions.setScreenHeight(667);         // CSS pixel height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
sandboxOptions.setUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
    "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

// Build the sandbox
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

**Why this matters:** `devicePixelRatio` říká vykreslovacímu enginu, kolik fyzických pixelů odpovídá jednomu CSS pixelu. Bez jeho nastavení by váš výstupní obrázek vypadal rozmazaně na obrazovkách s vysokým DPI. Explicitním nastavením zajistíte, že vygenerovaný PNG bude mít správné množství detailů.

> **Pro tip:** Pokud cílíte na Android zařízení, můžete použít `3.0` pro zařízení s 3× škálováním. Šířku/výšku upravte odpovídajícím způsobem.

## Krok 2: Načtení HTML stránky pro html to png conversion

Jakmile je sandbox připraven, můžeme načíst stránku, kterou chceme zachytit. Třída `HTMLDocument` z Aspose.HTML přijímá URL a instanci sandboxu, takže se stránka vykreslí přesně tak, jako by byla na simulovaném zařízení.

```java
import com.aspose.html.HTMLDocument;

// Load the remote page inside the sandbox
HTMLDocument document = new HTMLDocument(
    "https://example.com/mobile.html", // Replace with your own URL
    mobileSandbox);
```

**What’s happening under the hood?** Knihovna načte HTML, parsuje CSS, spustí jakýkoli JavaScript (pokud je povolen), a rozvrhne stránku pomocí rozměrů viewportu, které jste definovali dříve. Tento krok je jádrem **java html to image** konverze, protože vám poskytuje plně vykreslený DOM připravený k rasterizaci.

> **Edge case:** Pokud stránka používá externí fonty, ujistěte se, že jsou přístupné z počítače, na kterém kód běží. Jinak se text může vrátit k výchozímu fontu, což změní vizuální výsledek.

## Krok 3: Uložení webové stránky jako PNG – jak renderovat png pomocí Aspose.HTML

Po vykreslení dokumentu je posledním krokem skutečně zapsat PNG soubor na disk. Třída `PngSaveOptions` vám umožní upravit úroveň komprese a další nastavení specifické pro PNG, ale výchozí hodnoty fungují perfektně pro většinu scénářů.

```java
import com.aspose.html.saving.PngSaveOptions;

// Define PNG options (optional)
PngSaveOptions pngOptions = new PngSaveOptions();
// You could adjust pngOptions.setCompressionLevel(9); for maximum compression

// Save the rendered page as a PNG image
document.save("output/mobile_view.png", pngOptions);

System.out.println("Mobile view rendered and saved as PNG.");
```

Když spustíte program, v adresáři `output` se objeví soubor `mobile_view.png`. Otevřete jej a měli byste vidět přesný snímek vzdálené stránky, vykreslený v rozlišení s vysokou hustotou, které jste specifikovali pomocí **set device pixel ratio**.

### Rychlé ověření

```text
$ java -jar MobileRenderTutorial.jar
Mobile view rendered and saved as PNG.
$ ls output
mobile_view.png
```

Otevřete obrázek v libovolném prohlížeči; text by měl být ostrý, ikony jasné a rozvržení identické s tím, co byste viděli na skutečném iPhonu.

## Volitelné: Úprava renderovacího pipeline

### Dynamická změna DPI

Pokud potřebujete generovat obrázky pro různé hustoty obrazovek, zabalte vytvoření sandboxu do metody:

```java
private static Sandbox createSandbox(double dpr) {
    SandboxOptions opts = new SandboxOptions();
    opts.setScreenWidth(375);
    opts.setScreenHeight(667);
    opts.setDevicePixelRatio(dpr); // Pass 1.0, 2.0, 3.0, etc.
    opts.setUserAgent("...");
    return new Sandbox(opts);
}
```

Pak zavolejte `createSandbox(3.0)` pro zařízení s 3×. Tato flexibilita je užitečná, když budujete službu, která najednou vrací miniatury pro iPhone, iPad a Android tablety.

### Renderování bez JavaScriptu

Pokud stránka, kterou zachytáváte, obsahuje těžké skripty, které nepotřebujete, můžete JavaScript vypnout pro rychlejší **html to png conversion**:

```java
sandboxOptions.setJavaScriptEnabled(false);
```

Vypnutí skriptů může zkrátit dobu renderování na polovinu, ale buďte si vědomi, že některý dynamický obsah může zmizet.

## Časté úskalí a jak se jim vyhnout

| Problém | Proč se to děje | Řešení |
|-------|----------------|-----|
| **Rozmazaný výstup** | `devicePixelRatio` left at default (1.0) | Explicitly **set device pixel ratio** to 2.0 or higher |
| **Chybějící fonty** | Remote fonts blocked by firewall | Ensure the machine has internet access or embed fonts locally |
| **Chyby nedostatku paměti** | Rendering very large pages at high DPI | Limit the viewport size or lower the `devicePixelRatio` |
| **Nesprávná URL** | Using a relative path without a base URL | Provide a full absolute URL or set `document.setBaseUrl()` |

Řešení těchto problémů již na začátku vám ušetří frustrující ladící sezení později.

## Kompletní funkční příklad

Níže je kompletní, připravený Java program. Zkopírujte jej do souboru pojmenovaného `MobileRenderTutorial.java`, přidejte Aspose.HTML JAR do classpath a spusťte.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.SandboxOptions;
import com.aspose.html.saving.PngSaveOptions;

public class MobileRenderTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that mimics a mobile device viewport
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixel width
        sandboxOptions.setScreenHeight(667);         // CSS pixel height
        sandboxOptions.setDevicePixelRatio(2.0);     // High‑density screen (set device pixel ratio)
        sandboxOptions.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1");

        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // Step 2: Load the HTML page inside the sandbox
        HTMLDocument document = new HTMLDocument(
            "https://example.com/mobile.html", // Replace with your own URL
            mobileSandbox);

        // Step 3: Render the page to a PNG image
        PngSaveOptions pngOptions = new PngSaveOptions();
        document.save("output/mobile_view.png", pngOptions);

        System.out.println("Mobile view rendered.");
    }
}
```

> **Result:** Program vytvoří `output/mobile_view.png`, snímek ve vysokém rozlišení, který respektuje **set device pixel ratio**, který jste definovali.

## Vizuální potvrzení

<img src="output/mobile_view.png" alt="set device pixel ratio example screenshot" width="400"/>

Obrázek výše (placeholder) ukazuje finální PNG po renderovacím procesu. Všimněte si ostrého textu a správně škálovaných UI prvků – přesně to, co očekáváte, když **set device pixel ratio** správně.

## Závěr

Nyní máte pevné pochopení, jak **set device pixel ratio** v Javě, provést **html to png conversion** a **save webpage as png** pomocí Aspose.HTML. Toto pokrývá základní workflow “jak renderovat png” a poskytuje vám znovupoužitelný vzor pro jakýkoli úkol **java html to image**, na který můžete narazit.

Jste připraveni na další krok? Zkuste vyměnit URL za dynamickou stránku, experimentujte s různými hodnotami `devicePixelRatio`, nebo integrujte tento úryvek do Spring Boot endpointu, který vrací PNG na požádání. Možnosti jsou neomezené a s pevnými základy vám rozšíření tohoto řešení půjde jako po másle.

Šťastné kódování a neváhejte zanechat komentář

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}