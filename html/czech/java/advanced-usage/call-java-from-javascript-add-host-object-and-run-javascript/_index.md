---
category: general
date: 2026-10-14
description: Volání java z javascriptu pomocí Aspose.HTML. Naučte se, jak přidat host
  objekt, spustit javascript v java a log z javascriptu v stručném tutoriálu.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Volání java z javascriptu pomocí Aspose.HTML. Tento průvodce ukazuje,
  jak přidat host objekt, spustit javascript v java a log z javascriptu, vše během
  několika řádků kódu.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Volání java z javascriptu – přidání host objektu a spuštění javascriptu
  v java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Volání java z javascriptu – přidání host objektu a spuštění javascriptu v java
url: /cs/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Volání Java z JavaScriptu – přidání host objektu a spuštění JavaScriptu v Javě

Už jste někdy potřebovali **call java from javascript** uvnitř Java aplikace? Možná vytváříte dynamický HTML reportovací engine nebo chcete jednoduše zpřístupnit Java logger skriptu, který ovládáte. V tomto tutoriálu uvidíte přesně, jak přidat host objekt, spustit JavaScript v Javě a dokonce **log from JavaScript** zpět do JVM — vše pomocí Aspose.HTML.

Provedeme kompletní, spustitelný příklad, který vytvoří prázdný HTML dokument, vloží Java třídu `Logger` jako host objekt, spustí malý skript a vypíše výsledek do konzole. Není potřeba žádný externí webový prohlížeč, žádná mystická „magie“ — jen čistý Java kód, který můžete dnes zkopírovat a spustit.

## Rychlé odpovědi
- **Jak přidám host objekt?** Zaregistrujte Java instanci pomocí `document.getWindow().addHostObject("name", object)`.  
- **Mohu spustit JavaScript v Javě?** Ano — použijte `document.getWindow().eval(yourScript)`.  
- **Je možné logovat z JavaScriptu?** Ano; host objekt může vystavit libovolnou metodu `void log(String)`.  
- **Jaká verze Aspose.HTML je vyžadována?** Verze 23.10 nebo novější podporuje kompletní host‑object API.  
- **Potřebuji webový prohlížeč?** Ne — Aspose.HTML poskytuje vestavěný engine, takže vše běží head‑less.

## Co je call java from javascript?
**Call java from javascript** je technika zpřístupnění Java objektů JavaScript runtime, aby skripty mohly přímo volat Java metody. Aspose.HTML vytváří lehký JavaScript engine uvnitř Java procesu, což umožňuje plynulou obousměrnou komunikaci bez externích prohlížečů.

## Proč použít Aspose.HTML pro spouštění javascriptu v Javě?
Aspose.HTML podporuje **více než 50 vstupních a výstupních formátů** a dokáže vyhodnocovat JavaScript v plně kompatibilním HTML5 prostředí. Zpracovává skripty v průměru do 200 ms pro jednoduchý jednorázový kód a to bez načítání kompletního prohlížečového stacku, což snižuje využití paměti až o 80 % ve srovnání s přístupy založenými na Seleniumu.

## Požadavky

- Java 17 (nebo jakýkoli recentní JDK) nainstalovaný a nakonfigurovaný.  
- Knihovna Aspose.HTML pro Java (verze 23.10 nebo novější). Můžete ji získat z Maven Central nebo z webu Aspose.  
- Jednoduché IDE nebo textový editor; příklad funguje také z příkazové řádky.

> **Tip:** Pokud používáte Maven, přidejte následující závislost do vašeho `pom.xml`:

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

Nyní, když máme základy vyřešené, pojďme se ponořit do krok‑za‑krokem řešení.

## Jak přidat host objekt a spustit javascript v Javě?
`addHostObject` zaregistruje Java objekt jako globální proměnnou v JavaScript kontextu. Načtěte svůj `HTMLDocument`, zaregistrujte Java logger pod názvem `"javaLogger"` pomocí `addHostObject` a poté vyhodnoťte krátký skript, který volá `javaLogger.log`. Celý tok vyžaduje pouze tři API volání a funguje v jakémkoli Java 17 runtime.

### Krok 1: vytvořte minimální java projekt

Nejprve vytvořte novou Java třídu s názvem `JsHostObjectDemo`. Třída bude obsahovat naši metodu `main` a definici host objektu. Udržení všeho v jednom souboru činí tutoriál samostatným a snadno kopírovatelným.

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

`HTMLDocument` představuje v‑paměti HTML dokument a poskytuje JavaScript engine. Třída `HTMLDocument` spouští plně HTML‑5 kompatibilní skriptovací prostředí. I když nikdy nenačítáme žádný markup, objekt `window` dokumentu nám dává přístup k JavaScript engine, kde se odehrává magie **run javascript in java**. Navíc můžete manipulovat s DOM, načítat zdroje nebo vyhodnocovat skripty bez prohlížeče.

## Jak přidat host objekt – “javaLogger”?
`Logger` je jednoduchá Java třída s metodou `log(String)`, která zapisuje zprávy do konzole. Zaregistrujte instanci `Logger` pod názvem `"javaLogger"`, aby jakýkoli skript vyhodnocený v tomto dokumentu mohl volat `javaLogger.log(...)`. Toto je jádro požadavku **add host object** a zpřístupňuje logger jako globální proměnnou pro JavaScript kód.

### Časté úskalí

