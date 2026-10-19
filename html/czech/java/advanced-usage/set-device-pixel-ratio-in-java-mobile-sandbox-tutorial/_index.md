---
category: general
date: 2026-10-19
description: nastavte device pixel ratio v Java pomocí Aspose.HTML sandbox. Naučte
  se, jak nastavit screen width height a získat název stránky java s kompletním, spustitelným
  příkladem.
draft: false
keywords:
- get page title java
- device pixel ratio java
- create virtual device java
- set screen width height
lastmod: 2026-10-19
og_description: Získat název stránky java s Aspose.HTML sandbox. Tento průvodce vám
  ukáže, jak nastavit screen width height a device pixel ratio v Java během několika
  jednoduchých kroků.
og_image_alt: 'Developer guide: set device pixel ratio in Java using Aspose.HTML sandbox'
og_title: Získat název stránky java – nastavení device pixel ratio v Java sandbox
  tutoriálu
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: set device pixel ratio in Java using Aspose.HTML sandbox. Learn how
    to set screen width height and get page title java with a complete, runnable example.
  headline: Get page title java – set device pixel ratio in Java sandbox tutorial
  type: TechArticle
- questions:
  - answer: Yes—create a new `SandboxOptions` with a different `setDevicePixelRatio`
      value and instantiate a fresh `Sandbox`. Re‑using the same sandbox after changing
      its options is not supported.
    question: Can I change the pixel ratio at runtime?
  - answer: Loop over a list of `SandboxOptions` (e.g., iPhone 8, Pixel 4) and run
      the same load‑and‑title logic for each.
    question: What if I need to test multiple devices?
  - answer: Aspose.HTML respects Java’s default SSL trust store. Add the cert to the
      JVM’s keystore or, for testing only, disable verification (not recommended for
      production).
    question: Does this work with HTTPS sites that have self‑signed certificates?
  - answer: The `HTMLDocument` API provides `save` methods that can export the rendered
      page to PNG or JPEG. Use `htmlDoc.save("output.png", SaveFormat.PNG);` after
      loading.
    question: How do I capture a screenshot instead of just the title?
  - answer: Each `Sandbox` instance is isolated, but you should avoid sharing a single
      instance across multiple threads without synchronization.
    question: Is the sandbox thread‑safe?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- mobile emulation
title: Získat název stránky java – nastavení device pixel ratio v Java sandbox tutoriálu
url: /cs/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Získání názvu stránky v Java – nastavení poměru pixelů zařízení v sandboxu Java

Už jste někdy potřebovali **nastavit poměr pixelů zařízení** při testování responzivního webu v Javě? Nejste v tom sami. Mnoho vývojářů narazí na problém, když stránka vypadá perfektně na desktopu, ale rozbije se na telefonech s vysokým DPI. Dobrá zpráva? S sandboxem Aspose.HTML můžete emulovat iPhone X (nebo jakékoli zařízení) přímo z vašeho Java kódu – není potřeba prohlížeč.

V tomto průvodci si projdeme **jak nastavit šířku a výšku obrazovky**, nakonfigurovat **poměr pixelů zařízení** a nakonec **získat název stránky v Java** pro ověření, že vše bylo správně vykresleno. Na konci budete mít samostatný program, který můžete vložit do libovolného projektu a okamžitě začít testovat mobilní rozvržení.

## Rychlé odpovědi
- **Jak nastavit poměr pixelů zařízení v Javě?** Použijte `SandboxOptions.setDevicePixelRatio(double)` před vytvořením sandboxu.  
- **Která metoda vrací název stránky?** Zavolejte `htmlDocument.getTitle()` na načteném `HTMLDocument`.  
- **Mohu emulovat jiná zařízení?** Ano – vytvořte nový `SandboxOptions` s požadovanou šířkou, výškou a poměrem pixelů.  
- **Potřebuji ovladač prohlížeče?** Ne, sandbox Aspose.HTML je bezhlavý a běží čistě v Javě.  
- **Která verze Aspose.HTML je vyžadována?** Verze 23.7 nebo novější podporuje všechny funkce mobilní emulace.

## Co je get page title java?
`get page title java` je operace získání elementu `<title>` z HTML dokumentu pomocí Java kódu. Umožňuje vám potvrdit, že stránka načtená ve virtuálním kontextu zařízení vykreslila očekávaný název. Získání názvu je běžný krok v automatizované validaci, aby se zajistilo, že byla načtena správná stránka po aplikaci parametrů emulace zařízení.

## Proč použít sandbox Aspose.HTML pro mobilní emulaci?
Aspose.HTML podporuje **30+** vstupních a výstupních formátů – včetně HTML, CSS, SVG a PDF – a může vykreslovat stránky bez spouštění plného prohlížeče. Jeho sandbox zpracovává stovky stránek při zachování využití paměti pod 200 MB, což ho činí ideálním pro CI pipeline.

