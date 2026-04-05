---
date: 2026-04-05
description: Leer hoe je PDF genereert vanuit HTML, lettertypen configureert, aangepaste
  CSS toepast, een tijdelijke licentie gebruikt en HTML naar PDF converteert in Java
  met Aspose.HTML.
keywords:
- generate pdf from html
- convert html pdf java
- add custom fonts pdf
- fonts not showing pdf
linktitle: Lettertypen configureren in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: 'PDF genereren uit HTML: Lettertypen configureren met Aspose.HTML voor Java'
url: /nl/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lettertypen configureren voor HTML‑naar‑PDF Java met Aspose.HTML

## Inleiding
In deze tutorial ontdek je hoe je **PDF uit HTML genereert** met Aspose.HTML en hoe je lettertypen configureert voor HTML‑naar‑PDF-conversie in Java. Bij het werken met HTML‑documenten zorgt het instellen van de juiste lettertypen ervoor dat de gegenereerde PDF er precies uitziet als de oorspronkelijke webpagina — met behoud van merkkleuren, typografie en lay-out. Of je nu rapporten, facturen of een ander documentgeneratie‑pipeline bouwt, een juiste lettertypeconfiguratie is de sleutel tot professioneel ogende PDF‑bestanden. Laten we het volledige proces doorlopen, van het voorbereiden van de omgeving tot het converteren van HTML naar PDF met aangepaste lettertypen en CSS.

## Snelle antwoorden
- **Wat is het primaire doel van deze tutorial?** Lettertypen configureren voor HTML‑naar‑PDF-conversie in Java met Aspose.HTML.  
- **Welke bibliotheek verwerkt de conversie?** Aspose.HTML for Java (de `Converter`‑klasse).  
- **Heb ik een licentie nodig?** Een tijdelijke Aspose‑licentie verwijdert evaluatielimieten; een volledige licentie is vereist voor productie.  
- **Waar moeten mijn aangepaste lettertypen worden geplaatst?** In een map die wordt gerefereerd door `FontsLookupFolder`, bijvoorbeeld een `fonts`‑directory naast je project.  
- **Kan ik de PDF‑uitvoer aanpassen?** Ja — gebruik `PdfSaveOptions` om paginagrootte, marges en meer aan te passen.

## Wat is **generate PDF from HTML** en waarom is lettertypeconfiguratie belangrijk?
Het **generate PDF from HTML**‑proces rendert een HTML‑document naar een PDF‑pagina. Lettertypen zijn een cruciaal onderdeel van het renderen omdat ze de lay‑out, regelafstand en visuele getrouwheid beïnvloeden. Door Aspose.HTML naar een aangepaste lettertypefolder te laten wijzen, zorg je ervoor dat de PDF exact de lettertypen gebruikt die je voor de webpagina hebt ontworpen, waardoor fallback‑lettertypen worden vermeden en merkconsistentie behouden blijft.

## Waarom Aspose.HTML gebruiken voor lettertypeconfiguratie?
- **Nauwkeurige weergave:** Ondersteunt CSS2.1 en veel CSS3‑functies, zodat je HTML er hetzelfde uitziet in PDF.  
- **Cross‑platform:** Werkt op elk OS dat Java 1.8+ ondersteunt.  
- **Licentie‑flexibiliteit:** Test met een tijdelijke licentie, schakel daarna over naar een volledige licentie voor productie.  
- **Prestaties:** Snelle conversie, zelfs voor complexe pagina’s.

## Voorvereisten
Voordat we beginnen, zorg dat je het volgende hebt:

