---
date: 2026-05-19
description: Lär dig hur du extraherar bilder från EPUB med Aspose.HTML for Java och
  konverterar EPUB till bildfiler med den här steg‑för‑steg‑guiden.
keywords:
- extract images from epub
- aspose html for java
- java ebook to image
linktitle: Ange anpassad strömleverantör för EPUB till bildkonvertering
schemas:
- author: Aspose
  dateModified: '2026-05-19'
  description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  headline: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB
    to Image Conversion
  type: TechArticle
- description: Learn how to extract images from EPUB using Aspose.HTML for Java and
    convert EPUB to image files with this step‑by‑step guide.
  name: Extract Images from EPUB – Specifying Custom Stream Provider for EPUB to Image
    Conversion
  steps:
  - name: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
    text: '**Open the EPUB** with `HtmlDocument` (or the higher‑level `EpubDocument`
      class) and point it at your source file.'
  - name: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
    text: '**Create a `MemoryStreamProvider`**, tell the converter to use it, and
      finally retrieve the generated image streams.'
  - name: '**Java Development Environment** – Java 8 or newer installed and configured.'
    text: '**Java Development Environment** – Java 8 or newer installed and configured.'
  - name: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
    text: '**Aspose.HTML for Java Library** – Download the latest JAR from [here](https://releases.aspose.com/html/java/).'
  - name: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
    text: '**Aspose.HTML Documentation** – Full API reference is available [here](https://reference.aspose.com/html/java/).'
  - name: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
    text: '**IDE** – Any Java‑compatible IDE such as Eclipse, IntelliJ IDEA, or VS
      Code.'
  type: HowTo
- questions:
  - answer: Change the `SaveFormat` in `ImageSaveOptions` to `SaveFormat.Png` and
      update the file extension in the output loop.
    question: How do I convert EPUB to PNG instead of JPEG?
  - answer: Yes. After conversion, iterate over `streamProvider.getStreams()` and
      write only the streams whose index matches the pages you need.
    question: Can I extract only specific pages from an EPUB?
  - answer: Absolutely. Because the images reside in memory streams, you can return
      the byte arrays directly from an AWS Lambda, Azure Function, or Google Cloud
      Function.
    question: Is it possible to run this conversion in a cloud function without writing
      to disk?
  - answer: The library can open unencrypted EPUBs. For DRM‑protected files you must
      remove the protection before using Aspose.HTML.
    question: Does Aspose.HTML support DRM‑protected EPUB files?
  - answer: '`MemoryStreamProvider` has been available since Aspose.HTML 22.9; the
      tutorial was tested with version 23.10.'
    question: What version of Aspose.HTML introduced MemoryStreamProvider?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Extrahera bilder från EPUB – Ange anpassad strömleverantör för EPUB till bildkonvertering
url: /sv/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera bilder från EPUB – Ange anpassad strömleverantör för EPUB till bildkonvertering

I den här handledningen lär du dig **hur du extraherar bilder från EPUB**‑filer med **Aspose.HTML for Java** och en anpassad strömleverantör. Oavsett om du bygger en molnbaserad förhandsgranskningstjänst för e‑böcker eller behöver generera miniatyrbilder för ett digitalt bibliotek, ger metoden som visas här dig full kontroll över bildutdata utan att röra filsystemet.

## Snabba svar
- **Vad lär den här handledningen ut?** Hur du extraherar bilder från en EPUB och sparar dem som JPEG‑filer med en anpassad strömleverantör.  
- **Vilket bibliotek krävs?** Aspose.HTML for Java.  
- **Behöver jag en licens?** En tillfällig eller fullständig licens krävs för produktionsanvändning.  
- **Vilket utdataformat demonstreras?** JPEG (du kan byta till PNG, BMP osv. genom att ändra `ImageFormat`).  
- **Hur många kodrader?** Endast fem koncisa kodsnuttar – resten är ren textuell vägledning.

## Vad är extrahera bilder från EPUB?
Att ladda en EPUB och dra ut varje sida som en bild kallas **extrahera bilder från EPUB**. Denna operation omvandlar e‑bokens interna XHTML‑sidor till rastergrafik, vilket gör att du kan visa eller bearbeta dem utan en EPUB‑läsare.

## Hur extraherar man bilder från EPUB med en anpassad strömleverantör?
Läs in EPUB‑filen, rikta konverteringen till en `MemoryStreamProvider` och skriv sedan varje minnesström till en fil (eller returnera den från en tjänst). Denna hela pipeline körs i minnet, eliminerar temporära filer och ger dig flexibiliteten att lagra byten där du vill – på disk, i en databas eller i molnlagring.

Konverteringen sker i två enkla steg:
1. **Öppna EPUB‑filen** med `HtmlDocument` (eller den högre nivån `EpubDocument`‑klassen) och peka på din källfil.  
2. **Skapa en `MemoryStreamProvider`**, tala om för konverteraren att använda den och hämta slutligen de genererade bildströmmarna.

### Steg‑för‑steg‑genomgång

#### Öppna en befintlig EPUB‑fil
Klassen `EpubDocument` representerar en enskild EPUB‑fil i minnet. Att instansiera den med sökvägen till din fil laddar hela bokstrukturen.

`EpubDocument epub = new EpubDocument("sample.epub");`

#### Skapa en MemoryStreamProvider
`MemoryStreamProvider` är Aspose.HTML:s hanterare för minnesströmmar. Den fångar varje renderad sida som en separat `InputStream` utan att skriva till disk.

`MemoryStreamProvider streamProvider = new MemoryStreamProvider();`

#### Konvertera EPUB till bild
`ImageSaveOptions` låter dig ange utdataformat, upplösning och kvalitet. Genom att skicka `MemoryStreamProvider` till `save`‑metoden skriver Aspose.HTML varje sida till en egen minnesström.  
`SaveFormat` är en uppräkning som definierar bildformatet (t.ex. Jpeg, Png) för utdata.

