---
category: general
date: 2026-02-14
description: Wie man DPI für die SVG-zu-PNG-Konvertierung mit Java festlegt. Exportieren
  Sie hochauflösende PNGs, lernen Sie, SVG in PNG zu konvertieren, und verwenden Sie
  eine Java-Bildkonvertierungsbibliothek.
draft: false
keywords:
- how to set dpi
- convert svg to png
- export high resolution png
- how to convert svg
- java image conversion library
language: de
og_description: Wie man DPI für die SVG‑zu‑PNG‑Konvertierung mit Java festlegt. Dieser
  Leitfaden zeigt, wie man hochauflösende PNGs exportiert und eine Java‑Bildkonvertierungsbibliothek
  verwendet.
og_title: Wie man DPI beim Konvertieren von SVG zu PNG mit Java festlegt
tags:
- java
- image-conversion
- svg
- png
title: Wie man DPI beim Konvertieren von SVG nach PNG mit Java festlegt
url: /de/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/
---

answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man DPI beim Konvertieren von SVG zu PNG mit Java einstellt

Haben Sie sich jemals gefragt, **wie man DPI** für eine SVG‑zu‑PNG‑Konvertierung festlegt, damit das Ergebnis auf einem druckfertigen Poster scharf aussieht? Sie sind nicht der Einzige. In vielen Projekten – denken Sie an Marketing‑Flyer, UI‑Mock‑Ups oder technische Diagramme – ist es unverzichtbar, ein hochauflösendes PNG aus einer SVG zu erhalten.  

In diesem Tutorial gehen wir die genauen Schritte durch, um **SVG zu PNG zu konvertieren**, **hochauflösendes PNG zu exportieren** und, am wichtigsten, die DPI mit der Aspose.HTML for Java‑Bibliothek zu steuern. Am Ende haben Sie ein wiederverwendbares Snippet, das Sie in jede Java‑Anwendung einbinden können, egal ob Sie ein Desktop‑Tool oder einen Backend‑Service bauen.

## Was Sie benötigen

- **Java 8+** (der Code kompiliert mit jedem aktuellen JDK)
- **Aspose.HTML for Java** JARs (verfügbar über Maven Central oder die Aspose‑Website)
- Eine SVG‑Datei, die Sie rasterisieren möchten  
- Ein bisschen Neugier – sonst nichts.

Wenn Sie mit Maven vertraut sind, fügen Sie einfach die im nächsten Abschnitt gezeigte Abhängigkeit hinzu; andernfalls laden Sie die JARs manuell herunter und fügen sie Ihrem Klassenpfad hinzu.

## Schritt 1: Die Java‑Bildkonvertierungsbibliothek hinzufügen

Zuerst muss Ihr Projekt die **java image conversion library** enthalten, die tatsächlich weiß, wie man SVG liest und PNG schreibt. Aspose.HTML ist eine solide Wahl, weil es CSS, Schriftarten und komplexe Vektor‑Features out of the box unterstützt.

**Maven‑Benutzer** können das Folgende in Ihre `pom.xml` einfügen:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- use the latest stable version -->
</dependency>
```

**Gradle‑Fans** können hinzufügen:

```gradle
implementation 'com.aspose:aspose-html:23.12'
```

Wenn Sie den manuellen Weg bevorzugen, laden Sie das JAR von der Aspose‑Download‑Seite herunter und legen Sie es in `libs/` ab, dann fügen Sie es Ihrem IDE‑Build‑Pfad hinzu.

> **Pro‑Tipp:** Achten Sie auf die Versionsnummer; neuere Releases verbessern oft die DPI‑Verarbeitung und beheben Randfall‑Bugs.

## Schritt 2: Konvertierungsoptionen erstellen und die gewünschte DPI festlegen

Jetzt, wo die Bibliothek eingebunden ist, müssen wir ihr sagen, *wie* das Ausgabe‑PNG aussehen soll. Hier kommt das zentrale Stichwort – **wie man DPI einstellt** – ins Spiel. Die Klasse `ImageConversionOptions` gibt Ihnen feine Kontrolle über die horizontale (`dpiX`) und vertikale (`dpiY`) Auflösung.

```java
import com.aspose.html.converters.ImageConversionOptions;

// Step 2: Build the options object and set DPI
ImageConversionOptions conversionOptions = new ImageConversionOptions();
conversionOptions.setDpiX(300); // 300 DPI horizontally
conversionOptions.setDpiY(300); // 300 DPI vertically
```

Warum 300 DPI? Für die meisten Druck‑Workflows gelten 300 dots‑per‑inch als „Druckqualität“. Wenn Sie nur Web‑Assets erzeugen, können Sie das auf 72 oder 96 DPI reduzieren, um die Dateigröße klein zu halten.

> **Was, wenn ich unterschiedliche DPI‑Werte für Breite und Höhe brauche?**  
> Ändern Sie einfach `setDpiX` und `setDpiY` unabhängig voneinander. Die Bibliothek unterstützt nicht‑uniforme Werte, was bei anamorphischen Bildern praktisch ist.

## Schritt 3: Die SVG‑zu‑PNG‑Konvertierung durchführen

Mit den vorbereiteten Optionen ist die eigentliche Konvertierung ein einziger statischer Aufruf. Wir verwenden `java.nio.file.Paths`, um plattformunabhängig zu bleiben.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;

public class SvgToPng {
    public static void main(String[] args) throws Exception {
        // Paths to input SVG and output PNG
        var inputSvg  = Paths.get("YOUR_DIRECTORY/input.svg").toUri();
        var outputPng = Paths.get("YOUR_DIRECTORY/output.png").toUri();

        // Convert using the DPI settings we defined earlier
        Converter.convert(inputSvg, outputPng, conversionOptions);
    }
}
```

