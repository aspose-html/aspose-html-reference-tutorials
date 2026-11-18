---
category: general
date: 2026-03-20
description: Stel de user agent in een sandbox in om de paginatitel te extraheren
  met headless HTML-rendering – leer hoe je de DPI van het apparaat instelt en een
  sandbox‑instantie maakt.
draft: false
keywords:
- set user agent
- extract page title
- set device dpi
- create sandbox instance
- headless html rendering
language: nl
og_description: Stel de user‑agent in een sandbox in, haal de paginatitel op en beheer
  de DPI van het apparaat voor betrouwbare headless HTML‑rendering.
og_title: Stel de User Agent in voor headless HTML-rendering – Complete gids
tags:
- Java
- Web Scraping
- Headless Rendering
title: Stel de user agent in voor headless HTML-rendering – Complete gids
url: /nl/java/configuring-environment/set-user-agent-for-headless-html-rendering-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Stel User Agent in voor Headless HTML Rendering – Complete Gids

Heb je ooit **user agent moeten instellen** tijdens het scrapen van een site, maar wist je niet hoe dit de gerenderde pagina beïnvloedt? Je bent niet de enige. In veel headless‑scenario's bepaalt de server welke HTML te sturen op basis van de UA‑string, dus het correct instellen kan het verschil betekenen tussen een lege pagina en de inhoud die je echt nodig hebt.  

In deze tutorial lopen we door het configureren van een sandbox, **een sandbox‑instance maken**, het aanpassen van de **device DPI**, en uiteindelijk **het extraheren van de paginatitel** uit een **headless HTML rendering**‑sessie. Geen poespas—alleen een uitvoerbaar Java‑voorbeeld dat je vandaag nog in je project kunt gebruiken.

> **Pro tip:** Als je al Aspose.HTML (of een vergelijkbare bibliotheek) gebruikt, komen de onderstaande stappen 1‑op‑1 overeen met de API. Als je een andere stack gebruikt, beschouw de sandbox dan als elke headless‑browser‑context (Playwright, Selenium, enz.).

## Wat je gaat bouwen

- Een sandbox met een aangepaste **user‑agent**‑string.
- DPI‑bewuste rendering zodat CSS‑eenheden (pt, in, cm) zich gedragen als een echt scherm.
- Een nette manier om **de paginatitel te extraheren** nadat de pagina volledig is gerenderd.
- Een zelfstandige Java‑klasse die je vanaf de commandoregel kunt uitvoeren.

Vereisten? Alleen Java 8+ en de Aspose.HTML for Java JAR op je classpath. Niets anders.

---

## User Agent instellen en Sandbox configureren

Het eerste wat je moet doen is de rendering‑engine vertellen welke browser je wilt nabootsen. Dit gebeurt via de `SandboxConfiguration#setUserAgent`‑methode.

```java
import com.aspose.html.Sandbox;
import com.aspose.html.SandboxConfiguration;
import com.aspose.html.HTMLDocument;

/* Step 1: Configure the sandbox – screen size, DPI, and user‑agent */
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
sandboxConfig.setScreenSize(1280, 800);      // width × height in pixels
sandboxConfig.setDeviceDPI(96);              // DPI for CSS unit conversion
sandboxConfig.setUserAgent("AsposeHTML/1.0"); // <-- set user agent
```

Waarom is dit belangrijk? Veel sites leveren een vereenvoudigde lay-out aan onbekende agents (denk aan “bot”) en verbergen de gegevens die je echt nodig hebt. Door een echte browser na te bootsen, lok je de server om de volledige pagina te retourneren.

![set user agent configuratie](/images/set-user-agent.png "Illustratie van set user agent in sandbox configuratie")

*Afbeeldingsalt‑tekst: screenshot van set user agent configuratie.*

## Sandbox‑instance maken voor Headless HTML Rendering

Zodra de configuratie klaar is, start je de sandbox. Beschouw het als het starten van een headless Chrome die alleen in het geheugen leeft.

```java
/* Step 2: Create the sandbox using the configuration */
try (Sandbox sandboxInstance = new Sandbox(sandboxConfig)) {
    // The sandbox is now ready for rendering tasks.
    // Anything you do inside this block runs headlessly.
}
```

Het gebruik van het try‑with‑resources‑patroon garandeert dat de sandbox correct wordt vrijgegeven, waardoor native resources worden vrijgemaakt. Als je vergeet deze te sluiten, kun je geheugen of bestands‑handles lekken—iets wat ik vaak bij nieuwkomers zie.

## Device DPI instellen voor nauwkeurige CSS‑rendering

De `setDeviceDPI`‑aanroep is niet alleen een extra; het beïnvloedt direct hoe CSS‑eenheden zoals `pt` of `mm` worden berekend. Als je facturen, PDF’s of een layout‑gevoelige pagina rendert, zorgt het afstemmen op de gewenste DPI ervoor dat je screenshots of geëxtraheerde data er precies zo uitzien als op een echt scherm.

Je hebt de aanroep al gezien in het configuratiesnippet, maar hier is een snelle sanity‑check:

```java
int dpi = sandboxConfig.getDeviceDPI(); // should return 96
System.out.println("Sandbox DPI set to: " + dpi);
```

Als je een hogere resolutie nodig hebt (bijv. voor retina‑achtige assets), verhoog je de waarde naar `144` of `192`. Vergeet niet de schermgrootte proportioneel te houden; anders kan de lay-out overlopen.

## Paginatitel extraheren uit gerenderd document

