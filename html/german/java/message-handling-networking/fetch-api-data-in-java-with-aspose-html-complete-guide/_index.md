---
category: general
date: 2026-05-28
description: API-Daten in Java mit Aspose.HTML abrufen – lernen Sie, wie man asynchrones
  JavaScript ausführt, ein asynchrones Skript startet und ein DOM-Attribut aus dem
  abgerufenen JSON setzt.
draft: false
keywords:
- fetch api data
- execute async javascript
- run async script
- set dom attribute
- how to run async
language: de
og_description: API-Daten in Java mit Aspose.HTML abrufen. Dieses Tutorial zeigt,
  wie man asynchrones JavaScript ausführt, ein asynchrones Skript startet und ein
  DOM-Attribut aus API-Ergebnissen setzt.
og_title: API-Daten in Java abrufen – Schritt‑für‑Schritt Aspose.HTML‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  headline: fetch api data in Java with Aspose.HTML - Complete Guide
  type: TechArticle
- description: fetch api data in Java using Aspose.HTML – learn how to execute async
    javascript, run async script, and set dom attribute from fetched JSON.
  name: fetch api data in Java with Aspose.HTML - Complete Guide
  steps:
  - name: Expected Output
    text: '``` GitHub stars: 84327 ```'
  - name: What if the fetch call fails?
    text: 'The script will throw a JavaScript exception, which propagates to `ScriptEngine.evaluate`.
      You can catch it in Java:'
  - name: Can I fetch from a private API that requires authentication?
    text: 'Sure—just add the appropriate headers in the script:'
  - name: Does this work on older Java versions?
    text: Aspose.HTML ships with its own JavaScript engine, so you don’t need Nashorn
      or GraalVM. However, the `try‑with‑resources` syntax requires Java 7+. For Java
      6 you’d have to close the document manually.
  type: HowTo
tags:
- Java
- Aspose.HTML
- Async JavaScript
title: API-Daten in Java mit Aspose.HTML abrufen – Komplettanleitung
url: /de/java/message-handling-networking/fetch-api-data-in-java-with-aspose-html-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# API-Daten in Java mit Aspose.HTML – Komplettanleitung

Haben Sie sich jemals gefragt, wie man **API-Daten abruft** in Java, ohne den Komfort Ihrer IDE zu verlassen? Sie sind nicht allein. Viele Entwickler stoßen an ihre Grenzen, wenn sie einen entfernten Dienst von einer von Aspose.HTML gerenderten HTML‑Seite aus aufrufen und das Ergebnis zurück nach Java holen müssen.  

In diesem Tutorial führen wir Sie durch ein praktisches Beispiel, das **asynchrones JavaScript ausführt**, ein **asynchrones Skript** startet und schließlich **ein DOM‑Attribut** mit dem abgerufenen Wert setzt. Am Ende wissen Sie genau, *wie man asynchrone* Vorgänge sicher ausführt und die benötigten Daten abruft.

## Was Sie erstellen werden

Wir erstellen eine kleine Java‑Konsolenanwendung, die:

1. Eine HTML‑Datei lädt, die eine async‑Funktion enthält.  
2. Ein Skript ausführt, das die **fetch API** verwendet, um den öffentlichen Endpunkt von GitHub aufzurufen.  
3. Auf die Auflösung des Promises wartet (bis zu 10 Sekunden).  
4. Die Sternzahl in einem benutzerdefinierten `data-stars`‑Attribut im `<body>`‑Element speichert.  
5. Dieses Attribut in Java ausliest und ausgibt.

Keine externen HTTP‑Client‑Bibliotheken, kein zusätzlicher Thread‑Code – nur Aspose.HTML übernimmt die schwere Arbeit.

## Voraussetzungen

- **Java 17** oder neuer (der Code kompiliert auch mit früheren Versionen, aber 17 ist das aktuelle LTS).  
- **Aspose.HTML for Java** Bibliothek (Version 23.9 oder höher).  
- Eine einfache HTML‑Datei (`async-page.html`), die irgendwo auf Ihrer Festplatte liegt.  
- Eine Internetverbindung (der fetch‑Aufruf greift auf `https://api.github.com` zu).  

Falls Sie bereits ein Maven‑Projekt haben, fügen Sie die Aspose.HTML‑Abhängigkeit hinzu:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

