---
category: general
date: 2026-02-10
description: Ορίστε το μέγεθος σελίδας PDF χρησιμοποιώντας το Aspose HTML για Java.
  Μάθετε πώς να μετατρέψετε μια ιστοσελίδα σε PDF, να αυξήσετε το DPI του PDF και
  να δημιουργήσετε PDF από έναν ιστότοπο σε λίγα λεπτά.
draft: false
keywords:
- set pdf page size
- convert webpage to pdf
- increase pdf dpi
- aspose html to pdf
- generate pdf from website
language: el
og_description: Ορίστε το μέγεθος σελίδας PDF με το Aspose HTML for Java. Αυτός ο
  οδηγός δείχνει πώς να μετατρέψετε μια ιστοσελίδα σε PDF, να αυξήσετε το DPI του
  PDF και να δημιουργήσετε PDF από έναν ιστότοπο.
og_title: Ορισμός μεγέθους σελίδας PDF με το Aspose HTML – Εγχειρίδιο Java
tags:
- Aspose
- Java
- PDF
- HTML-to-PDF
title: Ορισμός μεγέθους σελίδας PDF με το Aspose HTML – Πλήρης οδηγός Java
url: /el/java/conversion-html-to-other-formats/set-pdf-page-size-with-aspose-html-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός μεγέθους σελίδας PDF με Aspose HTML – Πλήρης Οδηγός Java

Έχετε ποτέ χρειαστεί να **ορίσετε το μέγεθος σελίδας PDF** όταν μετατρέπετε μια ζωντανή ιστοσελίδα σε εκτυπώσιμο έγγραφο; Δεν είστε μόνοι—οι προγραμματιστές αντιμετωπίζουν συνεχώς προβλήματα με τα περιθώρια, το DPI και τις διαστάσεις της σελίδας όταν **μετατρέπουν ιστοσελίδα σε PDF** για αναφορές, τιμολόγια ή αρχειοθέτηση.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **ορίσετε το μέγεθος σελίδας PDF**, να αυξήσετε την ανάλυση εικόνας και, τέλος, να δημιουργήσετε ένα επαγγελματικό PDF απευθείας από ένα URL χρησιμοποιώντας το Aspose HTML for Java. Στο τέλος θα γνωρίζετε ακριβώς γιατί κάθε επιλογή είναι σημαντική και πώς να τις προσαρμόσετε στα δικά σας έργα.

## Τι Θα Μάθετε

- Πώς να προσθέσετε τη βιβλιοθήκη Aspose HTML σε ένα έργο Maven/Gradle.  
- Τον ακριβή κώδικα που απαιτείται για **ορισμό μεγέθους σελίδας PDF** σε A4 (ή οποιοδήποτε προσαρμοσμένο μέγεθος).  
- Πώς να **αυξήσετε το DPI του PDF** ώστε τα στιγμιότυπα και τα γραφικά να παραμένουν καθαρά.  
- Την εντολή‑μια‑γραμμή που **μετατρέπει ιστοσελίδα σε PDF** με όλες τις επιλογές που μόλις ρυθμίσατε.  
- Συμβουλές για την αντιμετώπιση ακραίων περιπτώσεων, όπως σελίδες που απαιτούν επιπλέον περιθώριο ή μη‑τυπικό μέγεθος σελίδας.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose—απλώς ένα IDE με υποστήριξη Java και σύνδεση στο διαδίκτυο.

## Προαπαιτούμενα

| Απαίτηση | Γιατί είναι σημαντικό |
|----------|------------------------|
| Java 8 ή νεότερο | Το Aspose HTML στοχεύει σε Java 8+· παλαιότερα runtimes θα ρίξουν `UnsupportedClassVersionError`. |
| Maven ή Gradle (προαιρετικό) | Κάνει τη διαχείριση εξαρτήσεων απλή. Μπορείτε επίσης να κατεβάσετε το JAR χειροκίνητα. |
| Πρόσβαση στο διαδίκτυο | Το παράδειγμα κατεβάζει το `https://example.com` κατά την εκτέλεση, οπότε ο κεντρικός υπολογιστής πρέπει να είναι προσβάσιμος. |
| Βασική κατανόηση των PDF | Η γνώση του τι σημαίνουν “A4”, “points” και “DPI” βοηθά στην επιλογή των σωστών τιμών. |

> **Pro tip:** Αν εργάζεστε πίσω από εταιρικό proxy, ορίστε τις ιδιότητες JVM `http.proxyHost` και `http.proxyPort` ώστε ο μετατροπέας να μπορεί να φέρει τη σελίδα.

## Βήμα 1: Προσθήκη του Aspose HTML στο Έργο σας (aspose html to pdf)

