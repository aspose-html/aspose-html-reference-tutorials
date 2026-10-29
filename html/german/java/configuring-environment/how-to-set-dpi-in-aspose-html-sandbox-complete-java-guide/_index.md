---
category: general
date: 2026-04-02
description: Erfahren Sie, wie Sie DPI, die Viewport‑Größe und den User‑Agent im Aspose.HTML
  Sandbox festlegen. Schritt‑für‑Schritt‑Java‑Beispiel mit vollständigem Code und
  Tipps.
draft: false
keywords:
- how to set dpi
- set viewport size
- set user agent
- Aspose.HTML sandbox
- Java rendering settings
language: de
og_description: Meistern Sie das Setzen von DPI, Viewport-Größe und User-Agent im
  Aspose.HTML Sandbox mit einem vollständigen Java‑Beispiel.
og_title: Wie DPI im Aspose.HTML Sandbox festlegen – Java‑Tutorial
tags:
- Aspose.HTML
- Java
- Rendering
- Sandbox
title: Wie man DPI im Aspose.HTML‑Sandbox festlegt – Vollständiger Java‑Leitfaden
url: /de/java/configuring-environment/how-to-set-dpi-in-aspose-html-sandbox-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man DPI im Aspose.HTML Sandbox festlegt – Vollständige Java‑Anleitung

Haben Sie sich schon einmal gefragt, **wie man DPI** beim Rendern einer Webseite mit Aspose.HTML festlegt? Sie sind nicht allein. In vielen Test‑Szenarien muss das Layout einer bestimmten Bildschirm‑Dichte entsprechen – denken Sie an druckfertige PDFs oder hochauflösende Screenshots. Die gute Nachricht: Der Aspose.HTML Sandbox ermöglicht es Ihnen, DPI, Viewport‑Größe und sogar den User‑Agent‑String in einem kompakten Paket zu steuern.

In diesem Tutorial führen wir Sie durch ein praktisches Java‑Beispiel, das **DPI festlegt**, **die Viewport‑Größe setzt** und **den User‑Agent** gleichzeitig definiert. Am Ende haben Sie ein lauffähiges Programm, verstehen, warum jede Einstellung wichtig ist, und können den Sandbox für Ihre eigenen Projekte anpassen.

---

## Was Sie benötigen

- **Java 17** (oder ein aktuelles JDK; die API ist kompatibel mit Java 8+)
- **Aspose.HTML for Java** Bibliothek (Version 23.12 oder neuer)
- Eine IDE oder ein einfacher Text‑Editor + Kommandozeilen‑Kompilierung
- Internetzugang für die Beispiel‑URL (`https://example.com`)

Es werden keine externen Build‑Tools benötigt; der Code kompiliert mit `javac` und läuft mit `java`. Wenn Sie Maven oder Gradle bevorzugen, fügen Sie einfach die Aspose.HTML‑Abhängigkeit hinzu – nichts Aufwändiges.

---

## Schritt 1: Erstellen eines Sandbox, das die Render‑Umgebung definiert

Der Sandbox ist dort, wo Sie Aspose.HTML mitteilen, welchen „Bildschirm“ Sie simulieren möchten. Hier setzen wir einen **Viewport von 1024 × 768**, ein **DPI von 96** und einen benutzerdefinierten **User‑Agent‑String**.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox – this is the core of how to set dpi, viewport, and user agent.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent
```

**Warum das wichtig ist:**  
- **DPI** beeinflusst, wie CSS‑`pt`‑Einheiten in Pixel übersetzt werden; ein höheres DPI liefert schärferes Rendering.  
- **Viewport‑Größe** bestimmt die Layout‑Breakpoints, die responsives CSS auslöst.  
- **User‑Agent** kann serverseitige Inhaltsvarianten aktivieren (mobile vs. Desktop).

> **Pro‑Tipp:** Wenn Sie später PDFs erzeugen, passen Sie das DPI an die Ziel‑Druckauflösung an (z. B. 300 dpi für hochwertige Drucke).

---

## Schritt 2: Laden einer Webseite im Sandbox

Jetzt zeigen wir dem Sandbox eine URL. Der `HTMLDocument`‑Konstruktor akzeptiert den Sandbox, sodass die Layout‑Engine die von uns definierten Einstellungen berücksichtigt.

```java
        // Load the page using the sandbox we just configured.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {
