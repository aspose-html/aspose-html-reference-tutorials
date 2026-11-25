---
category: general
date: 2026-03-26
description: Naučte se, jak emulovat iPhone v Javě pomocí Aspose.HTML. Zahrnuje kroky
  pro nastavení vlastního uživatelského agenta a nastavení poměru pixelů zařízení
  pro přesné mobilní vykreslování.
draft: false
keywords:
- how to emulate iphone
- set custom user agent
- set device pixel ratio
- how to set user-agent
- how to set dpr
language: cs
og_description: Jak emulovat iPhone v Javě? Tento tutoriál ukazuje, jak nastavit vlastní
  uživatelský agent a poměr pixelů zařízení pomocí Aspose.HTML, což umožňuje doručovat
  mobilní stránky s dokonalou pixelovou přesností.
og_title: Jak emulovat iPhone – krok za krokem průvodce Aspose.HTML
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Jak emulovat iPhone – Kompletní průvodce s Aspose.HTML
url: /cs/java/html5-canvas-rendering/how-to-emulate-iphone-complete-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak emulovat iPhone – Kompletní průvodce s Aspose.HTML

Už jste se někdy zamýšleli **jak emulovat iPhone** při lokálním testování webové stránky? Možná ladíte responzivní rozvržení a desktopový prohlížeč prostě nevyhovuje. Dobrá zpráva je, že nepotřebujete fyzické zařízení — `DocumentSandbox` z Aspose.HTML vám umožní napodobit obrazovku iPhone, user‑agent a device‑pixel‑ratio (DPR) pomocí několika řádků Javy.  

V tomto tutoriálu projdeme přesně kroky, jak nastavit **vlastní user agent**, nakonfigurovat **device pixel ratio** a ověřit, že vše funguje podle očekávání. Na konci budete mít znovupoužitelný sandbox, který vykresluje stránky přesně jako iPhone 8, a pochopíte, proč je každé nastavení důležité.

## Co dosáhnete

- Vytvoříte objekt `Screen`, který odráží rozměry iPhone a jeho DPR.  
- Aplikujete **vlastní user agent** řetězec, aby servery myslely, že požadavek pochází ze Safari na iOS.  
- Sestavíte `DocumentSandbox`, který spojuje obrazovku a user‑agent.  
- Spustíte `HTMLDocument` uvnitř sandboxu a uvidíte výstup v konzoli potvrzující konfiguraci.  

Nejsou potřeba žádné externí knihovny kromě Aspose.HTML a kód běží v libovolném prostředí Java 17+.

---

