---
category: general
date: 2026-03-17
description: Μάθετε πώς να αποθηκεύετε μια σελίδα HTML ως PNG γρήγορα. Αυτός ο οδηγός
  δείχνει πώς να αποδίδετε HTML σε PNG και να ορίζετε το μέγεθος του viewport σε Java
  χρησιμοποιώντας το Aspose.HTML.
draft: false
keywords:
- save html page as png
- how to render html to png
- set viewport size java
- Aspose.HTML Java rendering
- export HTML as image
language: el
og_description: Αποθηκεύστε τη σελίδα HTML ως PNG με Java. Ακολουθήστε αυτό το σεμινάριο
  για να μάθετε πώς να αποδίδετε HTML σε PNG και να ορίσετε το μέγεθος του viewport
  με Java χρησιμοποιώντας το Aspose.HTML.
og_title: Αποθήκευση σελίδας HTML ως PNG σε Java – Οδηγός βήμα‑προς‑βήμα
tags:
- Java
- AsposeHTML
- Image Rendering
title: Αποθήκευση σελίδας HTML ως PNG σε Java – Πλήρης οδηγός
url: /el/java/conversion-html-to-various-image-formats/save-html-page-as-png-in-java-complete-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αποθήκευση σελίδας HTML ως PNG σε Java – Πλήρης Οδηγός

Έχετε χρειαστεί ποτέ να **αποθηκεύσετε σελίδα HTML ως PNG** αλλά δεν ήξερατε από πού να ξεκινήσετε; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν χρειάζονται ένα γρήγορο στιγμιότυπο μιας ιστοσελίδας για αναφορές, μικρογραφίες ή δοκιμές. Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από το **πώς να αποδώσετε HTML σε PNG** χρησιμοποιώντας το Aspose.HTML for Java, και θα σας δείξουμε επίσης πώς να **ορίσετε το μέγεθος του viewport σε Java** ώστε το αποτέλεσμα να φαίνεται ακριβώς όπως το περιμένετε.

Θα καλύψουμε τα πάντα, από την εγκατάσταση της βιβλιοθήκης μέχρι τη ρύθμιση του λόγου συσκευής (device pixel ratio), και στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα που παράγει ένα καθαρό αρχείο PNG από οποιοδήποτε URL. Χωρίς ασαφείς αναφορές, μόνο μια πλήρης, αυτόνομη λύση.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- Java 11 ή νεότερη (η τρέχουσα LTS έκδοση λειτουργεί τέλεια)
- Maven ή Gradle για διαχείριση εξαρτήσεων (θα δείξουμε το απόσπασμα για Maven)
- Σύνδεση στο διαδίκτυο για το δείγμα URL (`https://example.com`) ή οποιαδήποτε σελίδα θέλετε να καταγράψετε
- Έναν εγγράψιμο φάκελο στον δίσκο όπου θα αποθηκευτεί το PNG

Αυτό είναι όλο—χωρίς επιπλέον SDKs, χωρίς εγγενή binaries. Το Aspose.HTML αναλαμβάνει τη βαριά δουλειά εσωτερικά.

## Βήμα 1: Προσθήκη Εξάρτησης Aspose.HTML

Πρώτα, προσθέστε τη βιβλιοθήκη Aspose.HTML στο έργο σας. Αν χρησιμοποιείτε Maven, προσθέστε το παρακάτω στο `pom.xml`:

```xml
<!-- Aspose.HTML for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>22.12</version> <!-- Use the latest stable version -->
</dependency>
```

Οι χρήστες Gradle μπορούν να τοποθετήσουν αυτό στο `build.gradle`:

```groovy
implementation 'com.aspose:aspose-html:22.12'
```

