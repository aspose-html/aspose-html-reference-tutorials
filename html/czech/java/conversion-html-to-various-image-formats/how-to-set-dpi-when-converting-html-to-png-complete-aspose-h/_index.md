---
category: general
date: 2026-06-29
description: Naučte se, jak nastavit DPI a rozlišení obrázku při převodu HTML na PNG
  pomocí Aspose HTML Converter. Krok‑za‑krokem je zahrnut Java příklad.
draft: false
keywords:
- how to set dpi
- convert html to png
- set image resolution
- convert html page
- aspose html converter
language: cs
og_description: Jak nastavit DPI při konverzi HTML pomocí Aspose. Tento průvodce vám
  ukáže, jak převést HTML stránku na vysoce rozlišený PNG obrázek v Javě.
og_title: Jak nastavit DPI při převodu HTML na PNG – Tutoriál Aspose HTML
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  headline: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  type: TechArticle
- description: Learn how to set DPI and image resolution while converting HTML to
    PNG with Aspose HTML Converter. Step‑by‑step Java example included.
  name: How to Set DPI When Converting HTML to PNG – Complete Aspose HTML Guide
  steps:
  - name: 1. Different Output Formats
    text: Aspose.HTML isn’t limited to PNG. Swap the file extension and use a matching
      options class, e.g., `JpegConversionOptions` for JPEGs. The DPI logic stays
      identical.
  - name: 2. Dynamically Determining Screen Size
    text: 'If you need the sandbox to mimic a mobile device, read the dimensions from
      a config file:'
  - name: 3. Batch Conversion
    text: Wrap the conversion call inside a loop that iterates over a directory of
      HTML files. Remember to reuse the same `Sandbox` and `ImageConversionOptions`
      objects to avoid unnecessary allocations.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Image Processing
title: Jak nastavit DPI při převodu HTML na PNG – Kompletní průvodce Aspose HTML
url: /cs/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png-complete-aspose-h/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit DPI při převodu HTML na PNG – Kompletní průvodce Aspose HTML

Už jste se někdy zamýšleli **jak nastavit DPI** pro PNG, které generujete z HTML stránky? V mnoha scénářích reportování nebo automatizace snímků obrazovky není výchozí 96 dpi dostatečně ostré. Dobrou zprávou je, že Aspose.HTML pro Java vám dává plnou kontrolu nad simulací obrazovky a rozlišením obrázku, takže můžete DPI zvýšit na 300 nebo dokonce 600 pomocí několika řádků kódu.

V tomto tutoriálu projdeme reálný příklad v Javě, který **převádí HTML stránku na PNG** a zároveň **nastavuje DPI** a **rozlišení obrázku**. Na konci budete mít připravenou třídu, pochopíte, proč každé nastavení má význam, a budete vědět, jak jej upravit pro různé případy použití, jako jsou vysoce rozlišené výtisky nebo webové miniatury.

> **Rychlý přehled:** Hlavní kroky jsou (1) vytvořit `Sandbox`, který napodobuje obrazovku, (2) nastavit její DPI, (3) nakonfigurovat `ImageConversionOptions` s požadovaným rozlišením a (4) zavolat `Converter.convert`. Žádné externí nástroje, žádné příkazy v terminálu — pouze čistá Java.

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

