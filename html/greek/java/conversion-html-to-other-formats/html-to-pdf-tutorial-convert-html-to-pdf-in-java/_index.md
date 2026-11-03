---
category: general
date: 2026-06-19
description: Μάθετε πώς να δημιουργείτε PDF από HTML χρησιμοποιώντας ένα απλό παράδειγμα
  Java. Αυτό το σεμινάριο HTML σε PDF σας δείχνει πώς να μετατρέψετε ένα αρχείο HTML
  σε PDF με το OpenHTMLtoPDF.
draft: false
keywords:
- html to pdf tutorial
- generate pdf from html
- convert html file pdf
- create pdf from html
- convert webpage to pdf
language: el
og_description: Το tutorial html σε pdf σας δείχνει πώς να δημιουργήσετε PDF από HTML
  χρησιμοποιώντας Java. Ακολουθήστε τα βήματα για να μετατρέψετε γρήγορα το αρχείο
  HTML σε PDF.
og_title: 'Μάθημα HTML σε PDF: Οδηγός μετατροπής Java'
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  headline: 'html to pdf tutorial: Convert HTML to PDF in Java'
  type: TechArticle
- description: Learn how to generate pdf from html using a simple Java example. This
    html to pdf tutorial shows you how to convert html file pdf with OpenHTMLtoPDF.
  name: 'html to pdf tutorial: Convert HTML to PDF in Java'
  steps:
  - name: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
    text: '**Resource flexibility** – the method first checks if the supplied path
      points to a real file; if not, it falls back to a classpath resource. That means
      you can **convert webpage to pdf** later by feeding a URL string (just replace
      the `withHtmlContent` call with `withUri`).'
  - name: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
    text: '**Automatic directory creation** – `Files.createDirectories` guarantees
      the `target/` folder exists, so you won’t get a “No such file or directory”
      error.'
  - name: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
    text: '**Single‑line conversion** – `PdfRendererBuilder` handles CSS, fonts, and
      page layout internally. No need to manually manage PDF pages; the library does
      it for you, keeping the example short and focused on the **convert html file
      pdf** concept.'
  type: HowTo
tags:
- Java
- PDF
- HTML conversion
title: 'Οδηγός HTML σε PDF: Μετατροπή HTML σε PDF με Java'
url: /el/java/conversion-html-to-other-formats/html-to-pdf-tutorial-convert-html-to-pdf-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to pdf tutorial – Μετατρέψτε μια σελίδα HTML σε PDF με Java

Έχετε αναρωτηθεί ποτέ πώς να μετατρέψετε μια στατική σελίδα HTML σε ένα κομψό έγγραφο PDF χωρίς να αφήσετε το IDE σας; Δεν είστε μόνοι. Σε αυτόν τον **html to pdf tutorial** θα περάσουμε από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα Java που **generate pdf from html** σε λίγα μόνο λεπτά.

Θα καλύψουμε όλα όσα χρειάζεστε—τη ρύθμιση του έργου, την προσθήκη της σωστής βιβλιοθήκης, τη συγγραφή του κώδικα μετατροπής, και ακόμη μια γρήγορη συμβουλή για τη μετατροπή μιας ζωντανής ιστοσελίδας σε PDF. Στο τέλος θα μπορείτε να **convert html file pdf** στον δικό σας υπολογιστή, και θα καταλάβετε πώς να **create pdf from html** για οποιοδήποτε μελλοντικό έργο.

## Τι θα χρειαστείτε

- Java 17 ή νεότερο (ο κώδικας λειτουργεί με οποιοδήποτε πρόσφατο JDK)
- Maven ή Gradle (θα δείξουμε το απόσπασμα Maven)
- Ένα μικρό αρχείο HTML που θέλετε να μετατρέψετε σε PDF (θα δημιουργήσουμε ένα επί τόπου)
- Ένα IDE ή ένας απλός επεξεργαστής κειμένου—όπως προτιμάτε

Αυτό είναι όλο. Χωρίς βαριές εξυπηρετητές, χωρίς πληρωμένα SDK, μόνο καθαρή Java και μια δωρεάν ανοιχτού κώδικα βιβλιοθήκη.

## Βήμα 1: html to pdf tutorial – Ρύθμιση έργου Maven

