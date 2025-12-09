---
date: 2025-11-29
description: Erfahren Sie, wie Sie HTML mit Aspose.HTML für Java in XPS konvertieren
  und die XPS‑Seitengröße anpassen. Steuern Sie die Ausgabedimensionen ganz einfach.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: HTML in XPS konvertieren und XPS‑Seitengröße mit Aspose.HTML für Java anpassen
url: /de/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML in XPS konvertieren und XPS‑Seitengröße anpassen mit Aspose.HTML für Java

In diesem Tutorial erfahren Sie **wie Sie HTML in XPS konvertieren** und die resultierende Seitengröße mit Aspose.HTML für Java feinjustieren. Egal, ob Sie druckbare Berichte, Rechnungen oder Archivdokumente erstellen, die Kontrolle über die XPS‑Abmessungen sorgt dafür, dass die Ausgabe exakt so aussieht, wie Sie es erwarten. Wir führen Sie Schritt für Schritt durch den gesamten Prozess – von der Einrichtung der Umgebung bis zum Rendern der finalen XPS‑Datei – sodass Sie diese Funktion sofort in Ihre Java‑Anwendungen integrieren können.

## Schnelle Antworten
- **Was bedeutet “HTML in XPS konvertieren”?** Es rendert ein HTML‑Dokument in eine XPS‑Datei und bewahrt dabei Layout und Styling.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert für die Entwicklung; für den Produktionseinsatz ist eine kommerzielle Lizenz erforderlich.  
- **Welche Java‑Version wird unterstützt?** Java 8 oder höher (JDK 11+ empfohlen).  
- **Kann ich die Seitengröße ändern?** Ja – Aspose.HTML ermöglicht das Festlegen benutzerdefinierter Abmessungen vor dem Rendern.  
- **Wie lange dauert die Konvertierung?** In der Regel unter einer Sekunde für Standardseiten; größere Dokumente können länger benötigen.

## Was bedeutet das Konvertieren von HTML zu XPS?
Das Konvertieren von HTML zu XPS bedeutet, dass eine web‑orientierte Markup‑Datei in ein XPS‑Dokument (XML Paper Specification) umgewandelt wird – ein festes Layout‑Format, das druckfertig ist und dem PDF ähnelt. Dies ist nützlich, wenn Sie hochqualitative, geräteunabhängige Dokumente für die Archivierung oder den Druck aus Java‑Anwendungen benötigen.

## Warum die XPS‑Seitengröße anpassen?
Das Anpassen der Seitengröße gibt Ihnen die Kontrolle über die physischen Abmessungen des finalen Dokuments (z. B. A4, Letter, benutzerdefinierte Etiketten). Es verhindert unerwünschtes Skalieren, sorgt dafür, dass der Inhalt perfekt passt, und kann die Dateigröße reduzieren, indem überflüssiger Weißraum eliminiert wird.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

