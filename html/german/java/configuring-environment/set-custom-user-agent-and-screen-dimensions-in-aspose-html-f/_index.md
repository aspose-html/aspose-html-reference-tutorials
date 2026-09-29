---
category: general
date: 2026-09-29
description: Legen Sie einen benutzerdefinierten User‑Agent in Aspose.HTML für Java
  fest und erfahren Sie, wie Sie die virtuelle Bildschirmgröße für eine genaue HTML‑Darstellung
  einstellen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: de
lastmod: 2026-09-29
og_description: Legen Sie einen benutzerdefinierten User‑Agent in Aspose.HTML für
  Java fest und erfahren Sie, wie Sie die virtuelle Bildschirmgröße für eine genaue
  HTML‑Darstellung einstellen.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Benutzerdefinierten User-Agent und Bildschirmabmessungen in Aspose.HTML
  für Java festlegen
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Benutzerdefinierten User-Agent und Bildschirmabmessungen in Aspose.HTML für
  Java festlegen
url: /de/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benutzerdefinierten User-Agent und Bildschirmabmessungen in Aspose.HTML für Java festlegen

Wenn Sie beim Rendern von HTML mit Aspose.HTML für Java **einen benutzerdefinierten User-Agent festlegen** müssen, zeigt Ihnen dieser Leitfaden genau, wie das geht. Durch die Konfiguration eines Sandboxes erhalten Sie außerdem die Möglichkeit, **die virtuelle Bildschirmgröße festzulegen**, sodass das Layout einem echten Browser-Viewport entspricht.

Sie schließen dieses Tutorial mit einem vollständigen, ausführbaren Programm ab, das **den User-Agent angibt**, **die Bildschirmbreite festlegt** und **die Bildschirmhöhe festlegt**. Es werden keine externen Werkzeuge benötigt – nur Aspose.HTML für Java und eine Java 8+ Laufzeit.

## Was Sie lernen werden

* Wie man eine `SandboxConfiguration` erstellt, um das Rendern zu isolieren.
* Wie man **einen benutzerdefinierten User-Agent festlegt** und warum das für responsive Seiten wichtig ist.
* Wie man **die virtuelle Bildschirmgröße festlegt** (Bildschirmbreite und -höhe) für ein genaues Layout.
* Wie man eine HTML-Datei im Sandbox lädt und das verarbeitete Ergebnis speichert.
* Häufige Fallstricke und Best‑Practice‑Tipps für sandboxbasiertes Rendering.

> **Voraussetzungen** – Sie benötigen eine gültige Aspose.HTML für Java Lizenz, Java 8 oder neuer und eine IDE (IntelliJ IDEA, Eclipse oder VS Code). Das Beispiel verwendet eine lokale `input.html`‑Datei, aber jede erreichbare URL funktioniert.

![Sandbox-Flussdiagramm](sandbox-flow.png "Beispiel für benutzerdefinierten User-Agent in Java")

## Schritt 1: Erstellen einer Sandbox-Konfiguration (die Grundlage)

Die Sandbox isoliert die Rendering-Umgebung von der Host‑JVM, was wichtig ist, wenn Sie **einen benutzerdefinierten User-Agent festlegen** oder die Viewport‑Größe ändern möchten.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Warum dieser Schritt?*  
`SandboxConfiguration` enthält alle Rendering‑Optionen, einschließlich **Bildschirmabmessungen** und **User‑Agent**‑Strings. Durch die Konfiguration vor dem Laden des Dokuments stellen Sie sicher, dass die HTML‑Engine diese Einstellungen bereits bei der ersten Anforderung berücksichtigt.

## Schritt 2: Bildschirmabmessungen festlegen, um ein echtes Gerät zu simulieren

Responsive Websites lesen häufig `window.innerWidth` und `window.innerHeight`. Um die Engine glauben zu lassen, sie läuft auf einem 1024 × 768‑Bildschirm, **legen Sie die virtuelle Bildschirmgröße fest**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Warum das wichtig ist* – Wenn Sie **Bildschirmabmessungen festlegen** weglassen, könnte der Renderer standardmäßig ein winziges Viewport verwenden, wodurch CSS‑Media‑Queries das mobile Layout auswählen. Durch das explizite **Festlegen der Bildschirmbreite** und **Festlegen der Bildschirmhöhe** steuern Sie, welche CSS‑Regeln angewendet werden.

## Schritt 3: Einen benutzerdefinierten User‑Agent‑String angeben

Einige Webseiten liefern unterschiedliche Inhalte basierend auf dem User‑Agent‑Header. Um **den User-Agent anzugeben**, setzen Sie ihn einfach in der Sandbox‑Konfiguration:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Warum einen benutzerdefinierten User‑Agent verwenden?*  
Ein benutzerdefinierter String kann Bot‑Erkennungen umgehen, Desktop‑only‑Funktionen auslösen oder testen, wie sich eine Seite für eine bestimmte Browser‑Version verhält. Die Aspose‑Engine leitet diesen Wert bei jeder HTTP‑Anfrage weiter, die beim Laden externer Ressourcen (CSS, Bilder, Skripte) gestellt wird.

## Schritt 4: Das HTML‑Dokument innerhalb der Sandbox laden

