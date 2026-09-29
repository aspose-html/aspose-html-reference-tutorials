---
category: general
date: 2026-09-29
description: Αλλάξτε το χρώμα φόντου με JavaScript σε αρχείο HTML χρησιμοποιώντας
  Java. Μάθετε πώς να φορτώνετε HTML σε Java, να εκτελείτε JavaScript σε HTML και
  να τροποποιείτε το HTML με Java για νέο φόντο σελίδας.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change background color javascript
- load html in java
- run js in html
- modify html with java
- set page background
language: el
lastmod: 2026-09-29
og_description: Αλλάξτε το χρώμα φόντου με JavaScript σε μια σελίδα HTML χρησιμοποιώντας
  Java. Αυτό το σεμινάριο σας δείχνει πώς να φορτώσετε HTML σε Java, να εκτελέσετε
  JS σε HTML και να ορίσετε το φόντο της σελίδας προγραμματιστικά.
og_image_alt: Screenshot of Java code that changes the page background color
og_title: Αλλαγή χρώματος φόντου JavaScript με Java – οδηγός βήμα‑προς‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Change background color javascript in an HTML file using Java. Learn
    to load html in java, run js in html, and modify html with java for a new page
    background.
  headline: How to change background color javascript using Java
  type: TechArticle
tags:
- Java
- HTMLUnit
- JavaScript
- HTML manipulation
title: Πώς να αλλάξετε το χρώμα του φόντου σε JavaScript χρησιμοποιώντας Java
url: /el/java/editing-html-documents/how-to-change-background-color-javascript-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να αλλάξετε το χρώμα φόντου javascript χρησιμοποιώντας Java

Αν χρειάζεστε **change background color javascript** σε ένα υπάρχον αρχείο HTML, μπορείτε να το κάνετε εξ ολοκλήρου από τη Java χωρίς να ανοίξετε έναν περιηγητή. Αυτό το tutorial σας δείχνει πώς να **load html in java**, να εκτελέσετε ένα μικρό απόσπασμα JavaScript, και στη συνέχεια να **modify html with java** ώστε το φόντο της σελίδας να ενημερωθεί.  

Η λύση λειτουργεί με τη βιβλιοθήκη ανοιχτού κώδικα **HTMLUnit**, η οποία παρέχει έναν headless browser που μπορεί να αξιολογήσει JavaScript ακριβώς όπως θα έκανε ένας πραγματικός περιηγητής. Στο τέλος αυτού του οδηγού θα έχετε μια επαναχρησιμοποιήσιμη μέθοδο που **sets page background** σε οποιοδήποτε χρώμα επιλέγετε.

## Προαπαιτούμενα

| Τι χρειάζεστε | Γιατί είναι σημαντικό |
|---------------|-----------------------|
| Java 8 ή νεότερη | Η HTMLUnit απαιτεί τουλάχιστον Java 8. |
| Maven ή Gradle εργαλείο κατασκευής | Για την αυτόματη λήψη της εξάρτησης HTMLUnit. |
| Ένα αρχείο HTML που θέλετε να επεξεργαστείτε (π.χ., `input.html`) | Το πηγαίο έγγραφο που θα φορτωθεί και θα τροποποιηθεί. |

Προσθέστε την HTMLUnit στο έργο σας:

*Maven*  

```xml
<dependency>
    <groupId>net.sourceforge.htmlunit</groupId>
    <artifactId>htmlunit</artifactId>
    <version>2.71.0</version>
</dependency>
```

*Gradle*  

```gradle
implementation 'net.sourceforge.htmlunit:htmlunit:2.71.0'
```

> **Συμβουλή επαγγελματία:** Χρησιμοποιήστε την πιο πρόσφατη σταθερή έκδοση της HTMLUnit για να έχετε τη πιο ακριβή μηχανή JavaScript.

## Change background color javascript – load HTML in Java

