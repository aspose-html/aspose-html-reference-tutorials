---
date: 2026-01-07
description: Konvertieren Sie EPUB mühelos in XPS mit Aspose.HTML für Java. Folgen
  Sie dieser Schritt‑für‑Schritt‑Anleitung für einen nahtlosen Konvertierungsprozess.
linktitle: How to Convert EPUB to XPS with a Custom Stream Provider
second_title: Java HTML Processing with Aspose.HTML
title: Wie man EPUB in XPS mit einem benutzerdefinierten Stream‑Provider konvertiert
url: /de/java/converting-epub-to-xps/convert-epub-to-xps-specify-custom-stream-provider/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# EPUB in XPS mit einem benutzerdefinierten Stream‑Provider konvertieren

In der heutigen digitalen Verlagswelt ist **convert EPUB to XPS** eine häufige Anforderung – egal, ob Sie eine festes Layout‑Darstellung für den Druck, die Archivierung oder das Teilen über Windows‑Geräte benötigen. Aspose.HTML for Java macht diese Konvertierung einfach, und durch die Verwendung eines benutzerdefinierten Memory‑Stream‑Providers bleibt der gesamte Prozess im Speicher, was ideal für cloud‑basierte oder Hochleistungs‑Szenarien ist. Im Folgenden finden Sie alles, was Sie für den Einstieg benötigen, von den Voraussetzungen bis zu einem vollständigen, ausführbaren Beispiel.

## Schnelle Antworten
- **Was erzeugt die Konvertierung?** Ein XPS‑Dokument, das Layout und Schriftarten beibehält.  
- **Benötige ich eine Lizenz?** Eine kostenlose Testversion funktioniert zum Testen; für die Produktion ist eine kommerzielle Lizenz erforderlich.  
- **Kann ich das in einem Container ausführen?** Ja – keine Dateisystem‑Schreibvorgänge sind nötig, wenn alles im Speicher bleibt.  
- **Welche Java‑Version wird unterstützt?** Java 8 oder höher.  
- **Ist ein benutzerdefineter Stream‑Provider zwingend erforderlich?** Nein, aber er gibt Ihnen volle Kontrolle über Speicherverbrauch und Ausgabe‑Handling.

## Was ist „convert EPUB to XPS“?
Das Konvertieren einer EPUB‑Datei in XPS wandelt ein nachfließbares E‑Book‑Format in ein festes Layout, geräteunabhängiges Dokument um. XPS (XML Paper Specification) ist Microsofts Gegenstück zu PDF und ideal für Szenarien, in denen Sie eine getreue visuelle Darstellung benötigen, die sich über Plattformen hinweg nicht ändert.

## Warum einen benutzerdefinierten Stream‑Provider verwenden?
Ein benutzerdefinierter `MemoryStreamProvider` ermöglicht es, das Konvertierungsergebnis im RAM zu behalten, anstatt eine temporäre Datei auf die Festplatte zu schreiben. Dieser Ansatz:
- Reduziert I/O‑Overhead.
- Verbessert die Leistung in serverlosen oder Micro‑Service‑Architekturen.
- Gibt Ihnen die Flexibilität, das Ergebnis direkt an einen Client, Cloud‑Speicher oder eine andere API zu streamen.

## Voraussetzungen

Um **convert EPUB to XPS** erfolgreich durchzuführen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

### 1. Aspose.HTML for Java Bibliothek  

