---
category: general
date: 2026-03-14
description: Erfahren Sie, wie Sie Java aus JavaScript mit Aspose.HTML aufrufen. Dieser
  Leitfaden zeigt, wie man ein Host‑Objekt hinzufügt, JavaScript in Java ausführt
  und aus JavaScript protokolliert.
draft: false
keywords:
- call java from javascript
- add host object
- run javascript in java
- javascript host object
- log from javascript
language: de
og_description: Rufen Sie Java aus JavaScript mit Aspose.HTML auf. Fügen Sie ein Host‑Objekt
  hinzu, führen Sie JavaScript in Java aus und protokollieren Sie aus JavaScript –
  alles in einem einzigen Tutorial.
og_title: Java aus JavaScript aufrufen – Vollständige Anleitung mit Host‑Objekt
tags:
- Java
- JavaScript
- Aspose.HTML
- Scripting
title: Java aus JavaScript aufrufen – Host‑Objekt hinzufügen und JavaScript in Java
  ausführen
url: /de/java/advanced-usage/call-java-from-javascript-add-host-object-and-run-javascript/
---

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java aus JavaScript aufrufen – Host‑Objekt hinzufügen und JavaScript in Java ausführen

Haben Sie schon einmal **Java aus JavaScript** innerhalb einer Java‑Anwendung aufrufen müssen? Vielleicht bauen Sie eine dynamische HTML‑Report‑Engine oder möchten einfach einen Java‑Logger einem von Ihnen kontrollierten Skript zur Verfügung stellen. In diesem Tutorial sehen Sie genau, wie Sie ein Host‑Objekt hinzufügen, JavaScript in Java ausführen und sogar **aus JavaScript loggen** zurück zur JVM – alles mit Aspose.HTML.

Wir gehen ein vollständiges, ausführbares Beispiel durch, das ein leeres HTML‑Dokument erstellt, eine Java‑`Logger`‑Klasse als Host‑Objekt injiziert, ein winziges Skript ausführt und das Ergebnis in der Konsole ausgibt. Kein externer Web‑Browser nötig, keine mystische „Magie“ – nur reiner Java‑Code, den Sie heute kopieren‑und‑einfügen und ausführen können.

## Voraussetzungen

- Java 17 (oder ein aktuelles JDK) installiert und konfiguriert.
- Aspose.HTML for Java Bibliothek (Version 23.10 oder neuer). Sie können sie von Maven Central oder der Aspose‑Website beziehen.
- Eine einfache IDE oder ein Text‑Editor; das Beispiel funktioniert auch über die Kommandozeile.

> **Pro‑Tipp:** Wenn Sie Maven verwenden, fügen Sie die folgende Abhängigkeit zu Ihrer `pom.xml` hinzu:

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

## Schritt 1: Ein minimales Java‑Projekt erstellen

Erstellen Sie zunächst eine neue Java‑Klasse namens `JsHostObjectDemo`. Die Klasse enthält unsere `main`‑Methode und die Definition des Host‑Objekts. Alles in einer Datei zu halten, macht das Tutorial eigenständig und leicht kopierbar.

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

Die Klasse `HTMLDocument` von Aspose.HTML startet eine vollständige HTML‑5‑konforme Skript‑Umgebung. Auch wenn wir nie Markup laden, gibt uns das `window`‑Objekt des Dokuments Zugriff auf die JavaScript‑Engine, wo die **run JavaScript in Java**‑Magie stattfindet.

## Schritt 2: Das Host‑Objekt hinzufügen – „javaLogger“

Die Zeile

```java
document.getWindow().addHostObject("javaLogger", new Logger());
```

erledigt die schwere Arbeit für die Anforderung **add host object**. Durch die Registrierung der `Logger`‑Instanz unter dem Namen `"javaLogger"` kann jedes in diesem Dokument ausgewertete Skript `javaLogger.log(...)` aufrufen. Das ist das Kernkonzept des **javascript host object**: eine Brücke, die JavaScript den Zugriff auf die JVM ermöglicht.

### Häufige Stolperfallen

- **Namenskollisionen** – Wenn Sie bereits eine globale Variable namens `javaLogger` in Ihrem Skript haben, wird das Host‑Objekt überschrieben. Wählen Sie einen eindeutigen Namen.
- **Thread‑Sicherheit** – Das Host‑Objekt wird über Skriptausführungen hinweg im selben Dokument geteilt. Wenn Sie Skripte parallel ausführen wollen, machen Sie die Host‑Klasse thread‑sicher (z. B. mit `synchronized` oder `java.util.concurrent`‑Primitiven).

## Schritt 3: JavaScript schreiben und ausführen

Das Skript, das wir an `eval` übergeben, ist bewusst klein:

```javascript
javaLogger.log('Hello from JavaScript!');
```

