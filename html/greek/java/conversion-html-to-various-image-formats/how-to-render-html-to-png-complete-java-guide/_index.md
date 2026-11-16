---
category: general
date: 2026-03-07
description: Μάθετε πώς να αποδίδετε HTML σε PNG χρησιμοποιώντας το Aspose.HTML. Αυτό
  το βήμα‑βήμα εκπαιδευτικό υλικό δείχνει επίσης πώς να μετατρέψετε HTML σε PNG, να
  ορίσετε το μέγεθος του viewport, να φορτώσετε έγγραφο HTML και να ορίσετε το DPI.
draft: false
keywords:
- how to render html
- convert html to png
- set viewport size
- load html document
- how to set dpi
language: el
og_description: Μάθετε πώς να αποδίδετε HTML σε PNG χρησιμοποιώντας το Aspose.HTML.
  Αυτός ο οδηγός καλύπτει τη μετατροπή HTML σε PNG, τον καθορισμό του μεγέθους του
  viewport, τη φόρτωση του εγγράφου HTML και πώς να ορίσετε το DPI.
og_title: Πώς να μετατρέψετε HTML σε PNG – Πλήρης οδηγός Java
tags:
- Aspose.HTML
- Java
- Rendering
title: Πώς να αποδώσετε HTML σε PNG – Πλήρης οδηγός Java
url: /el/java/conversion-html-to-various-image-formats/how-to-render-html-to-png-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Μετατρέψετε HTML σε PNG – Πλήρης Οδηγός Java

Έχετε αναρωτηθεί ποτέ **πώς να αποδώσετε HTML** σε αρχείο εικόνας χωρίς να ανοίξετε έναν περιηγητή; Δεν είστε μόνοι—πολλοί προγραμματιστές χρειάζονται έναν αξιόπιστο τρόπο να μετατρέψουν μια ιστοσελίδα σε PNG για αναφορές, μικρογραφίες ή PDF. Τα καλά νέα είναι ότι το Aspose.HTML κάνει αυτή τη διαδικασία παιχνιδάκι. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, από τη φόρτωση του εγγράφου HTML μέχρι τον ορισμό του μεγέθους του viewport και του DPI, και τελικά τη μετατροπή της σε εικόνα PNG.

Θα αγγίξουμε επίσης συναφή εργασίες όπως **convert HTML to PNG**, πώς να **set viewport size** για ακριβή έλεγχο διάταξης, και τα ακριβή βήματα για **load HTML document** με ασφάλεια. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Java.

---

## Τι Θα Χρειαστείτε

- **Java 17** ή νεότερη (ο κώδικας μεταγλωττίζεται με οποιοδήποτε πρόσφατο JDK).  
- **Aspose.HTML for Java** 23.9 (ή την πιο πρόσφατη έκδοση).  
- Ένα αρχείο `input.html` που θέλετε να μετατρέψετε σε εικόνα.  
- Έναν φάκελο όπου θέλετε να εμφανιστεί το `output.png`.  

Δεν απαιτούνται εξωτερικοί περιηγητές ή εκτελέσεις headless Chrome—το Aspose.HTML αναλαμβάνει όλη τη βαριά δουλειά εσωτερικά.

---

## Βήμα 1: Δημιουργία Sandbox – Το Περιβάλλον Απόδοσης

Πριν μπορέσετε να **render HTML**, χρειάζεστε ένα sandbox που ορίζει το περιβάλλον απόδοσης. Σκεφτείτε το sandbox ως ένα εικονικό παράθυρο περιηγητή όπου μπορείτε να ελέγξετε το μέγεθος του viewport, το DPI και ακόμη και τη συμβολοσειρά user‑agent. Αυτό είναι κρίσιμο επειδή το ίδιο HTML μπορεί να φαίνεται διαφορετικά σε κινητό και σε επιτραπέζιο υπολογιστή.

```java
import com.aspose.html.rendering.*;
import java.nio.file.Paths;

public class SandboxRenderExample {
    public static void main(String[] args) throws Exception {

        // Define the sandbox (viewport, DPI, user‑agent)
        Sandbox sandbox = new Sandbox.Builder()
                .setViewportSize(1024, 768)   // set viewport size
                .setDpi(96)                   // how to set DPI
                .setUserAgent("AsposeHTML/23.9")
                .build();
```

> **Γιατί είναι σημαντικό:**  
> - **Viewport size** καθορίζει το πλάτος και το ύψος που η σελίδα «πιστεύει» ότι έχει, επηρεάζοντας άμεσα τα CSS media queries.  
> - **DPI** (dots per inch) ελέγχει την ανάλυση της εικόνας· υψηλότερο DPI παράγει πιο οξυές PNG, ειδικά για γραφικά έτοιμα για εκτύπωση.  
> - Το **user‑agent** μπορεί να επηρεάσει τη λογική απόδοσης στο διακομιστή (ορισμένοι ιστότοποι σερβίρουν markup βελτιστοποιημένο για κινητά).

