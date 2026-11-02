---
category: general
date: 2026-03-04
description: Μάθετε πώς να ορίζετε το DPI κατά τη μετατροπή HTML σε PNG. Αυτός ο οδηγός
  καλύπτει επίσης την εξαγωγή HTML ως PNG, την αποθήκευση HTML ως PNG και τη δημιουργία
  PNG από HTML χρησιμοποιώντας το Aspose.HTML για Java.
draft: false
keywords:
- how to set dpi
- convert html to png
- export html as png
- save html as png
- generate png from html
language: el
og_description: Πώς να ορίσετε DPI για τη μετατροπή HTML σε PNG εξηγείται. Ακολουθήστε
  τον οδηγό βήμα‑βήμα για να εξάγετε HTML ως PNG, να αποθηκεύσετε HTML ως PNG και
  να δημιουργήσετε PNG από HTML.
og_title: Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG
tags:
- Aspose.HTML
- Java
- Image Conversion
title: Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG
url: /el/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-html-to-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε DPI κατά τη μετατροπή HTML σε PNG

Έχετε αναρωτηθεί ποτέ **πώς να ορίσετε DPI** για μια ραστερ εικόνα που δημιουργείτε από μια ιστοσελίδα; Ίσως δημιουργείτε ένα εργαλείο αναφορών, μια υπηρεσία μικρογραφιών ή μια αλυσίδα παραγωγής περιουσιακών στοιχείων έτοιμων για εκτύπωση — σε όλα αυτά τα σενάρια ξεκινάτε συνήθως με ένα έγγραφο HTML που πρέπει να μετατραπεί σε PNG υψηλής ανάλυσης.  

Τα καλά νέα είναι ότι το Aspose.HTML for Java κάνει την **μετατροπή HTML σε PNG** παιχνιδάκι, και μπορείτε να ελέγξετε το DPI με μόνο μία γραμμή κώδικα. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, από τη φόρτωση του αρχείου HTML μέχρι την εξαγωγή του ως PNG στα 300 DPI, αγγίζοντας επίσης σχετικές εργασίες όπως **export HTML as PNG**, **save HTML as PNG**, και **generate PNG from HTML**.

## Τι θα μάθετε

- Πώς να ρυθμίσετε το DPI (dots per inch) για την εικόνα εξόδου.
- Τη διαφορά μεταξύ DPI, ανάλυσης και ποιότητας συμπίεσης.
- Ένα πλήρες, εκτελέσιμο παράδειγμα Java που μπορείτε να αντιγράψετε‑και‑επικολλήσετε.
- Συνηθισμένα προβλήματα (π.χ. ελλιπείς γραμματοσειρές, μεγάλες σελίδες) και πώς να τα αποφύγετε.
- Γρήγορες συμβουλές για την προσαρμογή της εξόδου όταν χρειάζεται να **convert HTML to PNG** σε διαφορετικά περιβάλλοντα.

### Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη στο σύστημα σας.
- Βιβλιοθήκη Aspose.HTML for Java (η πιο πρόσφατη έκδοση μέχρι Μάρτιο 2026). Μπορείτε να την προσθέσετε από το Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

- Ένα απλό αρχείο `input.html` που θέλετε να μετατρέψετε σε εικόνα PNG.

---

## Πώς να ορίσετε DPI για τη μετατροπή HTML σε PNG

