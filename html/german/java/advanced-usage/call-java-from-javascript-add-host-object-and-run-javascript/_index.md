---
category: general
date: 2026-10-14
description: Java aus JavaScript mit Aspose.HTML aufrufen. Erfahren Sie, wie Sie ein
  Host-Objekt hinzufügen, JavaScript in Java ausführen und aus JavaScript protokollieren,
  in einem kurzen Tutorial.
keywords:
- call java from javascript
- execute javascript in java
- run javascript in java
- java host object
- aspose.html scripting
lastmod: 2026-10-14
og_description: Java aus JavaScript mit Aspose.HTML aufrufen. Dieser Leitfaden zeigt,
  wie Sie ein Host-Objekt hinzufügen, JavaScript in Java ausführen und aus JavaScript
  protokollieren, alles in wenigen Codezeilen.
og_image_alt: Screenshot of Java console output showing javascript logging via Aspose.HTML
  host object
og_title: Java aus JavaScript aufrufen – Host-Objekt hinzufügen und JavaScript in
  Java ausführen
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Call java from javascript using Aspose.HTML. Learn how to add a host
    object, execute javascript in java, and log from javascript in a concise tutorial.
  headline: Call java from javascript – add host object and run javascript in java
  type: TechArticle
- questions:
  - answer: Yes. Aspose.HTML is a pure‑Java library, so it runs on any JVM, including
      Android’s ART runtime.
    question: Does this work on Android?
  - answer: You can expose POJOs with getters and setters; the engine maps them to
      JavaScript objects automatically. Collections such as `java.util.List` or arrays
      are also convertible.
    question: What if I need to pass complex objects?
  - answer: If the script throws a JavaScript error, `eval` propagates a `ScriptException`.
      Wrap the call in a try‑catch block to log or recover.
    question: How does error handling work?
  - answer: Absolutely. The same `HTMLDocument` retains its global scope, so you can
      call `eval` repeatedly. Just manage variable names to avoid clashes.
    question: Can I run multiple scripts sequentially?
  - answer: Treat any external script as untrusted input. Validate parameters and
      consider sandboxing by exposing only the minimal required methods.
    question: Is the host object safe for untrusted scripts?
  type: FAQPage
tags:
- java
- javascript
- aspose.html
- scripting
- host object
title: Java aus JavaScript aufrufen – Host-Objekt hinzufügen und JavaScript in Java
  ausführen
url: /de/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java aus JavaScript aufrufen – Host-Objekt hinzufügen und JavaScript in Java ausführen

Haben Sie jemals **call java from javascript** in einer Java-Anwendung aufrufen müssen? Vielleicht bauen Sie eine dynamische HTML-Berichts‑Engine oder möchten einfach einen Java‑Logger einem von Ihnen kontrollierten Skript zur Verfügung stellen. In diesem Tutorial sehen Sie genau, wie Sie ein Host‑Objekt hinzufügen, JavaScript in Java ausführen und sogar **log from JavaScript** zurück an die JVM protokollieren – alles mit Aspose.HTML.

Wir gehen ein komplettes, ausführbares Beispiel durch, das ein leeres HTML‑Dokument erstellt, eine Java‑`Logger`‑Klasse als Host‑Objekt injiziert, ein winziges Skript ausführt und das Ergebnis in der Konsole ausgibt. Kein externer Webbrowser nötig, keine mystische „Magie“ – nur reiner Java‑Code, den Sie heute kopieren‑und‑einfügen und ausführen können.

## Schnelle Antworten
- **Wie füge ich ein Host‑Objekt hinzu?** Register a Java instance with `document.getWindow().addHostObject("name", object)`.  
- **Kann ich JavaScript in Java ausführen?** Yes—use `document.getWindow().eval(yourScript)`.  
- **Ist das Protokollieren von JavaScript aus möglich?** Absolutely; the host object can expose any `void log(String)` method.  
- **Welche Version von Aspose.HTML wird benötigt?** Version 23.10 or newer supports the full host‑object API.  
- **Brauche ich einen Webbrowser?** No—Aspose.HTML provides an embedded engine, so everything runs head‑less.

## Was ist call java from javascript?
**Call java from javascript** ist die Technik, Java‑Objekte einem JavaScript‑Laufzeitumfeld zur Verfügung zu stellen, sodass Skripte Java‑Methoden direkt aufrufen können. Aspose.HTML erstellt eine leichte JavaScript‑Engine innerhalb eines Java‑Prozesses und ermöglicht nahtlose bidirektionale Kommunikation ohne externe Browser.