---

## Βήμα 2: Φόρτωση του Εγγράφου HTML

Τώρα που το sandbox είναι έτοιμο, πρέπει να **load HTML document** σε ένα αντικείμενο `HTMLDocument`. Το Aspose.HTML δέχεται URI, ώστε να μπορείτε να δείξετε σε τοπικό αρχείο, απομακρυσμένο URL ή ακόμη και σε συμβολοσειρά στη μνήμη.

```java
        // Load the HTML file you want to render
        HTMLDocument htmlDocument = new HTMLDocument(
                Paths.get("YOUR_DIRECTORY/input.html").toUri().toString());
```

> **Συμβουλή:** Αν το HTML σας αναφέρεται σε εξωτερικά assets (CSS, εικόνες, γραμματοσειρές), κρατήστε τα στον ίδιο φάκελο ή χρησιμοποιήστε απόλυτα URLs ώστε ο renderer να μπορεί να τα εντοπίσει σωστά.

---

## Βήμα 3: Απόδοση του Εγγράφου σε PNG

Με το έγγραφο φορτωμένο, το τελικό βήμα είναι να **convert HTML to PNG**. Η κλάση `Renderer` παίρνει το sandbox που δημιουργήσαμε νωρίτερα και γράφει τη σελίδα που αποδόθηκε στο σύστημα αρχείων.

```java
        // Render the document inside the sandbox to a PNG image
        try (Renderer renderer = new Renderer(sandbox)) {
            renderer.render(htmlDocument, Paths.get("YOUR_DIRECTORY/output.png"));
        }

        System.out.println("Rendering completed – see YOUR_DIRECTORY/output.png");
    }
}
```

Ο παραπάνω κώδικας κάνει όλα όσα χρειάζεστε: σέβεται το μέγεθος του viewport, το DPI και το user‑agent που ορίσαμε προηγουμένως, και παράγει ένα καθαρό αρχείο PNG στη θέση που καθορίσατε.

---

## Βήμα 4: Επαλήθευση του Αποτελέσματος (Τι Να Περιμένετε)

Αφού εκτελέσετε το πρόγραμμα, ανοίξτε το `output.png`. Θα πρέπει να δείτε μια ακριβή οπτική αναπαράσταση του `input.html` όπως θα εμφανιζόταν σε παράθυρο περιηγητή 1024 × 768 με 96 DPI. Αν η εικόνα φαίνεται θολή, δοκιμάστε να αυξήσετε το DPI:

```java
.setDpi(300)   // higher DPI for sharper output
```

Θυμηθείτε, μεγαλύτερες τιμές DPI αυξάνουν το μέγεθος του αρχείου, οπότε ισορροπήστε την ποιότητα με τις απαιτήσεις αποθήκευσης.

---

## Πώς να Ορίσετε το Μέγεθος Viewport για Διαφορετικά Σενάρια

Μερικές φορές χρειάζεστε ένα mobile viewport (π.χ. 375 × 667) για να συλλάβετε μια responsive διάταξη. Απλώς αλλάξτε την κλήση `setViewportSize`:

```java
.setViewportSize(375, 667)   // iPhone 6/7/8 dimensions
```

Μπορείτε επίσης να δημιουργήσετε πολλαπλά sandboxes στο ίδιο πρόγραμμα αν χρειαστεί να δημιουργήσετε μικρογραφίες τόσο για την έκδοση desktop όσο και για την έκδοση mobile της ίδιας σελίδας.

---

## Φόρτωση HTML από Συμβολοσειρά – Όταν Δεν Έχετε Αρχείο

Αν το HTML σας παράγεται «on‑the‑fly», μπορείτε να παραλείψετε εντελώς το σύστημα αρχείων:

```java
String htmlContent = "<!DOCTYPE html><html><body><h1>Hello, world!</h1></body></html>";
HTMLDocument doc = new HTMLDocument(htmlContent, "about:blank");
```

Αυτή η προσέγγιση είναι χρήσιμη για unit tests ή όταν λαμβάνετε HTML μέσω ενός API.

---

## Συνηθισμένα Πιθανά Προβλήματα και Επαγγελματικές Συμβουλές

