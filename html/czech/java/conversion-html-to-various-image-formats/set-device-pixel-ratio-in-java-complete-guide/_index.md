---
category: general
date: 2026-02-22
description: Nastavte poměr pixelů zařízení v Javě s sandboxem Aspose.HTML. Naučte
  se, jak nastavit vlastní uživatelský agent, získat název stránky v Javě a převést
  HTML na PNG v jednom tutoriálu.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- save html as image
- convert html to png
- get page title java
language: cs
og_description: Nastavte poměr pixelů zařízení v Javě pomocí sandboxu Aspose.HTML.
  Tento tutoriál ukazuje, jak nastavit vlastní uživatelský agent, získat název stránky
  v Javě a převést HTML na PNG.
og_title: Nastavte poměr pixelů zařízení v Javě – kompletní průvodce
tags:
- Aspose.HTML
- Java
- Web Rendering
title: Nastavení poměru pixelů zařízení v Javě – Kompletní průvodce
url: /cs/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení Device Pixel Ratio v Javě – Kompletní průvodce

Už jste se někdy zamýšleli, jak **set device pixel ratio** při vykreslování webové stránky z Javy? Nejste v tom sami. Mnoho vývojářů potřebuje emulovat vysokodpi mobilní obrazovky, aby snímky vypadaly ostré, zejména když je později **save html as image** pro zprávy nebo marketingové materiály. V tomto tutoriálu projdeme praktickým příkladem, který přesně to dělá — a zároveň vám ukážeme, jak **set custom user agent**, **get page title java**, a **convert html to png** pomocí Aspose.HTML.

Začneme stručným přehledem sandbox API, poté se ponoříme do jednotlivých konfiguračních kroků a nakonec vytvoříme PNG soubor, který odráží skutečný iPhone displej. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného Java projektu. Nepotřebujete žádné externí nástroje, jen čistou Javu a Aspose.HTML 7.x (nebo novější).

---

## Požadavky

- Java 17 nebo novější (kód se kompiluje i s dřívějšími verzemi, ale 17 je doporučená).
- Aspose.HTML for Java knihovna (stáhněte z oficiálního webu Aspose; Maven koordináty: `com.aspose:aspose-html:23.10`).
- IDE nebo textový editor dle vašeho výběru (IntelliJ IDEA, VS Code, Eclipse… všechny fungují).
- Přístup k internetu pro demonstrační URL (`https://example.com/responsive.html`), nebo ji nahraďte libovolnou veřejnou HTML stránkou, kterou vlastníte.

> **Pro tip:** Pokud jste za proxy, nakonfigurujte systémové vlastnosti JVM `http.proxyHost` a `http.proxyPort` před spuštěním kódu.

## Krok 1: Nastavení Device Pixel Ratio a dalších Sandbox možností

Prvním, co potřebujeme, je instance **SandboxOptions**, kde definujeme virtuální velikost obrazovky a *device pixel ratio* (DPR). DPR představuje faktor, který říká prohlížeči, kolik fyzických pixelů odpovídá jednomu CSS pixelu. Na Retina iPhone je DPR obvykle **2.0**, proto použijeme tuto hodnotu.

```java
// Step 1: Create and configure SandboxOptions
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS width of an iPhone X
sandboxOptions.setScreenHeight(667);         // CSS height
sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
```

> **Why this matters:** Bez nastavení správného DPR bude vykreslený obrázek rozmazaný nebo příliš velký, protože rasterizér předpokládá mapování 1:1 pixel.

## Krok 2: Nastavení vlastního User Agent

Webové stránky často poskytují odlišný markup na základě hlavičky **User‑Agent**. Aby naše stránka fungovala jako na skutečném iPhone, vložíme vlastní řetězec, který napodobuje Safari na iOS.

```java
// Step 2: Define a mobile‑specific user agent
String iphoneUA = "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                  "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                  "Version/14.0 Mobile/15E148 Safari/604.1";

sandboxOptions.setUserAgent(iphoneUA);   // <-- set custom user agent
```

> **Edge case:** Některé stránky také kontrolují hlavičku `Accept-Language`. Pokud zaznamenáte chybějící překlady, přidejte `sandboxOptions.setAcceptLanguage("en-US,en;q=0.9");`.

## Krok 3: Načtení stránky v sandboxu a získání titulu

Nyní spustíme sandbox s právě definovanými možnostmi. Objekt **Sandbox** izoluje proces vykreslování a zajišťuje, že naše nastavení DPR a user‑agent jsou respektována.

```java
// Step 3: Create the sandbox and load the HTML document
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
HTMLDocument htmlDoc = new HTMLDocument(
        "https://example.com/responsive.html", mobileSandbox);
```

Jakmile se stránka načte, získání titulu je tak jednoduché jako zavolat `getTitle()`. Tím splníme požadavek **get page title java**.

```java
// Step 3b: Print the page title to the console
System.out.println("Title: " + htmlDoc.getTitle());   // <-- get page title java
```

**Očekávaný výstup v konzoli**

```
Title: Responsive Demo – Mobile View
```

Pokud je titulek prázdný, zkontrolujte URL nebo se ujistěte, že stránka není blokována CORS politikou.

## Krok 4: Převod HTML na PNG a uložení HTML jako obrázku

