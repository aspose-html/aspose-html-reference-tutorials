---
category: general
date: 2026-10-28
description: Πώς να διαβάσετε HTML σε Java και να εξάγετε κείμενο από αρχεία HTML.
  Μάθετε να μετατρέπετε HTML σε κείμενο με το Jsoup, καλύπτοντας τεχνικές ανάγνωσης
  HTML από αρχείο και μετατροπής HTML σε κείμενο σε Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to read html
- extract text from html
- convert html to text
- html to text java
- read html from file
language: el
lastmod: 2026-10-28
og_description: Πώς να διαβάσετε HTML σε Java και να εξάγετε κείμενο από αρχεία HTML.
  Αυτό το σεμινάριο δείχνει μια πλήρη λύση για τη μετατροπή του HTML σε κείμενο χρησιμοποιώντας
  το Jsoup.
og_image_alt: Diagram showing how to read HTML and extract text in Java
og_title: Πώς να διαβάσετε HTML και να εξάγετε κείμενο σε Java – γρήγορος οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  headline: How to read HTML and extract text in Java – a step‑by‑step guide
  type: TechArticle
- description: How to read HTML in Java and extract text from HTML files. Learn to
    convert HTML to text with Jsoup, covering read html from file and html to text
    java techniques.
  name: How to read HTML and extract text in Java – a step‑by‑step guide
  steps:
  - name: Maven
    text: '```xml <dependency> <groupId>org.jsoup</groupId> <artifactId>jsoup</artifactId>
      <version>1.17.2</version> </dependency> ```'
  - name: Gradle
    text: '```gradle implementation ''org.jsoup:jsoup:1.17.2'' ```'
  - name: Expected output
    text: 'Assuming `input.html` contains:'
  - name: Running the program
    text: '```bash javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java java -cp .:jsoup-1.17.2.jar
      HtmlToTextDemo ```'
  type: HowTo
tags:
- Java
- HTML parsing
- Text extraction
title: Πώς να διαβάσετε HTML και να εξάγετε κείμενο σε Java – ένας βήμα‑βήμα οδηγός
url: /el/java/conversion-html-to-other-formats/how-to-read-html-and-extract-text-in-java-a-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διαβάσετε HTML και να εξάγετε κείμενο σε Java – ένας οδηγός βήμα‑βήμα

Αν χρειάζεστε **how to read html** από τοπικό αρχείο, αυτός ο οδηγός παρέχει μια πλήρη λύση. Θα μάθετε πώς να φορτώνετε ένα έγγραφο HTML, να εξάγετε το απλό κείμενο και προαιρετικά να μετατρέπετε το HTML σε κείμενο με λεπτομερή έλεγχο. Στο τέλος του οδηγού μπορείτε να εκτελέσετε τον κώδικα παραδείγματος και να δείτε το εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα.

Η ανάγνωση αρχείων HTML είναι μια συνηθισμένη εργασία όταν επεξεργάζεστε δεδομένα που έχουν συλλεχθεί από το web, δημιουργείτε αναφορές ή καθαρίζετε περιεχόμενο που δημιουργείται από χρήστες. Τα παρακάτω βήματα καλύπτουν όλα όσα χρειάζεστε, από την προσθήκη της απαιτούμενης βιβλιοθήκης μέχρι τη διαχείριση ειδικών περιπτώσεων όπως κατεστραμμένο markup ή προβλήματα κωδικοποίησης χαρακτήρων.

## Τι θα χρειαστείτε

- Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται και με παλαιότερες εκδόσεις)
- Maven ή Gradle για διαχείριση εξαρτήσεων, ή το Jsoup JAR προστιθέμενο χειροκίνητα
- Ένα αρχείο HTML με όνομα `input.html` τοποθετημένο στον φάκελο `src/main/resources` του έργου (μπορείτε να αλλάξετε τη διαδρομή αργότερα)

## Ρύθμιση της βιβλιοθήκης Jsoup

Το Jsoup είναι μια ελαφριά, καλά τεκμηριωμένη βιβλιοθήκη που αναλύει HTML σε μια δομή τύπου DOM. Διαχειρίζεται σπασμένο HTML με χάρη, κάτι που το καθιστά ιδανικό για εργασίες **extract text from html**.

### Maven

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

### Gradle

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Αν προτιμάτε μια χειροκίνητη λήψη, τοποθετήστε το JAR στο classpath σας και εισάγετε `org.jsoup.*` στο αρχείο πηγαίου κώδικα.

## Φόρτωση HTML από αρχείο

Το πρώτο προγραμματιστικό βήμα είναι η ανάγνωση του αρχείου σε ένα αντικείμενο `Document`. Το Jsoup προσφέρει τη στατική μέθοδο `parse` που δέχεται ένα `File` και ένα όνομα charset.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Path to the HTML file – adjust if your file lives elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Parse the file using UTF‑8 encoding
            Document doc = Jsoup.parse(input, "UTF-8");
            // Continue with text extraction…
        } catch (IOException e) {
            System.err.println("Failed to read the HTML file: " + e.getMessage());
        }
    }
}
```