Das war’s – führen Sie die `main`‑Methode aus und Sie finden ein scharfes 300 DPI‑PNG in `YOUR_DIRECTORY`. Die Bibliothek skaliert die Vektorgrafik automatisch auf die von Ihnen angegebene DPI, wobei Seitenverhältnis und Textschärfe erhalten bleiben.

## Schritt 4: Das Ergebnis überprüfen (optional, aber empfohlen)

Ein kurzer Plausibilitätstest kann später Kopfschmerzen ersparen. Öffnen Sie das erzeugte PNG in einem Bildbetrachter, der DPI‑Metadaten anzeigt (z. B. Photoshop, GIMP oder sogar der „Details“-Tab im Windows‑Explorer). Dort sollte **300 DPI** unter horizontaler und vertikaler Auflösung stehen.

Wenn die Datei unscharf wirkt, prüfen Sie:

1. Ob die ursprüngliche SVG nicht bereits eine niedrige Auflösung hat (Vektordateien sind auflösungsunabhängig, aber eingebettete Rasterbilder können die Qualität begrenzen).  
2. Ob Sie die Datei wirklich nach dem Setzen der DPI gespeichert haben – IDEs cachen manchmal alte Builds.  
3. Ob die Konvertierungsoptionen nicht an anderer Stelle im Code überschrieben wurden.

## Warum DPI für den Export hochauflösender PNGs wichtig ist

Sie fragen sich vielleicht: „Warum überhaupt DPI? Ist PNG nicht nur Pixel?“ Die Wahrheit ist, dass DPI ein *Metadaten‑Tag* ist, das nachgelagerten Anwendungen (insbesondere druckorientierten) sagt, wie viele Pixel einem Zoll physischen Raums entsprechen. Wenn Sie einem Drucker ein 1200 × 800 PNG ohne korrekte DPI‑Metadaten geben, nimmt er möglicherweise einen Standardwert (oft 72 DPI) an und vergrößert das Bild, was zu unscharfen Ausgaben führt.

Die korrekte DPI‑Einstellung ist zudem ein Performance‑Vorteil: Sie vermeiden ein späteres Upscaling von Rasterbildern, das rechenintensiv ist und die Qualität mindert.

## Randfälle & häufige Stolperfallen

| Situation | Worauf zu achten ist | Wie zu beheben |
|-----------|----------------------|----------------|
| **SVG enthält eingebettete Bitmap‑Bilder** | Das eingebettete Bitmap kann eine niedrige Auflösung haben, wodurch das endgültige PNG selbst bei hoher DPI pixelig aussieht. | Ersetzen Sie das Bitmap durch eine höherauflösende Version oder bearbeiten Sie das SVG, um ein externes Bild zu referenzieren. |
| **Große DPI‑Werte (z. B. 1200 DPI)** | Der Speicherverbrauch steigt stark; es kann zu einem `OutOfMemoryError` kommen. | Erhöhen Sie die JVM‑Heap‑Größe (`-Xmx2g`) oder begrenzen Sie die DPI auf ein sinnvolles Maximum für Ihren Anwendungsfall. |
| **Nicht‑quadratische Pixel** | Einige Anzeigen interpretieren DPI unterschiedlich, was zu gestreckten Bildern führt. | Stellen Sie sicher, dass `setDpiX` gleich `setDpiY` ist, es sei denn, Sie haben einen konkreten Grund für eine Abweichung. |
| **Fehlende Schriftarten** | Text im SVG kann auf eine Standardschriftart zurückgreifen und das Layout verändern. | Betten Sie Schriftarten im SVG ein oder installieren Sie die erforderlichen Schriftarten auf der Laufzeitmaschine. |

## Kurzfassung (in einem Satz)

Um **wie man DPI einstellt** für eine SVG‑zu‑PNG‑Konvertierung, erstellen Sie ein `ImageConversionOptions`‑Objekt, setzen `dpiX`/`dpiY` und rufen `Converter.convert` aus der Aspose.HTML Java‑Bibliothek auf.

## Nächste Schritte & verwandte Themen

- **Batch‑Verarbeitung:** Durchlaufen Sie ein Verzeichnis von SVG‑Dateien und wenden Sie dieselben DPI‑Einstellungen an.  
- **Dynamische DPI:** Lesen Sie eine Konfigurationsdatei oder ein Befehlszeilenargument, um die DPI zur Laufzeit festzulegen.  
- **Alternative Bibliotheken:** Wenn Sie Aspose nicht verwenden können, erwägen Sie **Batik** (Apache) oder **SVG Salamander**, obwohl sie möglicherweise zusätzlichen Code zur DPI‑Handhabung benötigen.  
- **Export hochauflösendes PNG** für Android‑Assets: Kombinieren Sie diese Technik mit Androids `drawable‑hdpi`, `xhdpi` usw. Ordnern.

Experimentieren Sie gern – probieren Sie 72 DPI für Web‑Thumbnails, 600 DPI für großformatige Drucke oder sogar 150 DPI als Mittelwert. Der Code bleibt gleich; nur die Zahlen ändern sich.

---

![wie man DPI einstellt](placeholder-image.png "Illustration der DPI‑Einstellung im Java‑Konvertierungs‑Workflow")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}