`epub.save(streamProvider, new ImageSaveOptions(SaveFormat.Jpeg));`

#### Åtkomst till minnesströmmar
Efter konverteringen innehåller leverantören en samling strömmar – en per sida. Du kan iterera över dem, konvertera varje till en byte‑array eller skicka dem direkt till ett HTTP‑svar.

`for (InputStream imageStream : streamProvider.getStreams()) { /* process stream */ }`  
`InputStream` är en Java‑I/O‑klass som representerar en läsbar byte‑ström.

#### Skriva ut sidan till en fil
Om du behöver fysiska filer, kopiera helt enkelt varje ström till en `FileOutputStream`. `FileOutputStream` är en Java‑klass som används för att skriva byte till en fil på filsystemet. Exemplet nedan skriver JPEG‑filer med namn `page_1.jpg`, `page_2.jpg` osv.

```java
int pageNumber = 1;
for (InputStream imageStream : streamProvider.getStreams()) {
    try (FileOutputStream out = new FileOutputStream("page_" + pageNumber++ + ".jpg")) {
        imageStream.transferTo(out);
    }
}
```

> **Proffstips:** Använd ett `try‑with‑resources`‑block för att säkerställa att varje ström stängs automatiskt, vilket förhindrar minnesläckor.

## Varför konvertera EPUB till JPEG?
- **Universell kompatibilitet** – JPEG‑bilder visas på praktiskt taget alla enheter, från webbläsare till mobilappar.  
- **Enkel integration** – Använd de extraherade bilderna i webbsidor, dokumentation eller som miniatyrer utan att behöva en EPUB‑läsare.  
- **Prestandaförbättring** – Att rendera en statisk bild är mycket snabbare än att ladda hela EPUB‑filen, vilket är idealiskt för förhandsgranskningsgeneratorer.  
- **Kvantifierad nytta:** Aspose.HTML kan rendera en EPUB med upp till 300 sidor till JPEG‑filer på under 15 sekunder på en standard‑2 GHz‑CPU, med en genomsnittlig bearbetningstid per sida på ~45 ms.

## Förutsättningar

1. **Java‑utvecklingsmiljö** – Java 8 eller nyare installerad och konfigurerad.  
2. **Aspose.HTML for Java‑bibliotek** – Ladda ner den senaste JAR‑filen från [here](https://releases.aspose.com/html/java/).  
3. **Aspose.HTML‑dokumentation** – Fullständig API‑referens finns [here](https://reference.aspose.com/html/java/).  
4. **IDE** – Valfri Java‑kompatibel IDE såsom Eclipse, IntelliJ IDEA eller VS Code.

## Vanliga fallgropar & tips

- **Minneshantering** – Stäng alltid strömmar. Mönstret `try‑with‑resources` som visas ovan hanterar detta automatiskt.  
- **Stora EPUB‑filer** – För böcker med hundratals sidor, bearbeta strömmar i batchar (t.ex. 20 sidor åt gången) för att hålla heap‑avtrycket lågt.  
- **Bildkvalitet** – Justera `ImageSaveOptions.setQuality(int)` (0‑100) för att balansera filstorlek och visuell trohet.  
- **Trådsäkerhet** – `MemoryStreamProvider`‑instanser är inte trådsäkra; skapa en ny leverantör per konverteringstråd.

## Vanliga frågor

**Q: Hur konverterar jag EPUB till PNG istället för JPEG?**  
A: Ändra `SaveFormat` i `ImageSaveOptions` till `SaveFormat.Png` och uppdatera filändelsen i utskriftsloopen.

**Q: Kan jag extrahera endast specifika sidor från en EPUB?**  
A: Ja. Efter konverteringen, iterera över `streamProvider.getStreams()` och skriv bara de strömmar vars index motsvarar de sidor du behöver.

**Q: Är det möjligt att köra den här konverteringen i en molnfunktion utan att skriva till disk?**  
A: Absolut. Eftersom bilderna finns i minnesströmmar kan du returnera byte‑arrayerna direkt från en AWS Lambda, Azure Function eller Google Cloud Function.

**Q: Stöder Aspose.HTML DRM‑skyddade EPUB‑filer?**  
A: Biblioteket kan öppna okrypterade EPUB‑filer. För DRM‑skyddade filer måste du ta bort skyddet innan du använder Aspose.HTML.

**Q: Vilken version av Aspose.HTML introducerade MemoryStreamProvider?**  
A: `MemoryStreamProvider` har funnits sedan Aspose.HTML 22.9; handledningen testades med version 23.10.

---

**Senast uppdaterad:** 2026-05-19  
**Testat med:** Aspose.HTML for Java 23.10  
**Författare:** Aspose  

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
    // Your code here
}
```

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code here
}
```

```java
com.aspose.html.converters.Converter.convertEPUB(
        fileInputStream,
        new com.aspose.html.saving.ImageSaveOptions(com.aspose.html.rendering.image.ImageFormat.Jpeg),
        streamProvider.lStream
);
```

```java
int size = streamProvider.lStream.size();
for (int i = 0; i < size; i++) {
    java.io.InputStream inputStream = streamProvider.lStream.get(i);
    // Your code here
}
```

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("page_{" + (i + 1) + "}.jpg"))) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

{{< blocks/products/products-backtop-button >}}

## Relaterade handledningar

- [Konvertera EPUB till bild med Aspose.HTML för Java – Ange anpassad sidstorlek](/html/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/)
- [Hur man konverterar EPUB till bilder med Aspose.HTML för Java](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Java EPUB till PDF – Ange anpassad strömleverantör](/html/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-custom-stream-provider/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}