![jak emulovat iPhone screenshot](https://example.com/images/iphone-emulation.png "jak emulovat iPhone pomocí Aspose.HTML sandbox")

## Jak emulovat iPhone s Aspose.HTML Sandbox

Prvním krokem je vytvořit `Screen`, který odráží fyzické rozměry iPhone *a* jeho hustotu pixelů. To je jádro **jak emulovat iPhone** přesně.

```java
import com.aspose.html.devices.Screen;

// Step 1: Define iPhone 8 screen size (width, height) and DPR
Screen mobileScreen = new Screen(375, 667, 2.0); // iPhone 8 dimensions, DPR = 2
```

**Proč je to důležité:**  
- Šířka = 375 px a výška = 667 px jsou CSS rozměry, které uvidíte v Chrome DevTools při výběru iPhone 8.  
- Nastavení DPR na 2 říká vykreslovacímu enginu, aby každý CSS pixel považoval za dva fyzické pixely, což poskytuje ostrý text a obrázky — přesně tak, jak to dělá skutečné zařízení.

> *Tip:* Pokud potřebujete emulovat novější iPhone (např. iPhone 13), stačí změnit čísla na 390 × 844 a DPR = 3.

## Nastavení vlastního User Agent (set custom user agent)

Dále potřebujeme **nastavit vlastní user agent**, aby server poskytl mobilní specifické HTML/CSS. Bez toho si mnoho stránek stále myslí, že jste na desktopu.

```java
// Step 2: Define an iPhone Safari user‑agent string
String iPhoneUserAgent = "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) " +
                         "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                         "Version/16.0 Mobile/15E148 Safari/604.1";
```

**Jak to funguje:**  
- Header `User-Agent` je „handshake“, který prohlížeče používají k představení sebe.  
- Poskytnutím přesného řetězce, který posílá Safari na iOS 16, zajistíte, že server vrátí mobilně optimalizované assety (responsivní obrázky, adaptivní skripty atd.).  

Když budete potřebovat **jak nastavit user-agent** pro jiné zařízení, stačí řetězec nahradit odpovídající hodnotou — Google Chrome, Firefox nebo dokonce vlastní bot.

## Konfigurace Device Pixel Ratio (set device pixel ratio)

Nyní skutečně **nastavíme device pixel ratio** uvnitř sandboxu. Tento krok přímo odpovídá na otázku “**jak nastavit dpr**” pro simulované prostředí.

```java
import com.aspose.html.sandbox.DocumentSandbox;

// Step 3: Build the sandbox with screen and user‑agent
DocumentSandbox documentSandbox = new DocumentSandbox.Builder()
        .setScreen(mobileScreen)          // applies the DPR we defined earlier
        .setUserAgent(iPhoneUserAgent)    // applies the custom user‑agent
        .build();
```

**Vysvětlení:**  
- Vzor `Builder` vám umožňuje plynule připojit jak obrazovku (která nese DPR), tak user‑agent.  
- Když sandbox vykreslí `HTMLDocument`, bude se tvářit, že běží na zařízení s touto přesnou hustotou pixelů.  

> *Proč na tom záleží:* Některé CSS media queries používají `device-pixel-ratio` (např. `@media (-webkit-min-device-pixel-ratio: 2)`). Pokud DPR nenastavíte, tato pravidla se nikdy neaktivují a přijdete o vysoce rozlišené assety.

## Ověření konfigurace sandboxu (how to set user-agent)

Pojďme sandbox vyzkoušet. Následující úryvek vytvoří `HTMLDocument`, načte stránku a vytiskne potvrzení, že sandbox je aktivní.

```java
import com.aspose.html.HTMLDocument;

public class SandboxWithDprAndUa {
    public static void main(String[] args) {
        // Re‑use the sandbox we built earlier
        // DocumentSandbox documentSandbox = ... (from previous step)

        // Step 4: Load a page inside the sandbox
        HTMLDocument doc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 5: Optional – output a sanity check
        System.out.println("Sandbox configured with DPR=2 and iPhone user‑agent.");
    }
}
```

**Očekávaný výstup v konzoli**

```
Sandbox configured with DPR=2 and iPhone user-agent.
```

Pokud spustíte program a uvidíte tento řádek, úspěšně jste **jak emulovat iPhone** s správným DPR a user‑agentem. Otevřete stránku v reálném prohlížeči a zkontrolujte rozměry viewportu — uvidíte, že odpovídají hodnotám iPhone, které jsme nastavili.

## Časté problémy a jak správně nastavit DPR (how to set dpr)

I při správném kódu se můžete setkat s několika úskalími:

| Problém | Proč k tomu dochází | Řešení |
|---------|---------------------|--------|
| **DPR zůstává na 1** | Předali jste `Screen` bez třetího argumentu (DPR). | Vždy používejte `new Screen(width, height, dpr)`. |
| **User‑Agent je ignorován** | Sandbox nebyl připojen k `HTMLDocument`. | Předávejte `documentSandbox` jako druhý argument konstruktoru `HTMLDocument`. |
| **Špatné rozměry** | Používáte pixelové hodnoty zařízení místo CSS pixelů. | Pamatujte: šířka/výška jsou **CSS pixely**, ne hardwarové pixely. |
| **Server stále posílá desktop CSS** | Některé stránky detekují zařízení pomocí JavaScriptu, ne jen hlavičky. | Zvažte také injekci meta tagu viewport, pokud je potřeba. |

Když budete mít tyto body na paměti, zřídka narazíte na situaci, kdy emulace nefunguje podle očekávání.

## Rozšíření sandboxu – další kroky

Nyní, když už víte **jak nastavit vlastní user agent** a **jak nastavit dpr**, můžete experimentovat dál:

- **Změňte velikost obrazovky** a emulujte tablety nebo větší telefony.  
- **Vyměňte user‑agent** a testujte Chrome na Androidu (`"Mozilla/5.0 (Linux; Android 12; ...) Chrome/110.0"`).  
- **Přidejte cookies nebo další hlavičky** pomocí metody sandboxu `setHeaders` pro testování s autentifikací.  
- **Pořiďte screenshot** pomocí `HTMLDocument.renderToFile("output.png")` a automaticky porovnávejte vizuální rozdíly.

Tyto rozšíření vám umožní vytvořit plnohodnotný testovací rámec, aniž byste opustili své IDE.

---

## Závěr

Probrali jsme **jak emulovat iPhone** pomocí `DocumentSandbox` z Aspose.HTML, ukázali vám přesně **jak nastavit vlastní user agent**, **jak nastavit device pixel ratio** a dokonce i jemné rozdíly mezi “**jak nastavit user-agent**” a “**jak nastavit dpr**”. Kompletní, spustitelný příklad demonstruje všechny části na jednom místě, takže můžete kopírovat, upravovat a okamžitě začít testovat mobilní rozvržení.  

Vyzkoušejte to — změňte rozměry obrazovky, pohrávejte si s různými user‑agenty a sledujte, jak vaše stránky reagují. Jakmile ovládnete tato nastavení, ladění responzivních designů bude hračkou a ušetříte nespočet hodin strávených hledáním chyb na reálných zařízeních.

Máte otázky nebo chcete sdílet vlastní variace? Zanechte komentář níže a šťastnou emulaci!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}