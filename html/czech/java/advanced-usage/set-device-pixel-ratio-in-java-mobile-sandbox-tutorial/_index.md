---
category: general
date: 2026-02-10
description: Nastavte poměr pixelů zařízení v Javě pomocí sandboxu Aspose.HTML. Naučte
  se, jak nastavit šířku a výšku obrazovky a získat název stránky v Javě s kompletním,
  spustitelným příkladem.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: cs
og_description: Nastavte poměr pixelů zařízení v Javě s sandboxem Aspose.HTML. Tento
  průvodce vám ukáže, jak nastavit šířku a výšku obrazovky a získat název stránky
  v Javě během několika jednoduchých kroků.
og_title: nastavit poměr pixelů zařízení v Javě – Mobile Sandbox tutoriál
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Nastavte poměr pixelů zařízení v Javě – tutoriál Mobile Sandbox
url: /cs/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# nastavení poměru pixelů zařízení v Javě – Mobilní sandbox tutoriál

Už jste někdy potřebovali **nastavit poměr pixelů zařízení** při testování responzivního webu v Javě? Nejste v tom sami. Mnoho vývojářů narazí na problém, když stránka vypadá perfektně na desktopu, ale na telefonech s vysokým DPI selže. Dobrá zpráva? S sandboxem Aspose.HTML můžete emulovat iPhone X (nebo jakékoli jiné zařízení) přímo z vašeho Java kódu – bez nutnosti prohlížeče.

V tomto průvodci si ukážeme **jak nastavit šířku a výšku obrazovky**, nakonfigurovat **poměr pixelů zařízení** a nakonec **získat název stránky v Javě** pro ověření, že vše bylo správně vykresleno. Na konci budete mít samostatný program, který můžete vložit do libovolného projektu a okamžitě začít testovat mobilní rozvržení.

## Požadavky

- Java 8 nebo novější (kód se také kompiluje s JDK 11)  
- Knihovna Aspose.HTML pro Java (verze 23.7 nebo novější) – můžete ji získat z Maven Central  
- IDE nebo jednoduché nastavení příkazové řádky `javac`  
- Přístup k internetu pro demonstrační URL (`https://responsive.example.com`)

Žádné další frameworky, žádný Selenium, jen čistá Java a Aspose.HTML.

---

## Krok 1: Nastavit šířku a výšku obrazovky a poměr pixelů zařízení

Prvním, co potřebujeme, je objekt `SandboxOptions`, který sandboxu říká, jaké “zařízení” předstíráme. Zde použijeme rozměry iPhone X (375 × 812 CSS pixelů) a **poměr pixelů zařízení** 3,0, který napodobuje displej s vysokým DPI Retina.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Proč je to důležité:**  
> Volání `setDevicePixelRatio` škáluje vše – od obrázků po vykreslování fontů – takže stránka si myslí, že běží na skutečném telefonu. Pokud to vynecháte, rozvržení může přejít na desktopové CSS media queries, čímž se zruší smysl mobilního testování.

---

## Krok 2: Vytvořit instanci sandboxu

Nyní proměníme tyto možnosti na živý sandbox. Představte si sandbox jako malý, bezhlavý prohlížeč, který respektuje definované rozměry a poměr pixelů.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Tip:** Můžete znovu použít stejný objekt `Sandbox` pro načítání více stránek; stačí změnit URL a sandbox si zachová stejné charakteristiky zařízení.

---

## Krok 3: Načíst stránku v sandboxu

S připraveným sandboxem je načtení stránky tak jednoduché jako vytvořit `HTMLDocument` a předat sandbox jako druhý argument. Tím se dokument vynutí vykreslit pomocí virtuálního zařízení, které jsme dříve nastavili.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Pokud je URL nedostupná nebo stránka obsahuje chyby, Aspose.HTML vyhodí výjimku. V produkčním kódu byste to pravděpodobně zabalili do `try‑catch` a zaznamenali selhání, ale pro tutoriál to ponecháme jednoduché.

---

## Krok 4: Ověřit pomocí get page title java

Nejrychlejší kontrola je přečíst název dokumentu. Pokud sandbox správně použil **poměr pixelů zařízení**, bude název shodný s tím, co byste viděli na skutečném iPhone X.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Očekávaný výstup (příklad):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Pokud vidíte vytištěný název, úspěšně jste **nastavili poměr pixelů zařízení**, **nastavili šířku a výšku obrazovky** a **získali název stránky** pomocí Javy.

---

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do souboru pojmenovaného `SandboxDemo.java`. Ujistěte se, že jsou Aspose.HTML JAR soubory ve vaší classpath (`-cp` přepínač) před kompilací.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Zkompilujte a spusťte:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Měli byste vidět název vytištěný do konzole, což potvrzuje, že stránka byla vykreslena s požadovaným **poměrem pixelů zařízení**.

---

## Často kladené otázky a okrajové případy

| Otázka | Odpověď |
|----------|--------|
| **Mohu změnit poměr pixelů během běhu?** | Ano – stačí vytvořit nový `SandboxOptions` s jinou hodnotou `setDevicePixelRatio` a vytvořit nový `Sandbox`. Opětovné použití stejného sandboxu po změně jeho možností není podporováno. |
| **Co když potřebuji testovat více zařízení?** | Projděte seznam `SandboxOptions` (např. iPhone 8, Pixel 4) a pro každé spusťte stejnou logiku načtení a získání názvu. |
| **Funguje to s HTTPS stránkami, které mají samopodepsané certifikáty?** | Aspose.HTML respektuje výchozí SSL trust store Javy. Přidejte certifikát do keystore JVM nebo vypněte ověřování pouze pro testování (nedoporučuje se pro produkci). |
| **Jak zachytím screenshot místo pouhého názvu?** | `HTMLDocument` API poskytuje metody `save`, které mohou exportovat vykreslenou stránku do PNG nebo JPEG. Po načtení použijte `htmlDoc.save("output.png", SaveFormat.PNG);`. |
| **Je sandbox thread‑safe?** | Každá instance `Sandbox` je izolovaná, ale neměli byste sdílet jednu instanci napříč více vlákny bez synchronizace. |

---

## Vizuální přehled

![Diagram ukazující nastavení poměru pixelů zařízení v mobilním sandboxu](https://example.com/images/sandbox-diagram.png "diagram nastavení poměru pixelů zařízení")

*Ilustrace výše mapuje tok od konfigurace `SandboxOptions` (včetně **nastavení šířky a výšky obrazovky** a **nastavení poměru pixelů zařízení**) po načtení URL a získání názvu.*

---

## Závěr

Nyní víte, **jak nastavit poměr pixelů zařízení** v Javě, **jak nastavit šířku a výšku obrazovky** pro přesnou mobilní emulaci a **jak získat název stránky v Javě** pro potvrzení úspěšného vykreslení. Tento kompaktní workflow eliminuje potřebu těžkopádných prohlížečů během automatizovaného UI testování a snadno se integruje do CI pipeline.

Jste připraveni na další krok? Zkuste exportovat vykreslenou stránku jako obrázek, nebo experimentujte s laděním CSS media‑query přepínáním `devicePixelRatio` mezi 1,0 a 3,0. Můžete také prozkoumat funkce převodu PDF v Aspose.HTML pro zachycení tisknutelné verze mobilního zobrazení.

Šťastné kódování a ať vaše mobilní rozvržení vždy vypadá ostré – bez ohledu na hustotu pixelů!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}