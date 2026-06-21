---
category: general
date: 2026-03-15
description: Ορίστε εύκολα το μέγεθος σελίδας PDF με Java. Μάθετε πώς να μετατρέπετε
  HTML σε PDF με Java, ορίστε το μέγεθος σελίδας A4 και ενεργοποιήστε τη JavaScript
  για υψηλής ποιότητας έξοδο.
draft: false
keywords:
- set pdf page size
- java html to pdf
- how to convert html
- convert html to pdf java
- set a4 page size
language: el
og_description: Ορίστε το μέγεθος της σελίδας PDF στη Java και δείτε πώς να μετατρέψετε
  HTML σε PDF με το Aspose.HTML. Πλήρης κώδικας, επιλογές και συμβουλές περιλαμβάνονται.
og_title: Ορισμός μεγέθους σελίδας PDF σε Java – Πλήρης οδηγός HTML σε PDF
tags:
- pdf
- java
- aspose
- html
title: Ορισμός μεγέθους σελίδας PDF σε Java – Οδηγός Java HTML σε PDF
url: /el/java/conversion-html-to-other-formats/set-pdf-page-size-in-java-java-html-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ορισμός Μεγέθους Σελίδας PDF σε Java – Οδηγός Java HTML σε PDF

Έχετε χρειαστεί ποτέ να **ορίσετε το μέγεθος σελίδας PDF** από τη Java αλλά δεν ήσασταν σίγουροι ποια κλήση API να χρησιμοποιήσετε; Δεν είστε μόνοι. Σε πολλά έργα το τελικό PDF φαίνεται συμπιεσμένο ή τεντωμένο επειδή οι προεπιλεγμένες διαστάσεις σελίδας δεν ταιριάζουν με την αρχική διάταξη HTML.

Τα καλά νέα είναι ότι με το Aspose.HTML for Java μπορείτε να ελέγξετε το μέγεθος σελίδας, το DPI και ακόμη και την εκτέλεση JavaScript με μία μόνο, καθαρή κλήση. Σε αυτό το tutorial θα περάσουμε από τη μετατροπή ενός αρχείου HTML σε PDF ενώ ορίζουμε ρητά **μέγεθος σελίδας a4**, και θα προσθέσουμε μερικά επιπλέον κόλπα για ένα επαγγελματικό αποτέλεσμα. Στο τέλος θα γνωρίζετε **πώς να μετατρέψετε HTML** σε PDF με στυλ Java, και θα έχετε ένα επαναχρησιμοποιήσιμο απόσπασμα που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle.

## Τι Θα Μάθετε

- Πώς να εισάγετε τα σωστά πακέτα Aspose.HTML.
- Πώς να δημιουργήσετε `PdfConversionOptions` και να διαμορφώσετε **μέγεθος σελίδας**, ανάλυση και υποστήριξη JavaScript.
- Γιατί η ρύθμιση του DPI στα 300 είναι σημαντική για PDF έτοιμα για εκτύπωση.
- Ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε.
- Κοινά προβλήματα (π.χ., ελλιπείς γραμματοσειρές, μη υποστηριζόμενο CSS) και πώς να τα αποφύγετε.

**Προαπαιτούμενα**  
Ένα πρόσφατο JDK (8 +), Maven ή Gradle, και άδεια Aspose.HTML for Java (η δωρεάν δοκιμή λειτουργεί για δοκιμές). Δεν απαιτούνται άλλες βιβλιοθήκες τρίτων.

---

## Βήμα 1: Προσθήκη Εξαρτήσεων Aspose.HTML

Αν χρησιμοποιείτε Maven, προσθέστε τα παρακάτω στο `pom.xml` σας. Για Gradle, οι ίδιες συντεταγμένες λειτουργούν με `implementation`.

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.10</version> <!-- use the latest version -->
</dependency>
```

> **Συμβουλή:** Διατηρήστε τον αριθμό έκδοσης ενημερωμένο· οι νεότερες εκδόσεις διορθώνουν σφάλματα απόδοσης που μπορούν να επηρεάσουν την τελική διάταξη PDF.

---

## Βήμα 2: Δημιουργία Επιλογών Μετατροπής PDF (Ορισμός Μεγέθους Σελίδας PDF)

Η καρδιά της λειτουργίας βρίσκεται στο `PdfConversionOptions`. Αυτό το αντικείμενο σας επιτρέπει να ορίσετε ακριβώς πώς πρέπει να φαίνεται το PDF.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.pdf.PdfConversionOptions;
import com.aspose.html.converters.pdf.PdfPageSize;

public class AdvancedConvert {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Initialise the options container
        PdfConversionOptions conversionOptions = new PdfConversionOptions();

        // 2️⃣ Set the page size – here we pick A4, which is 210 mm × 297 mm
        conversionOptions.setPageSize(PdfPageSize.A4); // set a4 page size

        // 3️⃣ Choose a high‑resolution DPI for crisp text and images
        conversionOptions.setDpi(300); // 300 DPI ensures print‑quality output

        // 4️⃣ Enable JavaScript if your HTML relies on it (e.g., dynamic charts)
        conversionOptions.setEnableJavaScript(true);

        // 5️⃣ Perform the conversion using the custom options
        Converter.convert(
                "YOUR_DIRECTORY/input.html",   // source HTML
                "YOUR_DIRECTORY/output.pdf",   // target PDF
                conversionOptions);            // our configured options
    }
}
```

