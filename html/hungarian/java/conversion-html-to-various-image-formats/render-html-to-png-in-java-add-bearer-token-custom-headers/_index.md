---
category: general
date: 2026-05-06
description: HTML renderelése PNG-re Java-ban az Aspose.HTML használatával, bearer
  token és egyéni fejlécek hozzáadása a védett oldalak betöltéséhez. Tanulja meg,
  hogyan mentse el gyorsan a HTML-t PNG formátumba.
draft: false
keywords:
- render html to png
- save html as png
- add bearer token
- how to pass header
- use custom headers
language: hu
og_description: HTML konvertálása PNG-re Java-ban az Aspose.HTML használatával, bearer
  token és egyedi fejlécek hozzáadása védett oldalak betöltéséhez, majd az HTML mentése
  PNG formátumban.
og_title: HTML renderelése PNG-re Java-ban – Bearer token és egyéni fejlécek hozzáadása
tags:
- Java
- Aspose.HTML
- Image Rendering
- HTTP Authentication
title: HTML konvertálása PNG-re Java-ban – Bearer token és egyéni fejlécek hozzáadása
url: /hu/java/conversion-html-to-various-image-formats/render-html-to-png-in-java-add-bearer-token-custom-headers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML renderelése PNG-re Java-ban – Teljes útmutató

Szükséged volt már **HTML PNG-re renderelésére** Java-ban, miközben egy védett végponthoz férsz hozzá? Az Aspose.HTML segítségével betölthetsz egy védett oldalt, **hozzáadhatsz egy bearer tokent**, és **elmentheted a HTML-t PNG-ként** – mindezt néhány sor kóddal.

Ebben a bemutatóban lépésről lépésre végigvezetünk: a saját fejlécek előkészítésétől a betöltött dokumentum PNG fájlba konvertálásáig. A végére egy kész, futtatható programod lesz, amely bármely hitelesített HTML oldalt képpé alakít le a lemezen.

## Mit fogsz megtanulni

* Hogyan **adj hozzá bearer tokent** egy HTTP kéréshez egy `Map` fejlécek használatával.  
* A pontos szintaxis, **hogyan adjuk át a fejlécek** értékeit a `HTMLDocument`‑nek.  
* A legegyszerűbb módja a **HTML PNG‑ként mentésének** az Aspose.HTML `Converter`‑rel.  
* Tippek a gyakori hibák (pl. tanúsítványhibák, hiányzó erőforrások) elhárításához.  

Nincs szükség külső eszközökre, varázslatra – csak tiszta Java, néhány import, és az Aspose.HTML könyvtár (23.10 vagy újabb verzió).

### Előfeltételek

* Java 8 vagy újabb telepítve.  
* Aspose.HTML for Java JAR a classpath‑on.  
* Érvényes bearer token a céloldalhoz (szerezheted OAuth2‑vel, API kulccsal stb.).  

Ha ismered az alap Java szintaxist, már indulhatsz.

## HTML renderelése PNG-re – Áttekintés

Az alapötlet egyszerű: hozzunk létre egy `HTMLDocument`‑et, amely **egyéni fejlécekkel** tudja lekérni az oldalt, majd adjuk át ezt a dokumentumot a `Converter.convertHtmlToPng`‑nek. A konverter végzi el a nehéz munkát – elrendezés, CSS, képek, betűtípusok – így egy pixel‑pontos pillanatképet kapsz.

```java
import com.aspose.html.*;
import java.util.*;

public class AuthenticatedLoad {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare the HTTP headers with the bearer token
        Map<String, String> authHeaders = new HashMap<>();
        authHeaders.put("Authorization", "Bearer my-secure-token");

        // Step 2: Load the protected HTML page using the custom headers
        String protectedUrl = "https://secure.example.com/report.html";
        HTMLDocument document = new HTMLDocument(protectedUrl, authHeaders);

        // Step 3: Render the loaded page to a PNG file to verify the result
        String outputImagePath = "YOUR_DIRECTORY/secure.png";
        Converter.convertHtmlToPng(document, outputImagePath);

        System.out.println("Page rendered and saved to: " + outputImagePath);
    }
}
```

Ez a kódrészlet a teljes megoldás, de bontsuk le, miért fontos minden sor.

## Bearer token hozzáadása HTTP kéréshez

Amikor egy oldal védett erőforrásait szeretnéd elérni, egy `Authorization` fejlécet vár, amely így néz ki: `Bearer <token>`. Ha ezt a fejlécet egy `Map<String,String>`‑be helyezzük, és átadjuk a `HTMLDocument` konstruktorának, az Aspose.HTML automatikusan beilleszti a fejlécet minden kérésbe (HTML, CSS, képek, AJAX hívások).

```java
Map<String, String> authHeaders = new HashMap<>();
authHeaders.put("Authorization", "Bearer my-secure-token");
```

**Miért használjunk map‑et?**  
* Típus‑biztonságos, és lehetővé teszi **tetszőleges számú** egyéni fejléc hozzáadását – tökéletes API‑khoz, amelyek `X‑API‑KEY` vagy `Accept-Language` fejléceket igényelnek.  
* A map újrahasználható minden további erőforrás lekérdezésnél, így az autentikáció konzisztens marad.

