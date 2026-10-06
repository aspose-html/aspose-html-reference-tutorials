---
category: general
date: 2026-03-04
description: Nastavte pixelový poměr zařízení v Javě, aby se vaše HTML vykreslilo
  v mobilním zobrazení. Naučte se, jak převést HTML na mobilní verzi, testovat responzivní
  HTML a snadno uložit vykreslený HTML soubor.
draft: false
keywords:
- set device pixel ratio
- convert html to mobile
- test responsive html
- save rendered html file
- render html file java
language: cs
og_description: Nastavte poměr pixelů zařízení v Javě pro vykreslení mobilního zobrazení
  vašeho HTML. Tento průvodce ukazuje, jak převést HTML na mobilní verzi, testovat
  responzivní HTML a uložit vykreslený HTML soubor.
og_title: Nastavte poměr pixelů zařízení v Javě – Převod HTML na mobil
tags:
- Aspose.HTML
- Java
- Responsive Design
title: Nastavte poměr pixelů zařízení v Javě – převod HTML na mobilní zařízení
url: /cs/java/conversion-html-to-other-formats/set-device-pixel-ratio-in-java-convert-html-to-mobile/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení device pixel ratio v Javě – Převod HTML na mobil

Už jste se někdy zamýšleli, jak **nastavit device pixel ratio** v Javě, aby váš HTML kód vypadal tak, jako by byl na telefonu? Nejste v tom sami. Mnoho vývojářů narazí na problém, když se snaží **převést HTML na mobil** bez skutečného zařízení, a končí tím, že hádají, zda jejich rozvržení skutečně funguje.  

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který **nastavuje device pixel ratio**, načte responzivní stránku, **renderuje HTML soubor v Java‑stylu** a nakonec **uloží renderovaný HTML soubor** pro pozdější kontrolu. Na konci budete schopni **testovat responzivní HTML** lokálně, bez emulátoru.

## Co budete potřebovat

- **Java 17** nebo novější (API funguje s jakýmkoli aktuálním JDK).  
- Knihovna **Aspose.HTML for Java** – doporučena verze 22.12 nebo novější.  
- Jednoduchá responzivní HTML stránka (např. `responsive.html`).  
- IDE nebo obyčejný textový editor a terminál – podle toho, co preferujete.

To je vše. Žádné další nástroje pro sestavení, žádné Docker kontejnery, jen čistá Java a jediný JAR.

---

## Krok 1: Vytvořte sandbox, který **nastaví device pixel ratio**

Jádrem řešení je třída `DocumentSandbox`. Nastavením rozměrů obrazovky a **device pixel ratio** napodobíte displej s vysokou hustotou pixelů (např. iPhone 6/7/8).  

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class MobileSandbox {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that simulates a mobile device screen
        DocumentSandbox mobileSandbox = new DocumentSandbox();
        mobileSandbox.setScreenWidth(375);          // width in CSS pixels
        mobileSandbox.setScreenHeight(667);         // height in CSS pixels
        mobileSandbox.setDevicePixelRatio(2.0);     // high‑density display

        // The sandbox now **sets device pixel ratio** to 2.0, which tells the renderer
        // to treat each CSS pixel as two physical pixels – exactly what modern phones do.
```

**Proč je to důležité:**  
Pokud vynecháte volání `setDevicePixelRatio`, výstup bude na retina obrazovkách rozmazaný a vaše media queries závislé na `devicePixelRatio` se nikdy neaktivují. Explicitním **nastavením device pixel ratio** zajistíte, že rozvržení se bude chovat přesně jako na skutečném zařízení.

---

## Krok 2: Načtěte svou stránku a **převést HTML na mobil**

Nyní nasměrujeme sandbox na HTML, které chcete prozkoumat. Stejná třída `Document`, kterou používáte pro desktopové renderování, funguje i zde, jen jako druhý argument předáme sandbox.

```java
        // 2️⃣ Load the responsive HTML document inside the sandbox
        // This is where we **convert HTML to mobile** by feeding it the mobileSandbox.
        Document htmlDocument = new Document("YOUR_DIRECTORY/responsive.html", mobileSandbox);
```

**Co se děje pod kapotou?**  
Aspose.HTML načte soubor, použije nastavení viewportu sandboxu a přepočítá CSS jednotky na základě **device pixel ratio**, které jste nastavili dříve. To znamená, že jakákoli pravidla `@media (min-device-pixel-ratio: 2)` budou respektována, což vám umožní **testovat responzivní HTML** bez fyzického telefonu.

---

## Krok 3: **Render HTML soubor v Java‑stylu** a **uložit renderovaný HTML soubor**

Nakonec požádáme `Document`, aby zapsal zpracovaný markup. Výstupem je běžný `.html` soubor, který odráží, jak stránka vypadá na simulovaném zařízení.

```java
        // 3️⃣ Render and save the mobile view of the document
        // The save call creates a new HTML file that you can open in any browser.
        htmlDocument.save("YOUR_DIRECTORY/mobile_view.html");
    }
}
```

Otevřete `mobile_view.html` v Chrome, stiskněte **Ctrl + Shift + I** a přepněte na panel zařízení – uvidíte stejný layout, který jste právě renderovali. Jinými slovy, úspěšně jste **renderovali html soubor v Java** a **uložili renderovaný html soubor** pro pozdější QA.

---

## Úplný, spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do `MobileSandbox.java`. Nezapomeňte nahradit `YOUR_DIRECTORY` skutečnou cestou ke složce, kde se nachází `responsive.html`.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class MobileSandbox {
    public static void main(String[] args) throws Exception {

        // Step 1 – create a sandbox that simulates a mobile device screen
        DocumentSandbox mobileSandbox = new DocumentSandbox();
        mobileSandbox.setScreenWidth(375);          // width in CSS pixels (iPhone 6/7/8)
        mobileSandbox.setScreenHeight(667);         // height in CSS pixels
        mobileSandbox.setDevicePixelRatio(2.0);     // ★ set device pixel ratio ★

        // Step 2 – load the responsive HTML document inside the sandbox
        // This effectively **convert html to mobile** for testing.
        Document htmlDocument = new Document("YOUR_DIRECTORY/responsive.html", mobileSandbox);

        // Step 3 – render and **save rendered html file** for inspection
        htmlDocument.save("YOUR_DIRECTORY/mobile_view.html");

        // Optional: print a friendly confirmation
        System.out.println("Mobile view saved to mobile_view.html – you can now open it in any browser.");
    }
}
```

