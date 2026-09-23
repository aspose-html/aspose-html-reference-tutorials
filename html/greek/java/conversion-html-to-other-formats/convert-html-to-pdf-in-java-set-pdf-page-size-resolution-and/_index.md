---
category: general
date: 2026-01-06
description: Μετατρέψτε HTML σε PDF σε Java με προσαρμοσμένο μέγεθος σελίδας, περιθώρια
  και ανάλυση. Μάθετε πώς να ορίζετε το μέγεθος της σελίδας PDF και να αποθηκεύετε
  HTML ως PDF χρησιμοποιώντας το Aspose.HTML.
draft: false
keywords:
- convert html to pdf
- set pdf page size
- save html as pdf
- set pdf resolution
- html to pdf java
language: el
og_description: Μετατρέψτε το HTML σε PDF στη Java γρήγορα. Αυτός ο οδηγός δείχνει
  πώς να ορίσετε το μέγεθος σελίδας PDF, να ρυθμίσετε την ανάλυση και να αποθηκεύσετε
  το HTML ως PDF με το Aspose.HTML.
og_title: Μετατροπή HTML σε PDF με Java – Ορισμός μεγέθους σελίδας PDF & ανάλυσης
tags:
- Java
- PDF
- Aspose.HTML
title: Μετατροπή HTML σε PDF σε Java – Ορισμός μεγέθους σελίδας PDF, ανάλυσης και
  αποθήκευση HTML ως PDF
url: /el/java/conversion-html-to-other-formats/convert-html-to-pdf-in-java-set-pdf-page-size-resolution-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PDF σε Java – Πλήρης Οδηγός με Προσαρμοσμένες Επιλογές

Έχετε αναρωτηθεί ποτέ πώς να **μετατρέψετε HTML σε PDF** σε Java χωρίς να μπλεχτείτε σε ένα λαβύρινθο ρυθμίσεων; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές συναντούν εμπόδια όταν χρειάζονται ακριβή έλεγχο του μεγέθους σελίδας, των περιθωρίων ή της ανάλυσης DPI ενώ μετατρέπουν μια ιστοσελίδα σε εκτυπώσιμο έγγραφο.  

Τα καλά νέα; Με το Aspose.HTML μπορείτε να **αποθηκεύσετε HTML ως PDF** με λίγες μόνο γραμμές κώδικα, και έχετε πλήρη πρόσβαση σε επιλογές όπως *set PDF page size* και *set PDF resolution*. Αυτό το tutorial σας οδηγεί βήμα‑βήμα στη διαδικασία, εξηγεί γιατί κάθε ρύθμιση είναι σημαντική και σας δείχνει ένα έτοιμο‑για‑εκτέλεση παράδειγμα.

Στο τέλος αυτού του οδηγού θα μπορείτε να πάρετε οποιοδήποτε τοπικό ή απομακρυσμένο αρχείο HTML και να δημιουργήσετε ένα PDF υψηλής ποιότητας που σέβεται τις απαιτήσεις διάταξης—ιδανικό για τιμολόγια, αναφορές ή e‑books.

---

![Μετατροπή HTML σε PDF με προσαρμοσμένες επιλογές](image.png "παράδειγμα μετατροπής html σε pdf")

## Τι Θα Μάθετε

- Πώς να φορτώσετε ένα αρχείο HTML με σωστή base URI ώστε οι σχετικές συνδέσεις να επιλύονται.
- Πώς να **ορίσετε το μέγεθος σελίδας PDF** (A4, Letter, προσαρμοσμένες διαστάσεις) και τα περιθώρια.
- Πώς να **ορίσετε την ανάλυση PDF** (DPI) για καθαρές εικόνες και κείμενο.
- Τον ακριβή κώδικα που απαιτείται για **αποθήκευση HTML ως PDF** χρησιμοποιώντας τη βιβλιοθήκη Aspose.HTML για Java.
- Συνηθισμένα προβλήματα—όπως ελλιπείς base URI ή υπερμεγέθεις εικόνες—και πώς να τα αποφύγετε.

### Προαπαιτούμενα

