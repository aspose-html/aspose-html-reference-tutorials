---
category: general
date: 2026-02-13
description: Μάθετε πώς να χρησιμοποιείτε sandbox κατά τη μετατροπή HTML σε PDF με
  Java, να απενεργοποιήσετε τη JavaScript, να ορίσετε προσαρμοσμένο user agent και
  να λαμβάνετε αξιόπιστα PDF γρήγορα.
draft: false
keywords:
- how to use sandbox
- html to pdf java
- convert html to pdf
- how to disable javascript
- set user agent
language: el
og_description: Μάθετε πώς να χρησιμοποιείτε το sandbox για μετατροπές HTML σε PDF
  με Java, να απενεργοποιήσετε τη JavaScript και να ορίσετε έναν πράκτορα χρήστη σε
  λίγα μόνο λεπτά.
og_title: Πώς να χρησιμοποιήσετε το Sandbox για HTML σε PDF Java – Πλήρης Οδηγός
tags:
- Java
- Aspose.HTML
- PDF conversion
- Sandbox
title: Πώς να χρησιμοποιήσετε το Sandbox για HTML σε PDF Java – Οδηγός βήμα‑βήμα
url: /el/java/advanced-usage/how-to-use-sandbox-for-html-to-pdf-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Χρησιμοποιήσετε το Sandbox για HTML σε PDF με Java – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να χρησιμοποιήσετε το sandbox** όταν χρειάζεται να μετατρέψετε μια σελίδα HTML σε PDF με Java; Δεν είστε ο μόνος—πολλοί προγραμματιστές συναντούν εμπόδια όταν το HTML τους εξαρτάται από scripts ή από ένα συγκεκριμένο αποτύπωμα προγράμματος περιήγησης, και η μετατροπή δεν μοιάζει καθόλου με το αρχικό.  

Τα καλά νέα; Με την κλάση `Sandbox` του Aspose.HTML μπορείτε να **απενεργοποιήσετε τη JavaScript**, να προσομοιώσετε ένα **user agent**, και να διατηρήσετε τη μετατροπή σε sandbox ώστε να μην αγγίζει ποτέ το πραγματικό σύστημα αρχείων. Σε αυτό το tutorial θα περάσουμε βήμα-βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που δείχνει τη μετατροπή **html to pdf java**, καλύπτει το **πώς να απενεργοποιήσετε τη javascript**, και εξηγεί πώς να **ορίσετε user agent** για καθοριστικό αποτέλεσμα.

## Τι Θα Δημιουργήσετε

1. Δημιουργεί ένα sandbox που προσομοιώνει οθόνη 800 × 600.  
2. Μετατρέπει το `input.html` σε `output.pdf` χωρίς να εκτελεί καμία JavaScript.  
3. Στέλνει μια προσαρμοσμένη συμβολοσειρά user‑agent ώστε η σελίδα να αποδίδει ακριβώς όπως αναμένετε.  

Χωρίς εξωτερικές υπηρεσίες, χωρίς κρυφή μαγεία—μόνο απλή Java και Aspose.HTML.

## Προαπαιτούμενα

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK) εγκατεστημένο και ορισμένο `JAVA_HOME`.  
- **Aspose.HTML for Java 4.0** JARs στο classpath σας. Μπορείτε να τα κατεβάσετε από το επίσημο αποθετήριο Maven ή από τον ιστότοπο Aspose.  
- Ένα απλό αρχείο `input.html` σε φάκελο που ελέγχετε.  

Αυτό είναι όλο. Αν έχετε ήδη ένα Maven project, προσθέστε την εξάρτηση:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>4.0</version>
</dependency>
```

Διαφορετικά, απλώς τοποθετήστε τα JARs στο `libs/` και αναφερθείτε σε αυτά στη γραμμή εντολών.

---

## Πώς να Χρησιμοποιήσετε το Sandbox για Ασφαλή Μετατροπή HTML σε PDF

### Βήμα 1: Αρχικοποίηση του Sandbox

Το sandbox είναι η καρδιά της λύσης. Απομονώνει τη μηχανή μετατροπής, προσποιείται ότι είναι συγκεκριμένου μεγέθους συσκευής, και—βασικά—σας επιτρέπει να **απενεργοποιήσετε τη JavaScript**. Ακολουθεί ο κώδικας:

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // Create a sandbox that mimics an 800×600 screen
        Sandbox sandbox = new Sandbox();
        sandbox.setDeviceSize(new Size(800, 600));

        // Disable JavaScript execution – this is how to disable JavaScript in the sandbox
        sandbox.setEnableJavaScript(false);

        // Spoof a custom user‑agent so the page thinks it’s being rendered by AsposeHTML/4.0
        sandbox.setUserAgent("AsposeHTML/4.0 (Java)");
```

**Γιατί είναι σημαντικό:**  
- Το **μέγεθος συσκευής** επηρεάζει τα CSS media queries (`@media screen and (max-width:…)`).  
- Η **απενεργοποίηση της JavaScript** αποτρέπει τα scripts από το να τροποποιούν το DOM, κάτι που είναι απαραίτητο όταν χρειάζεστε καθοριστικό PDF.  
- Ένα **προσαρμοσμένο user agent** μπορεί να αναγκάσει τον server να σερβίρει μια mobile‑φιλική διάταξη ή ένα συγκεκριμένο stylesheet.

