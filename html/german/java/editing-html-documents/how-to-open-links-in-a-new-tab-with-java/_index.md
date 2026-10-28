---
category: general
date: 2026-10-28
description: Lernen Sie, wie Sie Links in einem neuen Tab öffnen, indem Sie HTML in
  Java parsen, externe Links finden und `target="_blank"` hinzufügen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: de
lastmod: 2026-10-28
og_description: 'Öffne Links in einem neuen Tab mit Java: HTML parsen, externe Links
  finden, target="_blank" hinzufügen und das modifizierte HTML speichern.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Links in einem neuen Tab mit Java öffnen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Wie man Links mit Java in einem neuen Tab öffnet
url: /de/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Links in Java in einem neuen Tab öffnet

Wenn Sie **Links in einem neuen Tab** aus einer statischen HTML‑Datei öffnen müssen, zeigt Ihnen diese Anleitung genau, wie das geht. Sie lernen, **HTML in Java zu parsen**, **externe Links zu finden**, **target="_blank" hinzuzufügen** und **das modifizierte HTML zu speichern**, ohne Ihre IDE zu verlassen.

Das Öffnen externer Links in einem neuen Browser‑Tab verbessert die Benutzererfahrung und hält Besucher auf der ursprünglichen Seite. Die untenstehende Lösung funktioniert mit jedem HTML‑Dokument, benötigt nur die beliebte jsoup‑Bibliothek und läuft auf Java 8 oder neuer.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

* JDK 8 + installiert  
* Ein Build‑Tool (Maven oder Gradle), um die **jsoup**‑Abhängigkeit zu holen  
* Eine HTML‑Datei, die Anker‑Tags mit der Klasse `external` enthält

Ein Web‑Server oder zusätzliche Frameworks sind nicht nötig – jsoup erledigt alles lokal.

## Schritt 1: jsoup im Projekt einrichten

Fügen Sie jsoup als Abhängigkeit hinzu. Wenn Sie Maven verwenden, platzieren Sie das Folgende in `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Für Gradle fügen Sie die folgende Zeile zu `build.gradle` hinzu:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Diese Koordinaten holen die neueste stabile Version (Stand Oktober 2026). Nach dem Sync können Sie `org.jsoup`‑Klassen in Ihren Java‑Quelldateien importieren.

## Schritt 2: Das HTML‑Dokument parsen

Das Parsen der Datei ist der erste Schritt zu **open links new tab**. Die Methode `Jsoup.parse` liest die Datei in eine veränderbare DOM‑ähnliche Struktur ein.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Warum das wichtig ist*: `Document` liefert CSS‑ähnliche Selektoren, wodurch das Auffinden der benötigten Elemente trivial wird.

## Schritt 3: Externe Links finden

Jetzt lokalisieren Sie jedes `<a>`‑Element, das die Klasse `external` trägt. Das entspricht der Anforderung **find external links**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

`Elements` ist eine Sammlung der passenden Knoten. Gibt der Selektor ein leeres Set zurück, fehlt in Ihrem HTML entweder die Klasse oder es wird eine andere Benennung verwendet – passen Sie den Selektor entsprechend an.

## Schritt 4: `target="_blank"` zu jedem Link hinzufügen

Für jeden Knoten, den **find external links** zurückgibt, setzen Sie das Attribut `target` auf `_blank`. Das erfüllt den Schritt **add target blank** und sorgt dafür, dass Browser den Link in einem neuen Tab öffnen.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

Die Methode `attr` überschreibt jeden vorhandenen `target`‑Wert und garantiert ein konsistentes Verhalten aller externen Anker.

## Schritt 5: Das modifizierte HTML speichern

Nachdem Sie den DOM aktualisiert haben, schreiben Sie die Änderungen zurück in eine Datei. Damit ist der Teil **save modified html** der Anleitung abgeschlossen.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

`doc.outerHtml()` serialisiert das gesamte Dokument und bewahrt Einrückungen sowie Formatierung, wie jsoup es ursprünglich geparst hat.

## Voll funktionsfähiges Beispiel

Alle Schritte zusammen ergeben ein eigenständiges Programm, das Sie kopieren, einfügen und ausführen können.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Erwartete Ausgabe

Angenommen, `sample.html` enthält:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Nach dem Ausführen des Programms wird `updated.html` folgendes enthalten:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Nur der externe Link hat das Attribut `target="_blank"` erhalten, wodurch Browser ihn nun in einem neuen Tab öffnen.

## Pro‑Tipps und häufige Stolperfallen

* **Pro‑Tipp:** Wenn Sie Links, die mit `http://` oder `https://` beginnen, als extern behandeln wollen, selbst ohne CSS‑Klasse, erweitern Sie den Selektor: `doc.select("a[href^=http]")`.
* **Randfall:** Einige Seiten geben bereits `target="_self"` an; der Aufruf von `attr` überschreibt es und sorgt für konsistentes Verhalten.
* **Performance:** Bei sehr großen HTML‑Dateien sollten Sie das Streaming‑Parsing (`Jsoup.parse(File, String, String, Parser.htmlParser())`) in Betracht ziehen, um den Speicherverbrauch zu reduzieren.
* **Testing:** Verifizieren Sie das Ergebnis, indem Sie `updated.html` in einem Browser öffnen und den Link mit den Entwickler‑Tools inspizieren – achten Sie auf das `target`‑Attribut.

## Fazit

Sie haben nun eine komplette, ausführbare Lösung, um **Links in einem neuen Tab** mit Java zu öffnen. Das Tutorial zeigte, wie man **HTML in Java parst**, **externe Links findet**, **target blank hinzufügt** und **modifiziertes HTML speichert**, alles mit der leichten jsoup‑Bibliothek.

Ab hier können Sie:

* Den Selektor erweitern, um andere Link‑Muster zu behandeln (z. B. `rel="external"`).  
* Diese Logik mit einem Build‑Schritt kombinieren, der alle HTML‑Dateien eines Projekts verarbeitet.  
* Den Code in eine größere Content‑Management‑Pipeline integrieren.

Experimentieren Sie gern mit verschiedenen Selektoren oder Ausgabeformaten und teilen Sie Ihre Ergebnisse mit der Community!

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Use CSS in Java – Load HTML, Count Links & Evaluate XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [How to Parse HTML in Java – Extract Text from HTML Articles](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Create new html element with Java – Full Aspose.HTML Guide](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}