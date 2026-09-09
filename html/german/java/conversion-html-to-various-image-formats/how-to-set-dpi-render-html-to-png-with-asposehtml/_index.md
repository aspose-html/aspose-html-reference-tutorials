---
category: general
date: 2026-01-14
description: Wie man DPI beim Konvertieren einer URL zu PNG einstellt. Lernen Sie,
  HTML zu PNG zu rendern, die Viewport-Größe festzulegen und HTML mit Aspose.HTML
  in Java als PNG zu speichern.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: de
og_description: Wie man DPI beim Konvertieren einer URL zu PNG festlegt. Schritt‑für‑Schritt‑Anleitung
  zum Rendern von HTML zu PNG, zur Steuerung der Viewport‑Größe und zum Speichern
  von HTML als PNG mit Aspose.HTML.
og_title: Wie man DPI einstellt – HTML zu PNG rendern mit AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: Wie man DPI einstellt – HTML zu PNG rendern mit AsposeHTML
url: /de/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man DPI festlegt – HTML zu PNG rendern mit AsposeHTML

Haben Sie sich jemals gefragt, **wie man DPI** für ein screenshot‑ähnliches Bild, das aus einer Webseite erzeugt wird, festlegt? Vielleicht benötigen Sie ein 300 DPI PNG für den Druck oder ein niedrigauflösendes Thumbnail für eine mobile App. In beiden Fällen besteht der Trick darin, der Rendering‑Engine das gewünschte logische DPI mitzuteilen und sie dann die schwere Arbeit erledigen zu lassen.  

In diesem Tutorial nehmen wir eine Live‑URL, rendern sie zu einer PNG‑Datei, **setzen die Viewport‑Größe**, passen das DPI an und speichern schließlich **HTML als PNG** – alles mit Aspose.HTML für Java. Keine externen Browser, keine unübersichtlichen Befehlszeilentools – nur sauberer Java‑Code, den Sie in jedes Maven‑ oder Gradle‑Projekt einbinden können.

> **Pro‑Tipp:** Wenn Sie nur ein schnelles Thumbnail benötigen, können Sie das DPI bei 96 DPI belassen (der Standard für die meisten Bildschirme). Für druckfertige Assets erhöhen Sie es auf 300 DPI oder mehr.

