---
category: general
date: 2026-04-26
description: Spusťte JavaScript z Javy pomocí Aspose.HTML a naučte se, jak nastavit
  vlastní user-agent pro simulované okno prohlížeče.
draft: false
keywords:
- run javascript from java
- set custom user-agent
- how to set user-agent
- configure window settings
- simulate browser java
language: cs
og_description: Spusťte JavaScript z Javy s Aspose.HTML. Naučte se, jak nastavit vlastní
  uživatelský agent a konfigurovat nastavení okna pro simulovaný prohlížeč.
og_title: Spusťte JavaScript z Javy – Nastavte vlastní User-Agent
tags:
- Java
- Aspose.HTML
- JavaScript Execution
title: Spouštění JavaScriptu z Javy – Nastavení vlastního User‑Agenta pomocí Aspose.HTML
url: /cs/java/advanced-usage/run-javascript-from-java-set-custom-user-agent-with-aspose-h/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Spusťte JavaScript z Javy – Nastavte vlastní User-Agent pomocí Aspose.HTML

Už jste někdy potřebovali **spustit JavaScript z Javy**, přičemž jste se tvářili jako skutečný prohlížeč? Možná scrapujete stránku, která blokuje neznámé agenty, nebo chcete jednoduše otestovat skript bez otevírání Chrome. V tomto tutoriálu vám přesně ukážeme, jak to provést, a také se podíváme na **nastavení user-agentu**, aby vzdálený server myslel, že komunikujete s běžným desktopovým prohlížečem.

Budeme používat knihovnu Aspose.HTML, která poskytuje Javě lehké prostředí podobné head‑less prohlížeči. Na konci tohoto průvodce budete schopni spustit libovolný úryvek JavaScriptu, nakonfigurovat nastavení okna a **simulovat chování prohlížeče v Javě** s vlastním řetězcem user‑agent. Žádné externí prohlížeče, žádný Selenium, jen čistý Java kód.

## Co budete potřebovat

- **Java 17** (nebo jakýkoli recentní JDK; API funguje na Java 8+)
- **Aspose.HTML for Java** 23.9 (nebo nejnovější verze v době psaní)
- Slušné IDE (IntelliJ IDEA, Eclipse, VS Code — podle vás)
- Základní znalost konceptů Java a JavaScript

Pokud je již máte, skvělé — přejděte rovnou kódu. Pokud ne, stáhněte si Aspose.HTML JAR z oficiální stránky a přidejte jej do classpath vašeho projektu; knihovna obsahuje všechny závislosti, takže nebudete potřebovat nic dalšího.

> **Tip:** Když přidáváte JAR do Maven projektu, použijte následující koordináty:  
> ```xml
> <dependency>
>     <groupId>com.aspose</groupId>
>     <artifactId>aspose-html</artifactId>
>     <version>23.9</version>
> </dependency>
> ```

---

## ## Spustit JavaScript z Javy: Základní myšlenka

V jádru třída `Window` z Aspose.HTML napodobuje okno prohlížeče. Můžete jí poskytnout HTML, CSS a JavaScript a poté požádat o vyhodnocení skriptu a vrácení výsledku. Představte si to jako malý Chrome, který běží uvnitř vašeho JVM, ale bez UI.

