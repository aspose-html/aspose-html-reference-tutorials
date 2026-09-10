---
category: general
date: 2026-01-10
description: Πώς να αποδώσετε HTML και να καταγράψετε στιγμιότυπο οθόνης της ιστοσελίδας
  ως PNG. Μάθετε πώς να μετατρέψετε HTML σε PNG, να αποθηκεύσετε HTML ως PNG και να
  δημιουργήσετε εικόνα από HTML χρησιμοποιώντας το Aspose.HTML.
draft: false
keywords:
- how to render html
- convert html to png
- save html as png
- capture webpage screenshot
- generate image from html
language: el
og_description: Πώς να αποδώσετε HTML και να καταγράψετε στιγμιότυπο οθόνης της ιστοσελίδας
  ως PNG. Ακολουθήστε αυτόν τον οδηγό για να μετατρέψετε HTML σε PNG, να αποθηκεύσετε
  HTML ως PNG και να δημιουργήσετε εικόνα από HTML με το Aspose.HTML.
og_title: Πώς να μετατρέψετε HTML σε PNG – Java Tutorial βήμα‑βήμα
tags:
- Java
- Aspose.HTML
- Image Rendering
title: Πώς να Μετατρέψετε HTML σε PNG – Πλήρης Οδηγός για Προγραμματιστές Java
url: /el/java/conversion-html-to-various-image-formats/how-to-render-html-to-png-complete-guide-for-java-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Μετατρέψετε HTML σε PNG – Πλήρης Οδηγός για Προγραμματιστές Java

Έχετε αναρωτηθεί ποτέ **πώς να αποδώσετε HTML** και να πάρετε ένα τέλειο στιγμιότυπο PNG χωρίς να ανοίξετε πρόγραμμα περιήγησης; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές χρειάζονται **συγγραφή στιγμιότυπου ιστοσελίδας** για αναφορές, email ή αυτοματοποιημένες δοκιμές, αλλά η εκκίνηση ενός πλήρους stack προγράμματος περιήγησης είναι υπερβολική. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια σύντομη, ολοκληρωμένη λύση που **μετατρέπει HTML σε PNG**, **αποθηκεύει HTML ως PNG**, και τελικά **δημιουργεί εικόνα από HTML** χρησιμοποιώντας τη βιβλιοθήκη Aspose.HTML.

Θα καλύψουμε όλα όσα χρειάζεστε: την απαιτούμενη εξάρτηση Maven, ανάλυση κώδικα γραμμή‑για‑γραμμή, κοινά προβλήματα, και πώς να προσαρμόσετε την έξοδο για διαφορετικές περιπτώσεις χρήσης. Στο τέλος, θα έχετε ένα έτοιμο πρόγραμμα Java που παίρνει οποιοδήποτε HTML string—συμπεριλαμβανομένου JavaScript—και παράγει ένα καθαρό αρχείο PNG.

## Τι Θα Χρειαστείτε

- **Java 17** ή νεότερη (ο κώδικας λειτουργεί με οποιοδήποτε πρόσφατο JDK)
- **Aspose.HTML for Java** (το Maven artifact `com.aspose:aspose-html:23.9` τη στιγμή της συγγραφής)
- Ένα IDE ή απλός επεξεργαστής κειμένου και ένα τερματικό για τη μεταγλώττιση
- Έναν φάκελο όπου θέλετε να αποθηκευτεί η εικόνα εξόδου (αντικαταστήστε το `YOUR_DIRECTORY` στον κώδικα)

Χωρίς εξωτερικά προγράμματα περιήγησης, χωρίς Selenium, χωρίς headless Chrome—μόνο καθαρή Java.

## Βήμα 1: Ρύθμιση της Εξάρτησης Aspose.HTML

Πρώτα, προσθέστε τη βιβλιοθήκη Aspose.HTML στο έργο σας. Αν χρησιμοποιείτε Maven, επικολλήστε αυτό στο `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.9</version>
</dependency>
```

Οι χρήστες Gradle μπορούν να προσθέσουν:

```groovy
implementation 'com.aspose:aspose-html:23.9'
```

