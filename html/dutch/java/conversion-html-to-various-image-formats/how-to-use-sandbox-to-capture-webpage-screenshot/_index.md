---
category: general
date: 2026-03-25
description: Hoe je de sandbox gebruikt om een screenshot van een webpagina te maken
  met Aspose.HTML voor Java. Leer HTML opslaan als PNG, HTML‑naar‑afbeeldingconversie
  en HTML‑naar‑PNG‑conversie in enkele minuten.
draft: false
keywords:
- how to use sandbox
- capture webpage screenshot
- save html as png
- html to image conversion
- html to png conversion
language: nl
og_description: Hoe je sandbox gebruikt om een screenshot van een webpagina te maken.
  Deze tutorial laat zien hoe je HTML opslaat als PNG, met uitleg over HTML‑naar‑afbeelding
  conversie en HTML‑naar‑PNG conversie met Aspose.HTML voor Java.
og_title: Hoe je Sandbox gebruikt om een screenshot van een webpagina te maken
tags:
- Aspose.HTML
- Java
- Web Automation
title: Hoe Sandbox te gebruiken om een screenshot van een webpagina te maken
url: /nl/java/conversion-html-to-various-image-formats/how-to-use-sandbox-to-capture-webpage-screenshot/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Sandbox te Gebruiken om een Webpagina Screenshot te Maken

Het gebruik van sandbox om een webpagina screenshot te maken is een veelvoorkomende eis wanneer je een pixel‑perfecte preview van een responsieve pagina nodig hebt. In deze gids laten we je ook zien hoe je **save HTML as PNG** kunt gebruiken met Aspose.HTML for Java, waarbij we alles behandelen van *html to image conversion* tot *html to png conversion* in één reproduceerbaar voorbeeld.

Stel je voor dat je een marketing‑landingspagina test die er anders uitziet op een telefoon, een tablet en een desktop. In plaats van drie browsers te openen, kun je een sandbox starten, deze op de URL richten en direct een PNG krijgen die precies weergeeft wat een echt apparaat zou renderen. Aan het einde van deze tutorial heb je een compleet, uitvoerbaar Java‑programma dat precies dat doet, plus een reeks praktische tips die je in je eigen projecten kunt hergebruiken.

## Wat je nodig hebt

- **Aspose.HTML for Java** (v23.9 of nieuwer). De bibliotheek is beschikbaar via Maven Central, dus het toevoegen van de afhankelijkheid is een fluitje van een cent.
- Een **JDK 11+** geïnstalleerd op je machine.
- Een IDE of teksteditor naar keuze (IntelliJ IDEA, VS Code, Eclipse… alles kan).
- Internettoegang voor de voorbeeld‑URL (`https://example.com/responsive.html`) of vervang deze door elke pagina die je wilt vastleggen.

Er zijn geen extra native binaries of headless browsers nodig — de sandbox draait volledig in het geheugen.

---

## Hoe Sandbox te Gebruiken – Stap 1: Definieer het Virtuele Apparaat

Het eerste wat je doet, is de sandbox vertellen welke schermgrootte je wilt emuleren. Hier komt het primaire zoekwoord goed van pas: *how to use sandbox* voor een specifieke viewport.

```java
// Step 1: Create a DeviceInfo that describes the virtual screen
DeviceInfo sandboxDevice = new DeviceInfo();
sandboxDevice.setWidth(800);               // width in pixels
sandboxDevice.setHeight(600);              // height in pixels
sandboxDevice.setDevicePixelRatio(1.0);    // 1 × for standard displays
sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");
```

**Waarom dit belangrijk is:**  
Het instellen van de breedte en hoogte dwingt de layout‑engine de pagina te behandelen alsof deze wordt weergegeven op een 800×600 monitor. De `devicePixelRatio` beïnvloedt hoe CSS‑gebaseerde media‑queries (`@media (min‑device‑pixel‑ratio: ...)`) zich gedragen, waardoor de screenshot overeenkomt met de real‑world ervaring.

> **Pro tip:** Als je een high‑DPI screenshot nodig hebt (denk aan Retina‑displays), verhoog dan de `devicePixelRatio` naar `2.0` en pas de breedte/hoogte dienovereenkomstig aan.

---

## Capture Webpage Screenshot – Stap 2: Laad de Pagina in de Sandbox

Nu vragen we Aspose.HTML om de externe HTML op te halen en te renderen binnen de sandbox die we zojuist hebben gedefinieerd. Deze stap is het hart van **capture webpage screenshot**.

```java
// Step 2: Load the remote HTML page using the sandboxed environment
HTMLDocument document = new HTMLDocument(
        "https://example.com/responsive.html",
        new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));
```

**Wat gebeurt er onder de motorkap?**  
`HTMLDocumentLoadOptions` ontvangt een `Sandbox`‑instantie die onze `DeviceInfo` bevat. De bibliotheek maakt vervolgens een headless render‑context die rekening houdt met de viewport, user‑agent string en eventuele JavaScript die de pagina kan uitvoeren — *alles zonder Chrome of Firefox te starten*.

Als de doelpagina authenticatie vereist, kun je cookies of aangepaste headers injecteren via `HTMLDocumentLoadOptions`. Dat is een nuttig randgeval wanneer je met intranet‑portalen werkt.

---

## Save HTML as PNG – Stap 3: Converteer het Gerenderde Document naar een Afbeelding

Met de pagina gerenderd, is het laatste stuk om **save HTML as PNG** uit te voeren. Dit is de daadwerkelijke *html to png conversion* stap.

```java
// Step 3: Convert the rendered document to PNG and write it to disk
try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
    Converter.convertDocument(
            document,
            new ConversionOptions(ConversionFormat.PNG),
            out);
}
```