Aspose.HTML vám umožní vykreslit DOM přímo do souboru obrázku. Protože jsme již nastavili DPR na 2.0, výsledné PNG bude mít dvojnásobnou hustotu pixelů, což poskytne ostrý snímek.

```java
// Step 4: Render and save as PNG (convert html to png)
htmlDoc.save("mobile_view.png");   // <-- save html as image
```

Metoda `save` automaticky detekuje příponu souboru a vybere vhodný renderer. Pokud potřebujete jiný formát (JPEG, BMP), stačí změnit název souboru.

> **What if you need a specific image size?**  
> Použijte `ImageSaveOptions` k nastavení šířky, výšky a barvy pozadí:

```java
ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
pngOptions.setWidth(750);   // 375 CSS px * DPR 2
pngOptions.setHeight(1334);
htmlDoc.save("mobile_view_custom.png", pngOptions);
```

## Kompletní funkční příklad

Níže je kompletní, připravený program, který spojuje všechny kroky. Zkopírujte jej do souboru `SandboxDemo.java`, přidejte závislost Aspose.HTML a spusťte `java SandboxDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.rendering.image.ImageSaveOptions;
import com.aspose.html.rendering.image.SaveFormat;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Configure sandbox – set device pixel ratio, screen size, and user agent
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS width (iPhone)
        sandboxOptions.setScreenHeight(667);         // CSS height
        sandboxOptions.setDevicePixelRatio(2.0);     // <-- set device pixel ratio
        sandboxOptions.setUserAgent(
                "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
                "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                "Version/14.0 Mobile/15E148 Safari/604.1");   // <-- set custom user agent

        // 2️⃣ Create sandbox instance
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // 3️⃣ Load the target page inside the sandboxed environment
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox);

        // 4️⃣ Retrieve and print the page title (get page title java)
        System.out.println("Title: " + htmlDoc.getTitle());

        // 5️⃣ Render the page – convert html to png and save html as image
        // Simple save (auto‑detect PNG)
        htmlDoc.save("mobile_view.png");   // <-- save html as image

        // 6️⃣ Optional: custom size rendering
        ImageSaveOptions opts = new ImageSaveOptions(SaveFormat.PNG);
        opts.setWidth(750);   // 375 * DPR 2
        opts.setHeight(1334);
        htmlDoc.save("mobile_view_custom.png", opts); // another convert html to png example
    }
}
```

Spuštěním programu vzniknou dva PNG soubory:

| Soubor | Popis |
|--------|-------|
| `mobile_view.png` | Výchozí vykreslení s nastaveným DPR. |
| `mobile_view_custom.png` | Vykreslení s explicitní šířkou/výškou (užitečné pro fixní velikostní assety). |

Můžete otevřít kterýkoli soubor v libovolném prohlížeči obrázků a ověřit výstup ve vysokém rozlišení.

## Časté otázky a okrajové případy

| Otázka | Odpověď |
|--------|---------|
| **Co když stránka obsahuje JavaScript, který po načtení modifikuje DOM?** | Aspose.HTML spouští skripty ve výchozím nastavení. Pokud potřebujete statický snímek před vykonáním skriptů, nastavte `sandboxOptions.setEnableJavaScript(false)`. |
| **Mohu vykreslit stránku, která vyžaduje autentizaci?** | Ano. Použijte `sandboxOptions.setCredentials(new NetworkCredential("user","pass"))` nebo injektujte cookies pomocí `sandboxOptions.getCookies().add(...)`. |
| **Je DPR omezen na 2.0?** | Ne. Můžete nastavit libovolné kladné číslo typu double (např. 3.0 pro ultra‑vysoké DPI zařízení). Pamatujte však, že vyšší DPR znamená větší soubory obrázků. |
| **Jak zacházet se stránkami s velkými assety (obrázky, fonty)?** | Zvyšte limit paměti sandboxu pomocí `sandboxOptions.setMemoryLimit(512 * 1024 * 1024)` (bajtů). Tím se zabrání chybám out‑of‑memory na těžkých stránkách. |
| **Musím sandbox zavírat ručně?** | Objekt `Sandbox` implementuje `AutoCloseable`. Zabalte jej do bloku try‑with‑resources pro automatické uvolnění. |

## Závěr

Ukázali jsme, jak **set device pixel ratio** v Java sandboxu, **set custom user agent**, **get page title java** a **convert html to png** (efektivně **save html as image**) pomocí Aspose.HTML. Kompletní příklad demonstruje praktický workflow, který můžete přizpůsobit pro automatizovanou generaci snímků, vizuální regresní testování nebo jakýkoli scénář, kde je vyžadována pixel‑dokonalá reprezentace webové stránky.

Neváhejte experimentovat — změňte DPR na 3.0, vyměňte user‑agent za Android řetězec, nebo nasměrujte URL na lokální HTML soubor. Stejný vzor funguje i pro PDF, SVG nebo i vícestránkové vykreslování.

Pokud se vám tento průvodce líbil, zvažte prozkoumání souvisejících témat, jako je **PDF generation with Aspose.HTML**, **headless Chrome alternatives**, nebo **batch rendering of multiple URLs**. Šťastné kódování a ať jsou vaše snímky vždy ostré jako břitva!

![set device pixel ratio in Java sandbox](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}