```

**Was im Hintergrund passiert:**  
Aspose.HTML erstellt einen isolierten Rendering‑Kontext, ähnlich einem headless Browser, jedoch ohne den Overhead einer kompletten Chromium‑Instanz. Das macht den Vorgang schnell und speicherschonend – ideal für Batch‑Verarbeitung.

---

## Schritt 3: Interaktion mit dem DOM – Lesen des Seitentitels

Zur Demonstration holen wir den Titel und geben ihn aus. In einem realen Szenario könnten Sie einen Screenshot erstellen, als PDF exportieren oder Daten auslesen.

```java
            // Simple DOM interaction – fetch and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());
        }
    }
}
```

**Erwartete Ausgabe** (wenn `https://example.com` erreichbar ist):

```
Title inside sandbox: Example Domain
```

Wenn die Seite einen anderen Titel zurückgibt, sehen Sie diesen stattdessen – es muss nichts weiter geändert werden.

---

## Schritt 4: Überprüfen der Einstellungen (optionales Debugging)

Manchmal möchte man sicherstellen, dass der Sandbox die DPI‑ und Viewport‑Werte tatsächlich respektiert. Aspose.HTML stellt diese Werte nicht direkt bereit, aber Sie können sie durch Messung von Element‑Abmessungen ableiten.

```java
        // Example: measure a known element's width in pixels.
        int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
        System.out.println("Measured width (px): " + elementWidth);
```

Wenn Sie wissen, dass das CSS das Element mit `width: 200pt;` deklariert, sollten Sie bei **96 dpi** etwa `200pt * (96/72) ≈ 267px` sehen. Ändern Sie das DPI und führen Sie das Beispiel erneut aus, um die Zahl zu verändern – ein Beweis dafür, dass **wie man DPI setzt** tatsächlich funktioniert.

---

## Vollständiger Quellcode in einem Block

Kopieren Sie den folgenden Code in `SandboxExample.java`. Er kompiliert sofort; stellen Sie nur sicher, dass die Aspose.HTML‑JAR im Klassenpfad liegt.

```java
import com.aspose.html.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        // (viewport size 1024×768 and 96 dpi) and a custom user‑agent string.
        DocumentSandbox renderingSandbox = new DocumentSandbox(
                new Size(1024, 768),   // set viewport size
                96,                    // how to set dpi (96 dots per inch)
                "MyCustomUserAgent/1.0"); // set user agent

        // Step 2: Load a web page inside the sandbox so layout respects the settings.
        try (HTMLDocument webDoc = new HTMLDocument("https://example.com", renderingSandbox)) {

            // Step 3: Interact with the DOM – here we simply read and print the page title.
            System.out.println("Title inside sandbox: " + webDoc.getTitle());

            // Optional: verify DPI effect by measuring an element (if you know its CSS size).
            // int elementWidth = (int) webDoc.querySelector("div").getBoundingClientRect().getWidth();
            // System.out.println("Measured width (px): " + elementWidth);
        }
    }
}
```

Kompilieren und ausführen:

```bash
javac -cp "aspose-html-23.12.jar" SandboxExample.java
java -cp ".:aspose-html-23.12.jar" SandboxExample
```

Sie sollten den Titel sehen, was bestätigt, dass der Sandbox mit dem **festgelegten DPI**, **der festgelegten Viewport‑Größe** und dem **angegebenen User‑Agent** arbeitet.

---

## Häufige Fragen & Sonderfälle

### Was tun, wenn ich ein anderes DPI benötige?

