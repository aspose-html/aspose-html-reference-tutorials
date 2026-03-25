---
category: general
date: 2026-03-25
description: Jak použít sandbox k zachycení snímku webové stránky pomocí Aspose.HTML
  pro Java. Naučte se uložit HTML jako PNG, převod HTML na obrázek a převod HTML na
  PNG během několika minut.
draft: false
keywords:
- how to use sandbox
- capture webpage screenshot
- save html as png
- html to image conversion
- html to png conversion
language: cs
og_description: Jak použít sandbox k zachycení snímku webové stránky. Tento tutoriál
  ukazuje, jak uložit HTML jako PNG, zahrnuje konverzi HTML na obrázek a konverzi
  HTML na PNG pomocí Aspose.HTML pro Javu.
og_title: Jak použít Sandbox k pořízení snímku webové stránky
tags:
- Aspose.HTML
- Java
- Web Automation
title: Jak použít Sandbox k pořízení screenshotu webové stránky
url: /cs/java/conversion-html-to-various-image-formats/how-to-use-sandbox-to-capture-webpage-screenshot/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak použít sandbox k zachycení snímku webové stránky

Použití sandboxu k zachycení snímku webové stránky je častý požadavek, když potřebujete pixel‑dokonalý náhled responzivní stránky. V tomto průvodci vám také ukážeme, jak **uložit HTML jako PNG** pomocí Aspose.HTML for Java, pokrývající vše od *html to image conversion* po *html to png conversion* v jednom reprodukovatelném příkladu.

Představte si, že testujete marketingovou vstupní stránku, která vypadá odlišně na telefonu, tabletu a desktopu. Místo otevírání tří prohlížečů můžete spustit sandbox, nasměrovat jej na URL a okamžitě získat PNG, které přesně odráží to, co by vykreslilo skutečné zařízení. Na konci tohoto tutoriálu budete mít kompletní spustitelný Java program, který to dělá, plus několik praktických tipů, které můžete znovu použít ve svých projektech.

## Co budete potřebovat

- **Aspose.HTML for Java** (v23.9 nebo novější). Knihovna je dostupná přes Maven Central, takže přidání závislosti je hračka.
- **JDK 11+** nainstalovaný na vašem počítači.
- IDE nebo textový editor podle vašeho výběru (IntelliJ IDEA, VS Code, Eclipse… jakýkoli bude stačit).
- Přístup k internetu pro ukázkovou URL (`https://example.com/responsive.html`) nebo ji nahraďte libovolnou stránkou, kterou chcete zachytit.

Žádné další nativní binární soubory ani headless prohlížeče nejsou potřeba — sandbox běží zcela v paměti.

---

## Jak použít sandbox – Krok 1: Definovat virtuální zařízení

První věc, kterou uděláte, je říct sandboxu, jakou velikost obrazovky chcete emulovat. Zde se ukáže hlavní klíčové slovo: *how to use sandbox* pro konkrétní viewport.

```java
// Step 1: Create a DeviceInfo that describes the virtual screen
DeviceInfo sandboxDevice = new DeviceInfo();
sandboxDevice.setWidth(800);               // width in pixels
sandboxDevice.setHeight(600);              // height in pixels
sandboxDevice.setDevicePixelRatio(1.0);    // 1 × for standard displays
sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");
```

**Proč je to důležité:**  
Nastavení šířky a výšky nutí layout engine zacházet se stránkou, jako by byla zobrazena na monitoru 800×600. `devicePixelRatio` ovlivňuje, jak se chovají CSS‑založené media queries (`@media (min‑device‑pixel‑ratio: ...)`), což zajišťuje, že snímek odpovídá reálnému zážitku.

> **Tip:** Pokud potřebujete snímek s vysokým DPI (např. Retina displeje), zvyšte `devicePixelRatio` na `2.0` a podle toho navýšte šířku/výšku.

## Zachycení snímku webové stránky – Krok 2: Načíst stránku uvnitř sandboxu

Nyní požádáme Aspose.HTML, aby načetl vzdálené HTML a vykreslil jej uvnitř sandboxu, který jsme právě definovali. Tento krok je jádrem **capture webpage screenshot**.

```java
// Step 2: Load the remote HTML page using the sandboxed environment
HTMLDocument document = new HTMLDocument(
        "https://example.com/responsive.html",
        new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));
```

**Co se děje pod kapotou?**  
`HTMLDocumentLoadOptions` získá instanci `Sandbox`, která obsahuje náš `DeviceInfo`. Knihovna pak vytvoří headless renderovací kontext, který respektuje viewport, řetězec user‑agent a jakýkoli JavaScript, který stránka může spustit — *bez spouštění Chrome nebo Firefox*.

Pokud cílová stránka vyžaduje autentizaci, můžete pomocí `HTMLDocumentLoadOptions` také injektovat cookies nebo vlastní hlavičky. To je užitečný okrajový případ při práci s intranetovými portály.

## Uložit HTML jako PNG – Krok 3: Převést vykreslený dokument na obrázek

Po vykreslení stránky je posledním krokem **uložit HTML jako PNG**. Toto je skutečný krok *html to png conversion*.

