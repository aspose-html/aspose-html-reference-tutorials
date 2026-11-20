---
category: general
date: 2026-05-31
description: Zakázat externí obrázky při převodu webové stránky na PNG v Javě pomocí
  Aspose HTML. Naučte se bezpečně načíst webovou stránku v sandboxu a uložit HTML
  dokument jako PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: cs
og_description: Zakázat externí obrázky při renderování webové stránky do PNG v Javě.
  Tento krok‑za‑krokem návod ukazuje, jak načíst webovou stránku v sandboxu a uložit
  HTML dokument jako PNG.
og_title: Zakázat externí obrázky při renderování webové stránky do PNG v Javě
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Zakázat externí obrázky při renderování webové stránky do PNG v Javě
url: /cs/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zakázat externí obrázky při renderování webové stránky do PNG v Javě

Už jste někdy potřebovali **zakázat externí obrázky**, když renderujete webovou stránku do PNG v Javě? Možná budujete službu pro miniatury, která musí zůstat izolovaná od veřejného internetu, nebo prostě chcete mít jistotu, že během konverze neuniknou žádné obrázky třetích stran. V každém případě jste na správném místě.

V tomto tutoriálu vás provedeme načtením webové stránky v sandboxu, vypnutím načítání externích obrázků a nakonec uložením HTML dokumentu jako PNG souboru — vše pomocí Aspose.HTML pro Java. Na konci budete mít připravený příklad, plus několik praktických tipů, jak se vyhnout běžným úskalím.

## Co se naučíte

- **Jak renderovat HTML do obrázku v Javě** pomocí `Converter` z Aspose.HTML.
- Přesné kroky k **načtení webové stránky v sandboxu** s vlastním viewportem a DPI.
- Konfiguraci potřebnou k **zakázání externích obrázků** při zachování renderování stránky.
- Jak **uložit HTML dokument jako PNG** (nebo jakýkoli jiný podporovaný formát) na disk.
- Řešení okrajových případů, tipy na výkon a rady pro odstraňování problémů.

### Požadavky

- Java 8 nebo novější (kód funguje i s JDK 11+).
- Maven nebo Gradle pro stažení knihovny Aspose.HTML pro Java.
- Základní znalost syntaxe Javy a práce s výjimkami.
- Připojení k internetu pro počáteční načtení stránky (pokud HTML neobsluhujete lokálně).

> **Pro tip:** Pokud pracujete za firemním proxy, nastavte před spuštěním příkladu JVM vlastnosti `http.proxyHost` a `http.proxyPort`.

---

## Krok 1: Nastavte projekt a přidejte Aspose.HTML

