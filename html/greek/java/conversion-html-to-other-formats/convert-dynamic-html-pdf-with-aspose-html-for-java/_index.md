---
category: general
date: 2026-02-14
description: Μάθετε πώς να μετατρέψετε δυναμικό HTML σε PDF χρησιμοποιώντας το Aspose
  HTML for Java, να φορτώνετε HTML με σενάρια, να περιμένετε την εκτέλεση JavaScript
  και να κάνετε ερώτημα στις σειρές του πίνακα με selector σε μια ενιαία ροή εργασίας.
draft: false
keywords:
- convert dynamic html pdf
- load html with scripts
- wait for javascript execution
- query selector table rows
- aspose html pdf java
language: el
og_description: Οδηγός βήμα‑προς‑βήμα για τη μετατροπή δυναμικού HTML σε PDF, τη φόρτωση
  HTML με σενάρια, την αναμονή εκτέλεσης JavaScript και την ανάκτηση γραμμών πίνακα
  με χρήση του Aspose HTML PDF Java.
og_title: Μετατροπή δυναμικού HTML σε PDF με το Aspose HTML for Java
tags:
- Aspose
- Java
- HTML-to-PDF
title: Μετατροπή δυναμικού HTML σε PDF με το Aspose HTML για Java
url: /el/java/conversion-html-to-other-formats/convert-dynamic-html-pdf-with-aspose-html-for-java/
---

table, list.

Make sure to preserve code block placeholders unchanged.

Now craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή δυναμικού HTML σε PDF με Aspose HTML for Java

Ποτέ χρειάστηκε να **convert dynamic html pdf** αλλά η σελίδα που αντιμετωπίζετε βασίζεται σε JavaScript για να δημιουργήσει τους πίνακες, τα διαγράμματα ή τα μενού; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα το HTML που λαμβάνετε δεν είναι στατικό – τρέχουν σενάρια, εμφανίζονται κόμβοι DOM, και μόνο τότε η σελίδα φαίνεται όπως περιμένετε.  

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που **loads HTML with scripts**, **waits for javascript execution**, ελέγχει το τελικό DOM χρησιμοποιώντας **query selector table rows**, και τελικά **converts the dynamic HTML to PDF** με τη βιβλιοθήκη Aspose HTML for Java. Στο τέλος θα έχετε μια μοναδική κλάση Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle και να την εκτελέσετε αμέσως.

> **Γιατί να νοιαζόμαστε;**  
> Η μετατροπή μιας σελίδας πριν ολοκληρωθούν τα scripts της συχνά οδηγεί σε κενό PDF ή σε ελλιπές πίνακα. Η προσέγγιση που παρουσιάζεται εδώ εγγυάται ότι το PDF αντικατοπτρίζει ακριβώς ό,τι θα έδειχνε ένας χρήστης σε ένα πρόγραμμα περιήγησης.

## Τι θα χρειαστείτε

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK· το API λειτουργεί με Java 8+ αλλά τα νεότερα JDK προσφέρουν καλύτερη απόδοση)  
- **Aspose.HTML for Java** 23.10 (ή νεότερη) – μπορείτε να το κατεβάσετε από το Maven Central  
- Ένα **dynamic HTML file** (θα χρησιμοποιήσουμε το `dynamic.html` που περιέχει ένα script που δημιουργεί έναν πίνακα)  
- Βασική εξοικείωση με Java I/O και Maven/Gradle (δεν απαιτείται βαθιά εξειδίκευση)

Αν έχετε ήδη ένα Maven `pom.xml`, προσθέστε την εξάρτηση Aspose:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

## Βήμα 1: Φόρτωση HTML με ενεργοποιημένα Scripts

Το πρώτο πράγμα που πρέπει να κάνουμε είναι να πούμε στο Aspose ότι το HTML που πρόκειται να φορτώσουμε μπορεί να περιέχει JavaScript που πρέπει να εκτελεστεί. Αυτό γίνεται μέσω του `HTMLLoadOptions` – ορίστε τη σημαία **enableScripts** σε `true`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.nio.file.Paths;

/**
 * Demonstrates loading an HTML file that contains JavaScript.
 */
public class RunJsBeforeConversion {