Sie müssen die Aspose.HTML for Java‑Bibliothek in Ihrer Java‑Umgebung installiert und konfiguriert haben. Falls Sie dies noch nicht getan haben, können Sie die Bibliothek über den [download link](https://releases.aspose.com/html/java/) herunterladen.

### 2. Eingabe‑EPUB‑Datei  

Sie benötigen eine vorhandene EPUB‑Datei, die Sie in XPS konvertieren möchten. Stellen Sie sicher, dass diese Datei für den Konvertierungsprozess bereitsteht.

Jetzt, da Sie alle Voraussetzungen haben, gehen wir die Konvertierung Schritt für Schritt durch.

## Pakete importieren

Stellen Sie vor dem Start sicher, dass Sie die erforderlichen Pakete für Aspose.HTML for Java importieren, um dessen Funktionalitäten zu nutzen.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.saving.MemoryStreamProvider;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.InputStream;
```

## EPUB‑Datei öffnen

Zuerst müssen Sie die vorhandene EPUB‑Datei zum Lesen öffnen. In diesem Schritt verwenden wir einen `FileInputStream`, um auf die EPUB‑Datei zuzugreifen.

```java
try (FileInputStream fileInputStream = new FileInputStream("path/to/your/input.epub")) {
    // Your code for Step 1
}
```

## MemoryStreamProvider erstellen

Als Nächstes erstellen Sie eine Instanz von `MemoryStreamProvider`. Dieses Objekt hält die Konvertierungsausgabe im Speicher.

```java
try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
    // Your code for Step 2
}
```

## EPUB in XPS konvertieren

Jetzt konvertieren Sie die EPUB‑Datei mit der Methode `Converter.convertEPUB` in XPS. Der `MemoryStreamProvider` liefert den Ziel‑Stream.

```java
Converter.convertEPUB(
    fileInputStream,
    new XpsSaveOptions(),
    streamProvider.getStream().findFirst().get()
);
```

## Ergebnisdaten abrufen

Nachdem die Konvertierung abgeschlossen ist, rufen Sie den Memory‑Stream ab, der die XPS‑Daten enthält.

```java
InputStream inputStream = streamProvider.getStream().findFirst().get();
```

## Ausgabe speichern (optional)

Falls Sie eine physische Datei benötigen – vielleicht zum Debuggen oder zur Offline‑Inspektion – schreiben Sie den Memory‑Stream auf die Festplatte. In den meisten Produktionsszenarien können Sie diesen Schritt überspringen und die Daten direkt an den Client streamen.

```java
try (FileOutputStream fileOutputStream = new FileOutputStream("path/to/your/output.xps")) {
    byte[] buffer = new byte[inputStream.available()];
    inputStream.read(buffer);
    fileOutputStream.write(buffer);
}
```

## Vollständiger Quellcode

Unten finden Sie das vollständige, sofort ausführbare Beispiel, das alle Teile zusammenführt. Sie können es gerne kopieren, einfügen und an Ihr Projekt anpassen.

```java
        // Open an existing EPUB file for reading.
        try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream(Resources.input("input.epub"))) {
            // Create an instance of MemoryStreamProvider
            try (MemoryStreamProvider streamProvider = new MemoryStreamProvider()) {
                // Convert EPUB to XPS by using the MemoryStreamProvider
                com.aspose.html.converters.Converter.convertEPUB(
                        fileInputStream,
                        new com.aspose.html.saving.XpsSaveOptions(),
                        streamProvider.lStream
                );
                // Get access to the memory stream that contains the resulted data
                java.io.InputStream inputStream = streamProvider.lStream.stream().findFirst().get();
                // Flush the result data to the output file
                try (java.io.FileOutputStream fileOutputStream = new java.io.FileOutputStream(Resources.output("output.xps"))) {
                    byte[] buffer = new byte[inputStream.available()];
                    inputStream.read(buffer);
                    fileOutputStream.write(buffer);
                }
            }
        }
```

## Häufige Probleme und Lösungen

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **`java.lang.OutOfMemoryError`** | Große EPUB‑Dateien können die Standard‑Heap‑Größe überschreiten, wenn sie vollständig im Speicher gehalten werden. | Erhöhen Sie den JVM‑Heap (`-Xmx`) oder verarbeiten Sie die EPUB‑Datei nach Möglichkeit in Teilen. |
| Fehlende Schriftarten in XPS | Schriftarten, die nicht im EPUB eingebettet sind, stehen auf der Konvertierungsmaschine nicht zur Verfügung. | Stellen Sie sicher, dass die benötigten Schriftarten auf dem Server installiert sind oder betten Sie sie in das EPUB ein. |
| `UnsupportedOperationException` von `MemoryStreamProvider` | Verwendung einer veralteten Aspose.HTML‑Version. | Aktualisieren Sie auf die neueste Aspose.HTML for Java‑Version. |

## Häufig gestellte Fragen

### 1. Was ist EPUB?

EPUB, kurz für Electronic Publication, ist ein weit verbreitetes Dateiformat für E‑Books. Es ist so konzipiert, dass es auf verschiedenen Geräten wie E‑Readern, Tablets und Smartphones leicht lesbar ist.

### 2. Was ist XPS?

XPS steht für XML Paper Specification, ein von Microsoft geschaffenes Dokumentformat. Es wird zum Teilen und Archivieren von Dokumenten mit einheitlichem Aussehen und Layout verwendet.

### 3. Warum Aspose.HTML for Java verwenden?

Aspose.HTML for Java ist eine leistungsstarke Bibliothek, die Aufgaben der Dokumentmanipulation, -konvertierung und -rendering vereinfacht. Sie bietet umfangreiche Funktionen und Unterstützung für verschiedene Dokumentformate und ist damit ein wertvolles Werkzeug für Entwickler.

### 4. Kann ich mit Aspose.HTML for Java andere Dokumentformate konvertieren?

Ja, Aspose.HTML for Java unterstützt die Konvertierung verschiedener Dokumentformate, einschließlich HTML, EPUB, XPS und mehr. Es ist ein vielseitiges Werkzeug für das Dokumentenmanagement.

### 5. Wo finde ich zusätzliche Ressourcen und Support?

Für Dokumentation und Support besuchen Sie die [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/) und das [support forum](https://forum.aspose.com/).

---

**Zuletzt aktualisiert:** 2026-01-07  
**Getestet mit:** Aspose.HTML for Java 24.12 (zuletzt zum Zeitpunkt des Schreibens)  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}