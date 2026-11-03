---
category: general
date: 2026-05-31
description: Απενεργοποιήστε τις εξωτερικές εικόνες όταν αποδίδετε μια ιστοσελίδα
  σε PNG σε Java χρησιμοποιώντας το Aspose HTML. Μάθετε πώς να φορτώνετε την ιστοσελίδα
  σε ασφαλή sandbox και να αποθηκεύετε το έγγραφο HTML ως PNG.
draft: false
keywords:
- disable external images
- render webpage to png
- load webpage in sandbox
- how to render html to image java
- save html document as png
language: el
og_description: Απενεργοποιήστε τις εξωτερικές εικόνες κατά τη μετατροπή μιας ιστοσελίδας
  σε PNG στην Java. Αυτός ο οδηγός βήμα‑προς‑βήμα δείχνει πώς να φορτώσετε μια ιστοσελίδα
  σε sandbox και να αποθηκεύσετε το έγγραφο HTML ως PNG.
og_title: Απενεργοποίηση εξωτερικών εικόνων κατά τη μετατροπή ιστοσελίδας σε PNG στην
  Java
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Disable external images when you render webpage to PNG in Java using
    Aspose HTML. Learn to load webpage in sandbox safely and save HTML document as
    PNG.
  headline: Disable External Images While Rendering Webpage to PNG in Java
  type: TechArticle
- questions:
  - answer: Yes. Inline `data:` URIs or base64‑encoded images are treated as part
      of the document and will appear in the PNG.
    question: Can I still display images that are bundled inside the HTML?
  - answer: The sandbox works as an all‑or‑nothing switch. For fine‑grained control,
      download the allowed images yourself, embed them as data URIs, and then render.
    question: What if I need to keep some external images but block others?
  - answer: Absolutely. Aspose.HTML is a pure‑Java library; it does not require a
      display server or browser engine.
    question: Does this approach work on headless servers?
  - answer: 'Selenium drives a real browser, which is heavyweight and harder to sandbox.
      Aspose.HTML renders HTML directly in memory, giving you deterministic performance
      and easier security controls like **disable external images**. --- ## Conclusion
      You now have a solid, end‑to‑end recipe for **disabling exter'
    question: How does this differ from using Selenium or Puppeteer?
  type: FAQPage
tags:
- Aspose.HTML
- Java
- Image Rendering
title: Απενεργοποίηση εξωτερικών εικόνων κατά τη μετατροπή ιστοσελίδας σε PNG σε Java
url: /el/java/conversion-html-to-various-image-formats/disable-external-images-while-rendering-webpage-to-png-in-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απενεργοποίηση Εξωτερικών Εικόνων Κατά τη Σχεδίαση Ιστοσελίδας σε PNG με Java

Έχετε χρειαστεί ποτέ να **απενεργοποιήσετε εξωτερικές εικόνες** όταν μετατρέπετε μια ιστοσελίδα σε PNG με Java; Ίσως δημιουργείτε μια υπηρεσία μικρογραφιών που πρέπει να παραμείνει απομονωμένη από το δημόσιο διαδίκτυο, ή απλώς θέλετε να εξασφαλίσετε ότι καμία εικόνα τρίτου δεν θα διαρρεύσει κατά τη μετατροπή. Σε κάθε περίπτωση, βρίσκεστε στο σωστό σημείο.

Σε αυτό το tutorial θα δούμε πώς να φορτώσουμε μια ιστοσελίδα σε sandbox, να απενεργοποιήσουμε τη λήψη εξωτερικών εικόνων και, τέλος, να αποθηκεύσουμε το έγγραφο HTML ως αρχείο PNG — όλα με το Aspose.HTML for Java. Στο τέλος θα έχετε ένα έτοιμο παράδειγμα, μαζί με μια σειρά πρακτικών συμβουλών για να αποφύγετε τα συνηθισμένα προβλήματα.

## Τι Θα Μάθετε