## Warum Aspose.HTML für die Ausführung von JavaScript in Java verwenden?
Aspose.HTML unterstützt **50+ Eingabe‑ und Ausgabeformate** und kann JavaScript in einer vollständig konformen HTML5‑Umgebung auswerten. Es verarbeitet Skripte im Durchschnitt bis zu 200 ms für einfachen Einzeiler‑Code und tut dies, ohne einen kompletten Browser‑Stack zu laden, was den Speicherverbrauch im Vergleich zu Selenium‑basierten Ansätzen um bis zu 80 % reduziert.

## Voraussetzungen

- Java 17 (oder ein aktuelles JDK) installiert und konfiguriert.  
- Aspose.HTML for Java‑Bibliothek (Version 23.10 oder neuer). Sie können sie von Maven Central oder der Aspose‑Website beziehen.  
- Eine einfache IDE oder ein Texteditor; das Beispiel funktioniert auch über die Befehlszeile.

> **Pro Tipp:** Wenn Sie Maven verwenden, fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml` hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Oder für Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

Jetzt, wo die Grundlagen geklärt sind, tauchen wir in die Schritt‑für‑Schritt‑Lösung ein.

## Wie fügt man ein Host‑Objekt hinzu und führt JavaScript in Java aus?
`addHostObject` registriert ein Java‑Objekt als globale Variable im JavaScript‑Kontext. Laden Sie Ihr `HTMLDocument`, registrieren Sie einen Java‑Logger unter dem Namen `"javaLogger"` mittels `addHostObject` und werten Sie dann ein kurzes Skript aus, das `javaLogger.log` aufruft. Der gesamte Ablauf erfordert nur drei API‑Aufrufe und funktioniert in jeder Java 17‑Runtime.

### Schritt 1: ein minimales Java‑Projekt erstellen

Zuerst richten Sie eine neue Java‑Klasse namens `JsHostObjectDemo` ein. Die Klasse enthält unsere `main`‑Methode und die Definition des Host‑Objekts. Alles in einer Datei zu halten macht das Tutorial eigenständig und leicht kopierbar.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Demonstrates how to call Java from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    // -----------------------------------------------------------------
    // Step 1.1 – Define a simple Java class that will be callable from JS
    // -----------------------------------------------------------------
    public static class Logger {
        /**
         * This method will be invoked from JavaScript.
         *
         * @param message Text to print.
         */
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // Step 1.2 – Create an empty HTMLDocument – it gives us a scripting engine
        // -----------------------------------------------------------------
        HTMLDocument document = new HTMLDocument();

        // -----------------------------------------------------------------
        // Step 1.3 – Add the Java Logger instance as a host object named "javaLogger"
        // -----------------------------------------------------------------
        document.getWindow().addHostObject("javaLogger", new Logger());

        // -----------------------------------------------------------------
        // Step 1.4 – Prepare JavaScript code that uses the host object
        // -----------------------------------------------------------------
        String script = "javaLogger.log('Hello from JavaScript!');";

        // -----------------------------------------------------------------
        // Step 1.5 – Execute the script; the Java Logger handles the call
        // -----------------------------------------------------------------
        document.getWindow().eval(script);
    }
}
```

### Warum ein `HTMLDocument`?
`HTMLDocument` repräsentiert ein HTML‑Dokument im Speicher und stellt eine JavaScript‑Engine bereit. Die `HTMLDocument`‑Klasse startet eine vollständig HTML‑5‑konforme Skriptumgebung. Auch wenn wir nie Markup laden, gibt uns das `window`‑Objekt des Dokuments Zugriff auf die JavaScript‑Engine, wo die **run javascript in java**‑Magie passiert. Zusätzlich können Sie den DOM manipulieren, Ressourcen laden oder Skripte auswerten, ohne einen Browser zu benötigen.

## Wie fügt man das Host‑Objekt hinzu – “javaLogger”?
`Logger` ist eine einfache Java‑Klasse mit einer `log(String)`‑Methode, die Nachrichten in die Konsole schreibt. Registrieren Sie die `Logger`‑Instanz unter dem Namen `"javaLogger"`, sodass jedes im Dokument ausgewertete Skript `javaLogger.log(...)` aufrufen kann. Das ist der Kern der **add host object**‑Anforderung und macht den Logger als globale Variable für JavaScript‑Code verfügbar.

### Häufige Fallstricke