> **Pro tip:** Ελέγξτε τις [σημειώσεις έκδοσης του Aspose.HTML](https://docs.aspose.com/html/java/) για την πιο πρόσφατη έκδοση· τα νεότερα builds συχνά περιλαμβάνουν βελτιώσεις απόδοσης για την απόδοση.

## Βήμα 2: Φόρτωση του HTML Document από URL

Τώρα θα δημιουργήσουμε ένα αντικείμενο `HTMLDocument` που δείχνει στη σελίδα που θέλετε να καταγράψετε. Αυτό το βήμα είναι η καρδιά του **πώς να αποδώσετε HTML σε PNG** επειδή η βιβλιοθήκη αναλύει το markup και δημιουργεί ένα DOM εσωτερικά.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class SandboxRenderTutorial {
    public static void main(String[] args) throws Exception {
        // Load an HTML document from a web address
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com");
```

Αν προτιμάτε τοπικό αρχείο, απλώς αντικαταστήστε τη συμβολοσειρά URL με μια διαδρομή αρχείου όπως `"file:///C:/mypage.html"`.

## Βήμα 3: Διαμόρφωση του Sandbox και Ορισμός Μεγέθους Viewport

Το sandbox απομονώνει την απόδοση από το κύριο νήμα της εφαρμογής σας και σας επιτρέπει να ορίσετε τις εικονικές χαρακτηριστικές της συσκευής. Εδώ είναι που **ορίζουμε το μέγεθος του viewport σε Java** για να ελέγξουμε τις διαστάσεις του παραγόμενου bitmap.

```java
        // Configure a sandboxed rendering device (viewport 1280×800, DPR 2.0)
        RenderingDeviceSettings deviceSettings = new RenderingDeviceSettings();
        deviceSettings.setViewportSize(new Size(1280, 800));   // <-- set viewport size Java
        deviceSettings.setDevicePixelRatio(2.0);              // High‑DPI rendering
        deviceSettings.setUserAgent("AsposeHTML/1.0");        // Optional but useful

        // Attach the sandbox to the document so rendering uses the settings above
        DocumentSandbox sandbox = new DocumentSandbox(deviceSettings);
        htmlDoc.setSandbox(sandbox);
```

Γιατί να χρησιμοποιήσετε sandbox; Αποτρέπει παρενέργειες όπως αιτήματα δικτύου που διαρρέουν εκτός του πλαισίου απόδοσης και παρέχει ντετερμινιστικά αποτελέσματα—ιδιαίτερα σημαντικό όταν τρέχετε τον κώδικα σε CI server.

## Βήμα 4: Προετοιμασία Επιλογών Αποθήκευσης Εικόνας

Το Aspose.HTML μπορεί να εξάγει σε πολλές μορφές (PNG, JPEG, BMP κ.λπ.). Θα διαμορφώσουμε το `ImageSaveOptions` ώστε να στοχεύει την πρώτη σελίδα του εγγράφου και να ορίσουμε το PNG ως μορφή εξόδου.

```java
        // Prepare image save options to export the first page as PNG
        try (ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG)) {
            pngOptions.setPageNumber(1); // Render only the first page
```

Μπορείτε να αλλάξετε το `setPageNumber` σε `2` ή `-1` (όλες οι σελίδες) αν χρειάζεστε ακολουθία εικόνων πολλαπλών σελίδων.

## Βήμα 5: Απόδοση και Αποθήκευση του Αρχείου PNG

Τέλος, καλέστε `save` στο `HTMLDocument`. Η μέθοδος σέβεται όλες τις ρυθμίσεις sandbox που εφαρμόσαμε νωρίτερα, παράγοντας ένα pixel‑perfect στιγμιότυπο.

```java
            // Render and save the page to a file
            String outputPath = "rendered_page.png"; // adjust the path as needed
            htmlDoc.save(outputPath, pngOptions);
            System.out.println("✅ PNG saved to: " + outputPath);
        }
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα δείτε ένα μήνυμα στην κονσόλα που επιβεβαιώνει τη θέση του αρχείου. Ανοίξτε το PNG—θα δείτε την ακριβή οπτική αναπαράσταση του `https://example.com` σε 1280 × 800 pixels, αποδομένο με λόγο συσκευής 2.0 (οπότε η εικόνα φαίνεται οξεία σε οθόνες Retina).

### Αναμενόμενο Αποτέλεσμα

```
✅ PNG saved to: rendered_page.png
```

Το παραγόμενο `rendered_page.png` θα είναι ένα αρχείο εικόνας υψηλής ποιότητας, έτοιμο για ενσωμάτωση σε αναφορές, email ή προεπισκοπήσεις UI.

## Πώς να Αποδώσετε HTML σε PNG – Συνηθισμένες Παραλλαγές

### Απόδοση με Διαφορετικό Μέγεθος Σελίδας

Αν χρειάζεστε διαφορετική διάσταση, απλώς αλλάξτε τις τιμές του `Size`:

```java
deviceSettings.setViewportSize(new Size(1920, 1080)); // Full HD
```

### Αλλαγή του Λόγου Συσκευής (Device Pixel Ratio)

Ένας DPR `1.0` δίνει μια εικόνα τυπικής ανάλυσης, ενώ `3.0` μιμείται πολύ πυκνές οθόνες. Ρυθμίστε το όπως χρειάζεται:

```java
deviceSettings.setDevicePixelRatio(3.0);
```

### Προσθήκη Προσαρμοσμένων Headers ή Cookies

Μερικές φορές η στόχευση σελίδα απαιτεί έλεγχο ταυτότητας. Μπορείτε να εισάγετε headers πριν τη φόρτωση:

```java
htmlDoc.getHeaders().add("Authorization", "Bearer YOUR_TOKEN");
```

### Απόδοση Πολλαπλών Σελίδων

Για εξαγωγή κάθε σελίδας ως ξεχωριστό PNG, κάντε βρόχο πάνω στον αριθμό σελίδων:

```java
int totalPages = htmlDoc.getPages().size();
for (int i = 1; i <= totalPages; i++) {
    pngOptions.setPageNumber(i);
    htmlDoc.save("page_" + i + ".png", pngOptions);
}
```

## Συμβουλές Επίλυσης Προβλημάτων

- **Κενή Εικόνα:** Βεβαιωθείτε ότι το URL είναι προσβάσιμο και ότι το sandbox έχει πρόσβαση στο διαδίκτυο. Αν βρίσκεστε πίσω από proxy, ορίστε τις ιδιότητες proxy του JVM (`-Dhttp.proxyHost=…`).
- **Σφάλματα Out‑of‑Memory:** Η απόδοση πολύ μεγάλων viewport μπορεί να καταναλώσει πολύ RAM. Μειώστε το μέγεθος του viewport ή το DPR.
- **Λείπουν Γραμματοσειρές:** Το Aspose.HTML χρησιμοποιεί τις συστημικές γραμματοσειρές εξ ορισμού. Αν η σελίδα σας βασίζεται σε web fonts, βεβαιωθείτε ότι είναι προσβάσιμα ή ενσωματώστε τα μέσω CSS `@font-face`.

## Πλήρες Παράδειγμα Εργασίας (Όλος ο Κώδικας σε Ένα Σημείο)

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class SandboxRenderTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the HTML document
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com");

        // 2️⃣ Set up sandbox with viewport size (set viewport size java)
        RenderingDeviceSettings deviceSettings = new RenderingDeviceSettings();
        deviceSettings.setViewportSize(new Size(1280, 800));
        deviceSettings.setDevicePixelRatio(2.0);
        deviceSettings.setUserAgent("AsposeHTML/1.0");
        DocumentSandbox sandbox = new DocumentSandbox(deviceSettings);
        htmlDoc.setSandbox(sandbox);

        // 3️⃣ Configure PNG export (how to render html to png)
        try (ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG)) {
            pngOptions.setPageNumber(1); // first page only

            // 4️⃣ Render and write the file
            String output = "rendered_page.png";
            htmlDoc.save(output, pngOptions);
            System.out.println("✅ PNG saved to: " + output);
        }
    }
}
```

Αντιγράψτε‑και‑επικολλήστε αυτό στο IDE σας, προσαρμόστε το URL ή τη διαδρομή εξόδου, και πατήστε **Run**. Αν όλα είναι ρυθμισμένα σωστά, θα έχετε ένα PNG σε δευτερόλεπτα.

## Συμπέρασμα

Σε αυτόν τον οδηγό σας δείξαμε **πώς να αποθηκεύσετε σελίδα HTML ως PNG** χρησιμοποιώντας Java, καλύψαμε τις λεπτομέρειες του **πώς να αποδώσετε HTML σε PNG**, και παρουσιάσαμε τα ακριβή βήματα για **ορισμό μεγέθους viewport σε Java** για ακριβή έλεγχο του αποτελέσματος. Τώρα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορεί να ενσωματωθεί σε οποιοδήποτε έργο Java—είτε πρόκειται για υπηρεσία backend που δημιουργεί μικρογραφίες είτε για δοκιμαστικό περιβάλλον που επαληθεύει οπτικές διατάξεις.

### Τι Ακολουθεί;

- Πειραματιστείτε με διαφορετικές τιμές `DevicePixelRatio` για assets έτοιμα για retina.
- Συνδυάστε αυτήν την προσέγγιση με έναν headless browser για καταγραφή δυναμικών, JavaScript‑βαριών σελίδων.
- Εξερευνήστε άλλες μορφές εξαγωγής όπως JPEG ή PDF αντικαθιστώντας το `SaveFormat.PNG` με `SaveFormat.JPEG` ή `SaveFormat.PDF`.

Μη διστάσετε να τροποποιήσετε τον κώδικα, να μοιραστείτε τα αποτελέσματά σας ή να θέσετε ερωτήσεις στα σχόλια. Καλή απόδοση!  

![Στιγμιότυπο HTML αποθηκευμένο ως PNG](https://example.com/placeholder.png "παράδειγμα αποθήκευσης html σε png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}