- **Java 17** (nebo jakýkoli novější JDK) nainstalovanou a nastavenou ve vašem IDE.
- **Aspose.HTML pro Java** knihovnu (Maven artefakt `com.aspose:aspose-html`). Nejnovější verzi můžete získat z [Aspose Maven repository](https://repo.aspose.com/repo) nebo si stáhnout JAR přímo.
- Jednoduchý HTML soubor (`page.html`), který chcete převést na PNG. Umístěte jej na dostupné místo, např. `C:/temp/page.html`.
- Základní znalost práce s výjimkami v Javě — nic složitého.

Pokud vám některá z těchto položek není známá, zastavte se na okamžik a nainstalujte chybějící součást. Zbytek průvodce předpokládá, že jste zvyklí otevírat Java projekt a přidávat externí JAR soubory.

## Krok 1: Nastavte Maven projekt (nebo přidejte JAR ručně)

Pokud používáte Maven, přidejte závislost do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.11</version> <!-- Check for the newest version -->
</dependency>
```

Jinak vložte `aspose-html-*.jar` do složky `libs` vašeho projektu a přidejte jej do build path. Tento krok se přímo netýká **jak nastavit DPI**, ale bez knihovny nemůžete použít třídu `Sandbox`, která umožňuje kontrolu DPI.

## Krok 2: Vytvořte Sandbox, který simuluje skutečnou obrazovku

*Sandbox* je způsob, jakým Aspose reprodukuje prostředí prohlížeče. Představte si jej jako virtuální monitor, kde určujete šířku, výšku a hlavně **DPI**. Níže je úryvek kódu, který vytváří obrazovku 1024 × 768 při 96 dpi — pouze výchozí hodnota před zvýšením rozlišení:

```java
// Step 2.1: Initialise the sandbox
Sandbox sandbox = new Sandbox();

// Step 2.2: Define virtual screen dimensions (pixels)
sandbox.setScreenWidth(1024);
sandbox.setScreenHeight(768);

// Step 2.3: Set the DPI – this is the key to controlling image sharpness
sandbox.setDpi(96); // Change this value to 300, 600, etc., later
```

> **Proč sandbox?** Bez něj by Aspose padl zpět na nastavení obrazovky hostitelského počítače, což vede k nekonzistentním výsledkům na různých vývojových strojích. Uzamčením DPI zajistíte, že každá konverze vypadá stejně, ať už ji spustíte na notebooku nebo na CI serveru.

## Krok 3: Nakonfigurujte možnosti konverze obrázku – nastavte rozlišení obrázku

Nyní, když je sandbox připraven, řekneme konvertoru, jaké **rozlišení obrázku** chceme. Třída `ImageConversionOptions` vám umožňuje nastavit DPI výstupního PNG nezávisle na DPI sandboxu, takže máte dvě páky, se kterými můžete pracovat.

```java
// Step 3.1: Prepare conversion options
ImageConversionOptions conversionOptions = new ImageConversionOptions();

// Step 3.2: Desired output DPI – this directly influences PNG quality
conversionOptions.setResolution(300); // 300 dpi is print‑quality; increase for sharper prints

// Step 3.3: Bind the sandbox to the options so the layout engine respects our virtual screen
conversionOptions.setSandbox(sandbox);
```

**Tip:** Pokud chcete PNG s 600 dpi pro vysoce kvalitní brožury, jednoduše změňte `setResolution(300)` na `setResolution(600)`. Mějte na paměti, že vyšší hodnoty DPI zvyšují spotřebu paměti a dobu zpracování, proto nejprve otestujte na malé stránce.

## Krok 4: Převod HTML stránky na PNG

S nastaveným sandboxem a volbami je samotný **convert html to png** krok jedním řádkem:

```java
// Step 4: Perform the conversion
Converter.convert(
        "C:/temp/page.html",   // Source HTML file (convert html page)
        "C:/temp/page.png",    // Destination PNG file
        conversionOptions);    // Options that include DPI and sandbox
```

Pokud vše proběhne hladce, uvidíte zprávu v konzoli z následujícího kroku.

## Krok 5: Ověřte výsledek a vypište potvrzení

Rychlé `System.out.println` vám řekne, že úloha je dokončena. V reálném projektu možná budete chtít zkontrolovat velikost souboru, rozměry nebo dokonce programově otevřít PNG a ověřit DPI.

```java
System.out.println("PNG generated with sandboxed layout at 300 dpi.");
```

Spuštěním třídy by se měl vytvořit soubor `page.png` ve stejné složce jako váš HTML soubor. Otevřete jej v prohlížeči obrázků, který zobrazuje DPI (např. Windows Photo Viewer → Properties → Details) a ověřte, že je nastaveno **300 dpi**.

## Kompletní funkční příklad

Sestavením všeho dohromady získáte samostatnou Java třídu, kterou můžete zkopírovat a vložit do svého IDE:

```java
import com.aspose.html.conversions.Converter;
import com.aspose.html.conversions.options.ImageConversionOptions;
import com.aspose.html.sandbox.Sandbox;

public class HtmlToPngWithSandbox {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox that simulates a 1024×768 screen with 96 dpi.
        Sandbox sandbox = new Sandbox();
        sandbox.setScreenWidth(1024);
        sandbox.setScreenHeight(768);
        sandbox.setDpi(96); // <-- This is where you learn how to set dpi

        // Step 2: Configure image conversion options – 300 dpi PNG using the sandbox.
        ImageConversionOptions conversionOptions = new ImageConversionOptions();
        conversionOptions.setResolution(300); // Set image resolution (dpi)
        conversionOptions.setSandbox(sandbox);

        // Step 3: Convert the HTML page to a PNG image using the defined options.
        Converter.convert(
                "C:/temp/page.html",   // convert html page
                "C:/temp/page.png",    // output PNG
                conversionOptions);    // includes dpi and resolution settings

        // Step 4: Indicate that the conversion has completed.
        System.out.println("PNG generated with sandboxed layout at 300 dpi.");
    }
}
```

> **Pamatujte:** Řádek `sandbox.setDpi(96);` je částí **jak nastavit DPI**. Upravit jej podle požadované hustoty obrazovky; `conversionOptions.setResolution(300);` řídí DPI finálního obrázku.

## Řešení běžných problémů

| Situace | Na co si dát pozor | Navrhované řešení |
|-----------|-------------------|-------------------|
| **Out‑of‑Memory errors** při použití 600 dpi | Vysoké DPI dramaticky zvyšuje raster (např. 1024 × 768 @ 600 dpi ≈ 4 MP). | Snižte rozměry obrazovky nebo provádějte konverzi po částech pomocí `ConversionProgress` callbacků. |
| **HTML používá externí CSS/JS, který se nenačítá** | Sandbox běží izolovaně; vzdálené zdroje musí být dostupné. | Použijte absolutní URL nebo vložte CSS přímo do HTML. |
| **Nesprávné DPI ve výstupu** | Změnili jste `sandbox.setDpi`, ale zapomněli upravit `conversionOptions.setResolution`. | Ujistěte se, že obě hodnoty odpovídají vašemu cílovému výstupu. |
| **FileNotFoundException** | Špatná cesta nebo chybějící oprávnění k souboru. | Použijte `Paths.get(...).toAbsolutePath()` a ověřte práva čtení/zápisu. |

## Pokročilé varianty

### 1. Různé výstupní formáty

Aspose.HTML není omezen na PNG. Změňte příponu souboru a použijte odpovídající třídu možností, např. `JpegConversionOptions` pro JPEG. Logika DPI zůstává stejná.

```java
import com.aspose.html.conversions.options.JpegConversionOptions;

