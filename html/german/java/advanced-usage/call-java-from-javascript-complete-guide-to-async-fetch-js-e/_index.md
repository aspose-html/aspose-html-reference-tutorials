---
category: general
date: 2026-03-04
description: Rufen Sie Java aus JavaScript mit Aspose.HTML auf, führen Sie asynchrones
  JavaScript aus und holen Sie JSON in Java mit einem einfachen Beispiel. Lernen Sie,
  die JavaScript‑Engine effizient auszuführen.
draft: false
keywords:
- call java from javascript
- run async javascript
- fetch json in java
- asynchronous fetch api
- execute javascript engine
language: de
og_description: Rufen Sie Java aus JavaScript mit Aspose.HTML auf, führen Sie asynchrones
  JavaScript aus und holen Sie JSON in Java. Vollständiger Code, Erklärungen und Tipps
  inklusive.
og_title: Java aus JavaScript aufrufen – Schritt‑für‑Schritt Async‑Fetch‑Tutorial
tags:
- Java
- JavaScript
- Aspose.HTML
- Async Programming
title: Java aus JavaScript aufrufen – Vollständiger Leitfaden zu Async Fetch & JS‑Engine‑Ausführung
url: /de/java/advanced-usage/call-java-from-javascript-complete-guide-to-async-fetch-js-e/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java von JavaScript aufrufen – Vollständiges Tutorial mit Async Fetch API

Haben Sie sich jemals gefragt, wie man **Java von JavaScript** aus aufruft, ohne Ihre Java‑Anwendung zu verlassen? Vielleicht bauen Sie einen serverseitigen HTML‑Renderer, oder Sie müssen etwas Java‑Logik einem Skript zugänglich machen, das innerhalb eines Dokuments läuft. Die gute Nachricht ist, dass Aspose.HTML das zum Kinderspiel macht. In diesem Leitfaden zeigen wir Ihnen nicht nur, wie man *asynchrones JavaScript* in einem Java‑basierten Dokument **ausführt**, sondern auch, wie man **JSON in Java** mit der modernen **asynchronen Fetch‑API** abruft und schließlich **JavaScript‑Engine**‑Aufrufe sicher **ausführt**.

Kurz gesagt erhalten Sie ein vollständiges, ausführbares Beispiel, das ein JSON‑Payload von einem öffentlichen Endpunkt abruft, es an ein Java‑Host‑Objekt übergibt und das Ergebnis in der Konsole ausgibt. Keine externen Web‑Server, keine zusätzlichen Bibliotheken – nur reines Java und Aspose.HTML.

## Was Sie lernen werden

- Wie man ein leeres HTML‑Dokument mit Aspose.HTML erstellt.
- Wie man die **execute JavaScript engine** von Java aus erhält.
- Wie man ein Java‑Host‑Objekt registriert, das von JavaScript aufgerufen werden kann.
- Wie man eine **asynchronous JavaScript**‑Funktion schreibt, die die **asynchronous fetch API** verwendet.
- Wie man die abgerufenen Daten in Java mit einem sauberen Callback verarbeitet.
- Erwartete Ausgabe und Tipps zur Fehlersuche.

### Voraussetzungen

- Java 17 oder neuer (der Code kompiliert auch mit JDK 11).
- Aspose.HTML für Java 23.7 (oder die zum Zeitpunkt des Schreibens neueste Version).
- Grundlegende Kenntnisse von Java und JavaScript‑Promises.
- Internetzugang für die Demo‑Anfrage `jsonplaceholder`.

Falls Ihnen etwas davon unbekannt ist, keine Panik – jeder Schritt wird in einfachem Englisch erklärt, und Sie werden genau sehen, warum wir tun, was wir tun.

---

## Schritt 1 – Erstellen Sie ein leeres HTML‑Dokument und holen Sie sich dessen JavaScript‑Engine