Nejprve přidejte závislost Aspose.HTML. Pokud používáte Maven, vložte následující do souboru `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Pro Gradle je ekvivalentní zápis:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Jakmile je knihovna na classpath, můžete začít kódovat.

---

## Krok 2: **Zakázat externí obrázky** pomocí sandboxu

Jádrem řešení je `DocumentSandbox`. Předáním hodnoty `false` pro parametr *allowExternalImages* říkáme Aspose.HTML, aby ignoroval všechny `<img>` tagy odkazující na URL mimo sandbox. Toto je přesný mechanismus, který **zakazuje externí obrázky**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Proč je to důležité:** Bez sandboxu by renderer zkoušel stáhnout každý obrázek, na který stránka odkazuje, což může být pomalé, nespolehlivé nebo dokonce bezpečnostní riziko. Nastavením příznaku na `false` zajistíte čistý, samostatný renderovací průchod.

---

## Krok 3: **Načíst webovou stránku v sandboxu**  

Nyní nasměrujeme Aspose.HTML na URL, kterou chceme zachytit. Konstruktor `HTMLDocument` přijímá instanci sandboxu a automaticky aplikuje omezení, která jsme právě definovali.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Pokud stránka silně spoléhá na externí skripty pro rozvržení, můžete si všimnout chybějícího obsahu, protože jsme také zakázali skripty. V takovém případě přepněte příznak `allowExternalScripts` na `true`, přičemž `allowExternalImages` ponechte na `false`.

---

## Krok 4: **Renderovat webovou stránku do PNG**  

Po načtení dokumentu je konverze do obrázku jednorázová pomocí `Converter.convert`. Objekt `ImageSaveOptions` vám umožní zvolit výstupní formát; zde používáme PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Výsledný soubor `sandboxed.png` obsahuje snímek stránky **bez jakýchkoli externích obrázků** — zůstávají jen vložené SVG nebo grafika zakódovaná v base64, pokud nějaká je.

---

## Krok 5: Ověřte výstup a odstraňujte běžné problémy

Po spuštění programu otevřete `sandboxed.png` v libovolném prohlížeči obrázků. Měli byste vidět rozvržení stránky, text a CSS styly, ale všechny elementy `<img src="http://…">` budou prázdné (často vykreslené jako bílý obdélník nebo úplně vynechané).

### Typické problémy a jejich řešení

| Problém | Pravděpodobná příčina | Řešení |
|---|---|---|
| Prázdná stránka | Cílová URL blokovala požadavek (např. Cloudflare) | Přidejte správné hlavičky do sandboxu user‑agent nebo použijte proxy. |
| Chybějící fonty | Fontové soubory jsou hostovány externě | Nainstalujte fonty lokálně nebo je vložte jako `@font-face` s data URI. |
| Posun rozvržení | CSS odkazuje na externí styly, které byly zablokovány | Nastavte `allowExternalScripts` na `true` *pouze* pro načítání CSS, pak spusťte znovu. |
| `java.lang.OutOfMemoryError` | Renderování velmi velké stránky při vysokém DPI | Zmenšete velikost viewportu nebo DPI, nebo zvýšte heap JVM (`-Xmx2g`). |

---

## Krok 6: Rozšíření příkladu — uložit do jiných formátů

Stejný kód funguje pro JPEG, BMP nebo i PDF. Stačí změnit výčtový typ `SaveFormat`:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Pokud potřebujete PDF, nahraďte `ImageSaveOptions` za `PdfSaveOptions` a upravte příponu souboru odpovídajícím způsobem.

---

## Kompletní funkční příklad (připravený ke zkopírování)

Níže je **úplný, spustitelný program**. Vytvořte novou třídu v Javě, vložte kód, ujistěte se, že adresář `output` existuje, a spusťte jej.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Očekávaný výstup** (konzole):

```
PNG image saved to: output/sandboxed.png
```

Otevřete `sandboxed.png` — uvidíte stránku renderovanou **bez externích obrázků**.

---

## Často kladené otázky

**Q: Můžu stále zobrazovat obrázky, které jsou součástí HTML?**  
A: Ano. Inline `data:` URI nebo base64‑zakódované obrázky jsou považovány za součást dokumentu a objeví se v PNG.

**Q: Co když potřebuji ponechat některé externí obrázky a jiné blokovat?**  
A: Sandbox funguje jako přepínač vše‑nebo‑nic. Pro jemnější kontrolu si povolené obrázky stáhněte sami, vložte je jako data URI a pak renderujte.

**Q: Funguje tento přístup na headless serverech?**  
A: Rozhodně. Aspose.HTML je čistě Java knihovna; nevyžaduje zobrazovací server ani prohlížečový engine.

**Q: Jak se liší od použití Selenium nebo Puppeteer?**  
A: Selenium ovládá skutečný prohlížeč, což je těžkopádné a obtížně sandboxovatelné. Aspose.HTML renderuje HTML přímo v paměti, poskytuje deterministický výkon a jednodušší bezpečnostní kontroly jako **zakázat externí obrázky**.

---

## Závěr

Nyní máte solidní, end‑to‑end recept na **zakázání externích obrázků při renderování webové stránky do PNG v Javě**. Využitím `DocumentSandbox` získáte přísnou kontrolu nad tím, jaké externí zdroje jsou povoleny, což zajišťuje jak bezpečnost, tak reprodukovatelnost. Odtud můžete experimentovat s různými velikostmi viewportu, nastavením DPI nebo výstupními formáty — každá úprava otevírá nové možnosti pro generování miniatur, náhledů nebo archivních snímků.

Jste připraveni na další výzvu? Zkuste renderovat dávku URL paralelně, nebo integrovat tuto logiku do Spring Boot microservice, která na požádání vrací PNG. Možnosti jsou neomezené, když spojíte flexibilitu Aspose.HTML s konkurenčními nástroji Javy.

Šťastné kódování a nezapomeňte sdílet své úspěchy v komentářích!

## Co se naučíte dál?

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}