- **Πώς να αποδίδετε HTML σε εικόνα Java** χρησιμοποιώντας το `Converter` του Aspose.HTML.  
- Τα ακριβή βήματα για **φόρτωση ιστοσελίδας σε sandbox** με προσαρμοσμένο viewport και DPI.  
- Τη διαμόρφωση που απαιτείται για **απενεργοποίηση εξωτερικών εικόνων** ενώ η σελίδα εξακολουθεί να αποδίδεται.  
- Πώς να **αποθηκεύσετε το έγγραφο HTML ως PNG** (ή οποιαδήποτε άλλη υποστηριζόμενη μορφή) στο δίσκο.  
- Διαχείριση edge‑case, συμβουλές απόδοσης και οδηγίες αντιμετώπισης προβλημάτων.

### Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη (ο κώδικας λειτουργεί επίσης με JDK 11+).  
- Maven ή Gradle για τη λήψη της βιβλιοθήκης Aspose.HTML for Java.  
- Βασική εξοικείωση με τη σύνταξη της Java και τη διαχείριση εξαιρέσεων.  
- Σύνδεση στο διαδίκτυο για το αρχικό φόρτωμα της σελίδας (εκτός εάν εξυπηρετείτε το HTML τοπικά).

> **Pro tip:** Εάν εργάζεστε πίσω από εταιρικό proxy, ορίστε τις ιδιότητες JVM `http.proxyHost` και `http.proxyPort` πριν τρέξετε το παράδειγμα.

---

## Step 1: Ρυθμίστε το Project σας και Προσθέστε το Aspose.HTML

Πρώτα απ’ όλα — προσθέστε την εξάρτηση Aspose.HTML. Αν χρησιμοποιείτε Maven, τοποθετήστε αυτό στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Για Gradle, το ισοδύναμο είναι:

```gradle
implementation 'com.aspose:aspose-html:23.9'
```

Μόλις η βιβλιοθήκη βρίσκεται στο classpath, είστε έτοιμοι να αρχίσετε τον κώδικα.

---

## Step 2: **Απενεργοποίηση Εξωτερικών Εικόνων** με Περιβάλλον Sandbox

Η καρδιά της λύσης βρίσκεται στο `DocumentSandbox`. Με το να περάσουμε `false` για τη σημαία *allowExternalImages*, υποδεικνύουμε στο Aspose.HTML να αγνοήσει τυχόν ετικέτες `<img>` που δείχνουν σε URLs εκτός του sandbox. Αυτός είναι ο ακριβής μηχανισμός που **απενεργοποιεί εξωτερικές εικόνες**.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that blocks external scripts and images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport size (width x height)
                96,                     // DPI – 96 is the screen default
                "MyApp/1.0",            // custom user‑agent string
                false,                  // allowExternalScripts = false
                false);                 // allowExternalImages = false  <-- disables external images
```

> **Γιατί είναι σημαντικό:** Χωρίς το sandbox, ο renderer θα προσπαθούσε να κατεβάσει κάθε εικόνα που αναφέρεται στη σελίδα, κάτι που μπορεί να είναι αργό, αναξιόπιστο ή ακόμη και κίνδυνο ασφαλείας. Ορίζοντας τη σημαία σε `false` εξασφαλίζουμε μια καθαρή, αυτοσυνεπή διαδικασία απόδοσης.

---

## Step 3: **Φόρτωση Ιστοσελίδας σε Sandbox**  

Τώρα κατευθύνουμε το Aspose.HTML στο URL που θέλουμε να καταγράψουμε. Ο κατασκευαστής `HTMLDocument` δέχεται το αντικείμενο sandbox, εφαρμόζοντας αυτόματα τους περιορισμούς που ορίσαμε.

```java
        // 2️⃣ Load the target page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // replace with your target URL
                sandbox);
