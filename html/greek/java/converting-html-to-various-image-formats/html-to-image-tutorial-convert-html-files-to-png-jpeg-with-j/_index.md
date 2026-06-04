---
category: general
date: 2026-06-03
description: Μάθετε έναν οδηγό μετατροπής HTML σε εικόνα που δείχνει πώς να μετατρέψετε
  HTML σε PNG, να αποθηκεύσετε HTML ως PNG, και επίσης να μετατρέψετε HTML σε JPEG
  ενώ ορίζετε την ποιότητα JPEG για τα καλύτερα αποτελέσματα.
draft: false
keywords:
- html to image tutorial
- convert html to png
- save html as png
- convert html to jpeg
- set jpeg quality
language: el
og_description: Αυτό το σεμινάριο μετατροπής HTML σε εικόνα εξηγεί πώς να μετατρέψετε
  HTML σε PNG, να αποθηκεύσετε HTML ως PNG και να μετατρέψετε HTML σε JPEG ενώ ορίζετε
  την ποιότητα JPEG για βέλτιστο αποτέλεσμα.
og_title: Μάθημα html σε εικόνα – Οδηγός Java για μετατροπή PNG & JPEG
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Learn an html to image tutorial that shows how to convert html to png,
    save html as png, and also convert html to jpeg while set jpeg quality for best
    results.
  headline: html to image tutorial – Convert HTML Files to PNG & JPEG with Java
  type: TechArticle
tags:
- Java
- ImageProcessing
- HTMLConversion
title: Μάθημα html σε εικόνα – Μετατροπή αρχείων HTML σε PNG & JPEG με Java
url: /el/java/converting-html-to-various-image-formats/html-to-image-tutorial-convert-html-files-to-png-jpeg-with-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# html to image tutorial – Μετατροπή σελίδων HTML σε εικόνες PNG ή JPEG σε Java

Ποτέ κοίταξες ένα *html to image tutorial* και αναρωτήθηκες γιατί τα παραδείγματα φαίνονται ημιτελή; Ίσως χρειάζεται να ενσωματώσεις ένα στιγμιότυπο ιστοσελίδας σε μια αναφορά, ή να δημιουργήσεις μικρογραφίες για μια γκαλερί, και δεν μπορείς να βρεις έναν σαφή, ολοκληρωμένο οδηγό. **Καλά νέα:** αυτό το άρθρο σε καθοδηγεί μέσα από μια πλήρη, έτοιμη‑για‑εκτέλεση λύση που **μετατρέπει HTML σε PNG**, σου επιτρέπει να **αποθηκεύσεις HTML ως PNG** με προσαρμοσμένη συμπίεση, και ακόμη δείχνει πώς να **μετατρέψεις HTML σε JPEG** ενώ **ορίζεις την ποιότητα JPEG** για τέλεια ισορροπία μεταξύ μεγέθους και καθαρότητας.

Στις επόμενες λίγες λεπτά θα δημιουργήσουμε ένα μικρό πρόγραμμα Java, θα ρυθμίσουμε μερικές επιλογές, και θα καταλήξουμε με καθαρές εικόνες στο δίσκο. Χωρίς μαγεία, μόνο απλός κώδικας που μπορείς να αντιγράψεις‑και‑επικολλήσεις και να τρέξεις.

## Προαπαιτούμενα

* **Java 17** (ή οποιοδήποτε πρόσφατο JDK) – ο κώδικας χρησιμοποιεί το τυπικό API `java.nio.file`, οπότε οποιοδήποτε σύγχρονο JDK λειτουργεί.
* **Aspose.HTML for Java** (ή οποιαδήποτε παρόμοια βιβλιοθήκη που παρέχει `ImageSaveOptions` και `Converter`). Μπορείτε να κατεβάσετε το Maven artifact από το επίσημο αποθετήριο.
* Ένα απλό αρχείο HTML (π.χ., `sample.html`) τοποθετημένο σε φάκελο που έχετε πρόσβαση.  
* Ένα IDE ή ένα τερματικό όπου μπορείτε να μεταγλωττίσετε και να εκτελέσετε μια κλάση Java.