**Γιατί είναι σημαντικό:** `Jsoup.parse(File, String)` διαβάζει τα ακατέργαστα bytes, τα αποκωδικοποιεί σύμφωνα με το παρεχόμενο charset και δημιουργεί ένα καθαρό DOM. Αυτή η προσέγγιση είναι πιο ασφαλής από το να διαβάζετε το αρχείο σε μια συμβολοσειρά μόνοι σας, επειδή το Jsoup κανονικοποιεί τις αλλαγές γραμμής και διορθώνει αυτόματα κοινά σφάλματα markup.

## Εξαγωγή απλού κειμένου από το HTML

Μόλις έχετε ένα `Document`, η ανάκτηση του ορατού κειμένου γίνεται με μία κλήση μεθόδου. Η μέθοδος `text()` συνενώνει το κειμενικό περιεχόμενο όλων των στοιχείων ενώ απορρίπτει ετικέτες, scripts και styles.

```java
// Inside the try block from the previous snippet
String plainText = doc.body().text();
System.out.println("Extracted text:");
System.out.println(plainText);
```

Η κλήση `body()` περιορίζει την εξαγωγή στο στοιχείο `<body>`, το οποίο είναι ο τυπικός στόχος όταν **read html from file** για ανάλυση περιεχομένου. Η προκύπτουσα συμβολοσειρά περιέχει κενά που έχουν συμπτυχθεί σε μονά κενά, μιμούμενη τον τρόπο που ένας φυλλομετρητής θα εμφανίσει το κείμενο.

### Αναμενόμενη έξοδος

Υποθέτοντας ότι το `input.html` περιέχει:

```html
<!DOCTYPE html>
<html>
<head><title>Sample</title></head>
<body>
  <h1>Hello World</h1>
  <p>This is a <strong>demo</strong> page.</p>
</body>
</html>
```

Η εκτέλεση του προγράμματος εκτυπώνει:

```
Extracted text:
Hello World This is a demo page.
```

## Μετατροπή HTML σε κείμενο με πρόσθετες επιλογές

Μερικές φορές χρειάζεστε περισσότερο έλεγχο από ό,τι παρέχει η `text()`—π.χ. διατήρηση αλλαγών γραμμής, διατήρηση αρίθμησης λιστών ή αγνόηση ορισμένων ετικετών. Το `NodeTraversor` του Jsoup σε συνδυασμό με έναν προσαρμοσμένο `NodeVisitor` σας δίνει αυτή την ευελιξία.

