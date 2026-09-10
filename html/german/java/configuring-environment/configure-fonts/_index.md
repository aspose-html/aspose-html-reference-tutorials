---
date: 2026-02-04
description: Erfahren Sie, wie Sie Aspose.HTML verwenden, um Schriftarten zu konfigurieren,
  benutzerdefiniertes CSS anzuwenden, eine temporäre Lizenz zu nutzen und PDF aus
  HTML in Java zu erzeugen.
linktitle: Configure Fonts in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Wie man Aspose.HTML verwendet, um Schriftarten für HTML‑zu‑PDF in Java zu konfigurieren
url: /de/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Schriftarten für HTML‑to‑PDF Java mit Aspose.HTML konfigurieren

## Einführung
In diesem Tutorial erfahren Sie **wie Sie Aspose.HTML** verwenden, um Schriftarten für die HTML‑zu‑PDF‑Konvertierung in Java zu konfigurieren. Beim Arbeiten mit HTML‑Dokumenten sorgt die richtige Schriftart dafür, dass das erzeugte PDF exakt wie die ursprüngliche Webseite aussieht — Markenfarben, Typografie und Layout bleiben erhalten. Egal, ob Sie Berichte, Rechnungen oder irgendeine Dokument‑Generierungspipeline erstellen, die korrekte Schriftartkonfiguration ist der Schlüssel zu professionell aussehenden PDFs. Lassen Sie uns den gesamten Prozess durchgehen, von der Vorbereitung der Umgebung bis zur Konvertierung von HTML zu PDF mit benutzerdefinierten Schriftarten und CSS.

## Schnellantworten
- **Was ist das Hauptziel dieses Tutorials?** Schriftarten für die HTML‑zu‑PDF‑Konvertierung in Java mit Aspose.HTML konfigurieren.  
- **Welche Bibliothek übernimmt die Konvertierung?** Aspose.HTML für Java (die `Converter`‑Klasse).  
- **Benötige ich eine Lizenz?** Eine temporäre Aspose‑Lizenz entfernt Evaluationsbeschränkungen; für die Produktion ist eine Voll‑Lizenz erforderlich.  
- **Wo sollen meine benutzerdefinierten Schriftarten abgelegt werden?** In einem Ordner, der über `FontsLookupFolder` referenziert wird, z. B. ein `fonts`‑Verzeichnis neben Ihrem Projekt.  
- **Kann ich die PDF‑Ausgabe anpassen?** Ja — verwenden Sie `PdfSaveOptions`, um Seitengröße, Ränder und mehr zu ändern.

## Verwendung von Aspose.HTML für die Schriftartkonfiguration
Im Folgenden erklären wir, warum die Schrifthandhabung wichtig ist, wie benutzerdefiniertes CSS angewendet wird und wie Sie **eine temporäre Lizenz** nutzen, um die volle Funktionalität während des Tests freizuschalten.

## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

