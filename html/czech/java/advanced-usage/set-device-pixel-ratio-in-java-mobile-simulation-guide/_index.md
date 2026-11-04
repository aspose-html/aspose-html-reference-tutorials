---
category: general
date: 2026-04-05
description: Naučte se, jak nastavit poměr pixelů zařízení v Javě pomocí sandboxu
  Aspose.HTML, nastavit vlastní uživatelský agent, simulovat mobilní zařízení, získat
  vypočtený styl v Javě a získat pozadí elementu.
draft: false
keywords:
- set device pixel ratio
- set custom user agent
- simulate mobile device
- get computed style java
- retrieve element background
language: cs
og_description: Nastavte poměr pixelů zařízení v Javě pomocí sandboxu Aspose.HTML,
  nastavte vlastní uživatelský agent, simulujte mobilní zařízení, získejte vypočtený
  styl v Javě a načtěte pozadí prvku.
og_title: Nastavte poměr pixelů zařízení v Javě – Průvodce mobilní simulací
tags:
- Aspose.HTML
- Java
- Web testing
title: Nastavení poměru pixelů zařízení v Javě – Průvodce mobilní simulací
url: /cs/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-simulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# nastavení poměru pixelů zařízení v Javě – Průvodce simulací mobilu

Už jste někdy potřebovali **nastavit poměr pixelů zařízení** v Javě, abyste viděli, jak stránka vypadá na telefonu s retina displejem? Nejste v tom sami. S Aspose.HTML můžete spustit sandbox, **nastavit vlastní user agent**, a dokonce **získat barvu pozadí elementu** – vše bez opuštění vašeho IDE.

V tomto tutoriálu vás provedeme vytvořením sandboxu, který **simuluje chování mobilního zařízení**, upraví hustotu pixelů, získá vypočtené CSS a vytiskne pozadí hlavičky. Na konci budete mít kompletní, spustitelný příklad, který funguje s libovolným responzivním webem. Žádné externí nástroje, jen čistá Java a knihovna Aspose.HTML.

## Požadavky

- Java 17 nebo novější (kód se kompiluje i se staršími verzemi, ale 17 je doporučeno).
- Aspose.HTML pro Javu 23.4 nebo novější – můžete získat JAR z Maven Central.
- Základní znalost HTML a CSS (není potřeba nic složitého).
- Přístup k internetu pro demonstrační stránku (`https://example.com/responsive.html`).

> **Tip:** Pokud jste za firemním proxy, nastavte JVM proxy vlastnosti před spuštěním dema.

## Krok 1: Jak **nastavit poměr pixelů zařízení** v sandboxu

Prvním krokem je vytvořit instanci `Sandbox` a nastavit jí logickou velikost viewportu zařízení, které chcete napodobit. Poté použijete `setDevicePixelRatio`, aby renderovací engine věděl, že každý CSS pixel odpovídá dvěma fyzickým pixelům – stejně jako u iPhone 6/7/8.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // Create a sandbox that pretends to be a mobile phone
        Sandbox mobileSandbox = new Sandbox();

        // Define the logical screen size (width × height in CSS pixels)
        mobileSandbox.setViewportSize(new Size(375, 667)); // iPhone 6/7/8 dimensions

        // 👇 This is where we **set device pixel ratio** to 2.0
        mobileSandbox.setDevicePixelRatio(2.0);

        // Continue with the rest of the steps…
```

Proč je to důležité? Prohlížeče používají poměr pixelů zařízení k určení ostrosti obrázků a k aktivaci media queries jako `@media (min-device-pixel-ratio: 2)`. Když poměr odpovídá, získáte věrnou reprezentaci stránky na obrazovkách s vysokou hustotou pixelů.

## Krok 2: **nastavit vlastní user agent** pro realistické požadované hlavičky

Webové stránky často poskytují odlišný markup na základě řetězce `User‑Agent`. Aby váš sandbox opravdu věřil, že je iPhone, musíte **nastavit vlastní user agent**. Tím se vyhnete přesměrování na desktopovou verzi nebo obdržení generické náhradní verze.

```java
        // Set a realistic iPhone user‑agent string
        mobileSandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 14_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0 Mobile/15E148 Safari/604.1"
        );