Níže je kompletní, připravený k spuštění program, který demonstruje celý tok:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JsEngineExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create window settings and define a custom User‑Agent string
        WindowSettings windowSettings = new WindowSettings();
        windowSettings.setUserAgent(
            "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
        );

        // Step 2: Open a browser‑like window using the configured settings
        try (Window browserWindow = new Window(windowSettings)) {

            // Step 3: Execute JavaScript that reads the navigator.userAgent property
            browserWindow.evaluateScript("var ua = navigator.userAgent; ua;");

            // Step 4: Retrieve the script result (the custom User‑Agent) and display it
            String userAgent = (String) browserWindow.getLastResult();
            System.out.println("Custom user‑agent: " + userAgent);
        }
    }
}
```

**Očekávaný výstup**

```
Custom user‑agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36
```

Spuštění tohoto programu najednou dokazuje tři věci:

1. Vy **spustíte JavaScript z Javy** (`evaluateScript`).
2. Vy **nastavíte vlastní user-agent** (`setUserAgent` na `WindowSettings`).
3. Vy **nakonfigurujete nastavení okna** pro simulaci reálného prostředí prohlížeče.

---

## ## Nakonfigurujte nastavení okna pro realistický prohlížeč

Proč vůbec používat `WindowSettings`? Většina webových služeb kontroluje hlavičku `User‑Agent`, aby rozhodla, zda poskytne mobilní, desktopový nebo bot‑specifický obsah. Pokud vynecháte realistický řetězec, můžete dostat zjednodušenou verzi stránky, nebo můžete být přímo zablokováni.

### Postupné rozdělení

| Krok | Co děláme | Proč je to důležité |
|------|------------|----------------|
| **Create `WindowSettings`** | `new WindowSettings()` | Poskytuje kontejner pro všechny možnosti podobné prohlížeči. |
| **Set the user‑agent** | `windowSettings.setUserAgent("…")` | Napodobuje klienta Chrome/Edge/Firefox, vyhýbá se detekci botů. |
| **Pass settings to `Window`** | `new Window(windowSettings)` | Okno nyní dědí naše vlastní nastavení. |

Můžete také upravit další vlastnosti, jako `setLocale`, `setScreenWidth` nebo `setScreenHeight`, abyste dále **simulovali podmínky prohlížeče v Javě**. Například nastavení šířky obrazovky na 1920 px způsobí, že responzivní stránky si myslí, že jste na desktopovém monitoru.

```java
windowSettings.setScreenWidth(1920);
windowSettings.setScreenHeight(1080);
```

## ## Nastavte vlastní User-Agent: Běžné varianty

Neexistuje univerzální řetězec user‑agent. V závislosti na cílové stránce můžete potřebovat:

- **Chrome na Windows** (příklad výše)
- **Safari na macOS**  
  ```java
  windowSettings.setUserAgent(
      "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) " +
      "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.1 Safari/605.1.15"
  );
  ```
- **Mobilní Chrome**  
  ```java
  windowSettings.setUserAgent(
      "Mozilla/5.0 (Linux; Android 11; Pixel 5) " +
      "AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.71 Mobile Safari/537.36"
  );
  ```

Když se objeví otázka **jak nastavit user-agent**, odpověď je jednoduchá – „zavolejte `setUserAgent` s přesným řetězcem, který chcete.“ Žádné extra hlavičky, žádné manipulace na úrovni sítě. Knihovna vše vyřeší pod kapotou.

## ## Simulujte prohlížeč v Javě: Přesahování User-Agentu

Pokud chcete **simulovat prohlížeč v Javě** důkladněji — například potřebujete cookies, lokální úložiště nebo dokonce vlastní objekt `navigator` — Aspose.HTML nabízí několik dalších nastavení:

```java
// Enable cookies
windowSettings.setCookiePolicy(CookiePolicy.ACCEPT_ALL);

// Pre‑populate local storage
browserWindow.getLocalStorage().setItem("token", "abc123");