> *Pro tip:* Αν αργότερα χρειαστείτε JavaScript για μια συγκεκριμένη σελίδα, απλώς ορίστε `sandbox.setEnableJavaScript(true);`—το ίδιο sandbox μπορεί να επαναχρησιμοποιηθεί.

### Βήμα 2: Προετοιμασία Επιλογών Μετατροπής PDF

Το `PdfConvertOptions` του Aspose.HTML σας δίνει λεπτομερή έλεγχο του αποτελέσματος. Για αυτή τη demo οι προεπιλογές είναι τέλειες, αλλά μπορείτε να ρυθμίσετε DPI, ενσωμάτωση γραμματοσειρών ή έκδοση PDF αν το επιθυμείτε.

```java
        // Default PDF conversion options – good enough for most html to pdf java scenarios
        PdfConvertOptions pdfOptions = new PdfConvertOptions();
```

**Γιατί μπορεί να το αλλάξετε:**  
- Υψηλότερο DPI για PDF έτοιμα για εκτύπωση.  
- `pdfOptions.setEmbedStandardFonts(true);` για να εγγυηθείτε την πιστότητα των γραμματοσειρών σε οποιονδήποτε υπολογιστή.

### Βήμα 3: Μετατροπή του Αρχείου HTML Χρησιμοποιώντας το Sandbox

Τώρα ενώνουμε όλα τα κομμάτια. Η μέθοδος `Converter.convert` παίρνει τη διαδρομή του πηγαίου HTML, τη διαδρομή του στόχου PDF, τις επιλογές μετατροπής, και το sandbox που διαμορφώσαμε.

```java
        // Perform the conversion inside the sandbox
        Converter.convert(
                "YOUR_DIRECTORY/input.html",   // source HTML (html to pdf java)
                "YOUR_DIRECTORY/output.pdf",   // target PDF
                pdfOptions,
                sandbox);                      // sandbox applied here

        System.out.println("PDF generated with sandbox settings.");
    }
}
```

Αν όλα είναι σωστά συνδεδεμένα, θα δείτε το μήνυμα στην κονσόλα και θα βρείτε το `output.pdf` δίπλα στο αρχείο HTML σας.

### Βήμα 4: Επαλήθευση του Αποτελέσματος

Ανοίξτε το παραγόμενο PDF σε οποιονδήποτε προβολέα. Θα πρέπει να δείτε μια πιστή απόδοση του `input.html` **χωρίς καμία αλλαγή που προέρχεται από JavaScript**. Οι διαστάσεις της σελίδας θα ταιριάζουν με το μέγεθος συσκευής 800 × 600, και το περιεχόμενο θα αντανακλά το **ορισμένο user agent** που δώσατε.

> *Τι γίνεται αν το PDF φαίνεται κενό;* Ελέγξτε ξανά ότι το αρχείο HTML είναι προσβάσιμο και ότι απενεργοποιήσατε τη JavaScript μόνο όταν το θέλατε. Μερικές φορές εξωτερικοί πόροι (γραμματοσειρές, εικόνες) χρειάζονται πρόσβαση στο δίκτυο· το sandbox μπορεί να ρυθμιστεί ώστε να επιτρέπει ή να μπλοκάρει αυτά επίσης.

---

## Πώς να Απενεργοποιήσετε τη JavaScript στο Sandbox (Δευτερεύουσα Λέξη-Κλειδί)

Αν ενδιαφέρεστε μόνο για το τμήμα **πώς να απενεργοποιήσετε τη javascript**, η βασική γραμμή είναι:

```java
sandbox.setEnableJavaScript(false);
```

Αυτή η εντολή λέει στη μηχανή απόδοσης να αγνοήσει τυχόν ετικέτες `<script>`, χειριστές `onclick`, ή ενσωματωμένα URLs `javascript:`. Είναι ο πιο ασφαλής τρόπος για να εγγυηθείτε ότι η έξοδος PDF δεν θα τροποποιηθεί από λογική στην πλευρά του πελάτη.

### Πότε Μπορείτε να Διατηρήσετε τη JavaScript Ενεργοποιημένη;

- Μετατροπή μιας εφαρμογής μονής σελίδας που βασίζεται σε χειρισμό του DOM για την κατασκευή της τελικής προβολής.  
- Δημιουργία γραφημάτων με βιβλιοθήκη όπως Chart.js που σχεδιάζει σε στοιχείο canvas.  

Σε αυτές τις περιπτώσεις, θα ορίσετε τη σημαία σε `true` και πιθανόν να αυξήσετε το timeout του sandbox ώστε τα scripts να έχουν αρκετό χρόνο για να ολοκληρωθούν.

## Ορισμός User Agent για Μετατροπές HTML σε PDF με Java

Ορισμένοι ιστότοποι σερβίρουν διαφορετικό markup ανάλογα με το πρόγραμμα περιήγησης του επισκέπτη. Με το **set user agent** μπορείτε να αναγκάσετε τον server να παρέχει μια συνεπή διάταξη.

