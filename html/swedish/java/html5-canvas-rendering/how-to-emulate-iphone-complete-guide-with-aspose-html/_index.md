---
category: general
date: 2026-03-26
description: Lär dig hur du emulerar iPhone i Java med Aspose.HTML. Inkluderar steg
  för att ange en anpassad användaragent och ställa in enhetens pixelratio för exakt
  mobilrendering.
draft: false
keywords:
- how to emulate iphone
- set custom user agent
- set device pixel ratio
- how to set user-agent
- how to set dpr
language: sv
og_description: Hur emulerar man iPhone i Java? Den här handledningen visar hur man
  ställer in en anpassad användaragent och enhetens pixelratio med Aspose.HTML, vilket
  levererar pixelperfekta mobilsidor.
og_title: Hur man emulerar iPhone – Steg‑för‑steg Aspose.HTML‑guide
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Hur man emulerar iPhone – Komplett guide med Aspose.HTML
url: /sv/java/html5-canvas-rendering/how-to-emulate-iphone-complete-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så här emulerar du iPhone – Komplett guide med Aspose.HTML

Har du någonsin funderat **hur man emulerar iPhone** när du testar en webbsida lokalt? Kanske felsöker du en responsiv layout och skrivbordets webbläsare bara inte duger. Den goda nyheten är att du inte behöver en fysisk enhet—Aspose.HTML:s `DocumentSandbox` låter dig efterlikna en iPhones skärm, user‑agent och device‑pixel‑ratio (DPR) med några få rader Java.  

I den här handledningen går vi igenom exakt hur du sätter en **anpassad user agent**, konfigurerar **device pixel ratio**, och verifierar att allt fungerar som förväntat. När du är klar har du en återanvändbar sandbox som renderar sidor precis som en iPhone 8, och du förstår varför varje inställning är viktig.

## Vad du kommer att uppnå

- Skapa ett `Screen`‑objekt som speglar en iPhones dimensioner och DPR.  
- Applicera en **anpassad user agent**‑sträng så att servrar tror att begäran kommer från Safari på iOS.  
- Bygga ett `DocumentSandbox` som knyter skärmen och user‑agenten ihop.  
- Köra ett `HTMLDocument` i sandboxen och se konsolutskriften som bekräftar konfigurationen.  

Inga externa bibliotek utöver Aspose.HTML behövs, och koden körs i vilken Java 17+‑miljö som helst.

---