- Java Development Kit (JDK) 8 ή νεότερο.
- Maven ή Gradle για την προσθήκη του `aspose-html` (η τελευταία έκδοση τη στιγμή της συγγραφής είναι 23.10).
- Βασική κατανόηση της σύνταξης Java.
- Ένα αρχείο HTML που θέλετε να μετατρέψετε (θα χρησιμοποιήσουμε το `sample.html` στα παραδείγματα).

---

## Μετατροπή HTML σε PDF με Προσαρμοσμένες Επιλογές

Παρακάτω βρίσκεται το πλήρες, εκτελέσιμο πρόγραμμα που δείχνει κάθε βήμα. Αντιγράψτε‑και‑επικολλήστε το στο IDE σας, προσαρμόστε τις διαδρομές και τρέξτε το.

```java
import com.aspose.html.converters.*;
import com.aspose.html.rendering.*;

public class ConvertWithOptions {
    public static void main(String[] args) throws Exception {
        // Step 1: Define the base URI so that relative URLs in the HTML are resolved correctly
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setBaseUri("file:///YOUR_DIRECTORY/");

        // Step 2: Load the source HTML document using the load options
        HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/sample.html", loadOptions);

        // Step 3: Set up PDF conversion options – page size, margins, and output resolution
        PdfSaveOptions saveOptions = new PdfSaveOptions();
        saveOptions.setPageSize(PdfPageSize.A4);   // <-- set pdf page size
        saveOptions.setMarginTop(20);
        saveOptions.setMarginBottom(20);
        saveOptions.setResolution(300);           // <-- set pdf resolution (DPI)

        // Step 4: Convert the HTML document to PDF with the configured options
        document.save("YOUR_DIRECTORY/sample_custom.pdf", saveOptions);

        // Step 5: Inform the user that the conversion succeeded
        System.out.println("Custom PDF saved.");
    }
}
```

### Γιατί Κάθε Βήμα Είναι Σημαντικό

| Βήμα | Σκοπός | Συμβουλές & Ακραίες Περιπτώσεις |
|------|--------|--------------------------------|
| **1. Base URI** | Εξασφαλίζει ότι το `<img src="images/pic.png">` και άλλοι σχετικοί σύνδεσμοι δείχνουν στο σωστό φάκελο. | Αν το παραλείψετε, οι εικόνες μπορεί να λείπουν στο τελικό PDF. Χρησιμοποιήστε `file:///` για τοπικά αρχεία ή μια HTTP URL για απομακρυσμένους πόρους. |
| **2. Φόρτωση HTML** | Αναλύει το HTML στο μοντέλο DOM του Aspose. | Μεγάλα αρχεία HTML (>10 MB) μπορεί να χρειάζονται περισσότερη μνήμη· σκεφτείτε την αύξηση του heap της JVM (`-Xmx2g`). |
| **3. PDF Options** | Ελέγχει τις διαστάσεις σελίδας (`set pdf page size`), τα περιθώρια και το DPI (`set pdf resolution`). | Το A4 είναι 210 × 297 mm· για Letter χρησιμοποιήστε `PdfPageSize.LETTER`. DPI 300 είναι ιδανικό για εκτύπωση· 72 αρκεί για PDF μόνο για οθόνη. |
| **4. Αποθήκευση** | Γράφει το τελικό PDF στο δίσκο (`save html as pdf`). | Η διαδρομή εξόδου πρέπει να είναι εγγράψιμη. Μπορείτε να προσθέσετε προστασία από αντικατάσταση ελέγχοντας αν το αρχείο υπάρχει. |
| **5. Επιβεβαίωση** | Απλή ανατροφοδότηση στην κονσόλα. | Σε πραγματικές εφαρμογές αντικαταστήστε το `System.out` με έναν logger. |

---

## Ανάλυση Βήμα‑Βήμα