```

Αν η σελίδα εξαρτάται έντονα από εξωτερικά scripts για το layout, μπορεί να παρατηρήσετε ελλιπές περιεχόμενο επειδή απενεργοποιήσαμε επίσης τα scripts. Σε αυτήν την περίπτωση, ενεργοποιήστε τη σημαία `allowExternalScripts` σε `true` ενώ διατηρείτε το `allowExternalImages` σε `false`.

---

## Step 4: **Απόδοση Ιστοσελίδας σε PNG**  

Με το έγγραφο φορτωμένο, η μετατροπή του σε εικόνα γίνεται με μία γραμμή κώδικα χρησιμοποιώντας το `Converter.convert`. Το αντικείμενο `ImageSaveOptions` σας επιτρέπει να επιλέξετε τη μορφή εξόδου· εδώ επιλέγουμε PNG.

```java
        // 3️⃣ Render the document to a PNG image.
        ImageSaveOptions saveOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png"; // ensure the folder exists

        Converter.convert(htmlDoc, saveOptions, outputPath);
        System.out.println("Image saved to: " + outputPath);
    }
}
```

Το παραγόμενο αρχείο, `sandboxed.png`, περιέχει ένα στιγμιότυπο της σελίδας **χωρίς καμία εξωτερική εικόνα** — παραμένουν μόνο τα ενσωματωμένα SVG ή οι εικόνες σε base64, εάν υπάρχουν.

---

## Step 5: Επαλήθευση του Αποτελέσματος και Εντοπισμός Συνηθισμένων Προβλημάτων

Αφού τρέξετε το πρόγραμμα, ανοίξτε το `sandboxed.png` σε οποιονδήποτε προβολέα εικόνων. Θα πρέπει να δείτε το layout της σελίδας, το κείμενο και το CSS, αλλά όλα τα στοιχεία `<img src="http://…">` θα είναι κενά (συχνά εμφανίζονται ως λευκό ορθογώνιο ή παραλείπονται εντελώς).

### Συνηθισμένα προβλήματα και πώς να τα διορθώσετε

| Συμπτωμα | Πιθανή αιτία | Διόρθωση |
|---|---|---|
| Κενή σελίδα | Το URL στόχος μπλόκαρε το αίτημα (π.χ., Cloudflare) | Προσθέστε κατάλληλες κεφαλίδες στον user‑agent του sandbox ή χρησιμοποιήστε proxy. |
| Λείπουν γραμματοσειρές | Τα αρχεία γραμματοσειρών φιλοξενούνται εξωτερικά | Εγκαταστήστε τις γραμματοσειρές τοπικά ή ενσωματώστε τις ως `@font-face` με data URIs. |
| Μετατόπιση layout | Το CSS αναφέρεται σε εξωτερικά stylesheets που μπλοκαρίστηκαν | Ορίστε `allowExternalScripts` σε `true` *μόνο* για τη φόρτωση CSS, μετά ξανατρέξτε. |
| `java.lang.OutOfMemoryError` | Απόδοση πολύ μεγάλης σελίδας σε υψηλό DPI | Μειώστε το μέγεθος του viewport ή το DPI, ή αυξήστε τη μνήμη heap της JVM (`-Xmx2g`). |

---

## Step 6: Επέκταση του Παραδείγματος – Αποθήκευση σε Άλλες Μορφές

Ο ίδιος κώδικας λειτουργεί για JPEG, BMP ή ακόμη και PDF. Απλώς αλλάξτε το enum `SaveFormat`:

```java
// Example: Save as JPEG with quality 80%
ImageSaveOptions jpegOptions = new ImageSaveOptions(SaveFormat.JPEG);
jpegOptions.setQuality(80);
Converter.convert(htmlDoc, jpegOptions, "output/sandboxed.jpg");
```

Αν χρειάζεστε PDF, αντικαταστήστε το `ImageSaveOptions` με `PdfSaveOptions` και προσαρμόστε την επέκταση του αρχείου αναλόγως.

---

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω βρίσκεται το **πλήρες, εκτελέσιμο πρόγραμμα**. Δημιουργήστε μια νέα κλάση Java, επικολλήστε τον κώδικα, βεβαιωθείτε ότι υπάρχει ο φάκελος `output`, και τρέξτε το.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;
import java.awt.geom.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Step 1 – Create a sandbox that disables external images.
        DocumentSandbox sandbox = new DocumentSandbox(
                new SizeF(1024, 768),   // viewport width & height
                96,                     // DPI
                "MyApp/1.0",            // custom user‑agent
                false,                  // external scripts disabled
                false);                 // external images disabled (primary goal)

        // Step 2 – Load the page inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument(
                "https://example.com", // change to your URL
                sandbox);

        // Step 3 – Render to PNG.
        ImageSaveOptions pngOptions = new ImageSaveOptions(SaveFormat.PNG);
        String outputPath = "output/sandboxed.png";

        Converter.convert(htmlDoc, pngOptions, outputPath);
        System.out.println("PNG image saved to: " + outputPath);
    }
}
```

