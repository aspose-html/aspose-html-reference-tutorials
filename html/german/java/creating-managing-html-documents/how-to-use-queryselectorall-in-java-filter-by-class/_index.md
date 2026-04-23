---
category: general
date: 2026-04-23
description: Wie man querySelectorAll in Java verwendet, um Elemente nach Klasse zu
  filtern, Attributwerte zu lesen und die NodeList für die Extraktion von Produktdaten
  zu iterieren.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: de
og_description: Wie man querySelectorAll in Java verwendet, um Elemente nach Klasse
  zu filtern, Attributwerte auszulesen und die NodeList für die Extraktion von Produktdaten
  zu iterieren.
og_title: Wie man querySelectorAll in Java verwendet – Nach Klasse filtern
tags:
- Java
- HTML parsing
- DOM manipulation
title: Wie man querySelectorAll in Java verwendet – nach Klasse filtern
url: /de/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man querySelectorAll in Java verwendet – Filtern nach Klasse

querySelectorAll in Java zu verwenden ist entscheidend, wenn Sie bestimmte Elemente aus einem HTML-Dokument extrahieren müssen. In diesem Tutorial filtern wir Elemente nach Klasse, lesen Attributwerte aus und iterieren über eine NodeList, um Produktpreise von einer Katalogseite zu holen.  

Haben Sie sich schon einmal an einer riesigen HTML-Datei vergriffen und gefragt, wie Sie nur die „on‑sale“-Karten extrahieren können, ohne einen eigenen Parser zu schreiben? Genau dieses Problem lösen wir hier – ohne zusätzliche Bibliotheken außer Aspose.HTML und mit ein paar einfachen Schritten.

Am Ende haben Sie ein vollständiges, ausführbares Programm, das:

* **Wählt Elemente** mit einem CSS-Selektor aus (`select elements css selector`),
* **Filtert nach Klasse** (`filter elements by class`),
* **Liest ein benutzerdefiniertes Attribut** (`how to read attribute`),
* **Iteriert über die resultierende NodeList** (`iterate nodelist java`).

Vorkenntnisse mit Aspose.HTML sind nicht erforderlich – Sie benötigen lediglich ein einfaches Java-Setup und eine HTML-Datei zum Testen.

![Wie man querySelectorAll in Java verwendet Beispiel](https://example.com/images/queryselectorall-java.png "Wie man querySelectorAll in Java verwendet")

---

## Was Sie benötigen

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| **Java 17+** | Moderne Sprachfeatures und bessere Modulverwaltung. |
| **Aspose.HTML for Java** (latest version) | Stellt die `Document`-Klasse und die CSS‑Selektor-Engine bereit. |
| **catalog.html** (sample HTML) | Die Quelle, gegen die wir abfragen. |
| **IDE or plain `javac`** | Zum Kompilieren und Ausführen des Demos. |

Falls Sie Aspose.HTML noch nicht zu Ihrem Projekt hinzugefügt haben, legen Sie die JAR-Datei in Ihren `libs`‑Ordner und fügen Sie sie dem Klassenpfad hinzu:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Schritt 1 – Laden des HTML-Dokuments

Bevor Sie etwas abfragen können, benötigen Sie ein `Document`‑Objekt, das die HTML‑Datei repräsentiert. Denken Sie daran, dass Sie ein Tabellenblatt laden müssen, bevor Sie Zellen lesen können.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Warum das wichtig ist:** Die `Document`‑Klasse parst das Markup in einen DOM‑Baum, wodurch die CSS‑Selektor‑Engine arbeiten kann. Wenn Sie diesen Schritt überspringen, bleibt Ihnen nur ein einfacher String und keine Möglichkeit, `querySelectorAll` zu verwenden.

---

## Schritt 2 – Elemente mit einem CSS-Selektor auswählen

Jetzt kommt das Kernstück: **wie man querySelectorAll verwendet**. Die Methode akzeptiert jeden gültigen CSS-Selektor, sodass Sie so präzise – oder so breit – sein können, wie Sie möchten. Für unser Szenario wollen wir Produktkarten, die:

* die Klasse `product-card` besitzen,
* ebenfalls die Klasse `sale` haben,
* und ein `data-price`‑Attribut besitzen.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Erklärung:**  
> * `.product-card.sale` → filtert Elemente, die **beide** Klassen enthalten.  
> * `[data-price]` → stellt sicher, dass das Attribut existiert und filtert damit effektiv **nach Klasse** **und** Attribut in einem Aufruf.  
> * Das Ergebnis ist eine `NodeList`, eine geordnete Sammlung, über die Sie iterieren können.

Falls Sie jemals **select elements css selector** für ein anderes Muster benötigen, ändern Sie einfach den String – kein Code‑Rewrite nötig.

---

## Schritt 3 – Die NodeList in Java iterieren

Eine `NodeList` verhält sich ähnlich wie ein Array, implementiert jedoch nicht `Iterable`. Deshalb verwenden wir eine klassische `for`‑Schleife – perfekt für **iterate nodelist java**‑Szenarien.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Warum eine `for`‑Schleife?**  
> Sie gibt Ihnen direkten Zugriff auf den Index, was für Logging oder bedingte Verzweigungen praktisch sein kann. Wenn Sie lieber eine `while`‑Schleife verwenden, bleibt die Logik identisch – ändern Sie einfach die Schleifen‑Konstruktion.

---

## Schritt 4 – Das `data-price`‑Attribut lesen

Jetzt beantworten wir endlich **how to read attribute** Werte von einem Element. In der DOM‑API gibt `getAttribute` den rohen String zurück, genau wie er im Markup erscheint.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Tipp:** Falls das Attribut fehlen könnte, gibt `getAttribute` `null` zurück. Sie können das mit einer einfachen Prüfung abfangen:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Schritt 5 – Ergebnisse ausgeben

Zu guter Letzt geben wir jeden Preis in der Konsole aus. Das spiegelt ein real‑weltliches Szenario wider, in dem Sie die Werte wahrscheinlich in eine Datenbank oder ein API‑Payload übertragen würden.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Erwartete Konsolenausgabe

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Findet der Selektor keine passenden Knoten, wird die Schleife einfach nie ausgeführt – es wird keine Ausnahme geworfen. Das ist ein nützliches Sicherheitsnetz für **edge cases**, bei denen der Katalog leer sein könnte.

---

## Vollständiges funktionierendes Beispiel

Wenn wir alles zusammenfügen, hier die komplette Datei, die Sie in `CssSelectorDemo.java` kopieren‑und‑einfügen können:

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

Speichern Sie die Datei, kompilieren und führen Sie sie aus – beobachten Sie, wie die Preise ausgegeben werden. 🎉

---

## Häufige Fragen & Pro‑Tipps

| Frage | Antwort |
|----------|--------|
| *Was ist, wenn ich zusätzlich nach Tag‑Name auswählen muss?* | Fügen Sie einfach das Tag voran: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Kann ich mehrere Attribut‑Filter verketten?* | Absolut. Beispiel: `[data-price][data-stock]` behält nur Elemente, die **beide** Attribute besitzen. |
| *Ist `querySelectorAll` case‑sensitive?* | Ja – CSS‑Selektoren behandeln Klassen- und Attributnamen in HTML5 als case‑sensitive. |
| *Wie gehe ich mit einer riesigen HTML‑Datei um?* | Aspose.HTML streamt das Dokument, Sie können den Selektor jedoch auch auf einen Teilbaum beschränken (`someElement.querySelectorAll(...)`). |
| *What |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}