Ändern Sie einfach das zweite Argument von `DocumentSandbox`. Für druckfertige PDFs könnten Sie `300` verwenden:

```java
new DocumentSandbox(new Size(1024, 768), 300, "MyCustomUserAgent/1.0");
```

Ein höheres DPI erzeugt größere Pixel‑Abmessungen für dieselben CSS‑Punkte, verbessert die Raster‑Qualität, verbraucht jedoch mehr Speicher.

### Kann ich eine lokale HTML‑Datei statt einer URL laden?

Natürlich. Ersetzen Sie die URL durch einen Dateipfad:

```java
HTMLDocument webDoc = new HTMLDocument("file:///C:/myfolder/page.html", renderingSandbox);
```

Stellen Sie sicher, dass der Pfad absolut ist und das `file:///`‑Schema verwendet.

### Wie ändere ich den User‑Agent, nachdem der Sandbox erstellt wurde?

Der Sandbox ist unveränderlich – sobald Sie ihn an `HTMLDocument` übergeben, sind die Einstellungen fest. Um einen anderen User‑Agent zu verwenden, erzeugen Sie einen neuen `DocumentSandbox` mit dem gewünschten String.

### Unterstützt Aspose.HTML die Ausführung von JavaScript?

Ja, die Engine führt die meisten client‑seitigen Skripte aus. Wenn ein Skript das DOM nach dem Laden verändert, können Sie kurz warten:

```java
webDoc.waitForLoad();
```

Oder Sie nutzen eine `setTimeout`‑ähnliche Logik innerhalb der Seite, bevor Sie Elemente abfragen.

---

## Visuelle Bestätigung (Bild)

![Konsolenausgabe, die zeigt, wie man DPI im Aspose.HTML Sandbox festlegt](/images/console-output.png)

*Alt‑Text:* *Konsolenausgabe, die demonstriert, wie man DPI, Viewport‑Größe und User‑Agent im Aspose.HTML Sandbox festlegt.*

---

## Zusammenfassung & nächste Schritte

Wir haben behandelt, **wie man DPI setzt** (96 dpi im Beispiel), **wie man die Viewport‑Größe festlegt** (1024 × 768) und **wie man den User‑Agent definiert** (benutzerdefinierter String) mithilfe der Sandbox‑API von Aspose.HTML. Das vollständige, ausführbare Java‑Programm beweist, dass diese Einstellungen nicht nur theoretisch sind – sie beeinflussen das Rendering und die DOM‑Interaktion direkt.

Bereit für mehr?

- **Export nach PDF:** Nach dem Laden der Seite `webDoc.save("output.pdf", SaveFormat.PDF);` aufrufen, um ein hochauflösendes PDF zu erzeugen, das das eingestellte DPI widerspiegelt.  
- **Screenshot erstellen:** `webDoc.renderToBitmap("screenshot.png");` verwenden für pixelgenaue Bilder.  
- **Responsive Layouts testen:** Ändern Sie die Viewport‑Abmessungen, um mobile Breakpoints zu prüfen, ohne ein echtes Gerät.

Experimentieren Sie mit verschiedenen DPI‑Werten, Viewport‑Kombinationen und User‑Agents, um zu sehen, wie Server und CSS reagieren. Der Sandbox ist ein leichtgewichtiges Spiel‑Feld, das Ihnen das Aufsetzen voller Browser erspart.

---

### Weiter erkunden

- **Aspose.HTML Dokumentation** – tiefere Einblicke in die Optionen von `DocumentSandbox`.  
- **Fortgeschrittene CSS‑Media‑Queries** – lernen Sie, wie die Viewport‑Größe unterschiedliche Styles auslöst.  
- **User‑Agent‑Spoofing** – entdecken Sie, wie manche Seiten basierend auf dem Agent‑String alternatives Markup liefern.

Haben Sie Fragen oder einen kniffligen Fall? Hinterlassen Sie einen Kommentar, und wir lösen das gemeinsam. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}