---
category: general
date: 2026-01-14
description: πώς να ορίσετε dpi κατά τη μετατροπή ενός URL σε PNG. Μάθετε πώς να αποδίδετε
  HTML σε PNG, να ορίζετε το μέγεθος του viewport και να αποθηκεύετε HTML ως PNG χρησιμοποιώντας
  το Aspose.HTML σε Java.
draft: false
keywords:
- how to set dpi
- render html to png
- convert url to png
- set viewport size
- save html as png
language: el
og_description: πώς να ορίσετε dpi κατά τη μετατροπή ενός URL σε PNG. Οδηγός βήμα‑προς‑βήμα
  για την απόδοση HTML σε PNG, τον έλεγχο του μεγέθους του viewport και την αποθήκευση
  του HTML ως PNG χρησιμοποιώντας το Aspose.HTML.
og_title: πώς να ορίσετε dpi – Απόδοση HTML σε PNG με το AsposeHTML
tags:
- AsposeHTML
- Java
- image rendering
title: πώς να ορίσετε dpi – Απόδοση HTML σε PNG με το AsposeHTML
url: /el/java/conversion-html-to-various-image-formats/how-to-set-dpi-render-html-to-png-with-asposehtml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να ορίσετε dpi – Απόδοση HTML σε PNG με AsposeHTML

Έχετε αναρωτηθεί ποτέ **πώς να ορίσετε dpi** για μια εικόνα τύπου screenshot που δημιουργείται από μια ιστοσελίδα; Ίσως χρειάζεστε ένα PNG 300 DPI για εκτύπωση, ή μια μικρή μικρογραφία χαμηλής ανάλυσης για μια εφαρμογή κινητού. Σε κάθε περίπτωση, το κόλπο είναι να πείτε στη μηχανή απόδοσης ποιο λογικό DPI θέλετε, και στη συνέχεια να αφήσετε αυτήν να κάνει τη βαριά δουλειά.  

Σε αυτό το tutorial θα πάρουμε ένα ζωντανό URL, θα το αποδώσουμε σε αρχείο PNG, **ορίσουμε το μέγεθος του viewport**, θα προσαρμόσουμε το DPI, και τελικά **αποθηκεύσουμε το HTML ως PNG**—όλα με το Aspose.HTML για Java. Χωρίς εξωτερικά προγράμματα περιήγησης, χωρίς ακατάστατα εργαλεία γραμμής εντολών—απλώς καθαρός κώδικας Java που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle.

> **Συμβουλή επαγγελματία:** Αν θέλετε μόνο μια γρήγορη μικρογραφία, μπορείτε να διατηρήσετε το DPI στα 96 DPI (η προεπιλογή για τις περισσότερες οθόνες). Για περιουσιακά στοιχεία έτοιμα για εκτύπωση, αυξήστε το σε 300 DPI ή περισσότερο.

![παράδειγμα ορισμού dpi](https://example.com/images/how-to-set-dpi.png "παράδειγμα ορισμού dpi")

## Τι Θα Χρειαστείτε

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK).  
- **Aspose.HTML for Java** 24.10 ή νεότερη. Μπορείτε να την κατεβάσετε από το Maven Central:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>24.10</version>
</dependency>
```

- Σύνδεση στο διαδίκτυο για λήψη της σελίδας-στόχου (το παράδειγμα χρησιμοποιεί `https://example.com/sample.html`).  
- Δικαίωμα εγγραφής στο φάκελο εξόδου.

Αυτό είναι όλο—χωρίς Selenium, χωρίς headless Chrome. Το Aspose.HTML κάνει την απόδοση εντός της διαδικασίας, πράγμα που σημαίνει ότι παραμένετε μέσα στη JVM και αποφεύγετε το κόστος εκκίνησης ενός προγράμματος περιήγησης.

## Βήμα 1 – Φόρτωση του HTML Εγγράφου από URL

Αρχικά δημιουργούμε μια παρουσία `HTMLDocument` που δείχνει στη σελίδα που θέλουμε να καταγράψουμε. Ο κατασκευαστής κατεβάζει αυτόματα το HTML, το αναλύει και προετοιμάζει το DOM.

```java
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

// Load the remote page
HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");
```

*Γιατί είναι σημαντικό:* Φορτώνοντας το έγγραφο απευθείας, παρακάμπτετε την ανάγκη για ξεχωριστό HTTP client. Το Aspose.HTML σέβεται τις ανακατευθύνσεις, τα cookies, και ακόμη και την βασική πιστοποίηση αν ενσωματώσετε διαπιστευτήρια στο URL.

## Βήμα 2 – Δημιουργία Sandbox με το Επιθυμητό DPI και Viewport

