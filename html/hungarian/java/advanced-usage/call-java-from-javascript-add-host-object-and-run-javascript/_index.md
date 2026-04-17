---
category: general
date: 2026-03-14
description: Tanulja meg, hogyan hívhat Java-t JavaScript-ből az Aspose.HTML használatával.
  Ez az útmutató megmutatja, hogyan adjon hozzá host objektumot, futtasson JavaScript-et
  Java-ban, és hogyan naplózzon JavaScript-ből.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: hu
og_description: Hívjon Java-t JavaScript-ből az Aspose.HTML segítségével. Adjon hozzá
  host objektumot, futtassa a JavaScriptet Java-ban, és naplózzon JavaScriptből egyetlen
  útmutatóban.
og_title: Java hívása JavaScriptből – Teljes útmutató a host objektummal
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Java hívása JavaScriptből – Host objektum hozzáadása és JavaScript futtatása
  Java‑ban
url: /hu/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java hívása JavaScript‑ből – Host objektum hozzáadása és JavaScript futtatása Java‑ban

Szükséged volt már **Java hívására JavaScript‑ből** egy Java alkalmazáson belül? Lehet, hogy egy dinamikus HTML jelentésgenerátort építesz, vagy egyszerűen csak egy Java naplózót szeretnél elérhetővé tenni egy általad irányított szkript számára. Ebben az útmutatóban pontosan megmutatjuk, hogyan adjunk hozzá egy host objektumot, hogyan futtassunk JavaScript‑et Java‑ban, és még **naplózhassunk JavaScript‑ből** vissza a JVM‑be – mindezt az Aspose.HTML segítségével.

Lépésről‑lépésre végigvezetünk egy teljes, futtatható példán, amely létrehoz egy üres HTML dokumentumot, beilleszti a Java `Logger` osztályt host objektumként, végrehajt egy apró szkriptet, és kiírja az eredményt a konzolra. Nincs szükség külső webböngészőre, nincs semmi „varázslat” – csak egyszerű Java kód, amit ma másolhatsz‑beilleszthetsz és futtathatsz.

## Előfeltételek

- Java 17 (vagy bármely friss JDK) telepítve és beállítva.
- Aspose.HTML for Java könyvtár (23.10 vagy újabb verzió). Letölthető a Maven Central‑ról vagy az Aspose weboldaláról.
- Egyszerű IDE vagy szövegszerkesztő; a példa parancssorból is futtatható.

> **Pro tipp:** Ha Maven‑t használsz, add hozzá a következő függőséget a `pom.xml`‑hez:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Vagy Gradle‑hez:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Miután az alapok rendben vannak, vágjunk bele a lépés‑ről‑lépésre megoldásba.

## 1. lépés: Minimális Java projekt létrehozása

Először hozz létre egy új Java osztályt `JsHostObjectDemo` néven. Az osztály tartalmazni fogja a `main` metódust és a host objektum definícióját. Minden egy fájlban tartása önállóvá és könnyen másolhatóvá teszi az útmutatót.

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

### Miért `HTMLDocument`?

Az Aspose.HTML `HTMLDocument` osztályja egy teljes HTML‑5 kompatibilis szkriptkörnyezetet indít el. Bár nem töltünk be semmilyen markup‑ot, a dokumentum `window` objektuma hozzáférést biztosít a JavaScript motorhoz, ahol a **run JavaScript in Java** varázslat történik.

## 2. lépés: Host objektum hozzáadása – „javaLogger”

A következő sor

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

végzi a nehéz munkát a **add host object** követelményhez. A `Logger` példányt a `"javaLogger"` név alatt regisztrálva bármely, ebben a dokumentumban kiértékelt szkript meghívhatja a `javaLogger.log(...)` metódust. Ez a **javascript host object** koncepciója: egy híd, amely lehetővé teszi, hogy a JavaScript a JVM‑be hatoljon.

### Gyakori hibák

- **Névg collision** – Ha a szkriptedben már létezik egy globális változó `javaLogger` néven, a host objektum felül lesz írva. Válassz egyedi nevet.
- **Szálbiztonság** – A host objektum a dokumentumon belül megosztott a szkript‑végrehajtások között. Ha párhuzamosan szeretnél szkripteket futtatni, tedd a host osztályt szálbiztossá (pl. `synchronized` vagy `java.util.concurrent` primitívekkel).

## 3. lépés: JavaScript írása és végrehajtása