1. **Java Development Environment** – Java Development Kit (JDK) auf Ihrem System installiert.  
2. **Aspose.HTML for Java Library** – Laden Sie die Aspose.HTML for Java‑Bibliothek herunter und binden Sie sie in Ihr Projekt ein. Sie finden die Bibliothek [hier](https://releases.aspose.com/html/java/).  
3. **Input HTML File** – Bereiten Sie eine HTML‑Datei vor, die Sie rendern und deren XPS‑Seitengröße Sie anpassen möchten. Sie können für dieses Tutorial Ihre eigene HTML‑Datei verwenden.

## Pakete importieren

Zuerst importieren Sie die Klassen, die Sie benötigen. Diese Pakete geben Ihnen Zugriff auf Dokumenten‑Handling, Rendering und Seiteneinrichtungs‑Funktionen.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Schritt 1: Eingabedateinamen festlegen

Lesen Sie die Quell‑HTML‑Datei mit einem `FileInputStream`. Dieser Stream liefert das rohe HTML an die Aspose.HTML‑Engine.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Schritt 2: HTML‑Dokument erstellen und Stile festlegen

Erstellen Sie eine `HTMLDocument`‑Instanz, die den Inhalt repräsentiert, den Sie rendern möchten. In diesem Beispiel fügen wir einen kleinen CSS‑Block ein, um das Styling zu demonstrieren – ersetzen Sie ihn gern durch Ihr eigenes Markup.

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

## Schritt 3: XPS‑Renderoptionen erstellen

Instanziieren Sie `XpsRenderingOptions`, um alle Einstellungen zu halten, die die Konvertierung von HTML zu XPS beeinflussen.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Schritt 4: Seitengröße anpassen

Definieren Sie eine benutzerdefinierte Seitengröße (Breite × Höhe in Punkten) und geben Sie dem Renderer an, ob er automatisch auf die breiteste Seite erweitern soll. Das Setzen von `adjustToWidestPage` auf `false` bewahrt die exakt angegebenen Abmessungen.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Schritt 5: Ausgabe rendern

Erstellen Sie schließlich ein `XpsDevice` mit den konfigurierten Optionen und rendern Sie das HTML‑Dokument. Das Ergebnis ist eine vollständig erzeugte XPS‑Datei mit den von Ihnen festgelegten benutzerdefinierten Seitendimensionen.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Häufige Probleme und Lösungen

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **Leere XPS‑Ausgabe** | Der Input‑Stream wurde nicht geschlossen oder `HTMLDocument` verweist auf die falsche Datei. | Stellen Sie sicher, dass der `FileInputStream` korrekt in einem try‑with‑resources‑Block eingebettet ist und der Dateipfad exakt ist. |
| **Seitengröße wird nicht übernommen** | `adjustToWidestPage` blieb auf `true` gesetzt. | Setzen Sie `pageSetup.setAdjustToWidestPage(false);` wie in Schritt 4 gezeigt. |
| **Nicht unterstütztes CSS** | Aspose.HTML unterstützt nur einen Teil von CSS. | Bleiben Sie bei grundlegenden Layouts, Schriftarten und Farben; vermeiden Sie fortgeschrittene Selektoren oder CSS‑Grid. |
| **LicenseException** | Ausführung ohne gültige Lizenz in der Produktion. | Laden Sie Ihre temporäre oder gekaufte Lizenz vor dem Rendern (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Häufig gestellte Fragen

**F: Was ist Aspose.HTML für Java?**  
A: Aspose.HTML für Java ist eine Java‑Bibliothek, die Entwicklern ermöglicht, HTML‑Dokumente zu manipulieren und in verschiedene Formate wie XPS, PDF und Bilder zu konvertieren.

**F: Wo kann ich Aspose.HTML für Java herunterladen?**  
A: Sie können die Aspose.HTML für Java‑Bibliothek von [diesem Link](https://releases.aspose.com/html/java/) herunterladen.

**F: Gibt es eine kostenlose Testversion von Aspose.HTML für Java?**  
A: Ja, Sie können eine kostenlose Testversion von Aspose.HTML für Java [hier](https://releases.aspose.com/) erhalten.

**F: Wie erhalte ich eine temporäre Lizenz für Aspose.HTML für Java?**  
A: Um eine temporäre Lizenz für Aspose.HTML für Java zu erhalten, besuchen Sie [diese Seite](https://purchase.aspose.com/temporary-license/).

**F: Kann ich Support für Aspose.HTML für Java erhalten?**  
A: Ja, Sie können Hilfe und Support von der Aspose‑Community im [Aspose Forum](https://forum.aspose.com/) erhalten.

**F: Kann ich HTML auf einem headless Server in XPS konvertieren?**  
A: Absolut. Aspose.HTML funktioniert in Umgebungen ohne GUI; stellen Sie lediglich sicher, dass die Java‑Runtime korrekt konfiguriert ist.

**F: Unterstützt die Bibliothek benutzerdefinierte Seitenränder?**  
A: Ja. Verwenden Sie `PageSetup.setMarginTop()`, `setMarginBottom()` usw., bevor Sie das `PageSetup` den Renderoptionen zuweisen.

## Fazit

Wir haben den kompletten Prozess **HTML in XPS konvertieren** und die Seitengröße mit Aspose.HTML für Java durchlaufen. Durch Befolgen dieser Schritte können Sie druckfertige XPS‑Dokumente erzeugen, die exakt Ihren Layout‑Anforderungen entsprechen. Experimentieren Sie gern mit verschiedenen Seitengrößen, Stilen oder fügen Sie Header und Footer hinzu, um Ihr Projekt optimal zu unterstützen.

Wenn Sie Fragen haben oder weitere Unterstützung benötigen, lesen Sie die [Aspose.HTML für Java‑Dokumentation](https://reference.aspose.com/html/java/) oder treten Sie im [Aspose Forum](https://forum.aspose.com/) in den Austausch.

---

**Last Updated:** 2025-11-29  
**Tested With:** Aspose.HTML for Java 24.11 (latest at time of writing)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}