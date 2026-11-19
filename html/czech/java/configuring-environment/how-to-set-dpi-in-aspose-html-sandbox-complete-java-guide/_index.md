---
category: general
date: 2026-04-02
description: Naučte se, jak nastavit DPI, velikost viewportu a uživatelského agenta
  v Aspose.HTML Sandbox. Krok za krokem Java příklad s kompletním kódem a tipy.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: cs
og_description: Naučte se, jak nastavit DPI, velikost viewportu a uživatelský agent
  v Aspose.HTML Sandbox pomocí kompletního příkladu v Javě.
og_title: Jak nastavit DPI v Aspose.HTML Sandbox – Java tutoriál
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Jak nastavit DPI v Aspose.HTML Sandbox – Kompletní průvodce pro Javu
url: /cs/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak nastavit DPI v Aspose.HTML Sandbox – Kompletní průvodce pro Javu

Už jste se někdy zamysleli **jak nastavit DPI** při vykreslování webové stránky pomocí Aspose.HTML? Nejste v tom sami. V mnoha testovacích scénářích potřebujete, aby rozvržení odpovídalo konkrétní hustotě obrazovky – například PDF připraveným k tisku nebo snímkům obrazovky ve vysokém rozlišení. Dobrou zprávou je, že sandbox Aspose.HTML vám umožňuje ovládat DPI, velikost viewportu a dokonce i řetězec user‑agent v jednom přehledném balíčku.

V tomto tutoriálu projdeme praktickým příkladem v Javě, který **nastavuje DPI**, **nastavuje velikost viewportu** a **nastavuje user‑agent** najednou. Na konci budete mít spustitelný program, pochopíte, proč každé nastavení má význam, a budete připraveni upravit sandbox pro své vlastní projekty.

---

## Co budete potřebovat

- **Java 17** (nebo jakýkoli aktuální JDK; API je kompatibilní s Java 8+)
- **Aspose.HTML for Java** knihovna (verze 23.12 nebo novější)
- IDE nebo jednoduchý textový editor + kompilace z příkazové řádky
- Přístup k internetu pro ukázkovou URL (`https://example.com`)

Externí nástroje pro sestavování nejsou vyžadovány; kód se kompiluje pomocí `javac` a spouští pomocí `java`. Pokud dáváte přednost Maven nebo Gradle, stačí přidat závislost Aspose.HTML – nic složitého.

---

## Krok 1: Vytvořte sandbox, který definuje prostředí vykreslování

Sandbox je místo, kde říkáte Aspose.HTML, jakou „obrazovku“ předstíráte. Zde nastavíme **viewport 1024 × 768**, **DPI 96** a vlastní **user‑agent řetězec**.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Proč je to důležité:**  
- **DPI** ovlivňuje, jak se CSS jednotky `pt` převádějí na pixely; vyšší DPI poskytuje ostřejší vykreslení.  
- **Velikost viewportu** určuje, kde se spustí breakpointy v responzivním CSS.  
- **User‑agent** může spustit různé varianty obsahu na straně serveru (mobilní vs. desktop).

> **Pro tip:** Pokud později generujete PDF, nastavte DPI odpovídající cílovému rozlišení tisku (např. 300 dpi pro vysoce kvalitní výtisky).

---

## Krok 2: Načtěte webovou stránku uvnitř sandboxu

Nyní nasměrujeme sandbox na URL. Konstruktor `HTMLDocument` přijímá sandbox, takže vykreslovací engine respektuje právě nastavená nastavení.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Co se děje pod kapotou?**  
Aspose.HTML vytvoří izolovaný kontext vykreslování, podobný headless prohlížeči, ale bez zátěže plnohodnotné instance Chromium. To činí operaci rychlou a úspornou na paměť – ideální pro dávkové zpracování.

---

## Krok 3: Interakce s DOM – přečtěte název stránky

Pro demonstraci získáme titulek a vypíšeme jej. Ve skutečném scénáři můžete pořídit snímek obrazovky, exportovat do PDF nebo scrapovat data.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Očekávaný výstup** (pokud je `https://example.com` dostupná):

```
Title inside sandbox: Example Domain
```

Pokud stránka vrátí jiný titulek, zobrazí se ten místo něj – žádná další úprava není potřeba.

---

## Krok 4: Ověřte nastavení (volitelná diagnostika)