**Αναμενόμενη έξοδος** (κονσόλα):

```
PNG image saved to: output/sandboxed.png
```

Ανοίξτε το `sandboxed.png` – θα δείτε τη σελίδα αποδομένη **χωρίς καμία εξωτερική εικόνα**.

---

## Συχνές Ερωτήσεις

**Ε: Μπορώ ακόμα να εμφανίσω εικόνες που είναι ενσωματωμένες στο HTML;**  
Α: Ναι. Τα ενσωματωμένα `data:` URIs ή οι εικόνες σε base64 θεωρούνται μέρος του εγγράφου και θα εμφανιστούν στο PNG.

**Ε: Τι γίνεται αν θέλω να κρατήσω κάποιες εξωτερικές εικόνες αλλά να μπλοκάρω άλλες;**  
Α: Το sandbox λειτουργεί ως εναλλαγή «όλα ή τίποτα». Για πιο λεπτομερή έλεγχο, κατεβάστε μόνο τις επιτρεπόμενες εικόνες, ενσωματώστε τις ως data URIs και μετά αποδώστε.

**Ε: Λειτουργεί αυτή η προσέγγιση σε headless servers;**  
Α: Απόλυτα. Το Aspose.HTML είναι μια καθαρά Java βιβλιοθήκη· δεν απαιτεί διακομιστή εμφάνισης ή μηχανή προγράμματος περιήγησης.

**Ε: Πώς διαφέρει από τη χρήση Selenium ή Puppeteer;**  
Α: Το Selenium οδηγεί έναν πραγματικό browser, που είναι βαρύ και πιο δύσκολο να απομονωθεί. Το Aspose.HTML αποδίδει HTML απευθείας στη μνήμη, προσφέροντας προβλέψιμη απόδοση και ευκολότερο έλεγχο ασφαλείας όπως η **απενεργοποίηση εξωτερικών εικόνων**.

---

## Συμπέρασμα

Τώρα διαθέτετε μια στέρεη, ολοκληρωμένη συνταγή για **απενεργοποίηση εξωτερικών εικόνων κατά τη σχεδίαση μιας ιστοσελίδας σε PNG με Java**. Με τη χρήση του `DocumentSandbox`, έχετε αυστηρό έλεγχο πάνω σε ποιοι εξωτερικοί πόροι επιτρέπονται, εξασφαλίζοντας τόσο την ασφάλεια όσο και την αναπαραγωγιμότητα. Από εδώ μπορείτε να πειραματιστείτε με διαφορετικά μεγέθη viewport, ρυθμίσεις DPI ή μορφές εξόδου — κάθε προσαρμογή ανοίγει νέες δυνατότητες για τη δημιουργία μικρογραφιών, προεπισκοπήσεων ή αρχειοθετημένων στιγμιοτύπων.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να αποδίδετε μια σειρά URLs παράλληλα ή ενσωματώστε αυτή τη λογική σε ένα microservice Spring Boot που επιστρέφει PNG κατ' απαίτηση. Ο ουρανός είναι το όριο όταν συνδυάζετε την ευελιξία του Aspose.HTML με τα εργαλεία ταυτόχρονης εκτέλεσης της Java.

Καλό coding, και μην ξεχάσετε να μοιραστείτε τις επιτυχίες σας στα σχόλια!

## Τι Θα Μάθετε Στη Σειρά;

- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)
- [How to Render HTML to PNG with Aspose – Complete Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-with-aspose-complete-guide/)
- [How to Edit CSS - Advanced External CSS Editing with Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-external-css-editing/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}