Wanneer de `Converter` klaar is, vind je een bestand genaamd `responsive_page.png` in de `output` map. Open het, en je ziet precies hoe de pagina eruitzag op 800×600 pixels — geen browser‑UI, geen scrollbars, alleen de pure weergave.

**Veelvoorkomende valkuilen:**  
- **Bestands‑toegangs‑fouten:** Zorg dat de directory bestaat (`output/` in het voorbeeld) en dat je proces ernaar kan schrijven.  
- **Grote pagina's:** Zeer lange pagina's kunnen enorme PNG‑bestanden opleveren; je kunt de hoogte beperken in `DeviceInfo` of bijsnijden na conversie.  
- **Dynamische inhoud:** Als de pagina data laadt via AJAX na de initiële load, moet je mogelijk een korte vertraging (`Thread.sleep(2000)`) inlassen vóór conversie, of `HTMLDocumentLoadOptions.setWaitForResources(true)` gebruiken.

### html to image conversion – Geavanceerde Opties

Aspose.HTML biedt verschillende instellingen die je kunt aanpassen om de **html to image conversion** fijn af te stemmen:

| Option | Description | When to use |
|--------|-------------|-------------|
| `ConversionOptions.setQuality(int)` | Stelt het PNG‑compressieniveau in (0‑100). | Verminder de bestandsgrootte voor web‑assets. |
| `ConversionOptions.setBackgroundColor(Color)` | Forceert een achtergrondkleur (standaard is transparant). | Handig wanneer de pagina transparante secties heeft. |
| `ConversionOptions.setPageSize(PageSize)` | Overschrijft de sandbox‑grootte voor de uitvoerafbeelding. | Maak thumbnails met een andere resolutie. |

Hieronder staat een kort fragment dat een witte achtergrond en 90 % kwaliteit instelt:

```java
ConversionOptions pngOptions = new ConversionOptions(ConversionFormat.PNG);
pngOptions.setBackgroundColor(java.awt.Color.WHITE);
pngOptions.setQuality(90);

try (FileOutputStream out = new FileOutputStream("output/white_bg_page.png")) {
    Converter.convertDocument(document, pngOptions, out);
}
```

---

## Volledig Werkend Voorbeeld

Alles bij elkaar genomen, hier is het complete programma dat je kunt kopiëren‑plakken in een `SandboxResponsiveExample.java` bestand en uitvoeren:

```java
import com.aspose.html.devices.DeviceInfo;
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.ConversionOptions;
import com.aspose.html.converters.ConversionFormat;
import com.aspose.html.render.HTMLDocument;
import com.aspose.html.render.HTMLDocumentLoadOptions;
import com.aspose.html.render.Sandbox;

import java.io.FileOutputStream;

public class SandboxResponsiveExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Define a sandbox with the desired viewport (800×600) and device pixel ratio
        DeviceInfo sandboxDevice = new DeviceInfo();
        sandboxDevice.setWidth(800);
        sandboxDevice.setHeight(600);
        sandboxDevice.setDevicePixelRatio(1.0);
        sandboxDevice.setUserAgent("AsposeHTML/Java Sandbox");

        // Step 2: Load the remote HTML page inside the sandboxed environment
        HTMLDocument document = new HTMLDocument(
                "https://example.com/responsive.html",
                new HTMLDocumentLoadOptions(new Sandbox(sandboxDevice)));

        // Step 3: Convert the document to PNG – the output reflects exactly how the page looks on the defined screen size
        try (FileOutputStream out = new FileOutputStream("output/responsive_page.png")) {
            Converter.convertDocument(
                    document,
                    new ConversionOptions(ConversionFormat.PNG),
                    out);
        }

        System.out.println("Screenshot saved to output/responsive_page.png");
    }
}
```

Het uitvoeren van het programma geeft een bevestigingsregel weer en plaatst de PNG in de `output` map. Open het bestand, en je ziet een getrouwe weergave van de externe pagina op precies de grootte die je hebt opgegeven.

---

## Veelgestelde Vragen

**Q: Werkt dit met lokale HTML‑bestanden?**  
A: Absoluut. Vervang de URL door een `file://` URI of geef een `java.io.File` pad door aan de constructor van `HTMLDocument`.

**Q: Wat als ik een PDF nodig heb in plaats van PNG?**  
A: Vervang `ConversionFormat.PNG` door `ConversionFormat.PDF`. De rest van de code blijft ongewijzigd.

**Q: Kan ik een volledige (scrollende) screenshot maken?**  
A: Stel de `DeviceInfo` hoogte in op de scroll‑hoogte van de pagina (`document.getDocumentElement().getScrollHeight()`) vóór conversie, of gebruik `ConversionOptions.setPageSize` om het canvas te vergroten.

---

## Conclusie

Je weet nu **how to use sandbox** om een webpagina screenshot te maken, HTML als PNG op te slaan, en betrouwbare html to image conversion uit te voeren met Aspose.HTML for Java. De aanpak is lichtgewicht, volledig programmeerbaar, en omzeilt de overhead van traditionele headless browsers.

Wat nu? Probeer de PNG‑output te vervangen door een PDF, experimenteer met verschillende device pixel ratios om Retina‑displays na te bootsen, of automatiseer batch‑verwerking van tientallen URL's. dezelfde sandbox‑techniek kan ook worden hergebruikt voor **html to png conversion** in CI‑pipelines, visuele regressietests, of het genereren van thumbnails voor een content‑management‑systeem.

Voel je vrij om een commentaar achter te laten als je tegen problemen aanloopt, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}