![Beispiel für DPI-Einstellung](https://example.com/images/how-to-set-dpi.png "Beispiel für DPI-Einstellung")

## Was Sie benötigen

- **Java 17** (oder ein aktuelles JDK).  
- **Aspose.HTML for Java** 24.10 oder neuer. Sie können es von Maven Central beziehen:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Eine Internetverbindung, um die Zielseite abzurufen (das Beispiel verwendet `https://example.com/sample.html`).  
- Schreibberechtigung für den Ausgabepfad.

Das war's – kein Selenium, kein Headless‑Chrome. Aspose.HTML führt das Rendering im Prozess aus, was bedeutet, dass Sie innerhalb der JVM bleiben und den Aufwand für das Starten eines Browsers vermeiden.

## Schritt 1 – HTML‑Dokument von einer URL laden

Zuerst erstellen wir eine `HTMLDocument`‑Instanz, die auf die Seite zeigt, die wir erfassen möchten. Der Konstruktor lädt das HTML automatisch herunter, parsed es und bereitet das DOM vor.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Warum das wichtig ist:* Durch das direkte Laden des Dokuments entfallen separate HTTP‑Clients. Aspose.HTML berücksichtigt Weiterleitungen, Cookies und sogar die Basisauthentifizierung, wenn Sie Anmeldeinformationen in die URL einbetten.

## Schritt 2 – Sandbox mit gewünschtem DPI und Viewport erstellen

Eine **Sandbox** ist Aspose.HTMLs Methode, eine Browser‑Umgebung zu simulieren. Hier lassen wir sie so tun, als wäre sie ein 1280 × 720‑Bildschirm und setzen dabei entscheidend das **Device‑DPI**. Das Ändern des DPI verändert die Pixeldichte des gerenderten Bildes, ohne die logische Größe zu ändern.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Warum Sie diese Werte anpassen könnten:*  
- **Viewport‑Größe** steuert, wie CSS‑Media‑Queries (`@media (max-width: …)`) reagieren.  
- **Device‑DPI** beeinflusst die physische Größe des Bildes beim Druck. Ein 96 DPI‑Bild sieht auf Bildschirmen gut aus; ein 300 DPI‑Bild behält die Schärfe auf Papier bei.

Wenn Sie ein quadratisches Thumbnail benötigen, ändern Sie einfach `setViewportSize(500, 500)` und lassen das DPI niedrig.

## Schritt 3 – PNG als Ausgabeformat wählen

Aspose.HTML unterstützt mehrere Rasterformate (PNG, JPEG, BMP, GIF). PNG ist verlustfrei, was es ideal für Screenshots macht, bei denen jeder Pixel erhalten bleiben soll.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Sie können außerdem die Kompressionsstufe anpassen (`pngOptions.setCompressionLevel(9)`), falls Sie sich um die Dateigröße sorgen.

## Schritt 4 – Bild rendern und speichern

Jetzt lassen wir das Dokument **sich selbst** als Bild **speichern**. Die `save`‑Methode erwartet einen Dateipfad und die zuvor konfigurierten Optionen.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Wenn das Programm beendet ist, finden Sie eine PNG‑Datei unter `YOUR_DIRECTORY/sandboxed.png`. Öffnen Sie sie – wenn Sie das DPI auf 300 gesetzt haben, wird das Bild‑Metadaten‑Tag dies widerspiegeln, obwohl die Pixelabmessungen weiterhin 1280 × 720 betragen.

## Schritt 5 – DPI überprüfen (optional, aber praktisch)

Wenn Sie sicherstellen möchten, dass das DPI wirklich angewendet wurde, können Sie die PNG‑Metadaten mit einer leichten Bibliothek wie **metadata‑extractor** auslesen:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Sie sollten `300` (oder den von Ihnen gesetzten Wert) in der Konsole ausgegeben sehen. Dieser Schritt ist für das Rendering nicht erforderlich, aber er dient als schneller Plausibilitätstest, besonders wenn Sie Assets für einen Druck‑Workflow erzeugen.

## Häufige Fragen & Sonderfälle

### „Was ist, wenn die Seite JavaScript verwendet, um Inhalte zu laden?“

Aspose.HTML führt einen **eingeschränkten Teil** von JavaScript aus. Für die meisten statischen Seiten funktioniert es sofort. Wenn die Seite stark von clientseitigen Frameworks (React, Angular, Vue) abhängt, müssen Sie die Seite eventuell vor‑rendern oder stattdessen einen Headless‑Browser verwenden. Das Setzen des DPI funktioniert jedoch genauso, sobald das DOM bereit ist.

### „Kann ich ein PDF statt PNG rendern?“

Natürlich. Ersetzen Sie `ImageSaveOptions` durch `PdfSaveOptions` und ändern Sie die Ausgabedateierweiterung zu `.pdf`. Die DPI‑Einstellung beeinflusst weiterhin das gerasterte Erscheinungsbild eingebetteter Bilder.

### „Wie sieht es mit hochauflösenden Screenshots für Retina‑Displays aus?“

Verdoppeln Sie einfach die Viewport‑Abmessungen bei gleichbleibendem DPI von 96 DPI, oder behalten Sie den Viewport bei und erhöhen das DPI auf 192. Das resultierende PNG enthält dann doppelt so viele Pixel und liefert das scharfe Retina‑Gefühl.

### „Muss ich Ressourcen aufräumen?“

`HTMLDocument` implementiert `AutoCloseable`. In einer Produktions‑App sollten Sie es in einem try‑with‑resources‑Block einbetten:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

Damit werden native Ressourcen umgehend freigegeben.

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das komplette, sofort ausführbare Programm. Ersetzen Sie `YOUR_DIRECTORY` durch einen tatsächlichen Ordner auf Ihrem Rechner.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Führen Sie die Klasse aus, und Sie erhalten ein PNG, das die von Ihnen festgelegte **DPI‑Einstellung** berücksichtigt.

## Fazit

Wir haben gezeigt, **wie man DPI festlegt**, wenn Sie **HTML zu PNG rendern**, den Schritt **Viewport‑Größe setzen** behandelt und Ihnen gezeigt, wie Sie **HTML als PNG speichern** mit Aspose.HTML für Java. Die wichtigsten Erkenntnisse sind:

- Verwenden Sie eine **Sandbox**, um DPI und Viewport zu steuern.  
- Wählen Sie die passenden **ImageSaveOptions** für verlustfreie Ausgabe.  
- Überprüfen Sie die DPI‑Metadaten, wenn Sie Druckqualität garantieren müssen.

Ab hier können Sie mit verschiedenen DPI‑Werten, größeren Viewports oder sogar einer Batch‑Verarbeitung einer URL‑Liste experimentieren. Möchten Sie eine komplette Website in PNG‑Thumbnails umwandeln? Durchlaufen Sie einfach ein Array von URLs und verwenden Sie dieselbe Sandbox‑Konfiguration erneut.

Viel Spaß beim Rendern, und möge Ihr Screenshot immer pixel‑perfekt sein!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}