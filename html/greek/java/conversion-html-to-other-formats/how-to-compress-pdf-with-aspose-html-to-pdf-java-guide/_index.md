---
category: general
date: 2026-02-14
description: Μάθετε πώς να συμπιέζετε PDF κατά τη μετατροπή HTML σε PDF σε Java χρησιμοποιώντας
  το Aspose HTML. Περιλαμβάνει ορισμό προσαρμοσμένης οθόνης και πλήρες παράδειγμα
  κώδικα.
draft: false
keywords:
- how to compress pdf
- convert html to pdf
- html to pdf java
- aspose html pdf
- set custom screen
language: el
og_description: Πώς να συμπιέσετε PDF κατά τη μετατροπή HTML σε PDF σε Java χρησιμοποιώντας
  το Aspose HTML. Πλήρης βήμα‑βήμα οδηγός με προσαρμοσμένες ρυθμίσεις οθόνης.
og_title: Πώς να συμπιέσετε PDF με το Aspose HTML σε PDF – Οδηγός Java
tags:
- Aspose
- Java
- PDF conversion
title: Πώς να συμπιέσετε PDF με το Aspose HTML σε PDF – Οδηγός Java
url: /el/java/conversion-html-to-other-formats/how-to-compress-pdf-with-aspose-html-to-pdf-java-guide/
---

ensure we didn't miss any code block placeholders: CODE_BLOCK_0 through CODE_BLOCK_7, and CODE_BLOCK_4 etc. They remain.

Check for any other markdown like blockquote we handled.

Now produce final content with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να συμπιέσετε PDF με Aspose HTML σε PDF – Οδηγός Java

Έχετε αναρωτηθεί ποτέ **how to compress pdf** αρχεία εν κινήσει όταν μετατρέπετε σελίδες HTML σε PDF; Δεν είστε ο μόνος. Πολλοί προγραμματιστές συναντούν πρόβλημα όταν τα PDF τους αυξάνονται σε μέγεθος μετά τη μετατροπή, ειδικά σε ιστοσελίδες mobile‑first όπου το bandwidth μετράει. Τα καλά νέα; Με το Aspose.HTML for Java μπορείτε να μειώσετε αυτά τα PDF — και μπορείτε επίσης να πείτε στον μετατροπέα να αποδώσει τη σελίδα σαν να εμφανίζεται σε συσκευή προσαρμοσμένου μεγέθους.

Σε αυτό το tutorial θα περάσουμε από ένα πλήρες, εκτελέσιμο παράδειγμα που σας δείχνει ακριβώς **how to compress pdf** την έξοδο, πώς να **convert html to pdf** σε Java, και πώς να **set custom screen** διαστάσεις ώστε η διάταξη να ταιριάζει με ένα τηλέφωνο 375×667 px. Στο τέλος θα έχετε μια μοναδική κλάση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο Maven ή Gradle και να αρχίσετε αμέσως να δημιουργείτε ελαφριά PDF.

## Τι θα χρειαστείτε

- **Java 17** (ή οποιοδήποτε πρόσφατο JDK· το Aspose.HTML υποστηρίζει Java 8+)
- **Aspose.HTML for Java** βιβλιοθήκη – μπορείτε να την κατεβάσετε από το Maven Central (`com.aspose:aspose-html:23.12` τη στιγμή της συγγραφής)
- Ένα απλό αρχείο HTML (`input.html`) που θέλετε να μετατρέψετε σε PDF
- Ένα IDE ή κειμενογράφο· δεν απαιτείται ειδικό πλαίσιο

> **Pro tip:** Αν χρησιμοποιείτε Maven, προσθέστε την εξάρτηση ως εξής:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Τώρα που τα προαπαιτούμενα έχουν καλυφθεί, ας βουτήξουμε στα πραγματικά βήματα.

## Βήμα 1: Δημιουργία sandbox και ορισμός προσαρμοσμένης οθόνης

Το πρώτο πράγμα που συνήθως κάνετε όταν μετατρέπετε HTML είναι να αποφασίσετε **how the page will be rendered**. Το Aspose.HTML σας επιτρέπει να προσομοιώσετε οποιαδήποτε συσκευή ρυθμίζοντας ένα `Sandbox` με ένα `Screen`. Στην περίπτωση μας θα μιμηθούμε μια τυπική οθόνη smartphone (375 px πλάτος, 667 px ύψος, 96 dpi, κλίμακα 1.0).

```java
// Step 1 – create a sandbox that pretends we’re on a phone screen
Sandbox renderingSandbox = new Sandbox();
renderingSandbox.setScreen(new Screen(375, 667, 96, 1.0));
```

Γιατί να ασχοληθείτε με ένα sandbox; Χωρίς αυτόν, ο μετατροπέας προεπιλέγει ένα viewport τύπου desktop, το οποίο μπορεί να προκαλέσει αλλαγές διάταξης και περιττά μεγάλες σελίδες PDF. Με το **setting a custom screen**, εξασφαλίζετε ότι το PDF ταιριάζει με το mobile design και συχνά μειώνει τον αριθμό των σελίδων — ένας έμμεσος τρόπος να κρατήσετε το μέγεθος του αρχείου χαμηλό.

