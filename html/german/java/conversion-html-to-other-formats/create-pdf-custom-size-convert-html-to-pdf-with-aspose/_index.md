---
category: general
date: 2026-03-26
description: Erstellen Sie PDFs mit benutzerdefinierter Größe aus HTML mit Aspose.HTML
  für Java. Erfahren Sie, wie Sie HTML in PDF konvertieren und die PDF‑Seitengröße
  in nur wenigen Schritten festlegen.
draft: false
keywords:
- create pdf custom size
- convert html to pdf
- change pdf page size
- generate pdf from html
- set pdf page size
language: de
og_description: Erstellen Sie PDFs in benutzerdefinierter Größe aus HTML mit Aspose.
  Dieser Leitfaden zeigt Ihnen, wie Sie HTML in PDF konvertieren, die PDF‑Seitengröße
  ändern und die PDF‑Seitengröße mühelos festlegen.
og_title: PDF mit benutzerdefinierter Größe erstellen – Schnellleitfaden zur Umwandlung
  von HTML in PDF
tags:
- aspose
- java
- pdf
- html
title: PDF mit benutzerdefinierter Größe erstellen – HTML mit Aspose in PDF konvertieren
url: /de/java/conversion-html-to-other-formats/create-pdf-custom-size-convert-html-to-pdf-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF mit benutzerdefinierter Größe erstellen – HTML zu PDF konvertieren mit Aspose

Haben Sie schon einmal **PDF mit benutzerdefinierter Größe** aus einer HTML‑Datei erstellen müssen? In diesem Tutorial zeigen wir Ihnen, wie Sie **HTML zu PDF** konvertieren und die PDF‑Seitengröße mit Aspose.HTML für Java festlegen.  

Wenn Sie Rechnungen, Berichte oder E‑Books erstellen, sind die genauen Seitenmaße entscheidend – sonst wirkt das Layout verschoben oder wird abgeschnitten.  

Wir gehen Schritt für Schritt durch den gesamten Prozess, vom Laden des Quell‑HTML bis zum Anpassen der Ränder, und schließen mit einem einsatzbereiten PDF ab. Keine vagen Verweise, sondern ein vollständiges, ausführbares Beispiel, das Sie noch heute kopieren‑und‑einfügen können.

## Was Sie benötigen

- **Java 17** (oder ein aktuelles JDK).  
- **Aspose.HTML for Java** JARs – Sie können die neueste Version aus dem Maven‑Repository oder von der Aspose‑Website beziehen.  
- Eine einfache `input.html`‑Datei, die Sie in einem Ordner Ihrer Wahl ablegen.  
- Eine IDE oder ein Text‑Editor Ihrer Wahl; ich programmiere meist mit IntelliJ IDEA, aber Eclipse funktioniert ebenfalls einwandfrei.

Wenn diese Voraussetzungen erfüllt sind, stoßen Sie nicht mitten im Prozess auf „class not found“-Fehler.  

Jetzt legen wir los.

![PDF mit benutzerdefinierter Größe Beispiel](/images/create-pdf-custom-size.png "Screenshot, der ein PDF mit benutzerdefinierter Seitengröße und Rändern zeigt – PDF mit benutzerdefinierter Größe erstellen")

## PDF mit benutzerdefinierter Größe – Kernschritte

Unten finden Sie das vollständige Java‑Programm, das Sie erhalten werden. Kopieren Sie es gern in eine Datei namens `ConvertHtmlToPdfCustomPage.java` und führen Sie es aus, nachdem Sie die Aspose‑Abhängigkeiten zu Ihrem Projekt hinzugefügt haben.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.PdfConversionOptions;
import com.aspose.html.saving.PageSize;
import com.aspose.html.saving.Margin;

public class ConvertHtmlToPdfCustomPage {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the source HTML document
        HTMLDocument htmlDoc = new HTMLDocument("YOUR_DIRECTORY/input.html");

