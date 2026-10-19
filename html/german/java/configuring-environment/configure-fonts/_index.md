---
date: 2026-04-05
description: Erfahren Sie, wie Sie PDF aus HTML generieren, Schriftarten konfigurieren,
  benutzerdefiniertes CSS anwenden, eine temporäre Lizenz verwenden und HTML in PDF
  in Java mit Aspose.HTML konvertieren.
keywords:
- generate pdf from html
- convert html pdf java
- add custom fonts pdf
- fonts not showing pdf
linktitle: Schriftarten in Aspose.HTML konfigurieren
second_title: Java HTML Processing with Aspose.HTML
title: 'PDF aus HTML generieren: Schriftarten mit Aspose.HTML für Java konfigurieren'
url: /de/java/configuring-environment/configure-fonts/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Schriftarten für HTML‑to‑PDF Java mit Aspose.HTML

## Einführung
In diesem Tutorial erfahren Sie, wie Sie **generate PDF from HTML** mit Aspose.HTML verwenden und Schriftarten für die HTML‑to‑PDF‑Konvertierung in Java konfigurieren. Beim Arbeiten mit HTML‑Dokumenten stellt die richtige Schriftart sicher, dass das erzeugte PDF exakt wie die ursprüngliche Webseite aussieht – Markenfarben, Typografie und Layout bleiben erhalten. Egal, ob Sie Berichte, Rechnungen oder irgendeine Dokument‑Generierungspipeline erstellen, die korrekte Schriftartkonfiguration ist der Schlüssel zu professionell aussehenden PDFs. Lassen Sie uns den gesamten Prozess durchgehen, von der Vorbereitung der Umgebung bis zur Konvertierung von HTML zu PDF mit benutzerdefinierten Schriftarten und CSS.

## Schnelle Antworten
- **Was ist der Hauptzweck dieses Tutorials?** Schriftarten für die HTML‑to‑PDF‑Konvertierung in Java mit Aspose.HTML konfigurieren.  
- **Welche Bibliothek führt die Konvertierung durch?** Aspose.HTML für Java (die `Converter`‑Klasse).  
- **Benötige ich eine Lizenz?** Eine temporäre Aspose‑Lizenz entfernt Bewertungseinschränkungen; für die Produktion ist eine Voll‑Lizenz erforderlich.  
- **Wo sollten meine benutzerdefinierten Schriftarten abgelegt werden?** In einem Ordner, auf den `FontsLookupFolder` verweist, z. B. ein `fonts`‑Verzeichnis neben Ihrem Projekt.  
- **Kann ich die PDF‑Ausgabe anpassen?** Ja – verwenden Sie `PdfSaveOptions`, um Seitengröße, Ränder und mehr zu ändern.

## Was ist **generate PDF from HTML** und warum ist die Schriftartkonfiguration wichtig?
Der **generate PDF from HTML**‑Prozess rendert ein HTML‑Dokument zu einer PDF‑Seite. Schriftarten sind ein entscheidender Teil des Renderings, da sie Layout, Zeilenabstand und visuelle Treue beeinflussen. Indem Sie Aspose.HTML auf einen benutzerdefinierten Schriftartenordner verweisen, stellen Sie sicher, dass das PDF exakt die Schriftarten verwendet, die Sie für die Webseite entworfen haben, wodurch Fallback‑Schriftarten vermieden und die Marken­konsistenz erhalten bleibt.

## Warum Aspose.HTML für die Schriftartkonfiguration verwenden?
- **Präzises Rendering:** Unterstützt CSS2.1 und viele CSS3‑Funktionen, sodass Ihr HTML im PDF gleich aussieht.  
- **Plattformübergreifend:** Funktioniert auf jedem Betriebssystem, das Java 1.8+ ausführt.  
- **Lizenzflexibilität:** Testen Sie mit einer temporären Lizenz und wechseln Sie dann für die Produktion zu einer Voll‑Lizenz.  
- **Leistung:** Schnelle Konvertierung selbst für komplexe Seiten.

## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes haben:

1. **Java Development Kit (JDK) 1.8+** – Der Code läuft auf jedem modernen JDK.  
2. **Aspose.HTML für Java** – Laden Sie das neueste JAR von der [Aspose-Website](https://releases.aspose.com/html/java/) herunter.  
3. **IDE** – IntelliJ IDEA, Eclipse oder ein beliebiger Java‑kompatibler Editor.  
4. **Grundlegende Java‑Kenntnisse** – Sie sollten mit Klassen, Methoden und Datei‑I/O vertraut sein.  
5. **Aspose.HTML‑Lizenz** – Eine [temporäre Lizenz](https://purchase.aspose.com/temporary-license/) hebt Bewertungseinschränkungen auf.

## Pakete importieren
Zuerst importieren Sie die Kern‑Java‑ und Aspose.HTML‑Klassen, die Sie benötigen.  

```java
import java.io.IOException;
```

Diese Importe geben Ihnen Zugriff auf Dateiverarbeitung und die Aspose.HTML‑API.

## Wie man benutzerdefinierte Schriftarten zur PDF‑Erstellung hinzufügt
Im Folgenden erklären wir, warum die Schriftartenbehandlung wichtig ist, wie Sie benutzerdefiniertes CSS anwenden und **eine temporäre Lizenz** nutzen, um die volle Funktionalität während des Tests freizuschalten.

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Erstellen Sie den HTML‑Inhalt
Wir beginnen damit, eine einfache HTML‑Datei zu erzeugen, die wir später zu PDF konvertieren.

#### 1.1 Schreiben Sie den HTML‑Code
```java
String code = "<h1>FontsSettings property</h1>\r\n" +
    "<p>The FontsSettings property is used for configuration of fonts handling.</p>\r\n";
```

Dieses Snippet definiert eine Überschrift und einen Absatz. Sie können das HTML nach Belieben erweitern, wenn Sie zusätzliche Stile testen möchten.

#### 1.2 Speichern Sie das HTML in einer Datei
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("user-agent-fontsetting.html")) {
    fileWriter.write(code);
}
```

Der `FileWriter` schreibt die Zeichenkette in die Datei `user-agent-fontsetting.html` in Ihrem Projektordner. Nach diesem Schritt haben Sie eine physische HTML‑Datei, die bereit zur Verarbeitung ist.

### Schritt 2: Konfigurieren Sie die Aspose.HTML‑Umgebung
Jetzt richten wir das Aspose.HTML‑`Configuration`‑Objekt ein, mit dem wir steuern können, wie das HTML gerendert wird.

#### 2.1 Erstellen Sie eine Configuration‑Instanz
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

Das `Configuration`‑Objekt ist der Einstiegspunkt für die Anpassung von Rendering‑Optionen wie Schriftartenverwaltung und User‑Agent‑Verhalten.

#### 2.2 Greifen Sie auf den User‑Agent‑Service zu
```java
com.aspose.html.services.IUserAgentService userAgent = configuration.getService(com.aspose.html.services.IUserAgentService.class);
```

Der `IUserAgentService` verwaltet Stylesheets, Schriftarten und weitere Rendering‑Details. Wir werden ihn nutzen, um benutzerdefiniertes CSS zu injizieren und auf unseren Schriftartenordner zu verweisen.

### Schritt 3: Anwenden benutzerdefinierter Stile und Schriftarten
Mit der vorbereiteten Umgebung können wir nun CSS‑Regeln hinzufügen und Aspose.HTML mitteilen, wo unsere Schriftarten zu finden sind.

#### 3.1 Benutzerdefiniertes CSS festlegen
```java
userAgent.setUserStyleSheet("h1 { color:#a52a2a; }\r\n" +
    "p { color:grey; }\r\n");
```

Dieses CSS färbt die Überschrift braun und den Absatz grau. Sie können hier beliebige gültige CSS‑Regeln hinzufügen – Aspose.HTML unterstützt die vollständige CSS2.1‑Spezifikation und viele CSS3‑Features. *(Dies ist ein Beispiel für **apply custom css**.)*

#### 3.2 Verweisen Sie auf den benutzerdefinierten Schriftartenordner
```java
userAgent.getFontsSettings().setFontsLookupFolder("fonts");
```

Platzieren Sie beliebige `.ttf`‑ oder `.otf`‑Dateien, die Sie verwenden möchten, in einem Ordner namens `fonts`, der im Stammverzeichnis Ihres Projekts liegt. Aspose.HTML lädt diese Schriftarten automatisch beim Rendern.

> **Pro tip:** Wenn Sie mehrere Schriftfamilien haben, organisieren Sie sie in Unterordnern und fügen Sie jeden übergeordneten Ordner mittels einer durch Semikolons getrennten Liste zu `FontsLookupFolder` hinzu.

### Schritt 4: Laden Sie das HTML‑Dokument mit der Konfiguration
Jetzt laden wir die zuvor erstellte HTML‑Datei und wenden die benutzerdefinierte Konfiguration an.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("user-agent-fontsetting.html", configuration);
```

Das `HTMLDocument`‑Objekt stellt nun das formatierte HTML bereit, das konvertiert werden kann.

### Schritt 5: HTML in PDF konvertieren
Abschließend führen wir die **aspose html pdf conversion** durch, um eine PDF‑Datei zu erzeugen, die unsere benutzerdefinierten Schriftarten und Stile berücksichtigt.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.PdfSaveOptions(),
    "user-agent-fontsetting_out.pdf"
);
```

Das `PdfSaveOptions`‑Objekt ermöglicht das Anpassen von Ausgabeeinstellungen wie Seitengröße, Kompression und Metadaten. Für eine einfache Konvertierung funktionieren die Standardoptionen perfekt.

### Schritt 6: Ressourcen bereinigen
Eine ordnungsgemäße Freigabe verhindert Speicherlecks, insbesondere bei der Verarbeitung vieler Dokumente in einer langlaufenden Anwendung.

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

Diese Aufrufe geben native Ressourcen frei, die von Aspose.HTML zugewiesen wurden.

## Häufige Probleme & Lösungen

| Problem | Lösung |
|---------|--------|
| **Schriftarten werden nicht angezeigt** | Stellen Sie sicher, dass der `fonts`‑Ordner korrekt referenziert wird und gültige `.ttf`/`.otf`‑Dateien enthält. Verwenden Sie absolute Pfade, wenn der Ordner außerhalb des Projektverzeichnisses liegt. |
| **PDF sieht leer aus** | Vergewissern Sie sich, dass der Pfad zur HTML‑Datei korrekt ist und die Datei lesbar ist. Prüfen Sie, ob das `Configuration`‑Objekt an den `HTMLDocument`‑Konstruktor übergeben wurde. |
| **Lizenzausnahme** | Laden Sie vor dem Aufruf von Aspose‑APIs eine temporäre oder vollständige Aspose‑Lizenz. Platzieren Sie die Lizenzdatei im Klassenpfad und laden Sie sie mit `License license = new License(); license.setLicense("Aspose.Total.Java.lic");`. |
| **Unerwartetes CSS‑Rendering** | Aspose.HTML unterstützt die meisten CSS‑Eigenschaften, jedoch nicht alle modernen Features (z. B. CSS Grid). Vereinfachen Sie die Stile oder nutzen Sie unterstützte CSS‑Eigenschaften. |

## Häufig gestellte Fragen

**Q: Kann ich jede Schriftart mit Aspose.HTML für Java verwenden?**  
A: Ja, jede TrueType (`.ttf`)‑ oder OpenType (`.otf`)‑Schrift, die Ihr Betriebssystem unterstützt, kann verwendet werden. Legen Sie die Dateien einfach in den Ordner, den Sie mit `FontsLookupFolder` angegeben haben.

**Q: Benötige ich eine Lizenz, um Aspose.HTML für Java zu nutzen?**  
A: Sie können die Bibliothek ohne Lizenz evaluieren, aber eine [temporäre Aspose‑Lizenz](https://purchase.aspose.com/temporary-license/) hebt die Evaluationsbeschränkungen auf. Für die Produktion ist eine Voll‑Lizenz erforderlich.

**Q: Wie kann ich die PDF‑Ausgabe anpassen?**  
A: Übergeben Sie eine konfigurierte `PdfSaveOptions`‑Instanz an `convertHTML`. Sie können Seitengröße, Ränder, Kompressionsgrad und mehr festlegen.

**Q: Ist es möglich, komplexere CSS‑Stile anzuwenden?**  
A: Ja, Aspose.HTML unterstützt ein breites Spektrum an CSS. Komplexe Selektoren, Media Queries und Pseudo‑Klassen funktionieren wie im Browser, obwohl einige sehr neue CSS3/4‑Features möglicherweise nicht vollständig unterstützt werden.

**Q: Wo finde ich weitere Beispiele und Dokumentation?**  
A: Besuchen Sie die offizielle [Aspose.HTML für Java Dokumentationsseite](https://reference.aspose.com/html/java/) für detaillierte API‑Referenzen und zusätzliche Code‑Beispiele.

**Q: Wie wirkt sich die temporäre Aspose‑Lizenz auf die Konvertierung aus?**  
A: Die temporäre Lizenz hebt das 10‑Seiten‑Limit und das Wasserzeichen auf, die im Evaluationsmodus erscheinen, und ermöglicht Ihnen, den **aspose html pdf conversion**‑Workflow vollständig zu testen.

---

**Zuletzt aktualisiert:** 2026-04-05  
**Getestet mit:** Aspose.HTML für Java 24.12 (zum Zeitpunkt der Erstellung die neueste Version)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}