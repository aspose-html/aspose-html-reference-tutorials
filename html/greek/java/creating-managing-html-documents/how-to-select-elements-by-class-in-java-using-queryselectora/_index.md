---
category: general
date: 2026-09-29
description: Μάθετε πώς να επιλέγετε στοιχεία κατά κλάση, να διαβάζετε HTML από αρχείο
  και να εντοπίζετε εξωτερικούς συνδέσμους σε Java. Αυτός ο οδηγός βήμα‑βήμα καλύπτει
  την αποδοτική επανάληψη μιας λίστας κόμβων (NodeList).
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- select elements by class
- read html from file
- find external links
- iterate nodelist java
- use queryselectorall java
language: el
lastmod: 2026-09-29
og_description: Επιλέξτε στοιχεία κατά κλάση στην Java, διαβάστε HTML από αρχείο και
  βρείτε εξωτερικούς συνδέσμους χρησιμοποιώντας querySelectorAll. Ακολουθήστε το πλήρες
  παράδειγμα για να επαναλάβετε ένα NodeList.
og_image_alt: Screenshot showing Java code that selects elements by class from an
  HTML file
og_title: Επιλογή στοιχείων κατά κλάση στη Java – πλήρης οδηγός με querySelectorAll
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to select elements by class, read HTML from file, and find
    external links in Java. This step‑by‑step guide covers iterating a NodeList efficiently.
  headline: How to select elements by class in Java using querySelectorAll
  type: TechArticle
- questions:
  - answer: Yes. `Jsoup.parse` treats the input as a fragment and automatically adds
      missing root elements, allowing selectors to work on the fragment’s body.
    question: Does this work with HTML fragments that lack a `<html>` root?
  - answer: The standard Java DOM API (`org.w3c.dom`) does not include `querySelectorAll`.
      Libraries such as **HTMLUnit** or **jodd-lagarto** provide similar methods.
      The pattern shown here—load, select with CSS, iterate—remains the same.
    question: Can I use `querySelectorAll` without jsoup?
  - answer: 'After obtaining each `Element`, you can call `link.attr("href", "newUrl")`
      and then write the document back to disk with `Files.writeString`. ## Conclusion
      You now know how to **select elements by class**, **read HTML from file**, **find
      external links**, and **iterate a NodeList in Java** using `qu'
    question: What if I need to modify the links instead of just printing them?
  type: FAQPage
tags:
- Java
- HTML parsing
- DOM manipulation
title: Πώς να επιλέξετε στοιχεία κατά κλάση στη Java χρησιμοποιώντας το querySelectorAll
url: /el/java/creating-managing-html-documents/how-to-select-elements-by-class-in-java-using-queryselectora/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να επιλέξετε στοιχεία κατά κλάση σε Java χρησιμοποιώντας querySelectorAll

Αν χρειάζεστε **select elements by class** ενώ επεξεργάζεστε ένα αρχείο HTML σε Java, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα μάθετε να διαβάζετε HTML από αρχείο, να χρησιμοποιείτε `querySelectorAll` για να βρείτε εξωτερικούς συνδέσμους και να επαναλαμβάνετε με ασφάλεια το προκύπτον `NodeList`.

Η εργασία με HTML σε Java συχνά φαίνεται βαριά, αλλά οι σύγχρονες βιβλιοθήκες σας παρέχουν ένα σύντομο, API βασισμένο σε CSS‑selector. Το παρακάτω παράδειγμα χρησιμοποιεί **jsoup** (έκδοση 1.17.2) επειδή υλοποιεί επιλογείς σε στυλ `querySelectorAll` και επιστρέφει μια συλλογή `Elements` που συμπεριφέρεται όπως ένα `NodeList`. Μπορείτε να προσαρμόσετε την ίδια λογική σε άλλες υλοποιήσεις DOM αν χρειαστεί.

## Προαπαιτούμενα

* JDK 17 ή νεότερο εγκατεστημένο.
* Maven ή Gradle για διαχείριση εξαρτήσεων.
* Βασική εξοικείωση με Java streams και το μοντέλο DOM.

Προσθέστε το jsoup στο έργο σας:

```xml
<!-- Maven -->
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

