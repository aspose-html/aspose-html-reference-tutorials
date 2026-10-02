---
category: general
date: 2026-03-04
description: Hívj Java-t JavaScript-ből az Aspose.HTML használatával, futtass aszinkron
  JavaScript-et, és tölts le JSON-t Java-ban egy egyszerű példával. Tanulj meg hatékonyan
  végrehajtani a JavaScript motorját.
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: hu
og_description: Hívj Java-t JavaScript-ből az Aspose.HTML segítségével, futtass aszinkron
  JavaScript-et, és tölts le JSON-t Java-ban. Teljes kód, magyarázatok és tippek benne.
og_title: Java hívása JavaScriptből – Lépésről‑lépésre aszinkron fetch bemutató
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: Java hívása JavaScriptből – Teljes útmutató az aszinkron fetch-hez és a JS
  motor végrehajtásához
url: /hu/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java hívása JavaScriptből – Teljes útmutató az aszinkron Fetch API-val

Valaha is elgondolkodtál már azon, hogyan **call Java from JavaScript** anélkül, hogy elhagynád a Java alkalmazásodat? Lehet, hogy egy szerver‑oldali HTML renderert építesz, vagy Java logikát kell elérhetővé tenned egy dokumentumban futó szkript számára. A jó hír, hogy az Aspose.HTML ezt gyerekjátékra változtatja. Ebben az útmutatóban nem csak azt mutatjuk meg, hogyan *run async JavaScript*-t futtathatsz egy Java‑alapú dokumentumban, hanem azt is, hogyan **fetch JSON in Java** a modern **asynchronous fetch API** használatával, és végül hogyan **execute JavaScript engine** hívásokat végezhetsz biztonságosan.

## Mit fogsz megtanulni

- Hogyan hozzunk létre egy üres HTML dokumentumot az Aspose.HTML segítségével.
- Hogyan szerezzük meg és **execute JavaScript engine**-t Java‑ból.
- Hogyan regisztráljunk egy Java host objektumot, amelyet a JavaScript meghívhat.
- Hogyan írjunk egy **asynchronous JavaScript** függvényt, amely a **asynchronous fetch API**‑t használja.
- Hogyan kezeljük a lekért adatot vissza Java‑ban egy tiszta callback‑kel.
- Várt kimenet és hibaelhárítási tippek.

### Előfeltételek

- Java 17 vagy újabb (a kód JDK 11‑kel is lefordítható).
- Aspose.HTML for Java 23.7 (vagy a legfrissebb verzió a cikk írásakor).
- Alapvető ismeretek a Java‑ról és a JavaScript promise‑okról.
- Internetkapcsolat a `jsonplaceholder` demó kéréshez.

Ha bármelyik ismeretlennek tűnik, ne aggódj – minden lépést egyszerű angol nyelven magyarázunk, és pontosan látni fogod, miért csinálunk úgy, ahogy csináljuk.

---

## 1. lépés – Üres HTML dokumentum létrehozása és a JavaScript Engine lekérése

Az első dolog, amire szükségünk van, egy üres dokumentum, amely egy elszigetelt JavaScript környezetet biztosít. Az Aspose.HTML `Document` osztályja pontosan ezt teszi.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**Why this matters:** A `Document` objektum egy böngészőablakot utánoz, és a `JavaScriptEngine` lehetővé teszi, hogy szkripteket futtassunk úgy, ahogy egy böngésző tenné. Ez a **call java from javascript** alapja – a motor a híd szerepét tölti be.

---

## 2. lépés – Host objektum regisztrálása, hogy a JavaScript visszahívhassa a Java‑t

Az Aspose.HTML lehetővé teszi, hogy bármely Java objektumot kitettsünk a szkriptvilágnak. Létrehozunk egy anonim osztályt egyetlen `onResult` metódussal, amely egyszerűen kiírja a kapott JSON‑t.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**Explanation:**  
- `addHostObject` a `javaCallback` nevet köti az anonim Java objektumhoz.  
- A JavaScript‑ben a `javaCallback.onResult(...)` hívást fogjuk használni.  
- Ez a **call java from javascript** központja – a szkript beavatkozik a Java oldalba, és a Java reagál.

> **Pro tip:** Tartsd a host objektum metódusait `public`‑on és egyszerűen; a komplex objektumok sorosítási problémákat okozhatnak.

---

## 3. lépés – Aszinkron JavaScript függvény írása az Aszinkron Fetch API használatával

