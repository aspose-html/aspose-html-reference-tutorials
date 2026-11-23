---
category: general
date: 2026-03-18
description: Δημιουργήστε PDF από HTML σε Java γρήγορα. Μάθετε πώς να μετατρέπετε
  HTML σε PDF, να προσομοιώνετε την οθόνη iPhone και να ορίζετε το μέγεθος οθόνης
  για ανταποκρινόμενα PDF.
draft: false
keywords:
- create pdf from html
- convert html to pdf
- simulate iphone screen
- how to set screen
- how to convert html
language: el
og_description: Δημιουργήστε PDF από HTML σε Java. Αυτός ο οδηγός δείχνει πώς να μετατρέψετε
  το HTML σε PDF, να προσομοιώσετε την οθόνη iPhone και να ορίσετε τις διαστάσεις
  της οθόνης για τέλεια ανταποκρινόμενα PDF.
og_title: Δημιουργία PDF από HTML με Προσαρμογή Προβολής για Κινητά – Εγχειρίδιο Java
tags:
- Java
- Aspose.HTML
- PDF
- Responsive Design
- Mobile Viewport
title: Δημιουργία PDF από HTML με Προβολή για κινητά – Πλήρης Οδηγός Java
url: /el/java/conversion-html-to-other-formats/create-pdf-from-html-with-mobile-viewport-complete-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PDF from HTML with Mobile Viewport – Complete Java Guide

Έχετε ποτέ χρειαστεί να **create PDF from HTML** αλλά το αποτέλεσμα έδειχνε σαν σελίδα επιφάνειας εργασίας σε μικρή οθόνη τηλεφώνου; Δεν είστε ο μόνος. Όταν μετατρέπετε έναν ανταποκρινόμενο ιστότοπο σε PDF, το προεπιλεγμένο viewport συχνά αγνοεί τα mobile breakpoints, αφήνοντάς σας με ένα στενό χάος.  

Τα καλά νέα; Μπορείτε να **convert HTML to PDF** ενώ **simulating an iPhone screen**, όλα από απλό κώδικα Java. Σε αυτό το tutorial θα περάσουμε από κάθε βήμα—πώς να ορίσετε το μέγεθος της οθόνης, πώς να ρυθμίσετε το device‑scale factor, και γιατί αυτές οι ρυθμίσεις είναι σημαντικές για ένα pixel‑perfect PDF.

> **Pro tip:** Αν έχετε ήδη χρησιμοποιήσει το Aspose.HTML για απλές μετατροπές, θα βρείτε τις ρυθμίσεις του viewport μόλις μερικές επιπλέον γραμμές μακριά.

---

## What You’ll Learn

* Πώς να **create PDF from HTML** χρησιμοποιώντας το Aspose.HTML for Java.  
* Ο ακριβής κώδικας για **simulate iPhone screen** διαστάσεις (375 × 667 px @ 2× density).  
* Πού να τοποθετήσετε τις επιλογές **how to set screen** στη διαδικασία μετατροπής.  
* Συνηθισμένα προβλήματα όταν μετατρέπετε responsive σελίδες και πώς να τα αποφύγετε.  
* Ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα Java που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο IDE σας.

### Prerequisites