### Γιατί Αυτές οι Ρυθμίσεις Είναι Σημαντικές

- **`setPageSize(PdfPageSize.A4)`** – Χωρίς αυτό, το Aspose προεπιλέγει US Letter (8.5×11 ίντσες). Αν το σχέδιό σας δημιουργήθηκε για A4, το περιεχόμενο είτε θα υπερχειλίσει είτε θα αφήσει ανεπιθύμητα λευκά περιθώρια.  
- **`setDpi(300)`** – Ένα υψηλότερο DPI προσφέρει πιο οξυμένη διανυσματική γραφή και ραστερ εικόνες. Για PDF στην οθόνη τα 150 DPI είναι επαρκή, αλλά για εκτύπωση θα θέλετε τουλάχιστον 300 DPI.  
- **`setEnableJavaScript(true)`** – Πολλές σύγχρονες αναφορές HTML ενσωματώνουν γραφήματα που αποδίδονται από βιβλιοθήκες όπως το Chart.js. Η ενεργοποίηση του JavaScript επιτρέπει στον μετατροπέα να εκτελέσει αυτά τα σενάρια πριν τη ραστεροποίηση της σελίδας.

---

## Βήμα 3: Εκτέλεση του Μετατροπέα και Επαλήθευση του Αποτελέσματος

Compile and run the class:

```bash
javac -cp "path/to/aspose-html.jar" AdvancedConvert.java
java -cp ".:path/to/aspose-html.jar" AdvancedConvert
```

Αν όλα είναι ρυθμισμένα σωστά, θα βρείτε το `output.pdf` στον ίδιο φάκελο. Ανοίξτε το με οποιονδήποτε προβολέα PDF· θα πρέπει να δείτε μια σελίδα μεγέθους A4, γραφικά υψηλής ανάλυσης και πλήρως αποδομένο περιεχόμενο JavaScript.

> **Τι γίνεται αν το PDF φαίνεται κενό;**  
> Ελέγξτε ξανά ότι το αρχείο HTML χρησιμοποιεί απόλυτες διαδρομές για τις εικόνες ή ότι το `baseUri` είναι σωστά ορισμένο. Επίσης, βεβαιωθείτε ότι η κονσόλα JavaScript δεν έδωσε σφάλμα—το Aspose παραλείπει σιωπηλά τα αποτυχημένα σενάρια εκτός αν ενεργοποιήσετε την καταγραφή εντοπισμού σφαλμάτων.

---

## Πώς να Μετατρέψετε HTML σε PDF Java Χρησιμοποιώντας Διαφορετικό Μέγεθος Σελίδας

Μερικές φορές χρειάζεστε **letter**, **legal**, ή ακόμη και **προσαρμοσμένο** μέγεθος (π.χ., 5 ίντσες × 7 ίντσες για αποδείξεις). Το API προσφέρει υπερφορτώσεις:

```java
// Custom size: width = 5 inches, height = 7 inches (converted to points)
conversionOptions.setPageSize(new com.aspose.html.converters.pdf.PdfPageSize(5 * 72, 7 * 72));
```

Θυμηθείτε: 1 point = 1/72 ίντσες, έτσι πολλαπλασιάζουμε τις ίντσες με 72 για να πάρουμε τις σωστές διαστάσεις.

---

## Περιπτώσεις Άκρων & Συχνές Ερωτήσεις

### 1️⃣ Λειτουργεί αυτό με τους κανόνες CSS @page;

Το Aspose.HTML σέβεται τις δηλώσεις μεγέθους `@page`, αλλά η ρητή `setPageSize` τις παρακάμπτει. Αν προτιμάτε ο δημιουργός του HTML να καθορίζει το μέγεθος, απλώς παραλείψτε την κλήση `setPageSize`.

### 2️⃣ Τι γίνεται με τις γραμματοσειρές που δεν είναι εγκατεστημένες στον διακομιστή;

