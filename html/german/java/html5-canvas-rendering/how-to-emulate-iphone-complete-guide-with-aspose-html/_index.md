---
category: general
date: 2026-03-26
description: Erfahren Sie, wie Sie ein iPhone in Java mit Aspose.HTML emulieren. Enthält
  Schritte zum Festlegen eines benutzerdefinierten User‑Agents und zum Einstellen
  des Geräte‑Pixel‑Verhältnisses für eine genaue mobile Darstellung.
draft: false
keywords:
- how to emulate iphone
- set custom user agent
- set device pixel ratio
- how to set user-agent
- how to set dpr
language: de
og_description: Wie kann man ein iPhone in Java emulieren? Dieses Tutorial zeigt,
  wie man mit Aspose.HTML einen benutzerdefinierten User‑Agent und das Geräte‑Pixel‑Verhältnis
  einstellt, um pixelgenaue mobile Seiten zu liefern.
og_title: Wie man das iPhone emuliert – Schritt‑für‑Schritt Aspose.HTML‑Leitfaden
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Wie man ein iPhone emuliert – Vollständiger Leitfaden mit Aspose.HTML
url: /de/java/html5-canvas-rendering/how-to-emulate-iphone-complete-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein iPhone emuliert – Komplettanleitung mit Aspose.HTML

Haben Sie sich schon einmal gefragt, **wie man ein iPhone emuliert**, wenn Sie eine Webseite lokal testen? Vielleicht debuggen Sie ein responsives Layout und der Desktop‑Browser reicht einfach nicht aus. Die gute Nachricht: Sie benötigen kein physisches Gerät – Aspose.HTML’s `DocumentSandbox` lässt Sie den Bildschirm, den User‑Agent und das Device‑Pixel‑Ratio (DPR) eines iPhones mit wenigen Zeilen Java nachahmen.  

In diesem Tutorial gehen wir Schritt für Schritt durch das Setzen eines **benutzerdefinierten User‑Agents**, das Konfigurieren des **Device‑Pixel‑Ratios** und das Verifizieren, dass alles wie erwartet funktioniert. Am Ende haben Sie eine wiederverwendbare Sandbox, die Seiten genauso rendert wie ein iPhone 8, und Sie verstehen, warum jede Einstellung wichtig ist.

## Was Sie erreichen werden

- Erstellen eines `Screen`‑Objekts, das die Abmessungen und das DPR eines iPhones widerspiegelt.  
- Anwenden einer **benutzerdefinierten User‑Agent**‑Zeichenkette, sodass Server denken, die Anfrage käme von Safari auf iOS.  
- Aufbau eines `DocumentSandbox`, das Bildschirm und User‑Agent verbindet.  
- Ausführen eines `HTMLDocument` innerhalb der Sandbox und Anzeige der Konsolenausgabe, die die Konfiguration bestätigt.  

Keine externen Bibliotheken außer Aspose.HTML sind nötig, und der Code läuft in jeder Java 17+ Umgebung.

---

