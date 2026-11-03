---
category: general
date: 2026-02-10
description: Ställ in enhetens pixelratio i Java med Aspose.HTML‑sandbox. Lär dig
  hur du sätter skärmbredd och -höjd samt hämtar sidans titel i Java med ett komplett,
  körbart exempel.
draft: false
keywords:
- set device pixel ratio
- get page title java
- set screen width height
language: sv
og_description: Ställ in enhetens pixelförhållande i Java med Aspose.HTML‑sandbox.
  Den här guiden visar hur du ställer in skärmbredd och -höjd samt hämtar sidans titel
  i Java i några enkla steg.
og_title: Ställ in enhetens pixelförhållande i Java – Mobile Sandbox-handledning
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Ställ in enhetens pixelförhållande i Java – Mobile Sandbox‑handledning
url: /sv/java/advanced-usage/set-device-pixel-ratio-in-java-mobile-sandbox-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in enhetens pixelförhållande i Java – Mobile Sandbox‑handledning

Har du någonsin behövt **set device pixel ratio** när du testar en responsiv webbplats i Java? Du är inte ensam. Många utvecklare stöter på problem när sidan ser perfekt ut på skrivbordet men går sönder på hög‑DPI‑telefoner. Den goda nyheten? Med Aspose.HTML:s sandbox kan du emulera en iPhone X (eller någon enhet) direkt från din Java‑kod—ingen webbläsare behövs.

I den här guiden går vi igenom **how to set screen width height**, konfigurerar **device pixel ratio**, och slutligen **get page title java** för att verifiera att allt renderas korrekt. När du är klar har du ett självständigt program som du kan lägga in i vilket projekt som helst och börja testa mobila layouter omedelbart.

## Förutsättningar

- Java 8 eller nyare (koden kompilerar även med JDK 11)  
- Aspose.HTML för Java‑bibliotek (version 23.7 eller senare) – du kan hämta det från Maven Central  
- En IDE eller en enkel `javac`‑kommandoradsuppsättning  
- Internetåtkomst för demo‑URL:en (`https://responsive.example.com`)

Inga extra ramverk, ingen Selenium, bara ren Java och Aspose.HTML.

---

## Steg 1: Ställ in skärmbredd‑höjd och enhetens pixelförhållande

Det första vi behöver är ett `SandboxOptions`‑objekt som talar om för sandboxen vilken “enhet” vi låtsas vara. Här använder vi iPhone X‑dimensionerna (375 × 812 CSS‑pixlar) och ett **device pixel ratio** på 3.0, vilket speglar den hög‑DPI‑retina‑displayen.

```java
// Step 1 – configure the virtual device
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setScreenWidth(375);          // CSS pixels width
sandboxOptions.setScreenHeight(812);         // CSS pixels height
sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI factor (set device pixel ratio)
```

> **Varför detta är viktigt:**  
> Anropet `setDevicePixelRatio` skalar allt—från bilder till teckensnittsrendering—så att sidan tror att den är på en riktig telefon. Om du hoppar över det kan layouten falla tillbaka på desktop‑stil CSS‑media queries, vilket undergräver syftet med mobilt testande.

---

## Steg 2: Skapa sandbox‑instansen

Nu omvandlar vi dessa alternativ till en levande sandbox. Tänk på sandboxen som en liten, huvudlös webbläsare som respekterar de dimensioner och den pixelförhållande vi just definierade.

```java
// Step 2 – spin up the sandbox with the options above
Sandbox mobileSandbox = new Sandbox(sandboxOptions);
```

> **Proffstips:** Du kan återanvända samma `Sandbox`‑objekt för flera sidladdningar; ändra bara URL:en så behåller sandboxen samma enhetsegenskaper.

---

## Steg 3: Ladda sidan i sandboxen

När sandboxen är klar är det lika enkelt att ladda en sida som att konstruera ett `HTMLDocument` och skicka sandboxen som ett andra argument. Detta tvingar dokumentet att renderas med den virtuella enhet vi satte tidigare.

```java
// Step 3 – fetch the target page using the sandbox
HTMLDocument htmlDoc = new HTMLDocument(
        new URL("https://responsive.example.com"), mobileSandbox);
```

Om URL:en är oåtkomlig eller sidan innehåller fel kommer Aspose.HTML att kasta ett undantag. För produktionskod skulle du troligen omsluta detta i ett `try‑catch` och logga felet, men för handledningen håller vi det enkelt.

---

## Steg 4: Verifiera med get page title java

Det snabbaste sundhetskontrollen är att läsa dokumentets titel. Om sandboxen korrekt tillämpade **device pixel ratio** kommer titeln att vara identisk med vad du skulle se på en riktig iPhone X.

