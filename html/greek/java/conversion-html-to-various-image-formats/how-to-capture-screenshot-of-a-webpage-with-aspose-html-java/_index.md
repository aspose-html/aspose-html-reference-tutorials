---
category: general
date: 2026-01-07
description: πώς να καταγράψετε στιγμιότυπο οθόνης μιας ιστοσελίδας χρησιμοποιώντας
  το Aspose HTML σε Java. Μάθετε πώς να μετατρέψετε HTML σε εικόνα, να ορίσετε το
  μέγεθος του viewport και να αποθηκεύσετε την ιστοσελίδα ως PNG.
draft: false
keywords:
- how to capture screenshot
- convert html to image
- set viewport size
- save webpage as png
- how to convert html
language: el
og_description: πώς να καταγράψετε στιγμιότυπο οθόνης μιας ιστοσελίδας με το Aspose
  HTML Java. Οδηγός βήμα‑προς‑βήμα για τη μετατροπή HTML σε εικόνα, ορισμό μεγέθους
  προβολής και αποθήκευση ως PNG.
og_title: πώς να τραβήξετε στιγμιότυπο οθόνης μιας ιστοσελίδας – οδηγός Java
tags:
- Aspose HTML
- Java
- Web automation
title: πώς να καταγράψετε στιγμιότυπο οθόνης μιας ιστοσελίδας με το Aspose HTML –
  οδηγός Java
url: /el/java/conversion-html-to-various-image-formats/how-to-capture-screenshot-of-a-webpage-with-aspose-html-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να καταγράψετε στιγμιότυπο οθόνης μιας ιστοσελίδας με Aspose HTML – Java guide

Έχετε αναρωτηθεί ποτέ **πώς να καταγράψετε στιγμιότυπο οθνης** μιας δυναμικής ιστοσελίδας χωρίς να ανοίξετε πρόγραμμα περιήγησης; Δεν είστε ο μόνος. Σε πολλά έργα—δοκιμές, παρακολούθηση ή αρχειοθέτηση περιεχομένου—χρειάζεστε έναν αξιόπιστο τρόπο να μετατρέψετε HTML σε αρχείο bitmap. Τα καλά νέα; Το Aspose.HTML for Java το κάνει παιχνιδάκι.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: διαμόρφωση sandbox, ορισμός μεγέθους viewport, φόρτωση ζωντανής URL και τελικά **convert html to image** και **save webpage as png**. Στο τέλος θα έχετε ένα έτοιμο‑για‑εκτέλεση πρόγραμμα Java που κάνει ακριβώς αυτό.

