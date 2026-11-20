---
category: general
date: 2026-06-16
description: Naučte se, jak nastavit DPI zařízení v Aspose a nastavit šířku a výšku
  viewportu při renderování HTML pomocí Aspose.HTML sandboxu v Javě. Kód krok po kroku
  je zahrnut.
draft: false
keywords:
- set device dpi aspose
- set viewport width height
language: cs
og_description: Objevte, jak nastavit DPI zařízení v Aspose a nastavit šířku a výšku
  viewportu pomocí Aspose.HTML sandboxu pro Javu. Kompletní kód a vysvětlení.
og_title: Nastavení DPI zařízení Aspose v Javě – Kompletní průvodce Sandbox
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  headline: set device dpi aspose in Java – Complete Sandbox Guide
  type: TechArticle
- description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  name: set device dpi aspose in Java – Complete Sandbox Guide
  steps:
  - name: Configure sandbox options (including DPI and viewport size).
    text: Configure sandbox options (including DPI and viewport size).
  - name: Instantiate a `DocumentSandbox` with those options.
    text: Instantiate a `DocumentSandbox` with those options.
  - name: Load an external HTML page inside the sandbox.
    text: Load an external HTML page inside the sandbox.
  - name: Perform a simple DOM operation—printing the page title.
    text: Perform a simple DOM operation—printing the page title.
  type: HowTo
tags:
- Aspose.HTML
- Java
- HTML rendering
- Sandbox
title: Nastavit DPI zařízení Aspose v Javě – Kompletní průvodce sandboxem
url: /cs/java/advanced-usage/set-device-dpi-aspose-in-java-complete-sandbox-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device dpi aspose – Java Sandbox tutoriál

Už jste se někdy zamýšleli, jak **set device dpi aspose** při renderování webové stránky v Javě? Nejste v tom sami. Mnoho vývojářů narazí na problém, když potřebují, aby renderovaná stránka vypadala přesně tak, jako by byla na skutečné obrazovce – zejména když DPI ovlivňuje výpočty rozvržení.  

V tomto průvodci vás provedeme praktickým příkladem, který nejen **set device dpi aspose**, ale také ukazuje, jak **set viewport width height**, aby se stránka chovala přesně jako v okně prohlížeče o rozměrech 1280 × 800 pixelů. Na konci budete mít spustitelný úryvek, jasné vysvětlení každého kroku a tipy, jak se vyhnout běžným úskalím.

## Co tento tutoriál pokrývá

Nejprve shrneme předpoklady, poté se pustíme do čtyř stručných kroků:

1. Nakonfigurujte sandboxové možnosti (včetně DPI a velikosti viewportu).  
2. Vytvořte `DocumentSandbox` s těmito možnostmi.  
3. Načtěte externí HTML stránku uvnitř sandboxu.  
4. Proveďte jednoduchou DOM operaci – vytištění názvu stránky.

Uvidíte, proč je každá část důležitá, jak nastavit parametry pro různá zařízení a jaký by měl být výstup. Žádná externí dokumentace není potřeba; vše, co potřebujete, je zde.

## Předpoklady

- Java 8 nebo novější (knihovna Aspose.HTML for Java podporuje JDK 8+).  
- JAR soubory Aspose.HTML for Java přidané do classpath vašeho projektu.  
- IDE nebo nástroj pro sestavení (Maven/Gradle) pro kompilaci a spuštění kódu.  
- Přístup k internetu, pokud plánujete načíst živou URL jako `https://example.com`.

Pokud máte všechny tyto položky splněny, pojďme na to.

## Krok 1: Set device DPI aspose – Definice sandboxových možností

První věc, kterou musíte udělat, je říct sandboxu, jakou „obrazovku“ předstíráte. Zde vstupuje do hry **set device dpi aspose**. DPI (dots per inch) ovlivňuje, jak jsou interpretovány CSS jednotky `px`, což může změnit velikosti fontů, škálování obrázků a media queries.

```java
// Step 1: Create sandbox options and configure DPI and viewport.
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
sandboxOptions.setViewportWidth(1280);         // set viewport width height
sandboxOptions.setViewportHeight(800);         // set viewport width height
```

> **Proč je to důležité:**  
> *Volání `setDeviceDpi` říká Aspose.HTML, aby považoval jeden CSS pixel za 1/96 palce, což odpovídá většině desktopových monitorů. Pokud toto vynecháte, rozvržení může na obrazovkách s vysokým DPI vypadat příliš malé nebo příliš velké.*

## Krok 2: Vytvořte sandbox s nakonfigurovanými možnostmi

Jakmile jsou možnosti připravené, potřebujete instanci sandboxu, která je bude respektovat. Představte si sandbox jako malý, izolovaný prohlížečový engine, který se nedotkne vašeho souborového systému.

```java
// Step 2: Initialise the DocumentSandbox using the options above.
DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);
```

> **Pro tip:**  
> Opakované používání stejného `DocumentSandbox` pro více stránek šetří paměť, ale nezapomeňte resetovat možnosti, pokud později potřebujete jiné DPI nebo viewport.

## Krok 3: Načtěte HTML dokument uvnitř sandboxu

S připraveným sandboxem je načtení stránky jednoduché. Konstruktor `HTMLDocument` přijímá URL a sandbox, který jste právě vytvořili.

```java
// Step 3: Load a remote HTML page using the sandbox.
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);
```

> **Hraniční případ:**  
> Pokud cílový web blokuje automatizované požadavky, můžete získat chybu 403. V takovém případě buď stáhněte HTML lokálně a načtěte jej ze souborové cesty, nebo nastavte vlastní řetězec user‑agent pomocí `sandboxOptions`.

