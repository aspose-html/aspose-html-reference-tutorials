---
category: general
date: 2026-09-29
description: Nastavte vlastní uživatelský agent v Aspose.HTML pro Javu a naučte se,
  jak nastavit virtuální velikost obrazovky pro přesné vykreslování HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: cs
lastmod: 2026-09-29
og_description: Nastavte vlastní uživatelský agent v Aspose.HTML pro Javu a zjistěte,
  jak nastavit virtuální velikost obrazovky pro přesné vykreslování HTML.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Nastavte vlastní uživatelský agent a rozměry obrazovky v Aspose.HTML pro
  Javu
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Nastavte vlastní uživatelský agent a rozměry obrazovky v Aspose.HTML pro Javu
url: /cs/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nastavení vlastního uživatelského agenta a rozměrů obrazovky v Aspose.HTML pro Java

Pokud potřebujete **nastavit vlastní uživatelský agent** při renderování HTML pomocí Aspose.HTML pro Java, tento návod vám přesně ukáže, jak na to. Konfigurací sandboxu získáte také možnost **nastavit virtuální velikost obrazovky**, což zajistí, že rozvržení odpovídá skutečnému viewportu prohlížeče.

Na konci tohoto tutoriálu budete mít kompletní spustitelný program, který **určuje uživatelský agent**, **nastavuje šířku obrazovky** a **nastavuje výšku obrazovky**. Nejsou potřeba žádné externí nástroje – stačí Aspose.HTML pro Java a runtime Java 8+.

## Co se naučíte

* Jak vytvořit `SandboxConfiguration` pro izolaci renderování.
* Jak **nastavit vlastní uživatelský agent** a proč je to důležité pro responzivní stránky.
* Jak **nastavit virtuální velikost obrazovky** (šířka a výška) pro přesné rozvržení.
* Jak načíst HTML soubor v sandboxu a uložit zpracovaný výsledek.
* Běžné úskalí a tipy na osvědčené postupy pro sandboxové renderování.

> **Požadavky** – Potřebujete platnou licenci Aspose.HTML pro Java, Java 8 nebo novější a IDE (IntelliJ IDEA, Eclipse nebo VS Code). Příklad používá lokální soubor `input.html`, ale funguje jakýkoli přístupný URL.

![Diagram toku sandboxu](sandbox-flow.png "příklad nastavení vlastního uživatelského agenta v Javě")

## Krok 1: Vytvoření konfigurace sandboxu (základ)

Sandbox izoluje renderovací prostředí od hostitelské JVM, což je nezbytné, když chcete **nastavit vlastní uživatelský agent** nebo změnit velikost viewportu.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Proč je tento krok důležitý?*  
`SandboxConfiguration` obsahuje všechna nastavení renderování, včetně **rozměrů obrazovky** a řetězců **user‑agent**. Konfigurací před načtením dokumentu zajistíte, že HTML engine bude respektovat tato nastavení již od první žádosti.

## Krok 2: Nastavení rozměrů obrazovky tak, aby napodobovaly skutečné zařízení

Responzivní stránky často čtou `window.innerWidth` a `window.innerHeight`. Aby engine „myslel“, že běží na obrazovce 1024 × 768, **nastavíte virtuální velikost obrazovky**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Proč je to důležité* – Pokud vynecháte **nastavení rozměrů obrazovky**, renderer může použít výchozí malý viewport, což způsobí, že CSS media queries zvolí mobilní rozvržení. Explicitním **nastavením šířky obrazovky** a **výšky obrazovky** řídíte, které CSS pravidla se použijí.

## Krok 3: Specifikace vlastního řetězce user‑agent

Některé webové stránky poskytují odlišný obsah na základě hlavičky user‑agent. Pro **specifikaci uživatelského agenta** jej jednoduše nastavíte v konfiguraci sandboxu:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Proč použít vlastní user agent?*  
Vlastní řetězec může obejít detekci botů, spustit funkce určené jen pro desktop nebo otestovat, jak se stránka chová pro konkrétní verzi prohlížeče. Aspose engine předává tuto hodnotu s každým HTTP požadavkem při načítání externích zdrojů (CSS, obrázky, skripty).

## Krok 4: Načtení HTML dokumentu uvnitř sandboxu

Jakmile je sandbox plně nakonfigurován, načtěte HTML soubor. Konstruktor, který přijímá cestu k souboru a `SandboxConfiguration`, automaticky použije všechna nastavení, která jsme definovali.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Pokud potřebujete načíst ze vzdáleného URL, nahraďte cestu k souboru řetězcem URL – Aspose.HTML i nadále bude respektovat **nastavený vlastní user agent** a **rozměry obrazovky**.

