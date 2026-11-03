---
category: general
date: 2026-04-03
description: Zjistěte, jak používat sandbox v Aspose.HTML Java k nastavení uživatelského
  agenta, nastavení velikosti a okamžitému získání velikosti viewportu. Kompletní
  kód, vysvětlení a tipy jsou zahrnuty.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: cs
og_description: Naučte se, jak používat sandbox v Aspose.HTML Java k nastavení uživatelského
  agenta, nastavení velikosti a okamžitému získání velikosti viewportu. Kompletní
  průvodce s kódem a osvědčenými postupy.
og_title: Jak používat Sandbox – nastavit User Agent a získat velikost viewportu
tags:
- AsposeHTML
- Java
- Sandbox
title: Jak používat Sandbox – nastavit uživatelský agent a získat velikost viewportu
url: /cs/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat Sandbox – nastavit User Agent a získat velikost viewportu

Už jste se někdy zamýšleli **jak používat sandbox** při renderování HTML pomocí Aspose.HTML for Java? Možná jste narazili na problém při simulaci konkrétní velikosti obrazovky nebo potřebujete podvrhnout řetězec user‑agent, aby se stránka chovala, jako by byla navštívena z mobilního prohlížeče.  

Dobrou zprávou je, že sandbox API vám umožní přesně to, a také můžete získat vypočtenou velikost viewportu po načtení stránky. V tomto tutoriálu projdeme vytvoření sandboxu, nastavení velikosti, nastavení vlastního user agenta, načtení vzdálené stránky a nakonec přečtení rozměrů viewportu. Na konci budete vědět **jak nastavit velikost**, **jak získat viewport** a proč jsou tyto kroky důležité pro spolehlivé headless renderování.

> **Rychlý výsledek:** budete mít spustitelnou třídu Java, která během několika sekund vytiskne něco jako `Viewport: 1280×800`.

---

## Co budete potřebovat

- **Aspose.HTML for Java** verze 24.6 nebo novější (API, které používáme, bylo zavedené v 24.5).  
- Vývojový kit Java 17+ (jakýkoli aktuální JDK funguje).  
- IDE nebo jednoduchý textový editor – žádné speciální pluginy nejsou potřeba.  
- Přístup k internetu, pokud chcete načíst externí URL, například `https://example.com`.

To je vše. Není povinné používat Maven/Gradle; můžete JAR soubory přidat na classpath ručně, pokud chcete.

---

## Jak používat Sandbox – přehled

Sandbox izoluje renderovací engine od hostitelského OS, což vám umožní definovat virtuální obrazovku (šířka, výška, DPI) a vlastní **user agent** řetězec. Představte si to jako miniaturální okno prohlížeče, které existuje výhradně v paměti. Když později požádáte `HTMLDocument` o jeho výchozí pohled, engine vrátí **velikost viewportu**, kterou vypočítal na základě nastavení sandboxu.  

Níže je vysokou úrovní tok:

1. **Vytvořte** `DocumentSandbox` a nakonfigurujte šířku, výšku, DPI a user‑agent.  
2. **Načtěte** `HTMLDocument` uvnitř tohoto sandboxu.  
3. **Dotazujte** výchozí pohled dokumentu na velikost viewportu.  

Pojďme se ponořit do jednotlivých kroků.

---

## Krok 1: Vytvořit sandbox a nastavit velikost

Nejprve spustíme sandbox a řekneme mu, jak velká má být virtuální obrazovka. Zde odpovídáte na otázku **jak nastavit velikost** pro headless renderování.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Tip:** Pokud testujete responzivní rozvržení, zkuste úzkou šířku jako `360` pro emulaci telefonu, nebo širokou jako `1920` pro desktop. Sandbox respektuje nastavené DPI, takže obrazovka s vysokou hustotou (např. 144 DPI) ovlivní media‑queries používající `device-pixel-ratio`.

---

## Krok 2: Nastavit User Agent pro sandbox

Proč se obtěžovat s vlastním **user agent**? Některé stránky dodávají odlišný markup nebo skripty v závislosti na hlášeném prohlížeči. Voláním `setUserAgent` můžete stránku přimět, aby si myslela, že je navštěvována z Chrome, Firefoxu nebo mobilního zařízení.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Nyní si stránka bude myslet, že se renderuje na iPhone. Pokud potřebujete **nastavit user agent** zpět na výchozí, stačí znovu použít dříve uvedený řetězec “AsposeHTML/24.6 …”.

---

## Krok 3: Načíst HTML dokument uvnitř sandboxu

Po připravení sandboxu můžeme načíst libovolnou URL nebo lokální HTML soubor. Konstruktor `HTMLDocument` přijímá sandbox jako druhý argument, čímž je spojuje.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

Blok `try‑with‑resources` zajišťuje, že dokument je řádně uvolněn, čímž se uvolní nativní zdroje, které Aspose.HTML alokuje pod kapotou.

---

## Krok 4: Získat velikost viewportu z dokumentu

Tady je okamžik, na který jste čekali: získání **viewport size**, kterou renderovací engine vypočítal. To odpovídá na otázku **jak získat viewport** po rozložení stránky.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Po spuštění programu byste měli vidět něco jako:

```
Viewport: 1280×800
```

Pokud jste v Kroku 1 změnili rozměry sandboxu, vytištěná čísla budou odrážet tyto nové hodnoty – ideální pro automatizované testy ověřující responzivní breakpointy.

---

## Kompletní funkční příklad

Níže je kompletní, připravená třída, která spojuje všechny části. Zkopírujte a vložte ji do souboru pojmenovaného `SandboxExample.java`, přidejte JAR‑y Aspose.HTML do classpath a spusťte `java SandboxExample`.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Očekávaný výstup** (při výše uvedených nastaveních sandboxu):

```
Viewport: 1280×800
```

Pokud nastavíte jinou šířku/výšku v sandboxu, výstup se podle toho změní – přesně to, co potřebujete při testování responzivních návrhů.

---

## Okrajové případy a časté otázky

### Co když stránka používá `window.innerWidth` místo CSS media queries?

Virtuální velikost obrazovky sandboxu ovlivňuje jak CSS rozvržení, tak JavaScriptové `window.innerWidth/innerHeight`. Takže **jak získat viewport** pomocí JavaScriptu vrátí stejná čísla, která vidíte v Java konzoli.

### Můžu spustit více sandboxů paralelně?

Ano. Každá instance `DocumentSandbox` je nezávislá, takže můžete vytvořit thread pool, přidělit každému vláknu vlastní sandbox s různými rozměry a renderovat desítky stránek současně. Jen nezapomeňte, že JAR‑y jsou thread‑safe (jsou).

### Ovlivňuje nastavení DPI škálování obrázků?

Rozhodně. Vyšší DPI způsobí, že jeden CSS pixel mapuje na více zařízení pixelů, což může způsobit, že obrázky s vysokým rozlišením budou vypadat ostřeji. Pokud testujete assety ve stylu retina, zkuste `sandbox.setDeviceDpi(144)`.

### Jak zacházet s HTTPS certifikáty, které jsou self

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}