```java
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

public class HtmlToTextDemo {

    // ... (main method unchanged)

    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();
        NodeVisitor visitor = new NodeVisitor() {
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Preserve line breaks for block elements
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }
            public void tail(Node node, int depth) {
                // No action needed on exit
            }
        };
        NodeTraversor.traverse(visitor, doc.body());
        // Collapse multiple newlines into a single one
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

Αντικαταστήστε την απλή κλήση `doc.body().text()` με:

```java
String detailedText = convertHtmlToText(doc);
System.out.println("Detailed conversion:");
System.out.println(detailedText);
```

**Γιατί λειτουργεί:** Ο επισκέπτης διασχίζει το DOM βάθος‑πρώτα, προσθέτοντας μια νέα γραμμή πριν από κάθε στοιχείο επιπέδου block (π.χ. `<p>`, `<div>`, `<h1>`). Αυτό διατηρεί το διαχωρισμό παραγράφων, κάτι που είναι χρήσιμο όταν **convert html to text** για αναγνωσιμότητα ή για επόμενες NLP διεργασίες.

## Συνηθισμένα προβλήματα και βέλτιστες πρακτικές

| Πρόβλημα | Γιατί συμβαίνει | Προτεινόμενη διόρθωση |
|----------|----------------|-----------------------|
| Λάθος κωδικοποίηση χαρακτήρων | Αρχεία αποθηκευμένα σε ISO‑8859‑1 αλλά αναλυμένα ως UTF‑8 παράγουν παραμορφωμένους χαρακτήρες. | Ανιχνεύστε την κωδικοποίηση από το meta tag του αρχείου (`<meta charset="...">`) ή περάστε το σωστό όνομα στο `Jsoup.parse`. |
| Μεγάλα αρχεία | Η φόρτωση ενός πολύ μεγάλου αρχείου HTML στη μνήμη μπορεί να προκαλέσει `OutOfMemoryError`. | Μεταδώστε το αρχείο με `Jsoup.parse(File, String, String baseUri)` και επεξεργαστείτε τους κόμβους σταδιακά, ή αυξήστε το μέγεθος της μνήμης heap της JVM. |
| Ανεπιθύμητο κείμενο script/style | `text()` αφαιρεί το περιεχόμενο script και style, αλλά προσαρμοσμένοι επισκέπτες μπορεί ακούσια να το συμπεριλάβουν. | Παραλείψτε κόμβους των οποίων το όνομα ετικέτας είναι `script` ή `style` μέσα στη μέθοδο `head` του επισκέπτη. |
| Διατήρηση κενών | Η κατάρρευση των κενών μπορεί να χάσει τη μορφοποίηση που χρειάζεται για τη μετατροπή σε markdown. | Χρησιμοποιήστε `Element.wholeText()` για ακατέργαστους κόμβους κειμένου, μετά επεξεργαστείτε τα κενά χειροκίνητα. |

Η αντιμετώπιση αυτών των ζητημάτων διασφαλίζει ότι η λύση **html to text java** λειτουργεί αξιόπιστα σε διάφορες εισόδους.

## Πλήρες εκτελέσιμο παράδειγμα

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που δείχνει όλη τη ροή εργασίας—από τη ρύθμιση των εξαρτήσεων μέχρι την επαλήθευση του αποτελέσματος. Αντιγράψτε τον κώδικα σε ένα αρχείο με όνομα `HtmlToTextDemo.java`, τοποθετήστε ένα αρχείο `input.html` δίπλα του και εκτελέστε `javac && java` όπως φαίνεται.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.nodes.Node;
import org.jsoup.select.NodeTraversor;
import org.jsoup.select.NodeVisitor;

import java.io.File;
import java.io.IOException;

public class HtmlToTextDemo {

    public static void main(String[] args) {
        // Adjust the path if your HTML file is located elsewhere
        File input = new File("src/main/resources/input.html");

        try {
            // Load and parse the HTML file using UTF‑8
            Document doc = Jsoup.parse(input, "UTF-8");

            // Simple extraction – suitable for most cases
            String plain = doc.body().text();
            System.out.println("=== Simple extraction ===");
            System.out.println(plain);
            System.out.println();

            // Detailed conversion – keeps line breaks for readability
            String detailed = convertHtmlToText(doc);
            System.out.println("=== Detailed conversion ===");
            System.out.println(detailed);
        } catch (IOException e) {
            System.err.println("Error reading HTML file: " + e.getMessage());
        }
    }

    /**
     * Walks the DOM and builds a text representation that preserves
     * line breaks for block‑level elements.
     *
     * @param doc the parsed HTML document
     * @return a readable plain‑text version of the HTML body
     */
    private static String convertHtmlToText(Document doc) {
        StringBuilder sb = new StringBuilder();

        NodeVisitor visitor = new NodeVisitor() {
            @Override
            public void head(Node node, int depth) {
                if (node instanceof Element) {
                    Element el = (Element) node;
                    // Add a newline before block elements (e.g., <p>, <div>, <h1>)
                    if (el.isBlock()) {
                        sb.append('\n');
                    }
                } else if (node instanceof org.jsoup.nodes.TextNode) {
                    sb.append(((org.jsoup.nodes.TextNode) node).text());
                }
            }

            @Override
            public void tail(Node node, int depth) {
                // No operation needed when exiting a node
            }
        };

        NodeTraversor.traverse(visitor, doc.body());

        // Collapse consecutive newlines and trim leading/trailing whitespace
        return sb.toString().replaceAll("\\n{2,}", "\n").trim();
    }
}
```

### Εκτέλεση του προγράμματος

```bash
javac -cp jsoup-1.17.2.jar HtmlToTextDemo.java
java -cp .:jsoup-1.17.2.jar HtmlToTextDemo
```

Η κονσόλα εμφανίζει τόσο την απλή εξαγωγή όσο και την λεπτομερή

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να χρησιμοποιήσετε XPath σε Java – Διαβάστε HTML και εξάγετε κείμενο](/html/english/java/creating-managing-html-documents/how-to-use-xpath-in-java-read-html-and-extract-text/)
- [Πώς να αναλύσετε HTML σε Java – Εξάγετε κείμενο από άρθρα HTML](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Εξαγωγή κειμένου από HTML με Java – Πλήρης οδηγός βήμα‑βήμα](/html/english/java/creating-managing-html-documents/extract-text-from-html-with-java-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}