## Krok 5: Uložení zpracovaného výstupu

Po dokončení načítání dokumentu jej můžete uložit v libovolném podporovaném formátu. Zde zapisujeme sandboxovaný HTML soubor, který odráží všechny změny DOM způsobené vlastními nastaveními.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

Uložený soubor bude obsahovat stejný markup, ale všechny skripty, které dotazovaly `navigator.userAgent` nebo kontrolovaly `window.innerWidth`, nyní uvidí hodnoty, které jste zadali.

## Kompletní, spustitelný příklad

Spojením všech kroků dohromady získáte samostatný program, který můžete zkopírovat, vložit a spustit.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Očekávaný výstup

Spuštěním programu se vytvoří `sandboxed_output.html`. Pokud jej otevřete v prohlížeči a v konzoli zkontrolujete `navigator.userAgent`, uvidíte **AsposeHTML/1.0**. Stejně tak `window.innerWidth` zobrazí **1024**, což potvrzuje, že **nastavení rozměrů obrazovky** fungovalo podle očekávání.

## Časté otázky a řešení okrajových případů

| Otázka | Odpověď |
|----------|--------|
| **Co když stránka načítá další zdroje z jiné domény?** | Sandbox předává **vlastní user agent** s každým požadavkem, ale zásady cross‑origin stále platí. Použijte `sandboxConfig.setAllowCrossDomain(true)`, pokud potřebujete tyto omezení uvolnit. |
| **Mohu změnit velikost obrazovky po načtení dokumentu?** | Ne. Rozměry obrazovky jsou načteny během počátečního průchodu layoutem. Pro renderování s jinou velikostí vytvořte novou `SandboxConfiguration` a dokument načtěte znovu. |
| **Musím volat `document.close()`?** | `HTMLDocument` implementuje `AutoCloseable`. Použití bloku try‑with‑resources zajišťuje řádné uvolnění prostředků, ale explicitní volání `close()` je v jednoduchých skriptech volitelné. |
| **Jak se to liší od nastavení user‑agentu v HTTP klientovi?** | Nastavení user‑agentu v sandboxu ovlivňuje **všechny** požadavky na zdroje prováděné HTML engine, ne jen počáteční načtení HTML. To napodobuje skutečný prohlížeč přesněji. |
| **Je sandbox bezpečný pro nedůvěryhodné HTML?** | Ano. Sandbox izoluje přístup k souborovému systému a omezuje síťová volání podle konfigurace, čímž snižuje riziko, že škodlivé skripty ovlivní vaši hostitelskou JVM. |

## Pro tipy

* **Znovupoužití konfigurací** – Pokud renderujete mnoho stránek se stejným viewportem, vytvořte jednu `SandboxConfiguration` a znovu ji použijte, abyste se vyhnuli režii při vytváření objektů.
* **Ladění pomocí logování** – Povolením logování Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`) můžete vidět, které zdroje byly načteny s vlastním user‑agentem.
* **Kombinace s CSS media queries** – Úpravou **nastavení šířky obrazovky** můžete testovat, jak se vaše responzivní design chová na tabletech, telefonech nebo velkých desktopech, aniž byste otevírali skutečný prohlížeč.

## Závěr

Nyní víte, jak **nastavit vlastní uživatelský agent** a **nastavit rozměry obrazovky** při renderování HTML pomocí Aspose.HTML pro Java. Konfigurací sandboxu izolujete prostředí, řídíte viewport a zajistíte, že externí zdroje uvidí přesně hlavičky, které určíte. Tato technika je nezbytná pro testování responzivních rozvržení, obcházení blokování botů nebo reprodukci funkcí určených jen pro desktop v automatizovaných pipelinech.

Dále můžete prozkoumat **jak nastavit vlastní cookies** nebo **zachytit renderované screenshoty** pomocí renderovacího API Aspose.HTML – oba koncepty staví na stejném vzoru konfigurace sandboxu, který jste právě zvládli.

Šťastné kódování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto návodu. Každý zdroj obsahuje kompletní funkční příklady kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Vysoké DPI renderování v Javě – Zachycení screenshotů webových stránek s vlastním uživatelským agentem](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [Jak načíst HTML, nastavit DPI zařízení a přečíst barvu pozadí](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Vytvoření HTML souboru v Javě a nastavení síťové služby (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}