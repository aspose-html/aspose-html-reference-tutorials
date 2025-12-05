---
date: 2025-12-05
description: Μάθετε πώς να ορίζετε τα περιθώρια σελίδας HTML με Java χρησιμοποιώντας
  το Aspose.HTML και να προσθέτετε αριθμούς σελίδων και τίτλους στα έγγραφά σας.
language: el
linktitle: CSS Extensions - Adding Title and Page Number
second_title: Java HTML Processing with Aspose.HTML
title: Πώς να ορίσετε τα περιθώρια σελίδας HTML σε Java με το Aspose.HTML
url: /java/advanced-usage/css-extensions-adding-title-page-number/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε τα περιθώρια σελίδας HTML σε Java με το Aspose.HTML

Σε αυτό το σεμινάριο θα ανακαλύψετε **πώς να ορίσετε τα περιθώρια σελίδας HTML σε Java**‑στυλ χρησιμοποιώντας το Aspose.HTML για Java. Θα περάσουμε από τη δημιουργία προσαρμοσμένων περιθωρίων σελίδας, την εισαγωγή αριθμών σελίδων και την προσθήκη τίτλου εγγράφου—όλα με σαφή, βήμα‑βήμα κώδικα που μπορείτε να αντιγράψετε στο δικό σας έργο.

## Γρήγορες Απαντήσεις
- **What library is needed?** Aspose.HTML for Java  
- **Can I control margins programmatically?** Ναι, μέσω ενός κανόνα CSS `@page` στο φύλλο στυλ του χρήστη  
- **Which output formats support margins?** XPS, PDF και άλλες μορφές raster  
- **Do I need a license for production?** Απαιτείται έγκυρη άδεια Aspose.HTML για χρήση εκτός δοκιμής  
- **Is this compatible with Java 11+?** Απόλυτα – η βιβλιοθήκη λειτουργεί με σύγχρονες εκδόσεις της Java  

## Τι είναι η «Ρύθμιση περιθωρίων σελίδας HTML σε Java»;
Η ρύθμιση των περιθωρίων σελίδας HTML σε Java σημαίνει τη διαμόρφωση της μηχανής απόδοσης (που παρέχεται από το Aspose.HTML) ώστε να εφαρμόζει τις ιδιότητες CSS page‑box πριν το έγγραφο μετατραπεί σε εκτυπώσιμη μορφή όπως XPS ή PDF. Ορίζοντας έναν προσαρμοσμένο κανόνα `@page` ελέγχετε την εκτυπώσιμη περιοχή, τους αριθμούς σελίδων και το περιεχόμενο της κεφαλίδας/υποσέλιδου.

## Γιατί να χρησιμοποιήσετε το Aspose.HTML για έλεγχο περιθωρίων;
- **Ακριβής διάταξη** – CSS `@page` σας παρέχει έλεγχο pixel‑perfect στα περιθώρια, τις κεφαλίδες και τα υποσέλιδα.  
- **Συνεπής σε πολλαπλές μορφές** – Οι ίδιες ορισμοί περιθωρίων λειτουργούν για XPS, PDF και εξόδους εικόνας.  
- **Χωρίς εξάρτηση από πρόγραμμα περιήγησης** – Η απόδοση γίνεται στο διακομιστή, επομένως δεν χρειάζεστε headless browser.  

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:

1. **Περιβάλλον Ανάπτυξης Java** – Εγκατεστημένο JDK 11 ή νεότερο.  
2. **Aspose.HTML for Java** – Κατεβάστε και εγκαταστήστε τη βιβλιοθήκη από [here](https://releases.aspose.com/html/java/).  

## Εισαγωγή Πακέτων

Για να ξεκινήσετε, εισάγετε τις απαραίτητες κλάσεις του Aspose.HTML:

```java
// Import Aspose.HTML packages
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

## Πώς να ορίσετε τα περιθώρια σελίδας HTML σε Java – Οδηγός βήμα‑βήμα

### Βήμα 1: Αρχικοποίηση Διαμόρφωσης και Ορισμός Προσαρμοσμένων Περιθωρίων Σελίδας

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

Σε αυτό το τμήμα δημιουργούμε ένα αντικείμενο `Configuration`, λαμβάνουμε το `IUserAgentService` και ενσωματώνουμε έναν κανόνα CSS `@page` που ορίζει τα περιθώρια, έναν μετρητή σελίδας κάτω‑δεξιά, και έναν τίτλο εγγράφου στην κορυφή‑κέντρο.

### Βήμα 2: Δημιουργία του HTML Εγγράφου

```java
// Initialize an HTML document
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Εδώ δημιουργούμε ένα `HTMLDocument` με ένα απλό απόσπασμα “Hello World”. Η ίδια διαμόρφωση από το Βήμα 1 εφαρμόζεται, ώστε τα προσαρμοσμένα περιθώρια να τηρούνται όταν το έγγραφο αποδίδεται.

### Βήμα 3: Απόδοση σε αρχείο XPS (ή οποιαδήποτε υποστηριζόμενη έξοδος)

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

Αυτό το βήμα δημιουργεί ένα `XpsDevice` που γράφει τις αποδοθείσες σελίδες στο `output.xps`. Τα περιθώρια, οι αριθμοί σελίδων και ο τίτλος που ορίσατε νωρίτερα θα εμφανιστούν στο τελικό αρχείο.

## Συνηθισμένα Προβλήματα & Συμβουλές

- **Τα περιθώρια εμφανίζονται αμετάβλητα** – Βεβαιωθείτε ότι ο κανόνας `@page` δεν παρακάμπτεται από άλλα φύλλα στυλ. Η κλήση `setUserStyleSheet` το επιβάλλει με την υψηλότερη προτεραιότητα.  
- **Οι αριθμοί σελίδων εμφανίζουν “NaN”** – Επαληθεύστε ότι χρησιμοποιείτε την έκδοση Aspose.HTML 23.10 ή νεότερη· οι παλαιότερες εκδόσεις δεν διαθέτουν τη λειτουργία `currentPageNumber()`.  
- **Το αρχείο εξόδου είναι κενό** – Επιβεβαιώστε ότι η διαδρομή `Resources.output` επιλύεται σωστά και έχετε δικαιώματα εγγραφής.  

## Συχνές Ερωτήσεις

### Ε1: Τι είναι το Aspose.HTML για Java;

**Α:** Το Aspose.HTML για Java είναι μια βιβλιοθήκη Java που παρέχει ισχυρά εργαλεία για εργασία με έγγραφα HTML σε εφαρμογές Java, συμπεριλαμβανομένων της μετατροπής, της απόδοσης και της επεξεργασίας.

### Ε2: Μπορώ να προσαρμόσω περαιτέρω τα περιθώρια της σελίδας;

**Α:** Ναι, απλώς επεξεργαστείτε το CSS μέσα στο `setUserStyleSheet`. Μπορείτε να αλλάξετε οποιεσδήποτε τιμές `margin-*` ή να προσθέσετε επιπλέον κουτιά `@top-*` / `@bottom-*`.

### Ε3: Πώς μπορώ να προσθέσω περισσότερο περιεχόμενο στο HTML έγγραφο;

**Α:** Αντικαταστήστε τη συμβολοσειρά στο `new HTMLDocument("<div>Hello World!!!</div>", …)` με το δικό σας HTML markup, ή φορτώστε ένα εξωτερικό αρχείο χρησιμοποιώντας τον κατασκευαστή `HTMLDocument(String url, …)`.

### Ε4: Είναι το Aspose.HTML για Java συμβατό με άλλες μορφές εγγράφων;

**Α:** Απόλυτα. Το ίδιο `HTMLDocument` μπορεί να αποδοθεί σε PDF, XPS, εικόνες ή ακόμη και EPUB αλλάζοντας τη συσκευή εξόδου (π.χ., `PdfDevice`, `PngDevice`).

### Ε5: Χρειάζομαι άδεια για τη χρήση του Aspose.HTML για Java;

**Α:** Ναι, απαιτείται άδεια για χρήση σε παραγωγή. Μπορείτε να αποκτήσετε δοκιμαστική άδεια ή να αγοράσετε άδεια από [here](https://purchase.aspose.com/buy) ή [here](https://releases.aspose.com/).

### Ε6: Πώς ορίζω διαφορετικά περιθώρια για περιττές και ζυγές σελίδες;

**Α:** Χρησιμοποιήστε τις ψευδο‑κλάσεις `@page :left` και `@page :right` στο φύλλο στυλ σας για να ορίσετε διαφορετικά περιθώρια για τις αριστερές (ζυγές) και δεξιές (περιττές) σελίδες.

### Ε7: Μπορώ να ενσωματώσω προσαρμοσμένες γραμματοσειρές στο αποδοθέν έγγραφο;

**Α:** Ναι. Προσθέστε κανόνες `@font-face` στο φύλλο στυλ του χρήστη και αναφέρετε τις γραμματοσειρές στο HTML περιεχόμενό σας.

## Συμπέρασμα

Τώρα έχετε κατακτήσει **πώς να ορίσετε τα περιθώρια σελίδας HTML σε Java** χρησιμοποιώντας το Aspose.HTML, και γνωρίζετε πώς να προσθέσετε αριθμούς σελίδων και έναν τίτλο για να κάνετε τα έγγραφά σας επαγγελματικά. Μη διστάσετε να πειραματιστείτε με επιπλέον κουτιά `@page`, προσαρμοσμένες γραμματοσειρές ή διαφορετικές μορφές εξόδου ώστε να ταιριάζουν στις ανάγκες του έργου σας.

Αν αντιμετωπίσετε προκλήσεις, η επίσημη [τεκμηρίωση Aspose.HTML για Java](https://reference.aspose.com/html/java/) και το [φόρουμ υποστήριξης Aspose](https://forum.aspose.com/) είναι εξαιρετικά μέρη για βοήθεια.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Τελευταία ενημέρωση:** 2025-12-05  
**Δοκιμή με:** Aspose.HTML for Java 23.12  
**Συγγραφέας:** Aspose  

---