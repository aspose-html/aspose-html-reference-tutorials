---
date: 2026-08-28
description: Passen Sie die XPS‑Seitengröße beim Konvertieren von HTML zu XPS in Java
  mit Aspose.HTML an. Rendern Sie HTML zu XPS mit genauen Abmessungen.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: Anpassen der XPS‑Seitengröße
og_description: Passen Sie die XPS‑Seitengröße beim Konvertieren von HTML zu XPS in
  Java mit Aspose.HTML an. Erfahren Sie, wie Sie HTML in Sekunden zu XPS mit genauen
  Abmessungen rendern.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Anpassen der XPS‑Seitengröße beim Konvertieren von HTML zu XPS in Java
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Anpassen der XPS‑Seitengröße beim Konvertieren von HTML zu XPS in Java
url: /de/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# XPS‑Seitengröße beim Konvertieren von HTML zu XPS in Java anpassen

In diesem Tutorial lernen Sie **wie Sie die XPS‑Seitengröße** beim Konvertieren von HTML zu XPS mit Aspose.HTML für Java anpassen können. Egal, ob Sie druckbare Rechnungen, Archivberichte oder benutzerdefinierte Etiketten benötigen, die Kontrolle der Seitendimensionen stellt sicher, dass das endgültige XPS genau wie gewünscht aussieht. Wir führen Sie durch die Einrichtung der Umgebung, die Rendering‑Optionen und die endgültige XPS‑Erstellung, sodass Sie diese Fähigkeit direkt in Ihre Java‑Anwendungen einbetten können.

## Schnelle Antworten
- **Was bedeutet „HTML zu XPS konvertieren“?** Es rendert ein HTML‑Dokument in eine XPS‑Datei und bewahrt Layout und Stil.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Welche Java‑Version wird unterstützt?** Java 8 oder höher (JDK 11+ empfohlen).  
- **Kann ich die Seitengröße ändern?** Ja – Aspose.HTML ermöglicht das Festlegen benutzerdefinierter Abmessungen vor dem Rendering.  
- **Wie lange dauert die Konvertierung?** In der Regel unter einer Sekunde für Standardseiten; größere Dokumente können länger dauern.

## Was bedeutet das Konvertieren von HTML zu XPS?

Das Konvertieren von HTML zu XPS bedeutet, eine web‑orientierte Markup‑Datei zu nehmen und ein XPS‑Dokument (XML Paper Specification) zu erzeugen – ein festes Layout, druckfertiges Format, ähnlich wie PDF. Dies ist nützlich, wenn Sie hochqualitative, geräteunabhängige Dokumente für die Archivierung oder den Druck aus Java‑Anwendungen benötigen.

## Warum die XPS‑Seitengröße anpassen?

Das Anpassen der XPS‑Seitengröße gibt Ihnen Kontrolle über die physischen Abmessungen des endgültigen Dokuments (z. B. A4, Letter, benutzerdefinierte Etiketten). Es verhindert unerwünschtes Skalieren, sorgt dafür, dass der Inhalt perfekt passt, und kann die Dateigröße reduzieren, indem überflüssiger Weißraum eliminiert wird.

## Wie rendert man HTML zu XPS mit einer benutzerdefinierten Seitengröße?

Laden Sie Ihr HTML, konfigurieren Sie `XpsRenderingOptions` mit einem `PageSetup`, das die genaue Breite und Höhe definiert, die Sie benötigen, und rendern Sie dann zu einem `XpsDevice`. Dieser zweistufige Ablauf ermöglicht es Ihnen, das Layout beizubehalten und gleichzeitig die von Ihnen angegebenen Abmessungen durchzusetzen, alles in einem einzigen API‑Aufruf.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllt haben:

1. **Java‑Entwicklungsumgebung** – Java Development Kit (JDK) auf Ihrem System installiert.  
2. **Aspose.HTML für Java Bibliothek** – Laden Sie die Aspose.HTML für Java Bibliothek herunter und binden Sie sie in Ihr Projekt ein. Sie finden die Bibliothek auf der [Aspose.HTML für Java Download‑Seite](https://releases.aspose.com/html/java/).  
3. **Eingabe‑HTML‑Datei** – Bereiten Sie eine HTML‑Datei vor, die Sie rendern und für die Sie die XPS‑Seitengröße anpassen möchten. Sie können Ihre eigene HTML‑Datei für dieses Tutorial verwenden.

## Pakete importieren

Die Klasse `Page` repräsentiert die Seitendimensionen und Einstellungen für die XPS‑Ausgabe. Die Klasse `HtmlRenderer` führt die Konvertierung von HTML zu XPS durch.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Schritt‑für‑Schritt‑Anleitung

Unten finden Sie eine prägnante, nummerierte Anleitung, die die ursprünglichen Schritte widerspiegelt und zusätzlichen Kontext zur Klarheit bietet.

### Schritt 1: Eingabedateinamen festlegen

Die Klasse `FileInputStream` liest Rohbytes aus einer Datei und liefert die HTML‑Quelle an den Renderer.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Schritt 2: HTML‑Dokument erstellen und Stile festlegen

Die Klasse `HTMLDocument` repräsentiert ein im Speicher befindliches HTML‑DOM, das von Aspose.HTML zum Rendern verwendet wird.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Schritt 3: XPS‑Rendering‑Optionen erstellen

Die Klasse `XpsRenderingOptions` enthält Einstellungen, die steuern, wie HTML zu XPS gerendert wird, z. B. Seitengröße und Bildqualität.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Schritt 4: Seitengröße anpassen  

**Wie man die XPS‑Seitengröße festlegt** – Definieren Sie eine benutzerdefinierte Seitengröße (Breite × Höhe in Punkten) und geben Sie dem Renderer an, ob er automatisch auf die breiteste Seite erweitern soll. Das Setzen von `adjustToWidestPage` auf `false` bewahrt die genauen von Ihnen angegebenen Abmessungen.

Die Klasse `PageSetup` definiert Seitengröße, Ränder und Ausrichtung für die XPS‑Ausgabe.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Schritt 5: Ausgabe rendern

Die Klasse `XpsDevice` ist das Rendering‑Ziel, das den verarbeiteten Inhalt in eine XPS‑Datei schreibt.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Häufige Probleme und Lösungen

| Problem | Warum es passiert | Lösung |
|-------|----------------|-----|
| **Leere XPS‑Ausgabe** | Eingabestream nicht geschlossen oder HTMLDocument verweist auf die falsche Datei. | Stellen Sie sicher, dass der `FileInputStream` korrekt in einem try‑with‑resources‑Block eingebettet ist und der Dateipfad exakt ist. |
| **Seitengröße nicht angewendet** | `adjustToWidestPage` bleibt auf `true` gesetzt. | Setzen Sie `pageSetup.setAdjustToWidestPage(false);` wie in Schritt 4 gezeigt. |
| **Nicht unterstütztes CSS** | Aspose.HTML unterstützt nur einen Teil von CSS. | Verwenden Sie grundlegendes Layout, Schriftarten und Farben; vermeiden Sie fortgeschrittene Selektoren oder CSS‑Grid. |
| **LicenseException** | Ausführung ohne gültige Lizenz in der Produktion. | Wenden Sie Ihre temporäre oder gekaufte Lizenz vor dem Rendering an (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Häufig gestellte Fragen

**Q: Was ist Aspose.HTML für Java?**  
A: Aspose.HTML für Java ist eine Java‑Bibliothek, die Entwicklern ermöglicht, HTML‑Dokumente zu manipulieren und in verschiedene Formate wie XPS, PDF und Bilder zu konvertieren. Sie können die Bibliothek von der [Aspose.HTML für Java Download‑Seite](https://releases.aspose.com/html/java/) herunterladen.

**Q: Wo kann ich Aspose.HTML für Java herunterladen?**  
A: Sie können die Aspose.HTML für Java Bibliothek von der [Aspose Produktveröffentlichungs‑Seite](https://releases.aspose.com/) herunterladen.

**Q: Gibt es eine kostenlose Testversion für Aspose.HTML für Java?**  
A: Ja, Sie können eine kostenlose Testversion von Aspose.HTML für Java über die [Seite für temporäre Lizenzanfrage](https://purchase.aspose.com/temporary-license/) erhalten.

**Q: Wie kann ich eine temporäre Lizenz für Aspose.HTML für Java erhalten?**  
A: Um eine temporäre Lizenz für Aspose.HTML für Java zu erhalten, besuchen Sie die [Seite für temporäre Lizenzanfrage](https://purchase.aspose.com/temporary-license/).

**Q: Kann ich Support für Aspose.HTML für Java erhalten?**  
A: Ja, Sie können Hilfe und Support von der Aspose‑Community im [Aspose‑Forum](https://forum.aspose.com/) erhalten.

**Q: Kann ich HTML zu XPS auf einem headless‑Server konvertieren?**  
A: Absolut. Aspose.HTML funktioniert in Umgebungen ohne GUI; stellen Sie lediglich sicher, dass die Java‑Laufzeit korrekt konfiguriert ist.

**Q: Unterstützt die Bibliothek benutzerdefinierte Seitenränder?**  
A: Ja. Verwenden Sie `PageSetup.setMarginTop()`, `setMarginBottom()` usw., bevor Sie das `PageSetup` den Rendering‑Optionen zuweisen.

## Fazit

Wir haben den vollständigen Prozess des **Konvertierens von HTML zu XPS** und **Anpassens der XPS‑Seitengröße** mit Aspose.HTML für Java durchlaufen. Wenn Sie diesen Schritten folgen, können Sie druckfertige XPS‑Dokumente erzeugen, die exakt Ihren Layout‑Anforderungen entsprechen. Experimentieren Sie gern mit verschiedenen Seitengrößen, Stilen oder fügen Sie sogar Kopf‑ und Fußzeilen hinzu, um den Bedürfnissen Ihres Projekts gerecht zu werden.

Wenn Sie Fragen haben oder weitere Unterstützung benötigen, schauen Sie in die [Aspose.HTML für Java Dokumentation](https://reference.aspose.com/html/java/) oder beteiligen Sie sich an der Diskussion im [Aspose‑Forum](https://forum.aspose.com/).

---

**Zuletzt aktualisiert:** 2026-08-28  
**Getestet mit:** Aspose.HTML für Java 24.11 (zum Zeitpunkt des Schreibens aktuell)  
**Autor:** Aspose

## Verwandte Tutorials

- [HTML zu XPS konvertieren mit Aspose.HTML für Java](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [PDF‑Seitengröße anpassen mit Aspose.HTML für Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [EPUB zu XPS Konvertierung mit Aspose.HTML für Java](/html/java/converting-epub-to-xps/convert-epub-to-xps/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}