```java
// Step 3: Convert the rendered document to PNG and write it to disk
try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
    Converter.convertDocument(
            document,
            new ConversionOptions(ConversionFormat.PNG),
            out);
}
```

Když `Converter` dokončí, najdete soubor pojmenovaný `responsive_page.png` ve složce `output`. Otevřete jej a uvidíte přesně, jak stránka vypadala při 800×600 pixelech — žádné UI prohlížeče, žádné posuvníky, jen čisté vykreslení.

**Časté úskalí:**  
- **Chyby oprávnění k souborům:** Ujistěte se, že adresář existuje (`output/` v příkladu) a váš proces do něj může zapisovat.  
- **Velké stránky:** Velmi dlouhé stránky mohou vytvořit obrovské PNG soubory; můžete omezit výšku v `DeviceInfo` nebo oříznout po konverzi.  
- **Dynamický obsah:** Pokud stránka načítá data přes AJAX po úvodním načtení, možná budete muset zavést krátké zpoždění (`Thread.sleep(2000)`) před konverzí, nebo použít `HTMLDocumentLoadOptions.setWaitForResources(true)`.

### html to image conversion – Pokročilé možnosti

Aspose.HTML nabízí několik nastavení, která můžete otáčet pro jemné doladění **html to image conversion**:

| Option | Description | When to use |
|--------|-------------|-------------|
| `ConversionOptions.setQuality(int)` | Nastaví úroveň komprese PNG (0‑100). | Snížení velikosti souboru pro webové assety. |
| `ConversionOptions.setBackgroundColor(Color)` | Vynutí barvu pozadí (výchozí je průhledná). | Užitečné, když má stránka průhledné sekce. |
| `ConversionOptions.setPageSize(PageSize)` | Přepíše velikost sandboxu pro výstupní obrázek. | Vytvořit miniatury s jiným rozlišením. |

Níže je rychlý úryvek, který nastavuje bílou barvu pozadí a kvalitu 90 %:

```java
ConversionOptions pngOptions = new ConversionOptions(ConversionFormat.PNG);
pngOptions.setBackgroundColor(java.awt.Color.WHITE);
pngOptions.setQuality(90);

try (FileOutputStream out = new FileOutputStream("output/white_bg_page.png")) {
    Converter.convertDocument(document, pngOptions, out);
}
```

## Kompletní funkční příklad

Spojením všeho dohromady, zde je kompletní program, který můžete zkopírovat a vložit do souboru `SandboxResponsiveExample.java` a spustit:

```java
import com.aspose.html.devices.DeviceInfo;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ConversionOptions;
import com.aspose.html.converters.ConversionFormat;
import com.aspose.html.render.HTMLDocument;
import com.aspose.html.render.HTMLDocumentLoadOptions;
import com.aspose.html.render.Sandbox;

import java.io.FileOutputStream;

public class SandboxResponsiveExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Define a sandbox with the desired viewport (800×600) and device pixel ratio
        DeviceInfo sandboxDevice = new DeviceInfo();
        sandboxDevice.setWidth(800);
        sandboxDevice.setHeight(600);
        sandboxDevice.setDevicePixelRatio(1.0);
        sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");

        // Step 2: Load the remote HTML page inside the sandboxed environment
        HTMLDocument document = new HTMLDocument(
                "https://example.com/responsive.html",
                new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));

        // Step 3: Convert the document to PNG – the output reflects exactly how the page looks on the defined screen size
        try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
            Converter.convertDocument(
                    document,
                    new ConversionOptions(ConversionFormat.PNG),
                    out);
        }

        System.out.println("Screenshot saved to output/responsive_page.png");
    }
}
```

Spuštění programu vypíše potvrzovací řádek a uloží PNG do složky `output`. Otevřete soubor a uvidíte věrnou reprezentaci vzdálené stránky v přesně zadané velikosti.

## Často kladené otázky

**Q: Funguje to s lokálními HTML soubory?**  
A: Naprosto. Nahraďte URL `file://` URI nebo předáte cestu `java.io.File` do konstruktoru `HTMLDocument`.

**Q: Co když potřebuji PDF místo PNG?**  
A: Vyměňte `ConversionFormat.PNG` za `ConversionFormat.PDF`. Zbytek kódu zůstane stejný.

**Q: Můžu zachytit celostránkový (posouvací) snímek?**  
A: Nastavte výšku `DeviceInfo` na výšku posouvání stránky (`document.getDocumentElement().getScrollHeight()`) před konverzí, nebo použijte `ConversionOptions.setPageSize` pro zvětšení plátna.

## Závěr

Nyní víte, **jak použít sandbox** k zachycení snímku webové stránky, uložit HTML jako PNG a provést spolehlivou html to image conversion pomocí Aspose.HTML for Java. Přístup je lehký, plně programovatelný a obchází zátěž tradičních headless prohlížečů.

Co dál? Zkuste vyměnit výstup PNG za PDF, experimentujte s různými device pixel ratio pro napodobení Retina displejů, nebo automatizujte dávkové zpracování desítek URL. Stejná technika sandboxu může být také přetížena pro **html to png conversion** v CI pipelinech, vizuálním regresním testování nebo generování miniatur pro systém správy obsahu.

Neváhejte zanechat komentář, pokud narazíte na problémy, a šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}