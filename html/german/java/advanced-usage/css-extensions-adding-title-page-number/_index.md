---
date: 2025-12-05
description: Erfahren Sie, wie Sie HTML‑Seitenränder in Java mit Aspose.HTML festlegen
  und Seitenzahlen sowie Titel zu Ihren Dokumenten hinzufügen.
language: de
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Wie man HTML‑Seitenränder in Java mit Aspose.HTML festlegt
url: /java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man HTML‑Seitenränder in Java mit Aspose.HTML festlegt

In diesem Tutorial erfahren Sie **wie man HTML‑Seitenränder in Java**‑Stil mit Aspose.HTML für Java setzt. Wir gehen Schritt für Schritt durch das Erstellen benutzerdefinierter Seitenränder, das Einfügen von Seitenzahlen und das Hinzufügen eines Dokumenttitels – alles mit klaren Code‑Beispielen, die Sie in Ihr eigenes Projekt übernehmen können.

## Schnelle Antworten
- **Welche Bibliothek wird benötigt?** Aspose.HTML für Java  
- **Kann ich die Ränder programmgesteuert steuern?** Ja, über eine CSS `@page`‑Regel im Benutzer‑Stylesheet  
- **Welche Ausgabeformate unterstützen Ränder?** XPS, PDF und andere Rasterformate  
- **Benötige ich eine Lizenz für die Produktion?** Eine gültige Aspose.HTML‑Lizenz ist für die Nutzung außerhalb der Testphase erforderlich  
- **Ist das mit Java 11+ kompatibel?** Absolut – die Bibliothek funktioniert mit modernen Java‑Versionen  

## Was bedeutet „HTML‑Seitenränder in Java festlegen“?
HTML‑Seitenränder in Java festzulegen bedeutet, die Rendering‑Engine (bereitgestellt von Aspose.HTML) so zu konfigurieren, dass CSS‑Page‑Box‑Eigenschaften angewendet werden, bevor das Dokument in ein druckbares Format wie XPS oder PDF konvertiert wird. Durch das Definieren einer benutzerdefinierten `@page`‑Regel steuern Sie den druckbaren Bereich, Seitenzahlen sowie Kopf‑/Fußzeilen‑Inhalte.

## Warum Aspose.HTML für die Randsteuerung verwenden?
- **Präzises Layout** – CSS `@page` gibt Ihnen pixelgenaue Kontrolle über Ränder, Kopf‑ und Fußzeilen.  
- **Konsistenz über Formate hinweg** – dieselben Randdefinitionen funktionieren für XPS, PDF und Bildausgaben.  
- **Keine Browser‑Abhängigkeit** – das Rendering erfolgt serverseitig, sodass kein Headless‑Browser nötig ist.  

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