### 1. Ρύθμιση του Έργου σας (HTML to PDF Java)

Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση Aspose.HTML:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version>
</dependency>
```

Για χρήστες Gradle:

```gradle
implementation 'com.aspose:aspose-html:23.10'
```

> **Pro tip:** Η βιβλιοθήκη είναι πλήρως αυτόνομη· δεν χρειάζεστε επιπλέον native binaries ή γραμματοσειρές για βασικές μετατροπές.

### 2. Ορισμός της Base URI

Οι σχετικές URL είναι κοινή πηγή σπασμένων εικόνων. Ορίζοντας το `loadOptions.setBaseUri` στο φάκελο που περιέχει το HTML, επιτρέπετε στον μετατροπέα να επιλύει τις διαδρομές ακριβώς όπως θα έκανε ένας φυλλομετρητής.

```java
HtmlLoadOptions loadOptions = new HtmlLoadOptions();
loadOptions.setBaseUri("file:///C:/projects/pdf-demo/");
```

Αν το HTML σας αναφέρεται σε εξωτερικά CSS ή γραμματοσειρές που φιλοξενούνται σε CDN, μπορείτε να παραλείψετε τη base URI, αλλά προσέξτε την καθυστέρηση του δικτύου.

### 3. Φόρτωση του Εγγράφου HTML

```java
HtmlDocument document = new HtmlDocument("C:/projects/pdf-demo/sample.html", loadOptions);
```

Μπορείτε επίσης να φορτώσετε από URL:

```java
HtmlDocument document = new HtmlDocument("https://example.com/report.html", loadOptions);
```

### 4. Διαμόρφωση PDF Options – **Set PDF Page Size** & **Set PDF Resolution**

Η κλάση `PdfSaveOptions` σας δίνει λεπτομερή έλεγχο.

```java
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setPageSize(PdfPageSize.A4);   // set pdf page size
saveOptions.setMarginTop(20);
saveOptions.setMarginBottom(20);
saveOptions.setResolution(300);           // set pdf resolution (DPI)
```

- **Page Size:** Επιλέξτε από `PdfPageSize.A4`, `LETTER`, `LEGAL` ή δημιουργήστε προσαρμοσμένο `PdfPageSize` με πλάτος/ύψος σε points.
- **Resolution:** Υψηλότερο DPI προσφέρει πιο οξείες ραστερ εικόνες αλλά αυξάνει το μέγεθος του αρχείου. Για τις περισσότερες εργασίες εκτύπωσης 300 DPI είναι η «γλυκιά θέση».

### 5. Εκτέλεση της Μετατροπής – **Save HTML as PDF**

```java
document.save("C:/projects/pdf-demo/sample_custom.pdf", saveOptions);
```

Η μέθοδος ρέει αυτόματα το PDF στην καθορισμένη τοποθεσία. Αν χρειάζεστε το PDF στη μνήμη (π.χ. για αποστολή ως συνημμένο email), χρησιμοποιήστε την υπερφόρτωση με `OutputStream`:

```java
try (ByteArrayOutputStream baos = new ByteArrayOutputStream()) {
    document.save(baos, saveOptions);
    byte[] pdfBytes = baos.toByteArray();
    // attach pdfBytes to email, store in DB, etc.
}
```

### 6. Επαλήθευση του Αποτελέσματος

Ανοίξτε το `sample_custom.pdf` σε οποιονδήποτε προβολέα PDF. Θα πρέπει να δείτε:

- Σελίδες μεγέθους A4 με περιθώρια 20 pt πάνω/κάτω.
- Όλες οι εικόνες αποδομένες σε 300 DPI (σημειώστε την ευκρίνεια).
- Συνδέσμους και CSS όπως στο αρχικό HTML.

Αν κάτι φαίνεται λανθασμένο, ελέγξτε ξανά τη base URI και βεβαιωθείτε ότι όλοι οι εξωτερικοί πόροι είναι προσβάσιμοι.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

**Ε: Τι γίνεται αν το HTML μου περιέχει JavaScript;**  
Α: Το Aspose.HTML *δεν* εκτελεί JavaScript. Αν η σελίδα σας εξαρτάται από περιεχόμενο που δημιουργείται από script, προ‑αποδώστε το HTML (π.χ. με headless browser) πριν το περάσετε στον μετατροπέα.

**Ε: Μπορώ να ενσωματώσω προσαρμοσμένες γραμματοσειρές;**  
Α: Ναι. Τοποθετήστε τα αρχεία `.ttf` ή `.otf` στον ίδιο φάκελο και αναφέρετέ τα μέσω `@font-face` στο CSS. Η base URI θα τα κάνει προσβάσιμα.

**Ε: Πώς αλλάζω τον προσανατολισμό σε landscape;**  
```java
saveOptions.setPageOrientation(PdfPageOrientation.LANDSCAPE);
```

**Ε: Το PDF μου είναι τεράστιο—τι μπορώ να κάνω;**  
- Μειώστε το DPI (`setResolution(150)`).
- Συμπιέστε τις εικόνες με `saveOptions.setCompressionLevel(PdfCompressionLevel.HIGH)`.
- Αφαιρέστε περιττά υψηλής ανάλυσης στοιχεία από το πηγαίο HTML.

---

## Πλήρες Παράδειγμα (All‑In‑One)

Ακολουθεί η ολοκληρωμένη κλάση, έτοιμη για μεταγλώττιση. Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη διαδρομή του μηχανήματός σας.

```java
import com.aspose.html.converters.*;
import com.aspose.html.rendering.*;