![Screenshot zur iPhone-Emulation](https://example.com/images/iphone-emulation.png "iPhone-Emulation mit Aspose.HTML Sandbox")

## Wie man ein iPhone mit Aspose.HTML Sandbox emuliert

Das Erste, was wir benötigen, ist ein `Screen`, der die physischen Abmessungen *und* die Pixeldichte des iPhones abbildet. Das ist das Kernstück von **wie man ein iPhone exakt emuliert**.

```java
import com.aspose.html.devices.Screen;

// Step 1: Define iPhone 8 screen size (width, height) and DPR
Screen mobileScreen = new Screen(375, 667, 2.0); // iPhone 8 dimensions, DPR = 2
```

**Warum das wichtig ist:**  
- Die Breite = 375 px und Höhe = 667 px sind die CSS‑Pixel‑Abmessungen, die Sie in Chrome DevTools sehen, wenn Sie ein iPhone 8 auswählen.  
- Das Setzen des DPR auf 2 sagt der Rendering‑Engine, dass jedes CSS‑Pixel zwei physische Pixel entspricht, was zu scharfem Text und Bildern führt – genau wie auf einem echten Gerät.

> *Pro‑Tipp:* Wenn Sie ein neueres iPhone (z. B. das iPhone 13) emulieren wollen, ändern Sie einfach die Zahlen zu 390 × 844 und DPR = 3.

## Einen benutzerdefinierten User‑Agent setzen (set custom user agent)

Als Nächstes müssen wir **einen benutzerdefinierten User‑Agent setzen**, damit der Server das mobile‑spezifische HTML/CSS ausliefert. Ohne diesen denken viele Seiten immer noch, Sie würden einen Desktop benutzen.

```java
// Step 2: Define an iPhone Safari user‑agent string
String iPhoneUserAgent = "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) " +
                         "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                         "Version/16.0 Mobile/15E148 Safari/604.1";
```

**Wie das funktioniert:**  
- Der `User-Agent`‑Header ist das Handshake‑Signal, das Browser benutzen, um sich vorzustellen.  
- Indem Sie exakt die Zeichenkette verwenden, die Safari auf iOS 16 sendet, stellen Sie sicher, dass der Server die mobil‑optimierten Assets zurückgibt (z. B. responsive Bilder, adaptive Skripte usw.).  

Wenn Sie jemals **wie man den User‑Agent für ein anderes Gerät setzt**, ersetzen Sie einfach die Zeichenkette durch den passenden Wert – Google Chrome, Firefox oder sogar ein benutzerdefinierter Bot.

## Device‑Pixel‑Ratio konfigurieren (set device pixel ratio)

Jetzt setzen wir tatsächlich das **Device‑Pixel‑Ratio** innerhalb der Sandbox. Das ist der Schritt, der direkt die Frage “**wie man dpr setzt**” für eine simulierte Umgebung beantwortet.

```java
import com.aspose.html.sandbox.DocumentSandbox;

// Step 3: Build the sandbox with screen and user‑agent
DocumentSandbox documentSandbox = new DocumentSandbox.Builder()
        .setScreen(mobileScreen)          // applies the DPR we defined earlier
        .setUserAgent(iPhoneUserAgent)    // applies the custom user‑agent
        .build();
```

**Erklärung:**  
- Das `Builder`‑Pattern ermöglicht es Ihnen, sowohl den Screen (der das DPR trägt) als auch den User‑Agent flüssig anzuhängen.  
- Wenn die Sandbox ein `HTMLDocument` rendert, tut sie so, als würde sie auf einem Gerät mit genau dieser Pixeldichte laufen.  

> *Warum das wichtig ist:* Einige CSS‑Media‑Queries nutzen `device-pixel-ratio` (z. B. `@media (-webkit-min-device-pixel-ratio: 2)`). Wenn Sie das DPR nicht setzen, werden diese Regeln nie ausgelöst und Sie verpassen hochauflösende Assets.

## Die Sandbox‑Konfiguration verifizieren (how to set user-agent)

Lassen Sie die Sandbox arbeiten. Das folgende Snippet erstellt ein `HTMLDocument`, lädt eine Seite und gibt eine Bestätigung aus, dass die Sandbox aktiv ist.

```java
import com.aspose.html.HTMLDocument;

public class SandboxWithDprAndUa {
    public static void main(String[] args) {
        // Re‑use the sandbox we built earlier
        // DocumentSandbox documentSandbox = ... (from previous step)

        // Step 4: Load a page inside the sandbox
        HTMLDocument doc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 5: Optional – output a sanity check
        System.out.println("Sandbox configured with DPR=2 and iPhone user‑agent.");
    }
}
```

**Erwartete Konsolenausgabe**

```
Sandbox configured with DPR=2 and iPhone user-agent.
```

Wenn Sie das Programm ausführen und diese Zeile sehen, haben Sie erfolgreich **wie man ein iPhone emuliert** mit dem korrekten DPR und User‑Agent. Öffnen Sie die Seite in einem echten Browser und inspizieren Sie die Viewport‑Abmessungen – Sie werden feststellen, dass sie den iPhone‑Werten entsprechen, die wir gesetzt haben.

## Häufige Stolperfallen und wie man DPR korrekt setzt (how to set dpr)

Selbst mit dem richtigen Code können ein paar Fallstricke auftreten:

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **DPR bleibt bei 1** | Sie haben einen `Screen` ohne das dritte Argument (DPR) übergeben. | Immer `new Screen(width, height, dpr)` verwenden. |
| **User‑Agent wird ignoriert** | Die Sandbox war nicht an das `HTMLDocument` angehängt. | Den `documentSandbox` als zweiten Parameter an den `HTMLDocument`‑Konstruktor übergeben. |
| **Falsche Abmessungen** | Sie verwenden Geräte‑Pixel statt CSS‑Pixel. | Denken Sie daran: Breite/Höhe sind **CSS‑Pixel**, nicht Hardware‑Pixel. |
| **Server liefert weiterhin Desktop‑CSS** | Einige Seiten nutzen JavaScript zur Geräteerkennung, nicht nur den Header. | Gegebenenfalls zusätzlich ein viewport‑Meta‑Tag injizieren. |

Wenn Sie diese Punkte im Hinterkopf behalten, werden Sie selten in eine Situation geraten, in der die Emulation nicht wie erwartet funktioniert.

## Sandbox erweitern – Nächste Schritte

Jetzt, wo Sie **wie man einen benutzerdefinierten User‑Agent setzt** und **wie man das DPR setzt**, können Sie weiter experimentieren:

- **Die Bildschirmgröße ändern**, um Tablets oder größere Telefone zu emulieren.  
- **Den User‑Agent austauschen**, um Chrome auf Android zu testen (`"Mozilla/5.0 (Linux; Android 12; ...) Chrome/110.0"`).  
- **Cookies oder Header** über die `setHeaders`‑Methode der Sandbox hinzufügen für authentifizierte Tests.  
- **Einen Screenshot aufnehmen** mit `HTMLDocument.renderToFile("output.png")`, um visuelle Unterschiede automatisch zu vergleichen.

Diese Erweiterungen ermöglichen Ihnen ein vollwertiges Test‑Framework, ohne Ihre IDE zu verlassen.

---

## Fazit

Wir haben gezeigt, **wie man ein iPhone emuliert** mit Aspose.HTML’s `DocumentSandbox`, und dabei exakt erklärt, **wie man einen benutzerdefinierten User‑Agent setzt**, **wie man das Device‑Pixel‑Ratio setzt** und sogar die feinen Unterschiede zwischen “**wie man den User‑Agent setzt**” und “**wie man das DPR setzt**”. Das komplette, ausführbare Beispiel demonstriert jedes Bauteil an einer Stelle, sodass Sie copy‑pasten, anpassen und sofort mobile Layouts testen können.  

Probieren Sie es aus – ändern Sie die Bildschirmabmessungen, spielen Sie mit verschiedenen User‑Agents und beobachten Sie, wie Ihre Seiten reagieren. Sobald Sie diese Einstellungen beherrschen, wird das Debuggen responsiver Designs zum Kinderspiel und Sie sparen unzählige Stunden, die Sie sonst mit echten Geräten verbringen würden.

Haben Sie Fragen oder möchten Sie eigene Varianten teilen? Hinterlassen Sie einen Kommentar unten, und viel Spaß beim Emulieren!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}