- **Relative Paths:** Βεβαιωθείτε ότι τα URLs των CSS και των εικόνων είναι είτε απόλυτα είτε σχετικά με το φάκελο που περνάτε στο `HTMLDocument`. Διαφορετικά ο renderer δεν θα τα βρει.  
- **Fonts:** Αν χρειάζεστε προσαρμοσμένες γραμματοσειρές, ενσωματώστε τις με `@font-face` στο CSS ή τοποθετήστε τα αρχεία γραμματοσειρών δίπλα στο HTML.  
- **Large Pages:** Η απόδοση πολύ μεγάλων σελίδων (π.χ. infinite scroll) μπορεί να καταναλώσει πολύ μνήμη. Σκεφτείτε να χωρίσετε τη σελίδα ή να χρησιμοποιήσετε τις δυνατότητες σελιδοποίησης του Aspose.HTML.  
- **Thread Safety:** Η κλάση `Renderer` δεν είναι thread‑safe· δημιουργήστε ένα νέο instance ανά νήμα αν κάνετε απόδοση παράλληλα.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή)

Παρακάτω βρίσκεται η πλήρης, έτοιμη προς εκτέλεση κλάση Java. Αντικαταστήστε το `YOUR_DIRECTORY` με μια πραγματική διαδρομή στον υπολογιστή σας.

```java
import com.aspose.html.rendering.*;
import com.aspose.html.HTMLDocument;
import java.nio.file.Paths;

/**
 * Demonstrates how to render HTML to PNG using Aspose.HTML.
 * This example shows how to set viewport size, DPI, and load an HTML document.
 */
public class SandboxRenderExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a sandbox that defines the rendering environment
        Sandbox sandbox = new Sandbox.Builder()
                .setViewportSize(1024, 768)   // set viewport size
                .setDpi(96)                   // how to set DPI
                .setUserAgent("AsposeHTML/23.9")
                .build();

        // Step 2: Load the HTML document you want to render
        HTMLDocument htmlDocument = new HTMLDocument(
                Paths.get("YOUR_DIRECTORY/input.html").toUri().toString());

        // Step 3: Render the document inside the sandbox to a PNG image
        try (Renderer renderer = new Renderer(sandbox)) {
            renderer.render(htmlDocument, Paths.get("YOUR_DIRECTORY/output.png"));
        }

        System.out.println("Rendering completed – see YOUR_DIRECTORY/output.png");
    }
}
```

Τρέξτε το πρόγραμμα με:

```bash
javac -cp "path/to/aspose-html.jar" SandboxRenderExample.java
java -cp ".:path/to/aspose-html.jar" SandboxRenderExample
```

Θα δείτε το μήνυμα στην κονσόλα που επιβεβαιώνει την επιτυχία, και το PNG θα βρίσκεται στη θέση που ορίσατε.

---

## Αναμενόμενη Στιγμιότυπο Αποτελέσματος

![how to render html result](https://example.com/output-screenshot.png "Screenshot of the rendered PNG file – how to render html")

*Η παραπάνω εικόνα δείχνει ένα τυπικό αποτέλεσμα όταν αποδίδεται μια απλή σελίδα HTML.*

---

## Ανακεφαλαίωση – Τι Καλύψαμε

- **How to render HTML** σε PNG χρησιμοποιώντας το Aspose.HTML.  
- Ο πλήρης **convert HTML to PNG** κύκλος εργασίας, από τη δημιουργία sandbox μέχρι την έξοδο αρχείου.  
- Πώς να **set viewport size** για δοκιμές responsive.  
- Τα ακριβή βήματα για **load HTML document** από αρχείο ή συμβολοσειρά.  
- Ο σωστός τρόπος για **how to set DPI** για εικόνες υψηλής ανάλυσης.  

Με αυτά τα κομμάτια, μπορείτε να αυτοματοποιήσετε τη δημιουργία μικρογραφιών, να παράγετε προεπισκοπήσεις PDF, ή να τροφοδοτήσετε εικόνες σε οποιοδήποτε σύστημα που χρειάζεται οπτική αναπαράσταση του web περιεχομένου.

---

## Επόμενα Βήματα & Σχετικά Θέματα

- **Batch Rendering:** Επανάληψη πάνω σε πολλά αρχεία HTML για παραγωγή μιας γκαλερί PNG.  
- **PDF Conversion:** Αντικαταστήστε το `Renderer.render` με `PdfRenderer` για παραγωγή PDF αντί για PNG.  
- **Watermarking:** Μετά την απόδοση, χρησιμοποιήστε το Aspose.Imaging για να προσθέσετε λογότυπο ή υδατογράφημα.  
- **Performance Tuning:** Πειραματιστείτε με διαφορετικές τιμές DPI και επαναχρησιμοποίηση sandbox για να επιταχύνετε μεγάλες εργασίες.

Αν έχετε οποιεσδήποτε ερωτήσεις—π.χ. “Τι γίνεται αν το HTML μου χρησιμοποιεί JavaScript?”—αφήστε ένα σχόλιο παρακάτω. Καλή απόδοση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}