Das erste, was wir benötigen, ist ein leeres Dokument, das uns eine sandbox‑artige JavaScript‑Umgebung bietet. Die `Document`‑Klasse von Aspose.HTML erledigt genau das.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Create an empty HTML document
        Document document = new Document();

        // Obtain the JavaScript engine associated with the document's window
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();
```

**Warum das wichtig ist:** Das `Document`‑Objekt ahmt ein Browser‑Fenster nach, und seine `JavaScriptEngine` ermöglicht es uns, Skripte genau wie ein Browser auszuführen. Das ist die Grundlage für **call java from javascript** – die Engine fungiert als Brücke.

## Schritt 2 – Registrieren Sie ein Host‑Objekt, damit JavaScript zurück nach Java aufrufen kann

Aspose.HTML ermöglicht es Ihnen, jedes Java‑Objekt der Skriptwelt zugänglich zu machen. Wir erstellen eine anonyme Klasse mit einer einzigen `onResult`‑Methode, die einfach das empfangene JSON ausgibt.

```java
        // Register a Java host object that the script can invoke
        jsEngine.addHostObject("javaCallback", new Object() {
            // This method will be called from JavaScript with the fetched JSON string
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });
```

**Erklärung:**  
- `addHostObject` bindet den Namen `javaCallback` an das anonyme Java‑Objekt.  
- Innerhalb von JavaScript rufen wir `javaCallback.onResult(...)` auf.  
- Das ist das Kernstück von **call java from javascript** – das Skript greift in den Java‑Bereich ein, und Java reagiert.

> **Pro‑Tipp:** Halten Sie die Methoden des Host‑Objekts `public` und einfach; komplexe Objekte können Serialisierungsprobleme verursachen.

## Schritt 3 – Schreiben Sie eine asynchrone JavaScript‑Funktion unter Verwendung der asynchronen Fetch‑API

Jetzt kommt der spaßige Teil: ein winziges Skript, das JSON von einem entfernten Endpunkt abruft. Wir verwenden `async/await`, das die moderne Art ist, **run async JavaScript** auszuführen.

```java
        // Asynchronous script that fetches JSON and passes it to the Java host object
        String asyncScript =
            "async function fetchData() {" +
            "  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "  const json = await response.json();" +
            "  javaCallback.onResult(JSON.stringify(json));" +
            "}" +
            "fetchData();";
```

**Warum wir `fetch` gegenüber älterem XHR wählen:**  
- `fetch` gibt ein `Promise` zurück, was den Code sauberer macht.  
- Es funktioniert nativ mit `await`, sodass der Ablauf von oben nach unten gelesen wird – perfekt für **asynchronous fetch api**‑Demos.  
- Die API ist zukunftssicher; die meisten Browser und Engines (einschließlich Aspose) unterstützen sie sofort.

## Schritt 4 – Führen Sie das Skript innerhalb der JavaScript‑Engine des Dokuments aus

Schließlich übergeben wir das Skript an die Engine. Die Engine startet eine kleine Ereignisschleife, löst das `fetch`‑Promise auf und ruft Java zurück, wenn sie fertig ist.

```java
        // Execute the async script
        jsEngine.execute(asyncScript);
    }
}
```

Wenn Sie die Klasse `AsyncJsTutorial` ausführen, sollten Sie etwa Folgendes sehen:

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Diese Ausgabe bestätigt drei Dinge:

1. Die **asynchronous fetch API** hat erfolgreich Daten abgerufen.  
2. Das JSON wurde serialisiert und an Java übergeben.  
3. Unser **execute javascript engine**‑Aufruf wurde ohne Deadlocks abgeschlossen.

## Schritt 5 – Fehlerbehandlung und Randfälle (optionale Erweiterungen)

Im echten Einsatz läuft Code selten jedes Mal perfekt. Im Folgenden finden Sie einige häufige Fallstricke und wie man sie vermeidet.

### 5.1 Netzwerkfehler

Wenn der entfernte Server nicht erreichbar ist, wirft `fetch` eine Ausnahme. Wickeln Sie den Aufruf in einen `try/catch`‑Block:

```java
String asyncScript =
    "async function fetchData() {" +
    "  try {" +
    "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
    "    if (!response.ok) throw new Error('Network response was not ok');" +
    "    const json = await response.json();" +
    "    javaCallback.onResult(JSON.stringify(json));" +
    "  } catch (e) {" +
    "    javaCallback.onResult('Error: ' + e.message);" +
    "  }" +
    "}" +
    "fetchData();";