- **Kolize názvů** – Pokud již ve vašem skriptu máte globální proměnnou nazvanou `javaLogger`, host objekt bude přepsán. Zvolte jedinečný název.  
- **Bezpečnost vláken** – Host objekt je sdílen napříč vykonáváním skriptů ve stejném dokumentu. Pokud plánujete spouštět skripty souběžně, udělejte třídu host thread‑safe (např. použijte `synchronized` nebo `java.util.concurrent` primitivy).

## Jak psát a spouštět javascript v Javě?
`eval` spouští JavaScript řetězec v skriptovacím engine dokumentu a vrací jakýkoli výsledek. Předáte malý skript do `eval`. Engine vyhledá `javaLogger` z globálního rozsahu a zavolá jeho metodu `log` s předaným řetězcem. Můžete také vracet hodnoty, zpracovávat výjimky a řetězit více vyhodnocení pro složitější interakce.

### Očekávaný výstup

```
[JS] Hello from JavaScript!
```

## Jak rozšířit host – více než jen logování?
Host objekt je libovolná Java instance zpřístupněná JavaScriptu pomocí `addHostObject`. Zpřístupněte další funkce přidáním metod do třídy `Logger` nebo vytvořením nové host třídy. Níže je rychlý příklad, který také vrací hodnotu do JavaScriptu. Host objekt může vystavit komplexní typy, provádět I/O nebo komunikovat s jinými službami. Vrácením hodnoty může skript získat data zpět, což umožňuje obousměrnou komunikaci mezi Javou a JavaScriptem.

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

Now the console shows:

```
[JS] 3+4=7
```

## Jak uvolnit zdroje po spuštění skriptů?
`dispose` uvolňuje nativní zdroje držené instancí `HTMLDocument`. Když skončíte s skriptovacím prostředím, uvolněte `HTMLDocument`, aby se uvolnily nativní zdroje. Nepozvání `dispose()` může vést k únikům paměti, zejména při vytváření mnoha dokumentů ve smyčkách nebo dlouho běžících službách. Vždy obalte použití do bloku try‑with‑resources nebo zajistěte, že `document.dispose()` je voláno ve finally bloku.

```java
document.dispose(); // Important for long‑running applications
```

## Kompletní funkční příklad

Níže je kompletní zdrojový soubor, který můžete okamžitě zkompilovat a spustit. Uložte jej jako `JsHostObjectDemo.java`, ujistěte se, že Aspose.HTML JAR je na vašem classpath, a spusťte `java JsHostObjectDemo`.

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

Running this program yields:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Často kladené otázky

**Q: Funguje to na Androidu?**  
A: Ano. Aspose.HTML je čistě Java knihovna, takže běží na jakémkoli JVM, včetně Android ART runtime.

**Q: Co když potřebuji předat komplexní objekty?**  
A: Můžete zpřístupnit POJO s gettery a settery; engine je automaticky mapuje na JavaScript objekty. Kolekce jako `java.util.List` nebo pole jsou také převoditelné.

**Q: Jak funguje zpracování chyb?**  
A: Pokud skript vyhodí JavaScript chybu, `eval` propaguje `ScriptException`. Zabalte volání do try‑catch bloku pro logování nebo zotavení.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: Můžu spouštět více skriptů sekvenčně?**  
A: Rozhodně. Stejný `HTMLDocument` si zachovává svůj globální rozsah, takže můžete volat `eval` opakovaně. Jen spravujte názvy proměnných, aby nedocházelo ke kolizím.

**Q: Je host objekt bezpečný pro nedůvěryhodné skripty?**  
A: Považujte jakýkoli externí skript za nedůvěryhodný vstup. Validujte parametry a zvažte sandboxování tím, že zpřístupníte jen minimální potřebné metody.

## Nejlepší postupy a tipy

- **Jasně pojmenujte své host objekty** — `javaLogger`, `javaUtils` atd. — aby nedocházelo ke zmatení.  
- **Udržujte host metody malé a bez vedlejších efektů**, pokud je to možné; usnadňuje to ladění.  
- **Uvolněte dokument** co nejdříve po dokončení; uvolní nativní paměť, kterou alokuje Aspose.HTML.  
- **Validujte vstupy** z JavaScriptu, zejména pokud skripty pocházejí z nedůvěryhodných zdrojů. Považujte je za jakákoli externí data.

## Závěr

Nyní máte solidní, end‑to‑end příklad, jak **call java from javascript** pomocí **přidání host objektu**, **spuštění javascriptu v Javě** a **logování z javascriptu** pomocí Aspose.HTML. Tento vzor je výkonný: jakákoli Java služba může být zpřístupněna skriptům, čímž se vaše Java aplikace promění v lehkou skriptovací platformu.

Dále můžete zkoumat:

- Vložení kompletní HTML stránky a manipulaci s DOM z JavaScriptu.  
- Použití host objektu pro streamování dat zpět do Java (např. JSON serializace).  
- Integraci s dalšími skriptovacími enginy jako Nashorn nebo GraalVM pro širší podporu jazyků.

Vyzkoušejte to, upravte třídy `Logger` nebo `Utils` a podívejte se, jak daleko můžete posunout koncept **javascript host object** ve svých projektech.

---

**Poslední aktualizace:** 2026-10-14  
**Testováno s:** Aspose.HTML for Java 23.10  
**Autor:** Aspose  

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Související tutoriály

- [Povolení spouštění skriptů v Javě – kompletní průvodce Aspose Html Guide](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Spuštění Javascriptu v Javě – kompletní průvodce spouštěním Js From](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [Jak sandboxovat Javascript – kompletní průvodce Aspose Html Guide](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}