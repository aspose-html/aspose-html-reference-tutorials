---
date: 2026-08-28
description: Ρυθμίστε το μέγεθος σελίδας XPS κατά τη μετατροπή HTML σε XPS με Java
  χρησιμοποιώντας το Aspose.HTML. Αποδώστε HTML σε XPS με ακριβείς διαστάσεις.
keywords:
- adjust xps page size
- render html to xps
- aspose.html java
- xps conversion java
- html to xps
lastmod: 2026-08-28
linktitle: Ρύθμιση του μεγέθους σελίδας XPS
og_description: Ρυθμίστε το μέγεθος σελίδας XPS κατά τη μετατροπή HTML σε XPS με Java
  χρησιμοποιώντας το Aspose.HTML. Μάθετε πώς να αποδίδετε HTML σε XPS με ακριβείς
  διαστάσεις σε δευτερόλεπτα.
og_image_alt: Tutorial showing how to adjust XPS page size during HTML to XPS conversion
  with Aspose.HTML for Java
og_title: Ρύθμιση του μεγέθους σελίδας XPS κατά τη μετατροπή HTML σε XPS με Java
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  headline: Adjust XPS page size when converting HTML to XPS in Java
  type: TechArticle
- description: Adjust XPS page size while converting HTML to XPS in Java using Aspose.HTML.
    Render HTML to XPS with precise dimensions.
  name: Adjust XPS page size when converting HTML to XPS in Java
  steps:
  - name: set the input file name
    text: The `FileInputStream` class reads raw bytes from a file, providing the HTML
      source to the renderer.
  - name: create an HTML document and set styles
    text: The `HTMLDocument` class represents an in‑memory HTML DOM used by Aspose.HTML
      for rendering.
  - name: create XPS rendering options
    text: The `XpsRenderingOptions` class holds settings that control how HTML is
      rendered to XPS, such as page size and image quality.
  - name: adjust the page size
    text: '**How to set XPS page size** – Define a custom page size (width × height
      in points) and tell the renderer whether it should automatically expand to the
      widest page. Setting `adjustToWidestPage` to `false` preserves the exact dimensions
      you specify. The `PageSetup` class defines page size, margins, a'
  - name: render the output
    text: The `XpsDevice` class is the rendering target that writes the processed
      content to an XPS file.
  type: HowTo