## Požadavky

- Java 8 nebo novější (kód se také kompiluje s JDK 11)  
- Knihovna Aspose.HTML pro Java (verze 23.7 nebo novější) – můžete ji získat z Maven Central  
- IDE nebo jednoduché nastavení příkazové řádky `javac`  
- Přístup k internetu pro demo URL (`https://responsive.example.com`)

Žádné další frameworky, žádný Selenium, jen čistá Java a Aspose.HTML.

## Jak nastavit šířku a výšku obrazovky a poměr pixelů zařízení v Javě

`SandboxOptions` třída vám umožňuje specifikovat rozměry obrazovky a hustotu pixelů virtuálního zařízení. Pro emulaci konkrétního mobilního zařízení musíte sandbox nakonfigurovat s požadovanou šířkou, výškou a poměrem pixelů zařízení. Vytvořením objektu `SandboxOptions` a nastavením těchto vlastností bude vykreslovací engine považovat stránku, jako by byla zobrazena na tomto zařízení, což zajistí správné chování CSS media queries a škálování obrázků.

Vytvořte instanci `SandboxOptions`, nastavte šířku na **375**, výšku na **812** a poměr pixelů zařízení na **3.0**. Poté předávejte tyto možnosti novému `Sandbox`. Tím plně nakonfigurujete virtuální zařízení před načtením jakékoli stránky.

`SandboxOptions` třída definuje velikost obrazovky a hustotu pixelů virtuálního zařízení. Je vstupním bodem pro jakýkoli scénář mobilní emulace.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Proč je to důležité:**  
> Volání `setDevicePixelRatio` škáluje vše – od obrázků po vykreslování fontů – takže stránka si myslí, že běží na skutečném telefonu. Pokud to vynecháte, rozložení může přejít na desktopové CSS media queries, čímž se zruší smysl mobilního testování.

## Jak vytvořit instanci sandboxu

`Sandbox` třída představuje prostředí bezhlavého prohlížeče, které vykresluje HTML pomocí dříve definovaných možností. Po nakonfigurování `SandboxOptions` vytvořte instanci `Sandbox` s těmito možnostmi, abyste získali izolovaný vykreslovací kontext. Tento sandbox funguje jako lehký prohlížeč, aplikuje velikost obrazovky a hustotu pixelů, které jste zadali, a může být znovu použit pro více načtení stránek při zachování čistého prostředí.

Instancujte `Sandbox` s dříve nakonfigurovanými `SandboxOptions`. Sandbox se chová jako malý, bezhlavý prohlížeč, který respektuje zadané rozměry a poměr pixelů.

Objekt `Sandbox` je izolovaný vykreslovací engine Aspose.HTML, který běží bez UI. Zaručuje, že každý test běží v čistém prostředí.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Tip:** Můžete znovu použít stejný objekt `Sandbox` pro více načtení stránek; stačí změnit URL a sandbox si zachová stejné charakteristiky zařízení.

## Jak načíst stránku uvnitř sandboxu

`HTMLDocument` třída představuje parsovaný HTML soubor v paměti, poskytující přístup k DOM a možnosti vykreslování. S připraveným sandboxem vytvořte `HTMLDocument` předáním cílové URL a instance sandboxu. Tím se načte a vykreslí stránka pomocí nastavení virtuálního zařízení, což vám umožní pracovat s DOM nebo extrahovat informace, jako je název.

Vytvořte `HTMLDocument` předáním cílové URL a instance `Sandbox`. Toto vynutí, aby dokument byl vykreslen pomocí virtuálního zařízení, které jste nastavili dříve.

`HTMLDocument` třída představuje parsovaný HTML soubor v paměti a poskytuje metody pro manipulaci s DOM a extrakci metadat.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Pokud je URL nedostupná nebo stránka obsahuje chyby, Aspose.HTML vyhodí výjimku. Pro produkční kód byste to zabalili do `try‑catch` a zaznamenali selhání, ale tutoriál to drží jednoduché.

## Jak ověřit pomocí get page title java

Metoda `getTitle()` vrací obsah elementu `<title>` HTML dokumentu jako obyčejný řetězec. Čtení názvu je nejrychlejší kontrola. Po načtení stránky zavolejte `htmlDocument.getTitle()`, abyste získali text názvu. Tato jednoduchá kontrola potvrzuje, že stránka byla správně vykreslena pod nastavením emulovaného zařízení a poskytuje rychlý způsob, jak ověřit navigaci nebo změny obsahu v automatizovaných testech.