![Διάγραμμα που δείχνει τη ρύθμιση DPI στον κώδικα – πώς να ορίσετε dpi όταν μετατρέπετε HTML σε PNG](https://example.com/images/dpi-setting.png)

Το **κύριο βήμα** που ελέγχει την ευκρίνεια της εικόνας είναι η ιδιότητα `Resolution` του `ImageSaveOptions`. Παρακάτω θα αναλύσουμε τη διαδικασία σε μικρά βήματα.

### Βήμα 1: Ορισμός διαδρομών εισόδου και εξόδου (convert html to png)

Πρώτα, πείτε στον μετατροπέα πού βρίσκεται το πηγαίο HTML και πού πρέπει να γραφτεί το PNG.

```java
// Step 1 – file locations
String htmlFilePath = "YOUR_DIRECTORY/input.html";
String pngFilePath  = "YOUR_DIRECTORY/output.png";
```

> **Γιατί είναι σημαντικό:** Η σκληρή κωδικοποίηση διαδρομών είναι αποδεκτή για μια επίδειξη, αλλά στην παραγωγή πιθανότατα θα τις παίρνετε από ρυθμίσεις ή παραμέτρους γραμμής εντολών. Αυτό κρατά τον κώδικα ευέλικτο για οποιαδήποτε ροή εργασίας **save HTML as PNG**.

### Βήμα 2: Δημιουργία ImageSaveOptions και ορισμός DPI (how to set dpi)

Τώρα δημιουργούμε ένα `ImageSaveOptions` για PNG και ορίζουμε το DPI στα 300. Το DPI καθορίζει πόσα pixel θα συσσωρευτούν σε κάθε ίντσα όταν η εικόνα εκτυπώνεται ή εμφανίζεται στο φυσικό της μέγεθος.

```java
// Step 2 – configure PNG options
ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
saveOptions.setResolution(300);   // <-- This is the DPI you asked for
saveOptions.setQuality(95);       // PNG compression (0‑100); higher = larger file, better fidelity
```

> **Εξήγηση:**  
> - `setResolution(300)` λέει στο Aspose.HTML να αποδώσει τη σελίδα στα 300 dots per inch.  
> - `setQuality(95)` είναι προαιρετικό για PNG· ελέγχει το επίπεδο συμπίεσης ZLIB. Μπορείτε να το μειώσετε για μικρότερα αρχεία αν δεν χρειάζεστε κάθε pixel τέλειο.

### Βήμα 3: Εκτέλεση της μετατροπής (export html as png)

Με τις επιλογές έτοιμες, η πραγματική μετατροπή είναι μια γραμμή κώδικα.

```java
// Step 3 – run the conversion
Converter.convert(htmlFilePath, pngFilePath, saveOptions);
```

> **Τι συμβαίνει στο παρασκήνιο;** Το Aspose.HTML αναλύει το HTML, εφαρμόζει το CSS, διατάσσει το DOM, ραστερίζει τη διάταξη στο ζητούμενο DPI και τέλος γράφει ένα αρχείο PNG. Αν χρειαστεί να **generate PNG from HTML** σε μια web υπηρεσία, μπορείτε να αντικαταστήσετε τις διαδρομές αρχείων με ροές (streams).

### Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα παραπάνω, εδώ είναι μια πλήρης κλάση Java που μπορείτε να μεταγλωττίσετε και να τρέξετε.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.*;
import com.aspose.html.saving.*;

public class ConvertHtmlToPngWithDpi {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the input HTML file and the output PNG file
        String htmlFilePath = "YOUR_DIRECTORY/input.html";
        String pngFilePath  = "YOUR_DIRECTORY/output.png";

        // Step 2: Create image save options for PNG and configure high‑resolution output
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        saveOptions.setResolution(300);   // Set resolution to 300 DPI (how to set dpi)
        saveOptions.setQuality(95);       // PNG compression quality (0‑100)

        // Step 3: Perform the conversion from HTML to PNG using the configured options
        Converter.convert(htmlFilePath, pngFilePath, saveOptions);

        System.out.println("Conversion complete! PNG saved at " + pngFilePath);
    }
}
```

Τρέξτε το πρόγραμμα και θα βρείτε ένα καθαρό PNG 300 DPI στη θέση που ορίσατε. Ανοίξτε το σε οποιονδήποτε προβολέα εικόνων και ελέγξτε τις ιδιότητες – το DPI πρέπει να εμφανίζει **300**.

---

## Συχνές ερωτήσεις & Ακραίες περιπτώσεις

### Τι γίνεται αν η ρύθμιση DPI φαίνεται να αγνοείται;

- **Βεβαιωθείτε ότι χρησιμοποιείτε πρόσφατη έκδοση Aspose.HTML.** Παλαιότερες εκδόσεις αγνοούσαν το `Resolution` για PNG.
- **Ελέγξτε το μέγεθος του πηγαίου HTML.** Μια μικρή σελίδα HTML που αποδίδεται στα 300 DPI μπορεί να παράγει ακόμα μικρή διάσταση pixel. Το DPI επηρεάζει μόνο τον παράγοντα κλιμάκωσης, όχι το εγγενές μέγεθος της σελίδας.

### Πώς διαφέρει το DPI από τις διαστάσεις της εικόνας;

Το DPI είναι μια *φυσική* μέτρηση (dots per inch). Το πραγματικό πλάτος/ύψος σε pixel υπολογίζεται ως:

```
pixel width  = CSS width  * DPI / 96
pixel height = CSS height * DPI / 96
```

Αν το σώμα του HTML είναι 800 px πλάτος, στα 300 DPI το PNG εξόδου θα είναι περίπου 2500 px πλάτος (800 × 300 ÷ 96).

### Μπορώ να χρησιμοποιήσω άλλες μορφές (JPEG, BMP) διατηρώντας το DPI;

Απόλυτα. Απλώς αλλάξτε το `SaveFormat.PNG` σε `SaveFormat.JPEG` (ή `BMP`) και κρατήστε το `setResolution`. Θυμηθείτε ότι το JPEG επίσης σέβεται τη ρύθμιση `Quality`, η οποία αντιστοιχεί στο επίπεδο συμπίεσης.

### Τι γίνεται με γραμματοσειρές που δεν είναι εγκατεστημένες στον διακομιστή;

Το Aspose.HTML θα επιστρέψει σε προεπιλεγμένη γραμματοσειρά, κάτι που μπορεί να αλλάξει τη διάταξη. Για να εξασφαλίσετε ταυτόσημη απόδοση, ενσωματώστε τις απαιτούμενες γραμματοσειρές χρησιμοποιώντας `FontSettings`:

```java
FontSettings fontSettings = new FontSettings();
fontSettings.setFontFolder("YOUR_FONT_DIRECTORY", true);
saveOptions.setFontSettings(fontSettings);
```

### Δημιουργία πολλαπλών PNG σε batch

Αν χρειάζεται να **generate PNG from HTML** για πολλά αρχεία, τυλίξτε τη λογική μετατροπής σε βρόχο και επαναχρησιμοποιήστε ένα ενιαίο αντικείμενο `ImageSaveOptions`. Αυτό μειώνει την κατανάλωση μνήμης και επιταχύνει την επεξεργασία.

```java
for (Path htmlPath : Files.newDirectoryStream(Paths.get("batch_html"))) {
    String outPath = htmlPath.toString().replace(".html", ".png");
    Converter.convert(htmlPath.toString(), outPath, saveOptions);
}
```

---

## Pro Tips για εξαγωγή PNG υψηλής ποιότητας

1. **Χρησιμοποιήστε CSS φιλικό προς vectors** (π.χ. `transform: scale(1)`) για να αποφύγετε τα artefacts anti‑aliasing σε υψηλό DPI.  
2. **Ορίστε χρώμα φόντου** αν το HTML σας έχει διαφανή στοιχεία και χρειάζεστε στερεό καμβά:

   ```java
   saveOptions.setBackgroundColor(Color.WHITE);
   ```

3. **Αποφύγετε ενσωματωμένες εικόνες base64** μεγαλύτερες από λίγα MB· μπορούν να αυξήσουν τη χρήση μνήμης κατά τη μετατροπή.  
4. **Δοκιμάστε σε διαφορετικές οθόνες DPI** (π.χ. οθόνες 72 DPI vs. εκτυπωτές 300 DPI) για να βεβαιωθείτε ότι η οπτική ποιότητα ανταποκρίνεται στις προσδοκίες.  
5. **Εκμεταλλευτείτε το `setPageSize()`** αν θέλετε το PNG να ταιριάζει με συγκεκριμένο μέγεθος εκτύπωσης (A4, Letter κ.λπ.) ανεξάρτητα από τις αρχικές διαστάσεις του HTML.

---

## Συμπέρασμα

Καλύψαμε **πώς να ορίσετε DPI** όταν **convert HTML to PNG** χρησιμοποιώντας το Aspose.HTML for Java, παρουσιάσαμε ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα, και εξετάσαμε σχετικές εργασίες όπως **export HTML as PNG**, **save HTML as PNG**, και **generate PNG from HTML**. Με το `ImageSaveOptions.setResolution` ελέγχετε τη φυσική ευκρίνεια της εξόδου, ενώ το `setQuality` σας επιτρέπει να ισορροπήσετε το μέγεθος του αρχείου με την οπτική πιστότητα.

Τι θα κάνετε μετά; Δοκιμάστε να αλλάξετε τη μορφή PNG σε JPEG για να δείτε πώς η συμπίεση αλληλεπιδρά με το DPI, ή πειραματιστείτε με batch processing για **convert HTML to PNG** σε κλίμακα. Μπορείτε επίσης να προσθέσετε υδατογραφήματα ή προσαρμοσμένα μεταδεδομένα — και τα δύο υποστηρίζονται από το πλούσιο API του Aspose.HTML.

Έχετε κάποιο δύσκολο σενάριο που δεν καλύφθηκε; Αφήστε ένα σχόλιο και θα το λύσουμε μαζί. Καλό κώδικα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}