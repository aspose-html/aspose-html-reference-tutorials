---
category: general
date: 2026-03-26
description: Top-Level‑Await‑Beispiel, das await‑Delay in JavaScript, eine Inkrement‑Zähler‑Klasse
  und öffentliche Klassenfelder in JavaScript in einer Live‑Demo zeigt.
draft: false
keywords:
- top level await example
- await delay javascript
- increment counter class
- public class fields javascript
- javascript class public field
language: de
og_description: Top-Level‑Await‑Beispiel, das await‑Delay in JavaScript, eine Inkrement‑Zähler‑Klasse
  und öffentliche Klassenfelder in JavaScript in einem kurzen Tutorial demonstriert.
og_title: Top-Level‑Await‑Beispiel – Verwendung von await delay in JavaScript
tags:
- JavaScript
- ES2022
- async‑await
- classes
title: Top-Level-Await-Beispiel – Verwendung von await delay in JavaScript
url: /de/java/advanced-usage/top-level-await-example-using-await-delay-in-javascript/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Top‑Level‑Await‑Beispiel – Verwendung von await delay in JavaScript

Haben Sie sich jemals gefragt, wie man die Ausführung eines Moduls pausieren kann, ohne alles in eine async IIFE zu verpacken? Genau das ermöglicht ein **top level await example**. In diesem Tutorial gehen wir eine kleine Webseite durch, die `await delay javascript` verwendet, um Arbeit zu verzögern, und dann eine `increment counter class` erstellt, die **public class fields javascript** nutzt. Am Ende haben Sie ein komplettes Copy‑and‑Paste‑Snippet, das in jedem modernen Browser läuft.

Wir behandeln alles, von der Definition einer Klasse mit einem öffentlichen Feld bis hin zur Verkabelung einer einfachen, versprechenbasierten Delay‑Hilfsfunktion. Keine externen Bibliotheken, kein Build‑Schritt – nur reines HTML, ein `<script type="module">` und die neuesten ECMAScript‑Features. Wenn Sie bereits mit async‑Funktionen vertraut sind, werden Sie sehen, warum Top‑Level‑Await wie eine natürliche Erweiterung wirkt. Wenn Sie neu in der **javascript class public field**‑Syntax sind, keine Sorge – wir erklären das Warum hinter jeder Zeile.

## Was Sie lernen werden

- Wie ein **top level await example** innerhalb eines Modul‑Scripts funktioniert.
- Das Muster für einen `await delay javascript`‑Helper, der `setTimeout` mit Promises nachahmt.
- Wie man eine **increment counter class** schreibt, die ein öffentliches Feld (`count`) und einen statischen Initialisierungsblock verwendet.
- Erwartete Konsolenausgabe und wie man überprüft, dass der statische Block vor dem Rest des Skripts ausgeführt wird.
- Tipps zur Fehlersuche bei gängigen Stolperfallen, z. B. älteren Browsern, die Top‑Level‑Await nicht unterstützen.

> **Pro‑Tipp:** Moderne Browser (Chrome 106+, Firefox 102+, Edge 106+) unterstützen Top‑Level‑Await bereits. Wenn Sie ältere Umgebungen unterstützen müssen, sollten Sie ein Bundling‑Tool wie Vite oder Babel in Betracht ziehen.

## Step 1 – Define a Class with a Public Field and a Static Block

Der erste Teil unserer Demo ist eine Klasse, die einen numerischen Zähler speichert. Beachten Sie die Zeile `count = 0;` – dies ist die **public class fields javascript**‑Syntax, die in ES2022 eingeführt wurde. Sie erzeugt eine Instanz‑Eigenschaft ohne Konstruktor.

```html
<!DOCTYPE html>
<html>
<head>
    <title>ECMAScript 2022 Demo</title>
</head>
<body>
<img src="placeholder.png" alt="top level await example screenshot" title="top level await example">

<script type="module">
    // Step 1: Class definition
    class Counter {
        // Public field holds the current count
        count = 0;

        // Static block runs once when the class is first evaluated
        static {
            console.log('Counter class initialized');
        }

        // Simple method that increments the public field
        increment() {
            this.count++;
        }
    }
```

**Warum ein statischer Block?** Er ermöglicht es uns, einmalige Initialisierungslogik (wie Logging) auszuführen, sobald das Modul geparst wird, *bevor* irgendein Top‑Level‑Await läuft. Das garantiert, dass die Meldung zuerst in der Konsole erscheint und beweist, dass die Klasse früh ausgewertet wurde.

## Step 2 – Create an `await delay javascript` Helper

Als Nächstes benötigen wir eine winzige, versprechenbasierte Delay‑Funktion. Sie ist im Wesentlichen ein Wrapper um `setTimeout`, aber die Rückgabe eines Promises macht sie await‑fähig.

```javascript
    // Step 2: Promise‑based delay helper
    const delay = ms => new Promise(resolve => setTimeout(resolve, ms));
```