> **Pro tipp:** Ha a token rövid idő után lejár, frissítsd a `HTMLDocument` létrehozása előtt. Ellenkező esetben 401 hibát kapsz, és a PNG üres lesz.

## Fejléc átadása egyéni fejlécek használatával

Az Aspose.HTML `HTMLDocument`‑nek azon túlterhelése, amely `Map`‑et fogad, a legkönnyebb módja a **egyéni fejlécek** használatának. Használhatsz `HttpClient`‑et is manuálisan, de az felesleges bonyolultságot hoz.

```java
HTMLDocument document = new HTMLDocument(protectedUrl, authHeaders);
```

A háttérben a könyvtár egy belső `HttpWebRequest`‑et épít, és minden bejegyzést átmásol a `authHeaders`‑ből. Így például átadhatsz olyan fejléceket is:

```java
authHeaders.put("User-Agent", "MyApp/1.0");
authHeaders.put("Accept-Language", "en-US");
```

Ha **feltételesen** szeretnél bearer tokent hozzáadni (pl. csak bizonyos domainekhez), egyszerűen ellenőrizd az URL‑t, mielőtt feltöltenéd a map‑et.

## HTML mentése PNG fájlba

Az utolsó lépés a varázslat: a teljesen betöltött DOM átalakítása raszteres képpé. A `Converter.convertHtmlToPng` automatikusan kezeli az elrendezést, DPI‑t és a színmélységet.

```java
String outputImagePath = "YOUR_DIRECTORY/secure.png";
Converter.convertHtmlToPng(document, outputImagePath);
```

A kimeneti minőséget testreszabhatod egy `PngDevice`‑el saját beállításokkal, de az alapértelmezett a legtöbb esetben megfelelő.

**Várható kimenet:** egy `YOUR_DIRECTORY/secure.png` helyen tárolt PNG fájl, amely pontosan úgy néz ki, mint a böngészőben megjelenő oldal (kivéve az interaktív JavaScript‑et).

## A renderelt kép ellenőrzése

A program befejezése után nyisd meg a PNG‑t bármely képmegjelenítővel. Ha a kép egy bejelentkezési képernyőt vagy 401 hibát mutat, ellenőrizd a következőket:

1. A bearer token még érvényes‑e.  
2. Az `Authorization` fejléc helyes‑e (`Bearer` + space).  
3. A cél‑URL elérhető‑e a gépedről (tűzfal, VPN stb.).  

Ha minden rendben, a védett jelentés pixel‑pontos renderelését fogod látni.

![Render result of protected page saved as PNG](render_html_to_png.png)

*Alt text: Képernyőkép, amely egy védett HTML oldalt mutat PNG‑ként mentve, miután hozzáadtuk a bearer tokent és egyéni fejléceket.*

## Szélsőséges esetek és gyakori buktatók

| Helyzet | Mit ellenőrizz | Javasolt megoldás |
|-----------|---------------|---------------|
| **Önaláírt SSL tanúsítvány** | `SSLHandshakeException` | Adj hozzá egy egyéni `TrustManager`‑t vagy indítsd a Java‑t a `-Djavax.net.ssl.trustStore`‑val, amely a tanúsítványra mutat. |
| **Nagy oldal (több mint 10 MB)** | Memória túlcsordulás | Növeld a JVM heap‑et (`-Xmx2g`) vagy csak egy konkrét elemet renderelj a `document.getElementById` segítségével. |
| **AJAX‑szal betöltött dinamikus tartalom** | Tartalom hiányzik a PNG‑ben | Hívj `document.waitForLoad()`‑t a konvertálás előtt, vagy engedélyezd a `HtmlLoadOptions.setEnableJavaScript(true)`‑t. |
| **Hiányzó betűtípusok** | Szöveg helyettesítő betűtípussal jelenik meg | Telepítsd a szükséges betűtípusokat a gépre, vagy ágyazd be őket CSS‑ben `@font-face`‑vel. |

Ezek korai kezelése órákat spórolhat a hibakeresésben.

## Összegzés: HTML renderelése PNG‑re magabiztosan

Áttekintettük a teljes munkafolyamatot a **HTML PNG‑re rendereléséhez** Java‑ban, a **bearer token hozzáadásától** a **egyéni fejlécek használatáig**, és végül a **HTML PNG‑ként mentéséig**. A teljes, futtatható példa a útmutató elején található, így egyszerűen másolhatod és testreszabhatod.

### Mi a következő lépés?

* Kísérletezz különböző képformátumokkal (`convertHtmlToJpeg`, `convertHtmlToBmp`).  
* Próbáld meg csak egy adott DOM elemet renderelni: töltsd be az oldalt, válaszd ki az elemet, és add át egy `PngDevice`‑nek.  
* Kombináld ezt a technikát egy ütemezővel, hogy napi jelentésképernyőket generálj automatikusan.

Nyugodtan módosítsd a fejléc‑map‑et, cseréld ki a token‑szolgáltatót, vagy integráld a kódot egy nagyobb mikroszolgáltatásba. A lehetőségek gyakorlatilag végtelenek, és a központi minta – **használd az egyéni fejléceket, töltsd be a dokumentumot, konvertálj PNG‑re** – változatlan marad.

Boldog kódolást, és legyenek a képernyőképeid mindig kristálytisztaak!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}