Αν χρησιμοποιείτε Maven, προσθέστε αυτήν την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Συμβουλή:** Η δωρεάν έκδοση αξιολόγησης προσθέτει υδατογράφημα στην εικόνα εξόδου. Για παραγωγή, αποκτήστε μια κατάλληλη άδεια – αφαιρεί το υδατογράφημα και ξεκλειδώνει το πλήρες σύνολο λειτουργιών.

## Βήμα 1: Ρύθμιση του Περιβάλλοντος του html to image tutorial

Πρώτα απ' όλα, χρειαζόμαστε μια κλάση Java που να εισάγει τις απαιτούμενες κλάσεις. Αυτό είναι το σκελετό πάνω στον οποίο θα χτίσετε:

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.ImageSaveOptions;
import java.nio.file.Paths;

public class HtmlToImageDemo {
    public static void main(String[] args) {
        // We'll fill this in step‑by‑step.
    }
}
```

Το **html to image tutorial** ξεκινά εδώ. Κρατώντας τη μέθοδο `main` μικρή, κάνουμε κάθε βήμα μετατροπής σαφές και εύκολο στην αποσφαλμάτωση.

## Βήμα 2: Μετατροπή HTML σε PNG – Ο πυρήνας του “convert html to png”

Τώρα πραγματικά **convert html to png**. Η μέθοδος `Converter.convert` της βιβλιοθήκης κάνει το σκληρό έργο· εμείς απλώς πρέπει να της πούμε πού βρίσκεται το πηγαίο HTML και πού πρέπει να αποθηκευτεί το PNG.

```java
// Step 2: Convert HTML to PNG
public static void convertToPng(String htmlPath, String pngPath) throws Exception {
    // Step 1: Create image save options
    ImageSaveOptions options = new ImageSaveOptions();

    // Step 2: Choose PNG format and configure compression
    options.setFormat(ImageSaveOptions.ImageFormat.Png);
    // Compression level: 0 = fastest, 9 = smallest file size
    options.setPngCompressionLevel(9);

    // Step 3 (optional): Set JPEG quality – ignored for PNG but kept for completeness
    options.setJpegQuality(85);

    // Step 4: Run the conversion
    Converter.convert(htmlPath, pngPath, options);
}
```

Μερικά σημεία που πρέπει να σημειώσετε:

* `setPngCompressionLevel(9)` λέει στον κωδικοποιητή να συμπιέσει το αρχείο όσο το δυνατόν περισσότερο. Αν χρειάζεστε ταχύτητα αντί για μέγεθος, μειώστε το επίπεδο σε `0` ή `1`.
* Ακόμη και αν **αποθηκεύουμε HTML ως PNG**, καλούμε ακόμα το `setJpegQuality`. Η μέθοδος δεν επηρεάζει το PNG· έχει σημασία μόνο όταν η μορφή αλλάξει σε JPEG αργότερα.

## Βήμα 3: Αποθήκευση HTML ως PNG με Προσαρμοσμένη Συμπίεση – Ρύθμιση “save html as png”

Ας υποθέσουμε ότι δημιουργείτε μικρογραφίες για μια web‑app και θέλετε τα μικρότερα δυνατά αρχεία χωρίς να θυσιάζετε την αναγνωσιμότητα. Εδώ το **save html as png** γίνεται ενδιαφέρον: μπορείτε να συνδυάσετε τη συμπίεση PNG με συγκεκριμένο DPI (σημεία ανά ίντσα) για να ελέγξετε την πυκνότητα εικονοστοιχείων.

```java
public static void convertToPngWithDpi(String htmlPath, String pngPath, int dpi) throws Exception {
    ImageSaveOptions options = new ImageSaveOptions();
    options.setFormat(ImageSaveOptions.ImageFormat.Png);
    options.setPngCompressionLevel(9);
    // Adjust the resolution – higher DPI = sharper image, larger file
    options.setResolution(dpi);
    Converter.convert(htmlPath, pngPath, options);
}
```

Καλώντας τη μέθοδο με `300` DPI θα έχετε μια εικόνα έτοιμη για εκτύπωση, ενώ `72` DPI αρκεί για μικρογραφίες στην οθόνη. Πειραματιστείτε· το **html to image tutorial** λειτουργεί με τον ίδιο τρόπο για οποιοδήποτε DPI επιλέξετε.

## Βήμα 4: Μετατροπή HTML σε JPEG και Ορισμός Ποιότητας JPEG – Κατανόηση του “convert html to jpeg” & “set jpeg quality”

Όταν χρειάζεστε έξοδο τύπου φωτογραφίας (ίσως για μια γκαλερί που απαιτεί JPEG), θα αλλάξετε τη μορφή και ρητά **set jpeg quality**. Οι τιμές ποιότητας κυμαίνονται από `0` (χειρότερη) έως `100` (καλύτερη). Ένα τυπικό βέλτιστο είναι `85`, που προσφέρει καλό οπτικό αποτέλεσμα ενώ διατηρεί το αρχείο κάτω από 200 KB για μια σελίδα κανονικού μεγέθους.

```java
public static void convertToJpeg(String htmlPath, String jpegPath, int quality) throws Exception {
    ImageSaveOptions options = new ImageSaveOptions();
    // Switch to JPEG format
    options.setFormat(ImageSaveOptions.ImageFormat.Jpeg);
    // Here we finally use the JPEG quality setting
    options.setJpegQuality(quality);
    // Optional: you can still set DPI if you need larger images
    options.setResolution(150);
    Converter.convert(htmlPath, jpegPath, options);
}
```

**Γιατί η ρύθμιση της ποιότητας JPEG είναι σημαντική;** Το JPEG είναι μορφή με απώλειες· κάθε βήμα ποιότητας απορρίπτει περισσότερα δεδομένα. Αν το θέσετε πολύ χαμηλό, το κείμενο γίνεται θολό και εμφανίζονται τεχνουργήματα. Πολύ υψηλό, και χάνετε τα οφέλη της συμπίεσης. Η παράμετρος `quality` σας δίνει λεπτομερή έλεγχο.

## Πλήρες Παράδειγμα Εργασίας – Συνδυάζοντας Όλα τα Στοιχεία

Παρακάτω υπάρχει ένα αυτόνομο πρόγραμμα που μπορείτε να μεταγλωττίσετε με `javac HtmlToImageDemo.java` και να τρέξετε με `java HtmlToImageDemo`. Δείχνει και τις μετατροπές PNG και JPEG, πώς να ρυθμίσετε τη συμπίεση, και εκτυπώνει τα μεγέθη των παραγόμενων αρχείων ώστε να δείτε την επίδραση κάθε ρύθμισης.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.saving.ImageSaveOptions;
import java.nio.file.Files;
import java.nio.file.Path;

public class HtmlToImageDemo {
    public static void main(String[] args) {
        // Adjust these paths to point to your actual files
        String htmlFile = "YOUR_DIRECTORY/sample.html";
        String pngFile  = "YOUR_DIRECTORY/sample.png";
        String pngHiDpi = "YOUR_DIRECTORY/sample_300dpi.png";
        String jpegFile = "YOUR_DIRECTORY/sample.jpg";

        try {
            // 1️⃣ Convert to PNG (default compression)
            convertToPng(htmlFile, pngFile);
            System.out.println("PNG saved: " + pngFile + " (" + fileSize(pngFile) + " bytes)");

            // 2️⃣ Convert to PNG with higher DPI
            convertToPngWithDpi(htmlFile, pngHiDpi, 300);
            System.out.println("Hi‑DPI PNG saved: " + pngHiDpi + " (" + fileSize(pngHiDpi) + " bytes)");

            // 3️⃣ Convert to JPEG with quality 85
            convertToJpeg(htmlFile, jpegFile, 85);
            System.out.println("JPEG saved: " + jpegFile + " (" + fileSize(jpegFile) + " bytes)");

        } catch (Exception e) {
            System.err.println("Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ---------- Helper methods (see steps above) ----------
    public static void convertToPng(String htmlPath, String pngPath) throws Exception {
        ImageSaveOptions options = new ImageSaveOptions();
        options.setFormat(ImageSaveOptions.ImageFormat.Png);
        options.setPngCompressionLevel(9);
        options.setJpegQuality(85); // ignored for PNG, kept for completeness
        Converter.convert(htmlPath, pngPath, options);
    }

    public static void convertToPngWithDpi(String htmlPath, String pngPath, int dpi) throws Exception {
        ImageSaveOptions options = new ImageSaveOptions();
        options.setFormat(ImageSaveOptions.ImageFormat.Png);
        options.setPngCompressionLevel(9);
        options.setResolution(dpi);
        Converter.convert(htmlPath, pngPath, options);
    }

    public static void convertToJpeg(String htmlPath, String jpegPath, int quality) throws Exception {
        ImageSaveOptions options = new ImageSaveOptions();
        options.setFormat(ImageSaveOptions.ImageFormat.Jpeg);
        options.setJpegQuality(quality);
        options.setResolution(150);
        Converter.convert(htmlPath, jpegPath, options);
    }

    private static long fileSize(String path) throws Exception {
        return Files.size(Path.of(path));
    }
}
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
PNG saved: YOUR_DIRECTORY/sample.png (42,317 bytes)
Hi‑DPI PNG saved: YOUR_DIRECTORY/sample_300dpi.png (118,942 bytes)
JPEG saved: YOUR_DIRECTORY/sample.jpg (37,105 bytes)
```