**Randfall:** Wenn `ms` negativ oder keine Zahl ist, behandelt `setTimeout` es als `0`. Sie könnten Validierung hinzufügen, aber für eine Demo hält die Einzeiler‑Lösung den Code lesbar.

## Step 3 – Use Top‑Level Await to Pause Execution

Jetzt kommt der Star der Show: Top‑Level‑Await. Da unser Skript ein Modul ist (`type="module"`), können wir `await` direkt im obersten Geltungsbereich platzieren. Das pausiert das Modul, bis das Promise aufgelöst ist, und lässt uns die Reihenfolge der Nebeneffekte steuern.

```javascript
    // Step 3: Top‑level await – delay half a second
    await delay(500);   // Wait 500 ms so the static block logs first
```

**Häufige Frage:** „Kann ich Top‑Level‑Await in einem normalen `<script>`‑Tag verwenden?“ Nein – nur Modul‑Scripts unterstützen das. Wenn Sie `type="module"` vergessen, erhalten Sie einen Syntaxfehler.

## Step 4 – Instantiate the Class, Increment, and Log the Result

Zum Schluss setzen wir alles zusammen: Eine Instanz erzeugen, `increment()` aufrufen und den finalen Zähler ausgeben. Das demonstriert die **increment counter class** in Aktion.

```javascript
    // Step 4: Work with the Counter instance
    const counterInstance = new Counter();
    counterInstance.increment();               // count becomes 1
    console.log('Final count:', counterInstance.count);
</script>
</body>
</html>
```

### Erwartete Konsolenausgabe

```
Counter class initialized
Final count: 1
```

Wenn Sie die Seite in den DevTools öffnen, sollten Sie die Meldung des statischen Blocks **vor** dem Abschluss des Delays sehen, was bestätigt, dass die Klasse zuerst ausgewertet wurde.

## Step 5 – Why Use Public Class Fields Instead of a Constructor?

Vielleicht fragen Sie sich, warum wir nicht geschrieben haben:

```javascript
class Counter {
    constructor() {
        this.count = 0;
    }
}
```

Beide Ansätze funktionieren, aber **public class fields javascript** bieten eine sauberere, deklarativere Syntax. Das Feld wird einmal definiert, nicht in jedem Konstruktoraufruf, was bei wachsenden Klassen leichter zu lesen ist. Außerdem können statische Blöcke nicht innerhalb eines Konstruktors platziert werden, sodass die Trennung von Initialisierungslogik natürlicher wird.

## Step 6 – Adapting the Example for Real‑World Apps

In der Produktion benötigen Sie oft mehr als einen einzigen Zähler. Hier ein paar schnelle Ideen:

- **Mehrere Zähler:** In einer `Map` speichern, die nach Identifiern indiziert ist.
- **Persistenter Zustand:** `console.log` durch Schreibvorgänge in `localStorage` ersetzen.
- **Async‑Initialisierung:** Den statischen Block nutzen, um Konfigurationen vom Server zu holen, bevor Instanzen erstellt werden.

All diese Muster profitieren weiterhin von Top‑Level‑Await, weil Sie Daten einmal beim Laden des Moduls abrufen und sicherstellen können, dass sie für jeden Verbraucher bereitstehen.

## Frequently Asked Questions

**Q: Blockiert Top‑Level‑Await andere Module?**  
A: Nein. Jedes Modul läuft unabhängig. Nur das Modul, das das Await enthält, wird pausiert; andere Module laden parallel weiter.

**Q: Was passiert, wenn das Delay‑Promise abgelehnt wird?**  
A: Eine unbehandelte Ablehnung bricht die Modulauswertung ab und erscheint als Fehler in der Konsole. Wickeln Sie das Await in ein `try…catch`, wenn Sie eine sanfte Fallback‑Logik benötigen.

**Q: Ist das Schlüsselwort `static` erforderlich?**  
A: Nicht für den Zähler selbst, aber der statische Block ist eine praktische Möglichkeit zu zeigen, dass Code *einmal* zur Ladezeit läuft – ideal für Logging oder Feature‑Detection.

## Conclusion

Sie haben gerade ein **top level await example** gebaut, das `await delay javascript`, eine **increment counter class** und die Kraft von **public class fields javascript** demonstriert. Das komplette, ausführbare Snippet befindet sich oben, und die Konsolenausgabe beweist, dass der statische Block vor dem verzögerten Code ausgeführt wird.  

Ab hier können Sie mit komplexeren async‑Abläufen experimentieren, das Delay durch einen echten API‑Aufruf ersetzen oder die Klasse um weitere Methoden erweitern. Denken Sie daran: Modernes JavaScript lässt Sie Module als erstklassige async‑Entitäten behandeln – keine zusätzlichen Wrapper nötig.

Viel Spaß beim Coden, und teilen Sie gern Ihre Varianten in den Kommentaren. Wenn Ihnen dieser Leitfaden geholfen hat, teilen Sie ihn mit einem Teamkollegen, der noch mit async‑Mustern kämpft!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}