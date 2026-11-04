---
category: general
date: 2026-04-03
description: Erfahren Sie, wie Sie die Sandbox in Aspose.HTML Java verwenden, um den
  User‑Agent festzulegen, die Größe zu setzen und die Viewport‑Größe sofort zu erhalten.
  Vollständiger Code, Erklärungen und Tipps inklusive.
draft: false
keywords:
- how to use sandbox
- set user agent
- get viewport size
- how to set size
- how to get viewport
language: de
og_description: Erfahren Sie, wie Sie die Sandbox in Aspose.HTML Java verwenden, um
  den User‑Agent festzulegen, die Größe zu setzen und die Viewport‑Größe sofort zu
  ermitteln. Vollständige Anleitung mit Code und bewährten Methoden.
og_title: Wie man Sandbox verwendet – User-Agent setzen & Viewport-Größe ermitteln
tags:
- AsposeHTML
- Java
- Sandbox
title: Wie man Sandbox verwendet – User-Agent festlegen & Viewport-Größe ermitteln
url: /de/java/configuring-environment/how-to-use-sandbox-set-user-agent-get-viewport-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Sandbox verwendet – User‑Agent festlegen & Viewport‑Größe ermitteln

Haben Sie sich jemals gefragt, **wie man Sandbox** beim Rendern von HTML mit Aspose.HTML für Java verwendet? Vielleicht sind Sie an eine Grenze gestoßen, wenn Sie eine bestimmte Bildschirmgröße simulieren wollten, oder Sie müssen einen User‑Agent‑String fälschen, damit die Seite sich so verhält, als würde sie von einem mobilen Browser besucht.  

Die gute Nachricht ist, dass die Sandbox‑API genau das ermöglicht, und Sie können nach dem Laden der Seite auch die berechnete Viewport‑Größe abrufen. In diesem Tutorial führen wir Sie durch das Erstellen einer Sandbox, das Festlegen der Größe, das Setzen eines benutzerdefinierten User‑Agents, das Laden einer Remote‑Seite und schließlich das Auslesen der Viewport‑Dimensionen. Am Ende wissen Sie **wie man Größe festlegt**, **wie man den Viewport abruft** und warum diese Schritte für zuverlässiges Headless‑Rendering wichtig sind.

> **Schneller Erfolg:** Sie erhalten eine ausführbare Java‑Klasse, die in Sekunden etwas wie `Viewport: 1280×800` ausgibt.

---

## Was Sie benötigen

- **Aspose.HTML for Java** Version 24.6 oder neuer (die von uns verwendete API wurde in 24.5 eingeführt).  
- Ein Java 17+ Development Kit (jedes aktuelle JDK funktioniert).  
- Eine IDE oder ein einfacher Texteditor – keine speziellen Plugins erforderlich.  
- Internetzugang, wenn Sie eine externe URL wie `https://example.com` laden möchten.

Das war's. Keine Maven/Gradle‑Magie ist zwingend erforderlich; Sie können die JARs bei Bedarf manuell in den Klassenpfad legen.  

---

## Wie man Sandbox verwendet – Überblick

Die Sandbox isoliert die Rendering‑Engine vom Host‑OS, sodass Sie einen virtuellen Bildschirm (Breite, Höhe, DPI) und einen benutzerdefinierten **User‑Agent**‑String definieren können. Denken Sie an ein Mini‑Browser‑Fenster, das vollständig im Speicher lebt. Wenn Sie später das `HTMLDocument` nach seiner Standard‑Ansicht fragen, meldet die Engine die **Viewport‑Größe**, die basierend auf den Sandbox‑Einstellungen berechnet wurde.  

Im Folgenden ein High‑Level‑Ablauf:

1. **Erstellen** Sie ein `DocumentSandbox` und konfigurieren Sie Breite, Höhe, DPI und User‑Agent.  
2. **Laden** Sie ein `HTMLDocument` innerhalb dieser Sandbox.  
3. **Abfragen** Sie die Standard‑Ansicht des Dokuments nach der Viewport‑Größe.  

Lassen Sie uns jeden Schritt genauer betrachten.

---

## Schritt 1: Sandbox erstellen und Größe festlegen

Zuerst starten wir eine Sandbox und geben ihr vor, wie groß der virtuelle Bildschirm sein soll. Hier beantworten Sie die Frage **wie man Größe festlegt** für ein Headless‑Rendern.

```java
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.drawing.Size2D;

/* Step 1 – instantiate the sandbox */
DocumentSandbox sandbox = new DocumentSandbox();

/* Set the virtual screen width & height (in pixels) */
sandbox.setScreenWidth(1280);   // width in pixels
sandbox.setScreenHeight(800);   // height in pixels

/* DPI influences CSS pixel calculations – 96 is the CSS default */
sandbox.setDeviceDpi(96);

/* Optional: give the sandbox a friendly name for debugging */
sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");
```

> **Pro‑Tipp:** Wenn Sie ein responsives Layout testen, probieren Sie eine schmale Breite wie `360`, um ein Telefon zu emulieren, oder eine breite wie `1920` für einen Desktop. Die Sandbox respektiert das eingestellte DPI, sodass ein hochdichter Bildschirm (z. B. 144 DPI) Media‑Queries beeinflusst, die `device-pixel-ratio` verwenden.

---

## Schritt 2: User‑Agent für die Sandbox festlegen