- questions:
  - answer: Aspose.HTML for Java is a Java library that allows developers to manipulate
      and convert HTML documents into various formats, such as XPS, PDF, and images.
      You can download the library from [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).
    question: What is Aspose.HTML for Java?
  - answer: You can download the Aspose.HTML for Java library from [Aspose product
      releases page](https://releases.aspose.com/).
    question: Where can I download Aspose.HTML for Java?
  - answer: Yes, you can get a free trial of Aspose.HTML for Java from the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: Is there a free trial available for Aspose.HTML for Java?
  - answer: To get a temporary license for Aspose.HTML for Java, visit the [temporary
      license request page](https://purchase.aspose.com/temporary-license/).
    question: How can I obtain a temporary license for Aspose.HTML for Java?
  - answer: Yes, you can seek help and support from the Aspose community on the [Aspose
      Forum](https://forum.aspose.com/).
    question: Can I get support for Aspose.HTML for Java?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
tags:
- adjust xps page size
- Aspose.HTML
- Java XPS conversion
- HTML to XPS
- document rendering
title: Ρύθμιση του μεγέθους σελίδας XPS κατά τη μετατροπή HTML σε XPS με Java
url: /el/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσαρμογή μεγέθους σελίδας XPS κατά τη μετατροπή HTML σε XPS σε Java

Σε αυτό το σεμινάριο θα μάθετε **πώς να προσαρμόζετε το μέγεθος σελίδας XPS** κατά τη μετατροπή HTML σε XPS με το Aspose.HTML for Java. Είτε χρειάζεστε εκτυπώσιμα τιμολόγια, αρχειακές αναφορές ή ετικέτες προσαρμοσμένου μεγέθους, ο έλεγχος των διαστάσεων της σελίδας εξασφαλίζει ότι το τελικό XPS θα εμφανίζεται ακριβώς όπως προορίζεται. Θα περάσουμε από τη ρύθμιση του περιβάλλοντος, τις επιλογές απόδοσης και τη δημιουργία του τελικού XPS, ώστε να μπορείτε να ενσωματώσετε αυτή τη δυνατότητα απευθείας στις εφαρμογές Java.

## Γρήγορες απαντήσεις
- **Τι σημαίνει η “μετατροπή HTML σε XPS”;** Δημιουργεί ένα αρχείο XPS από ένα έγγραφο HTML, διατηρώντας τη διάταξη και το στυλ.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγή.  
- **Ποια έκδοση της Java υποστηρίζεται;** Java 8 ή νεότερη (συνιστάται JDK 11+).  
- **Μπορώ να αλλάξω το μέγεθος της σελίδας;** Ναι – το Aspose.HTML σας επιτρέπει να ορίσετε προσαρμοσμένες διαστάσεις πριν από την απόδοση.  
- **Πόσο διαρκεί η μετατροπή;** Συνήθως κάτω από ένα δευτερόλεπτο για τυπικές σελίδες· μεγαλύτερα έγγραφα μπορεί να χρειαστούν περισσότερο χρόνο.

## Τι είναι η μετατροπή HTML σε XPS;
Η μετατροπή HTML σε XPS σημαίνει τη λήψη ενός αρχείου σήμανσης προσανατολισμένου στο web και η δημιουργία ενός εγγράφου XPS (XML Paper Specification) — μιας μορφής σταθερής διάταξης, έτοιμης για εκτύπωση, παρόμοια με το PDF. Αυτό είναι χρήσιμο όταν χρειάζεστε έγγραφα υψηλής πιστότητας, ανεξάρτητα από τη συσκευή, για αρχειοθέτηση ή εκτύπωση από εφαρμογές Java.

## Γιατί να προσαρμόσετε το μέγεθος σελίδας XPS;
Η προσαρμογή του μεγέθους σελίδας XPS σας δίνει έλεγχο στις φυσικές διαστάσεις του τελικού εγγράφου (π.χ., A4, Letter, προσαρμοσμένες ετικέτες). Αποτρέπει ανεπιθύμητη κλιμάκωση, εξασφαλίζει ότι το περιεχόμενο ταιριάζει τέλεια και μπορεί να μειώσει το μέγεθος του αρχείου αφαιρώντας περιττό λευκό χώρο.

## Πώς να αποδώσετε HTML σε XPS με προσαρμοσμένο μέγεθος σελίδας;
Φορτώστε το HTML σας, διαμορφώστε το `XpsRenderingOptions` με ένα `PageSetup` που ορίζει το ακριβές πλάτος και ύψος που χρειάζεστε, και στη συνέχεια αποδώστε σε ένα `XpsDevice`. Αυτή η ροή δύο βημάτων σας επιτρέπει να διατηρήσετε τη διάταξη αμετάβλητη ενώ επιβάλλετε τις διαστάσεις που καθορίζετε, όλα με μία κλήση API.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:

1. **Περιβάλλον Ανάπτυξης Java** – Java Development Kit (JDK) εγκατεστημένο στο σύστημά σας.  
2. **Βιβλιοθήκη Aspose.HTML for Java** – Κατεβάστε και συμπεριλάβετε τη βιβλιοθήκη Aspose.HTML for Java στο έργο σας. Μπορείτε να βρείτε τη βιβλιοθήκη στη [Σελίδα λήψης Aspose.HTML for Java](https://releases.aspose.com/html/java/).  
3. **Αρχείο Εισόδου HTML** – Προετοιμάστε ένα αρχείο HTML που θέλετε να αποδώσετε και να προσαρμόσετε το μέγεθος σελίδας XPS. Μπορείτε να χρησιμοποιήσετε το δικό σας αρχείο HTML για αυτό το σεμινάριο.

## Εισαγωγή πακέτων

Η κλάση `Page` αντιπροσωπεύει τις διαστάσεις και τις ρυθμίσεις της σελίδας για την έξοδο XPS. Η κλάση `HtmlRenderer` εκτελεί τη μετατροπή από HTML σε XPS.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Οδηγός βήμα‑βήμα

Παρακάτω υπάρχει ένας συνοπτικός, αριθμημένος οδηγός που αντικατοπτρίζει τα αρχικά βήματα προσθέτοντας επιπλέον περιεχόμενο για σαφήνεια.

### Βήμα 1: ορίστε το όνομα του αρχείου εισόδου

Η κλάση `FileInputStream` διαβάζει ακατέργαστα byte από ένα αρχείο, παρέχοντας την πηγή HTML στον αποδοχέα.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Βήμα 2: δημιουργήστε ένα έγγραφο HTML και ορίστε στυλ

Η κλάση `HTMLDocument` αντιπροσωπεύει ένα DOM HTML στη μνήμη που χρησιμοποιείται από το Aspose.HTML για απόδοση.

```java
com.aspose.html.HTMLDocument html_document = new com.aspose.html.HTMLDocument("YourOutputFile.html");

String style = "<style>\n" +
               ".st\n" +
               "{\n" +
               "color: green;\n" +
               "}\n" +
               "</style>\n" +
               "<div id=id1>Aspose.HTML rendering Text in Black Color</div>\n" +
               "<div id=id2 class=''st''>Aspose.HTML rendering Text in Green Color</div>\n" +
               "<div id=id3 class=''st'' style='color: blue;'>Aspose.HTML rendering Text in Blue Color</div>\n" +
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n" +
               "\n";

// ...
```

### Βήμα 3: δημιουργήστε επιλογές απόδοσης XPS

Η κλάση `XpsRenderingOptions` περιέχει ρυθμίσεις που ελέγχουν πώς το HTML αποδίδεται σε XPS, όπως το μέγεθος σελίδας και η ποιότητα εικόνας.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Βήμα 4: προσαρμόστε το μέγεθος σελίδας  

**Πώς να ορίσετε το μέγεθος σελίδας XPS** – Ορίστε ένα προσαρμοσμένο μέγεθος σελίδας (πλάτος × ύψος σε points) και ενημερώστε τον αποδοχέα αν πρέπει να επεκταθεί αυτόματα στην πιο πλατιά σελίδα. Ορίζοντας το `adjustToWidestPage` σε `false` διατηρεί τις ακριβείς διαστάσεις που καθορίζετε.

Η κλάση `PageSetup` ορίζει το μέγεθος σελίδας, τα περιθώρια και τον προσανατολισμό για την έξοδο XPS.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Βήμα 5: αποδώστε το αποτέλεσμα

Η κλάση `XpsDevice` είναι ο προορισμός απόδοσης που γράφει το επεξεργασμένο περιεχόμενο σε ένα αρχείο XPS.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Συχνά προβλήματα και λύσεις

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενό XPS αποτέλεσμα** | Η ροή εισόδου δεν κλείνει ή το HTMLDocument δείχνει σε λάθος αρχείο. | Βεβαιωθείτε ότι το `FileInputStream` είναι σωστά τυλιγμένο σε μπλοκ try‑with‑resources και ότι η διαδρομή του αρχείου είναι ακριβής. |
| **Το μέγεθος σελίδας δεν εφαρμόστηκε** | `adjustToWidestPage` παραμένει `true`. | Ορίστε `pageSetup.setAdjustToWidestPage(false);` όπως φαίνεται στο Βήμα 4. |
| **Μη υποστηριζόμενο CSS** | Το Aspose.HTML υποστηρίζει ένα υποσύνολο του CSS. | Παραμείνετε σε βασική διάταξη, γραμματοσειρές και χρώματα· αποφύγετε σύνθετους επιλεκτές ή CSS Grid. |
| **LicenseException** | Εκτέλεση χωρίς έγκυρη άδεια σε παραγωγή. | Εφαρμόστε την προσωρινή ή αγορασμένη άδειά σας πριν από την απόδοση (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Συχνές ερωτήσεις

**Ε: Τι είναι το Aspose.HTML for Java;**  
Α: Το Aspose.HTML for Java είναι μια βιβλιοθήκη Java που επιτρέπει στους προγραμματιστές να χειρίζονται και να μετατρέπουν έγγραφα HTML σε διάφορες μορφές, όπως XPS, PDF και εικόνες. Μπορείτε να κατεβάσετε τη βιβλιοθήκη από τη [Σελίδα λήψης Aspose.HTML for Java](https://releases.aspose.com/html/java/).

**Ε: Από πού μπορώ να κατεβάσω το Aspose.HTML for Java;**  
Α: Μπορείτε να κατεβάσετε τη βιβλιοθήκη Aspose.HTML for Java από τη [Σελίδα κυκλοφορίας προϊόντων Aspose](https://releases.aspose.com/).

**Ε: Υπάρχει δωρεάν δοκιμή για το Aspose.HTML for Java;**  
Α: Ναι, μπορείτε να λάβετε δωρεάν δοκιμή του Aspose.HTML for Java από τη [σελίδα αίτησης προσωρινής άδειας](https://purchase.aspose.com/temporary-license/).

**Ε: Πώς μπορώ να αποκτήσω προσωρινή άδεια για το Aspose.HTML for Java;**  
Α: Για να αποκτήσετε προσωρινή άδεια για το Aspose.HTML for Java, επισκεφθείτε τη [σελίδα αίτησης προσωρινής άδειας](https://purchase.aspose.com/temporary-license/).

**Ε: Μπορώ να λάβω υποστήριξη για το Aspose.HTML for Java;**  
Α: Ναι, μπορείτε να ζητήσετε βοήθεια και υποστήριξη από την κοινότητα Aspose στο [Φόρουμ Aspose](https://forum.aspose.com/).

**Ε: Μπορώ να μετατρέψω HTML σε XPS σε διακομιστή χωρίς γραφικό περιβάλλον;**  
Α: Απόλυτα. Το Aspose.HTML λειτουργεί σε περιβάλλοντα χωρίς GUI· απλώς βεβαιωθείτε ότι το Java runtime είναι σωστά διαμορφωμένο.

**Ε: Η βιβλιοθήκη υποστηρίζει προσαρμοσμένα περιθώρια σελίδας;**  
Α: Ναι. Χρησιμοποιήστε `PageSetup.setMarginTop()`, `setMarginBottom()`, κλπ., πριν αναθέσετε το `PageSetup` στις επιλογές απόδοσης.

## Συμπέρασμα

Διασχίσαμε τη πλήρη διαδικασία **μετατροπής HTML σε XPS** και **προσαρμογής του μεγέθους σελίδας XPS** με το Aspose.HTML for Java. Ακολουθώντας αυτά τα βήματα, μπορείτε να δημιουργήσετε έγγραφα XPS έτοιμα για εκτύπωση που ταιριάζουν ακριβώς στις απαιτήσεις διάταξης σας. Μη διστάσετε να πειραματιστείτε με διαφορετικές διαστάσεις σελίδας, στυλ ή ακόμη και να προσθέσετε κεφαλίδες και υποσέλιδα ώστε να ταιριάζουν στις ανάγκες του έργου σας.

Αν έχετε ερωτήσεις ή χρειάζεστε περαιτέρω βοήθεια, εξερευνήστε την [τεκμηρίωση Aspose.HTML for Java](https://reference.aspose.com/html/java/) ή συμμετέχετε στη συζήτηση στο [Φόρουμ Aspose](https://forum.aspose.com/).

**Τελευταία ενημέρωση:** 2026-08-28  
**Δοκιμή με:** Aspose.HTML for Java 24.11 (τελευταία έκδοση τη στιγμή της συγγραφής)  
**Συγγραφέας:** Aspose

## Σχετικά Σεμινάρια

- [Μετατροπή HTML σε XPS με Aspose.HTML for Java](/html/java/conversion-html-to-other-formats/convert-html-to-xps/)
- [Προσαρμογή μεγέθους σελίδας PDF με Aspose.HTML for Java](/html/java/advanced-usage/adjust-pdf-page-size/)
- [Μετατροπή EPUB σε XPS με Aspose.HTML for Java](/html/java/converting-epub-to-xps/convert-epub-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}