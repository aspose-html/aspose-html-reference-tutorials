---
date: 2026-06-24
description: Μάθετε πώς να μετατρέψετε HTML σε PDF Java με Aspose.HTML, ορίστε περιθώρια
  σελίδας, προσθέστε αριθμούς σελίδων και κεφαλίδες/υποσέλιδα αποδοτικά.
keywords:
- html to pdf java
- pdf from html java
- html to pdf tutorial
linktitle: Επεκτάσεις CSS - Προσθήκη τίτλου και αριθμού σελίδας
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to convert HTML to PDF Java with Aspose.HTML, set page margins,
    add page numbers and headers/footers efficiently.
  headline: How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML
  type: TechArticle
- description: Learn how to convert HTML to PDF Java with Aspose.HTML, set page margins,
    add page numbers and headers/footers efficiently.
  name: How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML
  steps:
  - name: Initialize Configuration and Define Custom Page Margins
    text: The `Configuration` object holds global settings for the rendering engine.
      By accessing its `IUserAgentService` you can inject a CSS style sheet that has
      the highest priority, ensuring your margins, header, and footer are applied.
  - name: Create the HTML Document
    text: '`HTMLDocument` represents a single HTML file in memory. When you pass the
      previously created `Configuration` to its constructor, the renderer automatically
      uses the custom `@page` rule you defined in Step 1.'
  - name: Render to an XPS File (or any supported output)
    text: '`XpsDevice` writes the rendered pages to an XPS container, but you can
      swap it for `PdfDevice` to get a PDF file instead. The same margin and footer
      definitions are honoured, so the output looks identical regardless of format.'
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java provides a complete HTML‑to‑PDF conversion engine.
    question: What library is needed?
  - answer: Yes – add a CSS `@page` rule to a user‑style sheet and the renderer respects
      it.
    question: Can I control margins programmatically?
  - answer: PDF, XPS, and raster image formats (PNG, JPEG) all honor the same `@page`
      definitions.
    question: Which output formats support margins?
  - answer: A valid Aspose.HTML license is required for any non‑trial deployment.
    question: Do I need a license for production?
  - answer: Absolutely – the library runs on Java 11, 17, and newer LTS releases.
    question: Is this compatible with Java 11+?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Πώς να μετατρέψετε HTML σε PDF Java - Ορισμός περιθωρίων σελίδας με Aspose.HTML
url: /el/java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Μετατρέψετε HTML σε PDF Java: Ορισμός Περιθωρίων Σελίδας με Aspose.HTML

Σε αυτό το σεμινάριο θα ανακαλύψετε **πώς να μετατρέψετε HTML σε PDF Java**‑στυλ χρησιμοποιώντας το Aspose.HTML για Java, ενώ θα μάθετε επίσης πώς να ορίζετε προσαρμοσμένα περιθώρια σελίδας, να εισάγετε αριθμούς σελίδων και να προσθέτετε τίτλο εγγράφου. Θα περάσουμε βήμα‑βήμα καθοδήγηση που μπορείτε να αντιγράψετε στο δικό σας έργο, ώστε να παράγετε επαγγελματικά PDFs απευθείας από HTML σε λίγα μόνο λεπτά.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη χρειάζεται;** Το Aspose.HTML για Java παρέχει μια πλήρη μηχανή μετατροπής HTML‑σε‑PDF.  
- **Μπορώ να ελέγξω τα περιθώρια προγραμματιστικά;** Ναι – προσθέστε έναν κανόνα CSS `@page` σε ένα φύλλο στυλ χρήστη και ο renderer τον τηρεί.  
- **Ποιοι μορφές εξόδου υποστηρίζουν περιθώρια;** Τα PDF, XPS και οι μορφές raster εικόνας (PNG, JPEG) τηρούν όλες τις ίδιες ορισμούς `@page`.  
- **Χρειάζομαι άδεια για παραγωγή;** Απαιτείται έγκυρη άδεια Aspose.HTML για οποιαδήποτε μη‑δοκιμαστική ανάπτυξη.  
- **Είναι συμβατό με Java 11+;** Απόλυτα – η βιβλιοθήκη λειτουργεί σε Java 11, 17 και νεότερες εκδόσεις LTS.  
- **Μπορώ να προσθέσω αριθμούς σελίδων σε Java;** Ναι – χρησιμοποιήστε το κουτί `@bottom-right` στον κανόνα CSS `@page` για να ενσωματώσετε `counter(page)`.