```gradle
// Gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

## Βήμα 1: Διαβάστε HTML από αρχείο

Η πρώτη εργασία είναι να φορτώσετε το έγγραφο HTML από το δίσκο. Η μέθοδος `Jsoup.parse(Path, Charset)` διαβάζει το αρχείο και δημιουργεί ένα δέντρο DOM που μπορείτε να ερωτήσετε.

```java
import java.nio.file.Paths;
import java.nio.charset.StandardCharsets;
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class HtmlLoader {
    /**
     * Loads an HTML file and returns a Jsoup Document.
     *
     * @param filePath absolute or relative path to the HTML file
     * @return parsed Document ready for DOM queries
     * @throws IOException if the file cannot be read
     */
    public static Document load(String filePath) throws IOException {
        return Jsoup.parse(Paths.get(filePath).toFile(),
                           StandardCharsets.UTF_8.name(),
                           "");
    }
}
```

*Γιατί είναι σημαντικό*: Η φόρτωση του αρχείου μία φορά αποφεύγει επαναλαμβανόμενες εισόδους/εξόδους ενώ επαναλαμβάνετε τα στοιχεία αργότερα. Το αντικείμενο `Document` διατηρεί ολόκληρο το DOM, επιτρέποντας γρήγορα ερωτήματα επιλογέα.

## Βήμα 2: Χρησιμοποιήστε `querySelectorAll` για να επιλέξετε στοιχεία κατά κλάση

Τώρα που το έγγραφο βρίσκεται στη μνήμη, μπορείτε να **select elements by class** χρησιμοποιώντας έναν CSS selector. Ο selector `"a.external"` ταιριάζει με ετικέτες `<a>` που έχουν την κλάση `external`—ακριβώς ό,τι χρειάζεστε για **find external links**.

```java
import org.jsoup.select.Elements;
import org.jsoup.nodes.Element;

/**
 * Returns all anchor elements with the CSS class "external".
 *
 * @param doc the parsed HTML document
 * @return a collection of matching Elements
 */
public static Elements findExternalLinks(Document doc) {
    // querySelectorAll is simulated by the select() method in Jsoup
    return doc.select("a.external");
}
```

*Γιατί είναι σημαντικό*: Η χρήση ενός selector κλάσης είναι τόσο εκφραστική όσο και αποδοτική. Η βιβλιοθήκη μετατρέπει τον selector σε βελτιστοποιημένη διάσχιση, ώστε να μην χρειάζεται να γράψετε χειροκίνητους βρόχους πάνω σε κάθε κόμβο.

## Βήμα 3: Επανάληψη του NodeList (Elements) σε Java

`Elements` υλοποιεί `Iterable<Element>`, πράγμα που σημαίνει ότι μπορείτε να χρησιμοποιήσετε έναν τυπικό βρόχο `for‑e​ach` για να **iterate NodeList Java** αντικείμενα. Ο παρακάτω βρόχος εκτυπώνει το χαρακτηριστικό `href` κάθε συνδέσμου.

```java
/**
 * Prints the href attribute of every external link.
 *
 * @param externalLinks collection returned by findExternalLinks()
 */
public static void printExternalLinks(Elements externalLinks) {
    for (Element link : externalLinks) {
        System.out.println("External link: " + link.attr("href"));
    }
}
```

*Γιατί είναι σημαντικό*: Η άμεση επανάληψη διατηρεί τον κώδικα αναγνώσιμο και αποφεύγει το κόστος μετατροπής της συλλογής σε stream όταν χρειάζεστε μόνο απλή έξοδο.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας τα τρία βήματα δημιουργείται ένα αυτόνομο πρόγραμμα που μπορείτε να εκτελέσετε από τη γραμμή εντολών.

```java
import java.io.IOException;
import org.jsoup.nodes.Document;
import org.jsoup.select.Elements;

public class ExternalLinkExtractor {