## Krok 4: Proveďte běžné DOM operace – vytiskněte název stránky

V tomto okamžiku je stránka plně renderována uvnitř sandboxu, takže jakýkoli DOM dotaz funguje přesně jako v plnohodnotném prohlížeči. Uděláme to jednoduše a získáme titulek.

```java
// Step 4: Access the DOM – print the page title.
System.out.println("Title: " + htmlDoc.getTitle());
```

**Očekávaný výstup**

```
Title: Example Domain
```

Pokud vidíte něco jiného, zkontrolujte, zda je URL dostupná a zda jste náhodou nezměnili hodnoty DPI nebo viewportu.

## Proč je nastavení Viewport Width Height zásadní

Možná se ptáte: „Proč vůbec **set viewport width height**?“ Odpověď spočívá v responzivním designu. Media queries jako `@media (max-width: 600px)` reagují na rozměry viewportu, nikoli na fyzickou velikost obrazovky. Zadáním `1280` × `800` zajistíte, že stránka vykreslí „desktopové“ rozvržení, i když kód běží na headless serveru bez displeje.

```java
sandboxOptions.setViewportWidth(1280);   // set viewport width height
sandboxOptions.setViewportHeight(800);   // set viewport width height
```

Změnou těchto čísel můžete simulovat tablety, telefony nebo dokonce ultra‑široké monitory, aniž byste opustili IDE.

## Kompletní funkční příklad

Níže je kompletní, připravená Java třída, která spojuje všechny kroky. Zkopírujte ji do souboru pojmenovaného `SandboxExample.java`, přidejte JAR soubory Aspose.HTML do classpath a spusťte `javac SandboxExample.java && java SandboxExample`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) {
        // Step 1: Define sandbox options – set device DPI and viewport.
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
        sandboxOptions.setViewportWidth(1280);         // set viewport width height
        sandboxOptions.setViewportHeight(800);         // set viewport width height

        // Step 2: Create a DocumentSandbox using the defined options.
        DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);

        // Step 3: Load an HTML document inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 4: Perform normal DOM operations – print the page title.
        System.out.println("Title: " + htmlDoc.getTitle());
    }
}
```

> **Rychlé ověření:**  
> Spusťte program. Pokud uvidíte `Title: Example Domain`, vše je nastaveno správně. Pokud ne, podívejte se do konzole na výjimky – většina problémů pramení z chybějících JAR souborů nebo síťových omezení.

## Časté úskalí a jak se jim vyhnout

| Příznak | Pravděpodobná příčina | Oprava |
|---|---|---|
| `NullPointerException` při `htmlDoc.getTitle()` | Sandbox se nepodařilo načíst stránku | Ověřte URL, přidejte try‑catch kolem konstruktoru `HTMLDocument`, nebo povolte logování pomocí `sandboxOptions.setLogLevel(...)`. |
| Rozvržení vypadá přiblížené/oddálené | DPI není nastaveno správně | Ujistěte se, že `sandboxOptions.setDeviceDpi(96)` (nebo vaše cílové DPI). |
| Media queries se nikdy nespouští | Chybí rozměry viewportu | Zkontrolujte, že jste zavolali jak `setViewportWidth`, **tak** `setViewportHeight`. |
| Chyba nedostatku paměti při velkých stránkách | Opakované používání jednoho sandboxu pro mnoho těžkých stránek | Vytvořte nový `DocumentSandbox` pro každou stránku nebo po použití zavolejte `documentSandbox.dispose()`. |

## Rozšíření příkladu

Nyní, když umíte **set device dpi aspose** a **set viewport width height**, můžete experimentovat dál:

- **Pořídit screenshot** renderované stránky pomocí `htmlDoc.renderToBitmap(...)`.  
- **Vložit vlastní CSS** před renderováním a otestovat témata pro tmavý režim.  
- **Spustit JavaScript** uvnitř sandboxu pomocí `htmlDoc.getWindow().eval(...)`.  

Všechny tyto akce respektují nastavené DPI a viewport, což vám poskytuje spolehlivé testovací prostředí pro responzivní rozvržení.

## Závěr

Prošli jsme stručným, end‑to‑end řešením, které ukazuje, jak **set device dpi aspose** a **set viewport width height** pomocí sandboxu Aspose.HTML v Javě. Nyní máte pevný základ pro renderování stránek přesně tak, jak by se zobrazily na libovolném zařízení, a to vše v bezpečném, izolovaném prostředí.

Jste připraveni na další krok? Zkuste renderovat stránku využívající CSS grid layout, nebo načtěte vzdálený stylesheet a podívejte se, jak DPI ovlivňuje vykreslování fontů. Sandbox vám dává svobodu experimentovat, aniž byste ovlivnili hostitelský systém.

Pokud narazíte na potíže, zanechte komentář níže nebo se podívejte do dokumentace Aspose.HTML for Java – všechno, co potřebujete, je už zde. Šťastné kódování!  

![set device dpi aspose sandbox diagram](https://example.com/images/set-device-dpi-aspose.png "Diagram showing DPI and viewport configuration in Aspose.HTML sandbox")

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Create PDF from HTML using Aspose.HTML for Java – Sandbox](/html/english/java/configuring-environment/implement-sandboxing/)
- [Create PDF from HTML – Set User Style Sheet in Aspose.HTML for Java](/html/english/java/configuring-environment/set-user-style-sheet/)
- [How to Set Charset in Aspose.HTML for Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}