## Τι είναι ο ορισμός περιθωρίων σελίδας HTML σε Java;
Ο ορισμός περιθωρίων σελίδας HTML σε Java σημαίνει ότι λέτε στη μηχανή απόδοσης του Aspose.HTML να εφαρμόσει τις ιδιότητες CSS `@page` πριν το HTML μετατραπεί σε PDF ή XPS. Ορίζοντας έναν προσαρμοσμένο κανόνα `@page` ελέγχετε την εκτυπώσιμη περιοχή, προσθέτετε αριθμούς σελίδων και εισάγετε περιεχόμενο κεφαλίδας/υποσέλιδου—όλα χωρίς πρόγραμμα περιήγησης.

## Γιατί να χρησιμοποιήσετε το Aspose.HTML για έλεγχο περιθωρίων;
Το Aspose.HTML σας παρέχει απόδοση pixel‑perfect, διακομιστή‑πλευρά που λειτουργεί σταθερά σε PDF, XPS και εικόνες. Υποστηρίζει **πάνω από 50 μορφές εισόδου και εξόδου** και μπορεί να επεξεργαστεί έγγραφα με εκατοντάδες σελίδες χωρίς να φορτώνει ολόκληρο το αρχείο στη μνήμη, προσφέροντας ταχύτητες μετατροπής έως **3 × γρηγορότερες** από λύσεις headless‑browser σε παρόμοιο υλικό.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:

1. **Περιβάλλον Ανάπτυξης Java** – Εγκατεστημένο JDK 11 ή νεότερο και ρυθμισμένο `JAVA_HOME`.  
2. **Aspose.HTML για Java** – Κατεβάστε και εγκαταστήστε τη βιβλιοθήκη από [εδώ](https://releases.aspose.com/html/java/).  
3. **Ένα έγκυρο αρχείο άδειας** – Απαιτείται για παραγωγικές εκδόσεις· μια προσωρινή δοκιμαστική άδεια λειτουργεί για δοκιμές.  
4. Μπορείτε επίσης να εξερευνήσετε όλες τις κυκλοφορίες του Aspose [εδώ](https://releases.aspose.com/).

## Εισαγωγή Πακέτων

Οι δηλώσεις `import` φέρνουν τις κλάσεις του Aspose.HTML στο χώρο ονομάτων της Java, ώστε να μπορείτε να τις αναφέρετε χωρίς πλήρως‑καθορισμένα ονόματα.

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Πώς να Μετατρέψετε HTML σε PDF Java με Προσαρμοσμένα Περιθώρια Σελίδας

Φορτώστε το HTML σας, εφαρμόστε ένα φύλλο στυλ χρήστη που ορίζει τον κανόνα `@page` και αποδώστε το έγγραφο σε PDF (ή XPS) σε τρία σύντομα βήματα. Αυτή η προσέγγιση εξαλείφει την ανάγκη για ξεχωριστό κώδικα κεφαλίδας/υποσέλιδου και εγγυάται ότι τα περιθώρια τηρούνται σε όλες τις σελίδες.

### Βήμα 1: Αρχικοποίηση Διαμόρφωσης και Ορισμός Προσαρμοσμένων Περιθωρίων Σελίδας

Το αντικείμενο `Configuration` περιέχει τις παγκόσμιες ρυθμίσεις για τη μηχανή απόδοσης. Με την πρόσβαση στο `IUserAgentService` μπορείτε να ενσωματώσετε ένα φύλλο στυλ CSS με την υψηλότερη προτεραιότητα, εξασφαλίζοντας ότι τα περιθώρια, η κεφαλίδα και το υποσέλιδο σας εφαρμόζονται.

```java
// Initialize configuration object and set up the page-margins for the document
Configuration configuration = new Configuration();
try {
    // Get the User Agent service
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Set the style of custom margins and create marks on it
    userAgent.setUserStyleSheet("@page\n" +
            "{\n" +
            "    /* Page margins should be not empty in order to write content inside the margin-boxes */\n" +
            "    margin-top: 1cm;\n" +
            "    margin-left: 2cm;\n" +
            "    margin-right: 2cm;\n" +
            "    margin-bottom: 2cm;\n" +
            "    /* Page counter located at the bottom of the page */\n" +
            "    @bottom-right\n" +
            "    {\n" +
            "        -aspose-content: \"Page \" currentPageNumber() \" of \" totalPagesNumber();\n" +
            "        color: green;\n" +
            "    }\n" +
            "\n" +
            "    /* Page title located at the top-center box */\n" +
            "    @top-center\n" +
            "    {\n" +
            "        -aspose-content: \"Hello World Document Title!!!\";\n" +
            "        vertical-align: bottom;\n" +
            "        color: blue;\n" +
            "    }\n" +
            "}\n");
```

### Βήμα 2: Δημιουργία του Εγγράφου HTML

`HTMLDocument` αντιπροσωπεύει ένα μόνο αρχείο HTML στη μνήμη. Όταν περνάτε τη δημιουργημένη προηγουμένως `Configuration` στον κατασκευαστή του, ο renderer χρησιμοποιεί αυτόματα τον προσαρμοσμένο κανόνα `@page` που ορίσατε στο Βήμα 1.

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

### Βήμα 3: Απόδοση σε αρχείο XPS (ή οποιαδήποτε υποστηριζόμενη έξοδος)

`XpsDevice` γράφει τις αποδοθείσες σελίδες σε ένα κοντέινερ XPS, αλλά μπορείτε να το αντικαταστήσετε με `PdfDevice` για να λάβετε αρχείο PDF. Οι ίδιες ορισμοί περιθωρίων και υποσέλιδου τηρούνται, έτσι το αποτέλεσμα φαίνεται πανομοιότυπο ανεξάρτητα από τη μορφή.

```java
// Initialize an output device
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    // Send the document to the output device
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

## Συχνά Προβλήματα & Συμβουλές
- **Τα περιθώρια παραμένουν αμετάβλητα** – Επαληθεύστε ότι κανένα άλλο φύλλο στυλ δεν παρακάμπτει τον κανόνα `@page`. Η κλήση `setUserStyleSheet` επιβάλλει τον κανόνα σας με την υψηλότερη προτεραιότητα.  
- **Οι αριθμοί σελίδων εμφανίζουν “NaN”** – Αυτό συμβαίνει με εκδόσεις του Aspose.HTML παλαιότερες από 23.10, οι οποίες δεν διαθέτουν τη λειτουργία `counter(page)`. Αναβαθμίστε στην πιο πρόσφατη έκδοση.  
- **Το αρχείο εξόδου είναι κενό** – Βεβαιωθείτε ότι ο φάκελος `Resources.output` υπάρχει και ότι η διαδικασία Java έχει δικαιώματα εγγραφής.  
- **Τα μεγάλα έγγραφα προκαλούν υψηλή χρήση μνήμης** – Χρησιμοποιήστε το streaming API (`XpsDevice` με `setPageCountLimit`) για επεξεργασία σελίδων σε παρτίδες.  

## Συχνές Ερωτήσεις

### Ε1: Τι είναι το Aspose.HTML για Java;
**Α:** Το Aspose.HTML για Java είναι μια βιβλιοθήκη διακομιστή‑πλευρά που επιτρέπει στους προγραμματιστές να δημιουργούν, επεξεργάζονται, αποδίδουν και μετατρέπουν έγγραφα HTML προγραμματιστικά, υποστηρίζοντας εξόδους PDF, XPS, εικόνας και EPUB.

### Ε2: Μπορώ να προσαρμόσω περαιτέρω τα περιθώρια σελίδας;
**Α:** Ναι – επεξεργαστείτε το CSS μέσα στο `setUserStyleSheet`. Μπορείτε να αλλάξετε οποιεσδήποτε τιμές `margin-*` ή να προσθέσετε επιπλέον κουτιά `@top-*` / `@bottom-*` για πιο σύνθετες κεφαλίδες ή υποσέλιδα.

### Ε3: Πώς μπορώ να προσθέσω περισσότερο περιεχόμενο στο έγγραφο HTML;
**Α:** Αντικαταστήστε τη συμβολοσειρά στο `new HTMLDocument("<div>Hello World!!!</div>", …)` με το δικό σας markup, ή φορτώστε ένα εξωτερικό αρχείο χρησιμοποιώντας τον κατασκευαστή `HTMLDocument(String url, …)`.

### Ε4: Είναι το Aspose.HTML για Java συμβατό με άλλες μορφές εγγράφων;
**Α:** Απόλυτα. Το ίδιο `HTMLDocument` μπορεί να αποδοθεί σε PDF, XPS, PNG, JPEG ή EPUB αντικαθιστώντας τη συσκευή εξόδου (π.χ., `PdfDevice`, `PngDevice`).

### Ε5: Χρειάζομαι άδεια για τη χρήση του Aspose.HTML για Java;
**Α:** Ναι, απαιτείται άδεια για παραγωγική χρήση. Μπορείτε να αποκτήσετε δοκιμαστική ή να αγοράσετε άδεια από [εδώ](https://purchase.aspose.com/buy) ή [εδώ](https://releases.aspose.com/).

### Ε6: Πώς ορίζω διαφορετικά περιθώρια για περιττές και ζυγές σελίδες;
**Α:** Χρησιμοποιήστε τις ψευδο‑κλάσεις `@page :left` και `@page :right` στο φύλλο στυλ σας για να ορίσετε διαφορετικά περιθώρια για τις αριστερές (ζυγές) και δεξιές (περιττές) σελίδες.

### Ε7: Μπορώ να ενσωματώσω προσαρμοσμένες γραμματοσειρές στο αποδοθέν έγγραφο;
**Α:** Ναι. Προσθέστε κανόνες `@font-face` στο φύλλο στυλ χρήστη και αναφερθείτε σε αυτές τις γραμματοσειρές στο HTML markup σας· ο renderer θα τις ενσωματώσει στο τελικό PDF ή XPS.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή συνταγή για **πώς να μετατρέψετε HTML σε PDF Java** χρησιμοποιώντας το Aspose.HTML, συμπεριλαμβανομένων προσαρμοσμένων περιθωρίων σελίδας, αριθμών σελίδων και τίτλου εγγράφου. Εκμεταλλευόμενοι τους κανόνες CSS `@page` αποκτάτε πλήρη έλεγχο της διάταξης χωρίς να γράφετε επιπλέον κώδικα Java για κεφαλίδες ή υποσέλιδα. Πειραματιστείτε με επιπλέον κουτιά `@page`, προσαρμοσμένες γραμματοσειρές ή διαφορετικές συσκευές εξόδου για να καλύψετε τις ακριβείς ανάγκες του συστήματος αναφορών ή τιμολόγησής σας.

Για πιο λεπτομερή καθοδήγηση, συμβουλευτείτε την επίσημη [τεκμηρίωση Aspose.HTML για Java](https://reference.aspose.com/html/java/) και ενταχθείτε στην κοινότητα στο [φόρουμ υποστήριξης Aspose](https://forum.aspose.com/).

---

**Τελευταία Ενημέρωση:** 2026-06-24  
**Δοκιμή Με:** Aspose.HTML for Java 23.12  
**Συγγραφέας:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Σχετικά Σεμινάρια

- [Προσθήκη αριθμών σελίδων με Aspose.HTML Java – Προχωρημένη Χρήση](/html/java/advanced-usage/)
- [Ρύθμιση Μεγέθους Σελίδας PDF με Aspose.HTML για Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Πώς να Μετατρέψετε HTML σε PDF Java – Χρήση Aspose.HTML για Java](/html/java/conversion-html-to-other-formats/convert-html-to-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}