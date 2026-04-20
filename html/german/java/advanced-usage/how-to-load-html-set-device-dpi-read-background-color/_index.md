---
category: general
date: 2026-02-16
description: Wie man HTML in Java lädt, die DPI des Geräts einstellt, eine virtuelle
  Bildschirmgröße definiert und die berechnete Hintergrundfarbe eines beliebigen Elements
  ausliest.
draft: false
keywords:
- how to load html
- read background color
- set device dpi
- set virtual screen size
- get computed background color
language: de
og_description: Wie man HTML in Java lädt, die DPI des Geräts einstellt, eine virtuelle
  Bildschirmgröße definiert und die berechnete Hintergrundfarbe eines beliebigen Elements
  ausliest.
og_title: Wie man HTML lädt, die DPI des Geräts einstellt und die Hintergrundfarbe
  ausliest
tags:
- Aspose.HTML
- Java
title: Wie man HTML lädt, die DPI des Geräts einstellt und die Hintergrundfarbe ausliest
url: /de/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man HTML lädt, Geräte‑DPI einstellt und Hintergrundfarbe ausliest

Haben Sie sich jemals gefragt, **wie man HTML** in einer Java‑App lädt und dann die Stile der Seite inspiziert? Sie sind nicht allein – Entwickler müssen häufig eine Webseite off‑screen rendern, die endgültigen CSS‑Werte erfassen und sie für PDF‑Konvertierung, Screenshots oder sogar automatisierte Tests verwenden.  

In diesem Leitfaden gehen wir genau darauf ein: Wir laden eine HTML‑Datei, **setzen das Geräte‑DPI**, definieren eine **virtuelle Bildschirmgröße** und lesen schließlich die **Hintergrundfarbe** des `<body>`‑Elements aus. Am Ende haben Sie ein vollständig ausführbares Snippet, das die **berechnete Hintergrundfarbe** ausgibt – kein Rätsel, nur reines Java.

## Was Sie benötigen

Bevor wir starten, stellen Sie sicher, dass Sie folgendes haben:

* Java 17 oder neuer (der Code funktioniert mit jedem aktuellen JDK).  
* Aspose.HTML for Java 23.9 oder später – laden Sie das JAR von der Aspose‑Website herunter oder fügen Sie es via Maven hinzu.  
* Eine einfache HTML‑Datei (z. B. `responsive.html`), die eine Hintergrundfarbe per CSS definiert.

Das war’s – keine zusätzlichen Frameworks, keine Browser‑Treiber. Bereit? Dann legen wir los.

![Diagram illustrating how to load html and extract computed styles](/images/load-html-diagram.png){alt="Diagramm, das zeigt, wie HTML geladen und berechnete Stile extrahiert werden"}

## Schritt 1: HTML laden und Rendering‑Optionen konfigurieren

Das Erste, was Sie tun, ist ein `HtmlLoadOptions`‑Objekt zu erstellen. Dieses Objekt sagt Aspose.HTML **wie HTML geladen** wird – einschließlich der virtuellen Bildschirmabmessungen und des DPI, das Sie emulieren möchten.

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create load options and define the virtual screen size and DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        // setVirtualScreenSize – width × height in CSS pixels
        loadOptions.setScreenSize(new Size(1280, 800));
        // setDeviceDpi – typical desktop DPI (96 is the default for most monitors)
        loadOptions.setDeviceDpi(96);
```

**Warum das wichtig ist:**  
Das Festlegen einer virtuellen Bildschirmgröße sorgt dafür, dass Media Queries wie `@media (max-width: 600px)` sich verhalten, als ob die Seite auf einem echten Monitor gerendert würde. Das DPI beeinflusst, wie CSS‑`px`‑Einheiten auf physische Pixel abgebildet werden – entscheidend, wenn Sie später Bilder oder PDFs erzeugen.

## Schritt 2: Die HTML‑Datei mit den konfigurierten Optionen laden

Jetzt laden wir die Datei tatsächlich. Beachten Sie, dass wir dieselben `loadOptions` übergeben, die wir gerade konfiguriert haben.

```java
        // 2️⃣ Load the HTML file with the options we just set.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);