Da die Sandbox nun vollständig konfiguriert ist, laden Sie die HTML‑Datei. Der Konstruktor, der einen Dateipfad und eine `SandboxConfiguration` entgegennimmt, wendet automatisch alle von uns definierten Einstellungen an.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Wenn Sie von einer entfernten URL laden müssen, ersetzen Sie den Dateipfad durch den URL‑String – Aspose.HTML wird weiterhin den **festgelegten benutzerdefinierten User‑Agent** und die **Bildschirmabmessungen** berücksichtigen.

## Schritt 5: Das verarbeitete Ergebnis speichern

Nachdem das Dokument das Laden abgeschlossen hat, können Sie es in einem beliebigen unterstützten Format speichern. Hier schreiben wir eine sandbox‑geprüfte HTML‑Datei, die alle DOM‑Änderungen widerspiegelt, die durch die benutzerdefinierten Einstellungen verursacht wurden.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

Die gespeicherte Datei enthält das gleiche Markup, aber Skripte, die `navigator.userAgent` abgefragt oder `window.innerWidth` inspiziert haben, sehen nun die von Ihnen bereitgestellten Werte.

## Vollständiges, ausführbares Beispiel

Wenn Sie alle Schritte zusammenfügen, erhalten Sie ein eigenständiges Programm, das Sie kopieren, einfügen und ausführen können.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Erwartete Ausgabe

Das Ausführen des Programms erzeugt `sandboxed_output.html`. Wenn Sie diese Datei in einem Browser öffnen und `navigator.userAgent` über die Konsole inspizieren, sehen Sie **AsposeHTML/1.0**. Ebenso wird `window.innerWidth` **1024** melden, was bestätigt, dass **die Bildschirmabmessungen festgelegt** wie beabsichtigt funktioniert haben.

## Häufige Fragen & Edge‑Case‑Behandlung

| Frage | Antwort |
|----------|--------|
| **Was, wenn die Seite zusätzliche Ressourcen von einer anderen Domain lädt?** | Die Sandbox leitet den **benutzerdefinierten User‑Agent** bei jeder Anfrage weiter, aber Cross‑Origin‑Richtlinien gelten weiterhin. Verwenden Sie `sandboxConfig.setAllowCrossDomain(true)`, wenn Sie diese Beschränkungen lockern müssen. |
| **Kann ich die Bildschirmgröße ändern, nachdem das Dokument geladen wurde?** | Nein. Die Bildschirmabmessungen werden während des initialen Layout‑Durchlaufs gelesen. Um mit einer anderen Größe zu rendern, erstellen Sie eine neue `SandboxConfiguration` und laden das Dokument erneut. |
| **Muss ich `document.close()` aufrufen?** | Das `HTMLDocument` implementiert `AutoCloseable`. Die Verwendung eines try‑with‑resources‑Blocks sorgt für ordnungsgemäße Bereinigung, aber ein explizites `close()` ist in einfachen Skripten optional. |
| **Wie unterscheidet sich das vom Setzen eines User‑Agents in einem HTTP‑Client?** | Das Setzen des User‑Agents in der Sandbox beeinflusst **alle** Ressourcenanfragen, die von der HTML‑Engine gestellt werden, nicht nur den initialen HTML‑Abruf. Das ahmt einen echten Browser genauer nach. |
| **Ist die Sandbox sicher für nicht vertrauenswürdiges HTML?** | Ja. Die Sandbox isoliert den Dateisystemzugriff und begrenzt Netzwerkaufrufe gemäß der Konfiguration, wodurch das Risiko reduziert wird, dass bösartige Skripte Ihre Host‑JVM beeinflussen. |

## Pro‑Tipps

* **Konfigurationen wiederverwenden** – Wenn Sie viele Seiten mit demselben Viewport rendern, erstellen Sie eine einzelne `SandboxConfiguration` und verwenden Sie sie erneut, um den Overhead bei der Objekterstellung zu vermeiden.
* **Mit Logging debuggen** – Aktivieren Sie das Aspose.HTML‑Logging (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`), um zu sehen, welche Ressourcen mit dem benutzerdefinierten User‑Agent abgerufen wurden.
* **Mit CSS‑Media‑Queries kombinieren** – Durch Anpassen der **Bildschirmbreite** können Sie testen, wie Ihr responsives Design auf Tablets, Handys oder großen Desktops funktioniert, ohne einen echten Browser zu öffnen.

## Fazit

Sie wissen jetzt, wie Sie **einen benutzerdefinierten User‑Agent festlegen** und **Bildschirmabmessungen festlegen** können, wenn Sie HTML mit Aspose.HTML für Java rendern. Durch die Konfiguration einer Sandbox isolieren Sie die Umgebung, steuern das Viewport und stellen sicher, dass externe Ressourcen die exakt von Ihnen angegebenen Header sehen. Diese Technik ist entscheidend zum Testen responsiver Layouts, zum Umgehen von Bot‑Blockaden oder zum Reproduzieren von Desktop‑Only‑Funktionen in automatisierten Pipelines.

Als Nächstes könnten Sie **wie man benutzerdefinierte Cookies setzt** oder **gerenderte Screenshots erfasst** mit der Rendering‑API von Aspose.HTML erkunden – beide Konzepte basieren auf dem gleichen Sandbox‑Konfigurations‑Muster, das Sie gerade gemeistert haben.

Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [High‑DPI‑Rendering in Java – Webseiten‑Screenshots mit benutzerdefiniertem User‑Agent erfassen](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [Wie man HTML lädt, Geräte‑DPI festlegt & Hintergrundfarbe ausliest](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [HTML‑Datei in Java erstellen & Netzwerk‑Service einrichten (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}