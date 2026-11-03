---
category: general
date: 2026-10-14
description: Μάθετε πώς να μετατρέψετε HTML σε PDF με προσαρμοσμένο μέγεθος σελίδας
  PDF σε Java χρησιμοποιώντας το Aspose.HTML. Αυτός ο οδηγός καλύπτει το html to pdf
  java conversion, την αποθήκευση αρχείων και τις κοινές παγίδες.
draft: false
keywords:
- custom pdf page size
- html to pdf java
- generate pdf from html
- save pdf file java
- html pdf example java
lastmod: 2026-10-14
og_description: Μάθετε πώς να μετατρέψετε HTML σε PDF με προσαρμοσμένο μέγεθος σελίδας
  PDF σε Java χρησιμοποιώντας το Aspose.HTML. Αυτός ο οδηγός καλύπτει το html to pdf
  java conversion, την αποθήκευση αρχείων και τις κοινές παγίδες.
og_image_alt: Tutorial showing how to convert HTML to PDF with custom page size in
  Java using Aspise.HTML
og_title: Πώς να μετατρέψετε HTML σε PDF με προσαρμοσμένο μέγεθος σελίδας PDF σε Java
schemas:
- author: Aspose
  dateModified: '2026-10-14'
  description: Learn how to convert HTML to PDF with custom pdf page size in Java
    using Aspose.HTML. This guide covers html to pdf java conversion, saving files,
    and common pitfalls.
  headline: How to convert HTML to PDF with custom pdf page size in Java
  type: TechArticle
- description: Learn how to convert HTML to PDF with custom pdf page size in Java
    using Aspose.HTML. This guide covers html to pdf java conversion, saving files,
    and common pitfalls.
  name: How to convert HTML to PDF with custom pdf page size in Java
  steps:
  - name: '**Batch conversion** – loop over a directory of HTML files and produce
      a PDF per file.'
    text: '**Batch conversion** – loop over a directory of HTML files and produce
      a PDF per file.'
  - name: '**Merging PDFs** – use Aspose.PDF to combine the generated PDFs into a
      single document.'
    text: '**Merging PDFs** – use Aspose.PDF to combine the generated PDFs into a
      single document.'
  - name: '**Adding headers/footers** – customize the PDF output with page numbers
      or watermarks.'
    text: '**Adding headers/footers** – customize the PDF output with page numbers
      or watermarks.'
  - name: '**Streaming conversion** – convert HTML from an `InputStream` directly
      to an `OutputStream` for web services.'
    text: '**Streaming conversion** – convert HTML from an `InputStream` directly
      to an `OutputStream` for web services.'
  type: HowTo
- questions:
  - answer: Yes, the same API works in servlet containers or Spring Boot services;
      just stream the output to the HTTP response.
    question: Can I use this approach in a web application?
  - answer: It supports over 95 % of HTML5 elements and most CSS3 properties, including
      flexbox and grid layouts.
    question: Does Aspose.HTML support HTML5 and modern CSS?
  - answer: Use `Converter.convert` with a `PdfDevice` that enables incremental saving;
      this keeps memory usage low.
    question: How do I handle very large HTML files?
  - answer: A valid Aspose.HTML license removes the evaluation watermark and unlocks
      full performance optimizations.
    question: Is a license required for production use?
  - answer: Yes, pass the remote URL as the source `URI` to `Converter.convert`; the
      library fetches the content automatically.
    question: Can I convert directly from a URL without downloading the file first?
  type: FAQPage
tags:
- custom pdf page size
- HTML to PDF
- Aspose.HTML
- Java conversion
- pdf generation
title: Πώς να μετατρέψετε HTML σε PDF με προσαρμοσμένο μέγεθος σελίδας PDF σε Java
url: /el/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να μετατρέψετε HTML σε PDF με προσαρμοσμένο μέγεθος σελίδας PDF σε Java