### Očekávaný výsledek

- `mobile_view.html` obsahuje přesně ten markup, který by prohlížeč použil na obrazovce s hustotou 2×.  
- Všechna media queries závislá na `device-pixel-ratio` se spustí správně.  
- Soubor můžete otevřít v libovolném desktopovém prohlížeči a stále uvidíte mobilní layout, což je ideální pro **testování responzivního HTML** v CI pipelinech.

---

## Tipy a okrajové případy

| Situace | Co dělat | Proč |
|-----------|------------|-----|
| **Různé velikosti obrazovky** | Upravit `setScreenWidth` / `setScreenHeight` tak, aby odpovídaly cílovému zařízení (např. 414 × 896 pro iPhone XR). | Zajišťuje, že váš layout funguje napříč různými breakpointy. |
| **Testování režimu na šířku** | Prohodit hodnoty šířky a výšky a poté znovu uložit. | Landscape často aktivuje odlišná CSS pravidla. |
| **Obrázky ve vysokém rozlišení** | Nechat `setDevicePixelRatio` na 3.0 pro zařízení jako iPhone X. | Donutí renderer vybrat `@2x` nebo `@3x` assety, pokud používáte `srcset`. |
| **Dynamický obsah (JS)** | Použít `htmlDocument.renderToBitmap(...)` místo `save`, pokud potřebujete rastrový snímek. | Některé skripty běží až po úplném vykreslení DOM. |
| **Integrace CI/CD** | Zabalit kód do Maven pluginu nebo Gradle úkolu a spouštět jej jako součást buildu. | Automatizuje **testování responzivního HTML** při každém pull requestu. |

---

## Často kladené otázky

**Q: Můžu tento přístup použít s remote URL místo lokálního souboru?**  
A: Rozhodně. Stačí předat řetězec URL konstruktoru `Document` – sandbox i nadále vynutí **device pixel ratio**, které jste definovali.

**Q: Funguje to na headless serverech?**  
A: Ano. Aspose.HTML je čistě Java knihovna; není potřeba grafické prostředí, což ji činí ideální pro CI pipeline.

**Q: Co když moje stránka používá fonty, které nejsou na serveru nainstalovány?**  
A: Přidejte odkazy na webové fonty do HTML nebo vložte fonty pomocí `@font-face`. Renderer si je stáhne stejně jako běžný prohlížeč.

---

## Závěr

Nyní máte robustní workflow pro **nastavení device pixel ratio**, které vám umožní **převést HTML na mobil**.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}