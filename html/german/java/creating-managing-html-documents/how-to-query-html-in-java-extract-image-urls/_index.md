---
category: general
date: 2026-03-05
description: Wie man HTML in Java abfragt, um eine HTML‑Datei zu lesen und Bilder
  zu extrahieren. Lernen Sie, HTML‑Dateien in Java zu lesen, Bild‑URLs in Java zu
  erhalten und über NodeList in Java zu iterieren.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: de
og_description: Wie man HTML in Java abfragt und Bild‑URLs abruft. Dieser Leitfaden
  zeigt, wie man eine HTML‑Datei in Java liest, Bilder findet und über eine NodeList
  in Java iteriert.
og_title: HTML in Java abfragen – Bild‑URLs extrahieren
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: HTML in Java abfragen – Bild‑URLs extrahieren
url: /de/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man HTML in Java abfragt – Bild‑URLs extrahieren

Haben Sie sich schon einmal gefragt, **wie man HTML** in Java abfragt, um jedes Bild auf einer Seite herauszuholen? Sie sind nicht allein – Entwickler müssen ständig HTML‑Dateien lesen, Bilder scrapen und dann etwas Nützliches mit den URLs machen. In diesem Tutorial gehen wir Schritt für Schritt durch ein praktisches Beispiel, das genau **zeigt, wie man HTML abfragt**, eine HTML‑Datei Java‑weise liest und Bild‑URLs Java‑weise erhält.

Wir verwenden Aspose.HTML für Java, aber die Konzepte – XPath, CSS‑Selektoren und das Durchlaufen einer `NodeList` – gelten für jede DOM‑Bibliothek. Am Ende dieses Leitfadens sind Sie sicher im **Extrahieren von Bildern**, wissen, **wie man über NodeList Java iteriert**, und haben einen einsatzbereiten Code‑Snippet, den Sie in Ihr Projekt übernehmen können.

