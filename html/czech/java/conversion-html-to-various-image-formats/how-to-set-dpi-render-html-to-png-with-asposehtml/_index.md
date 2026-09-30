---
category: general
date: 2026-01-14
description: jak nastavit DPI při převodu URL na PNG. Naučte se renderovat HTML do
  PNG, nastavit velikost viewportu a uložit HTML jako PNG pomocí Aspose.HTML v Javě.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: cs
og_description: Jak nastavit DPI při převodu URL na PNG. Krok za krokem návod, jak
  renderovat HTML do PNG, ovládat velikost viewportu a uložit HTML jako PNG pomocí
  Aspose.HTML.
og_title: jak nastavit dpi – Vykreslit HTML do PNG pomocí AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: jak nastavit DPI – renderovat HTML do PNG pomocí AsposeHTML
url: /cs/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak nastavit dpi – Render HTML do PNG s AsposeHTML

Už jste se někdy zamysleli **nad tím, jak nastavit dpi** pro obrázek podobný snímku obrazovky generovaný z webové stránky? Možná potřebujete PNG s 300 DPI pro tisk, nebo nízké rozlišení miniatury pro mobilní aplikaci. V obou případech je trik v tom, že řeknete vykreslovacímu enginu, jaké logické DPI chcete, a nechte ho udělat těžkou práci.  

V tomto tutoriálu vezmeme živou URL, vykreslíme ji do souboru PNG, **nastavíme velikost viewportu**, upravíme DPI a nakonec **uložíme HTML jako PNG**—vše pomocí Aspose.HTML pro Java. Žádné externí prohlížeče, žádné nešikovné nástroje z příkazové řádky—pouze čistý Java kód, který můžete vložit do libovolného Maven nebo Gradle projektu.

> **Pro tip:** Pokud potřebujete jen rychlou miniaturu, můžete nechat DPI na 96 DPI (výchozí pro většinu obrazovek). Pro tiskové soubory zvyšte na 300 DPI nebo více.