Το πρώτο βήμα είναι να φορτώσετε το έγγραφο HTML σε ένα αντικείμενο `HTMLPage`. Αυτό σας δίνει ένα API τύπου DOM και ένα περιβάλλον εκτέλεσης JavaScript.

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;

public class BackgroundColorChanger {

    /**
     * Loads an HTML file from the given path.
     *
     * @param htmlPath absolute or relative path to the source HTML file
     * @return HtmlPage representing the loaded document
     * @throws IOException if the file cannot be read
     */
    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        // WebClient acts as a headless browser; disabling CSS speeds up loading.
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);

        // Convert the file path to a URL that HTMLUnit can understand.
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }
}
```

*Γιατί αυτό είναι σημαντικό*: Το `WebClient` δημιουργεί ένα απομονωμένο περιβάλλον όπου μπορεί να τρέξει JavaScript, ώστε να **run js in html** ακριβώς όπως θα έκανε ο περιηγητής του χρήστη.

## Εκτελέστε js σε html για να ορίσετε το φόντο της σελίδας

Μόλις φορτωθεί η σελίδα, μπορείτε να αξιολογήσετε οποιαδήποτε έκφραση JavaScript. Το παρακάτω απόσπασμα αλλάζει το στυλ `backgroundColor` του στοιχείου `<body>`.

```java
/**
 * Executes JavaScript that changes the page background color.
 *
 * @param page   the HtmlPage loaded earlier
 * @param color  any valid CSS color string, e.g., "lightblue" or "#ffcc00"
 */
private static void changeBackground(HtmlPage page, String color) {
    // The eval method runs JavaScript in the page's context.
    String script = "document.body.style.backgroundColor = '" + color + "';";
    page.getEnclosingWindow().getScriptableObject().eval(script);
}
```

*Επεξήγηση*:  
- `document.body.style.backgroundColor` είναι η τυπική ιδιότητα DOM για το φόντο της σελίδας.  
- Καλώντας `eval`, **run js in html** χωρίς την ανάγκη πραγματικού παραθύρου περιηγητή.  
- Η μέθοδος είναι επαναχρησιμοποιήσιμη για οποιοδήποτε χρώμα, καλύπτοντας την απαίτηση **set page background**.

## Τροποποιήστε html με java και αποθηκεύστε το αποτέλεσμα

Αφού τρέξει το script, το DOM αντικατοπτρίζει το νέο στυλ. Τώρα μπορείτε να γράψετε το ενημερωμένο HTML πίσω στο δίσκο.

```java
import java.nio.file.Files;
import java.nio.file.Paths;

/**
 * Saves the modified HTML content to a new file.
 *
 * @param page          the HtmlPage that has been altered
 * @param outputPath    destination file path
 * @throws IOException  if writing fails
 */