    public static void main(String[] args) throws Exception {

        // --------------------------------------------------------------------
        // 1️⃣ Load the HTML document with JavaScript execution enabled
        // --------------------------------------------------------------------
        // The `true` argument tells Aspose to enable script execution.
        HTMLLoadOptions loadOptions = new HTMLLoadOptions(true);

        // Adjust the path to point at your own dynamic.html file.
        HTMLDocument htmlDocument = new HTMLDocument(
                Paths.get("YOUR_DIRECTORY/dynamic.html").toUri(),
                loadOptions);
```

> **Συμβουλή:** Κρατήστε το αρχείο HTML δίπλα στο φάκελο πηγών σας ή χρησιμοποιήστε απόλυτη διαδρομή· διαφορετικά η κλήση `toUri()` θα ρίξει `FileNotFoundException`.

## Βήμα 2: Αναμονή για την εκτέλεση JavaScript

Το Aspose εκτελεί scripts σε μια ελαφριά μηχανή, αλλά πρέπει να δώσετε στη σελίδα λίγο χρόνο για να ολοκληρωθεί. Σε ένα παραγωγικό σύστημα πιθανότατα θα συνδεθείτε σε ένα γεγονός DOM‑ready, αλλά για μια γρήγορη επίδειξη μια απλή παύση λειτουργεί καλά.

```java
        // --------------------------------------------------------------------
        // 2️⃣ Wait for JavaScript execution (simple pause for demo purposes)
        // --------------------------------------------------------------------
        // 2 seconds is usually enough for tiny demos; increase if your script
        // does heavy work or makes async network calls.
        Thread.sleep(2000);
```

> **Γιατί μια παύση;** Η βιβλιοθήκη εκτελεί scripts συγχρονισμένα, όμως ορισμένες λειτουργίες (όπως `setTimeout`) τοποθετούνται σε ουρά. Η αναμονή εξασφαλίζει ότι αυτές οι ουρές αδειάζουν πριν ελέγξουμε το DOM.

## Βήμα 3: Query Selector Table Rows – Επαλήθευση του DOM

Τώρα που τα scripts έχουν εκτελεστεί, μπορούμε να αντιμετωπίσουμε το έγγραφο όπως θα κάνατε στην κονσόλα του προγράμματος περιήγησης: χρησιμοποιούμε CSS selectors για να εντοπίσουμε στοιχεία. Εδώ εντοπίζουμε έναν πίνακα με `id="report"` και εκτυπώνουμε τον αριθμό των γραμμών που περιέχει.

```java
        // --------------------------------------------------------------------
        // 3️⃣ Inspect the DOM after script execution
        // --------------------------------------------------------------------
        // Using a CSS selector to find the table generated by JavaScript.
        Element reportTable = htmlDocument.querySelector("table#report");

        // Guard against a missing table – helpful when the script fails.
        if (reportTable == null) {
            System.out.println("⚠️ No table with id='report' found.");
            return;
        }

        // The Element API gives us direct access to rows collection.
        int rowCount = reportTable.getRows().getLength();
        System.out.println("Rows after script execution: " + rowCount);
```

Η τυπική έξοδος για το παράδειγμα `dynamic.html` φαίνεται ως εξής:

```
Rows after script execution: 5
```

Αν δείτε διαφορετικό αριθμό, ελέγξτε ξανά το script στο HTML σας – ίσως δημιουργεί γραμμές υπό όρους.

## Βήμα 4: Μετατροπή της τελικής κατάστασης του DOM σε PDF

Με το DOM επαληθευμένο, το τελευταίο βήμα είναι μια γραμμή κώδικα: περάστε το `HTMLDocument` στο `Converter.convert`. Το αποτέλεσμα είναι ένα PDF που αντικατοπτρίζει ακριβώς ό,τι θα έδειχνε ο περιηγητής μετά την ολοκλήρωση των scripts.

```java
        // --------------------------------------------------------------------
        // 4️⃣ Convert the final DOM state to a PDF file
        // --------------------------------------------------------------------
        Converter.convert(htmlDocument,
                Paths.get("YOUR_DIRECTORY/dynamic.pdf").toUri());

        System.out.println("✅ PDF generated at YOUR_DIRECTORY/dynamic.pdf");
    }
}
```

Ανοίξτε το `dynamic.pdf` με οποιονδήποτε προβολέα – θα πρέπει να δείτε τον πλήρως γεμάτο πίνακα, τα στυλ και τυχόν εικόνες που έδωσε το script.

## Πλήρες Παράδειγμα Λειτουργίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω βρίσκεται το πλήρες αρχείο πηγαίου κώδικα που μπορείτε να αντιγράψετε‑επικολλήσετε στο `src/main/java/RunJsBeforeConversion.java`. Θυμηθείτε να αντικαταστήσετε το `YOUR_DIRECTORY` με την πραγματική διαδρομή του φακέλου που περιέχει το `dynamic.html`.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.nio.file.Paths;

/**
 * End‑to‑end demo: load a dynamic HTML page, let its JavaScript run,
 * query the generated table, and convert the result to PDF.
 *
 * Requires Aspose.HTML for Java 23.10+ on the classpath.
 */
public class RunJsBeforeConversion {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load HTML with scripts enabled
        HTMLLoadOptions loadOptions = new HTMLLoadOptions(true);
        HTMLDocument htmlDocument = new HTMLDocument(
                Paths.get("YOUR_DIRECTORY/dynamic.html").toUri(),
                loadOptions);

        // 2️⃣ Wait for JavaScript execution (2 seconds)
        Thread.sleep(2000);

        // 3️⃣ Query selector table rows – verify script output
        Element reportTable = htmlDocument.querySelector("table#report");
        if (reportTable == null) {
            System.out.println("⚠️ No table with id='report' found.");
            return;
        }
        int rowCount = reportTable.getRows().getLength();
        System.out.println("Rows after script execution: " + rowCount);

        // 4️⃣ Convert the final DOM to PDF
        Converter.convert(htmlDocument,
                Paths.get("YOUR_DIRECTORY/dynamic.pdf").toUri());

        System.out.println("✅ PDF generated at YOUR_DIRECTORY/dynamic.pdf");
    }
}
```