Někdy chcete zkontrolovat, že sandbox skutečně respektuje vaše DPI a viewport. Aspose.HTML tyto hodnoty přímo neexponuje, ale můžete je odvodit měřením rozměrů elementů.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Pokud víte, že CSS deklaruje element jako `width: 200pt;`, při **96 dpi** byste měli vidět `200pt * (96/72) ≈ 267px`. Změňte DPI a spusťte znovu, abyste viděli změnu čísla – důkaz, že **jak nastavit dpi** skutečně funguje.

---

## Kompletní zdrojový kód v jednom bloku

Zkopírujte následující kód do souboru `SandboxExample.java`. Kompiluje se tak, jak je; jen se ujistěte, že je JAR Aspose.HTML na classpath.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Zkompilujte a spusťte:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Měli byste vidět vytištěný titulek, což potvrzuje, že sandbox funguje s **nastaveným dpi**, **nastavenou velikostí viewportu** a **nastaveným user agentem**, které jste zadali.

---

## Časté otázky a okrajové případy

### Co když potřebuji jiné DPI?

Stačí změnit druhý argument konstruktoru `DocumentSandbox`. Pro PDF připravené k tisku můžete použít `300`:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Vyšší DPI dává větší rozměry pixelů pro stejné CSS body, což zlepšuje kvalitu rastru, ale spotřebovává více paměti.

### Můžu načíst lokální HTML soubor místo URL?

Určitě. Nahraďte URL cestou k souboru:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Ujistěte se, že cesta je absolutní a používá schéma `file:///`.

### Jak změním user‑agent po vytvoření sandboxu?

Sandbox je neměnný – jakmile jej předáte `HTMLDocument`, nastavení jsou uzamčena. Pro použití jiného user‑agentu vytvořte nový `DocumentSandbox` s požadovaným řetězcem.

### Podporuje Aspose.HTML vykonávání JavaScriptu?

Ano, engine spouští většinu klientských skriptů. Pokud skript po načtení upraví DOM, můžete chvíli počkat:

```java
webDoc.waitForLoad();
```

Nebo použít logiku podobnou `setTimeout` přímo na stránce před dotazováním elementů.

---

## Vizuální potvrzení (obrázek)

Níže je snímek konzole ukazující úspěšné spuštění. Všimněte si, že výstup titulu odpovídá stránce, což potvrzuje, že sandbox respektoval naše nastavení.

![Console output showing how to set dpi in Aspose.HTML Sandbox](/images/console-output.png)

*Alt text:* *Výstup konzole demonstrující nastavení dpi, velikosti viewportu a user agenta v Aspose.HTML Sandbox.*

---

## Shrnutí a další kroky

Probrali jsme **jak nastavit DPI** (96 dpi v příkladu), **nastavit velikost viewportu** (1024 × 768) a **nastavit user‑agent** (vlastní řetězec) pomocí API sandboxu v Aspose.HTML. Kompletní, spustitelný Java program dokazuje, že tato nastavení nejsou jen teoretická – přímo ovlivňují vykreslování a interakci s DOM.

Připravení na další?

- **Export do PDF:** Po načtení stránky zavolejte `webDoc.save("output.pdf", SaveFormat.PDF);` a vytvořte PDF ve vysokém rozlišení, které odráží nastavené DPI.  
- **Pořízení snímku obrazovky:** Použijte `webDoc.renderToBitmap("screenshot.png");` pro pixel‑perfektní obrázky.  
- **Hrajte si s responzivními rozvrženími:** Změňte rozměry viewportu a testujte mobilní breakpointy bez skutečného zařízení.  

Experimentujte s různými hodnotami DPI, kombinacemi viewportu a user‑agenty a sledujte, jak servery a CSS reagují. Sandbox je lehká hřiště, která vám ušetří spouštění plnohodnotných prohlížečů.

---

### Pokračujte v objevování

- **Dokumentace Aspose.HTML** – podrobný průzkum možností `DocumentSandbox`.  
- **Pokročilé CSS Media Queries** – naučte se, jak velikost viewportu spouští různé styly.  
- **User‑Agent Spoofing** – zjistěte, jak některé stránky poskytují alternativní markup na základě řetězce agenta.

Máte otázky nebo složitý případ? Zanechte komentář a pojďme to společně vyřešit. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}