```

Jetzt erhält die Java‑Seite eine Fehlermeldung anstatt zu hängen.

### 5.2 Zeitüberschreitungen

Die Engine von Aspose stellt keinen nativen Timeout für `fetch` bereit, aber Sie können einen in JavaScript implementieren:

```javascript
const controller = new AbortController();
setTimeout(() => controller.abort(), 5000); // 5‑second timeout
const response = await fetch(url, { signal: controller.signal });
```

### 5.3 Mehrfache Aufrufe

Wenn Sie mehrere Ressourcen abrufen müssen, schleifen Sie einfach über ein Array von URLs oder verwenden Sie `map`. Das Host‑Objekt kann erweitert werden, um einen Bezeichner zu akzeptieren, sodass Sie Antworten korrelieren können.

## Vollständiges funktionierendes Beispiel

Unten finden Sie die **vollständige Quellcodedatei**, die Sie in Ihre IDE kopieren können. Keine versteckten Abhängigkeiten, nur das Aspose.HTML‑JAR im Klassenpfad.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty HTML document and obtain its JavaScript engine
        Document document = new Document();
        JavaScriptEngine jsEngine = document.getWindow().getJavaScriptEngine();

        // Step 2: Register a host object that JavaScript can call back into Java
        jsEngine.addHostObject("javaCallback", new Object() {
            public void onResult(String data) {
                System.out.println("Fetched data: " + data);
            }
        });

        // Step 3: Write an async function that uses the asynchronous fetch API
        String asyncScript =
            "async function fetchData() {" +
            "  try {" +
            "    const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');" +
            "    if (!response.ok) throw new Error('Network error');" +
            "    const json = await response.json();" +
            "    javaCallback.onResult(JSON.stringify(json));" +
            "  } catch (e) {" +
            "    javaCallback.onResult('Error: ' + e.message);" +
            "  }" +
            "}" +
            "fetchData();";

        // Step 4: Execute the script inside the document's JavaScript engine
        jsEngine.execute(asyncScript);
    }
}
```

**Erwartete Konsolenausgabe**

```
Fetched data: {"userId":1,"id":1,"title":"delectus aut autem","completed":false}
```

Wenn Sie eine Fehlermeldung sehen, die mit `Error:` beginnt, ist etwas schiefgelaufen – höchstwahrscheinlich ein Netzwerkproblem.

## Visueller Überblick

![Diagramm, das zeigt, wie Java JavaScript aufruft und asynchrone Fetch‑Ergebnisse empfängt – call java from javascript](/images/java-js-async.png)

*Das Bild zeigt den Ablauf: Java → JavaScriptEngine → async fetch → JavaCallback.*

## Häufig gestellte Fragen

**Kann ich diesen Ansatz mit anderen JavaScript‑Engines verwenden?**  
Ja, jede Engine, die einen Host‑Objekt‑Mechanismus bereitstellt (z. B. Nashorn, GraalVM), kann funktionieren, aber Aspose.HTML bietet Ihnen eine vollwertige, browserähnliche Umgebung mit integriertem `fetch`.

**Was, wenn ich ein komplexes Java‑Objekt statt eines Strings zurückgeben muss?**  
Sie können das Objekt auf der Java‑Seite in JSON serialisieren und JavaScript es parsen lassen, oder Sie können mehrere Methoden im Host‑Objekt bereitstellen, um einzelne Felder zu empfangen.

**Ist die `fetch`‑Implementierung vollständig standardkonform?**  
Aspose.HTML implementiert den WHATWG Fetch‑Standard, sodass Sie eine korrekte Handhabung von Weiterleitungen, CORS und Streaming erhalten.

**Blockiert dies den Java‑Thread, während auf das Netzwerk gewartet wird?**  
Nein. Der `execute`‑Aufruf gibt sofort zurück, und die interne Engine verarbeitet das Promise asynchron. Der Haupt‑Thread bleibt jedoch aktiv, bis das Skript beendet ist oder Sie die Engine explizit herunterfahren.

## Fazit

Wir haben gerade ein praktisches Szenario durchgangen, das Ihnen ermöglicht, **Java von JavaScript** aus **aufzurufen**, **asynchrones JavaScript** auszuführen und **JSON in Java** mit der **asynchronous fetch API** abzurufen. Durch das Erstellen eines Host‑Objekts, das Schreiben einer sauberen `async`‑Funktion und deren Ausführung mit der **JavaScript‑Engine** von Aspose.HTML erhalten Sie eine saubere, nicht blockierende Brücke zwischen den beiden Laufzeiten.

Probieren Sie es aus, ändern Sie die URL oder fügen Sie weitere Callbacks hinzu – Ihrer Fantasie sind keine Grenzen gesetzt. Als Nächstes könnten Sie erkunden:

- **Executing JavaScript engine** mit mehreren gleichzeitigen Skripten.  
- Verwendung von **run async javascript**, um große Datensätze parallel zu verarbeiten.  
- Integration dieses Musters in einen Web‑Service, der dynamisches HTML on the fly rendert.

Fühlen Sie sich frei zu experimentieren und zögern Sie nicht, einen Kommentar zu hinterlassen, falls Sie auf ein unerwartetes Problem stoßen. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}