1. **Java Development Kit (JDK) 1.8+** – der Code läuft auf jedem modernen JDK.  
2. **Aspose.HTML für Java** – laden Sie das neueste JAR von der [Aspose‑Website](https://releases.aspose.com/html/java/) herunter.  
3. **IDE** – IntelliJ IDEA, Eclipse oder ein beliebiger Java‑kompatibler Editor.  
4. **Grundlegende Java‑Kenntnisse** – Sie sollten mit Klassen, Methoden und Datei‑I/O vertraut sein.  
5. **Aspose.HTML‑Lizenz** – eine [temporäre Lizenz](https://purchase.aspose.com/temporary-license/) hebt Evaluationsbeschränkungen auf.

## Pakete importieren
Importieren Sie zunächst die Kern‑Java‑ und Aspose.HTML‑Klassen, die Sie benötigen.  

```java
import java.io.IOException;
```

Diese Importe geben Ihnen Zugriff auf Datei‑Handling und die Aspose.HTML‑API.

## Was ist **html to pdf java** und warum ist die Schriftartkonfiguration wichtig?
Der **html to pdf java**‑Prozess rendert ein HTML‑Dokument zu einer PDF‑Seite. Schriftarten sind ein zentraler Bestandteil des Renderings, weil sie Layout, Zeilenabstand und visuelle Treue beeinflussen. Indem Sie Aspose.HTML auf einen benutzerdefinierten Schriftarten‑Ordner verweisen, stellen Sie sicher, dass das PDF exakt die Typografie verwendet, die Sie für die Web‑Seite entworfen haben, wodurch Ersatz‑Schriftarten vermieden und Marken‑Konsistenz bewahrt wird.

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: HTML‑Inhalt erstellen
Wir beginnen mit der Erzeugung einer einfachen HTML‑Datei, die wir später zu PDF konvertieren.

#### 1.1 HTML‑Code schreiben
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

Dieses Snippet definiert eine Überschrift und einen Absatz. Ergänzen Sie das HTML gern um weitere Elemente, wenn Sie zusätzliche Stile testen möchten.

#### 1.2 HTML in eine Datei speichern
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

Der `FileWriter` schreibt den String in `user-agent-fontsetting.html` in Ihrem Projektordner. Nach diesem Schritt liegt eine physische HTML‑Datei zur Verarbeitung bereit.

### Schritt 2: Aspose.HTML‑Umgebung konfigurieren
Jetzt richten wir das Aspose.HTML‑`Configuration`‑Objekt ein, mit dem wir das Rendering steuern können.

#### 2.1 Eine Configuration‑Instanz erstellen
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

Das `Configuration`‑Objekt ist der Einstiegspunkt für die Anpassung von Rendering‑Optionen wie Schrifthandhabung und User‑Agent‑Verhalten.

#### 2.2 Auf den User Agent Service zugreifen
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

Der `IUserAgentService` verwaltet Stylesheets, Schriftarten und weitere Rendering‑Details. Wir nutzen ihn, um benutzerdefiniertes CSS zu injizieren und auf unseren Schriftarten‑Ordner zu verweisen.

### Schritt 3: Benutzerdefinierte Stile und Schriftarten anwenden
Mit der vorbereiteten Umgebung können wir nun CSS‑Regeln hinzufügen und Aspose.HTML mitteilen, wo die Schriftarten zu finden sind.

#### 3.1 Benutzerdefiniertes CSS setzen
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

Dieses CSS färbt die Überschrift braun und den Absatz grau. Sie können beliebige gültige CSS‑Regeln hinzufügen — Aspose.HTML unterstützt die komplette CSS 2.1‑Spezifikation und viele CSS 3‑Features. *(Dies ist ein Beispiel für **apply custom css**.)*

#### 3.2 Auf den benutzerdefinierten Schriftarten‑Ordner verweisen
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

Legen Sie alle `.ttf`‑ oder `.otf`‑Dateien, die Sie verwenden möchten, in einen Ordner namens `fonts` im Stammverzeichnis Ihres Projekts. Aspose.HTML lädt diese Schriftarten automatisch beim Rendern.

> **Pro‑Tipp:** Wenn Sie mehrere Schriftfamilien haben, organisieren Sie sie in Unterordnern und fügen Sie jeden übergeordneten Ordner mittels einer durch Semikolons getrennten Liste zu `FontsLookupFolder` hinzu.

### Schritt 4: HTML‑Dokument mit der Konfiguration laden
Jetzt laden wir die zuvor erstellte HTML‑Datei und wenden die benutzerdefinierte Konfiguration an.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

Das `HTMLDocument`‑Objekt repräsentiert nun das formatierte HTML, das zur Konvertierung bereitsteht.

### Schritt 5: HTML zu PDF konvertieren
Abschließend führen wir die **aspose html pdf conversion** durch, um eine PDF‑Datei zu erzeugen, die unsere benutzerdefinierten Schriftarten und Stile berücksichtigt.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

Das `PdfSaveOptions`‑Objekt ermöglicht das Anpassen von Ausgabeeinstellungen wie Seitengröße, Kompression und Metadaten. Für eine einfache Konvertierung funktionieren die Standard‑Optionen perfekt.

### Schritt 6: Ressourcen aufräumen
Ein korrektes Dispose verhindert Speicher‑Leaks, besonders bei der Verarbeitung vieler Dokumente in einer langlebigen Anwendung.

#### 6.1 HTMLDocument freigeben
```java
if (document != null) {
    document.dispose();
}
```

#### 6.2 Configuration freigeben
```java
if (configuration != null) {
    configuration.dispose();
}
```

Diese Aufrufe geben native Ressourcen frei, die von Aspose.HTML alloziert wurden.

## Häufige Probleme & Lösungen
| Problem | Lösung |
|-------|----------|
| **Schriftarten werden nicht angezeigt** | Prüfen Sie, ob der `fonts`‑Ordner korrekt referenziert wird und gültige `.ttf`/`.otf`‑Dateien enthält. Verwenden Sie absolute Pfade, wenn der Ordner außerhalb des Projektverzeichnisses liegt. |
| **PDF erscheint leer** | Stellen Sie sicher, dass der Pfad zur HTML‑Datei korrekt ist und die Datei lesbar ist. Überprüfen Sie, ob das `Configuration`‑Objekt an den `HTMLDocument`‑Konstruktor übergeben wird. |
| **Lizenz‑Ausnahme** | Laden Sie vor dem Aufruf irgendeiner Aspose‑API eine temporäre oder vollständige Lizenz. Platzieren Sie die Lizenzdatei im Klassenpfad und laden Sie sie mit `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`. |
| **Unerwartetes CSS‑Rendering** | Aspose.HTML unterstützt die meisten CSS‑Eigenschaften, jedoch nicht alle modernen Features (z. B. CSS Grid). Vereinfachen Sie die Stile oder verwenden Sie unterstützte CSS‑Eigenschaften. |

## Häufig gestellte Fragen

**F: Kann ich beliebige Schriftarten mit Aspose.HTML für Java verwenden?**  
A: Ja, jede TrueType (`.ttf`)‑ oder OpenType (`.otf`)‑Schrift, die Ihr Betriebssystem unterstützt, kann verwendet werden. Legen Sie die Dateien einfach in den Ordner, den Sie mit `FontsLookupFolder` angegeben haben.

**F: Benötige ich eine Lizenz für Aspose.HTML für Java?**  
A: Sie können die Bibliothek ohne Lizenz evaluieren, doch eine [temporäre Aspose‑Lizenz](https://purchase.aspose.com/temporary-license/) entfernt die Evaluationsbeschränkungen. Für den Produktionseinsatz ist eine Voll‑Lizenz erforderlich.

**F: Wie kann ich die PDF‑Ausgabe anpassen?**  
A: Übergeben Sie eine konfigurierte `PdfSaveOptions`‑Instanz an `convertHTML`. Sie können Seitengröße, Ränder, Kompressionsgrad und mehr festlegen.

**F: Ist es möglich, komplexere CSS‑Stile anzuwenden?**  
A: Ja, Aspose.HTML unterstützt ein breites Spektrum an CSS. Komplexe Selektoren, Media Queries und Pseudo‑Klassen funktionieren wie im Browser, wobei einige sehr neue CSS 3/4‑Features möglicherweise nicht vollständig unterstützt werden.

**F: Wo finde ich weitere Beispiele und Dokumentation?**  
A: Besuchen Sie die offizielle [Aspose.HTML für Java Dokumentationsseite](https://reference.aspose.com/html/java/) für detaillierte API‑Referenzen und zusätzliche Code‑Beispiele.

**F: Wie wirkt sich die temporäre Aspose‑Lizenz auf die Konvertierung aus?**  
A: Die temporäre Lizenz hebt das 10‑Seiten‑Limit und das Wasserzeichen, das im Evaluationsmodus erscheint, auf und ermöglicht Ihnen, den **aspose html pdf conversion**‑Workflow vollständig zu testen.

---

**Zuletzt aktualisiert:** 2026-02-04  
**Getestet mit:** Aspose.HTML für Java 24.12 (zum Zeitpunkt der Erstellung)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}