Warum einen benutzerdefinierten **User‑Agent** verwenden? Einige Websites liefern je nach gemeldetem Browser unterschiedliche Markups oder Skripte. Durch Aufruf von `setUserAgent` können Sie die Seite täuschen, dass sie von Chrome, Firefox oder einem mobilen Gerät besucht wird.

```java
/* Step 2 – customize the user‑agent string */
sandbox.setUserAgent("Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
                     "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                     "Version/15.0 Mobile/15E148 Safari/604.1");
```

Jetzt wird die Seite denken, sie würde auf einem iPhone gerendert. Wenn Sie den **User‑Agent** wieder auf den Standard zurücksetzen möchten, verwenden Sie einfach den vorherigen String „AsposeHTML/24.6 …“.

---

## Schritt 3: HTML‑Dokument innerhalb der Sandbox laden

Mit der vorbereiteten Sandbox können wir jede URL oder lokale HTML‑Datei laden. Der `HTMLDocument`‑Konstruktor nimmt die Sandbox als zweiten Parameter entgegen und bindet die beiden zusammen.

```java
import com.aspose.html.HTMLDocument;

/* Step 3 – load the page using the configured sandbox */
try (HTMLDocument doc = new HTMLDocument("https://example.com", sandbox)) {
    // The document is now rendered inside the sandbox environment.
    // Any JavaScript or CSS will see the size and user‑agent we defined.
```

Der `try‑with‑resources`‑Block sorgt dafür, dass das Dokument ordnungsgemäß freigegeben wird und native Ressourcen, die Aspose.HTML im Hintergrund allokiert, freigeschaltet werden.

---

## Schritt 4: Viewport‑Größe aus dem Dokument abrufen

Hier kommt der Moment, auf den Sie gewartet haben: das Abrufen der **Viewport‑Größe**, die die Rendering‑Engine berechnet hat. Das beantwortet **wie man den Viewport abruft** nach dem Layout der Seite.

```java
    /* Step 4 – fetch the viewport dimensions */
    Size2D viewport = doc.getDefaultView().getScreenSize();
    System.out.println("Viewport: " + viewport.getWidth() + "×" + viewport.getHeight());
}
```

Wenn Sie das Programm ausführen, sollten Sie etwas Ähnliches sehen:

```
Viewport: 1280×800
```

Wenn Sie die Sandbox‑Dimensionen in Schritt 1 geändert haben, spiegeln die ausgegebenen Zahlen diese neuen Werte wider – perfekt für automatisierte Tests, die responsive Breakpoints verifizieren.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie die komplette, sofort ausführbare Klasse, die alle Bausteine zusammenführt. Kopieren Sie sie in eine Datei namens `SandboxExample.java`, fügen Sie die Aspose.HTML‑JARs Ihrem Klassenpfad hinzu und führen Sie `java SandboxExample` aus.

```java
import com.aspose.html.*;
import com.aspose.html.drawing.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox with a custom screen size and DPI
        DocumentSandbox sandbox = new DocumentSandbox();
        sandbox.setScreenWidth(1280);          // width in pixels
        sandbox.setScreenHeight(800);          // height in pixels
        sandbox.setDeviceDpi(96);              // screen DPI
        sandbox.setUserAgent("AsposeHTML/24.6 (Linux; Java)");

        // Step 2: (Optional) Override the user agent if you need a mobile profile
        sandbox.setUserAgent(
            "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) " +
            "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
            "Version/15.0 Mobile/15E148 Safari/604.1");

        // Step 3: Load the HTML document inside the configured sandbox
        try (HTMLDocument htmlDocument = new HTMLDocument("https://example.com", sandbox)) {

            // Step 4: Retrieve and display the computed viewport size
            Size2D viewportSize = htmlDocument.getDefaultView().getScreenSize();
            System.out.println("Viewport: " + viewportSize.getWidth() + "×" + viewportSize.getHeight());
        }
    }
}
```

**Erwartete Ausgabe** (unter Annahme der oben genannten Sandbox‑Einstellungen):

```
Viewport: 1280×800
```

Wenn Sie eine andere Breite/Höhe in der Sandbox festlegen, ändert sich die Ausgabe entsprechend – genau das, was Sie beim Testen responsiver Designs benötigen.

---

## Randfälle & häufige Fragen

### Was, wenn die Seite `window.innerWidth` anstelle von CSS‑Media‑Queries verwendet?

Die virtuelle Bildschirmgröße der Sandbox beeinflusst sowohl das CSS‑Layout als auch das JavaScript‑`window.innerWidth/innerHeight`. Daher liefert **wie man den Viewport abruft** über JavaScript dieselben Zahlen, die Sie in der Java‑Konsole sehen.

### Kann ich mehrere Sandboxes parallel ausführen?

Ja. Jede `DocumentSandbox`‑Instanz ist unabhängig, sodass Sie einen Thread‑Pool starten, jedem Thread seine eigene Sandbox mit unterschiedlichen Dimensionen zuweisen und dutzende Seiten gleichzeitig rendern können. Denken Sie nur daran, die JARs thread‑sicher zu halten (sie sind es).

### Wirkt sich die DPI‑Einstellung auf die Bildskalierung aus?

Absolut. Ein höheres DPI lässt einen CSS‑Pixel auf mehr Geräte‑Pixel abbilden, was dazu führen kann, dass hochauflösende Bilder schärfer erscheinen. Wenn Sie Retina‑artige Assets testen, probieren Sie `sandbox.setDeviceDpi(144)`.

### How do I handle HTTPS certificates that are self

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}