Jetzt tauchen wir in den Code ein.

## Schritt 1: HTML‑Seite vorbereiten

Zuerst erstellen Sie eine minimale HTML‑Datei, die die async‑Funktion hostet. Sie benötigen kein ausgefallenes Markup – nur ein `<body>`‑Tag.

```html
<!-- async-page.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Async Demo</title>
</head>
<body>
    <!-- The script we’ll inject later will populate this attribute -->
</body>
</html>
```

Speichern Sie diese Datei an einem erreichbaren Ort, z. B. `C:/temp/async-page.html`. Der Pfad wird im Java‑Code verwendet.

![Beispiel für das Abrufen von API-Daten](https://example.com/fetch-api-data.png "Beispiel für das Abrufen von API-Daten")

*Bildbeschreibung: Beispiel für das Abrufen von API-Daten, das eine Konsolenausgabe der GitHub‑Sterne zeigt.*

## Schritt 2: HTML‑Dokument in Java laden

Mit der bereitstehenden HTML‑Datei öffnen wir sie mit `HTMLDocument` von Aspose.HTML. Der `try‑with‑resources`‑Block stellt sicher, dass das Dokument ordnungsgemäß freigegeben wird.

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {
            // The rest of the steps go here...
        }
    }
}
```

Warum `HTMLDocument` verwenden? Es liefert ein vollwertiges DOM, eine integrierte JavaScript‑Engine und eine bequeme Möglichkeit, aus Java mit der Seite zu interagieren – alles ohne einen Browser zu starten.

## Schritt 3: Das asynchrone Skript schreiben

Jetzt erstellen wir ein JavaScript‑Snippet, das **API‑Daten abruft**, auf das Promise wartet und anschließend **ein DOM‑Attribut setzt**. Beachten Sie die Verwendung von `async/await` – das gleiche Muster, das Sie im Browser schreiben würden.

```java
String script =
    "async function run() {" +
    "  const data = await fetch('https://api.github.com').then(r => r.json());" +
    "  document.body.setAttribute('data-stars', data.stargazers_count);" +
    "}" +
    "run();";
```

Ein paar Dinge, die zu beachten sind:

- Die Funktion `run` ist als `async` deklariert, sodass wir den `fetch`‑Aufruf mit `await` ausführen können.  
- Nachdem das JSON geparst wurde, speichern wir `data.stargazers_count` in ein benutzerdefiniertes Attribut `data-stars`.  
- Abschließend rufen wir `run()` sofort auf.  

Dieses kleine Skript erledigt alles, was wir benötigen, um **asynchrones Skript auszuführen** und das Ergebnis zu erfassen.

## Schritt 4: Skript ausführen und warten

Der `ScriptEngine` von Aspose.HTML kann JavaScript mit einem Timeout auswerten. Durch Übergabe von `10000` teilen wir der Engine mit, bis zu **10 Sekunden** auf den Abschluss der asynchronen Operation zu warten.

```java
// Execute the script and wait (up to 10 seconds) for the async operation to finish
ScriptEngine engine = doc.getScriptEngine();
engine.evaluate(script, 10000);   // timeout in milliseconds
```

Falls die Anfrage länger als das Timeout dauert, wird eine `ScriptException` ausgelöst – ideal, um instabile Netzwerkbedingungen zu handhaben. In der Produktion würden Sie dies wahrscheinlich in ein try‑catch‑Block einbetten und bei Bedarf erneut versuchen.

## Schritt 5: Attribut aus Java abrufen

Nachdem das Skript abgeschlossen ist, ist das `data-stars`‑Attribut nun Teil des DOM. Rufen Sie es mit einem einfachen Aufruf zurück nach Java:

```java
// Retrieve the value set by the script from the document
String stars = doc.getBody().getAttribute("data-stars");
System.out.println("GitHub stars: " + stars);
```

Diese Zeile gibt etwas aus wie `GitHub stars: 12345`. Die genaue Zahl ändert sich täglich, aber das Muster bleibt gleich.

## Vollständiges funktionierendes Beispiel

Wenn wir alle Teile zusammenfügen, erhalten Sie das komplette, sofort ausführbare Programm:

```java
import com.aspose.html.*;
import com.aspose.html.scripting.*;

