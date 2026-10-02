---
category: general
date: 2026-02-11
description: Erstellen Sie ein HTML‑Dokument in Java mit Aspose.HTML. Erfahren Sie,
  wie Sie JSON‑JavaScript abrufen, ein Skriptelement hinzufügen, HTML aus JSON generieren
  und JSON in pre konvertieren.
draft: false
keywords:
- create html document
- fetch json javascript
- add script element
- generate html from json
- convert json to pre
language: de
og_description: Erstellen Sie ein HTML‑Dokument in Java mit Aspose.HTML. JSON‑JavaScript
  abrufen, Skriptelement hinzufügen, HTML aus JSON generieren und JSON in <pre> umwandeln
  – alles in einem Tutorial.
og_title: HTML-Dokument in Java erstellen – Vollständige Anleitung
tags:
- Aspose.HTML
- Java
- Web Automation
title: HTML-Dokument mit Java erstellen – JSON abrufen und Inhalt generieren
url: /de/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML-Dokument erstellen – Vollständiges Java-Tutorial

Haben Sie jemals **HTML-Dokument erstellen** müssen, während das Programm läuft, waren sich aber nicht sicher, wie Sie entfernte Daten einbinden können? Sie sind nicht allein. In vielen Projekten möchten Sie JSON mit JavaScript abrufen, das Ergebnis in eine Seite einfügen und dann das endgültige Markup als statische Datei speichern. Dieser Leitfaden zeigt Ihnen genau, wie das mit Aspose.HTML für Java funktioniert.

## Voraussetzungen

- Java 17 oder neuer (der Code kompiliert auch mit JDK 11+)
- Aspose.HTML für Java Bibliothek (verfügbar über Maven Central)
- Grundlegende Kenntnisse in HTML und asynchronem JavaScript
- Eine IDE oder reiner `javac`/`java` Befehlszeile

## Schritt 1: Projekt einrichten und Aspose.HTML importieren

Fügen Sie zunächst die Aspose.HTML-Abhängigkeit zu Ihrer `pom.xml` hinzu (oder laden Sie das JAR manuell herunter).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- latest as of Feb 2026 -->
</dependency>
```

> **Profi‑Tipp:** Halten Sie die Versionsnummer aktuell; neuere Releases beheben Fehler und verbessern die Skript‑Engine.

## Schritt 2: **HTML-Dokument erstellen** – die leere Leinwand

Wir beginnen mit dem Erstellen eines leeren `HTMLDocument`. Stellen Sie sich das als eine frische Seite vor, in die wir später unser Skript einfügen.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();
```

Warum benötigen wir ein Dokumentobjekt? Die `ScriptEngine` von Aspose.HTML arbeitet gegen ein DOM, nicht gegen einen rohen String. Durch das Erstellen eines richtigen Dokuments geben wir der Engine eine reale Umgebung, um unser **fetch JSON JavaScript** auszuführen.

## Schritt 3: JavaScript‑Snippet schreiben – **Fetch JSON JavaScript** und **Convert JSON to pre**

Der Kern des Tutorials befindet sich in diesem mehrzeiligen String. Er führt ein asynchrones `fetch` aus, parsed das JSON und schreibt anschließend ein `<pre>`‑Element mit hübsch formatierten Daten.

```java
        // Step 3: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;
```

Beachten Sie den Kommentar *Convert JSON to <pre>* – genau das bewirkt der Aufruf `JSON.stringify(..., null, 2)`. Er fügt Einrückungen hinzu und macht die Ausgabe menschenlesbar.

## Schritt 4: **Script‑Element hinzufügen** zum Dokument

Jetzt erstellen wir ein `<script>`‑Tag, fügen unseren Code ein und hängen es an den Body an. Das ist der **add script element**‑Teil.

```java
        // Step 4: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);
```

Warum an den Body anhängen? In einem echten Browser würde das Skript sofort nach dem Parsen ausgeführt werden. Durch das Anhängen an das DOM imitieren wir genau dieses Verhalten und stellen sicher, dass das asynchrone fetch ausgeführt wird, wenn wir später die Engine aufrufen.

## Schritt 5: Script‑Engine ausführen – das asynchrone Fetch abschließen lassen

Aspose.HTML stellt eine `ScriptEngine` bereit, die das DOM‑basierte JavaScript ausführen kann. Wir rufen `run()` auf und warten, bis die Promise‑Kette abgewickelt ist.

```java
        // Step 5: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();
```

Die Engine blockiert, bis alle ausstehenden Aufgaben (unser fetch) abgeschlossen sind, wodurch garantiert wird, dass das erzeugte HTML bereits die Daten enthält.

## Schritt 6: **HTML aus JSON generieren** – Ergebnis speichern

Abschließend speichern wir das Dokument auf die Festplatte. Die Datei enthält nun den `<pre>`‑Block mit der JSON‑Nutzlast.

