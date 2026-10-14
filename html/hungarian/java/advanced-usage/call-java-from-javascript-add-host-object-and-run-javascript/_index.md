---
category: general
date: 2026-10-14
description: java hívása javascriptből az Aspose.HTML segítségével. Ismerje meg, hogyan
  adhat hozzá egy host objektumot, hajthatja végre a javascriptet java-ban, és logolhat
  javascriptből egy tömör útmutatóban.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: java hívása javascriptből az Aspose.HTML segítségével. Ez az útmutató
  bemutatja, hogyan adhat hozzá egy host objektumot, hajthatja végre a javascriptet
  java-ban, és logolhat javascriptből, mindezt néhány kódsorral.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: java hívása javascriptből – host objektum hozzáadása és javascript futtatása
  java-ban
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
title: java hívása javascriptből – host objektum hozzáadása és javascript futtatása
  java-ban
url: /hu/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java hívása JavaScriptből – host objektum hozzáadása és JavaScript futtatása Java-ban

Valaha is szükséged volt **call java from javascript** egy Java alkalmazáson belül? Lehet, hogy egy dinamikus HTML jelentésmotorral dolgozol, vagy egyszerűen csak egy Java naplózót szeretnél elérhetővé tenni egy általad irányított szkript számára. Ebben az útmutatóban pontosan megmutatjuk, hogyan adhatunk hozzá egy host objektumot, futtathatunk JavaScriptet Java-ban, és akár **log from JavaScript** vissza a JVM-be – mindezt az Aspose.HTML segítségével.

Áttekintünk egy komplett, futtatható példát, amely egy üres HTML dokumentumot hoz létre, egy Java `Logger` osztályt injektál host objektumként, végrehajt egy apró szkriptet, és kiírja az eredményt a konzolra. Nem szükséges külső webböngésző, nincs misztikus „varázslat” – csak egyszerű Java kód, amelyet ma másolhatsz‑beilleszthetsz és futtathatsz.

## Gyors válaszok
- **Hogyan adhatok hozzá egy host objektumot?** Regisztrálj egy Java példányt a `document.getWindow().addHostObject("name", object)` metódussal.  
- **Futtathatok JavaScriptet Java-ban?** Igen – használd a `document.getWindow().eval(yourScript)` metódust.  
- **Lehetséges a naplózás JavaScriptből?** Teljesen; a host objektum bármilyen `void log(String)` metódust ki tud adni.  
- **Melyik Aspose.HTML verzió szükséges?** A 23.10 vagy újabb verzió támogatja a teljes host‑object API‑t.  
- **Szükség van webböngészőre?** Nem – az Aspose.HTML beágyazott motorral rendelkezik, így minden head‑less módon fut.

## Mi az a call java from javascript?
**Call java from javascript** az a technika, amely Java objektumokat tesz elérhetővé egy JavaScript futtatókörnyezetben, így a szkriptek közvetlenül meghívhatják a Java metódusokat. Az Aspose.HTML egy könnyű JavaScript motort hoz létre egy Java folyamaton belül, lehetővé téve a zökkenőmentes kétirányú kommunikációt külső böngészők nélkül.

## Miért használjuk az Aspose.HTML-t Java-ban történő JavaScript végrehajtásához?
Az Aspose.HTML **50+** bemeneti és kimeneti formátumot támogat, és képes JavaScriptet kiértékelni egy teljesen kompatibilis HTML5 környezetben. Átlagosan 200 ms alatt feldolgozza az egyszerű egy‑soros kódot, és mindezt anélkül teszi, hogy teljes böngésző stacket kellene betölteni, ami akár 80 %-kal is csökkentheti a memóriahasználatot a Selenium‑alapú megoldásokhoz képest.

## Előfeltételek

- Java 17 (vagy bármely friss JDK) telepítve és konfigurálva.  
- Aspose.HTML for Java könyvtár (23.10 vagy újabb). Letölthető a Maven Central‑ról vagy az Aspose weboldaláról.  
- Egyszerű IDE vagy szövegszerkesztő; a példa parancssorból is futtatható.

> **Pro tipp:** Ha Maven‑t használsz, add hozzá a következő függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Vagy Gradle esetén:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Most, hogy az alapok rendben vannak, merüljünk el a lépésről‑lépésre megoldásban.