> **Pro tip:** Η Aspose προσφέρει δωρεάν δοκιμή με πλήρη λειτουργικότητα. Κατεβάστε ένα αρχείο άδειας και τοποθετήστε το δίπλα στο JAR σας για να αποφύγετε το υδατογράφημα αξιολόγησης.

## Βήμα 2: Προετοιμασία του Περιεχομένου HTML

Για το demo θα χρησιμοποιήσουμε ένα μικρό απόσπασμα HTML που εμφανίζει το τρέχον έτος μέσω JavaScript. Αυτό δείχνει ότι **η εκτέλεση JavaScript** υποστηρίζεται έτοιμη για χρήση.

```java
String htmlContent = "<script>document.body.innerHTML = '<h1>'+new Date().getFullYear()+'</h1>';</script>";
```

Μπορείτε να αντικαταστήσετε το `htmlContent` με οποιοδήποτε στατικό ή δυναμικό markup—πίνακες, γραφήματα, SVGs, ό,τι θέλετε. Το κλειδί είναι ότι το Aspose.HTML θα αναλύσει το DOM, θα εκτελέσει το script και θα σας δώσει το τελικό αποδομένο layout.

## Βήμα 3: Φόρτωση του HTML σε Έγγραφο Aspose.HTML

Η δημιουργία ενός αντικειμένου `Document` από μια συμβολοσειρά είναι απλή:

```java
// Load the HTML string into an Aspose HTML Document
Document htmlDocument = new Document(htmlContent);
```

Πίσω από τις σκηνές, το Aspose χτίζει ένα πλήρες DOM, λύνει τους πόρους και προετοιμάζεται για απόδοση. Αν το HTML σας αναφέρεται σε εξωτερικά CSS ή εικόνες, βεβαιωθείτε ότι είναι προσβάσιμα μέσω απόλυτων URL ή ενσωματωμένα ως Base64 data URIs.

## Βήμα 4: Ενεργοποίηση Εκτέλεσης JavaScript

Από προεπιλογή, το Aspose.HTML απενεργοποιεί την εκτέλεση script για ασφάλεια. Ενεργοποιήστε το με `RenderingOptions`:

```java
RenderingOptions renderOptions = new RenderingOptions();
renderOptions.setEnableJavaScript(true);
```

> **Γιατί είναι σημαντικό:** Χωρίς την ενεργοποίηση του JavaScript, η ετικέτα `<script>` στο παράδειγμά μας θα αγνοηθεί και θα καταλήξετε με μια κενή εικόνα. Η ενεργοποίηση επιτρέπει στη μηχανή να αξιολογήσει το `new Date().getFullYear()` και να εισάγει το `<h1>` στο σώμα.

## Βήμα 5: Επιλογή Μορφής Εξόδου και Προορισμού

Θα αποδώσουμε σε αρχείο PNG, αλλά το Aspose υποστηρίζει επίσης JPEG, BMP, GIF και ακόμη PDF. Ορίστε τη διαδρομή και τη μορφή εξόδου ως εξής:

```java
String outputImagePath = "YOUR_DIRECTORY/js_output.png";
ImageRenderDevice imageDevice = new ImageRenderDevice(outputImagePath, ImageFormat.Png);
```

Βεβαιωθείτε ότι ο φάκελος υπάρχει—το Aspose δεν δημιουργεί ενδιάμεσους φακέλους για εσάς.

## Βήμα 6: Απόδοση του Εγγράφου

Τώρα συμβαίνει η μαγεία. Η μέθοδος `render` επεξεργάζεται το DOM, εκτελεί JavaScript, διατάσσει τη σελίδα και γράφει την ραστερική εικόνα:

```java
htmlDocument.render(imageDevice, renderOptions);
System.out.println("Dynamic page rendered – see " + outputImagePath);
```

Όταν τρέξετε το πρόγραμμα, θα δείτε ένα αρχείο με όνομα `js_output.png` που περιέχει μια μεγάλη επικεφαλίδα με το τρέχον έτος.

## Πλήρες Παράδειγμα Εργασίας