```java
sandbox.setUserAgent("AsposeHTML/4.0 (Java)");
```

Αντικαταστήστε τη συμβολοσειρά με οποιοδήποτε έγκυρο user‑agent, π.χ., `"Mozilla/5.0 (Windows NT 10.0; Win64; x64)"` αν χρειάζεστε αποτύπωμα παρόμοιο με το Chrome.

### Γιατί Βοηθά

- Αποφεύγει στυλ μόνο για κινητές συσκευές όταν θέλετε ένα PDF στυλ desktop.  
- Παρακάμπτει τον περιορισμό λειτουργιών που κρύβει περιεχόμενο από άγνωστους browsers.

## Εικονογραφική Παράσταση

![how to use sandbox diagram](sandbox-diagram.png "how to use sandbox diagram")

*Το διάγραμμα δείχνει τη ροή: HTML → Sandbox (μέγεθος, JS απενεργοποιημένο, UA ορισμένο) → PDF.*

## Συνηθισμένα Προβλήματα & Πρακτικές Συμβουλές

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Blank PDF** | Η JavaScript αφαίρεσε κρίσιμους κόμβους του DOM. | Ενεργοποιήστε προσωρινά τη JavaScript ή προεπεξεργαστείτε το HTML ώστε να περιλαμβάνει στατικό περιεχόμενο. |
| **Missing Fonts** | Τα αρχεία γραμματοσειρών δεν είναι ενσωματωμένα ή δεν είναι προσβάσιμα. | Χρησιμοποιήστε `pdfOptions.setEmbedStandardFonts(true);` ή βεβαιωθείτε ότι οι γραμματοσειρές είναι διαθέσιμες τοπικά. |
| **Incorrect Layout** | Ασυμφωνία μεγέθους συσκευής. | Προσαρμόστε `sandbox.setDeviceSize(new Size(width, height));` ώστε να ταιριάζει με τα CSS media queries σας. |
| **Network Timeouts** | Το sandbox μπλοκάρει εξωτερικούς πόρους. | Καλέστε `sandbox.setAllowNetwork(true);` αν χρειάζεστε απομακρυσμένες εικόνες ή stylesheets. |

## Πλήρες Παράδειγμα Εργασίας (Όλος ο Κώδικας σε Ένα Σημείο)

```java
import com.aspose.html.*;
import com.aspose.html.converters.*;
import com.aspose.html.sandbox.*;

public class SandboxExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox that simulates an 800×600 screen and disables JavaScript
        Sandbox sandbox = new Sandbox();
        sandbox.setDeviceSize(new Size(800, 600));
        sandbox.setEnableJavaScript(false);               // how to disable javascript
        sandbox.setUserAgent("AsposeHTML/4.0 (Java)");     // set user agent

        // 2️⃣ Prepare PDF conversion options (default settings are fine for this demo)
        PdfConvertOptions pdfOptions = new PdfConvertOptions();

        // 3️⃣ Convert the HTML file to PDF using the configured sandbox
        Converter.convert(
                "YOUR_DIRECTORY/input.html",   // source HTML (html to pdf java)
                "YOUR_DIRECTORY/output.pdf",   // target PDF
                pdfOptions,
                sandbox);                      // sandbox applied here

        // 4️⃣ Inform the user that the PDF has been generated
        System.out.println("PDF generated with sandbox settings.");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Μετά την εκτέλεση `java -cp ".;aspose-html-4.0.jar" SandboxExample`, η κονσόλα εμφανίζει *“PDF generated with sandbox settings.”* και το `output.pdf` εμφανίζεται στον καθορισμένο φάκελο, αντιπροσωπεύοντας πιστά το αρχικό HTML—χωρίς JavaScript, προσαρμοσμένο user‑agent, και με σωστές διαστάσεις.

## Συμπέρασμα

Καλύψαμε **πώς να χρησιμοποιήσετε το sandbox** για μια καθαρή, επαναλήψιμη ροή εργασίας **html to pdf java**, δείξαμε τη συγκεκριμένη γραμμή για **απενεργοποίηση της JavaScript**, παρουσιάσαμε **ορισμό user agent**, και παρέχουμε ένα πλήρες, έτοιμο για αντιγραφή πρόγραμμα.  

Αν είστε έτοιμοι να προχωρήσετε πέρα από τα βασικά, δοκιμάστε να αλλάξετε το μέγεθος της συσκευής, να ενεργοποιήσετε την πρόσβαση δικτύου, ή να πειραματιστείτε με διαφορετικές επιλογές PDF όπως επίπεδα συμπίεσης. Το ίδιο μοτίβο λειτουργεί για μετατροπή πολλαπλών αρχείων HTML σε batch, ή ακόμη και για απόδοση δυναμικών αναφορών που δημιουργούνται σε πραγματικό χρόνο.

Έχετε ερωτήσεις για ειδικές περιπτώσεις, ή θέλετε να δείτε πώς να ενσωματώσετε γραμματοσειρές για διεθνή PDFs; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}