Κάποτε χρειάστηκε να **μετατρέψετε HTML σε PDF με προσαρμοσμένο μέγεθος σελίδας PDF** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας δώσει ένα καθαρό, έτοιμο για εκτύπωση αποτέλεσμα; Δεν είστε μόνοι. Πολλοί προγραμματιστές Java κοιτάζουν μια σελίδα που αποδίδεται από το πρόγραμμα περιήγησης και αναρωτιούνται πώς να μετατρέψουν αυτό το markup σε ένα φορητό έγγραφο χωρίς να χάσουν το στυλ CSS.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από ένα **πλήρες, εκτελέσιμο παράδειγμα** που παίρνει ένα αρχείο `input.html`, καλεί το Aspose.HTML for Java και **αποθηκεύει το PDF σε αρχείο** με μία μόνο γραμμή κώδικα. Στο τέλος θα ξέρετε πώς να **δημιουργήσετε PDF από HTML**, να διαχειριστείτε ελλιπή αρχεία και να προσαρμόσετε τη μετατροπή εάν χρειάζεστε προσαρμοσμένα μεγέθη σελίδας.

## Γρήγορες απαντήσεις
- **Μπορώ να ορίσω προσαρμοσμένο μέγεθος σελίδας;** Ναι – χρησιμοποιήστε τις επιλογές `PdfDevice` όταν καλείτε το `Converter.convert`.
- **Ποια βιβλιοθήκη είναι η καλύτερη για html to pdf java;** Το Aspose.HTML for Java προσφέρει την πιο πλήρη υποστήριξη CSS.
- **Χρειάζεται να εγκαταστήσω πρόγραμμα περιήγησης;** Όχι, η μετατροπή εκτελείται εξ ολοκλήρου στο περιβάλλον Java.
- **Πώς αποθηκεύω το αρχείο PDF;** Παρέχετε ένα στόχο `URI` στο `Converter.convert` και το αρχείο γράφεται αυτόματα.
- **Απαιτείται άδεια για παραγωγική χρήση;** Ναι, μια έγκυρη άδεια Aspose.HTML αφαιρεί το υδατογράφημα αξιολόγησης.

## Τι θα χρειαστείτε

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK· το API είναι συμβατό με Java 8+)
- **Aspose.HTML for Java** JARs – μπορείτε να τα κατεβάσετε από το Maven Central ή την ιστοσελίδα Aspose.
- Ένα απλό αρχείο `input.html` τοποθετημένο κάπου στο δίσκο.
- Το αγαπημένο σας IDE ή έναν απλό κειμενογράφο – δεν έχει σημασία, ο κώδικας είναι απλός.

> **Pro tip:** Εάν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση που φαίνεται στην ενότητα *Prerequisites*· διαφορετικά τοποθετήστε τα JARs στο φάκελο `libs/` και προσθέστε τα στο classpath.

## Προαπαιτούμενα – προσθήκη aspose.html στο έργο σας

Αν διαχειρίζεστε εξαρτήσεις με Maven, επικολλήστε αυτό το απόσπασμα στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Για Gradle:

```groovy
implementation 'com.aspose:aspose-html:24.10'
```

Αν προτιμάτε τη χειροκίνητη προσέγγιση, κατεβάστε το JAR από τη σελίδα λήψης του Aspose και προσθέστε το στο classpath:

```bash
javac -cp "libs/*" ConvertHtmlToPdfTutorial.java
java  -cp ".:libs/*" ConvertHtmlToPdfTutorial
```

Τώρα που η βιβλιοθήκη είναι έτοιμη, ας προχωρήσουμε στα πραγματικά βήματα μετατροπής.

## Βήμα 1 – εντοπισμός του πηγαίου αρχείου html

Το πρώτο που χρειάζεστε είναι ένα **URI** που δείχνει στο HTML που θέλετε να μετατρέψετε. Ένα URI (Uniform Resource Identifier) προσδιορίζει τη θέση ενός πόρου. Η χρήση του `java.nio.file.Paths` κάνει τον κώδικα ανεξάρτητο από το λειτουργικό σύστημα και αποφεύγει σκληρά κωδικοποιημένους διαχωριστές.

