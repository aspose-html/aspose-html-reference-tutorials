---
date: 2025-12-01
description: Erfahren Sie, wie Sie die PDF‑Seitengröße anpassen, HTML als PDF rendern
  und PDF aus HTML mit Aspose.HTML für Java erzeugen. Steuern Sie die Seitenabmessungen
  ganz einfach.
linktitle: Adjusting PDF Page Size
second_title: Java HTML Processing with Aspose.HTML
title: PDF‑Seitengröße mit Aspose.HTML für Java anpassen
url: /de/java/advanced-usage/adjust-pdf-page-size/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF-Seitengröße mit Aspose.HTML für Java anpassen

Das Erzeugen von PDFs aus HTML ist ein häufiges Bedürfnis für Berichte, Rechnungen und E‑Books. Wenn Sie **die PDF‑Seitengröße anpassen**, stellen Sie sicher, dass das endgültige Dokument dem Layout entspricht, das Sie in HTML entworfen haben. In diesem Tutorial lernen Sie, wie Sie HTML als PDF rendern, benutzerdefinierte Abmessungen festlegen und steuern, ob die Seite automatisch an die breiteste Inhaltselemente erweitert wird. Wir gehen Schritt für Schritt durch ein vollständiges Praxisbeispiel mit Aspose.HTML für Java.

## Schnelle Antworten
- **Was bedeutet „PDF‑Seitengröße anpassen“?** Sie können die Breite und Höhe jeder PDF‑Seite definieren oder den Renderer automatisch die breiteste Komponente anpassen lassen.  
- **Welche Bibliothek wird verwendet?** Aspose.HTML für Java (neueste Version).  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion reicht für die Entwicklung; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich die Abmessungen programmgesteuert ändern?** Ja – verwenden Sie `PageSetup` und die Eigenschaft `AdjustToWidestPage`.  
- **Ist das mit Java 8+ kompatibel?** Absolut – die API funktioniert mit jedem JDK 8 oder neuer.

## Was bedeutet „PDF‑Seitengröße anpassen“?
Die Anpassung der PDF‑Seitengröße bedeutet, die Abmessungen jeder Seite zu konfigurieren, die der HTML‑Renderer erzeugt. Sie können eine feste Größe (z. B. A4, Letter) festlegen oder den Renderer die optimale Breite basierend auf dem Inhalt berechnen lassen. Das gibt Ihnen präzise Kontrolle über Layout, Seitennummerierung und visuelle Treue.

## Warum PDF‑Seitengröße beim Konvertieren von HTML zu PDF anpassen?
- **Design‑Intention bewahren:** Verhindern Sie, dass Inhalte abgeschnitten oder verzerrt werden.  
- **Für den Druck optimieren:** Passen Sie die Papiergröße an die Anforderungen nachgelagerter Prozesse an.  
- **Lesbarkeit verbessern:** Vermeiden Sie übermäßigen Weißraum oder gedrückten Text.  
- **Dynamische Dokumente:** Breite Tabellen oder Bilder passen sich automatisch an, ohne manuelle Berechnungen.

## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

- **Java Development Kit (JDK) 8 oder höher** auf Ihrem Rechner installiert.  
- **Aspose.HTML für Java** – laden Sie das neueste JAR von der [offiziellen Release‑Seite](https://releases.aspose.com/html/java/) herunter.  
- **Eine HTML‑Datei**, die Sie konvertieren möchten (wir verwenden `FirstFile.html` im Beispiel).  

## Pakete importieren
Zuerst importieren wir die Klassen, die wir benötigen. Der untenstehende Code‑Block bleibt unverändert gegenüber dem Original‑Tutorial.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.rendering.pdf.PdfRenderingOptions;
import com.aspose.html.drawing.Size;
import com.aspose.html.rendering.PageSetup;
```

## Schritt 1: HTML‑Inhalt lesen
Wir lesen die Quell‑HTML‑Datei mit einem `FileInputStream`. Dieser Schritt bereitet das rohe Markup für die spätere Manipulation vor.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("FirstFile.html"))) {
```

## Schritt 2: HTML schreiben (und optional anreichern)
Hier kopieren wir das ursprüngliche HTML in eine neue Datei und fügen ein paar Inline‑Styles ein, um zu demonstrieren, wie das Styling das PDF‑Ergebnis beeinflusst. Ersetzen Sie das Beispiel‑CSS gern durch Ihr eigenes.

```java
try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("FirstFileOut.html"))) {
    byte[] bytes = new byte[fileInputStream.available()];
    fileInputStream.read(bytes);
    fileOutputStream.write(bytes);
    // Add custom HTML styles or content here
    String style = "<style>\n" +
                   ".st\n" +
                   "{\n" +
                   "color:\n" +
                   "green;\n" +
                   "}\n" +
                   "</style >\n" +
                   "<div id = id1 > Aspose.Html rendering Text in Black Color</div >\n" +
                   "<div id = id2 class='' st '' > Aspose.Html rendering Text in Green Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: blue;' > Aspose.Html rendering Text in Blue Color</div >\n" +
                   "<div id = id3 class='' st '' style = 'color: red;' ><font face = 'Arial' > Aspose.Html rendering Text in Red\n" +
                   "Color</font ></div >\n";
    fileOutputStream.write(style.getBytes(java.nio.charset.StandardCharsets.UTF_8));
}
```

## Schritt 3: HTML zu PDF rendern – Zwei Szenarien
Nun sehen wir, wie man **PDF aus HTML generiert** mit zwei unterschiedlichen Seitengrößen‑Strategien.

### 3.1 Seitengröße NICHT an Inhaltsbreite angepasst
In diesem Fall fixieren wir die Seitendimensionen (100 × 100 Points). Überschreitet ein Element diese Grenzen, wird es abgeschnitten.

```java
String pdf_output;
com.aspose.html.rendering.HtmlRenderer pdf_renderer = new com.aspose.html.rendering.HtmlRenderer();

// Create an HTMLDocument instance from the HTML file
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument(Resources.output("FirstFileOut.html"));

// Set PDF rendering options
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(false);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("not-adjusted-to-widest-page_out.pdf");
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

### 3.2 Seitengröße an Inhaltsbreite ANPASSEN
Hier aktivieren wir `AdjustToWidestPage`, sodass der Renderer die Seitenbreite automatisch erweitert, um das breiteste Element aufzunehmen, während die Höhe fest bleibt.

```java
com.aspose.html.rendering.pdf.PdfRenderingOptions pdf_options = new com.aspose.html.rendering.pdf.PdfRenderingOptions();
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100)));
pageSetup.setAdjustToWidestPage(true);
pdf_options.setPageSetup(pageSetup);