```java
        // Step 6: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

Das Ausführen des Programms erzeugt `fetchResult.html`. Öffnen Sie es in einem beliebigen Browser und Sie sehen etwa Folgendes:

```html
<pre>{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}</pre>
```

Das ist das Ergebnis **generate HTML from JSON**, das Sie gesucht haben.

## Vollständiges funktionierendes Beispiel

Unten finden Sie die komplette, sofort ausführbare Quelldatei. Kopieren, einfügen, den Ausgabepfad anpassen und `java JsFetchExample` ausführen.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import com.aspose.html.scripting.*;

public class JsFetchExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an empty HTML document that will host the script
        HTMLDocument htmlDoc = new HTMLDocument();

        // Step 2: Define a JavaScript snippet that fetches JSON data and injects it into the page
        String fetchScript = """
            (async function() {
                const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
                const data = await response.json();
                // Convert JSON to <pre> for readable formatting
                document.body.innerHTML = '<pre>' + JSON.stringify(data, null, 2) + '</pre>';
            })();
            """;

        // Step 3: Add the script element to the document's body
        HTMLScriptElement scriptElement = (HTMLScriptElement) htmlDoc.createElement("script");
        scriptElement.setTextContent(fetchScript);
        htmlDoc.getBody().appendChild(scriptElement);

        // Step 4: Run the script engine so the asynchronous fetch completes before saving
        ScriptEngine scriptEngine = new ScriptEngine(htmlDoc);
        scriptEngine.run();

        // Step 5: Save the resulting HTML, which now contains the fetched data
        htmlDoc.save("YOUR_DIRECTORY/fetchResult.html");
        System.out.println("HTML with fetched data saved.");
    }
}
```

## Erwartete Ausgabe & Verifizierung

1. **Konsole:** Sie sehen `HTML with fetched data saved.`  
2. **Datei (`fetchResult.html`):** Beim Öffnen wird das JSON innerhalb eines `<pre>`‑Blocks, schön eingerückt, angezeigt.  
3. **Validierung:** Wenn Sie den Seitenquelltext ansehen, finden Sie nur ein `<pre>`‑Element – keine zusätzlichen Script‑Tags mehr, da die Engine sie bereits ausgeführt hat.

## Häufige Fragen & Sonderfälle

| Frage | Antwort |
|----------|--------|
| *Was ist, wenn die API einen Fehler zurückgibt?* | Wickeln Sie den `fetch`‑Aufruf in einen `try…catch`‑Block und schreiben Sie eine Fehlermeldung in den Body anstelle des JSON. |
| *Kann ich mehrere Ressourcen abrufen?* | Ja – verketten Sie einfach weitere `await fetch(...)`‑Aufrufe oder verwenden Sie `Promise.all`. Das finale `innerHTML` kann mehrere `<pre>`‑Blöcke zusammenfügen. |
| *Muss ich CORS‑Header setzen?* | Da das Skript innerhalb der Sandbox von Aspose.HTML läuft, respektiert es die Same‑Origin‑Policy. Der öffentliche JSONPlaceholder‑Endpunkt erlaubt bereits Cross‑Origin‑Anfragen. |
| *Wie ändere ich das Ausgabeverzeichnis zur Laufzeit?* | Übergeben Sie den Pfad als Befehlszeilenargument (`args[0]`) und ersetzen Sie den fest codierten String in `htmlDoc.save`. |
| *Gibt es eine Möglichkeit, CSS für das Styling einzubetten?* | Absolut. Erstellen Sie ein `<style>`‑Element, setzen Sie dessen `textContent` auf Ihr CSS und hängen Sie es vor dem Ausführen der Engine an `<head>` an. |

## Tipps für den Produktionseinsatz

- **Cache das JSON**, wenn der Endpunkt langsam ist; Sie können den abgerufenen String in eine Datei schreiben und wiederverwenden.
- **Sanitisieren Sie die Daten**, bevor Sie sie einfügen, besonders wenn die Quelle nicht vertrauenswürdig ist. Verwenden Sie `JSON.stringify` sicher oder escapen Sie HTML‑Entitäten.
- **Konfigurieren Sie das Timeout der ScriptEngine** (`scriptEngine.setTimeout(5000)`), um ein Hängenbleiben bei nicht reagierenden Diensten zu vermeiden.

## Visuelle Zusammenfassung

![Beispiel für das Erstellen eines HTML-Dokuments, das das generierte HTML mit JSON innerhalb eines pre‑Tags zeigt](fetchResult.png "Screenshot des generierten HTML-Dokuments")

*Alt‑Text:* *Beispiel für das Erstellen eines HTML‑Dokuments – generierte HTML‑Datei, die das abgerufene JSON innerhalb eines pre‑Elements anzeigt.*

## Fazit

Sie wissen jetzt, wie man programmgesteuert in Java **HTML-Dokument erstellen**, **fetch JSON JavaScript**, **script‑Element hinzufügen**, **HTML aus JSON generieren** und **JSON in pre** konvertiert, um lesbare Ausgaben zu erhalten. Der gesamte Workflow läuft offline, benötigt nur Aspose.HTML und erzeugt eine saubere statische Datei, die Sie überall bereitstellen können.

Als Nächstes können Sie das Skript erweitern, um über ein Array von Objekten zu iterieren, CSS‑Styling hinzuzufügen oder mehrere Seiten mit derselben Technik zu erstellen. Sie könnten auch die `fetch`‑URL durch Ihre eigene API ersetzen, um dynamische Daten in statische Schnappschüsse zu verwandeln – ideal für SEO‑freundliches Pre‑Rendering.

Viel Spaß beim Coden und teilen Sie gerne Ihre Experimente in den Kommentaren!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}