## Βήμα 2: Διαμόρφωση επιλογών μετατροπής PDF (συμπεριλαμβανομένης της συμπίεσης)

Τώρα λέμε στο Aspose ότι θέλουμε ένα συμπιεσμένο PDF. Η κλάση `PdfConversionOptions` διαθέτει μια σημαία `setCompress` που εκτελεί έναν εσωτερικό βελτιστοποιητή PDF μετά την απόδοση. Μπορείτε επίσης να ρυθμίσετε άλλες επιλογές (όπως η έκδοση PDF ή η ποιότητα εικόνας) αν χρειάζεστε πιο ακριβή έλεγχο.

```java
// Step 2 – define PDF options and enable compression
PdfConversionOptions pdfOptions = new PdfConversionOptions();
pdfOptions.setSandbox(renderingSandbox);   // attach the sandbox from Step 1
pdfOptions.setCompress(true);              // this is the key to how to compress pdf
```

Όταν καλείται `setCompress(true)`, το Aspose αφαιρεί διπλότυπα αντικείμενα, μειώνει την ανάλυση των εικόνων και αφαιρεί αχρησιμοποίητους πόρους. Το αποτέλεσμα είναι συνήθως μια μείωση 30‑50 % στο μέγεθος του αρχείου χωρίς αισθητή οπτική απώλεια.

## Βήμα 3: Εκτέλεση της μετατροπής HTML‑σε‑PDF

Με το sandbox και τις επιλογές έτοιμες, η πραγματική μετατροπή είναι μια γραμμή κώδικα. Απλώς περνάτε το URI του πηγαίου HTML, το URI του προορισμού PDF, και τις επιλογές που δημιουργήσαμε.

```java
// Step 3 – run the conversion
Converter.convert(
        Paths.get("YOUR_DIRECTORY/input.html").toUri(),
        Paths.get("YOUR_DIRECTORY/output.pdf").toUri(),
        pdfOptions);
```

Αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει το `input.html`. Μετά το τέλος της κλήσης, το `output.pdf` θα βρίσκεται δίπλα του, συμπιεσμένο και προσαρμοσμένο σε οθόνη τηλεφώνου.

## Πλήρες, εκτελέσιμο παράδειγμα

Παρακάτω βρίσκεται η πλήρης κλάση Java που συνδυάζει και τα τρία βήματα. Μπορείτε να την αντιγράψετε‑επικολλήσετε σε ένα αρχείο με όνομα `ConvertWithSandbox.java`, να προσαρμόσετε τις διαδρομές, και να εκτελέσετε `javac` + `java` όπως συνήθως.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.rendering.Sandbox;
import com.aspose.html.rendering.Screen;
import java.nio.file.Paths;

/**
 * Demonstrates how to compress PDF while converting HTML to PDF in Java.
 * It also shows how to set a custom screen (375×667 px) to mimic a mobile device.
 */
public class ConvertWithSandbox {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create a sandbox with a custom screen size (mobile‑friendly)
        Sandbox renderingSandbox = new Sandbox();
        renderingSandbox.setScreen(new Screen(375, 667, 96, 1.0));

        // 2️⃣ Set up PDF conversion options – enable compression
        PdfConversionOptions pdfOptions = new PdfConversionOptions();
        pdfOptions.setSandbox(renderingSandbox);
        pdfOptions.setCompress(true); // <-- this is how to compress pdf

        // 3️⃣ Convert the HTML file to a compressed PDF
        Converter.convert(
                Paths.get("YOUR_DIRECTORY/input.html").toUri(),
                Paths.get("YOUR_DIRECTORY/output.pdf").toUri(),
                pdfOptions);

