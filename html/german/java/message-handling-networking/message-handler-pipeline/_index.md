---
date: 2026-02-23
description: Erfahren Sie, wie Sie ZIP‑Dateien mit Aspose.HTML für Java in PDF konvertieren.
  Diese Schritt‑für‑Schritt‑Anleitung zeigt, wie Sie den Netzwerkdienst konfigurieren,
  einen benutzerdefinierten Handler hinzufügen und die Anfragedauer protokollieren.
linktitle: Creating Message Handler Pipelines in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Wie man ZIP in PDF mit Aspose.HTML für Java konvertiert
url: /de/java/message-handling-networking/message-handler-pipeline/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ZIP in PDF mit Aspose.HTML für Java konvertiert

## Einleitung
In diesem umfassenden Tutorial erfahren Sie **wie man zip**-Archive in PDF‑Dokumente mit Aspose.HTML für Java konvertiert. Wir führen Sie Schritt für Schritt durch den Aufbau einer Message‑Handler‑Pipeline, die Konfiguration des Network Service, das Hinzufügen eines benutzerdefinierten Handlers und das Protokollieren der Anfragedauer – und das alles bei klarem, ausführbarem Code. Egal, ob Sie die Berichtserstellung automatisieren oder eine zuverlässige Methode benötigen, HTML‑Inhalte als PDF zu verpacken, diese Anleitung deckt alles ab.

## Schnelle Antworten
- **Was macht die Pipeline?** Sie verarbeitet eine ZIP‑Datei, extrahiert HTML und rendert es zu PDF.  
- **Welcher Handler protokolliert die Dauer?** `StartRequestDurationLoggingMessageHandler` und `StopRequestDurationLoggingMessageHandler`.  
- **Brauche ich eine Lizenz?** Eine kostenlose Testversion funktioniert für Tests; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich den Ausgabepfad ändern?** Ja – ändern Sie die Variable `savePath` in Schritt 1.  
- **Welche Java‑Version wird benötigt?** JDK 8 oder höher.

## Was ist eine Message‑Handler‑Pipeline?
Eine Message‑Handler‑Pipeline ist eine konfigurierbare Kette von Verarbeitungskomponenten, die Netzwerk‑Anfragen von Aspose.HTML abfangen. Durch das Einfügen benutzerdefinierter Handler können Sie steuern, wie Ressourcen abgerufen, transformiert und protokolliert werden – ideal für Szenarien wie das Konvertieren eines ZIP‑Archivs zu PDF.

## Warum eine Pipeline zum Konvertieren von ZIP zu PDF verwenden?
- **Feinkörnige Kontrolle** – Hinzufügen, Neuordnen oder Entfernen von Handlern, um Ihren Arbeitsablauf anzupassen.  
- **Performance‑Einblicke** – Protokollieren Sie die Anfragedauer, um Engpässe zu identifizieren.  
- **Erweiterbarkeit** – Integrieren Sie eigene Logik (z. B. Authentifizierung, Caching).  
- **Zuverlässigkeit** – Die Bibliothek behandelt Randfälle wie fehlerhaftes HTML automatisch.