Οι αριθμοί θα διαφέρουν ανάλογα με το περιεχόμενο του HTML, αλλά θα δείτε το PNG υψηλού DPI σημαντικά μεγαλύτερο από το κανονικό PNG, και το μέγεθος του JPEG να βρίσκεται μεταξύ των δύο λόγω της επιλεγμένης ποιότητας.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

* **Τι γίνεται αν το HTML μου αναφέρει εξωτερικά CSS ή εικόνες;**  
  Ο μετατροπέας ακολουθεί τις σχετικές URL βάσει της θέσης του αρχείου HTML. Βεβαιωθείτε ότι όλα τα assets βρίσκονται στον ίδιο φάκελο ή χρησιμοποιήστε απόλυτες URL. Αν αντιμετωπίσετε σφάλματα “resource not found”, περάστε ένα `baseUri` στην υπερφόρτωση του `Converter` που δέχεται ένα `java.net.URI`.

* **Μπορώ να αποδώσω μόνο ένα συγκεκριμένο στοιχείο (π.χ., ένα `<div>`);**  
  Ναι. Χρησιμοποιήστε `options.setCropRectangle(x, y, width, height)` για να περικόψετε την έξοδο σε μια περιοχή που ταιριάζει στο πλαίσιο του στοιχείου. Θα χρειαστεί να υπολογίσετε αυτές τις συντεταγμένες, ίσως μέσω ενός headless browser πρώτα.

* **Τι γίνεται με διαφανές φόντο;**  
  Το PNG υποστηρίζει διαφάνεια έτοιμο. Αν χρειάζεστε στερεό φόντο για JPEG, ορίστε `options.setBackground

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω μαθήματα καλύπτουν στενά σχετικά θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε σε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Convert HTML to PNG with Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-png/)
- [How to Convert HTML to JPEG Using Aspose.HTML for Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)
- [HTML to Image Java – Convert HTML to TIFF with Aspose.HTML](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-tiff/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}