Αν χρησιμοποιείτε Maven, τοποθετήστε το παρακάτω απόσπασμα στο `pom.xml`. Για Gradle, η αντίστοιχη γραμμή `implementation` φαίνεται παρακάτω.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- replace with the latest version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-html:23.10' // check Maven Central for newest
```

> **Why this step?** Το Aspose HTML παρέχει την κλάση `Converter` και το `PdfSaveOptions` που θα χρειαστούμε. Χωρίς τη βιβλιοθήκη ο κώδικας δεν θα μεταγλωττιστεί.

## Βήμα 2: Δημιουργία του `PdfSaveOptions` και **Ορισμός μεγέθους σελίδας PDF**

Τώρα δημιουργούμε το αντικείμενο επιλογών και λέμε στο Aspose ότι θέλουμε μια σελίδα A4. Η σταθερά `Size.A4` είναι μια βολική συντόμευση, αλλά μπορείτε επίσης να περάσετε ένα προσαρμοσμένο `Size` (πλάτος × ύψος σε points).

```java
import com.aspose.html.converters.PdfSaveOptions;
import com.aspose.html.rendering.drawing.Size;

// ...

// Step 2: Create options and set the page size to A4 (210 mm × 297 mm)
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(Size.A4);   // <-- this is where we set PDF page size
```

> **What’s happening?** Η μέθοδος `setPageSize` λέει στη μηχανή απόδοσης πόσο μεγάλο πρέπει να είναι το καμβά πριν σχεδιαστεί το περιεχόμενο. Αν το παραλείψετε, το Aspose χρησιμοποιεί προεπιλογή 8.5×11 ίντσες, που μπορεί να μην ταιριάζει με τις οδηγίες branding σας.

## Βήμα 3: Ορισμός Περιθωρίων (Προαιρετικό αλλά Συχνά Απαιτείται)

Τα περιθώρια εκφράζονται σε points (1 pt ≈ 0.352 mm). Εδώ δίνουμε ένα μέτριο περιθώριο 20 points σε όλες τις πλευρές. Προσαρμόστε το ανάλογα με το layout σας.

```java
// Step 3: Set 20‑point margins (left, top, right, bottom)
pdfOptions.setMargins(20, 20, 20, 20);
```

> **Why margins?** Ένα στενά ταιριαστό PDF μπορεί να κόψει κεφαλίδες ή υποσέλιδα κατά την εκτύπωση. Η προσθήκη ενός μικρού περιθωρίου αποτρέπει αυτή την άσχημη έκπληξη.

## Βήμα 4: **Αύξηση DPI PDF** για πιο Οξές Εικόνες

Αν η πηγή περιέχει γραφικά υψηλής ανάλυσης, αυξήστε το DPI από το προεπιλεγμένο 96 σε κάτι όπως 300. Αυτό κάνει το παραγόμενο PDF να φαίνεται καθαρό σε laser εκτυπωτές.

```java
// Step 4: Raise DPI to 300 for sharper raster graphics
pdfOptions.setDpi(300);   // <-- this is how we increase PDF DPI
```

> **Note:** Υψηλότερο DPI αυξάνει το μέγεθος του αρχείου αναλογικά. Αν παράγετε δεκάδες PDF σε batch, δοκιμάστε την ισορροπία μεταξύ ποιότητας και μεγέθους.

## Βήμα 5: **Μετατροπή Ιστοσελίδας σε PDF** Χρησιμοποιώντας τις Ρυθμισμένες Επιλογές

Τέλος, καλούμε το `Converter.convert`. Το πρώτο όρισμα είναι το URL, το δεύτερο το αντικείμενο `pdfOptions`, και το τρίτο η διαδρομή του αρχείου προορισμού.

```java
import com.aspose.html.converters.Converter;

// ...

// Step 5: Perform the conversion
String sourceUrl = "https://example.com";
String outputPath = "example.pdf";

Converter.convert(sourceUrl, pdfOptions, outputPath);
System.out.println("PDF generated at " + outputPath);
```

> **What if the page needs authentication?** Περάστε ένα προσαρμοσμένο `HttpRequest` με headers (π.χ., `Authorization: Bearer …`) στο `Converter.convert`. Τα overloads του API δέχονται αντικείμενο `HttpRequest` ακριβώς για αυτήν την περίπτωση.

## Βήμα 6: Επαλήθευση του Αποτελέσματος (Δημιουργία PDF από Ιστοσελίδα)

Ανοίξτε το `example.pdf` σε οποιονδήποτε προβολέα. Θα πρέπει να δείτε ένα έγγραφο μεγέθους A4, με περιθώρια 20 points παντού, και εικόνες αποδομένες σε 300 DPI. Η διάταξη του κειμένου θα ταιριάζει με το αρχικό CSS της ιστοσελίδας, χάρη στη πλήρη μηχανή απόδοσης HTML 5 του Aspose.

```text
✔ PDF page size: A4 (210 mm × 297 mm)
✔ Margins: 20 pt on each side
✔ DPI: 300 (high‑resolution)
✔ Source URL: https://example.com
```

Αν το αποτέλεσμα φαίνεται λανθασμένο, ελέγξτε:

1. **Network access** – Ήταν το URL προσβάσιμο;  
2. **CSS media queries** – Κάποιες ιστοσελίδες κρύβουν περιεχόμενο όταν ενεργοποιείται `@media print`.  
3. **Custom page size** – Αντικαταστήστε το `Size.A4` με `new Size(width, height)` για μη‑τυπικές διαστάσεις.

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται η πλήρης κλάση Java που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο IDE σας. Συγκεντρώνεται ακριβώς όπως είναι, εφόσον η εξάρτηση Maven/Gradle είναι ικανοποιημένη.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfSaveOptions;
import com.aspose.html.rendering.drawing.Size;

public class ConvertWithOptions {
    public static void main(String[] args) throws Exception {

        // Step 1: Create PDF save options to customize the conversion
        PdfSaveOptions pdfOptions = new PdfSaveOptions();

        // Step 2: Set the target page size (A4 in this example)
        pdfOptions.setPageSize(Size.A4);

        // Step 3: Define margins (left, top, right, bottom) in points
        pdfOptions.setMargins(20, 20, 20, 20);

        // Step 4: Increase DPI for sharper images in the resulting PDF
        pdfOptions.setDpi(300);

        // Step 5: Convert the web page at the given URL to a PDF file using the options above
        Converter.convert("https://example.com", pdfOptions, "example.pdf");

        // Step 6: Notify that the conversion has completed
        System.out.println("Converted with custom options.");
    }
}
```