- **Namenskollisionen** – Wenn Sie bereits eine globale Variable namens `javaLogger` in Ihrem Skript haben, wird das Host‑Objekt überschrieben. Wählen Sie einen eindeutigen Namen.  
- **Thread‑Sicherheit** – Das Host‑Objekt wird über Skriptausführungen im selben Dokument hinweg geteilt. Wenn Sie Skripte parallel ausführen wollen, machen Sie die Host‑Klasse thread‑sicher (z. B. mit `synchronized` oder `java.util.concurrent`‑Primitiven).

## Wie schreibt und führt man JavaScript in Java aus?
`eval` führt einen JavaScript‑String in der Skript‑Engine des Dokuments aus und gibt jedes Ergebnis zurück. Geben Sie ein winziges Skript an `eval`. Die Engine löst `javaLogger` aus dem globalen Scope auf und ruft dessen `log`‑Methode mit dem übergebenen String auf. Sie können auch Rückgabewerte erhalten, Ausnahmen behandeln und mehrere Auswertungen für komplexere Interaktionen verketten.

### Erwartete Ausgabe

Das Ausführen der `main`‑Methode gibt folgende Zeile in der Konsole aus:

```
[JS] Hello from JavaScript!
```

## Wie erweitert man das Host‑Objekt – mehr als nur Logging?
Ein Host‑Objekt ist jede Java‑Instanz, die über `addHostObject` JavaScript zur Verfügung gestellt wird. Ergänzen Sie zusätzliche Funktionalität, indem Sie Methoden zur `Logger`‑Klasse hinzufügen oder eine neue Host‑Klasse erstellen. Das folgende kurze Beispiel gibt zudem einen Wert an JavaScript zurück. Das Host‑Objekt kann komplexe Typen, I/O‑Operationen oder Interaktionen mit anderen Diensten bereitstellen. Durch Rückgabe eines Wertes kann das Skript Daten zurück erhalten, was bidirektionale Kommunikation zwischen Java und JavaScript ermöglicht.

```java
public static class Utils {
    public int add(int a, int b) {
        return a + b;
    }
}

// Register it
document.getWindow().addHostObject("javaUtils", new Utils());

// JavaScript side
String script2 = "var result = javaUtils.add(3, 4); javaLogger.log('3+4=' + result);";
document.getWindow().eval(script2);
```

Jetzt zeigt die Konsole:

```
[JS] 3+4=7
```

## Wie räumt man Ressourcen nach dem Ausführen von Skripten auf?
`dispose` gibt native Ressourcen frei, die von der `HTMLDocument`‑Instanz gehalten werden. Wenn Sie mit der Skript‑Umgebung fertig sind, rufen Sie `document.dispose()` auf, um native Ressourcen freizugeben. Das Nicht‑Aufrufen von `dispose()` kann zu Speicherlecks führen, besonders wenn viele Dokumente in Schleifen oder langlaufenden Diensten erstellt werden. Verpacken Sie die Nutzung stets in einen try‑with‑resources‑Block oder stellen Sie sicher, dass `document.dispose()` in einem finally‑Block aufgerufen wird.

```java
document.dispose(); // Important for long‑running applications
```

## Vollständiges funktionierendes Beispiel

Unten finden Sie die komplette Quelldatei, die Sie sofort kompilieren und ausführen können. Speichern Sie sie als `JsHostObjectDemo.java`, stellen Sie sicher, dass das Aspose.HTML‑JAR im Klassenpfad liegt, und führen Sie `java JsHostObjectDemo` aus.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.scripting.HostObject;

/**
 * Complete demo showing how to call Java from JavaScript, add host object,
 * run JavaScript in Java, and log from JavaScript using Aspose.HTML.
 */
public class JsHostObjectDemo {

    /** Simple logger that will be called from JavaScript. */
    public static class Logger {
        public void log(String message) {
            System.out.println("[JS] " + message);
        }
    }

    /** Utility class exposing arithmetic to JavaScript. */
    public static class Utils {
        public int add(int a, int b) {
            return a + b;
        }
    }

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create the HTMLDocument – this spins up the JavaScript engine.
        HTMLDocument document = new HTMLDocument();

        // 2️⃣ Register host objects.
        document.getWindow().addHostObject("javaLogger", new Logger());
        document.getWindow().addHostObject("javaUtils", new Utils());

        // 3️⃣ JavaScript that logs a message and performs a calculation.
        String script = ""
                + "javaLogger.log('Hello from JavaScript!');"
                + "var sum = javaUtils.add(5, 12);"
                + "javaLogger.log('5 + 12 = ' + sum);";