Ακολουθεί η πλήρης, αυτόνομη κλάση Java. Αντιγράψτε‑και‑επικολλήστε την σε ένα αρχείο με όνομα `JsExecution.java`, προσαρμόστε το `YOUR_DIRECTORY`, και τρέξτε `javac JsExecution.java && java JsExecution`.

```java
import com.aspose.html.*;
import com.aspose.html.render.*;

public class JsExecution {
    public static void main(String[] args) throws Exception {
        // Step 1: Define HTML that uses JavaScript to display the current year
        String htmlContent = "<script>document.body.innerHTML = '<h1>'+new Date().getFullYear()+'</h1>';</script>";

        // Step 2: Load the HTML string into an Aspose HTML Document
        Document htmlDocument = new Document(htmlContent);

        // Step 3: Create rendering options and enable JavaScript execution
        RenderingOptions renderOptions = new RenderingOptions();
        renderOptions.setEnableJavaScript(true);

        // Step 4: Prepare an image render device for the output PNG file
        String outputImagePath = "YOUR_DIRECTORY/js_output.png";
        ImageRenderDevice imageDevice = new ImageRenderDevice(outputImagePath, ImageFormat.Png);

        // Step 5: Render the final DOM (with JavaScript executed) to the image file
        htmlDocument.render(imageDevice, renderOptions);

        // Step 6: Inform the user that rendering is complete
        System.out.println("Dynamic page rendered – see " + outputImagePath);
    }
}
```

### Αναμενόμενη Έξοδος

Η εκτέλεση του προγράμματος θα δημιουργήσει ένα PNG που μοιάζει περίπου με αυτό:

![Παράδειγμα στιγμιότυπου render html](https://example.com/assets/render-html-example.png "πώς να αποδώσετε html στιγμιότυπο")

*Κείμενο alt εικόνας: “Παράδειγμα στιγμιότυπου render html”* – σημειώστε ότι η κύρια λέξη‑κλειδί εμφανίζεται στο χαρακτηριστικό alt, ικανοποιώντας το SEO για εικόνες.

## Συνηθισμένες Παραλλαγές & Ακραίες Περιπτώσεις

### Απόδοση Πολύπλοκων Σελίδων

Αν το HTML σας περιλαμβάνει εξωτερικά αρχεία CSS, γραμματοσειρές ή εικόνες, έχετε δύο επιλογές:

1. **Απόλυτα URLs** – Διασφαλίστε ότι κάθε πόρος είναι προσβάσιμος μέσω HTTP/HTTPS.
2. **Ενσωματωμένοι Πόροι** – Μετατρέψτε CSS και εικόνες σε Base64 και ενσωματώστε τα απευθείας στο HTML. Αυτό εξαλείφει τα δικτυακά αιτήματα και επιταχύνει την απόδοση.

### Έλεγχος Μεγέθους Εικόνας

Από προεπιλογή το Aspose αποδίδει στα 96 dpi με το πλάτος σελίδας που προέρχεται από το `<meta viewport>` ή το CSS. Για να επιβάλλετε συγκεκριμένο μέγεθος:

```java
renderOptions.setPageSize(new Size(800, 600)); // width x height in pixels
renderOptions.setResolution(150); // DPI
```

### Απενεργοποίηση JavaScript για Στατικές Σελίδες

Αν θέλετε μόνο **να αποθηκεύσετε HTML ως PNG** για στατικό περιεχόμενο, μπορείτε να παραλείψετε το `setEnableJavaScript(true)`. Αυτό βελτιώνει ελαφρώς την απόδοση και αφαιρεί τυχόν ανησυχίες ασφαλείας.

### Λήψη Στιγμιότυπων Πλήρους Σελίδας

Το Aspose αποδίδει το ορατό viewport από προεπιλογή. Για να καταγράψετε ολόκληρη τη σελίδα με κύλιση:

```java
renderOptions.setPageSize(htmlDocument.getDocumentElement().getScrollWidth(),
                          htmlDocument.getDocumentElement().getScrollHeight());
```

Τώρα το παραγόμενο PNG περιλαμβάνει τα πάντα, ακόμη και το περιεχόμενο που κανονικά απαιτεί κύλιση.

## Συμβουλές Απόδοσης

- **Επαναχρησιμοποίηση RenderingOptions** – Αν επεξεργάζεστε πολλές σελίδες, δημιουργήστε ένα μόνο αντικείμενο `RenderingOptions` και τροποποιήστε μόνο τις απαραίτητες ιδιότητες.
- **Batch Rendering** – Για μαζικές μετατροπές, σκεφτείτε τη χρήση `Parallel.ForEach` (ή του Java `parallelStream`) για αξιοποίηση πολλαπλών πυρήνων CPU.
- **Διαχείριση Μνήμης** – Μετά από κάθε απόδοση, καλέστε `htmlDocument.dispose()` για άμεση απελευθέρωση των εγγενών πόρων.

## Συχνές Ερωτήσεις & Αντιμετώπιση Προβλημάτων

| Πρόβλημα | Πιθανή Αιτία | Διόρθωση |
|----------|---------------|----------|
| Το PNG είναι κενό | Απενεργοποιημένο JavaScript ή το HTML δεν προσθέτει ορατά στοιχεία | Βεβαιωθείτε ότι `renderOptions.setEnableJavaScript(true)` και ότι το script γράφει στο DOM |
| Λείπουν εικόνες | Μη επιλυμένα σχετικά URLs | Χρησιμοποιήστε απόλυτα URLs ή ενσωματώστε εικόνες ως Base64 |
| Το κείμενο φαίνεται θολό | Ρύθμιση DPI χαμηλή | Αυξήστε `renderOptions.setResolution(300)` για υψηλής ποιότητας έξοδο |
| Σφάλμα Out‑of‑memory σε μεγάλες σελίδες | Απόδοση πολύ ψηλής σελίδας με προεπιλεγμένο DPI | Μειώστε το DPI ή αποδώστε σε τμήματα και συνδέστε τα αργότερα |

## Επόμενα Βήματα – Από PNG σε PDF, Email ή Web

Τώρα που **μετατρέπετε HTML σε PNG**, ίσως θέλετε:

- **Δημιουργία PDF**: Αντικαταστήστε το `ImageRenderDevice` με `PdfRenderDevice`.
- **Αποστολή μέσω Email**: Συνημμένο το PNG σε ένα `MimeMessage` του JavaMail.
- **Δημιουργία Μικρογραφιών**: Φορτώστε το PNG με `ImageIO` και αλλάξτε το μέγεθος.

Όλα αυτά ακολουθούν το ίδιο μοτίβο—φόρτωση HTML, ρύθμιση `RenderingOptions`, επιλογή συσκευής απόδοσης, και κλήση `render`.

## Συμπέρασμα

Μόλις ολοκληρώσαμε τον οδηγό **πώς να αποδώσετε HTML** σε εικόνα PNG χρησιμοποιώντας το Aspose.HTML for Java. Το tutorial κάλυψε τα πάντα: από τη ρύθμιση της εξάρτησης Maven, την ενεργοποίηση JavaScript, τη διαχείριση πόρων, την προσαρμογή μεγέθους εξόδου, μέχρι την αντιμετώπιση κοινών προβλημάτων. Με αυτή τη γνώση μπορείτε **να μετατρέψετε HTML σε PNG**, **να αποθηκεύσετε HTML ως PNG**, **να καταγράψετε στιγμιότυπο ιστοσελίδας**, και **να δημιουργήσετε εικόνα από HTML** για οποιοδήποτε σενάριο αυτοματοποίησης.

Δοκιμάστε το, πειραματιστείτε με διαφορετικό markup, και αφήστε τη βιβλιοθήκη να κάνει τη βαριά δουλειά. Αν συναντήσετε δυσκολίες, ελέγξτε το FAQ παραπάνω ή εξερευνήστε τα επίσημα docs της Aspose—υπάρχει ένας ολόκληρος κόσμος επιλογών απόδοσης που σας περιμένει.

Καλή προγραμματιστική δουλειά και απολαύστε τα καθαρά στιγμιότυπα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}