---
category: general
date: 2026-03-14
description: Naučte se, jak volat Java z JavaScriptu pomocí Aspose.HTML. Tento průvodce
  ukazuje, jak přidat hostitelský objekt, spustit JavaScript v Javě a zaznamenávat
  z JavaScriptu.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: cs
og_description: Vyvolejte Java z JavaScriptu pomocí Aspose.HTML. Přidejte hostitelský
  objekt, spusťte JavaScript v Javě a zaznamenejte výstup z JavaScriptu v jednom tutoriálu.
og_title: Volání Javy z JavaScriptu – Kompletní průvodce s hostitelským objektem
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Volání Javy z JavaScriptu – Přidání host objektu a spuštění JavaScriptu v Javě
url: /cs/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

.

Start with shortcodes at top: keep as is.

Then heading "# Call Java from JavaScript – Add Host Object and Run JavaScript in Java" translate.

Probably "# Volání Java z JavaScriptu – Přidání host objektu a spuštění JavaScriptu v Javě"

Proceed.

Paragraphs.

We need to translate but keep technical terms in English.

Let's produce final markdown.

Be careful with blockquotes >.

Also lists.

Let's translate.

Will produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Volání Java z JavaScriptu – Přidání host objektu a spuštění JavaScriptu v Javě

Už jste někdy potřebovali **volat Java z JavaScriptu** uvnitř Java aplikace? Možná budujete dynamický HTML reportovací engine nebo chcete jednoduše zpřístupnit Java logger skriptu, který ovládáte. V tomto tutoriálu uvidíte přesně, jak přidat host objekt, spustit JavaScript v Javě a dokonce **logovat z JavaScriptu** zpět do JVM – vše s Aspose.HTML.

Projdeme kompletní, spustitelný příklad, který vytvoří prázdný HTML dokument, vloží Java třídu `Logger` jako host objekt, vykoná malý skript a vypíše výsledek do konzole. Žádný externí webový prohlížeč, žádná mystická „magie“ – jen čistý Java kód, který můžete dnes zkopírovat‑vložit a spustit.

## Požadavky

- Java 17 (nebo jakýkoli aktuální JDK) nainstalovaný a nastavený.
- Aspose.HTML pro Java knihovna (verze 23.10 nebo novější). Získáte ji z Maven Central nebo z webu Aspose.
- Jednoduché IDE nebo textový editor; příklad funguje i z příkazové řádky.

> **Tip:** Pokud používáte Maven, přidejte následující závislost do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Nebo pro Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Nyní, když máme základy připravené, pojďme na krok‑za‑krokem řešení.

## Krok 1: Vytvořte minimální Java projekt

Nejprve vytvořte novou Java třídu s názvem `JsHostObjectDemo`. Třída bude obsahovat naši metodu `main` i definici host objektu. Držení všeho v jednom souboru dělá tutoriál samostatným a snadno kopírovatelným.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Proč `HTMLDocument`?

Třída `HTMLDocument` z Aspose.HTML spouští plně kompatibilní HTML‑5 skriptovací prostředí. I když nikdy nenačítáme žádný markup, objekt `window` dokumentu nám poskytuje přístup k JavaScript enginu, kde se odehrává **run JavaScript in Java** magie.

## Krok 2: Přidejte host objekt – „javaLogger“

Řádek

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

provádí těžkou práci pro požadavek **add host object**. Registrací instance `Logger` pod jménem `"javaLogger"` může jakýkoli skript vyhodnocený v tomto dokumentu volat `javaLogger.log(...)`. To je jádro konceptu **javascript host object**: most, který umožňuje JavaScriptu přistupovat do JVM.

### Časté úskalí

- **Kolize názvů** – pokud už ve skriptu máte globální proměnnou `javaLogger`, host objekt bude přepsán. Zvolte jedinečný název.
- **Bezpečnost vláken** – host objekt je sdílený napříč vykonáváním skriptů ve stejném dokumentu. Pokud plánujete spouštět skripty souběžně, udělejte třídu thread‑safe (např. pomocí `synchronized` nebo primitiv `java.util.concurrent`).

## Krok 3: Napište a spusťte JavaScript