        // 4️⃣ Execute the script.
        document.getWindow().eval(script);

        // 5️⃣ Clean up.
        document.dispose();
    }
}
```

Die Ausführung dieses Programms liefert:

```
[JS] Hello from JavaScript!
[JS] 5 + 12 = 17
```

## Häufig gestellte Fragen

**Q: Funktioniert das auf Android?**  
A: Ja. Aspose.HTML ist eine reine Java‑Bibliothek und läuft auf jeder JVM, einschließlich der ART‑Runtime von Android.

**Q: Was, wenn ich komplexe Objekte übergeben muss?**  
A: Sie können POJOs mit Getter‑ und Setter‑Methoden bereitstellen; die Engine mappt sie automatisch zu JavaScript‑Objekten. Sammlungen wie `java.util.List` oder Arrays sind ebenfalls konvertierbar.

**Q: Wie funktioniert die Fehlerbehandlung?**  
A: Wirft das Skript einen JavaScript‑Fehler, propagiert `eval` eine `ScriptException`. Umhüllen Sie den Aufruf mit einem try‑catch‑Block, um zu protokollieren oder zu erholen.

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

**Q: Kann ich mehrere Skripte nacheinander ausführen?**  
A: Absolut. Das gleiche `HTMLDocument` behält seinen globalen Scope, sodass Sie `eval` wiederholt aufrufen können. Achten Sie nur auf eindeutige Variablennamen, um Kollisionen zu vermeiden.

**Q: Ist das Host‑Objekt sicher für nicht vertrauenswürdige Skripte?**  
A: Behandeln Sie jedes externe Skript als potenziell unsicher. Validieren Sie Parameter und erwägen Sie ein Sandbox‑Modell, indem Sie nur die minimal erforderlichen Methoden exponieren.

## Best Practices & Tipps

- **Benennen Sie Ihre Host‑Objekte eindeutig** – `javaLogger`, `javaUtils` usw., um Verwechslungen zu vermeiden.  
- **Halten Sie Host‑Methoden klein und ohne Seiteneffekte**, wenn möglich; das erleichtert das Debuggen.  
- **Entsorgen Sie das Dokument**, sobald Sie fertig sind; das gibt den nativen Speicher frei, den Aspose.HTML allokiert.  
- **Validieren Sie Eingaben** aus JavaScript, besonders wenn Skripte aus untrusted Quellen stammen. Behandeln Sie sie wie jede andere externe Daten.

## Fazit

Sie haben nun ein solides End‑zu‑End‑Beispiel, wie man **java from javascript** durch **Hinzufügen eines Host‑Objekts**, **Ausführen von JavaScript in Java** und **Logging von JavaScript** mit Aspose.HTML realisiert. Das Muster ist leistungsfähig: Jeder Java‑Dienst kann Skripten zur Verfügung gestellt werden und verwandelt Ihre Java‑Anwendung in eine leichte Scripting‑Plattform.

Als Nächstes könnten Sie:

- Eine vollständige HTML‑Seite injizieren und den DOM von JavaScript aus manipulieren.  
- Das Host‑Objekt nutzen, um Daten zurück an Java zu streamen (z. B. JSON‑Serialisierung).  
- Die Integration mit anderen Scripting‑Engines wie Nashorn oder GraalVM für breitere Sprachunterstützung erkunden.

Probieren Sie es aus, passen Sie die `Logger`‑ oder `Utils`‑Klassen an und sehen Sie, wie weit Sie das **javascript host object**‑Konzept in Ihren eigenen Projekten treiben können.

---

**Last Updated:** 2026-10-14  
**Tested With:** Aspose.HTML for Java 23.10  
**Author:** Aspose  






```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

```javascript
javaLogger.log('Hello from JavaScript!');
```

## Verwandte Tutorials

- [Skript‑Ausführung in Java aktivieren – Vollständiger Aspose HTML Leitfaden](/html/java/advanced-usage/enable-script-execution-in-java-complete-aspose-html-guide/)
- [JavaScript in Java ausführen – Vollständiger Leitfaden zum Ausführen von JS](/html/java/advanced-usage/execute-javascript-in-java-complete-guide-to-running-js-from/)
- [Wie man JavaScript sandboxed – Vollständiger Aspose HTML Leitfaden](/html/java/advanced-usage/how-to-sandbox-javascript-complete-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}