```java
// Step 1: Locate the source HTML file
URI sourceHtml = Paths.get("YOUR_DIRECTORY/input.html").toUri();
```

> **Γιατί είναι σημαντικό:** Με τη μετατροπή της διαδρομής σε `URI`, ο Aspose `Converter` μπορεί να δεχτεί τόσο τοπικά αρχεία όσο και απομακρυσμένα URLs (π.χ., `http://example.com/page.html`). Αυτή η ευελιξία είναι χρήσιμη όταν αργότερα αλλάξετε σε πηγή web‑service.

## Βήμα 2 – ορισμός του σημείου αποθήκευσης του pdf

Το ίδιο σημαντικό όσο η ανάγνωση του HTML είναι να πείτε στον μετατροπέα **πού να γράψει το αποτέλεσμα**. Και πάλι χρησιμοποιούμε ένα `URI` για συνέπεια. Ένα URI (Uniform Resource Identifier) προσδιορίζει τη θέση ενός πόρου.

```java
// Step 2: Define the target PDF file location
URI targetPdf = Paths.get("YOUR_DIRECTORY/output.pdf").toUri();
```

> **Edge case:** Εάν ο φάκελος προορισμού δεν υπάρχει, το `Converter.convert` θα ρίξει εξαίρεση. Μπορείτε να δημιουργήσετε τον φάκελο εκ των προτέρων με `Files.createDirectories(Paths.get("YOUR_DIRECTORY"))`.

## Βήμα 3 – εκτέλεση της μετατροπής με μία κλήση

Η κλάση `Converter` εκτελεί τη μετατροπή HTML‑σε‑PDF. Η `Converter` είναι η κεντρική κλάση του Aspose.HTML που μετατρέπει το περιεχόμενο HTML σε διάφορες μορφές εξόδου, συμπεριλαμβανομένου του PDF.

```java
// Step 3: Convert the HTML document to PDF in a single call
Converter.convert(sourceHtml, targetPdf);
```

Αυτό είναι όλο—χωρίς να παίζετε με ρυθμίσεις σελίδας εκτός αν το θέλετε. Το προεπιλεγμένο μέγεθος σελίδας είναι A4 και η μετατροπή σέβεται τις περισσότερες σύγχρονες ιδιότητες CSS.

## Πώς να ορίσετε προσαρμοσμένο μέγεθος σελίδας pdf κατά τη μετατροπή HTML σε PDF σε Java;

Παρέχετε ένα `PdfDevice` με τις επιθυμητές διαστάσεις και περάστε το στο `Converter.convert`. Ένα `PdfDevice` αντιπροσωπεύει τις ρυθμίσεις εξόδου PDF όπως το μέγεθος σελίδας και ο προσανατολισμός. Για παράδειγμα, ορίστε μια σελίδα 6 × 9 ίντσες σε πορτραίτο και στη συνέχεια καλέστε τη μέθοδο μετατροπής. Αυτή η προσέγγιση σας επιτρέπει να ελέγξετε ακριβώς το μέγεθος εξόδου χωρίς μεταγενέστερη επεξεργασία του PDF. Η βιβλιοθήκη θα προσαρμόσει αυτόματα τη διάταξη ώστε να ταιριάζει στις νέες διαστάσεις σελίδας.

## Πλήρες λειτουργικό παράδειγμα

Η κλάση `ConvertHtmlToPdfTutorial` περιέχει τη μέθοδο `main` που εκτελεί τη μετατροπή.