![příklad nastavení dpi](https://example.com/images/how-to-set-dpi.png "příklad nastavení dpi")

## Co budete potřebovat

- **Java 17** (nebo jakýkoli novější JDK).  
- **Aspose.HTML for Java** 24.10 nebo novější. Můžete jej získat z Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Internetové připojení pro stažení cílové stránky (příklad používá `https://example.com/sample.html`).  
- Oprávnění k zápisu do výstupního adresáře.

A to je vše—žádný Selenium, žádný headless Chrome. Aspose.HTML provádí vykreslování v‑procesu, což znamená, že zůstáváte uvnitř JVM a vyhnete se režii spouštění prohlížeče.

## Krok 1 – Načtení HTML dokumentu z URL

Nejprve vytvoříme instanci `HTMLDocument`, která ukazuje na stránku, kterou chceme zachytit. Konstruktor automaticky stáhne HTML, parsuje jej a připraví DOM.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Proč je to důležité:* Načtením dokumentu přímo vynecháte potřebu samostatného HTTP klienta. Aspose.HTML respektuje přesměrování, cookies a dokonce i základní autentifikaci, pokud vložíte přihlašovací údaje do URL.

## Krok 2 – Vytvoření sandboxu s požadovaným DPI a viewportem

**Sandbox** je způsob, jakým Aspose.HTML napodobuje prostředí prohlížeče. Zde mu říkáme, aby se tvářil jako obrazovka 1280 × 720 a, co je klíčové, nastavíme **DPI zařízení**. Změna DPI mění hustotu pixelů vykresleného obrázku, aniž by změnila logickou velikost.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Proč byste mohli tyto hodnoty upravit:*  
- **Velikost viewportu** řídí, jak se chovají CSS media queries (`@media (max-width: …)`).  
- **DPI zařízení** ovlivňuje fyzickou velikost obrázku při tisku. Obrázek s 96 DPI vypadá dobře na obrazovkách; obrázek s 300 DPI si zachovává ostrost na papíře.  

Pokud potřebujete čtvercovou miniaturu, jednoduše změňte `setViewportSize(500, 500)` a nechte DPI nízké.

## Krok 3 – Výběr PNG jako výstupního formátu

Aspose.HTML podporuje několik rastrových formátů (PNG, JPEG, BMP, GIF). PNG je bezztrátový, což ho činí ideálním pro snímky obrazovky, kde chcete zachovat každý pixel.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Můžete také upravit úroveň komprese (`pngOptions.setCompressionLevel(9)`), pokud vás zajímá velikost souboru.

## Krok 4 – Vykreslení a uložení obrázku

Nyní řekneme dokumentu, aby se **uložil** jako obrázek. Metoda `save` přijímá cestu k souboru a dříve nakonfigurované možnosti.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Po dokončení programu najdete soubor PNG v `YOUR_DIRECTORY/sandboxed.png`. Otevřete jej—pokud jste nastavili DPI na 300, metadata obrázku to odrazí, i když rozměry pixelů zůstávají 1280 × 720.

## Krok 5 – Ověření DPI (volitelné, ale užitečné)

Pokud chcete dvojitě zkontrolovat, že DPI bylo skutečně použito, můžete přečíst metadata PNG pomocí lehké knihovny jako **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Měli byste vidět `300` (nebo jakoukoliv hodnotu, kterou jste nastavili) vytištěnou do konzole. Tento krok není pro vykreslování vyžadován, ale je to rychlá kontrola, zejména když generujete soubory pro tiskový workflow.

## Časté otázky a okrajové případy

### „Co když stránka používá JavaScript k načtení obsahu?“

Aspose.HTML spouští **omezenou podmnožinu** JavaScriptu. Pro většinu statických stránek funguje ihned. Pokud stránka silně závisí na klientských frameworkech (React, Angular, Vue), možná budete muset stránku předem vykreslit nebo místo toho použít headless prohlížeč. Nastavení DPI však funguje stejně, jakmile je DOM připraven.

### „Mohu místo PNG vykreslit PDF?“

Určitě. Vyměňte `ImageSaveOptions` za `PdfSaveOptions` a změňte výstupní příponu na `.pdf`. Nastavení DPI stále ovlivňuje rastrový vzhled všech vložených obrázků.

### „Co vysoké rozlišení snímků pro retina displeje?“

Jednoduše zdvojnásobte rozměry viewportu při zachování DPI na 96 DPI, nebo ponechte viewport a zvýšte DPI na 192. Výsledný PNG bude obsahovat dvakrát více pixelů, což vám poskytne ostrý retina vzhled.

### „Musím uvolňovat prostředky?“

`HTMLDocument` implements `AutoCloseable`. In a production app, wrap it in a try‑with‑resources block:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

To zajistí, že nativní prostředky budou uvolněny okamžitě.

## Kompletní funkční příklad (připravený ke kopírování)

Níže je kompletní program připravený ke spuštění. Nahraďte `YOUR_DIRECTORY` skutečným adresářem na vašem počítači.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Spusťte třídu a získáte PNG, který respektuje nastavení **jak nastavit dpi**, které jste zadali.

## Závěr

Prošli jsme **jak nastavit dpi** při **vykreslování HTML do PNG**, pokryli krok **nastavení velikosti viewportu** a ukázali vám, jak **uložit HTML jako PNG** pomocí Aspose.HTML pro Java. Hlavní body jsou:

- Použijte **sandbox** k řízení DPI a viewportu.  
- Vyberte správné **ImageSaveOptions** pro bezztrátový výstup.  
- Ověřte metadata DPI, pokud potřebujete zajistit kvalitu tisku.

Odtud můžete experimentovat s různými hodnotami DPI, většími viewporty nebo dokonce hromadně zpracovávat seznam URL. Chcete převést celý web na PNG miniatury? Stačí projít pole URL a znovu použít stejnou konfiguraci sandboxu.

Šťastné vykreslování a ať jsou vaše snímky obrazovky vždy pixel‑dokonalé!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}