Πρώτα απ' όλα. Δημιουργήστε ένα νέο έργο Maven (ή προσθέστε σε ένα υπάρχον). Η μόνη εξάρτηση που πραγματικά χρειάζεστε είναι **OpenHTMLtoPDF**, η οποία κάνει το βαρέως έργο της απόδοσης HTML και CSS σε PDF.

```xml
<!-- pom.xml snippet -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>html-to-pdf-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- OpenHTMLtoPDF core -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-pdfbox</artifactId>
            <version>1.0.10</version>
        </dependency>
        <!-- Optional: support for SVG, if your HTML uses it -->
        <dependency>
            <groupId>com.openhtmltopdf</groupId>
            <artifactId>openhtmltopdf-svg-support</artifactId>
            <version>1.0.10</version>
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Αν χρησιμοποιείτε Gradle, οι ίδιες εξαρτήσεις μπορούν να προστεθούν κάτω από `implementation` στο `build.gradle`.  

Γιατί αυτό το βήμα είναι σημαντικό: χωρίς τη βιβλιοθήκη η JVM δεν ξέρει πώς να μεταφράσει τις ετικέτες HTML σε εντολές σχεδίασης PDF. Το OpenHTMLtoPDF είναι ελαφρύ, ενεργά συντηρούμενο και λειτουργεί με CSS‑2.1, έτσι το στυλ σας παραμένει αμετάβλητο.

## Βήμα 2: generate pdf from html – Προετοιμασία δείγματος αρχείου HTML

Ας δημιουργήσουμε ένα μικρό `input.html` ακριβώς δίπλα στον κώδικα Java. Αυτό κρατά το παράδειγμα αυτό‑με‑αυτό και δείχνει τη ροή εργασίας **create pdf from html**.

```html
<!-- src/main/resources/input.html -->
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Sample Report</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        h1 { color: #2E86C1; }
        p { line-height: 1.5; }
    </style>
</head>
<body>
    <h1>Monthly Sales Report</h1>
    <p>This PDF was generated directly from an HTML file using Java.</p>
    <p>All you need is a few lines of code.</p>
</body>
</html>
```

Μπορείτε να αντικαταστήσετε το περιεχόμενο με οτιδήποτε—πίνακες, εικόνες, ακόμη και JavaScript (αν και ο renderer αγνοεί τα scripts). Το σημαντικό είναι το αρχείο να βρίσκεται στο classpath ώστε ο μετατροπέας να το εντοπίσει.

## Βήμα 3: convert html file pdf – Γράψτε το βοηθητικό πρόγραμμα μετατροπής

Τώρα η καρδιά του **html to pdf tutorial**: μια μικρή κλάση `HtmlToPdfConverter` που διαβάζει το HTML και γράφει ένα PDF. Ο παρακάτω κώδικας είναι ένα πλήρες, εκτελέσιμο παράδειγμα· αντιγράψτε‑και‑επικολλήστε το στο `src/main/java/com/example/HtmlToPdfConverter.java`.

```java
package com.example;

import com.openhtmltopdf.pdfboxout.PdfRendererBuilder;
import java.io.*;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardCopyOption;

/**
 * Simple utility that converts an HTML file to PDF.
 * It demonstrates the "convert html file pdf" use‑case.
 */
public class HtmlToPdfConverter {

    /**
     * Converts the given HTML file to a PDF file.
     *
     * @param htmlPath path to the source HTML file (can be absolute or classpath)
     * @param pdfPath  destination path for the generated PDF
     * @throws IOException if reading or writing fails
     */
    public static void convert(String htmlPath, String pdfPath) throws IOException {
        // Resolve the HTML file – support both absolute paths and classpath resources
        InputStream htmlStream = Files.exists(Path.of(htmlPath))
                ? Files.newInputStream(Path.of(htmlPath))
                : HtmlToPdfConverter.class.getResourceAsStream(htmlPath);

        if (htmlStream == null) {
            throw new FileNotFoundException("HTML source not found: " + htmlPath);
        }

        // Ensure the output directory exists
        Path pdfFile = Path.of(pdfPath);
        Files.createDirectories(pdfFile.getParent());

        try (OutputStream os = Files.newOutputStream(pdfFile);
             InputStream is = htmlStream) {

            // Builder does the heavy lifting – it parses HTML + CSS and writes PDF bytes
            new PdfRendererBuilder()
                    .withHtmlContent(new String(is.readAllBytes()), null) // base URI null = no external resources
                    .toStream(os)
                    .run();
        }
    }

    // Demo entry point – feel free to run this class directly
    public static void main(String[] args) {
        // Step 1: Specify the input HTML file location
        String htmlPath = "src/main/resources/input.html";

        // Step 2: Specify the desired output PDF file location
        String pdfPath = "target/output.pdf";

        // Step 3: Convert the HTML document to PDF using default conversion settings
        try {
            convert(htmlPath, pdfPath);
            System.out.println("✅ PDF successfully created at " + pdfPath);
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Γιατί αυτός ο κώδικας λειτουργεί

1. **Resource flexibility** – η μέθοδος πρώτα ελέγχει αν η παρεχόμενη διαδρομή δείχνει σε πραγματικό αρχείο· αν όχι, επιστρέφει σε πόρο του classpath. Αυτό σημαίνει ότι μπορείτε να **convert webpage to pdf** αργότερα παρέχοντας μια διεύθυνση URL (απλώς αντικαταστήστε την κλήση `withHtmlContent` με `withUri`).

2. **Automatic directory creation** – η `Files.createDirectories` εγγυάται ότι ο φάκελος `target/` υπάρχει, ώστε να μην λάβετε σφάλμα “No such file or directory”.

3. **Single‑line conversion** – η `PdfRendererBuilder` διαχειρίζεται εσωτερικά CSS, γραμματοσειρές και διάταξη σελίδας. Δεν χρειάζεται να διαχειριστείτε χειροκίνητα τις σελίδες PDF· η βιβλιοθήκη το κάνει για εσάς, κρατώντας το παράδειγμα σύντομο και εστιασμένο στην έννοια **convert html file pdf**.

## Βήμα 4: create pdf from html – Εκτελέστε το πρόγραμμα και επαληθεύστε

Ανοίξτε ένα τερματικό στη ρίζα του έργου και εκτελέστε:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HtmlToPdfConverter
```

Αν όλα έχουν ρυθμιστεί σωστά, θα δείτε:

```
✅ PDF successfully created at target/output.pdf
```

Ανοίξτε το `target/output.pdf` με οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε την μορφοποιημένη κεφαλίδα “Monthly Sales Report”, το κείμενο παραγράφου, και τα ίδια περιθώρια που ορίσατε στο μπλοκ `<style>` του HTML.

> **What if you don’t see the styling?**  
> Βεβαιωθείτε ότι το CSS είναι ενσωματωμένο ή βρίσκεται στον ίδιο φάκελο με το HTML. Το OpenHTMLtoPDF επιλύει σχετικές URL βάσει του base URI που περνάτε στο `withHtmlContent`. Στο παραπάνω απόσπασμα περάσαμε `null`, το οποίο λειτουργεί για απλό ενσωματωμένο CSS. Για εξωτερικά φύλλα στυλ, δώστε τη διαδρομή του καταλόγου ως δεύτερο όρισμα.

## Βήμα 5: convert webpage to pdf – Διαχείριση απομακρυσμένων URL (προαιρετικό)

Μερικές φορές χρειάζεται να **convert webpage to pdf** απευθείας από το διαδίκτυο—σκεφτείτε την αρχειοθέτηση μιας online απόδειξης. Η βιβλιοθήκη υποστηρίζει αυτό μέσω `withUri`. Εδώ είναι μια γρήγορη προσαρμογή:

```java
public static void convertUrl(String url, String pdfPath) throws IOException {
    Path pdfFile = Path.of(pdfPath);
    Files.createDirectories(pdfFile.getParent());

    try (OutputStream os = Files.newOutputStream(pdfFile)) {
        new PdfRendererBuilder()
                .withUri(url)          // Load HTML from the web
                .toStream(os)
                .run();
    }
}
```

Call it like:



## Τι Θα Πρέπει Να Μάθετε Στη Σειρά;

Τα παρακάτω tutorials καλύπτουν στενά σχετικές θεματικές που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να Μετατρέψετε HTML σε PDF με Java – Χρησιμοποιώντας Aspose.HTML για Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Μετατροπή HTML σε PDF Java – Ρύθμιση Περιβάλλοντος στο Aspose.HTML](/html/english/java/configuring-environment/)
- [Μετατροπή HTML σε PDF σε Java – Οδηγός Βήμα‑Βήμα με Ρυθμίσεις Μεγέθους Σελίδας](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-step-by-step-guide-with-page-siz/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}