```java
import com.aspose.html.converters.Converter;
import java.nio.file.Paths;
import java.net.URI;
import java.nio.file.Files;
import java.nio.file.Path;

public class ConvertHtmlToPdfTutorial {
    public static void main(String[] args) throws Exception {

        // ----- Step 1: Locate the source HTML file -----
        // Replace YOUR_DIRECTORY with the absolute or relative path where input.html lives.
        URI sourceHtml = Paths.get("YOUR_DIRECTORY/input.html").toUri();

        // ----- Step 2: Define the target PDF file location -----
        // Ensure the output folder exists; otherwise create it.
        Path outputDir = Paths.get("YOUR_DIRECTORY");
        if (!Files.exists(outputDir)) {
            Files.createDirectories(outputDir);
        }
        URI targetPdf = outputDir.resolve("output.pdf").toUri();

        // ----- Step 3: Convert HTML to PDF -----
        // This single line does the whole job: reading HTML, applying CSS, and writing PDF.
        Converter.convert(sourceHtml, targetPdf);

        System.out.println("✅ PDF successfully generated at: " + targetPdf);
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση θα βρείτε το `output.pdf` στον ίδιο φάκελο με το `input.html`. Ανοίξτε το με οποιονδήποτε προβολέα PDF—το HTML σας θα πρέπει να φαίνεται ακριβώς όπως θα το έδειχνε ένας περιηγητής, με γραμματοσειρές, εικόνες και στυλ.

## Διαχείριση κοινών προβλημάτων

### 1. Σφάλματα αρχείου‑δεν‑βρέθηκε

Το `FileNotFoundException` ρίχνεται όταν το καθορισμένο αρχείο δεν μπορεί να εντοπιστεί. Εάν λείπει το `input.html`, το `Converter.convert` ρίχνει ένα `java.io.FileNotFoundException`. Τυλίξτε την κλήση σε μπλοκ try‑catch για φιλικό μήνυμα:

```java
try {
    Converter.convert(sourceHtml, targetPdf);
} catch (Exception e) {
    System.err.println("❌ Conversion failed: " + e.getMessage());
}
```

### 2. Εξωτερικοί πόροι (εικόνες, css) δεν φορτώνονται

Το Aspose.HTML επιλύει σχετικές URL βάσει της θέσης του αρχείου HTML. Εάν το HTML σας αναφέρει πόρους σε διαφορετικό φάκελο, βεβαιωθείτε ότι οι διαδρομές είναι σωστές ή παρέχετε απόλυτη URL. Εναλλακτικά, ορίστε ένα **base URI** πριν από τη μετατροπή:

```java
Converter.convert(sourceHtml, targetPdf, new ConverterOptions()
        .setBaseUri(Paths.get("YOUR_DIRECTORY/assets/").toUri()));