public class ConvertWithOptions {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Base URI – resolves relative links
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();
        loadOptions.setBaseUri("file:///YOUR_DIRECTORY/");

        // 2️⃣ Load HTML
        HtmlDocument document = new HtmlDocument("YOUR_DIRECTORY/sample.html", loadOptions);

        // 3️⃣ PDF options – set pdf page size, margins, and resolution
        PdfSaveOptions saveOptions = new PdfSaveOptions();
        saveOptions.setPageSize(PdfPageSize.A4);   // set pdf page size
        saveOptions.setMarginTop(20);
        saveOptions.setMarginBottom(20);
        saveOptions.setResolution(300);           // set pdf resolution (DPI)

        // 4️⃣ Convert and save – this is where we actually save html as pdf
        document.save("YOUR_DIRECTORY/sample_custom.pdf", saveOptions);

        // 5️⃣ Confirmation
        System.out.println("Custom PDF saved at YOUR_DIRECTORY/sample_custom.pdf");
    }
}
```

Τρέξτε το πρόγραμμα, ανοίξτε το παραγόμενο PDF και θα δείτε ακριβώς τη διάταξη που ορίσατε. Αυτό είναι **convert HTML to PDF** σε Java, πλήρως εξοπλισμένο με προσαρμοσμένο μέγεθος σελίδας και ανάλυση.

---

## Επόμενα Βήματα & Σχετικά Θέματα

- **Batch conversion:** Επανάληψη σε φάκελο HTML αρχείων για μαζική παραγωγή PDF.
- **Dynamic content:** Συνδυάστε το Aspose.HTML με μηχανή προτύπων (π.χ. Thymeleaf) για δημιουργία τιμολογίων σε πραγματικό χρόνο.
- **Security hardening:** Επικυρώστε το εισερχόμενο HTML για αποφυγή κακόβουλης σήμανσης πριν τη μετατροπή.
- **Alternative libraries:** Συγκρίνετε το Aspose.HTML με το OpenHTMLtoPDF ή το wkhtmltopdf για ειδικές περιπτώσεις.

Πειραματιστείτε με διαφορετικά μεγέθη σελίδας (`PdfPageSize.LETTER`), προσανατολισμούς ή ακόμη και προσαρμοσμένες διαστάσεις αν ετοιμάζετε φυλλάδιο. Το API είναι αρκετά ευέλικτο για να καλύψει τις περισσότερες *html to pdf java* περιπτώσεις που θα συναντήσετε.

---

## Συμπέρασμα

Καλύψαμε όλα όσα χρειάζεστε για **convert HTML to PDF** σε Java, ενώ **set PDF page size**, **set PDF resolution**, και **save HTML as PDF** χρησιμοποιώντας το Aspose.HTML. Ο οδηγός βήμα‑βήμα, ο πλήρης κώδικας και οι συμβουλές αντιμετώπισης προβλημάτων

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}