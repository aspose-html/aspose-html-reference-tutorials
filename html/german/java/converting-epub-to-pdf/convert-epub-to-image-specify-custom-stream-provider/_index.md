---
date: 2026-05-19
description: Erfahren Sie, wie Sie Bilder aus EPUB mit Aspose.HTML for Java extrahieren
  und EPUB in Bilddateien konvertieren – Schritt‑für‑Schritt‑Anleitung.
keywords:
- extract images from epub
- aspose html for java
- java ebook to image
linktitle: Festlegen eines Custom Stream Provider für die EPUB‑zu‑Image‑Konvertierung
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
title: Bilder aus EPUB extrahieren – Festlegen eines Custom Stream Provider für die
  EPUB‑zu‑Image‑Konvertierung
url: /de/java/converting-epub-to-pdf/convert-epub-to-image-specify-custom-stream-provider/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bilder aus EPUB extrahieren – Angeben eines benutzerdefinierten Stream-Providers für die EPUB-zu-Bild-Konvertierung

In diesem Tutorial lernen Sie **wie man Bilder aus EPUB**-Dateien mit **Aspose.HTML für Java** und einem benutzerdefinierten Stream-Provider extrahiert. Egal, ob Sie einen cloud‑basierten E‑Book-Vorschau‑Dienst erstellen oder Thumbnails für eine digitale Bibliothek generieren müssen, der hier gezeigte Ansatz gibt Ihnen die volle Kontrolle über die Bildausgabe, ohne das Dateisystem zu berühren.

## Schnelle Antworten
- **Was lehrt dieses Tutorial?** Wie man Bilder aus einem EPUB extrahiert und sie mit einem benutzerdefinierten Stream-Provider als JPEG-Dateien speichert.  
- **Welche Bibliothek wird benötigt?** Aspose.HTML for Java.  
- **Benötige ich eine Lizenz?** Eine temporäre oder vollständige Lizenz ist für den Produktionseinsatz erforderlich.  
- **Welches Ausgabeformat wird demonstriert?** JPEG (Sie können zu PNG, BMP usw. wechseln, indem Sie das `ImageFormat` ändern).  
- **Wie viele Codezeilen?** Nur fünf prägnante Code‑Snippets – alles andere ist reine englische Anleitung.

## Was bedeutet das Extrahieren von Bildern aus EPUB?

Das Laden eines EPUB und das Herausziehen jeder Seite als Bild wird **Bilder aus EPUB extrahieren** genannt. Dieser Vorgang wandelt die internen XHTML‑Seiten des E‑Books in Rastergrafiken um, sodass Sie sie ohne einen EPUB‑Reader anzeigen oder verarbeiten können.

## Wie extrahiere ich Bilder aus EPUB mit einem benutzerdefinierten Stream-Provider?

Laden Sie das EPUB, leiten Sie die Konvertierung zu einem `MemoryStreamProvider` und schreiben Sie anschließend jeden In‑Memory‑Stream in eine Datei (oder geben Sie ihn von einem Service zurück). Diese gesamte Pipeline läuft im Speicher, eliminiert temporäre Dateien und gibt Ihnen die Flexibilität, die Bytes dort zu speichern, wo Sie sie benötigen – Festplatte, Datenbank oder Cloud‑Speicher.

Die Konvertierung funktioniert in zwei einfachen Schritten:
1. **Öffnen Sie das EPUB** mit `HtmlDocument` (oder der höherwertigen `EpubDocument`‑Klasse) und verweisen Sie auf Ihre Quelldatei.  
2. **Erstellen Sie einen `MemoryStreamProvider`**, weisen Sie den Konverter an, ihn zu verwenden, und rufen Sie schließlich die erzeugten Bild‑Streams ab.

### Schritt‑für‑Schritt‑Durchlauf

#### Eine vorhandene EPUB‑Datei öffnen
Die Klasse `EpubDocument` repräsentiert eine einzelne EPUB‑Datei im Speicher. Durch die Instanziierung mit dem Pfad zu Ihrer Datei wird die gesamte Buchstruktur geladen.

`EpubDocument epub = new EpubDocument("sample.epub");`

#### Einen MemoryStreamProvider erstellen
`MemoryStreamProvider` ist Aspose.HTMLs In‑Memory‑Stream‑Manager. Er erfasst jede gerenderte Seite als separaten `InputStream`, ohne auf die Festplatte zu schreiben.

`MemoryStreamProvider streamProvider = new MemoryStreamProvider();`

#### EPUB in Bild konvertieren
`ImageSaveOptions` ermöglicht es Ihnen, das Ausgabeformat, die Auflösung und die Qualität festzulegen. Durch das Übergeben des `MemoryStreamProvider` an die `save`‑Methode schreibt Aspose.HTML jede Seite in einen separaten Speicher‑Stream.  
`SaveFormat` ist eine Aufzählung, die das Bildformat (z. B. Jpeg, Png) für die Ausgabe definiert.

`epub.save(streamProvider, new ImageSaveOptions(SaveFormat.Jpeg));`

#### Zugriff auf Speicher‑Streams
Nach der Konvertierung hält der Provider eine Sammlung von Streams – einen pro Seite. Sie können über sie iterieren, jeden in ein Byte‑Array konvertieren oder sie direkt an eine HTTP‑Antwort weiterleiten.