```

### 3. Προσαρμοσμένο μέγεθος σελίδας ή προσανατολισμός

Το προεπιλεγμένο είναι A4 πορτραίτο. Για να δημιουργήσετε PDF σε τοπίο ή προσαρμοσμένο μέγεθος, περάστε ένα `PdfDevice` με τις επιθυμητές επιλογές:

```java
PdfDevice device = new PdfDevice(targetPdf);
device.setPageSize(PdfPageSize.LETTER);
device.setLandscape(true);
Converter.convert(sourceHtml, device);
```

### 4. Άδεια

Οι βιβλιοθήκες Aspose λειτουργούν σε λειτουργία αξιολόγησης για 30 ημέρες, προσθέτοντας υδατογράφημα στο PDF. Για **αφαίρεση του υδατογραφήματος**, εφαρμόστε το αρχείο άδειας πριν από τη μετατροπή:

```java
com.aspose.html.License license = new com.aspose.html.License();
license.setLicense("Aspose.Total.Java.lic");
```

## Γιατί να επιλέξετε aspose.html για java;

Το Aspose.HTML for Java παρέχει ολοκληρωμένη υποστήριξη CSS, λειτουργεί χωρίς εξωτερικά προγράμματα περιήγησης και προσφέρει υψηλή απόδοση για μαζικές μετατροπές. Απεικονίζει με ακρίβεια σύγχρονες διατάξεις, συμπεριλαμβανομένων των flexbox και grid, και μπορεί να επεξεργαστεί μεγάλα έγγραφα γρήγορα διατηρώντας χαμηλή χρήση μνήμης. Αυτά τα χαρακτηριστικά το καθιστούν ιδανικό για εφαρμογές SaaS που δημιουργούν τιμολόγια, αναφορές ή e‑books κατ' απαίτηση.

## Σύντομη ανακεφαλαίωση

- **Κύριος στόχος:** *μετατροπή html σε pdf* με μία σύντομη κλήση API, εφαρμόζοντας προαιρετικά προσαρμοσμένο μέγεθος σελίδας pdf.
- Μάθατε πώς να **δημιουργήσετε pdf από html**, **αποθηκεύσετε pdf σε αρχείο**, και να προσαρμόσετε τη διαδικασία για προσαρμοσμένα μεγέθη σελίδας.
- Το tutorial κάλυψε τις λεπτομέρειες του **pdf from html java**, τη διαχείριση ελλιπών αρχείων, εξωτερικών πόρων και άδειας.
- Διαθέτετε τώρα ένα **πλήρες, εκτελέσιμο παράδειγμα** που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.

## Επόμενα βήματα & συναφή θέματα

1. **Μαζική μετατροπή** – επανάληψη σε φάκελο HTML αρχείων και παραγωγή PDF ανά αρχείο.
2. **Συγχώνευση PDF** – χρήση Aspose.PDF για συνένωση των παραγόμενων PDF σε ένα ενιαίο έγγραφο.
3. **Προσθήκη κεφαλίδων/υποσέλιδων** – προσαρμογή της εξόδου PDF με αριθμούς σελίδων ή υδατογραφήματα.
4. **Μετατροπή σε ροή** – μετατροπή HTML από `InputStream` απευθείας σε `OutputStream` για web services.

Νιώστε ελεύθεροι να πειραματιστείτε: δοκιμάστε διαφορετικά θέματα CSS, ενσωματώστε γραμματοσειρές ή δημιουργήστε PDF από μια συμβολοσειρά HTML που δημιουργείται κατά το χρόνο εκτέλεσης. Οι δυνατότητες είναι ατελείωτες, και τώρα έχετε τη βάση για να τις εξερευνήσετε.

---

## Συχνές ερωτήσεις

**Ε: Μπορώ να χρησιμοποιήσω αυτήν την προσέγγιση σε εφαρμογή web;**  
Α: Ναι, το ίδιο API λειτουργεί σε servlet containers ή υπηρεσίες Spring Boot· απλώς ρέξτε το αποτέλεσμα στην HTTP απάντηση.

**Ε: Υποστηρίζει το Aspose.HTML HTML5 και σύγχρονα CSS;**  
Α: Υποστηρίζει πάνω από 95 % των στοιχείων HTML5 και τις περισσότερες ιδιότητες CSS3, συμπεριλαμβανομένων των flexbox και grid διατάξεων.

**Ε: Πώς διαχειρίζομαι πολύ μεγάλα αρχεία HTML;**  
Α: Χρησιμοποιήστε το `Converter.convert` με `PdfDevice` που ενεργοποιεί την σταδιακή αποθήκευση· αυτό μειώνει τη χρήση μνήμης.

**Ε: Απαιτείται άδεια για παραγωγική χρήση;**  
Α: Μια έγκυρη άδεια Aspose.HTML αφαιρεί το υδατογράφημα αξιολόγησης και ξεκλειδώνει τις πλήρεις βελτιστοποιήσεις απόδοσης.

**Ε: Μπορώ να μετατρέψω απευθείας από URL χωρίς να κατεβάσω το αρχείο πρώτα;**  
Α: Ναι, περάστε το απομακρυσμένο URL ως πηγή `URI` στο `Converter.convert`; η βιβλιοθήκη θα φέρει το περιεχόμενο αυτόματα.

---

**Τελευταία ενημέρωση:** 2026-10-14  
**Δοκιμή με:** Aspose.HTML for Java 24.10  
**Συγγραφέας:** Aspose

## Σχετικά Tutorials

- [Convert HTML to PDF Java – Configuring Environment in Aspose.HTML](/html/java/configuring-environment/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/java/advanced-usage/css-extensions-adding-title-page-number/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}