```java
// Step 4 – retrieve and print the page title (get page title java)
System.out.println("Title under sandbox: " + htmlDoc.getTitle());
```

**Förväntat resultat (exempel):**

```
Title under sandbox: Responsive Demo – Mobile View
```

Om du ser titeln skriven ut har du framgångsrikt **set device pixel ratio**, **set screen width height**, och **got the page title** med Java.

---

## Fullt, körbart exempel

Nedan är det kompletta programmet som du kan kopiera‑klistra in i en fil med namnet `SandboxDemo.java`. Se till att Aspose.HTML‑JAR‑filerna finns på din classpath (`-cp`‑flaggan) innan du kompilerar.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.Sandbox;
import com.aspose.html.sandbox.SandboxOptions;
import com.aspose.html.net.URL;

/**
 * Demonstrates how to set device pixel ratio, set screen width height,
 * and get page title java using Aspose.HTML sandbox.
 */
public class SandboxDemo {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define device characteristics ----------
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setScreenWidth(375);          // CSS pixels width
        sandboxOptions.setScreenHeight(812);         // CSS pixels height
        sandboxOptions.setDevicePixelRatio(3.0);     // High‑DPI screen factor (set device pixel ratio)

        // ---------- Step 2: Create the sandbox ----------
        Sandbox mobileSandbox = new Sandbox(sandboxOptions);

        // ---------- Step 3: Load a web page inside the sandbox ----------
        HTMLDocument htmlDoc = new HTMLDocument(
                new URL("https://responsive.example.com"), mobileSandbox);

        // ---------- Step 4: Verify the document loaded correctly ----------
        System.out.println("Title under sandbox: " + htmlDoc.getTitle());
    }
}
```

Kompilera och kör:

```bash
javac -cp "aspose-html-23.7.jar" SandboxDemo.java
java -cp ".:aspose-html-23.7.jar" SandboxDemo
```

Du bör se titeln skriven till konsolen, vilket bekräftar att sidan renderades med önskat **device pixel ratio**.

---

## Vanliga frågor & kantfall

| Fråga | Svar |
|----------|--------|
| **Kan jag ändra pixelförhållandet vid körning?** | Ja—skapa bara ett nytt `SandboxOptions` med ett annat `setDevicePixelRatio`‑värde och instansiera en ny `Sandbox`. Att återanvända samma sandbox efter att ha ändrat dess alternativ stöds inte. |
| **Vad händer om jag behöver testa flera enheter?** | Iterera över en lista med `SandboxOptions` (t.ex. iPhone 8, Pixel 4) och kör samma ladd‑och‑titel‑logik för varje. |
| **Fungerar detta med HTTPS‑sajter som har självsignerade certifikat?** | Aspose.HTML respekterar Javas standard‑SSL‑trust‑store. Lägg till certifikatet i JVM:s nyckelbutik eller inaktivera verifiering enbart för testning (rekommenderas inte i produktion). |
| **Hur fångar jag en skärmbild istället för bara titeln?** | `HTMLDocument`‑API:n erbjuder `save`‑metoder som kan exportera den renderade sidan till PNG eller JPEG. Använd `htmlDoc.save("output.png", SaveFormat.PNG);` efter laddning. |
| **Är sandboxen trådsäker?** | Varje `Sandbox`‑instans är isolerad, men du bör undvika att dela en enda instans över flera trådar utan synkronisering. |

---

## Visuell översikt

![Diagram som visar set device pixel ratio i mobile sandbox](https://example.com/images/sandbox-diagram.png "diagram för set device pixel ratio")

*Illustrationen ovan visar flödet från konfiguration av `SandboxOptions` (inklusive **set screen width height** och **set device pixel ratio**) till att ladda en URL och extrahera titeln.*

---

## Slutsats

Du vet nu **how to set device pixel ratio** i Java, hur du **set screen width height** för exakt mobilemulering, och hur du **get page title java** för att bekräfta att renderingen lyckades. Detta kompakta arbetsflöde eliminerar behovet av tunga webbläsare under automatiserad UI‑testning och passar smidigt in i CI‑pipelines.

Klar för nästa steg? Försök exportera den renderade sidan som en bild, eller experimentera med CSS‑media‑query‑debugging genom att växla `devicePixelRatio` mellan 1.0 och 3.0. Du kan också utforska Aspose.HTML:s PDF‑konverteringsfunktioner för att få en utskrivbar version av mobilvyn.

Lycka till med kodandet, och må dina mobila layouter alltid se skarpa ut—oavsett pixeltäthet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}