Wenn `document.getWindow().eval(script)` ausgeführt wird, sucht die Engine im globalen Scope nach `javaLogger`, findet das von uns hinzugefügte Java‑Objekt und ruft dessen `log`‑Methode mit dem übergebenen String auf.

### Erwartete Ausgabe

Der Aufruf der `main`‑Methode gibt folgende Zeile in der Konsole aus:

```
[JS] Hello from JavaScript!
```

Diese winzige Zeile beweist, dass wir erfolgreich **call java from javascript** durchgeführt haben und dass das **log from javascript** genau dort erscheint, wo eine normale Java‑`System.out`‑Nachricht ausgegeben würde.

## Schritt 4: Das Host‑Objekt erweitern – mehr als nur Logging

Wenn Sie weitere Funktionalitäten bereitstellen müssen (z. B. Dateizugriff, Datenbankabfragen), fügen Sie einfach weitere Methoden zur `Logger`‑Klasse hinzu – oder erstellen Sie eine komplett neue Host‑Klasse. Hier ein kurzes Beispiel, das zusätzlich einen Rückgabewert liefert:

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

Damit wird die Flexibilität des **javascript host object**‑Musters demonstriert: Sie können jede Java‑API exponieren, solange die Datentypen zwischen Java und JavaScript konvertierbar sind (Primitive, Strings, Arrays usw.).

## Schritt 5: Ressourcen aufräumen

Wenn Sie mit der Skript‑Umgebung fertig sind, entsorgen Sie das `HTMLDocument`, um native Ressourcen freizugeben:

```java
document.dispose(); // Important for long‑running applications
```

Das Weglassen der Entsorgung kann zu Speicherlecks führen, besonders wenn Sie viele Dokumente in einer Schleife erzeugen.

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

Damit ist der gesamte **call java from javascript**‑Workflow in wenigen Zeilen abgebildet.

## Häufig gestellte Fragen

### Funktioniert das auf Android?

Aspose.HTML ist eine reine Java‑Bibliothek und läuft auf jeder JVM, einschließlich Androids Dalvik/ART. Binden Sie einfach das JAR ein und Sie erhalten dieselben Host‑Object‑Funktionen.

### Was, wenn ich komplexe Objekte übergeben muss?

Sie können POJOs (plain old Java objects) mit Feldern, Gettern und Settern exponieren. Die Engine mappt sie automatisch zu JavaScript‑Objekten. Für Sammlungen verwenden Sie `java.util.List` oder Arrays – beide sind konvertierbar.

### Wie funktioniert die Fehlerbehandlung?

Wirft das Skript einen JavaScript‑Fehler, propagiert `eval` eine `ScriptException`. Umhüllen Sie den Aufruf mit einem try‑catch‑Block, um zu loggen oder zu recovern:

```java
try {
    document.getWindow().eval(script);
} catch (ScriptException e) {
    System.err.println("Script error: " + e.getMessage());
}
```

### Kann ich mehrere Skripte nacheinander ausführen?

Absolut. Die gleiche `HTMLDocument`‑Instanz behält ihren globalen Scope, sodass Sie `eval` wiederholt aufrufen können. Achten Sie nur auf Namenskollisionen zwischen den Skripten.

## Best Practices & Tipps

- **Benennen Sie Ihre Host‑Objekte eindeutig** – `javaLogger`, `javaUtils` usw., um Verwirrungen zu vermeiden.
- **Halten Sie Host‑Methoden klein und ohne Seiteneffekte**, wenn möglich; das erleichtert das Debuggen.
- **Entsorgen Sie das Dokument**, sobald Sie fertig sind; dadurch wird der von Aspose.HTML reservierte native Speicher freigegeben.
- **Validieren Sie Eingaben** aus JavaScript, besonders wenn Skripte aus unzuverlässigen Quellen stammen. Behandeln Sie sie wie jede andere externe Datenquelle.

## Fazit

Sie haben nun ein solides End‑to‑End‑Beispiel, wie Sie **java from javascript** aufrufen, indem Sie ein **Host‑Objekt hinzufügen**, **JavaScript in Java ausführen** und **aus JavaScript loggen** – alles mit Aspose.HTML. Das Muster ist mächtig: Jeder Java‑Dienst kann Skripten zur Verfügung gestellt werden, wodurch Ihre Java‑Anwendung zu einer leichten Skript‑Plattform wird.

Als nächstes könnten Sie:

- Eine komplette HTML‑Seite injizieren und das DOM aus JavaScript manipulieren.
- Das Host‑Objekt nutzen, um Daten zurück nach Java zu streamen (z. B. JSON‑Serialisierung).
- Andere Skript‑Engines wie Nashorn oder GraalVM integrieren, um breitere Sprachunterstützung zu erhalten.

Probieren Sie es aus, passen Sie die `Logger`‑ oder `Utils`‑Klassen an und sehen Sie, wie weit Sie das **javascript host object**‑Konzept in Ihren eigenen Projekten treiben können.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}