Zavolejte `htmlDocument.getTitle()` na načteném dokumentu a výsledek vytiskněte. Pokud sandbox správně aplikoval **poměr pixelů zařízení**, název bude odpovídat tomu, co byste viděli na skutečném iPhone X.

Metoda `getTitle()` vrací obsah elementu `<title>` jako obyčejný řetězec, což vám umožní validovat vykreslení bez vizuální kontroly.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Očekávaný výstup (příklad):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Pokud vidíte vytištěný název, úspěšně jste **nastavili poměr pixelů zařízení**, **nastavili šířku a výšku obrazovky** a **získali název stránky** pomocí Javy.

## Kompletní, spustitelný příklad

Níže je kompletní program, který můžete zkopírovat a vložit do souboru pojmenovaného `SandboxDemo.java`. Ujistěte se, že Aspose.HTML JAR soubory jsou na vaší classpath (`-cp` flag) před kompilací.

Třída `SandboxDemo` spojuje všechny předchozí kroky do jednoho spustitelného příkladu.

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

Měli byste vidět vytištěný název v konzoli, což potvrzuje, že stránka byla vykreslena s požadovaným **poměrem pixelů zařízení**.

## Často kladené otázky a okrajové případy

**Q: Mohu změnit poměr pixelů za běhu?**  
A: Ano – vytvořte nový `SandboxOptions` s jinou hodnotou `setDevicePixelRatio` a vytvořte nový `Sandbox`. Znovupoužití stejného sandboxu po změně jeho možností není podporováno.

**Q: Co když potřebuji testovat více zařízení?**  
A: Procházejte seznam `SandboxOptions` (např. iPhone 8, Pixel 4) a pro každé spusťte stejnou logiku načtení a získání názvu.

**Q: Funguje to s HTTPS stránkami, které mají samopodepsané certifikáty?**  
A: Aspose.HTML respektuje výchozí SSL trust store Javy. Přidejte certifikát do keystore JVM nebo, jen pro testování, deaktivujte ověřování (nedoporučuje se pro produkci).

**Q: Jak zachytit screenshot místo jen názvu?**  
A: API `HTMLDocument` poskytuje metody `save`, které mohou exportovat vykreslenou stránku do PNG nebo JPEG. Použijte `htmlDoc.save("output.png", SaveFormat.PNG);` po načtení.

**Q: Je sandbox thread‑safe?**  
A: Každá instance `Sandbox` je izolovaná, ale měli byste se vyhnout sdílení jedné instance napříč více vlákny bez synchronizace.

## Vizualizace

![Diagram ukazující nastavení poměru pixelů zařízení v mobilním sandboxu](https://example.com/images/sandbox-diagram.png "diagram nastavení poměru pixelů zařízení")

[Diagram ukazující nastavení poměru pixelů zařízení v mobilním sandboxu](https://example.com/images/sandbox-diagram.png "diagram nastavení poměru pixelů zařízení")

*Ilustrace výše mapuje tok od konfigurace `SandboxOptions` (včetně **nastavení šířky a výšky obrazovky** a **nastavení poměru pixelů zařízení**) po načtení URL a extrakci názvu.*

## Závěr

Nyní víte, **jak nastavit poměr pixelů zařízení** v Javě, **jak nastavit šířku a výšku obrazovky** pro přesnou mobilní emulaci a **jak získat název stránky v Java** pro potvrzení úspěšného vykreslení. Tento kompaktní workflow eliminuje potřebu těžkých prohlížečů během automatizovaného UI testování a snadno zapadá do CI pipeline.

Připraven na další krok? Zkuste exportovat vykreslenou stránku jako obrázek, nebo experimentujte s laděním CSS media‑query přepínáním `devicePixelRatio` mezi 1.0 a 3.0. Můžete také prozkoumat funkce konverze PDF v Aspose.HTML pro zachycení tisknutelné verze mobilního zobrazení.

Šťastné kódování a ať jsou vaše mobilní rozvržení vždy ostrá – bez ohledu na hustotu pixelů!

---

**Poslední aktualizace:** 2026-10-19  
**Testováno s:** Aspose.HTML 23.7 for Java  
**Autor:** Aspose

## Související tutoriály

- [Získat HTML název Java vykreslit stránku v sandboxu s šířkou obrazovky](/html/java/advanced-usage/get-html-title-java-render-page-in-sandbox-with-screen-width/)
- [Vytvořit kompletní průvodce Aspose HTML sandbox v Javě](/html/java/configuring-environment/create-aspose-html-sandbox-complete-java-guide/)
- [Nastavení poměru pixelů zařízení v Javě – kompletní průvodce](/html/java/conversion-html-to-various-image-formats/set-device-pixel-ratio-in-java-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}