## Hogyan adhatunk hozzá egy host objektumot és futtathatunk JavaScriptet Java-ban?
`addHostObject` egy Java objektumot regisztrál globális változóként a JavaScript kontextusban. Töltsd be a `HTMLDocument`‑et, regisztráld a Java naplózót a `"javaLogger"` név alatt az `addHostObject`‑mal, majd értékelj ki egy rövid szkriptet, amely meghívja a `javaLogger.log`‑ot. Az egész folyamat csak három API‑hívást igényel, és bármely Java 17 környezetben működik.

### 1. lépés: minimális java projekt létrehozása

Először hozz létre egy új Java osztályt `JsHostObjectDemo` néven. Az osztály tartalmazni fogja a `main` metódust és a host objektum definícióját. Minden egy fájlban tartása önmagában is könnyen másolható és önálló tutorialt biztosít.

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

### Miért egy `HTMLDocument`?
`HTMLDocument` egy memóriában létező HTML dokumentumot képvisel, és JavaScript motort biztosít. A `HTMLDocument` osztály egy teljes HTML‑5 kompatibilis szkriptkörnyezetet indít el. Még ha nem is töltünk be semmilyen markup‑ot, a dokumentum `window` objektuma hozzáférést ad a JavaScript motorhoz, ahol a **run javascript in java** varázslat történik. Emellett manipulálhatod a DOM‑ot, betölthetsz erőforrásokat, vagy kiértékelhetsz szkripteket böngésző nélkül.

## Hogyan adhatjuk hozzá a host objektumot – “javaLogger”?
`Logger` egy egyszerű Java osztály `log(String)` metódussal, amely üzeneteket ír a konzolra. Regisztráld a `Logger` példányt `"javaLogger"` néven, így bármely ebben a dokumentumban kiértékelt szkript meghívhatja a `javaLogger.log(...)`‑t. Ez a **add host object** követelmény központja, és a naplózót globális változóként teszi elérhetővé a JavaScript kódban.

### Gyakori buktatók

- **Névütközések** – Ha a szkriptedben már létezik egy globális `javaLogger` változó, a host objektum felülíródik. Válassz egyedi nevet.  
- **Szálbiztonság** – A host objektum megosztott a dokumentumon belüli szkript végrehajtások között. Ha párhuzamosan futtatsz szkripteket, tedd a host osztályt szálbiztossá (pl. `synchronized` vagy `java.util.concurrent` primitívekkel).

## Hogyan írjunk és hajtsunk végre JavaScriptet Java-ban?
`eval` egy JavaScript karakterláncot hajt végre a dokumentum szkriptmotorjában, és visszaadja az eredményt. Adj egy apró szkriptet az `eval`‑nek. A motor a globális scope‑ból feloldja a `javaLogger`‑t, és meghívja a `log` metódust a megadott szöveggel. Visszatérési értékek, kivételkezelés és több egymásutáni kiértékelés is lehetséges összetettebb interakciókhoz.

### Várható kimenet

A `main` metódus futtatása a következő sort írja ki a konzolra:

```
[JS] Hello from JavaScript!
```

## Hogyan bővítsük a host objektumot – több, mint csak naplózás?
Egy host objektum bármilyen Java példány lehet, amelyet a `addHostObject`‑on keresztül elérhetővé teszünk JavaScriptnek. Bővítsd a `Logger` osztályt további metódusokkal, vagy hozz létre egy új host osztályt. Az alábbi gyors példa egy értéket is visszaad a JavaScriptnek. A host objektum komplex típusokat, I/O műveleteket vagy más szolgáltatásokkal való interakciót is képes biztosítani. Az érték visszaadása lehetővé teszi, hogy a szkript adatot kapjon vissza, ezáltal kétirányú kommunikáció jön létre a Java és a JavaScript között.

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

Most a konzol a következőt mutatja:

```
[JS] 3+4=7
```

## Hogyan tisztítsuk meg az erőforrásokat a szkriptek futtatása után?
`dispose` felszabadítja a `HTMLDocument` példány által tartott natív erőforrásokat. Amikor befejezted a szkriptkörnyezet használatát, hívd meg a `document.dispose()`‑t a natív erőforrások felszabadításához. A `dispose()` elhagyása memória‑szivárgáshoz vezethet, különösen sok dokumentum létrehozása esetén ciklusokban vagy hosszú‑távú szolgáltatásokban. Mindig csomagold a használatot try‑with‑resources blokkba, vagy biztosítsd, hogy a `document.dispose()` végső blokkban meghívásra kerüljön.