        System.out.println("Conversion complete! Check output.pdf – it should be smaller and fit a 375×667 screen.");
    }
}
```

### Αναμενόμενο αποτέλεσμα

- **File size:** Αν το αρχικό σας HTML παρήγαγε ένα PDF 2 MB, η συμπιεσμένη έκδοση συνήθως θα είναι περίπου 1 MB ή λιγότερο.
- **Page layout:** Οι σελίδες PDF θα είναι 375 pt πλάτος (≈5 ίντσες) και 667 pt ύψος, ταιριάζοντας με τις διαστάσεις που δώσαμε στο sandbox.
- **Visual fidelity:** Το κείμενο παραμένει καθαρό· οι εικόνες μειώνονται μόνο όσο χρειάζεται για να είναι αναγνώσιμες σε καμβά μεγέθους τηλεφώνου.

Μπορείτε να επαληθεύσετε τη μείωση μεγέθους ελέγχοντας τις ιδιότητες του αρχείου πριν και μετά τη μετατροπή.

## Συνηθισμένες παραλλαγές και ειδικές περιπτώσεις

### 1. Θέλετε μεγαλύτερη συμπίεση;

`PdfConversionOptions` προσφέρει περισσότερες ρυθμίσεις:

```java
pdfOptions.setImageQuality(70);   // JPEG quality (0‑100)
pdfOptions.setRemoveUnusedObjects(true);
pdfOptions.setCompress(true);
```

Η μείωση του `setImageQuality` μειώνει περαιτέρω το μέγεθος των εικόνων, αλλά προσέξτε τα εμφανή ελαττώματα σε φωτογραφίες υψηλής ανάλυσης.

### 2. Χρειάζεστε διαφορετικό μέγεθος οθόνης;

Απλώς αλλάξτε τις τιμές στον κατασκευαστή `Screen`:

```java
renderingSandbox.setScreen(new Screen(1024, 768, 96, 1.0)); // tablet size
```

Αυτό είναι χρήσιμο όταν έχετε responsive σχεδιασμούς που φαίνονται διαφορετικά σε tablets σε σχέση με phones.

### 3. Μετατροπή πολλαπλών αρχείων HTML σε βρόχο

Αν έχετε μια δέσμη σελίδων HTML, τυλίξτε την κλήση μετατροπής σε έναν βρόχο `for`:

```java
String[] files = {"page1.html", "page2.html"};
for (String file : files) {
    Converter.convert(
        Paths.get("src/html/" + file).toUri(),
        Paths.get("out/" + file.replace(".html", ".pdf")).toUri(),
        pdfOptions);
}
```

Η ίδια παρουσία `pdfOptions` μπορεί να επαναχρησιμοποιηθεί, διατηρώντας τη συμπίεση συνεπή σε όλα τα αποτελέσματα.

### 4. Διαχείριση εξωτερικών πόρων (CSS, εικόνες)

Το Aspose.HTML επιλύει σχετικές URL βάσει της θέσης του αρχείου HTML. Βεβαιωθείτε ότι τυχόν συνδεδεμένα αρχεία CSS ή εικόνες είναι προσβάσιμα από τον ίδιο φάκελο, ή χρησιμοποιήστε απόλυτες URL (π.χ., `https://example.com/style.css`). Αν ένας πόρος αποτύχει να φορτωθεί, ο μετατροπέας θα καταγράψει μια προειδοποίηση αλλά θα συνεχίσει — έτσι θα λάβετε ακόμη PDF, ίσως χωρίς κάποια στυλ.

## Συχνές ερωτήσεις

**Q: Επηρεάζει η συμπίεση την ασφάλεια του PDF;**  
A: Όχι. Η διαδικασία συμπίεσης βελτιστοποιεί μόνο τη δομή του εσωτερικού PDF· δεν αλλάζει την κρυπτογράφηση ή τις ψηφιακές υπογραφές. Αν χρειάζεται να υπογράψετε το PDF, κάντε το *μετά* τη συμπίεση.

**Q: Μπορώ να μεταφέρω το αποτέλεσμα σε ροή αντί να το γράψω σε αρχείο;**  
A: Απόλυτα. Η `Converter.convert` διαθέτει επίσης υπερφόρτωση που δέχεται `OutputStream`. Αντικαταστήστε το URI προορισμού με ένα `OutputStream` συνδεδεμένο σε απόκριση servlet, για παράδειγμα.

**Q: Τι γίνεται αν χρειάζομαι συμμόρφωση PDF/A;**  
A: Χρησιμοποιήστε `PdfConversionOptions.setPdfACompliance(PdfACompliance.PdfA_1b)` πριν καλέσετε το `convert`. Η συμπίεση λειτουργεί ακόμη· το Aspose θα εφαρμόσει τους κανόνες PDF/A μετά.

## Οπτική επισκόπηση

![διάγραμμα παραδείγματος how to compress pdf](https://example.com/images/compress-pdf-diagram.png "Διάγραμμα που δείχνει τη ροή μετατροπής από HTML → Sandbox (custom screen) → PDF options (compress) → Output PDF")

*Το κείμενο alt περιλαμβάνει τη βασική λέξη-κλειδί για να ικανοποιήσει τις απαιτήσεις SEO.*

## Συμπέρασμα

Καλύψαμε το **how to compress pdf** αρχεία ενώ μετατρέπουμε HTML σε PDF με Java, παρουσιάσαμε τη ροή εργασίας **convert html to pdf** με το Aspose.HTML, και σας δείξαμε πώς να **set custom screen** διαστάσεις για mobile‑φιλικές διατάξεις. Το πλήρες απόσπασμα κώδικα παραπάνω είναι έτοιμο για εκτέλεση, και οι εξηγήσεις σας δίνουν το «γιατί» πίσω από κάθε γραμμή — ώστε να προσαρμόσετε τη λύση στα δικά σας έργα.

Επόμενα βήματα; Δοκιμάστε διαφορετικά μεγέθη οθόνης, ρυθμίστε το `setImageQuality` για πιο σφιχτή συμπίεση, ή συνδέστε τη μετατροπή με ένα βήμα υπογραφής PDF. Μπορείτε επίσης να εξερευνήσετε άλλες μορφές εξόδου του Aspose (π.χ., DOCX ή PNG) χρησιμοποιώντας την ίδια τεχνική sandbox.

Καλή προγραμματιστική, και απολαύστε τα πιο ελαφριά PDF!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}