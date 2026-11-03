---
category: general
date: 2026-05-31
description: Deaktivieren Sie externe Bilder, wenn Sie eine Webseite in Java mit Aspose HTML
  zu PNG rendern. Erfahren Sie, wie Sie eine Webseite sicher in einer Sandbox laden
  und das HTML‑Dokument als PNG speichern.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: de
og_description: Deaktivieren Sie externe Bilder beim Rendern einer Webseite zu PNG
  in Java. Diese Schritt‑für‑Schritt‑Anleitung zeigt, wie man eine Webseite in einer
  Sandbox lädt und das HTML‑Dokument als PNG speichert.
og_title: Externe Bilder beim Rendern einer Webseite zu PNG in Java deaktivieren
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Externe Bilder beim Rendern einer Webseite zu PNG in Java deaktivieren
url: /de/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Externe Bilder beim Rendern einer Webseite zu PNG in Java deaktivieren

Haben Sie schon einmal **externe Bilder deaktivieren** müssen, wenn Sie eine Webseite in Java zu PNG rendern? Vielleicht bauen Sie einen Thumbnail‑Dienst, der vom öffentlichen Internet isoliert bleiben muss, oder Sie wollen einfach sicherstellen, dass während der Konvertierung keine Drittanbieter‑Bilder durchgelassen werden. So oder so, Sie sind an der richtigen Stelle gelandet.

In diesem Tutorial führen wir Sie Schritt für Schritt durch das Laden einer Webseite in einer Sandbox, das Ausschalten des Abrufs externer Bilder und schließlich das Speichern des HTML‑Dokuments als PNG‑Datei – alles mit Aspose.HTML für Java. Am Ende haben Sie ein sofort lauffähiges Beispiel sowie einige praktische Tipps, um die üblichen Stolperfallen zu vermeiden.

## Was Sie lernen werden

- **Wie man HTML zu Bild in Java rendert** mit Aspose.HTMLs `Converter`.
- Die genauen Schritte, um **eine Webseite in einer Sandbox** mit benutzerdefiniertem Viewport und DPI zu laden.
- Die Konfiguration, die nötig ist, um **externe Bilder zu deaktivieren**, während die Seite trotzdem gerendert wird.
- Wie man **ein HTML‑Dokument als PNG** (oder ein anderes unterstütztes Format) auf die Festplatte speichert.
- Umgang mit Randfällen, Performance‑Hinweise und Fehlersuche.

### Voraussetzungen

- Java 8 oder neuer installiert (der Code funktioniert auch mit JDK 11+).
- Maven oder Gradle, um die Aspose.HTML‑Bibliothek für Java zu beziehen.
- Grundlegende Kenntnisse der Java‑Syntax und des Exception‑Handlings.
- Eine Internetverbindung für den ersten Seitenabruf (es sei denn, Sie stellen das HTML lokal bereit).

> **Pro‑Tipp:** Wenn Sie hinter einem Unternehmens‑Proxy arbeiten, setzen Sie die JVM‑Eigenschaften `http.proxyHost` und `http.proxyPort`, bevor Sie das Beispiel ausführen.

---

## Schritt 1: Projekt einrichten und Aspose.HTML hinzufügen