private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
    // page.asXml() returns the current HTML markup, including the changed style.
    String updatedHtml = page.asXml();
    Files.write(Paths.get(outputPath), updatedHtml.getBytes());
}
```

Συνδυάζοντας όλα μαζί, παίρνετε ένα ενιαίο, εκτελέσιμο πρόγραμμα:

```java
import com.gargoylesoftware.htmlunit.WebClient;
import com.gargoylesoftware.htmlunit.html.HtmlPage;
import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class BackgroundColorChanger {

    public static void main(String[] args) {
        // Adjust these paths for your environment.
        String inputFile = "YOUR_DIRECTORY/input.html";
        String outputFile = "YOUR_DIRECTORY/js_modified.html";
        String newColor = "lightblue"; // Change to any CSS color you need.

        try {
            HtmlPage page = loadHtml(inputFile);
            changeBackground(page, newColor);
            saveModifiedHtml(page, outputFile);
            System.out.println("Background color changed to '" + newColor + "' and saved to " + outputFile);
        } catch (IOException e) {
            System.err.println("Error processing HTML file: " + e.getMessage());
        }
    }

    private static HtmlPage loadHtml(String htmlPath) throws IOException {
        WebClient webClient = new WebClient();
        webClient.getOptions().setCssEnabled(false);
        webClient.getOptions().setJavaScriptEnabled(true);
        File file = new File(htmlPath);
        return webClient.getPage(file.toURI().toURL());
    }

    private static void changeBackground(HtmlPage page, String color) {
        String script = "document.body.style.backgroundColor = '" + color + "';";
        page.getEnclosingWindow().getScriptableObject().eval(script);
    }

    private static void saveModifiedHtml(HtmlPage page, String outputPath) throws IOException {
        String updatedHtml = page.asXml();
        Files.write(Paths.get(outputPath), updatedHtml.getBytes());
    }
}
```

### Αναμενόμενη έξοδος

Η εκτέλεση του προγράμματος εκτυπώνει:

```
Background color changed to 'lightblue' and saved to YOUR_DIRECTORY/js_modified.html
```

Ανοίγοντας το `js_modified.html` σε οποιονδήποτε περιηγητή εμφανίζεται η σελίδα με ένα ανοιχτό μπλε φόντο, επιβεβαιώνοντας ότι η λειτουργία **change background color javascript** ολοκληρώθηκε με επιτυχία.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

| Κατάσταση | Πώς να το αντιμετωπίσετε |
|-----------|--------------------------|
| **Διαφορετικές μορφές χρώματος** | Περνάτε οποιαδήποτε τιμή συμβατή με CSS (`"red"`, `"#ff0000"`, `"rgb(255,0,0)"`). |
| **Απουσία ετικέτας `<body>`** | Το script θα αποτύχει σιωπηλά· μπορείτε πρώτα να διασφαλίσετε ότι υπάρχει `<body>` με `page.getFirstByXPath("//body")`. |
| **Μεγάλα αρχεία HTML** | Απενεργοποιήστε το CSS (`setCssEnabled(false)`) και ενεργοποιήστε μόνο τις δυνατότητες JavaScript που χρειάζεστε για να μειώσετε τη χρήση μνήμης. |
| **Εκτέλεση πολλαπλών script** | Καλέστε το `changeBackground` επανειλημμένα ή δημιουργήστε μια βοηθητική μέθοδο που δέχεται λίστα εντολών JavaScript. |

## Συμπέρασμα

Τώρα ξέρετε πώς να **change background color javascript** φορτώνοντας ένα αρχείο HTML στη Java, **run js in html**, και **modify html with java** για να **set page background** σε οποιοδήποτε χρώμα επιλέγετε. Το πλήρες παράδειγμα παραπάνω λειτουργεί με τη νεότερη βιβλιοθήκη HTMLUnit και μπορεί να ενσωματωθεί σε μεγαλύτερες αλυσίδες αυτοματοποίησης, όπως η μαζική επεξεργασία HTML αναφορών ή η προετοιμασία προτύπων email.

**Επόμενα βήματα**  
- Εξερευνήστε άλλες επεμβάσεις DOM (π.χ., εισαγωγή στοιχείων, αφαίρεση script).  
- Συνδυάστε αυτήν την προσέγγιση με έναν renderer PDF για να δημιουργήσετε PDF των μορφοποιημένων σελίδων.  
- Δοκιμάστε τη χρήση διαφορετικής headless μηχανής όπως Selenium WebDriver αν χρειάζεστε πλήρη πιστότητα περιηγητή.

Καλή προγραμματιστική!

## Τι πρέπει να μάθετε στη συνέχεια;

Οι παρακάτω οδηγίες καλύπτουν στενά σχετικές θεματικές που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικά παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Αποκτήστε Υπολογιζόμενο Στυλ Java – Εξαγωγή Χρώματος Φόντου από HTML](/html/english/java/css-html-form-editing/get-computed-style-java-extract-background-color-from-html/)
- [Πώς να φορτώσετε HTML, ορίσετε DPI Συσκευής & διαβάσετε το χρώμα φόντου](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Δημιουργία HTML από JavaScript σε Java – Πλήρης Οδηγός βήμα‑βήμα](/html/english/java/creating-managing-html-documents/generate-html-from-javascript-in-java-complete-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}