Τρέξτε το με:

```bash
mvn compile exec:java -Dexec.mainClass=RunJsBeforeConversion
```

ή την αντίστοιχη εντολή Gradle.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενό PDF** | Τα scripts ήταν απενεργοποιημένα (`HTMLLoadOptions(false)`) ή η αναμονή ήταν πολύ σύντομη. | Ορίστε `true` για τα scripts και αυξήστε το `Thread.sleep` αν η σελίδα σας χρησιμοποιεί ασύγχρονες κλήσεις. |
| **`reportTable` is null** | Ο selector είναι λανθασμένος ή το script δεν δημιούργησε ποτέ το στοιχείο. | Επαληθεύστε ότι το `<script>` του HTML προσθέτει πραγματικά το `<table id="report">`. Χρησιμοποιήστε το Chrome DevTools για να ελέγξετε το τελικό DOM. |
| **Missing fonts or CSS** | Το HTML αναφέρεται σε εξωτερικά φύλλα στυλ που δεν είναι προσβάσιμα. | Παρέχετε απόλυτες URLs ή αντιγράψτε τα αρχεία CSS τοπικά και αναφερθείτε σε αυτά με διαδρομές `file://`. |
| **Large pages cause memory spikes** | Το Aspose φορτώνει ολόκληρο το DOM στη μνήμη. | Χρησιμοποιήστε `HTMLLoadOptions.setMaxMemoryUsage` για να περιορίσετε την κατανάλωση, ή χωρίστε τη μετατροπή σε τμήματα. |

## Επέκταση της Λύσης

- **Multiple Pages** – Εάν η δυναμική σας σελίδα χρησιμοποιεί σελιδοποίηση, καλέστε το `Converter.convert` μέσα σε βρόχο μετά την ενημέρωση του τμήματος URL (`#page=2`, κλπ.).  
- **Headless Browser Alternative** – Για εξαιρετικά πολύπλοκα scripts (π.χ., WebGL), σκεφτείτε την ενσωμάτωση ενός πραγματικού headless browser όπως το **Playwright** και τη μεταφορά του αποδομένου HTML στο Aspose.  
- **Custom Rendering Options** – Το `PdfSaveOptions` σας επιτρέπει να ορίσετε το μέγεθος σελίδας, τα περιθώρια και την ποιότητα εικόνας. Παράδειγμα: `new PdfSaveOptions(PdfPageSize.A4, PdfPageOrientation.Portrait)`.

## Συμπέρασμα

Μόλις σας δείξαμε πώς να **convert dynamic html pdf** αξιόπιστα με **loading html with scripts**, δίνοντας στη σελίδα λίγο χρόνο για **wait for javascript execution**, ελέγχοντας το αποτέλεσμα με **query selector table rows**, και τελικά χρησιμοποιώντας **aspose html pdf java** για να παραγάγετε ένα επαγγελματικό PDF.  

Το μοτίβο κλιμακώνεται: αντικαταστήστε το selector, προσαρμόστε τη λογική αναμονής, και μπορείτε να διαχειριστείτε οποιοδήποτε δυναμικό περιεχόμενο – από διαγράμματα που δημιουργούνται από το Chart.js μέχρι πίνακες που γεμίζουν μέσω AJAX.  

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να μετατρέψετε μια σελίδα που αντλεί δεδομένα από ένα REST endpoint, ή πειραματιστείτε με την ενσωμάτωση προσαρμοσμένων γραμματοσειρών ώστε να ταιριάζουν με το στυλ της μάρκας σας.  

Αν αντιμετωπίσατε κάποιο πρόβλημα ή έχετε ιδέες για βελτιώσεις, αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική δουλειά και απολαύστε τα τέλεια αποδομένα PDFs!  

---  

![παράδειγμα μετατροπής δυναμικού html pdf](/images/convert-dynamic-html-pdf.png "Στιγμιότυπο που δείχνει ένα PDF που δημιουργήθηκε από δυναμικό HTML χρησιμοποιώντας Aspose HTML for Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}