// Override navigator.platform if needed
browserWindow.evaluateScript(
    "Object.defineProperty(navigator, 'platform', { get: () => 'Win32' });"
);
```

Tyto úryvky ukazují, jak můžete tvarovat prostředí tak, aby odpovídalo téměř jakémukoli reálnému scénáři prohlížeče. Mějte na paměti, že každá další funkce může zvýšit spotřebu paměti, ale pro většinu automatizačních úkolů je režie zanedbatelná.

## ## Časté úskalí a jak se jim vyhnout

1. **Zapomenutí zavřít `Window`** – Blok `try‑with‑resources` v příkladu zajišťuje, že okno je uvolněno. Pokud jej vytváříte ručně, vždy zavolejte `browserWindow.close()` v `finally` bloku.
2. **Použití zastaralého user‑agentu** – Webové stránky často aktualizují logiku detekce. Pravidelně obnovujte řetězec z nástrojů vývojáře skutečného prohlížeče (Network → Headers → User‑Agent).
3. **Spouštění skriptů závislých na DOM** – `evaluateScript` funguje dobře pro čistý JavaScript, ale pokud potřebujete kompletní HTML dokument, načtěte jej nejprve:  
   ```java
   browserWindow.navigate("about:blank");
   browserWindow.getDocument().write("<html><body></body></html>");
   ```
4. **Bezpečnost vláken** – Každá instance `Window` je svázána s vláknem, které ji vytvořilo. Neshareujte stejné okno mezi více vlákny; místo toho vytvořte nové okno pro každé vlákno.

## ## Ověřte výsledek – Rychlý test

Po zkompilování a spuštění programu by se měl na konzoli vypsat vlastní user‑agent. Pro dvojitou kontrolu, že knihovna skutečně odesílá hlavičku, můžete nasměrovat okno na jednoduchou echo službu:

```java
browserWindow.navigate("https://httpbin.org/user-agent");
browserWindow.evaluateScript("document.body.textContent;");
String echoed = (String) browserWindow.getLastResult();
System.out.println("Echoed from server: " + echoed);
```

Výstup bude obsahovat stejný řetězec, který jste nastavili dříve, což potvrzuje, že krok **nakonfigurování nastavení okna** fungoval od začátku do konce.

## ## Kompletní funkční příklad (všechny kroky dohromady)

Níže je finální, samostatná Java třída, kterou můžete zkopírovat a vložit do libovolného IDE:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class JsEngineFullDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create and configure window settings
        WindowSettings settings = new WindowSettings();
        settings.setUserAgent(
            "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
        );
        settings.setScreenWidth(1920);
        settings.setScreenHeight(1080);
        settings.setCookiePolicy(CookiePolicy.ACCEPT_ALL);

        // 2️⃣ Open the headless window
        try (Window win = new Window(settings)) {

            // 3️⃣ Run a simple script that returns navigator.userAgent
            win.evaluateScript("var ua = navigator.userAgent; ua;");
            String ua = (String) win.getLastResult();
            System.out.println("Custom user‑agent: " + ua);

            // 4️⃣ Optional: Verify via an external service
            win.navigate("https://httpbin.org/user-agent");
            win.evaluateScript("document.body.textContent;");
            String echoed = (String) win.getLastResult();
            System.out.println("Echoed from server: " + echoed);
        }
    }
}
```

Spusťte ji, sledujte konzoli a úspěšně jste **spustili JavaScript z Javy**, nastavili **vlastní user-agent** a **nakonfigurovali nastavení okna** pro simulaci reálného prohlížeče — vše bez opuštění JVM.

## ## Ilustrace obrázku

![Spuštění JavaScriptu z Javy s vlastním user-agentem – příklad](https://example.com/images/run-js-from-java.png "Spuštění JavaScriptu z Javy s vlastním user-agentem – příklad")

*Diagram ukazuje tok: Java → Aspose.HTML `Window` → JavaScript vykonání → Výsledek.*

## ## Další kroky a související témata

- **Pokročilá manipulace s DOM** – Načtěte kompletní HTML stránku a použijte `document.querySelector` uvnitř `evaluateScript`.
- **Headless testování** – Kombinujte Aspose.HTML s JUnit pro automatické ověřování výsledků JavaScriptu.
- **Podpora proxy** – Pokud cílová stránka blokuje vaši IP, nakonfigurujte `WindowSettings.setProxy` pro směrování provozu přes proxy server.
- **Ladění výkonu** – Pro hromadné operace znovu použijte jedinou instanci `Window` a mezi běhy pouze vyčistěte její dokument.

Každé z těchto témat staví na základech, které jsme zde položili: **spustit javascript z java**, **nastavit vlastní user-agent** a **nakonfigurovat nastavení okna**. Prozkoumejte dokumentaci Aspose.HTML pro podrobnější pokrytí API, nebo experimentujte s výše uvedenými úryvky kódu, aby vyhovovaly vašemu konkrétnímu případu.

## ## Závěr

Prošli jsme kompletním, spustitelným příkladem, který vám ukazuje, jak **spustit JavaScript z Javy**, nastavit vlastní user‑agent a plně **nakonfigurovat nastavení okna** pro **simulaci chování prohlížeče v Javě**. Přístup je lehký

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}