pdf_output = Resources.output("adjusted-to-widest-page_out.pdf");
device = new com.aspose.html.rendering.pdf.PdfDevice(pdf_options, pdf_output);

// Render the output
pdf_renderer.render(device, html_document);
```

## Wie man PDF‑Abmessungen (wie man PDF‑Seitengröße ändert) im Code festlegt
Das `PageSetup`‑Objekt ist der Schlüssel:

- `setAnyPage(Page page)`: definiert die Basis‑Breite × Höhe.  
- `setAdjustToWidestPage(boolean)`: schaltet das automatische Erweitern ein oder aus.  

Durch Anpassen dieser beiden Eigenschaften können Sie **PDF‑Abmessungen** für jedes Szenario festlegen, egal ob Sie eine statische A4‑Seite oder eine dynamische Breite benötigen, die Ihrem HTML‑Layout folgt.

## Häufige Probleme & Tipps
| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| Inhalt wird abgeschnitten | Die feste Größe ist zu klein | Erhöhen Sie die `Size`‑Werte oder aktivieren Sie `AdjustToWidestPage`. |
| Text wirkt unscharf | Standard‑DPI beim Rendern ist niedrig | Verwenden Sie `PdfRenderingOptions.setResolution(int dpi)`, um die Qualität zu erhöhen. |
| Styles fehlen | Externes CSS nicht geladen | Betten Sie CSS inline ein oder verwenden Sie `HTMLDocument.setBaseUrl()`, um auf Ihren Stylesheet‑Ordner zu verweisen. |
| Große HTML-Dateien verursachen OutOfMemoryError | Der Renderer lädt das gesamte Dokument in den Speicher | Verarbeiten Sie das Dokument in Teilen oder erhöhen Sie den JVM‑Heap (`-Xmx`). |

## Häufig gestellte Fragen

**Q: Was ist Aspose.HTML für Java?**  
A: Es ist eine Java‑Bibliothek, mit der Sie HTML‑Dokumente erstellen, bearbeiten und rendern können, einschließlich Konvertierung zu PDF, PNG und anderen Formaten.

**Q: Wie kann ich die PDF‑Seitengröße beim Konvertieren von HTML zu PDF mit Aspose.HTML für Java anpassen?**  
A: Verwenden Sie die Klasse `PageSetup` und setzen Sie `AdjustToWidestPage` auf `true` (automatisch) oder `false` (fest). Dann weisen Sie die gewünschte `Size` über `new Page(new Size(width, height))` zu.

**Q: Kann ich das Styling von HTML‑Inhalten vor der Konvertierung zu PDF anpassen?**  
A: Ja – Sie können CSS einfügen, das DOM modifizieren oder externe Stylesheets nutzen. Das Tutorial zeigt die Inline‑CSS‑Injektion.

**Q: Wo finde ich die Dokumentation für Aspose.HTML für Java?**  
A: Umfassende Dokumentation ist [hier](https://reference.aspose.com/html/java/) verfügbar.

**Q: Gibt es eine kostenlose Testversion für Aspose.HTML für Java?**  
A: Absolut – laden Sie eine Testversion von der [Release‑Seite](https://releases.aspose.com/html/java/) herunter.

## Fazit
Sie wissen jetzt, wie Sie **PDF‑Seitengröße anpassen**, **HTML als PDF rendern** und **benutzerdefinierte PDF‑Abmessungen** mit Aspose.HTML für Java festlegen. Experimentieren Sie mit verschiedenen Seitengrößen, DPI‑Einstellungen und CSS‑Anpassungen, um das Ergebnis für Ihren Anwendungsfall zu perfektionieren. Bei Problemen konsultieren Sie die offizielle Dokumentation oder die Aspose‑Support‑Foren.

---

**Letzte Aktualisierung:** 2025-12-01  
**Getestet mit:** Aspose.HTML für Java 24.12 (neueste)  
**Autor:** Aspose  
**Verwandte Ressourcen:** [API Reference](https://reference.aspose.com/html/java/) | [Download Free Trial](https://releases.aspose.com/html/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}