1. **Java‑Entwicklungsumgebung** – JDK 11 oder höher installiert.  
2. **Aspose.HTML für Java** – Bibliothek von [hier](https://releases.aspose.com/html/java/) herunterladen und installieren.  

## Pakete importieren

Um loszulegen, importieren Sie die notwendigen Aspose.HTML‑Klassen:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Wie man HTML‑Seitenränder in Java festlegt – Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Konfiguration initialisieren und benutzerdefinierte Seitenränder definieren

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

In diesem Block erstellen wir ein `Configuration`‑Objekt, holen den `IUserAgentService` und fügen eine CSS `@page`‑Regel ein, die die Ränder, einen Seitenzähler unten rechts und einen Dokumenttitel oben mittig definiert.

### Schritt 2: Das HTML‑Dokument erstellen

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Hier instanziieren wir ein `HTMLDocument` mit einem einfachen „Hello World“‑Snippet. Die gleiche Konfiguration aus Schritt 1 wird angewendet, sodass die benutzerdefinierten Ränder beim Rendern berücksichtigt werden.

### Schritt 3: In eine XPS‑Datei (oder ein anderes unterstütztes Format) rendern

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Dieser Schritt erstellt ein `XpsDevice`, das die gerenderten Seiten in `output.xps` schreibt. Die zuvor definierten Ränder, Seitenzahlen und der Titel erscheinen in der finalen Datei.

## Häufige Probleme & Tipps

- **Ränder bleiben unverändert** – Stellen Sie sicher, dass die `@page`‑Regel nicht von anderen Stylesheets überschrieben wird. Der Aufruf `setUserStyleSheet` setzt sie mit höchster Priorität.  
- **Seitenzahlen zeigen „NaN“** – Vergewissern Sie sich, dass Sie Aspose.HTML Version 23.10 oder neuer verwenden; ältere Versionen besitzen die Funktion `currentPageNumber()` nicht.  
- **Ausgabedatei ist leer** – Prüfen Sie, ob der Pfad `Resources.output` korrekt aufgelöst wird und Sie Schreibrechte besitzen.  

## Häufig gestellte Fragen

### Q1: Was ist Aspose.HTML für Java?

**A:** Aspose.HTML für Java ist eine Java‑Bibliothek, die leistungsstarke Werkzeuge zum Arbeiten mit HTML‑Dokumenten in Java‑Anwendungen bereitstellt, einschließlich Konvertierung, Rendering und Manipulation.

### Q2: Kann ich die Seitenränder weiter anpassen?

**A:** Ja, bearbeiten Sie einfach das CSS innerhalb von `setUserStyleSheet`. Sie können beliebige `margin-*`‑Werte ändern oder zusätzliche `@top-*` / `@bottom-*`‑Boxen hinzufügen.

### Q3: Wie kann ich mehr Inhalt zum HTML‑Dokument hinzufügen?

**A:** Ersetzen Sie den String in `new HTMLDocument("<div>Hello World!!!</div>", …)` durch Ihr eigenes HTML‑Markup oder laden Sie eine externe Datei über den Konstruktor `HTMLDocument(String url, …)`.

### Q4: Ist Aspose.HTML für Java mit anderen Dokumentformaten kompatibel?

**A:** Absolut. Das gleiche `HTMLDocument` kann zu PDF, XPS, Bildern oder sogar EPUB gerendert werden, indem Sie das Ausgabegerät austauschen (z. B. `PdfDevice`, `PngDevice`).

### Q5: Benötige ich eine Lizenz für die Nutzung von Aspose.HTML für Java?

**A:** Ja, für den Produktionseinsatz ist eine Lizenz erforderlich. Sie können eine Testlizenz erhalten oder eine Lizenz erwerben [hier](https://purchase.aspose.com/buy) oder [hier](https://releases.aspose.com/).

### Q6: Wie setze ich unterschiedliche Ränder für ungerade und gerade Seiten?

**A:** Verwenden Sie die Pseudo‑Klassen `@page :left` und `@page :right` in Ihrem Stylesheet, um separate Ränder für linke (gerade) und rechte (ungerade) Seiten zu definieren.

### Q7: Kann ich benutzerdefinierte Schriftarten im gerenderten Dokument einbetten?

**A:** Ja. Fügen Sie `@font-face`‑Regeln zum Benutzer‑Stylesheet hinzu und referenzieren Sie die Schriften in Ihrem HTML‑Inhalt.

## Fazit

Sie haben nun **wie man HTML‑Seitenränder in Java** mit Aspose.HTML festlegt und wissen, wie Sie Seitenzahlen und einen Titel hinzufügen, um Ihre Dokumente professionell wirken zu lassen. Experimentieren Sie gern mit zusätzlichen `@page`‑Boxen, benutzerdefinierten Schriften oder verschiedenen Ausgabeformaten, um die Anforderungen Ihres Projekts zu erfüllen.

Bei Problemen helfen Ihnen die offizielle [Aspose.HTML für Java‑Dokumentation](https://reference.aspose.com/html/java/) und das [Aspose‑Support‑Forum](https://forum.aspose.com/) weiter.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Zuletzt aktualisiert:** 2025-12-05  
**Getestet mit:** Aspose.HTML für Java 23.12  
**Autor:** Aspose  

---