Ένα **sandbox** είναι ο τρόπος του Aspose.HTML να μιμηθεί ένα περιβάλλον προγράμματος περιήγησης. Εδώ του λέμε να προσποιηθεί ότι είναι μια οθόνη 1280 × 720 και, κρίσιμα, ορίζουμε το **device DPI**. Η αλλαγή του DPI αλλάζει την πυκνότητα εικονοστοιχείων της αποδοθείσας εικόνας χωρίς να τροποποιεί το λογικό μέγεθος.

```java
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;

// Create a sandbox that simulates a 1280×720 screen at 96 DPI
SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
        .setViewportSize(1280, 720)          // width, height in pixels
        .setDeviceDpi(96)                    // logical DPI (change to 300 for print)
        .setUserAgent("AsposeHTML/24.10")    // optional custom user‑agent
        .build();

// Apply the sandbox to the document
htmlDoc.setSandbox(sandbox);
```

*Γιατί μπορεί να θέλετε να προσαρμόσετε αυτές τις τιμές:*  
- **Το μέγεθος του viewport** ελέγχει τη συμπεριφορά των CSS media queries (`@media (max-width: …)`).  
- **Το Device DPI** επηρεάζει το φυσικό μέγεθος της εικόνας όταν εκτυπώνεται. Μια εικόνα 96 DPI φαίνεται καλά στις οθόνες· μια εικόνα 300 DPI διατηρεί την ευκρίνεια στο χαρτί.  

Αν χρειάζεστε μια τετράγωνη μικρογραφία, απλώς αλλάξτε `setViewportSize(500, 500)` και διατηρήστε το DPI χαμηλό.

## Βήμα 3 – Επιλογή PNG ως Μορφή Εξόδου

Το Aspose.HTML υποστηρίζει διάφορες μορφές raster (PNG, JPEG, BMP, GIF). Το PNG είναι loss‑less, κάτι που το καθιστά ιδανικό για screenshots όπου θέλετε κάθε εικονοστοιχείο να διατηρείται.

```java
import com.aspose.html.rendering.ImageSaveOptions;

// Prepare PNG save options
ImageSaveOptions pngOptions = new ImageSaveOptions();
pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);
```

Μπορείτε επίσης να ρυθμίσετε το επίπεδο συμπίεσης (`pngOptions.setCompressionLevel(9)`) αν σας ανησυχεί το μέγεθος του αρχείου.

## Βήμα 4 – Απόδοση και Αποθήκευση της Εικόνας

Τώρα λέμε στο έγγραφο να **αποθηκεύσει** τον εαυτό του ως εικόνα. Η μέθοδος `save` δέχεται μια διαδρομή αρχείου και τις προηγουμένως ρυθμισμένες επιλογές.

```java
// Define the output path (replace with your own directory)
String outputPath = "YOUR_DIRECTORY/sandboxed.png";

// Render the document to a PNG file
htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

System.out.println("Rendering completed.");
```

Όταν το πρόγραμμα ολοκληρωθεί, θα βρείτε ένα αρχείο PNG στο `YOUR_DIRECTORY/sandboxed.png`. Ανοίξτε το—αν έχετε ορίσει το DPI σε 300, τα μεταδεδομένα της εικόνας θα το αντικατοπτρίζουν, παρόλο που οι διαστάσεις των εικονοστοιχείων παραμένουν 1280 × 720.

## Βήμα 5 – Επαλήθευση του DPI (Προαιρετικό αλλά Χρήσιμο)

Αν θέλετε να ελέγξετε ξανά ότι το DPI εφαρμόστηκε πραγματικά, μπορείτε να διαβάσετε τα μεταδεδομένα PNG με μια ελαφριά βιβλιοθήκη όπως η **metadata‑extractor**:

```java
import com.drew.imaging.ImageMetadataReader;
import com.drew.metadata.png.PngDirectory;

File pngFile = new File(outputPath);
var metadata = ImageMetadataReader.readMetadata(pngFile);
var pngDir = metadata.getFirstDirectoryOfType(PngDirectory.class);
int dpi = pngDir.getInt(PngDirectory.TAG_PIXELS_PER_UNIT_X);
System.out.println("DPI stored in PNG: " + dpi);
```

Θα πρέπει να δείτε `300` (ή ό,τι έχετε ορίσει) να εκτυπώνεται στην κονσόλα. Αυτό το βήμα δεν απαιτείται για την απόδοση, αλλά είναι ένας γρήγορος έλεγχος λογικής, ειδικά όταν δημιουργείτε περιουσιακά στοιχεία για διαδικασία εκτύπωσης.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### “Τι γίνεται αν η σελίδα χρησιμοποιεί JavaScript για φόρτωση περιεχομένου;”