    public static void main(String[] args) {
        // Validate input
        if (args.length != 1) {
            System.err.println("Usage: java ExternalLinkExtractor <input.html>");
            System.exit(1);
        }

        String inputPath = args[0];

        try {
            // Step 1: read HTML from file
            Document doc = HtmlLoader.load(inputPath);

            // Step 2: select elements by class (find external links)
            Elements externalLinks = findExternalLinks(doc);

            // Step 3: iterate NodeList Java and print hrefs
            printExternalLinks(externalLinks);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    // Reuse methods from previous sections
    private static Elements findExternalLinks(Document doc) {
        return doc.select("a.external");
    }

    private static void printExternalLinks(Elements externalLinks) {
        for (org.jsoup.nodes.Element link : externalLinks) {
            System.out.println("External link: " + link.attr("href"));
        }
    }
}
```

### Αναμενόμενη έξοδος

Υποθέτοντας ότι το `input.html` περιέχει:

```html
<a class="external" href="https://example.com">Example</a>
<a class="internal" href="/about">About</a>
<a class="external" href="https://openai.com">OpenAI</a>
```

Η εκτέλεση του προγράμματος εκτυπώνει:

```
External link: https://example.com
External link: https://openai.com
```

## Επαγγελματικές συμβουλές και κοινά προβλήματα

* **Encoding matters** – Πάντα διαβάζετε το αρχείο με UTF‑8 (ή το charset που ταιριάζει με την πηγή σας). Λανθασμένο κωδικοποίηση μπορεί να καταστρέψει χαρακτήρες στις τιμές των χαρακτηριστικών.
* **Multiple classes** – Αν ένα στοιχείο έχει πολλές κλάσεις (π.χ., `class="btn external"`), ο selector `"a.external"` εξακολουθεί να ταιριάζει επειδή οι CSS class selectors ελέγχουν την παρουσία του token, όχι την ακριβή συμβολοσειρά.
* **Performance tip** – Αν χρειάζεστε μόνο το χαρακτηριστικό `href`, μπορείτε να το ζητήσετε απευθείας με `doc.select("a.external[href]").eachAttr("href")`. Αυτό αποφεύγει τη δημιουργία πλήρων αντικειμένων `Element` για κάθε αντιστοίχηση.
* **Null safety** – Η `link.attr("href")` επιστρέφει κενή συμβολοσειρά αν λείπει το χαρακτηριστικό, έτσι δεν χρειάζεται έλεγχος null πριν την εκτύπωση.

## Συχνές ερωτήσεις

**Q: Does this work with HTML fragments that lack a `<html>` root?**  
A: Ναι. Η `Jsoup.parse` αντιμετωπίζει την είσοδο ως απόσπασμα και προσθέτει αυτόματα τα ελλιπή στοιχεία ρίζας, επιτρέποντας στους selectors να λειτουργούν στο σώμα του αποσπάσματος.

**Q: Can I use `querySelectorAll` without jsoup?**  
A: Το τυπικό Java DOM API (`org.w3c.dom`) δεν περιλαμβάνει `querySelectorAll`. Βιβλιοθήκες όπως **HTMLUnit** ή **jodd-lagarto** παρέχουν παρόμοιες μεθόδους. Το μοτίβο που δείχνεται εδώ—φόρτωση, επιλογή με CSS, επανάληψη—παραμένει το ίδιο.

**Q: What if I need to modify the links instead of just printing them?**  
A: Αφού αποκτήσετε κάθε `Element`, μπορείτε να καλέσετε `link.attr("href", "newUrl")` και στη συνέχεια να γράψετε το έγγραφο πίσω στο δίσκο με `Files.writeString`.

## Συμπέρασμα

Τώρα ξέρετε πώς να **select elements by class**, **read HTML from file**, **find external links**, και **iterate a NodeList in Java** χρησιμοποιώντας selectors σε στυλ `querySelectorAll`. Το πλήρες παράδειγμα δείχνει μια καθαρή, έτοιμη για παραγωγή ροή εργασίας που μπορείτε να ενσωματώσετε σε μεγαλύτερα pipelines εξόρυξης ή μετασχηματισμού.

Στη συνέχεια, εξερευνήστε συναφή θέματα όπως **parsing dynamic content with HTMLUnit**, **writing modified HTML back to disk**, ή **using Java streams to collect link URLs into a list**. Κάθε ένα από αυτά βασίζεται στην κεντρική τεχνική επιλογής με βάση την κλάση που παρουσιάστηκε εδώ. Καλή προγραμματιστική!

## Τι θα πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to query HTML in Java – Select elements, filter by attribute, and get text](/html/english/java/css-html-form-editing/how-to-query-html-in-java-select-elements-filter-by-attribut/)
- [Iterate NodeList Java – Read HTML & Get Image src](/html/english/java/creating-managing-html-documents/iterate-nodelist-java-read-html-get-image-src/)
- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}