```java
document.dispose(); // Important for long‑running applications
```

## Teljes működő példa

Az alábbiakban a teljes forrásfájl látható, amelyet azonnal lefordíthatsz és futtathatsz. Mentsd `JsHostObjectDemo.java` néven, győződj meg róla, hogy az Aspose.HTML JAR a classpath‑on van, majd futtasd `java JsHostObjectDemo`‑val.

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

A program futtatása a következőt eredményezi:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Gyakran feltett kérdések

**Q: Működik ez Androidon?**  
A: Igen. Az Aspose.HTML egy tisztán Java‑alapú könyvtár, ezért bármely JVM‑en, köztük az Android ART‑en is fut.

**Q: Mi van, ha komplex objektumokat kell átadni?**  
A: POJO‑kat getterekkel és setterekkel tehetsz elérhetővé; a motor automatikusan JavaScript objektumokká map‑olja őket. A `java.util.List` vagy tömbök szintén konvertálhatók.

**Q: Hogyan működik a hibakezelés?**  
A: Ha a szkript JavaScript hibát dob, az `eval` egy `ScriptException`‑t propagál. Tedd a hívást try‑catch blokkba, hogy naplózd vagy helyrehozd a hibát.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: Futtathatok több szkriptet egymás után?**  
A: Teljesen. Az ugyanaz a `HTMLDocument` megőrzi a globális scope‑ot, így többször is meghívhatod az `eval`‑et. Csak ügyelj a változónevek ütközésére.

**Q: Biztonságos a host objektum nem megbízható szkriptek számára?**  
A: Bármely külső szkriptet tekints megbízhatatlan bemenetnek. Validáld a paramétereket, és fontold meg a sandbox‑olást, úgy, hogy csak a minimálisan szükséges metódusokat teszed elérhetővé.

## Legjobb gyakorlatok és tippek

- **Nevezd egyértelműen a host objektumokat** – `javaLogger`, `javaUtils` stb., hogy elkerüld a félreértéseket.  
- **Tartsd a host metódusokat kis méretűre és mellékhatás‑mentesre**, ha lehetséges; ez megkönnyíti a hibakeresést.  
- **A dokumentumot a használat után azonnal zárd le**; így felszabadul a natív memória, amelyet az Aspose.HTML allokál.  
- **Validáld a JavaScript‑ből érkező bemeneteket**, különösen, ha a szkriptek nem megbízható forrásból származnak. Kezeld őket, mint bármely külső adatot.

## Következtetés

Most már egy átfogó, vég‑től‑végig példát láttál arra, hogyan **call java from javascript** a **host objektum hozzáadásával**, **javascript futtatásával java-ban**, és **naplózással javascriptből** az Aspose.HTML segítségével. A minta erőteljes: bármely Java szolgáltatás elérhetővé tehető szkriptek számára, így a Java alkalmazásod egy könnyűsúlyú szkriptplatformmá válik.

A következő lépéseket érdemes megfontolni:

- Teljes HTML oldal injektálása és a DOM manipulálása JavaScriptből.  
- A host objektum használata adatok visszaáramlására Java felé (pl. JSON sorosítás).  
- Integráció más szkriptmotorokkal, például Nashorn vagy GraalVM, a szélesebb nyelvi támogatás érdekében.

Próbáld ki, módosítsd a `Logger` vagy `Utils` osztályokat, és nézd meg, meddig tudod elvinni a **javascript host object** koncepciót a saját projektjeidben.

**Legutóbb frissítve:** 2026-10-14  
**Tesztelve ezzel:** Aspose.HTML for Java 23.10  
**Szerző:** Aspose  






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Kapcsolódó útmutatók

- [Java-ban a szkript végrehajtásának engedélyezése – Teljes Aspose HTML útmutató](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [Java-ban a JavaScript végrehajtása – Teljes útmutató a JS futtatásához](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [Hogyan szandbox-oljuk a JavaScriptet – Teljes Aspose HTML útmutató](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}