Skript, který předáváme do `eval`, je úmyslně malý:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Když se spustí `document.getWindow().eval(script)`, engine vyhledá `javaLogger` ve svém globálním prostoru, najde přidaný Java objekt a zavolá jeho metodu `log` s předaným řetězcem.

### Očekávaný výstup

Spuštění metody `main` vypíše následující řádek do konzole:

```
[JS] Hello from JavaScript!
```

Ten malý řádek dokazuje, že jsme úspěšně **call java from javascript**, a **log from javascript** se objeví přesně tam, kde by se normálně zobrazil Java `System.out` výstup.

## Krok 4: Rozšíření host objektu – víc než jen logování

Pokud potřebujete zpřístupnit další funkce (např. přístup k souborům, databázové dotazy), stačí přidat další metody do třídy `Logger` – nebo vytvořit zcela novou host třídu. Zde je rychlý příklad, který také vrací hodnotu:

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Nyní konzole ukazuje:

```
[JS] 3+4=7
```

To demonstruje flexibilitu vzoru **javascript host object**: můžete zpřístupnit libovolné Java API, pokud jsou datové typy převoditelné mezi Javou a JavaScriptem (primitivy, řetězce, pole atd.).

## Krok 5: Uvolnění prostředků

Až skončíte se skriptovacím prostředím, uvolněte `HTMLDocument`, aby se uvolnily nativní prostředky:

```java
document.dispose(); // Important for long‑running applications
```

Přeskočení uvolnění může vést k únikům paměti, zejména pokud vytváříte mnoho dokumentů v cyklu.

## Kompletní funkční příklad

Níže je celý zdrojový soubor, který můžete okamžitě zkompilovat a spustit. Uložte jej jako `JsHostObjectDemo.java`, ujistěte se, že je Aspose.HTML JAR na classpath, a spusťte `java JsHostObjectDemo`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

Spuštění tohoto programu vypíše:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

To je celý **call java from javascript** workflow v několika řádcích.

## Často kladené otázky

### Funguje to na Androidu?

Aspose.HTML je čistě Java knihovna, takže běží na jakémkoli JVM, včetně Android Dalvik/ART. Stačí přidat JAR a budete mít stejné schopnosti host objektu.

### Co když potřebuji předat složité objekty?

Můžete zpřístupnit POJO (plain old Java objects) s poli, gettery a settery. Engine je automaticky namapuje na JavaScript objekty. Pro kolekce použijte `java.util.List` nebo pole – obě jsou převoditelné.

### Jak funguje zpracování chyb?

Pokud skript vyvolá JavaScriptovou chybu, `eval` propaguje `ScriptException`. Obalte volání do try‑catch bloku a logujte nebo zotavujte se:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Můžu spouštět více skriptů sekvenčně?

Ano. Stejná instance `HTMLDocument` si zachovává globální scope, takže můžete volat `eval` opakovaně. Jen dávejte pozor na kolize názvů proměnných mezi skripty.

## Nejlepší postupy a tipy

- **Jasně pojmenujte host objekty** – `javaLogger`, `javaUtils` atd., aby nedocházelo ke zmatkům.
- **Udržujte host metody malé a bez vedlejších efektů**, pokud je to možné; usnadní to ladění.
- **Uvolněte dokument** hned, jak jen skončíte; uvolní to nativní paměť, kterou Aspose.HTML alokuje.
- **Validujte vstupy** z JavaScriptu, zejména pokud skripty pocházejí z nedůvěryhodných zdrojů. Zacházejte s nimi jako s jakýmikoli externími daty.

## Závěr

Nyní máte solidní, end‑to‑end příklad, jak **call java from javascript** pomocí **add host object**, **run JavaScript in Java** a **log from JavaScript** s využitím Aspose.HTML. Vzor je výkonný: jakákoli Java služba může být zpřístupněna skriptům, čímž se vaše Java aplikace promění v lehkou skriptovací platformu.

Dále můžete zkoumat:

- Vkládání kompletní HTML stránky a manipulaci s DOM z JavaScriptu.
- Použití host objektu k streamování dat zpět do Java (např. JSON serializace).
- Integraci s dalšími skriptovacími enginy jako Nashorn nebo GraalVM pro širší podporu jazyků.

Vyzkoušejte to, upravte třídy `Logger` nebo `Utils` a podívejte se, kam až můžete posunout koncept **javascript host object** ve svých projektech.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}