1. **Java Development Kit (JDK) 1.8+** – de code draait op elke moderne JDK.  
2. **Aspose.HTML for Java** – download de nieuwste JAR van de [Aspose‑website](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse of een andere Java‑compatibele editor.  
4. **Basiskennis van Java** – je moet vertrouwd zijn met klassen, methoden en bestands‑I/O.  
5. **Aspose.HTML‑licentie** – een [tijdelijke licentie](https://purchase.aspose.com/temporary-license/) verwijdert evaluatiebeperkingen.

## Pakketten importeren
Importeer eerst de core Java‑ en Aspose.HTML‑klassen die je nodig hebt.  

```java
import java.io.IOException;
```

Deze imports geven je toegang tot bestandsafhandeling en de Aspose.HTML API.

## Hoe aangepaste lettertypen toe te voegen bij PDF‑generatie
Hieronder leggen we uit waarom lettertypebeheer belangrijk is, hoe je aangepaste CSS toepast, en hoe je **een tijdelijke licentie gebruikt** om volledige functionaliteit te ontgrendelen terwijl je de oplossing test.

## Stapsgewijze handleiding

### Stap 1: Maak de HTML‑inhoud
We beginnen met het genereren van een eenvoudig HTML‑bestand dat we later naar PDF converteren.

#### 1.1 Schrijf de HTML‑code
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

Dit fragment definieert een header en een alinea. Voel je vrij om de HTML uit te breiden met meer elementen als je extra stijlen wilt testen.

#### 1.2 Sla de HTML op in een bestand
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

De `FileWriter` schrijft de string naar `user-agent-fontsetting.html` in je projectmap. Na deze stap heb je een fysiek HTML‑bestand klaar voor verwerking.

### Stap 2: Configureer de Aspose.HTML‑omgeving
Nu stellen we het Aspose.HTML `Configuration`‑object in, waarmee we kunnen bepalen hoe de HTML wordt gerenderd.

#### 2.1 Maak een Configuration‑instantie
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

Het `Configuration`‑object is het startpunt voor het aanpassen van renderopties zoals lettertypebeheer en user‑agent gedrag.

#### 2.2 Toegang tot de User Agent Service
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

De `IUserAgentService` beheert stijlsheets, lettertypen en andere renderdetails. We gebruiken het om aangepaste CSS in te voegen en naar onze lettertypefolder te wijzen.

### Stap 3: Pas aangepaste stijlen en lettertypen toe
Nu de omgeving klaar is, kunnen we CSS‑regels toevoegen en Aspose.HTML vertellen waar onze lettertypen te vinden zijn.

#### 3.1 Stel aangepaste CSS in
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

Deze CSS kleurt de header bruin en de alinea grijs. Je kunt hier elke geldige CSS‑regel toevoegen — Aspose.HTML ondersteunt de volledige CSS2.1‑specificatie en veel CSS3‑functies. *(Dit is een voorbeeld van **apply custom css**.)*

#### 3.2 Verwijs naar de aangepaste lettertypefolder
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

Plaats alle `.ttf` of `.otf` bestanden die je wilt gebruiken in een map genaamd `fonts` in de root van je project. Aspose.HTML laadt deze lettertypen automatisch tijdens het renderen.

> **Pro tip:** Als je meerdere lettertypefamilies hebt, houd ze dan georganiseerd in subfolders en voeg elke bovenliggende folder toe aan `FontsLookupFolder` met een door puntkomma gescheiden lijst.

### Stap 4: Laad het HTML‑document met de configuratie
Nu laden we het HTML‑bestand dat we eerder hebben gemaakt, met de aangepaste configuratie die we net hebben opgebouwd.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

Het `HTMLDocument`‑object vertegenwoordigt nu de gestylede HTML die klaar is voor conversie.

### Stap 5: Converteer HTML naar PDF
Tot slot voeren we de **aspose html pdf conversion** uit om een PDF‑bestand te produceren dat onze aangepaste lettertypen en stijlen respecteert.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

Het `PdfSaveOptions`‑object laat je outputinstellingen aanpassen zoals paginagrootte, compressie en metadata. Voor een eenvoudige conversie werken de standaardopties perfect.

### Stap 6: Ruim bronnen op
Juiste opruiming voorkomt geheugenlekken, vooral bij het verwerken van veel documenten in een langdurige applicatie.

#### 6.1 Verwijder de HTMLDocument
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 Verwijder de Configuration
```java
if (configuration != null) {
    configuration.dispose();
}
```

Deze aanroepen vrijgeven native resources die door Aspose.HTML zijn toegewezen.

## Veelvoorkomende problemen & oplossingen
| Probleem | Oplossing |
|----------|-----------|
| **Lettertypen worden niet weergegeven** | Controleer of de `fonts`‑folder correct wordt gerefereerd en geldige `.ttf`/`.otf`‑bestanden bevat. Gebruik absolute paden als de folder buiten de projectdirectory ligt. |
| **PDF ziet er leeg uit** | Zorg ervoor dat het pad naar het HTML‑bestand correct is en dat het bestand leesbaar is. Controleer of het `Configuration`‑object wordt doorgegeven aan de `HTMLDocument`‑constructor. |
| **Licentie‑exception** | Pas een tijdelijke of volledige Aspose‑licentie toe voordat je een Aspose‑API aanroept. Plaats het licentiebestand in de classpath en laad het met `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`. |
| **Onverwachte CSS‑weergave** | Aspose.HTML ondersteunt de meeste CSS, maar niet alle moderne functies (bijv. CSS Grid). Vereenvoudig de stijlen of gebruik ondersteunde CSS‑eigenschappen. |

## Veelgestelde vragen

**Q: Kan ik elk lettertype gebruiken met Aspose.HTML voor Java?**  
A: Ja, elk TrueType (`.ttf`) of OpenType (`.otf`) lettertype dat je besturingssysteem ondersteunt, kan worden gebruikt. Plaats de bestanden gewoon in de folder die je hebt ingesteld met `FontsLookupFolder`.

**Q: Heb ik een licentie nodig om Aspose.HTML voor Java te gebruiken?**  
A: Hoewel je de bibliotheek kunt evalueren zonder licentie, verwijdert een [tijdelijke Aspose‑licentie](https://purchase.aspose.com/temporary-license/) de evaluatiebeperkingen. Voor productie is een volledige licentie vereist.

**Q: Hoe kan ik de PDF‑uitvoer aanpassen?**  
A: Geef een geconfigureerde `PdfSaveOptions`‑instantie door aan `convertHTML`. Je kunt paginagrootte, marges, compressieniveau en meer instellen.

**Q: Is het mogelijk om complexere CSS‑stijlen toe te passen?**  
A: Ja, Aspose.HTML ondersteunt een breed scala aan CSS. Complexe selectors, media‑queries en pseudo‑classes werken zoals in een browser, hoewel sommige zeer nieuwe CSS3/4‑functies mogelijk niet volledig worden ondersteund.

**Q: Waar vind ik meer voorbeelden en documentatie?**  
A: Bezoek de officiële [Aspose.HTML for Java documentatiepagina](https://reference.aspose.com/html/java/) voor gedetailleerde API‑referenties en extra code‑samples.

**Q: Hoe beïnvloedt de tijdelijke Aspose‑licentie de conversie?**  
A: De tijdelijke licentie verwijdert de 10‑pagina‑limiet en het watermerk dat in de evaluatiemodus verschijnt, waardoor je de **aspose html pdf conversion** workflow volledig kunt testen.

---

**Laatst bijgewerkt:** 2026-04-05  
**Getest met:** Aspose.HTML for Java 24.12 (latest at time of writing)  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}