> **Expected output:** Η εκτέλεση του προγράμματος εκτυπώνει `Converted with custom options.` και δημιουργεί το `example.pdf` στον τρέχοντα φάκελο. Ανοίγοντας το αρχείο θα δείτε μια σελίδα A4 με τα περιθώρια και τα γραφικά υψηλής ανάλυσης που καθορίσατε.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

| Ερώτηση | Απάντηση |
|----------|----------|
| *Τι κάνω αν χρειάζομαι προσαρμοσμένο μέγεθος σελίδας (π.χ., Letter ή φυλλάδιο);* | Χρησιμοποιήστε `new Size(widthInPoints, heightInPoints)` αντί για `Size.A4`. Για Letter (8.5×11 in) είναι `new Size(612, 792)`. |
| *Η ιστοσελίδα μου φορτώνει περιεχόμενο με JavaScript. Θα περιμένει ο μετατροπέας;* | Από προεπιλογή το Aspose HTML εκτελεί σενάρια έως 30 δευτερόλεπτα. Μπορείτε να το αλλάξετε με `pdfOptions.setScriptTimeout(milliseconds)`. |
| *Μπορώ να ενσωματώσω προσαρμοσμένη γραμματοσειρά;* | Ναι—καταχωρίστε τη γραμματοσειρά μέσω `pdfOptions.getFontProvider().addFont("path/to/font.ttf")`. |
| *Πώς διαχειρίζομαι πιστοποιητικά HTTPS που είναι αυτο‑υπογεγραμμένα;* | Παρέχετε ένα προσαρμοσμένο `SSLContext` στον υποκείμενο `HttpClient` και περάστε το προετοιμασμένο αίτημα στο `Converter.convert`. |
| *Υπάρχει τρόπος να επεξεργαστώ μαζικά πολλές URL;* | Τυλίξτε τη λογική μετατροπής σε βρόχο· απλώς επαναχρησιμοποιήστε το ίδιο αντικείμενο `PdfSaveOptions` για απόδοση. |

## Συμπέρασμα

Τώρα έχετε μια σταθερή, έτοιμη για παραγωγή συνταγή για **ορισμό μεγέθους σελίδας PDF** ενώ **μετατρέπετε ιστοσελίδα σε PDF**, **αυξάνετε DPI PDF**, και γενικά **δημιουργείτε PDF από ιστοσελίδα** χρησιμοποιώντας το Aspose HTML for Java. Η κεντρική ιδέα είναι απλή: δημιουργήστε ένα αντικείμενο `PdfSaveOptions`, ρυθμίστε τις ιδιότητές του ώστε να ταιριάζουν στις απαιτήσεις του layout σας, και περάστε το στο `Converter.convert`.  

Από εδώ μπορείτε να εξερευνήσετε την προσθήκη κεφαλίδων/υποσέλιδων, υδατογραφήματα, ή ακόμη και τη συγχώνευση πολλαπλών σελίδων σε ένα ενιαίο PDF. Το API του Aspose είναι τόσο πλούσιο που καλύπτει τις περισσότερες περιπτώσεις δημιουργίας PDF, οπότε μη διστάσετε να πειραματιστείτε.

Έχετε περισσότερες ερωτήσεις σχετικά με **aspose html to pdf** ή χρειάζεστε βοήθεια με κάποια συγκεκριμένη ακραία περίπτωση; Αφήστε ένα σχόλιο παρακάτω ή ελέγξτε την επίσημη τεκμηρίωση του Aspose για πιο βαθιές πληροφορίες. Καλό coding, και τα PDF σας να αποδίδουν πάντα ακριβώς όπως το φαντάζεστε!  

![Εικονογράφηση ορισμού μεγέθους PDF](set-pdf-page-size.png "Παράδειγμα ορισμού μεγέθους PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}