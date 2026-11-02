---
category: general
date: 2026-02-16
description: Tanulja meg, hogyan futtathat JavaScriptet Java‑ban a CompletableFuture
  segítségével, késleltetheti a JS‑t, és kiértékelheti az aszinkron kódot. Teljes
  lépésről‑lépésre útmutató az aszinkron JavaScript kiértékeléséhez.
draft: false
keywords:
- how to run javascript
- how to use completablefuture
- how to delay js
- how to evaluate async
- evaluate javascript asynchronously
language: hu
og_description: Tanulja meg, hogyan futtathat JavaScriptet Java‑ból, késleltetheti
  a JS‑t, és aszinkron kódot értékelhet a CompletableFuture segítségével ebben a teljes
  körű útmutatóban.
og_title: Hogyan futtassuk a JavaScript-et aszinkron módon a CompletableFuture segítségével
tags:
- javascript
- java
- asynchronous
- completablefuture
title: Hogyan futtassuk aszinkron módon a JavaScript-et a CompletableFuture segítségével
url: /hu/java/advanced-usage/how-to-run-javascript-asynchronously-using-completablefuture/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hogyan futtassunk JavaScriptet aszinkron módon a CompletableFuture segítségével

Valaha is elgondolkodtál **hogyan futtassunk JavaScriptet** egy Java alkalmazáson belül anélkül, hogy blokkolnád a fő szálat? Lehet, hogy egy apró szkriptet kell meghívnod, amely adatokat lekér, de nem akarod, hogy a felhasználói felület lefagyjon. A jó hír, hogy a modern Java könyvtárak lehetővé teszik a JavaScript **aszinkron** kiértékelését, és akár késleltetéseket is bevezethetsz, akárcsak egy böngészőben. Ebben az útmutatóban egy teljes, futtatható példát mutatunk be, amely az Aspose HTML `ScriptEngine`‑jét használja a `CompletableFuture`‑val együtt, hogy **hogyan futtassunk javascriptet** és visszakapjuk az eredményt Java-ban.

Kitérünk arra is, hogy **hogyan használjuk a CompletableFuture‑t**, **hogyan késleltessük a JS‑t**, és **hogyan értékeljünk ki aszinkron** kódot, hogy **aszinkron módon értékelhessük a JavaScriptet** bármely Java projektben. A végére egy stabil sablont kapsz, amelyet másolhatsz‑beilleszthetsz, módosíthatsz, és beágyazhatsz nagyobb rendszerekbe.

Nem szükséges külső build eszköz a Aspose HTML for Java JAR‑on kívül, amelyet egyszerűen a classpath‑ba helyezhetsz. Merüljünk el benne.

## Mit fogsz megtanulni

- Állíts be egy Java `ScriptEngine`‑t, amely képes modern ES2022 JavaScriptet futtatni.
- Írj egy `async` függvényt, amely késleltetést tartalmaz (**hogyan késleltessük a js**).
- Hívd meg a `evaluateAsync`‑t, és kapj egy `CompletableFuture`‑t (**hogyan használjuk a completablefuture**).
- Szerezd meg az eredményt, amint a JavaScript ígéret feloldódik (**hogyan értékeljünk ki aszinkron**).
- Tippek a hibakezeléshez, szálkezeléshez és a minta kiterjesztéséhez.

## 1. lépés: Hogyan futtassunk JavaScriptet – A szkriptmotor inicializálása

Először is. Az Aspose HTML könyvtár egy `ScriptEngine` osztályt biztosít, amely képes JavaScript kódot végrehajtani. Gondolj rá úgy, mint egy apró Chromium motorra, amely a JVM‑edben fut.

```java
import com.aspose.html.scripting.*;
import java.util.concurrent.CompletableFuture;

public class JsAsyncDemo {
    public static void main(String[] args) throws Exception {

        // Create a scripting engine that can run JavaScript
        ScriptEngine scriptEngine = new ScriptEngine();
```

> **Miért fontos:** A `ScriptEngine` példányosításával egy sandbox környezetet kapunk, ahol a modern JavaScript (beleértve az `async/await`-t) azonnal működik. Nincs szükség külső Node folyamat indítására.

## 2. lépés: Hogyan késleltessük a JS‑t – Async függvény írása ígéret‑alapú időzítővel

A JavaScript `setTimeout` a klasszikus módja a végrehajtás szüneteltetésének. Modern kódban egy `Promise`‑ba csomagoljuk, hogy `await`‑olhassuk. Pontosan ezt fogjuk tenni a szkript karakterláncban.

```java
        // ES2022 async function that resolves after a short delay
        String asyncScript = """
            async function fetchMessage() {
                const delay = ms => new Promise(r => setTimeout(r, ms));
                await delay(500); // 500 ms pause
                return "Hello from async JS!";
            }
            fetchMessage(); // Return the promise to Java
            """;
```

> **Hogyan késleltessük a js‑t:** A `delay` segédfüggvény egy ígéretet hoz létre, amely `ms` ezredmásodperc után teljesül. Az `await`‑olásával a függvény szünetel, anélkül hogy a Java szálat blokkolná.

## 3. lépés: Hogyan értékeljünk ki aszinkron – A szkript futtatása és egy CompletableFuture lekérése

A szinkron `evaluate` metódus helyett a `evaluateAsync`‑t hívjuk. Az azonnal visszaad egy `CompletableFuture<Object>`‑t, amely akkor lesz befejezve, amikor a JavaScript ígéret feloldódik.