public class AsyncJsExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML page that contains an async function
        try (HTMLDocument doc = new HTMLDocument("C:/temp/async-page.html")) {

            // Step 2: Define a script that calls the async function and stores the result in a DOM attribute
            String script =
                "async function run() {" +
                "  const data = await fetch('https://api.github.com').then(r => r.json());" +
                "  document.body.setAttribute('data-stars', data.stargazers_count);" +
                "}" +
                "run();";

            // Step 3: Execute the script and wait (up to 10 seconds) for the async operation to finish
            ScriptEngine engine = doc.getScriptEngine();
            engine.evaluate(script, 10000);

            // Step 4: Retrieve the value set by the script from the document
            String stars = doc.getBody().getAttribute("data-stars");
            System.out.println("GitHub stars: " + stars);
        }
    }
}
```

### Erwartete Ausgabe

```
GitHub stars: 84327
```

(Ihre Zahl wird abweichen; wichtig ist, dass der Wert ein **String** ist, der die Sternzahl darstellt.)

## Häufige Fragen & Sonderfälle

### Was passiert, wenn der fetch‑Aufruf fehlschlägt?

Das Skript wirft eine JavaScript‑Exception, die zu `ScriptEngine.evaluate` propagiert. Sie können sie in Java abfangen:

```java
try {
    engine.evaluate(script, 10000);
} catch (ScriptException e) {
    System.err.println("Failed to fetch data: " + e.getMessage());
}
```

### Kann ich von einer privaten API mit Authentifizierung abrufen?

Natürlich – fügen Sie einfach die entsprechenden Header im Skript hinzu:

```javascript
await fetch('https://api.example.com/secure', {
    headers: { 'Authorization': 'Bearer YOUR_TOKEN' }
}).then(r => r.json());
```

Denken Sie daran, Geheimnisse nicht im Quellcode-Repository zu speichern.

### Funktioniert das mit älteren Java‑Versionen?

Aspose.HTML liefert eine eigene JavaScript‑Engine, sodass Sie Nashorn oder GraalVM nicht benötigen. Allerdings erfordert die `try‑with‑resources`‑Syntax Java 7+. Für Java 6 müssten Sie das Dokument manuell schließen.

## Pro‑Tipps

- **ScriptEngine wiederverwenden**: Wenn Sie viele asynchrone Skripte ausführen müssen, behalten Sie eine einzelne Engine‑Instanz bei – das erzeugt weniger Overhead.  
- **Timeout erhöhen** für langsamere APIs, aber nicht auf `Integer.MAX_VALUE` setzen; Sie benötigen weiterhin ein Sicherheitsnetz.  
- **Attribut validieren** bevor Sie es verwenden. Das DOM‑Attribut könnte `null` sein, wenn das Skript nie ausgeführt wurde.  
- **Roh‑JSON protokollieren** während der Entwicklung; das hilft, wenn sich die API‑Struktur ändert.

## Nächste Schritte

Jetzt, da Sie wissen, wie man **API‑Daten abruft**, können Sie das Muster erweitern:

- **Komplexeres JSON parsen** und mehrere Attribute einfügen.  
- **Tabellen erstellen** innerhalb der HTML‑Seite basierend auf abgerufenen Daten.  
- **Mit Aspose.PDF kombinieren**, um ein PDF zu erzeugen, das Live‑API‑Ergebnisse enthält.  

Jeder dieser Schritte baut auf denselben Kernideen auf: **asynchrones JavaScript ausführen**, **asynchrones Skript starten** und **DOM‑Attribut setzen** aus dem Ergebnis. Experimentieren Sie gern – in Aspose.HTMLs Skript‑Engine steckt viel verborgene Power.

---

*Viel Spaß beim Coden! Wenn Sie auf Probleme stoßen, hinterlassen Sie unten einen Kommentar und wir helfen Ihnen gemeinsam weiter.*

## Verwandte Tutorials

- [Wie man JavaScript in Java ausführt – Komplettanleitung](/html/english/java/advanced-usage/how-to-run-javascript-in-java-complete-guide/)
- [Element an Body anhängen mit Aspose.HTML für Java mittels DOM‑Mutation‑Observer](/html/english/java/advanced-usage/dom-mutation-observer-observing-node-additions/)
- [Wie man Timeout setzt – Netzwerk‑Timeout in Aspose.HTML für Java verwalten](/html/english/java/message-handling-networking/network-timeout/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}