```

Všimněte si zalomení řádku a řetězení řetězců – udržuje to délku řádku čitelnou. Pokud tento krok vynecháte, server může myslet, že jste desktopový Chrome, a naservírovat zcela odlišné rozložení, což podkopává smysl **simulace mobilního zařízení**.

## Krok 3: Načtěte stránku a **simulujte chování mobilního zařízení**

Jakmile je sandbox nakonfigurován, můžete načíst libovolnou responzivní URL. Sandbox automaticky použije velikost viewportu, poměr pixelů a user‑agent, které jste právě nastavili, a tím efektivně **simuluje podmínky mobilního zařízení**.

```java
        // Load the responsive HTML document inside the configured sandbox
        try (HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com/responsive.html", mobileSandbox)) {

            // From here on we work with the DOM just like a normal browser
```

Pokud cílová stránka používá lazy‑loading obrázky nebo JavaScript, který závisí na `window.innerWidth`, vše se bude chovat přesně jako na skutečném iPhone. To je obzvláště užitečné pro CI pipeline, kde potřebujete deterministické screenshoty nebo ověření CSS.

## Krok 4: Jak **získat vypočtený styl v Javě** pro element

Jakmile je dokument načten, můžete dotazovat libovolný element a požádat engine o jeho *vypočtené* CSS hodnoty. V Javě je metoda `getComputedStyle()`. To je jádro použití **get computed style java**.

```java
            // Locate the <header> element we want to inspect
            HTMLElement headerElement = htmlDoc.getElementsByTagName("header").item(0);

            // Retrieve the computed CSS style for that element
            CSSStyleDeclaration computedStyle = headerElement.getComputedStyle();

            // Now we can read any property—background‑color, font‑size, etc.
```

Proč nečíst jen inline styl? Protože mnoho stránek nastavuje barvy pomocí externích stylových souborů nebo media queries. `getComputedStyle` vyřeší vše po kaskádě a poskytne vám finální hodnotu, kterou prohlížeč skutečně vykreslí.

## Krok 5: **získat pozadí elementu** a vypsat výsledek

Nakonec extrahujeme barvu pozadí a zobrazíme ji. Toto demonstruje **retrieve element background** v čistém jednorázovém výrazu.

```java
            // Output the background color that the browser would render
            System.out.println("Header background: " + computedStyle.getBackgroundColor());
        }
    }
}
```

Po spuštění programu byste měli vidět něco jako:

```
Header background: rgb(255, 255, 255)
```

Pokud stránka používá pro mobilní verzi tmavý header, výstup to odrazí – přesně to, co byste viděli na zařízení se stejným **nastaveným poměrem pixelů zařízení**.

## Vizualizace

![Diagram ukazující, jak nastavení poměru pixelů zařízení, vlastní user agent a viewport spolupracují v sandboxu Aspose.HTML k simulaci mobilního zařízení](https://example.com/images/sandbox-diagram.png)

*Alt text obrázku obsahuje hlavní klíčové slovo, což pomáhá jak vyhledávačům, tak čtečkám obrazovky.*

## Časté úskalí a jak se jim vyhnout

- **Chybějící velikost viewportu** – Pokud přeskočíte `setViewportSize`, sandbox použije výchozí desktop‑velikost viewportu a vaše media queries se neaktivují.
- **Špatný poměr pixelů** – Použití `1.0` podkopává smysl; většina moderních telefonů používá `2.0` nebo `3.0`. Zkontrolujte specifikace zařízení, pokud potřebujete přesnou shodu.
- **Neshody User‑Agent** – Některé stránky kontrolují `iPhone` *a* verzi `OS`. Držte se úplného řetězce, jak je uvedeno v kroku 2.
- **Chyby načítání zdrojů** – Ujistěte se, že sandbox má přístup k internetu; jinak se nenačtou externí CSS/JS a `getComputedStyle` může vracet výchozí hodnoty.

## Rozšíření příkladu

Nyní, když můžete **nastavit poměr pixelů zařízení**, **nastavit vlastní user agent**, **simulovat mobilní zařízení**, **získat vypočtený styl v Javě** a **získat pozadí elementu**, se možná ptáte, co dalšího můžete udělat.

- **Pořizovat screenshoty** – Aspose.HTML může renderovat sandbox do PNG nebo JPEG, ideální pro vizuální regresní testování.
- **Spouštět JavaScript** – Sandbox podporuje vykonávání skriptů, takže můžete testovat dynamické změny UI.
- **Iterovat přes breakpoints** – Procházet několik šířek viewportu a poměrů pixelů pro ověření responzivního designu napříč celým spektrem.

## Závěr

Právě jste se naučili, jak **nastavit poměr pixelů zařízení** v Javě, nakonfigurovat **vlastní user agent**, **simulovat podmínky mobilního zařízení**, **získat vypočtený styl v Javě** a **získat pozadí elementu** pomocí sandbox API Aspose.HTML. Kompletní úryvek kódu výše je připraven k vložení do libovolného Java projektu, kompilaci a spuštění.

Neváhejte upravit rozměry viewportu, vyzkoušet jinou URL nebo experimentovat s jinými CSS vlastnostmi jako `font-size` nebo `margin`. Stejný vzor funguje pro jakýkoli element, který potřebujete zkontrolovat, což z tohoto přístupu činí univerzální nástroj ve vaší sadě pro webové testování.

Pokud vám tento průvodce přišel užitečný, zvažte jeho sdílení s kolegy nebo přidání hvězdičky do repozitáře Aspose.HTML na GitHubu. Šťastné programování a ať vaše pixel‑perfektní testy vždy uspějí!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}