* Java 17 ή νεότερη (ο κώδικας μεταγλωττίζεται και με παλαιότερες εκδόσεις, αλλά συνιστάται η 17).  
* Βιβλιοθήκη Aspose.HTML for Java – μπορείτε να κατεβάσετε το τελευταίο JAR από το [Aspose website](https://products.aspose.com/html/java).  
* Ένα απλό αρχείο HTML (`input.html`) που θέλετε να μετατρέψετε σε PDF.  
* Βασική εξοικείωση με Maven ή Gradle (θα δείξουμε ένα απόσπασμα Maven).

---

## Step 1 – Add Aspose.HTML to Your Project

Πρώτα απ' όλα, χρειάζεστε τη βιβλιοθήκη στο classpath σας. Αν χρησιμοποιείτε Maven, προσθέστε αυτή την εξάρτηση στο `pom.xml` σας:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Why this matters:** Το Aspose.HTML αναλαμβάνει το βαρέως τύπου έργο—την ανάλυση HTML, την εφαρμογή CSS και τη rasterization της διάταξης. Χωρίς αυτό, θα έπρεπε να γράψετε έναν πλήρη μηχανισμό περιήγησης μόνοι σας, κάτι που είναι *πολύ* δουλειά.

Αν προτιμάτε Gradle, το ισοδύναμο είναι:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

---

## Step 2 – Prepare Load Options and Simulate an iPhone Viewport

Τώρα θα ρυθμίσουμε τις παραμέτρους **how to set screen**. Η κλάση `HtmlLoadOptions` σας επιτρέπει να πείτε στο Aspose ποιο μέγεθος και ποια πυκνότητα pixel πρέπει να προσποιηθεί ότι έχει ο φυλλομετρητής.

```java
import com.aspose.html.*;
import com.aspose.html.rendering.*;

public class ViewportDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create load options for the HTML document
        HtmlLoadOptions loadOptions = new HtmlLoadOptions();

        // 2️⃣ Simulate a mobile viewport (iPhone 6/7/8) – 375 × 667 pixels with retina density
        loadOptions.setScreenSize(new Size(375, 667));
        loadOptions.setDeviceScaleFactor(2.0);

        // 3️⃣ Convert the HTML file to PDF using the configured viewport
        Converter.convertDocument(
                "YOUR_DIRECTORY/input.html",          // source HTML
                "YOUR_DIRECTORY/output.pdf",          // destination PDF
                new PdfSaveOptions(),
                loadOptions);

        // 4️⃣ Notify that the conversion is complete
        System.out.println("Responsive conversion using mobile viewport.");
    }
}
```

### Why These Numbers?

* **375 × 667** ταιριάζει με τις λογικές διαστάσεις CSS pixel ενός iPhone 6/7/8 σε portrait mode.  
* **DeviceScaleFactor = 2.0** λέει στον renderer ότι κάθε CSS pixel αντιστοιχεί σε δύο φυσικά pixels, μιμείται την Retina οθόνη.  

Αν χρειάζεστε διαφορετική συσκευή—π.χ. iPhone 12 Pro Max—απλώς αλλάζετε το μέγεθος σε `428 × 926` και διατηρείτε το scale factor στο `3.0`.

---

## Step 3 – Run the Conversion and Verify the Output

Συγκεντρώστε και εκτελέστε την κλάση:

```bash
mvn compile exec:java -Dexec.mainClass=ViewportDemo
```

Μετά το τέλος του προγράμματος, ανοίξτε το `output.pdf`. Θα πρέπει να δείτε:

* Όλες οι media queries που στοχεύουν `max-width: 375px` να έχουν εφαρμοστεί σωστά.  
* Εικόνες να αποδίδονται οξυμένες χάρη στο 2× scale factor.  
* Κείμενο που σέβεται την ιεραρχία mobile font‑size που ορίσατε στο CSS.

Αν το PDF εξακολουθεί να μοιάζει με σελίδα desktop, ελέγξτε ξανά ότι το HTML σας χρησιμοποιεί responsive meta tags:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Χωρίς αυτήν την ετικέτα, ακόμη και η τέλεια ρύθμιση viewport δεν θα ενεργοποιήσει το mobile stylesheet.

---

## Step 4 – Handling External Resources (Images, Fonts, CSS)

Όταν **convert HTML to PDF**, το Aspose.HTML προσπαθεί να φορτώσει κάθε συνδεδεμένο πόρο. Αν μετατρέπετε μια σελίδα που βρίσκεται σε τοπικό σύστημα αρχείων, τα απόλυτα URLs (`file:///…`) λειτουργούν κανονικά. Για απομακρυσμένους πόρους μπορεί να αντιμετωπίσετε:

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **404 errors for images** | Το HTML δείχνει σε URL που απαιτεί πιστοποίηση. | Χρησιμοποιήστε `HtmlLoadOptions.setBaseUrl("file:///C:/myproject/")` για να επιλύσετε σχετικές διαδρομές, ή ενσωματώστε εικόνες ως Base64. |
| **Missing web fonts** | Η μηχανή PDF δεν μπορεί να κατεβάσει το αρχείο γραμματοσειράς. | Κατεβάστε τα αρχεία `.woff`/`.ttf` τοπικά και αναφέρετέ τα με σχετική διαδρομή. |
| **CSS not applied** | Το αρχείο CSS εμποδίζεται από CORS. | Φιλοξενήστε το CSS σε διακομιστή που επιτρέπει cross‑origin αιτήματα, ή ενσωματώστε το CSS απευθείας στο HTML. |

Ένας γρήγορος τρόπος για να δοκιμάσετε τη φόρτωση πόρων είναι να τυλίξετε την κλήση μετατροπής σε try‑catch block και να εκτυπώσετε το μήνυμα του `Exception`. Το Aspose.HTML παρέχει λεπτομερή logs που δείχνουν το ακριβές URL που απέτυχε.

```java
try {
    Converter.convertDocument(...);
} catch (Exception ex) {
    System.err.println("Conversion failed: " + ex.getMessage());
}
```

---

## Step 5 – Advanced Tweaks (Optional)

### a) Change PDF Page Size

Από προεπιλογή το Aspose.HTML δημιουργεί μια σελίδα PDF που ταιριάζει στο μέγεθος του viewport. Αν προτιμάτε A4 ή Letter, προσθέστε μια ρύθμιση `PdfSaveOptions`:

```java
PdfSaveOptions pdfOptions = new PdfSaveOptions();
pdfOptions.setPageSize(PageSize.A4);
Converter.convertDocument("input.html", "output.pdf", pdfOptions, loadOptions);
```

### b) Add a Header/Footer Programmatically

Μπορείτε να ενσωματώσετε ένα απλό header/footer μετά τη μετατροπή χρησιμοποιώντας το Aspose.PDF (διαφορετική βιβλιοθήκη). Η ροή εργασίας είναι:

1. Convert HTML → PDF (όπως φαίνεται).  
2. Ανοίξτε το παραγόμενο PDF με Aspose.PDF.  
3. Προσθέστε αντικείμενα `HeaderFooter` σε κάθε σελίδα.

```java
import com.aspose.pdf.*;

Document pdfDoc = new Document("output.pdf");
for (Page page : pdfDoc.getPages()) {
    page.addHeaderFooter(new HeaderFooter("Generated on " + LocalDate.now()));
}
pdfDoc.save("output-with-header.pdf");
```

### c) Batch Conversion

Αν έχετε φάκελο με αρχεία HTML, κάντε βρόχο πάνω τους:

```java
Files.list(Paths.get("html_folder"))
     .filter(p -> p.toString().endsWith(".html"))
     .forEach(p -> {
         String pdfPath = p.toString().replace(".html", ".pdf");
         Converter.convertDocument(p.toString(), pdfPath, new PdfSaveOptions(), loadOptions);
     });
```

---

## Frequently Asked Questions (FAQs)

**Q: Does this work with JavaScript‑heavy pages?**  
A: Το Aspose.HTML υποστηρίζει ένα υποσύνολο της JavaScript. Απλή διαχείριση DOM και αλλαγές CSS συνήθως λειτουργούν, αλλά πολύπλοκα frameworks (React, Angular) μπορεί να χρειάζονται ένα προ‑rendered static HTML snapshot.

**Q: What if I need to convert a page that uses `@media print` rules?**  
A: Η βιβλιοθήκη σέβεται αυτόματα το `@media print`. Ωστόσο, αν έχετε επίσης ορίσει mobile viewport, το stylesheet `print` μπορεί να υπερισχύσει κάποιων mobile στυλ. Δοκιμάστε και τις δύο περιπτώσεις.

**Q: Can I set a custom DPI for the PDF?**  
A: Ναι. Χρησιμοποιήστε `PdfSaveOptions.setDpi(300)` πριν τη μετατροπή. Υψηλότερο DPI δίνει μεγαλύτερα αρχεία αλλά πιο οξυμένες εικόνες.

---

## Expected Result Screenshot

Below is an illustration of the final PDF page (mobile viewport simulated).  
![Screenshot of PDF generated by create pdf from html demo showing iPhone‑sized layout]  

*Image alt text includes the primary keyword for SEO.*

---

## Conclusion

Τώρα έχετε μια στιβαρή, **create pdf from html** ροή εργασίας που σέβεται τα mobile breakpoints, προσομοιώνει μια οθόνη iPhone, και σας δίνει πλήρη έλεγχο στις διαστάσεις της σελίδας. Με τις ρυθμίσεις του `HtmlLoadOptions` μπορείτε να απαντήσετε στο “**how to set screen**” για οποιαδήποτε συσκευή, και με το `Converter.convertDocument` έχετε κατακτήσει το **how to convert html** σε Java.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να συνδυάσετε αυτήν την προσέγγιση με το Aspose.PDF για να προσθέσετε υδατογραφήματα, να συγχωνεύσετε πολλαπλά PDFs, ή να προστατέψετε το έγγραφο με κωδικό. Και μην ξεχάσετε να πειραματιστείτε με άλλες συσκευές—απλώς αλλάξτε τις τιμές `Size` και `DeviceScaleFactor` ώστε να ταιριάζουν στην πυκνότητα pixel που χρειάζεστε.

Happy coding, and may your PDFs always look as crisp on paper as they do on a phone screen! 

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}