Zuerst fügen Sie die Aspose.HTML‑Abhängigkeit hinzu. Wenn Sie Maven verwenden, platzieren Sie das Folgende in Ihrer `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Für Gradle lautet das Äquivalent:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Sobald die Bibliothek im Klassenpfad ist, können Sie mit dem Coden beginnen.

---

## Schritt 2: **Externe Bilder deaktivieren** mit einer Sandbox‑Umgebung

Der Kern der Lösung liegt in `DocumentSandbox`. Indem wir `false` für das *allowExternalImages*-Flag übergeben, weisen wir Aspose.HTML an, alle `<img>`‑Tags zu ignorieren, die auf URLs außerhalb der Sandbox verweisen. Das ist genau der Mechanismus, der **externe Bilder deaktiviert**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Warum das wichtig ist:** Ohne die Sandbox würde der Renderer versuchen, jedes Bild, das von der Seite referenziert wird, herunterzuladen – das kann langsam, unzuverlässig oder sogar ein Sicherheitsrisiko sein. Das Setzen des Flags auf `false` garantiert einen sauberen, eigenständigen Rendering‑Durchlauf.

---

## Schritt 3: **Webseite in Sandbox laden**  

Jetzt zeigen wir Aspose.HTML die URL, die wir erfassen wollen. Der Konstruktor von `HTMLDocument` akzeptiert die Sandbox‑Instanz und wendet automatisch die von uns definierten Einschränkungen an.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Wenn die Seite stark von externen Skripten für das Layout abhängt, kann es zu fehlenden Inhalten kommen, weil wir auch Skripte deaktiviert haben. In diesem Fall setzen Sie das Flag `allowExternalScripts` auf `true`, während `allowExternalImages` weiterhin `false` bleibt.

---

## Schritt 4: **Webseite zu PNG rendern**  

Nachdem das Dokument geladen ist, ist das Konvertieren zu einem Bild ein Einzeiler mit `Converter.convert`. Das Objekt `ImageSaveOptions` lässt Sie das Ausgabeformat wählen; hier wählen wir PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Die resultierende Datei `sandboxed.png` enthält einen Schnappschuss der Seite **ohne externe Bilder** – nur Inline‑SVGs oder base64‑kodierte Grafiken bleiben erhalten, falls vorhanden.

---

## Schritt 5: Ausgabe prüfen und häufige Probleme debuggen

Nach dem Ausführen des Programms öffnen Sie `sandboxed.png` in einem Bildbetrachter. Sie sollten das Seitenlayout, den Text und das CSS‑Styling sehen, aber alle `<img src="http://…">`‑Elemente werden leer sein (oft als weißes Rechteck dargestellt oder komplett weggelassen).

### Typische Stolpersteine und deren Behebung

| Symptom | Wahrscheinliche Ursache | Lösung |
|---|---|---|
| Leere Seite | Die Ziel‑URL blockiert die Anfrage (z. B. Cloudflare) | Setzen Sie passende Header im User‑Agent der Sandbox oder verwenden Sie einen Proxy. |
| Fehlende Schriften | Schriftdateien werden extern gehostet | Installieren Sie die Schriften lokal oder betten Sie sie als `@font-face` mit Data‑URIs ein. |
| Layout‑Verschiebungen | CSS‑Dateien werden extern geladen und blockiert | Setzen Sie `allowExternalScripts` nur für das Laden von CSS auf `true` und führen Sie den Vorgang erneut aus. |
| `java.lang.OutOfMemoryError` | Sehr große Seite bei hoher DPI | Reduzieren Sie die Viewport‑Größe oder DPI, oder erhöhen Sie den JVM‑Heap (`-Xmx2g`). |

---

## Schritt 6: Beispiel erweitern – Als andere Formate speichern

Der gleiche Code funktioniert für JPEG, BMP oder sogar PDF. Ändern Sie einfach das `SaveFormat`‑Enum:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Wenn Sie ein PDF benötigen, ersetzen Sie `ImageSaveOptions` durch `PdfSaveOptions` und passen die Dateierweiterung entsprechend an.

---

## Vollständiges, lauffähiges Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das **komplette, ausführbare Programm**. Erstellen Sie eine neue Java‑Klasse, fügen Sie den Code ein, stellen Sie sicher, dass das Verzeichnis `output` existiert, und führen Sie das Programm aus.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Erwartete Konsolenausgabe**:

```
PNG image saved to: output/sandboxed.png
```

Öffnen Sie `sandboxed.png` – Sie sehen die Seite gerendert **ohne externe Bilder**.

---

## Häufig gestellte Fragen

**F: Kann ich weiterhin Bilder anzeigen, die im HTML eingebettet sind?**  
A: Ja. Inline `data:`‑URIs oder base64‑kodierte Bilder werden als Teil des Dokuments behandelt und erscheinen im PNG.

**F: Was, wenn ich einige externe Bilder zulassen, andere aber blockieren möchte?**  
A: Die Sandbox funktioniert als Alles‑oder‑Nichts‑Schalter. Für feinkörnige Kontrolle laden Sie die erlaubten Bilder selbst herunter, betten sie als Data‑URIs ein und rendern dann.

**F: Funktioniert dieser Ansatz auf headless Servern?**  
A: Absolut. Aspose.HTML ist eine reine Java‑Bibliothek; sie benötigt keinen Display‑Server oder Browser‑Engine.

**F: Wie unterscheidet sich das von Selenium oder Puppeteer?**  
A: Selenium steuert einen echten Browser, was schwergewichtig und schwieriger zu sandboxen ist. Aspose.HTML rendert HTML direkt im Speicher, bietet deterministische Performance und einfachere Sicherheitskontrollen wie **externe Bilder deaktivieren**.

---

## Fazit

Sie haben nun ein solides End‑zu‑End‑Rezept, um **externe Bilder beim Rendern einer Webseite zu PNG in Java zu deaktivieren**. Durch die Nutzung von `DocumentSandbox` erhalten Sie eine strenge Kontrolle darüber, welche externen Ressourcen erlaubt sind, was sowohl Sicherheit als auch Reproduzierbarkeit gewährleistet. Von hier aus können Sie mit verschiedenen Viewport‑Größen, DPI‑Einstellungen oder Ausgabeformaten experimentieren – jede Anpassung eröffnet neue Möglichkeiten für Thumbnails, Vorschaubilder oder archivierte Snapshots.

Bereit für die nächste Herausforderung? Versuchen Sie, einen Stapel URLs parallel zu rendern, oder integrieren Sie diese Logik in einen Spring‑Boot‑Microservice, der PNGs auf Abruf liefert. Der Himmel ist das Limit, wenn Sie die Flexibilität von Aspose.HTML mit den Concurrency‑Tools von Java kombinieren.

Viel Spaß beim Coden und vergessen Sie nicht, Ihre Erfolgsgeschichten in den Kommentaren zu teilen!

## Was sollten Sie als Nächstes lernen?

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}