// ...

JpegConversionOptions jpegOpts = new JpegConversionOptions();
jpegOpts.setResolution(300);
jpegOpts.setSandbox(sandbox);

Converter.convert("page.html", "page.jpg", jpegOpts);
```

### 2. Dynamické určení velikosti obrazovky

Pokud potřebujete, aby sandbox napodoboval mobilní zařízení, načtěte rozměry z konfiguračního souboru:

```java
sandbox.setScreenWidth(Integer.parseInt(System.getProperty("screen.width", "375")));
sandbox.setScreenHeight(Integer.parseInt(System.getProperty("screen.height", "667")));
sandbox.setDpi(Integer.parseInt(System.getProperty("screen.dpi", "96")));
```

Spusťte s `-Dscreen.width=375 -Dscreen.height=667 -Dscreen.dpi=326`, abyste emulovali iPhone Retina displej.

### 3. Hromadná konverze

Zabalte volání konverze do smyčky, která prochází adresář s HTML soubory. Pamatujte na opětovné použití stejných objektů `Sandbox` a `ImageConversionOptions`, abyste se vyhnuli zbytečným alokacím.

```java
Files.list(Paths.get("C:/temp/html"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(htmlPath -> {
         String pngPath = htmlPath.toString().replace(".html", ".png");
         Converter.convert(htmlPath.toString(), pngPath, conversionOptions);
     });
```

## Očekávaný výstup

Spuštěním třídy s výchozím nastavením získáte PNG soubor o rozměrech přibližně **1024 × 768 pixelů** při **300 dpi**. Ve většině editorů obrázků se rozměry zobrazí jako 1024 × 768, zatímco metadata DPI ukazují 300. Pokud obrázek vytisknete na šířku 1 palec, získáte ostrou čáru o 300 pixelech — ideální pro vysoce kvalitní letáky.

## Vizualizace

![how to set dpi in Aspose HTML conversion](/images/aspose-dpi-example.png "how to set dpi – Aspose HTML sandbox example")

*Screenshot ukazuje metadata DPI vygenerovaného PNG (300 dpi).*

## Závěr

Probrali jsme **jak nastavit DPI** při **konverzi HTML na PNG** pomocí **Aspose HTML Converter** v Javě. Vytvořením sandboxu, nastavením `ImageConversionOptions` a voláním `Converter.convert` získáte pixel‑perfektní kontrolu nad simulací obrazovky i konečným rozlišením obrázku. Ať už generujete tisknutelné faktury, vysoce rozlišená webová aktiva nebo automatizované miniatury, stejný vzor platí — stačí upravit DPI a velikost obrazovky podle potřeby.

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, abyste si osvojili další funkce API a prozkoumali alternativní implementační přístupy ve svých projektech.

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Convert HTML to JPEG Using Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)
- [How to Convert HTML to BMP with Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-bmp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}