## Voraussetzungen
- **Java Development Kit (JDK) 8+** – Stellen Sie sicher, dass `java -version` 8 oder neuer ausgibt.  
- **Aspose.HTML for Java Bibliothek** – Laden Sie sie von der [Aspose downloads](https://releases.aspose.com/html/java/) Seite herunter.  
- **Eine IDE** – IntelliJ IDEA, Eclipse oder NetBeans erleichtern das Programmieren.  
- **Grundkenntnisse in Java und HTML** – Hilfreich, aber nicht zwingend erforderlich.

## Pakete importieren
Um zu beginnen, importieren wir die Klassen, die wir benötigen. Diese Importe geben uns Zugriff auf Konfiguration, Netzwerk und PDF‑Rendering‑Funktionen.

```java
import com.aspose.html.Configuration;
import com.aspose.html.HTMLDocument;
import com.aspose.html.net.MessageHandlerCollection;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.services.INetworkService;
```

## Schritt‑für‑Schritt‑Anleitung

### Schritt 1: Pfade zu Dateien vorbereiten
```java
// Prepare path to a source zip file
String documentPath = "input/test.zip";
// Prepare path for converted file saving
String savePath = "output/zip-to-pdf-duration.pdf";
```
Setzen Sie `documentPath` auf die ZIP‑Datei, die Ihre HTML‑Dateien enthält, und `savePath` auf den Ort, an dem Sie das endgültige PDF speichern möchten.

### Schritt 2: Eine Configuration‑Instanz erstellen
```java
// Create an instance of the Configuration class
Configuration configuration = new Configuration();
```
Das `Configuration`‑Objekt ist die Grundlage für die Anpassung der Verarbeitungspipeline.

### Schritt 3: Den Network Service initialisieren
```java
INetworkService service = configuration.getService(INetworkService.class);
MessageHandlerCollection handlers = service.getMessageHandlers();
```
Hier **konfigurieren wir den Network Service** und erhalten die `MessageHandlerCollection`, die das Werkzeugkasten für das Hinzufügen benutzerdefinierter Handler ist.

### Schritt 4: Den ZIP‑Datei‑Message‑Handler hinzufügen
```java
// Custom Schema: ZIP. Add ZipFileSchemaMessageHandler to the end of the pipeline
handlers.addItem(new ZIPFileSchemaMessageHandler(documentPath));
```
Durch **Hinzufügen eines benutzerdefinierten Handlers** (`ZIPFileSchemaMessageHandler`) teilen wir Aspose.HTML mit, die ZIP‑Datei als virtuelles Dateisystem zu behandeln.

### Schritt 5: Start Request Duration Logging Handler einfügen
```java
// Duration Logging. Add the StartRequestDurationLoggingMessageHandler at the first place in the pipeline
handlers.insertItem(0, new StartRequestDurationLoggingMessageHandler());
```
Dieser Handler **protokolliert die Anfragedauer** ganz am Anfang der Pipeline und liefert einen Zeitstempel, wann die Verarbeitung startet.

### Schritt 6: Stop Request Duration Logging Handler hinzufügen
```java
// Add the StopRequestDurationLoggingMessageHandler to the end of the pipeline
handlers.addItem(new StopRequestDurationLoggingMessageHandler());
```
Durch das Platzieren am Ende können Sie die gesamte für die Konvertierung von ZIP zu PDF benötigte Zeit erfassen.

### Schritt 7: Das HTML‑Document initialisieren
```java
// Initialize an HTML document with specified configuration
HTMLDocument document = new HTMLDocument("zip-file:///test.html", configuration);
```
Wir verweisen das `HTMLDocument` auf die Einstiegs‑HTML‑Datei innerhalb der ZIP (`zip-file:///test.html`). Die zuvor erstellte Konfiguration wird automatisch angewendet.

### Schritt 8: Das PDF‑Device erstellen
```java
// Create the PDF Device
PdfDevice device = new PdfDevice(savePath);
```
Das **PDF‑Device** (`PdfDevice`) ist das, was **PDF aus ZIP‑Inhalten erstellt**. Es empfängt die gerenderten Seiten und schreibt sie nach `savePath`.

### Schritt 9: Das ZIP zu PDF rendern
```java
// Render ZIP to PDF
document.renderTo(device);
```
Der Aufruf von `renderTo` löst die gesamte Pipeline aus: Die ZIP‑Datei wird entpackt, HTML wird gerendert, die Dauer wird protokolliert und das endgültige PDF wird geschrieben.

## Häufige Probleme und Lösungen
| Problem | Ursache | Lösung |
|-------|-------|-----|
| `FileNotFoundException` | Falscher `documentPath` oder `savePath` | Stellen Sie sicher, dass die Pfade absolut oder relativ zum Arbeitsverzeichnis sind. |
| Kein Inhalt im PDF | Falscher Einstiegs‑HTML‑Dateiname im `HTMLDocument`‑Konstruktor | Stellen Sie sicher, dass der Dateiname exakt der HTML‑Datei im ZIP (`test.html`) entspricht. |
| Dauer nicht protokolliert | Handler wurden nicht in der richtigen Reihenfolge eingefügt | Fügen Sie `StartRequestDurationLoggingMessageHandler` an Index 0 ein und `StopRequestDurationLoggingMessageHandler` nach allen anderen Handlern. |
| Nicht unterstützte HTML‑Funktionen | Verwendung von CSS/JS, das von Aspose.HTML nicht unterstützt wird | Vereinfachen Sie das Markup oder verarbeiten Sie das HTML vor dem Rendern vor. |

## Häufig gestellte Fragen

**F: Was ist Aspose.HTML für Java?**  
A: Aspose.HTML für Java ist eine Bibliothek, die die Manipulation von HTML‑Dokumenten und die Konvertierung in Formate wie PDF, Bild und EPUB ermöglicht.

**F: Wie lade ich Aspose.HTML für Java herunter?**  
A: Sie können es von der [Aspose downloads](https://releases.aspose.com/html/java/) Seite herunterladen.

**F: Kann ich Aspose.HTML kostenlos nutzen?**  
A: Ja, eine kostenlose Testversion ist verfügbar. Registrieren Sie sich dafür [hier](https://releases.aspose.com/).

**F: Wo finde ich Support für Aspose.HTML?**  
A: Besuchen Sie das [Aspose Support Forum](https://forum.aspose.com/c/html/29) für Hilfe von der Community und den Aspose‑Entwicklern.

**F: Was sind Message‑Handler in Aspose.HTML?**  
A: Message‑Handler sind Komponenten, die Netzwerk‑Anfragen innerhalb der Pipeline abfangen und verarbeiten – nützlich für Protokollierung, Authentifizierung oder benutzerdefinierte Inhaltsbeschaffung.

**F: Wie kann ich meinen eigenen benutzerdefinierten Handler hinzufügen?**  
A: Implementieren Sie `IMessageHandler` und fügen Sie ihn mit `handlers.addItem(new MyCustomHandler())` zur `MessageHandlerCollection` hinzu.

**F: Ist es möglich, mehrere ZIP‑Dateien stapelweise zu konvertieren?**  
A: Ja – iterieren Sie über eine Liste von ZIP‑Pfaden und verwenden Sie für jede Iteration dieselbe Konfiguration und Pipeline erneut.

## Fazit
Sie wissen jetzt **wie man zip**-Archive in PDF‑Dateien mit Aspose.HTML für Java konvertiert, komplett mit einem konfigurierbaren Network Service, einem benutzerdefinierten ZIP‑Handler und präzisem Protokollieren der Anfragedauer. Diese Pipeline gibt Ihnen die volle Kontrolle über den Konvertierungsprozess und ist ideal für automatisierte Berichte, Dokumentenarchivierung oder jedes Szenario, in dem HTML‑Inhalte als PDF verpackt werden müssen.

---

**Zuletzt aktualisiert:** 2026-02-23  
**Getestet mit:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}