        // Step 2: Set up PDF conversion options
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setPageSize(PageSize.A4); // Choose page size (A4, Letter, etc.)
        pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Portrait); // Portrait or Landscape
        pdfOptions.setMargins(new Margin(20, 20, 20, 20)); // Margins: left, top, right, bottom (points)

        // Step 3: Convert the HTML document to a PDF file with the custom settings
        Converter.convertHTML(htmlDoc, "YOUR_DIRECTORY/custom_page.pdf", pdfOptions);

        // Step 4: Inform the user that the PDF has been created
        System.out.println("PDF generated with custom page size and margins.");
    }
}
```

### Schritt 1 – HTML zu PDF konvertieren: Dokument laden

Zuerst **laden wir das HTML**, das wir in ein PDF umwandeln wollen.  
`HTMLDocument` liest die Datei, löst relative Links auf und baut ein DOM, das Aspose rendern kann.  

> **Warum das wichtig ist:** Wenn das HTML CSS oder Bilder referenziert, holt Aspose diese relativ zum Dateipfad. Ein absoluter Pfad (`YOUR_DIRECTORY/input.html`) verhindert „file not found“-Überraschungen.

### Schritt 2 – PDF‑Seitengröße ändern: Optionen konfigurieren

Hier erstellen wir ein `PdfConversionOptions`‑Objekt.  
- `setPageSize(PageSize.A4)` weist Aspose an, die Standard‑A4‑Abmessungen (210 × 297 mm) zu verwenden.  
- `setPageOrientation(...)` dreht die Seite, falls Sie Querformat benötigen.  
- `setMargins(new Margin(20, 20, 20, 20))` setzt an jeder Seite einen Rand von 20 Punkten.

Sie können `PageSize.A4` durch `PageSize.LETTER` oder sogar eine **benutzerdefinierte Größe** ersetzen, indem Sie ein `SizeF`‑Objekt übergeben, z. B.:

```java
pdfOptions.setPageSize(new SizeF(500, 800)); // width, height in points
```

> **Pro‑Tipp:** Ein Punkt entspricht 1/72 Zoll. Wenn Sie in Millimetern denken, multiplizieren Sie mit 2,83465, um Punkte zu erhalten.

### Schritt 3 – PDF aus HTML erzeugen: Konvertierung ausführen

`Converter.convertHTML` übernimmt die eigentliche Arbeit. Es nimmt das geladene `HTMLDocument`, den Ausgabepfad und die zuvor konfigurierten Optionen.  

Wenn Sie die **PDF‑Seitengröße** dynamisch anhand des Inhalts festlegen möchten, können Sie die erforderlichen Abmessungen vor diesem Schritt berechnen und `pdfOptions` entsprechend anpassen.

### Schritt 4 – Ergebnis überprüfen

Die Zeile `System.out.println` ist optional, liefert aber sofortiges Feedback, wenn Sie das Programm in einer Konsole ausführen. Nach der Ausführung öffnen Sie `custom_page.pdf` – Sie sollten ein A4‑Portrait‑PDF mit einheitlichen 20‑Punkt‑Rändern sehen, genau wie angegeben.

## HTML zu PDF – Häufige Varianten

### Einen Stream anstelle eines Dateipfads verwenden

Manchmal liegt keine physische Datei vor; das HTML kommt vielleicht aus einer Datenbank oder einer API. In diesem Fall wickeln Sie den String in einen `ByteArrayInputStream`:

```java
String htmlContent = "<html><body><h1>Hello, PDF!</h1></body></html>";
HTMLDocument htmlDoc = new HTMLDocument(
        new ByteArrayInputStream(htmlContent.getBytes(StandardCharsets.UTF_8)),
        "http://example.com/");
```

Das zweite Argument ist die Basis‑URL zum Auflösen relativer Ressourcen.

### Seitenorientierung ändern

Wenn Ihr Bericht breit ist, wechseln Sie zu Querformat:

```java
pdfOptions.setPageOrientation(PdfConversionOptions.Orientation.Landscape);
```

### Ränder feinjustieren

Ränder akzeptieren Gleitkommawerte, sodass Sie z. B. 0,5 pt für einen hauchdünnen Rand setzen können:

```java
pdfOptions.setMargins(new Margin(5.5, 10.2, 5.5, 10.2));
```

### Große HTML‑Dateien verarbeiten

Bei sehr umfangreichen Dokumenten sollten Sie **speichereffizientes Streaming** aktivieren:

```java
pdfOptions.setUseMemoryCache(true);
```

Damit schreibt Aspose Zwischendaten in temporäre Dateien, anstatt alles im RAM zu halten.

## PDF‑Seitengröße festlegen – Sonderfälle & Fallstricke

- **Fehlende Schriftarten:** Wenn Ihr HTML eine benutzerdefinierte Schrift verwendet, die nicht auf dem Server installiert ist, greift das PDF auf eine Standardschrift zurück. Betten Sie die Schrift mit `pdfOptions.getFontEmbeddingMode().setEmbeddingMode(EmbeddingMode.Always);` ein.  
- **Bildskalierung:** Hochauflösende Bilder können das PDF aufblähen. Nutzen Sie `pdfOptions.setImageResolution(150);`, um die Auflösung zu reduzieren und dennoch gute Qualität zu erhalten.  
- **CSS‑Kompatibilität:** Nicht alle CSS‑Eigenschaften werden vollständig unterstützt. Halten Sie sich an gängige Layout‑Techniken (Flexbox funktioniert, Grid kann quirlig sein).  
- **Pfad‑Berechtigungen:** Stellen Sie sicher, dass der Prozess Schreibzugriff auf `YOUR_DIRECTORY` hat. Andernfalls wird eine `IOException` ausgelöst.

## Erwartete Ausgabe

Das Ausführen des Programms erzeugt ein PDF, das etwa so aussieht (schematische Darstellung):

```
+---------------------------------------------------+
|                     Header                        |
|                                                   |
|   (HTML rendered content goes here)               |
|                                                   |
|                     Footer                        |
+---------------------------------------------------+
```

- Seitengröße: **A4** (210 × 297 mm).  
- Orientierung: **Portrait**.  
- Ränder: **20 pt** an jeder Seite.  

Öffnen Sie die Datei mit einem beliebigen PDF‑Betrachter (Adobe Reader, Chrome usw.), um das Ergebnis zu prüfen.

## Fazit

Sie wissen jetzt, wie Sie **PDF mit benutzerdefinierter Größe** aus einer HTML‑Quelle mit Aspose.HTML für Java erstellen. Das Tutorial hat die gesamte Pipeline abgedeckt: **HTML zu PDF konvertieren**, **PDF‑Seitengröße ändern**, **PDF‑Seitengröße festlegen** und **PDF aus HTML mit benutzerdefinierten Rändern generieren**.  

Experimentieren Sie gern – tauschen Sie `PageSize.LETTER` gegen Legal‑Größe aus, passen Sie die Ränder an oder betten Sie eigene Schriftarten ein. Als Nächstes könnten Sie **Wasserzeichen hinzufügen**, **das PDF verschlüsseln** oder **mehrere HTML‑Dateien stapelweise verarbeiten**. All diese Themen bauen auf den hier vorgestellten Kernkonzepten auf.

Haben Sie eine Frage zu einem speziellen Sonderfall? Hinterlassen Sie einen Kommentar unten, und ich helfe Ihnen gern beim Troubleshooting. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}