Nu de sandbox draait, laad je een pagina en haal je de titel op. De `HTMLDocument#getTitle`‑methode leest de `<title>`‑tag *nadat* de DOM van de pagina volledig is geparseerd.

```java
/* Step 3: Load a web page inside the sandboxed environment */
HTMLDocument htmlDoc = new HTMLDocument(sandboxInstance, "https://example.com");

/* Step 4: Work with the rendered document – extract its title */
String pageTitle = htmlDoc.getTitle();
System.out.println("Title: " + pageTitle);
```

Het uitvoeren van het bovenstaande tegen `https://example.com` geeft het volgende weer:

```
Title: Example Domain
```

Dat is de **extract page title**‑stap in actie. Als de site JavaScript gebruikt om de titel dynamisch in te stellen, zal de sandbox het script uitvoeren (mits je scripting hebt ingeschakeld, wat standaard aan staat). Als je ooit een lege string ziet, controleer dan of de pagina daadwerkelijk een `<title>`‑element bevat nadat scripts zijn uitgevoerd.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is een complete, kant‑klaar te‑runnen klasse. Voel je vrij om te copy‑pasten in `Main.java` en uit te voeren `javac Main.java && java Main`.

```java
import com.aspose.html.Sandbox;
import com.aspose.html.SandboxConfiguration;
import com.aspose.html.HTMLDocument;

/**
 * Demonstrates how to set user agent, configure DPI,
 * create a sandbox instance, and extract the page title
 * using headless HTML rendering.
 */
public class Main {
    public static void main(String[] args) {
        // 1️⃣ Configure sandbox: screen, DPI, and user‑agent
        SandboxConfiguration config = new SandboxConfiguration();
        config.setScreenSize(1280, 800);
        config.setDeviceDPI(96);
        config.setUserAgent("AsposeHTML/1.0"); // <-- set user agent

        // 2️⃣ Create sandbox (auto‑close with try‑with‑resources)
        try (Sandbox sandbox = new Sandbox(config);
             // 3️⃣ Load the page inside the sandbox
             HTMLDocument doc = new HTMLDocument(sandbox, "https://example.com")) {

            // 4️⃣ Extract and print the title
            String title = doc.getTitle();
            System.out.println("Title: " + title);
        } catch (Exception e) {
            // Simple error handling – in real code you might log this
            System.err.println("Rendering failed: " + e.getMessage());
        }
    }
}
```

### Verwachte output

```
Title: Example Domain
```

Als je `https://example.com` vervangt door een andere URL, zie je de titel van die pagina—mits de site geen headless agents blokkeert. Dat is de volledige **headless HTML rendering**‑pipeline in minder dan 30 regels Java.

---

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als de site onbekende UAs blokkeert?* | Gebruik een veelvoorkomende browser‑string, bijv. `"Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/119.0 Safari/537.36"`. De sandbox laat je elke willekeurige UA instellen. |
| *Moet ik JavaScript inschakelen?* | Deze staat standaard aan. Als je het eerder hebt uitgeschakeld, roep dan `config.setEnableJavaScript(true)` aan. |
| *Hoe maak ik een screenshot in plaats van alleen de titel?* | Na het laden van het document, roep `htmlDoc.save("page.png", SaveFormat.PNG)` aan. De DPI die je eerder hebt ingesteld, beïnvloedt de afbeeldingsgrootte. |
| *Kan ik meerdere pagina’s in één sandbox renderen?* | Ja. Hergebruik hetzelfde `Sandbox`‑object; maak gewoon nieuwe `HTMLDocument`‑objecten aan voor elke URL. |
| *Wat betreft HTTPS‑certificaten?* | De sandbox vertrouwt de standaard Java‑keystore. Voor zelf‑ondertekende certificaten, importeer ze in de JVM‑truststore of schakel verificatie uit via `config.setIgnoreCertificateErrors(true)`. |

## Tips voor productie‑klaar scrapen

1. **User Agents roteren** – Houd een lijst met populaire UA‑strings bij en kies er willekeurig één per verzoek. Dit verkleint de kans op een blokkering.
2. **Respecteer Robots.txt** – Ook al ben je headless, ethisch scrapen betekent dat je het crawl‑beleid van de site respecteert.
3. **Beperk verzoeken** – Voeg een `Thread.sleep(500)` toe tussen oproepen om te voorkomen dat je de server overbelast.
4. **Cache gerenderde HTML** – Als je dezelfde pagina herhaaldelijk nodig hebt, sla de HTML op schijf op en hergebruik deze; renderen is CPU‑intensief.
5. **Monitor geheugen** – De sandbox houdt native resources vast. In langdurige jobs, roep periodiek `System.gc()` aan of herstart de sandbox na een batch URL’s.

## Conclusie

Je weet nu hoe je **user agent moet instellen** voor betrouwbare **headless HTML rendering**, de **device DPI** configureert, een **sandbox‑instance maakt**, en **de paginatitel extrahert** in een nette Java‑workflow. Het volledige voorbeeld hierboven werkt direct, print de titel, en laat ruimte voor uitbreidingen zoals screenshots of PDF‑conversie.

Probeer nu de URL te vervangen door een site die verschillende content serveert op basis van de UA‑string, of experimenteer met hogere DPI‑waarden om te zien hoe CSS‑lay-outs verschuiven. Je kunt ook de `HTMLDocument.save`‑overloads van de bibliotheek verkennen om PDF’s te genereren—een handige manier om gerenderde pagina’s te archiveren.

Veel plezier met coderen, en moge je scrapers onopgemerkt blijven!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}