![How to query HTML in Java example](https://example.com/placeholder.png "How to query HTML in Java")

---

## Was Sie lernen werden

- Laden eines HTML‑Dokuments von der Festplatte (read HTML file Java)
- Finden von `<img>`‑Tags mit sowohl XPath als auch CSS‑Selektoren (how to extract images)
- Durchlaufen der resultierenden `NodeList` (iterate over NodeList Java)
- Ausgeben des `src`‑Attributs jedes Bildes (get image URLs Java)

Keine externen Services, keine komplexen Build‑Tools – nur reines Java und eine einzige Maven‑Abhängigkeit.

---

## Voraussetzungen

- Java 8 oder neuer installiert
- Maven oder Gradle für das Dependency‑Management
- Grundlegende Vertrautheit mit HTML‑Struktur
- Optional aber hilfreich: eine einfache HTML‑Datei (`sample.html`) mit einigen `<figure><img …></figure>`‑Elementen

Wenn Sie das haben, können wir gleich loslegen.

---

## Schritt 1: Read HTML File Java – Dokument laden

Zuerst müssen wir das HTML in den Speicher laden. Die Klasse `HTMLDocument` von Aspose.HTML übernimmt die schwere Arbeit. Stellen Sie sich das vor wie das Aufschlagen eines Buches, damit Sie zu jeder Seite blättern können.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Warum das wichtig ist:** Das Laden der Datei liefert Ihnen einen DOM‑Baum, den Sie abfragen können. Wenn der Pfad falsch ist, erhalten Sie eine `FileNotFoundException`, also prüfen Sie den Speicherort, bevor Sie das Programm starten.

---

## Schritt 2: Bilder mit XPath finden – How to Extract Images

XPath ist eine leistungsstarke Abfragesprache, mit der Sie Knoten punktgenau ansteuern können. Hier fragen wir nach jedem `<img>` innerhalb eines `<figure>`, das zudem ein `alt`‑Attribut besitzt.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Warum XPath?** Es ist kompakt und funktioniert selbst, wenn das HTML unordentlich ist. Der Ausdruck `//figure/img[@alt]` bedeutet: „jedes `<img>` unter einem `<figure>`, das ein `alt`‑Attribut hat.“ Wenn Sie nach anderen Attributen filtern wollen, passen Sie einfach die Klammern an.

---

## Schritt 3: Bilder mit CSS‑Selektor finden – Alternative Way to Extract Images

Manchmal bevorzugt man die CSS‑Syntax, weil sie der Schreibweise in Stylesheets entspricht. `querySelectorAll` akzeptiert denselben Selektor, den Sie im Browser verwenden würden.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Warum beides?** Die Demonstration beider Methoden zeigt, dass Sie das Werkzeug wählen können, mit dem Sie sich am wohlsten fühlen. In der Praxis würden Sie sich für eine Methode entscheiden, aber beide Beispiele machen das Tutorial vollständiger.

---

## Schritt 4: Iterate Over NodeList Java – Get Image URLs Java

Jetzt, wo wir eine Sammlung haben, müssen wir sie durchlaufen. Hier kommt **iterate over NodeList Java** ins Spiel. Wir holen das `src`‑Attribut jedes Bildes heraus und geben es aus.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Warum eine klassische `for`‑Schleife?** Die Aspose‑`NodeList` implementiert kein `Iterable`, sodass die erweiterte `for‑each`‑Syntax nicht kompiliert. Ein Index‑Loop ist der zuverlässige Weg, um **iterate over NodeList Java** zu realisieren.

---

## Erwartete Ausgabe

Wenn das Programm gegen ein Beispiel‑HTML wie folgt läuft:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Erhält man etwa folgende Ausgabe:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

Enthält Ihre Datei mehr `<img>`‑Tags, die den Kriterien entsprechen, erhöhen sich die Zahlen entsprechend.

---

## Häufige Stolperfallen & Pro‑Tipps

- **Dateipfad‑Probleme:** Verwenden Sie einen absoluten Pfad oder platzieren Sie `sample.html` relativ zum Arbeitsverzeichnis Ihres Projekts.  
- **Fehlendes `alt`‑Attribut:** Unsere XPath/CSS‑Abfragen filtern nach `[@alt]`. Wenn Sie *alle* Bilder benötigen, entfernen Sie den Attributfilter (`//figure/img` oder `figure img`).  
- **Performance:** Bei sehr großen Dokumenten sollten Sie Streaming‑Parser in Betracht ziehen, aber für die meisten Web‑Scraping‑Aufgaben ist der DOM‑Ansatz ausreichend.  
- **Kodierungsprobleme:** Aspose.HTML respektiert das im HTML deklarierte Charset. Wenn Sie unleserliche Zeichen sehen, stellen Sie sicher, dass die Datei als UTF‑8 gespeichert ist.  

---

## Erweiterung des Beispiels

Jetzt, wo Sie **get image URLs Java** beherrschen, könnten Sie:

1. **Die Bilder herunterladen** mit `java.net.URL` und `Files.copy`.  
2. **URLs in einer Datenbank speichern** für die spätere Verarbeitung.  
3. **Nach Dateierweiterungen filtern** (`src.endsWith(".png")`).  

All das lässt sich leicht aus der Schleife in Schritt 4 ableiten.

---

## Fazit

In diesem Leitfaden haben wir **gezeigt, wie man HTML** in Java von Anfang bis Ende abfragt: das Laden der Datei, das Finden von Bildern mit sowohl XPath als auch CSS‑Selektoren und das **Iterieren über NodeList Java**, um das `src`‑Attribut jedes Bildes auszugeben. Sie verfügen nun über ein solides Fundament für **how to extract images** und wissen genau, **wie man HTML‑Datei Java liest** mit Aspose.HTML.

Passen Sie den Code gern an Ihre eigenen Scraping‑Bedürfnisse an – sei es das Auslesen anderer Attribute, das Verarbeiten von `<a>`‑Tags oder das Weiterleiten der URLs an einen Downloader. Das Muster bleibt gleich: laden, abfragen, iterieren und handeln.

Haben Sie Fragen oder möchten Sie einen coolen Anwendungsfall teilen? Hinterlassen Sie einen Kommentar unten, und happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}