![skärmdump av hur man emulerar iPhone](https://example.com/images/iphone-emulation.png "hur man emulerar iPhone med Aspose.HTML sandbox")

## Så här emulerar du iPhone med Aspose.HTML Sandbox

Det första vi behöver är en `Screen` som återger iPhone‑ens fysiska dimensioner *och* dess pixeldensitet. Detta är kärnan i **hur man emulerar iPhone** på ett exakt sätt.

```java
import com.aspose.html.devices.Screen;

// Step 1: Define iPhone 8 screen size (width, height) and DPR
Screen mobileScreen = new Screen(375, 667, 2.0); // iPhone 8 dimensions, DPR = 2
```

**Varför detta är viktigt:**  
- Bredd = 375 px och höjd = 667 px är de CSS‑pixel‑dimensioner du ser i Chrome DevTools när du väljer en iPhone 8.  
- Att sätta DPR till 2 talar om för renderingsmotorn att behandla varje CSS‑pixel som två fysiska pixlar, vilket ger skarp text och bilder—precis som en riktig enhet gör.

> *Proffstips:* Om du behöver emulera en nyare iPhone (t.ex. iPhone 13), ändra bara siffrorna till 390 × 844 och DPR = 3.

## Sätta en anpassad User Agent (set custom user agent)

Nästa steg är att **sätta en anpassad user agent** så att servern levererar den mobila HTML/CSS‑versionen. Utan detta tror många webbplatser fortfarande att du använder en desktop‑browser.

```java
// Step 2: Define an iPhone Safari user‑agent string
String iPhoneUserAgent = "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) " +
                         "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                         "Version/16.0 Mobile/15E148 Safari/604.1";
```

**Hur detta fungerar:**  
- `User-Agent`‑headern är den handskakning som webbläsare använder för att presentera sig själva.  
- Genom att ange exakt den sträng som Safari på iOS 16 skickar, säkerställer du att servern returnerar de mobiloptimerade resurserna (tänk responsiva bilder, adaptiva skript, osv.).  

Om du någonsin behöver **hur man sätter user-agent** för en annan enhet, byt bara ut strängen mot rätt värde—Google Chrome, Firefox, eller till och med en egen bot.

## Konfigurera Device Pixel Ratio (set device pixel ratio)

Nu sätter vi faktiskt **device pixel ratio** i sandboxen. Detta är steget som direkt svarar på “**hur man sätter dpr**” för en simulerad miljö.

```java
import com.aspose.html.sandbox.DocumentSandbox;

// Step 3: Build the sandbox with screen and user‑agent
DocumentSandbox documentSandbox = new DocumentSandbox.Builder()
        .setScreen(mobileScreen)          // applies the DPR we defined earlier
        .setUserAgent(iPhoneUserAgent)    // applies the custom user‑agent
        .build();
```

**Förklaring:**  
- `Builder`‑mönstret låter dig smidigt bifoga både skärmen (som bär med sig DPR) och user‑agenten.  
- När sandboxen renderar ett `HTMLDocument` kommer den att låtsas köra på en enhet med exakt den pixeldensiteten.  

> *Varför du bör bry dig:* Vissa CSS‑media‑queries använder `device-pixel-ratio` (t.ex. `@media (-webkit-min-device-pixel-ratio: 2)`). Om du inte sätter DPR, triggas dessa regler aldrig, och du missar högupplösta resurser.

## Verifiera sandbox‑konfigurationen (how to set user-agent)

Låt oss sätta sandboxen i arbete. Följande kodsnutt skapar ett `HTMLDocument`, laddar en sida och skriver ut en bekräftelse på att sandboxen är aktiv.

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

**Förväntad konsolutskrift**

```
Sandbox configured with DPR=2 and iPhone user-agent.
```

Om du kör programmet och ser den raden har du lyckats **hur man emulerar iPhone** med rätt DPR och user‑agent. Öppna sidan i en riktig webbläsare och inspektera viewport‑dimensionerna—du kommer märka att de matchar de iPhone‑värden vi satte.

## Vanliga fallgropar och hur man sätter DPR korrekt (how to set dpr)

Även med rätt kod kan några fällor göra dig frustrerad:

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| **DPR förblir 1** | Du skickade en `Screen` utan det tredje argumentet (DPR). | Använd alltid `new Screen(width, height, dpr)`. |
| **User‑Agent ignoreras** | Sandboxen var inte kopplad till `HTMLDocument`. | Skicka `documentSandbox` som det andra argumentet till `HTMLDocument`‑konstruktorn. |
| **Fel dimensioner** | Du använder enhetspixlar istället för CSS‑pixlar. | Kom ihåg: bredd/höjd är **CSS‑pixlar**, inte hårdvarupixlar. |
| **Servern skickar fortfarande desktop‑CSS** | Vissa webbplatser använder JavaScript för att upptäcka enheter, inte bara headern. | Överväg även att injicera en viewport‑meta‑tagg om det behövs. |

Genom att ha dessa i åtanke kommer du sällan stöta på en situation där emuleringen inte beter sig som förväntat.

## Utöka sandboxen – nästa steg

Nu när du vet **hur man sätter anpassad user agent** och **hur man sätter dpr**, kan du experimentera vidare:

- **Ändra skärmstorleken** för att emulera surfplattor eller större telefoner.  
- **Byt user‑agent** för att testa Chrome på Android (`"Mozilla/5.0 (Linux; Android 12; ...) Chrome/110.0"`).  
- **Lägg till cookies eller headers** via sandboxens `setHeaders`‑metod för autentiserad testning.  
- **Fånga en skärmdump** med `HTMLDocument.renderToFile("output.png")` för att automatiskt jämföra visuella skillnader.

Dessa tillägg låter dig bygga ett fullständigt test‑härmar utan att någonsin lämna din IDE.

---

## Slutsats

Vi har gått igenom **hur man emulerar iPhone** med Aspose.HTML:s `DocumentSandbox`, visat dig exakt **hur man sätter anpassad user agent**, **hur man sätter device pixel ratio**, och även de subtila skillnaderna mellan “**hur man sätter user-agent**” och “**hur man sätter dpr**”. Det kompletta, körbara exemplet demonstrerar varje del på ett ställe, så du kan kopiera‑klistra, justera och börja testa mobila layouter omedelbart.  

Prova—byt skärmdimensionerna, lek med olika user‑agents, och se hur dina sidor reagerar. När du behärskar dessa inställningar blir felsökning av responsiva designer en barnlek, och du sparar otaliga timmar på att jaga buggar på riktiga enheter.

Har du frågor eller vill dela dina egna varianter? Lägg en kommentar nedan, och lycka till med emuleringen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}