```java
        // Evaluate the script asynchronously – a CompletableFuture is returned
        CompletableFuture<Object> resultFuture = scriptEngine.evaluateAsync(asyncScript);
```

> **Hogyan értékeljünk ki aszinkron:** A `evaluateAsync` összeköti a JavaScript eseményhurkot a Java `CompletableFuture`‑jával. Ez a **JavaScript aszinkron kiértékelésének** magja.

## 4. lépés: Hogyan használjuk a CompletableFuture‑t – Callback csatolása és blokkolás a demóhoz

Most egy callback‑et csatolunk a `thenAccept`‑el, hogy kiírjuk az eredményt, és blokkoljuk a fő szálat annyira, amíg a demó be nem fejeződik.

```java
        // When the promise resolves, print the JavaScript result
        resultFuture.thenAccept(result ->
                System.out.println("JS result: " + result));

        // Block the main thread long enough for the demo to finish
        resultFuture.get(); // throws checked exceptions, handled by main's throws clause
    }
}
```

> **Miért hívjuk a `get()`‑et:** Egy valódi alkalmazásban valószínűleg máshol folytatnád a feldolgozást. Itt blokkolunk, hogy a példa önmagában legyen.

## Vizuális áttekintés

![Diagram, amely bemutatja, hogyan futtassunk JavaScriptet aszinkron módon a CompletableFuture segítségével](https://example.com/diagram.png "Hogyan futtassunk JavaScriptet – Aszinkron folyamat")

*Alt szöveg:* **Diagram, amely bemutatja, hogyan futtassunk JavaScriptet aszinkron módon a CompletableFuture segítségével** – a kép illusztrálja a folyamatot a Java-tól a szkriptmotorig, az aszinkron késleltetést és a CompletableFuture befejezését.

## Gyakori buktatók és legjobb gyakorlatok (Hogyan értékeljünk ki aszinkron biztonságosan)

| Buktató | Mi történik | Megoldás |
|---------|--------------|----------|
| Elfelejtünk visszaadni egy ígéretet | `evaluateAsync` azonnal `undefined`‑dal oldódik fel | Győződj meg arról, hogy a szkript utolsó sorában az ígéret szerepel (`fetchMessage();`) |
| Blokkoló `Thread.sleep` használata JS-ben | Blokkolja a motor eseményhurkot, megsemmisíti az aszinkron működést | Használd a `delay` ígéret mintát (ahogy a példában látható) |
| Kivételek figyelmen kívül hagyása | A Future kivétellel fejeződik be, de nem látod | Csatold a `.exceptionally(e -> { e.printStackTrace(); return null; })`-t |
| A motor leállításának elhagyása | Erőforrás szivárgás hosszú távú alkalmazásokban | Hívd meg a `scriptEngine.dispose()`‑t, amikor kész vagy |

## A minta kiterjesztése (Hogyan használjuk a CompletableFuture‑t valós projektekben)

Több async JavaScript hívást láncolhatsz, kombinálhatod őket más future‑okkal, vagy akár egy egyedi `Executor`‑on is futtathatod őket. Íme egy gyors vázlat:

```java
ExecutorService jsPool = Executors.newFixedThreadPool(4);
CompletableFuture<Object> future = scriptEngine.evaluateAsync(asyncScript, jsPool)
    .thenApply(result -> {
        // Post‑process the JS string result
        return ((String) result).toUpperCase();
    })
    .exceptionally(ex -> {
        System.err.println("JS error: " + ex);
        return "fallback";
    });
```

> **Hogyan használjuk a CompletableFuture‑t:** Egy `Executor` átadásával irányíthatod a szálkészletet, így a UI reagálók marad és elkerülöd a szálak hiányát.

## Várt kimenet

Futtasd a `JsAsyncDemo` osztályt, és a következőt kell látnod:

```
JS result: Hello from async JS!
```

Az 500 ms-os szünet nem látható a konzolon, de ha szeretnéd, hozzáadhatsz időbélyeget a késleltetés ellenőrzéséhez.

## Összefoglalás – Hogyan futtassunk JavaScriptet a CompletableFuture‑val

Elkezdtem azzal, hogy **hogyan futtassunk javascriptet** Java-ban, írtunk egy `async` függvényt, amely **hogyan késleltessük a js‑t**, végrehajtottuk a `evaluateAsync`‑val (**hogyan értékeljünk ki aszinkron**), és a **hogyan használjuk a completablefuture‑t** segítségével kaptuk meg az eredményt. Az egész folyamat bemutatja a **JavaScript aszinkron kiértékelését** egy tiszta, újrahasználható mintában.

## Mi a következő?

- **Integrálás HTTP kliensekkel:** Adatok lekérése egy REST végpontról az async JS-ben, és visszaadása Java-nak.
- **Több szkript használata:** Több `evaluateAsync` hívás láncolása összetett folyamatokhoz.
- **Motor cseréje:** Ugyanez a minta működik Nashorn, GraalVM vagy más JavaScript futtatókörnyezetekkel – csak cseréld le a `ScriptEngine`‑t.

Nyugodtan kísérletezz hosszabb késleltetésekkel, hibát dobó szkriptekkel vagy akár WebAssembly modulokkal. A lehetőségek határtalanok, ha a Java párhuzamossági primitívjeit a modern JavaScript‑tel kombinálod.

### Van kérdésed?

Ha valami nem világos – talán azt kérdezed, hogyan kezeljünk elutasított ígéretet vagy hogyan adjunk át változókat Java‑ból a szkriptbe – hagyj egy megjegyzést alább. Boldog kódolást!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}