A `eval`‑nek átadott szkript szándékosan apró:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Amikor a `document.getWindow().eval(script)` lefut, a motor a globális környezetben megkeresi a `javaLogger`‑t, megtalálja a hozzáadott Java objektumot, és meghívja a `log` metódust a megadott szöveggel.

### Várt kimenet

A `main` metódus futtatása a konzolra a következő sort írja:

```
[JS] Hello from JavaScript!
```

Ez az apró sor bizonyítja, hogy sikeresen **call java from javascript**, és a **log from javascript** ott jelenik meg, ahol egy normál Java `System.out` üzenet lenne.

## 4. lépés: Host kibővítése – Több, mint csak naplózás

Ha további funkcionalitást (pl. fájlhozzáférés, adatbázis‑lekérdezések) szeretnél elérhetővé tenni, egyszerűen adj hozzá új metódusokat a `Logger` osztályhoz – vagy hozz létre egy teljesen új host osztályt. Íme egy gyors példa, amely értéket is visszaad:

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

Ez bemutatja a **javascript host object** minta rugalmasságát: bármilyen Java API‑t kiexponálhatsz, amíg a típusok konvertálhatóak Java és JavaScript között (primitívek, stringek, tömbök stb.).

## 5. lépés: Erőforrások felszabadítása

Amikor befejezted a szkriptkörnyezetet, zárd le a `HTMLDocument`‑et a natív erőforrások felszabadításához:

```java
document.dispose(); // Important for long‑running applications
```

A lezárás kihagyása memória‑szivárgáshoz vezethet, különösen ha sok dokumentumot hozol létre egy ciklusban.

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

A program futtatása a következő kimenetet adja:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

Ez a teljes **call java from javascript** munkafolyamat néhány sorban.

## Gyakran ismételt kérdések

### Működik ez Androidon?

Az Aspose.HTML egy tisztán Java könyvtár, ezért bármely JVM‑en fut, beleértve az Android Dalvik/ART környezetet is. Csak csatold a JAR‑t, és ugyanazok a host‑object képességek állnak rendelkezésre.

### Mit tehetek, ha összetett objektumokat kell átadni?

Kiexponálhatsz POJO‑kat (plain old Java objects), amelyek mezőket, gettereket és settereket tartalmaznak. A motor automatikusan leképezi őket JavaScript objektumokká. Gyűjteményekhez használj `java.util.List`‑et vagy tömböket – mindkettő konvertálható.

### Hogyan működik a hibakezelés?

Ha a szkript JavaScript hibát dob, az `eval` egy `ScriptException`‑t propagál. Tedd a hívást try‑catch blokkba, hogy naplózhass vagy helyreállíthass:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Futtathatok több szkriptet egymás után?

Természetesen. Az ugyanazon `HTMLDocument` példány megtartja a globális környezetet, így többször is meghívhatod az `eval`‑et. Csak ügyelj a változó‑ütközésekre a szkriptek között.

## Legjobb gyakorlatok és tippek

- **Adj egyértelmű neveket a host objektumoknak** – `javaLogger`, `javaUtils` stb. – a félreértések elkerülése érdekében.
- **Tartsd a host metódusokat kis méretűre és mellékhatás‑mentesre**, ha lehetséges; ez megkönnyíti a hibakeresést.
- **Zárd le a dokumentumot**, amint befejezted; ez felszabadítja az Aspose.HTML által lefoglalt natív memóriát.
- **Érvényesítsd a JavaScript‑ből érkező bemeneteket**, különösen ha a szkriptek nem megbízható forrásból származnak. Kezeld őket, mint bármely külső adatot.

## Összegzés

Most már van egy szilárd, vég‑től‑végig példád arra, hogyan **call java from javascript** a **host objektum hozzáadásával**, a **JavaScript futtatásával Java‑ban**, és a **naplózással JavaScript‑ből** az Aspose.HTML segítségével. A minta erőteljes: bármely Java szolgáltatást kiexponálhatsz a szkripteknek, így a Java alkalmazásod egy könnyű súlyú szkriptplatformmá válik.

A következő lépések lehetnek:

- Teljes HTML oldal injektálása és a DOM manipulálása JavaScript‑ből.
- Host objektum használata adatok visszaadására a Java oldalra (pl. JSON szerializáció).
- Integráció más szkriptmotorokkal, mint a Nashorn vagy a GraalVM, a nyelvi támogatás bővítéséhez.

Próbáld ki, módosítsd a `Logger` vagy `Utils` osztályokat, és nézd meg, meddig tudod elvinni a **javascript host object** koncepciót a saját projektjeidben.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}