```

Falls die Datei nicht gefunden wird, wirft Aspose eine klare `FileNotFoundException`. In der Produktion möchten Sie das vielleicht in einen try‑catch einbetten und auf einen Standard‑HTML‑String zurückgreifen.

## Schritt 3: Virtuelle Bildschirmgröße und Geräte‑DPI festlegen (explizit)

Obwohl wir oben bereits `setScreenSize` und `setDeviceDpi` aufgerufen haben, ist es wichtig zu betonen, dass **set virtual screen size** und **set device dpi** jederzeit vor dem Rendering angepasst werden können. Beispielsweise könnten Sie das DPI für hochauflösende Screenshots erhöhen:

```java
        // 3️⃣ Adjust DPI for a high‑resolution render (optional).
        loadOptions.setDeviceDpi(300);   // 300 DPI is common for print‑ready images
        // 4️⃣ Change screen size for a mobile layout test.
        loadOptions.setScreenSize(new Size(375, 667)); // iPhone X viewport
```

Denken Sie daran, das Dokument neu zu laden, wenn Sie diese Einstellungen nach dem ersten Laden ändern – Aspose behandelt sie als unveränderlich, sobald das `Document` erstellt wurde.

## Schritt 4: Hintergrundfarbe auslesen und berechnete Hintergrundfarbe erhalten

Mit dem Dokument im Speicher können Sie den berechneten Stil jedes Elements abfragen. Hier konzentrieren wir uns auf das `<body>`‑Tag, aber derselbe Ansatz funktioniert für `<div>`, `<p>` oder sogar Pseudo‑Elemente.

```java
        // 5️⃣ Retrieve the <body> element.
        Element bodyElement = document.getBody();

        // 6️⃣ Output the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

**Was Sie sehen werden:** Wenn `responsive.html` folgendes enthält `body { background: #ff5722; }`, gibt die Konsole etwa Folgendes aus:

```
Computed background color: rgba(255,87,34,1)
```

Das ist das Ergebnis von **get computed background color** – Aspose löst alle CSS‑Kaskadenregeln, Media Queries und sogar `!important`‑Deklarationen auf, bevor der endgültige Wert zurückgegeben wird.

## Vollständiges funktionierendes Beispiel

Alles zusammengeführt, hier das komplette, copy‑paste‑bereite Programm:

```java
import com.aspose.html.load.HtmlLoadOptions;
import com.aspose.html.load.Size;
import com.aspose.html.dom.Document;
import com.aspose.html.dom.Element;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create load options – virtual screen size + DPI.
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setScreenSize(new Size(1280, 800)); // set virtual screen size
        loadOptions.setDeviceDpi(96);                  // set device DPI (default desktop)

        // Optional: tweak for high‑resolution or mobile rendering.
        // loadOptions.setDeviceDpi(300);
        // loadOptions.setScreenSize(new Size(375, 667));

        // Step 2: Load the HTML document with the options.
        Document document = new Document("YOUR_DIRECTORY/responsive.html", loadOptions);

        // Step 3: Grab the <body> element.
        Element bodyElement = document.getBody();

        // Step 4: Print the computed background color.
        System.out.println("Computed background color: " +
                bodyElement.getComputedStyle().getBackgroundColor());
    }
}
```

### Erwartete Ausgabe

```
Computed background color: rgba(255,255,255,1)
```

*(Die genauen RGBA‑Werte hängen vom CSS in Ihrer HTML‑Datei ab.)*

## Häufige Stolperfallen & Profi‑Tipps

* **Fehlende DPI‑Einstellung?** Aspose verwendet standardmäßig 96 DPI, was hochauflösende Screenshots verwischen kann. Setzen Sie es immer explizit, wenn Sie ein scharfes Ergebnis benötigen.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}