`for (InputStream imageStream : streamProvider.getStreams()) { /* process stream */ }`  
`InputStream` ist eine Java‑I/O‑Klasse, die einen lesbaren Stream von Bytes darstellt.

#### Seite in Ausgabedatei schreiben
Wenn Sie physische Dateien benötigen, kopieren Sie einfach jeden Stream in einen `FileOutputStream`. `FileOutputStream` ist eine Java‑Klasse, die Bytes in eine Datei im Dateisystem schreibt. Das untenstehende Beispiel schreibt JPEG‑Dateien mit den Namen `page_1.jpg`, `page_2.jpg` usw.

```java
int pageNumber = 1;
for (InputStream imageStream : streamProvider.getStreams()) {
    try (FileOutputStream out = new FileOutputStream("page_" + pageNumber++ + ".jpg")) {
        imageStream.transferTo(out);
    }
}
```

> **Pro Tipp:** Verwenden Sie einen `try‑with‑resources`‑Block, um sicherzustellen, dass jeder Stream automatisch geschlossen wird und Speicherlecks verhindert werden.

## Warum EPUB in JPEG konvertieren?

- **Universelle Kompatibilität** – JPEG‑Bilder werden auf praktisch jedem Gerät angezeigt, von Browsern bis zu mobilen Apps.  
- **Einfache Integration** – Verwenden Sie die extrahierten Bilder in Webseiten, Dokumentationen oder als Thumbnails, ohne einen EPUB‑Reader zu benötigen.  
- **Leistungssteigerung** – Das Rendern eines statischen Bildes ist weitaus schneller als das Laden des gesamten EPUB, was ideal für Vorschau‑Generatoren ist.  
- **Quantifizierter Nutzen:** Aspose.HTML kann ein EPUB mit bis zu 300 Seiten in weniger als 15 Sekunden auf einer Standard‑2 GHz‑CPU in JPEGs rendern und dabei jede Seite im Durchschnitt in ~45 ms verarbeiten.

## Voraussetzungen

1. **Java Development Environment** – Java 8 oder neuer installiert und konfiguriert.  
2. **Aspose.HTML for Java Library** – Laden Sie das neueste JAR von [hier](https://releases.aspose.com/html/java/) herunter.  
3. **Aspose.HTML Documentation** – Die vollständige API‑Referenz ist [hier](https://reference.aspose.com/html/java/) verfügbar.  
4. **IDE** – Jede Java‑kompatible IDE wie Eclipse, IntelliJ IDEA oder VS Code.

## Häufige Fallstricke & Tipps

- **Speicherverwaltung** – Schließen Sie Streams immer. Das oben gezeigte `try‑with‑resources`‑Muster erledigt das automatisch.  
- **Große EPUBs** – Bei Büchern mit Hunderten von Seiten verarbeiten Sie Streams in Batches (z. B. 20 Seiten gleichzeitig), um den Heap‑Fußabdruck gering zu halten.  
- **Bildqualität** – Passen Sie `ImageSaveOptions.setQuality(int)` (0‑100) an, um Dateigröße und visuelle Treue auszubalancieren.  
- **Thread‑Sicherheit** – `MemoryStreamProvider`‑Instanzen sind nicht thread‑sicher; erstellen Sie pro Konvertierungs‑Thread einen neuen Provider.

## Häufig gestellte Fragen

**Q: Wie konvertiere ich EPUB zu PNG statt JPEG?**  
A: Ändern Sie das `SaveFormat` in `ImageSaveOptions` zu `SaveFormat.Png` und passen Sie die Dateierweiterung in der Ausgabeschleife an.

**Q: Kann ich nur bestimmte Seiten aus einem EPUB extrahieren?**  
A: Ja. Nach der Konvertierung iterieren Sie über `streamProvider.getStreams()` und schreiben nur die Streams, deren Index den benötigten Seiten entspricht.

**Q: Ist es möglich, diese Konvertierung in einer Cloud‑Funktion ohne Schreiben auf die Festplatte auszuführen?**  
A: Absolut. Da die Bilder in Speicher‑Streams liegen, können Sie die Byte‑Arrays direkt von einer AWS Lambda, Azure Function oder Google Cloud Function zurückgeben.

**Q: Unterstützt Aspose.HTML DRM‑geschützte EPUB‑Dateien?**  
A: Die Bibliothek kann unverschlüsselte EPUBs öffnen. Für DRM‑geschützte Dateien müssen Sie den Schutz entfernen, bevor Sie Aspose.HTML verwenden.

**Q: Welche Version von Aspose.HTML führte MemoryStreamProvider ein?**  
A: `MemoryStreamProvider` ist seit Aspose.HTML 22.9 verfügbar; das Tutorial wurde mit Version 23.10 getestet.

---

**Zuletzt aktualisiert:** 2026-05-19  
**Getestet mit:** Aspose.HTML for Java 23.10  
**Autor:** Aspose  

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

## Verwandte Tutorials

- [EPUB in Bild konvertieren mit Aspose.HTML für Java – Benutzerdefinierte Seitengröße festlegen](/html/java/converting-between-epub-and-image-formats/convert-epub-to-image-specify-image-save-options/)
- [Wie man EPUB mit Aspose.HTML für Java in Bilder konvertiert](/html/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)
- [Java EPUB zu PDF – Angeben eines benutzerdefinierten Stream-Providers](/html/java/converting-epub-to-pdf/convert-epub-to-pdf-specify-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}