Το Aspose.HTML εκτελεί ένα **περιορισμένο υποσύνολο** του JavaScript. Για τις περισσότερες στατικές ιστοσελίδες λειτουργεί αμέσως. Αν η σελίδα εξαρτάται έντονα από client‑side frameworks (React, Angular, Vue), ίσως χρειαστεί να προ‑αποδώσετε τη σελίδα ή να χρησιμοποιήσετε ένα headless browser. Ωστόσο, η ρύθμιση DPI λειτουργεί με τον ίδιο τρόπο μόλις το DOM είναι έτοιμο.

### “Μπορώ να αποδώσω PDF αντί για PNG;”

Απόλυτα. Αντικαταστήστε το `ImageSaveOptions` με `PdfSaveOptions` και αλλάξτε την επέκταση εξόδου σε `.pdf`. Η ρύθμιση DPI εξακολουθεί να επηρεάζει την rasterized εμφάνιση τυχόν ενσωματωμένων εικόνων.

### “Τι γίνεται με τα υψηλής ανάλυσης screenshots για οθόνες retina;”

Απλώς διπλασιάστε τις διαστάσεις του viewport διατηρώντας το DPI στα 96 DPI, ή διατηρήστε το viewport και αυξήστε το DPI σε 192. Το παραγόμενο PNG θα περιέχει δύο φορές περισσότερα εικονοστοιχεία, προσφέροντας αυτή τη διακριτική αίσθηση retina.

### “Χρειάζεται να καθαρίσω πόρους;”

`HTMLDocument` υλοποιεί το `AutoCloseable`. Σε μια παραγωγική εφαρμογή, τυλίξτε το σε ένα μπλοκ try‑with‑resources:

```java
try (HTMLDocument doc = new HTMLDocument(url)) {
    // configure sandbox, render, etc.
}
```

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αντικαταστήστε το `YOUR_DIRECTORY` με έναν πραγματικό φάκελο στο μηχάνημά σας.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.ImageSaveOptions;
import com.aspose.html.rendering.SandboxConfiguration;
import com.aspose.html.rendering.SandboxConfigurationBuilder;
import java.nio.file.Paths;

public class RenderHtmlToPng {
    public static void main(String[] args) {
        // 1️⃣ Load the HTML document from a URL
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com/sample.html");

        // 2️⃣ Create a sandbox – set viewport size and DPI
        SandboxConfiguration sandbox = new SandboxConfigurationBuilder()
                .setViewportSize(1280, 720)   // width × height in pixels
                .setDeviceDpi(96)             // change to 300 for print‑ready PNG
                .setUserAgent("AsposeHTML/24.10")
                .build();

        htmlDoc.setSandbox(sandbox); // apply sandbox to the document

        // 3️⃣ Prepare PNG save options
        ImageSaveOptions pngOptions = new ImageSaveOptions();
        pngOptions.setFormat(ImageSaveOptions.ImageFormat.Png);

        // 4️⃣ Render and save
        String outputPath = "YOUR_DIRECTORY/sandboxed.png";
        htmlDoc.save(Paths.get(outputPath).toString(), pngOptions);

        System.out.println("Rendering completed. Check: " + outputPath);
    }
}
```

Εκτελέστε την κλάση, και θα λάβετε ένα PNG που σέβεται τη ρύθμιση **πώς να ορίσετε dpi** που καθορίσατε.

## Συμπέρασμα

Περπατήσαμε μέσα από το **πώς να ορίσετε dpi** όταν **αποδίδετε HTML σε PNG**, καλύψαμε το βήμα **ορισμού μεγέθους viewport** και σας δείξαμε πώς να **αποθηκεύσετε HTML ως PNG** χρησιμοποιώντας το Aspose.HTML για Java. Τα βασικά συμπεράσματα είναι:

- Χρησιμοποιήστε ένα **sandbox** για έλεγχο DPI και viewport.  
- Επιλέξτε τις σωστές **ImageSaveOptions** για lossless έξοδο.  
- Επαληθεύστε τα μεταδεδομένα DPI αν χρειάζεται να εγγυηθείτε την ποιότητα εκτύπωσης.

Από εδώ μπορείτε να πειραματιστείτε με διαφορετικές τιμές DPI, μεγαλύτερα viewports, ή ακόμη και να επεξεργαστείτε κατά παρτίδες μια λίστα URLs. Θέλετε να μετατρέψετε ολόκληρη μια ιστοσελίδα σε μικρογραφίες PNG; Απλώς κάντε βρόχο πάνω σε έναν πίνακα URLs και επαναχρησιμοποιήστε την ίδια διαμόρφωση sandbox.

Καλή απόδοση, και εύχομαι οι στιγμιότυπές σας να είναι πάντα pixel‑perfect!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}