Μπορείτε να ενσωματώσετε προσαρμοσμένες γραμματοσειρές προσθέτοντάς τες στο `FontSettings` του μετατροπέα:

```java
conversionOptions.getFontSettings().setCustomFontsFolder("fonts/");
```

### 3️⃣ Μπορώ να μετατρέψω ένα URL αντί για τοπικό αρχείο;

Απόλυτα. Περνάτε το URL string απευθείας:

```java
Converter.convert("https://example.com/report.html", "report.pdf", conversionOptions);
```

Απλώς βεβαιωθείτε ότι ο διακομιστής είναι προσβάσιμος από τη διαδικασία Java.

### 4️⃣ Πώς να διαχειριστείτε έγγραφα HTML πολλαπλών σελίδων;

Το Aspose παγκοσμίως σελιδοποιεί αυτόματα βάσει του μεγέθους σελίδας που ορίσατε. Αν χρειάζεστε υποχρεωτική αλλαγή σελίδας, ενσωματώστε `<div style="page-break-before:always;"></div>` στο HTML.

---

## Πλήρες Παράδειγμα Εργασίας (All‑In‑One)

Παρακάτω είναι μια έκδοση έτοιμη για αντιγραφή‑επικόλληση που περιλαμβάνει εισαγωγές, επιλογές και έναν μικρό βοηθό για τον εντοπισμό του αρχείου εισόδου σε σχέση με τη ρίζα του έργου.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.pdf.PdfConversionOptions;
import com.aspose.html.converters.pdf.PdfPageSize;

public class AdvancedConvert {
    public static void main(String[] args) throws Exception {
        // Define where your HTML lives and where you want the PDF to appear
        String inputPath  = System.getProperty("user.dir") + "/src/main/resources/input.html";
        String outputPath = System.getProperty("user.dir") + "/output/output.pdf";

        // ① Initialise conversion options
        PdfConversionOptions conversionOptions = new PdfConversionOptions();

        // ② Set A4 page size – this is the core of “set pdf page size”
        conversionOptions.setPageSize(PdfPageSize.A4); // set a4 page size

        // ③ High‑resolution DPI for print‑ready PDFs
        conversionOptions.setDpi(300);

        // ④ Enable JavaScript for dynamic content (charts, calculations, etc.)
        conversionOptions.setEnableJavaScript(true);

        // ⑤ Perform the conversion
        Converter.convert(inputPath, outputPath, conversionOptions);

        System.out.println("✅ PDF created at: " + outputPath);
    }
}
```

**Αναμενόμενο Αποτέλεσμα:**  
Ένα PDF με όνομα `output.pdf` που ταιριάζει με τις διαστάσεις ενός φύλλου A4, αποδίδει τυχόν γραφήματα που οδηγούνται από JavaScript και φαίνεται καθαρό τόσο στην οθόνη όσο και στο εκτυπωμένο χαρτί.

---

## Συμπέρασμα

Τώρα γνωρίζετε πώς να **ορίσετε το μέγεθος σελίδας PDF** στη Java χρησιμοποιώντας το Aspose.HTML, και έχετε δει τη πλήρη ροή εργασίας για **convert html to pdf java**‑style. Με τη ρύθμιση του `PdfConversionOptions` μπορείτε να ελέγξετε το DPI, να ενεργοποιήσετε το JavaScript και ακόμη να επιλέξετε προσαρμοσμένη διάσταση σελίδας—όλα ενώ διατηρείτε τον κώδικα καθαρό και συντηρήσιμο.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αλλάξετε το μέγεθος **A4** σε **letter**, πειραματιστείτε με μετατροπές **java html to pdf** από απομακρυσμένα URLs, ή προσθέστε προστασία κωδικού μέσω `PdfSaveOptions`. Οι δυνατότητες είναι απεριόριστες, και το ίδιο μοτίβο ισχύει για όλα τα σενάρια μετατροπής Aspose.

### Περαιτέρω Ανάγνωση & Επόμενα Βήματα

- **Java HTML to PDF** – Εξερευνήστε άλλους μετατροπείς όπως το `ImageConversionOptions` για δημιουργία μικρογραφιών.  
- **How to Convert HTML** – Μάθετε για ασύγχρονη μετατροπή μεγάλων παρτίδων χρησιμοποιώντας το cloud API του Aspose.  
- **Set A4 Page Size** – Βυθιστείτε περισσότερο στις προσαρμοσμένες διαστάσεις σελίδας για τιμολόγια ή αποδείξεις.  

Αν αντιμετωπίσετε οποιοδήποτε πρόβλημα, αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική δουλειά, και απολαύστε τα τέλεια μεγέθη PDF σας! 

![Set PDF page size example](https://example.com/images/set-pdf-page-size.png "set pdf page size")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}