## What You’ll Need

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* Java 17 (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο.  
* Maven ή Gradle για διαχείριση εξαρτήσεων.  
* Άδεια Aspose.HTML for Java (η δωρεάν αξιολόγηση λειτουργεί για δοκιμές).  
* Βασική εξοικείωση με τη Java—δεν απαιτούνται προχωρημένα κόλπα.

> **Pro tip:** Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση Aspose.HTML στο `pom.xml` σας. Είναι μια μόνο γραμμή και κρατά τα πάντα τακτοποιημένα.

## Step 1 – Create a sandbox and **set viewport size**

Το sandbox απομονώνει το rendering από το μηχάνημά σας, εξασφαλίζοντας ότι το στιγμιότυπο είναι συνεπές σε όλα τα περιβάλλοντα. Ενώ το κάνετε αυτό, μπορείτε να ορίσετε τις λογικές διαστάσεις της οθόνης με `setViewportSize`. Είναι το ίδιο όπως η αλλαγή μεγέθους παραθύρου περιηγητή πριν τραβήξετε τη φωτογραφία.

```java
import com.aspose.html.*;

public class ScreenshotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a sandbox with high‑resolution settings
        Sandbox renderingSandbox = new Sandbox();
        // Set the logical viewport to 1024×768 pixels – perfect for most desktop pages
        renderingSandbox.setViewportSize(1024, 768);
        // Optional: increase DPI for sharper output (useful for print‑ready PNGs)
        renderingSandbox.setDeviceDpi(300);
```

Γιατί είναι σημαντικό το **set viewport size**; Αν αποδώσετε μια σελίδα σε 800×600, οποιοδήποτε στοιχείο που θα εμφανιζόταν κανονικά κάτω από αυτή τη γραμμή θα κοπεί. Συμφωνώντας το viewport με το πλάτος σχεδίασης, καταγράφετε ολόκληρη τη διάταξη με μία κίνηση.

## Step 2 – Load the target page inside the sandbox

Τώρα που το sandbox είναι έτοιμο, δείξτε το στη URL που θέλετε να καταγράψετε. Το Aspose.HTML φέρνει το HTML, επεξεργάζεται το CSS, εκτελεί JavaScript και δημιουργεί ένα DOM όπως ένας πραγματικός περιηγητής.

```java
        // 2️⃣ Load the web page you wish to screenshot
        // Replace the URL with any page you need to capture
        HtmlDocument webPage = new HtmlDocument("https://example.com", renderingSandbox);
```

> **What if the page needs authentication?**  
> Περνάτε cookies ή προσαρμοσμένα headers στον κατασκευαστή `HtmlDocument`. Το API σας επιτρέπει να ενσωματώσετε ένα αντικείμενο `RequestHeaders`—ιδανικό για εσωτερικά δίκτυα.

## Step 3 – **convert html to image** and **save webpage as png**

Με το έγγραφο πλήρως αποδομένο, το βήμα μετατροπής είναι απλό. Η κλάση `Converter` διαχειρίζεται τη rasterization και μπορείτε να ρυθμίσετε τις επιλογές εξόδου (μορφή pixel, ποιότητα κ.λπ.) μέσω `ImageConversionOptions`.

```java
        // 3️⃣ Convert the rendered HTML to a PNG file
        ImageConversionOptions options = new ImageConversionOptions();
        // You can force a specific pixel format, e.g., PNG24 or PNG32
        options.setPixelFormat(PixelFormat.Format32bppArgb);
        // Perform the conversion
        Converter.convert(webPage, "output/screenshot.png", options);

        System.out.println("Screenshot saved to output/screenshot.png");
    }
}
```

Η εκτέλεση του προγράμματος δημιουργεί το `screenshot.png` στο φάκελο `output`. Ανοίξτε το και θα δείτε ένα πιστό bitmap της ζωντανής σελίδας—με όλα τα στυλ CSS, τις γραμματοσειρές και ακόμη και τα client‑side scripts που έχουν εκτελεστεί.

### Full Working Example

Παρακάτω είναι ο πλήρης, έτοιμος για αντιγραφή κώδικας. Περιλαμβάνει imports, διαμόρφωση sandbox, φόρτωση σελίδας και μετατροπή. Χωρίς κρυφά κομμάτια, χωρίς συντομεύσεις “δείτε docs”.

```java
import com.aspose.html.*;

public class ScreenshotDemo {
    public static void main(String[] args) throws Exception {
        // Create and configure the sandbox
        Sandbox renderingSandbox = new Sandbox();
        renderingSandbox.setViewportSize(1024, 768);
        renderingSandbox.setDeviceDpi(300);

        // Load the target URL
        HtmlDocument webPage = new HtmlDocument("https://example.com", renderingSandbox);

        // Set conversion options (optional but recommended for quality)
        ImageConversionOptions options = new ImageConversionOptions();
        options.setPixelFormat(PixelFormat.Format32bppArgb);

        // Convert to PNG and save
        Converter.convert(webPage, "output/screenshot.png", options);

        System.out.println("Screenshot saved to output/screenshot.png");
    }
}
```

**Expected output:** Ένα αρχείο PNG ακριβώς 1024 × 768 pixel (ή μεγαλύτερο αν η διάταξη της σελίδας επεκτείνεται πέρα από το viewport). Η εικόνα θα είναι καθαρή χάρη στη ρύθμιση 300 DPI.

## Common Pitfalls & Edge Cases

| Situation | Why it Happens | How to Fix |
|-----------|----------------|------------|
| **Blank image** | Το DPI του sandbox δεν έχει οριστεί ή η σελίδα δεν έχει ολοκληρώσει τη φόρτωση. | Καλέστε `webPage.waitForLoad()` πριν τη μετατροπή ή αυξήστε το `DeviceDpi`. |
| **Clipped content** | Το viewport είναι μικρότερο από το πλάτος της σελίδας. | Χρησιμοποιήστε `setViewportSize` με διαστάσεις που ταιριάζουν στο πλάτος σχεδίασης της σελίδας. |
| **Missing fonts** | Η γραμματοσειρά δεν είναι εγκατεστημένη στο μηχάνημα. | Ενσωματώστε web fonts μέσω CSS `@font-face` ή εγκαταστήστε τις απαιτούμενες γραμματοσειρές στον server. |
| **Authentication required** | Η σελίδα ανακατευθύνει σε login. | Παρέχετε cookies ή προσαρμοσμένα headers μέσω `HtmlLoadOptions`. |
| **Large pages causing OOM** | Απόδοση τεράστιων σελίδων σε περιβάλλοντα με χαμηλή μνήμη. | Αυξήστε το μέγεθος heap της Java (`-Xmx2g`) ή αποδώστε σε χαμηλότερο DPI. |

Αυτές οι συμβουλές σας βοηθούν να **how to convert html** αξιόπιστα, ακόμη και όταν ο στόχος δεν είναι μια απλή στατική σελίδα.

## Bonus: Capture Multiple Pages in One Run

Αν χρειάζεστε μια σειρά από στιγμιότυπα, κάντε βρόχο πάνω σε λίστα URLs. Το sandbox μπορεί να επαναχρησιμοποιηθεί, επιταχύνοντας την επεξεργασία.

```java
String[] urls = {"https://example.com", "https://example.org/about", "https://example.net/contact"};
for (String url : urls) {
    HtmlDocument doc = new HtmlDocument(url, renderingSandbox);
    String fileName = "output/" + url.replaceAll("[^a-zA-Z0-9]", "_") + ".png";
    Converter.convert(doc, fileName, options);
    System.out.println("Saved: " + fileName);
}
```

## Conclusion

Τώρα έχετε μια ολοκληρωμένη, end‑to‑end λύση για **how to capture screenshot** οποιασδήποτε ιστοσελίδας χρησιμοποιώντας Aspose.HTML for Java. Καλύψαμε πώς να **set viewport size**, **convert html to image**, και **save webpage as png**—όλα σε λίγα σύντομα βήματα.  

Νιώστε ελεύθεροι να πειραματιστείτε: αλλάξτε το DPI για περιουσιακά στοιχεία εκτύπωσης, αντικαταστήστε PNG με JPEG αν σας ενδιαφέρει το μέγεθος αρχείου, ή ενσωματώστε αυτόν τον κώδικα σε CI pipeline για αυτοματοποιημένες δοκιμές UI regression.  

Έχετε ερωτήσεις για **how to convert html** σε άλλα περιβάλλοντα, ή χρειάζεστε βοήθεια με τεχνάσματα αυθεντικοποίησης; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!  

![how to capture screenshot of a webpage using Aspose HTML Java](https://example.com/assets/screenshot-demo.png "how to capture screenshot of a webpage using Aspose HTML Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}