Most jön a szórakoztató rész: egy apró szkript, amely JSON‑t kér le egy távoli végpontról. Az `async/await`-et használjuk, ami a modern módja a **run async JavaScript**‑nek.

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**Why we choose `fetch` over older XHR:**  
- A `fetch` egy `Promise`‑t ad vissza, ami tisztább kódot eredményez.  
- Natívan működik az `await`‑tal, így a folyamat felülről‑lefelé olvasható – tökéletes **asynchronous fetch api** bemutatókhoz.  
- Az API jövőbiztos; a legtöbb böngésző és motor (beleértve az Aspose‑t is) alapból támogatja.

---

## 4. lépés – A szkript futtatása a Dokumentum JavaScript Engine‑jében

Végül átadjuk a szkriptet a motornak. A motor felállít egy kis eseményhurkot, feloldja a `fetch` promise‑t, és a befejezéskor visszahívja a Java‑t.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

Amikor futtatod az `AsyncJsTutorial` osztályt, valami ilyesmit kell látnod:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Ez a kimenet három dolgot erősít meg:

1. Az **asynchronous fetch API** sikeresen lekérte az adatot.  
2. A JSON sorosítva lett és átadva a Java‑nak.  
3. A **execute javascript engine** hívás befejeződött deadlock nélkül.

---

## 5. lépés – Hibakezelés és szélsőséges esetek (opcionális fejlesztések)

A valós kód ritkán fut hibátlanul minden alkalommal. Az alábbiakban néhány gyakori buktatót és a védekezés módját mutatjuk be.

### 5.1 Hálózati hibák

Ha a távoli szerver leáll, a `fetch` kivételt dob. Tedd a hívást egy `try/catch` blokkba:

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

Most a Java oldal egy hibaüzenetet kap ahelyett, hogy elakadna.

### 5.2 Időkorlátok

Az Aspose motor nem biztosít natív timeout‑ot a `fetch`‑hez, de megvalósítható JavaScript‑ben:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 Több hívás

Ha több erőforrást kell lekérned, egyszerűen iterálj vagy map‑elj egy URL‑tömbön. A host objektum kibővíthető egy azonosító fogadására, így összekapcsolhatod a válaszokat.

---

## Teljes működő példa

Az alábbi **teljes forrásfájl**, amelyet egyszerűen bemásolhatsz az IDE‑dbe. Nincsenek rejtett függőségek, csak az Aspose.HTML JAR a classpath‑on.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**Várt konzolkimenet**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Ha egy `Error:` kezdetű sor jelenik meg, akkor valami rosszul ment – valószínűleg hálózati hiba.

---

## Vizuális áttekintés

![Diagram illustrating how Java calls JavaScript and receives async fetch results – call java from javascript](/images/java-js-async.png)

*A kép a folyamatot mutatja: Java → JavaScriptEngine → async fetch → JavaCallback.*

---

## Gyakran Ismételt Kérdések

**Használhatom ezt a megközelítést más JavaScript motorokkal?**  
Igen, bármely motor, amely host objektum mechanizmust biztosít (pl. Nashorn, GraalVM) működhet, de az Aspose.HTML egy teljes körű, böngészőhöz hasonló környezetet nyújt beépített `fetch`‑tel.

**Mi van, ha egy összetett Java objektumot kell visszaadni a string helyett?**  
Serializálhatod az objektumot JSON‑ra a Java oldalon, és a JavaScript‑ben parse‑olhatod, vagy több metódust is kiexponálhatsz a host objektumon, hogy külön mezőket fogadj.

**A `fetch` implementáció teljesen szabványos?**  
Az Aspose.HTML a WHATWG Fetch Standard‑ot valósítja meg, így megfelelően kezeli az átirányításokat, CORS‑t és a streaminget.

**Blokkolja ez a Java szálat a hálózati várakozás közben?**  
Nem. Az `execute` hívás azonnal visszatér, a belső motor aszinkron módon dolgozza fel a promise‑t. A fő szál azonban addig él, amíg a szkript be nem fejeződik, vagy explicit módon le nem állítod a motort.

---

## Összegzés

Áttekintettük, hogyan **call Java from JavaScript**, hogyan **run async JavaScript**, és hogyan **fetch JSON in Java** a **asynchronous fetch API** segítségével. Egy host objektum létrehozásával, egy rendezett `async` függvény írásával és az Aspose.HTML **JavaScript engine**‑jének használatával tiszta, nem blokkoló hidat építhetsz a két futtatókörnyezet között.

Próbáld ki, módosítsd az URL‑t, vagy adj hozzá több callback‑et – a képzeleted szab határt. A következő lépések lehetnek:

- **Executing JavaScript engine** több egyidejű szkripttel.  
- **run async javascript** nagy adathalmazok párhuzamos feldolgozásához.  
- Ennek a mintának a beépítése egy web‑szolgáltatásba, amely dinamikusan renderel HTML‑t menet közben.

Nyugodtan kísérletezz, és ne habozz kommentben jelezni, ha váratlan problémába ütközöl. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}