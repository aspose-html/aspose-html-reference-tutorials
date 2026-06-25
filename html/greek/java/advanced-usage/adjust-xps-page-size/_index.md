---
date: 2026-03-18
description: Μάθετε πώς να μετατρέπετε HTML σε XPS και να προσαρμόζετε το μέγεθος
  σελίδας XPS χρησιμοποιώντας το Aspose.HTML για Java. Ελέγξτε εύκολα τις διαστάσεις
  εξόδου.
linktitle: Adjusting XPS Page Size
second_title: Java HTML Processing with Aspose.HTML
title: Μετατροπή HTML σε XPS και προσαρμογή του μεγέθους σελίδας XPS με το Aspose.HTML
  για Java
url: /el/java/advanced-usage/adjust-xps-page-size/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε XPS και Προσαρμογή του Μεγέθους Σελίδας XPS με το Aspose.HTML για Java

Σε αυτό το tutorial θα ανακαλύψετε **πώς να μετατρέψετε HTML σε XPS** και να ρυθμίσετε ακριβώς το μέγεθος της σελίδας που προκύπτει χρησιμοποιώντας το Aspose.HTML για Java. Είτε δημιουργείτε εκτυπώσιμες αναφορές, τιμολόγια ή αρχειακά έγγραφα, ο έλεγχος των διαστάσεων του XPS εξασφαλίζει ότι το αποτέλεσμα φαίνεται ακριβώς όπως το περιμένετε. Θα περάσουμε από κάθε βήμα — από τη ρύθμιση του περιβάλλοντος μέχρι την απόδοση του τελικού αρχείου XPS — ώστε να ενσωματώσετε αυτή τη δυνατότητα στις εφαρμογές Java σας αμέσως.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “convert HTML to XPS”;** Μετατρέπει ένα έγγραφο HTML σε αρχείο XPS, διατηρώντας τη διάταξη και το στυλ.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγή.  
- **Ποια έκδοση της Java υποστηρίζεται;** Java 8 ή νεότερη (συνιστάται JDK 11+).  
- **Μπορώ να αλλάξω το μέγεθος της σελίδας;** Ναι – το Aspose.HTML σας επιτρέπει να ορίσετε προσαρμοσμένες διαστάσεις πριν από την απόδοση.  
- **Πόσο διαρκεί η μετατροπή;** Συνήθως κάτω από ένα δευτερόλεπτο για τυπικές σελίδες· μεγαλύτερα έγγραφα μπορεί να χρειαστούν περισσότερο χρόνο.

## Τι είναι η μετατροπή HTML σε XPS;

Η μετατροπή HTML σε XPS σημαίνει ότι παίρνετε ένα αρχείο σήμανσης προσανατολισμένο στο web και παράγετε ένα έγγραφο XPS (XML Paper Specification) — μια μορφή σταθερής διάταξης, έτοιμη για εκτύπωση, παρόμοια με το PDF. Αυτό είναι χρήσιμο όταν χρειάζεστε έγγραφα υψηλής πιστότητας, ανεξάρτητα από τη συσκευή, για αρχειοθέτηση ή εκτύπωση από εφαρμογές Java.

## Γιατί να προσαρμόσετε το μέγεθος σελίδας XPS;

Η προσαρμογή του μεγέθους σελίδας σας δίνει έλεγχο στις φυσικές διαστάσεις του τελικού εγγράφου (π.χ., A4, Letter, προσαρμοσμένες ετικέτες). Αποτρέπει ανεπιθύμητη κλιμάκωση, εξασφαλίζει ότι το περιεχόμενο ταιριάζει τέλεια και μπορεί να μειώσει το μέγεθος του αρχείου αφαιρώντας περιττό λευκό χώρο.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:

1. **Περιβάλλον Ανάπτυξης Java** – Java Development Kit (JDK) εγκατεστημένο στο σύστημά σας.  
2. **Βιβλιοθήκη Aspose.HTML for Java** – Κατεβάστε και συμπεριλάβετε τη βιβλιοθήκη Aspose.HTML for Java στο έργο σας. Μπορείτε να βρείτε τη βιβλιοθήκη [εδώ](https://releases.aspose.com/html/java/).  
3. **Αρχείο Εισόδου HTML** – Προετοιμάστε ένα αρχείο HTML που θέλετε να αποδώσετε και να προσαρμόσετε το μέγεθος σελίδας XPS. Μπορείτε να χρησιμοποιήσετε το δικό σας αρχείο HTML για αυτό το tutorial.

## Εισαγωγή Πακέτων

Πρώτα, εισάγετε τις κλάσεις που θα χρειαστείτε. Αυτά τα πακέτα σας δίνουν πρόσβαση στη διαχείριση εγγράφων, την απόδοση και τις λειτουργίες ρύθμισης σελίδας.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Οδηγός Βήμα‑βήμα

Παρακάτω υπάρχει ένας σύντομος, αριθμημένος οδηγός που αντικατοπτρίζει τα αρχικά βήματα προσθέτοντας επιπλέον πλαίσιο για σαφήνεια.

### Βήμα 1: Ορισμός Ονόματος Αρχείου Εισόδου

Διαβάστε το αρχικό αρχείο HTML χρησιμοποιώντας ένα `FileInputStream`. Αυτό το ρεύμα παρέχει το ακατέργαστο HTML στη μηχανή Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

### Βήμα 2: Δημιουργία Εγγράφου HTML και Ορισμός Στυλ

Δημιουργήστε ένα αντικείμενο `HTMLDocument` που αντιπροσωπεύει το περιεχόμενο που θα αποδώσετε. Σε αυτό το παράδειγμα εισάγουμε επίσης ένα μικρό μπλοκ CSS για να δείξουμε το στυλ — μπορείτε να το αντικαταστήσετε με το δικό σας markup.

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

### Βήμα 3: Δημιουργία Επιλογών Απόδοσης XPS

Δημιουργήστε ένα αντικείμενο `XpsRenderingOptions` για να κρατήσετε όλες τις ρυθμίσεις που επηρεάζουν τη μετατροπή από HTML σε XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

### Βήμα 4: Προσαρμογή Μεγέθους Σελίδας  

**Πώς να ορίσετε το μέγεθος σελίδας XPS** – Ορίστε ένα προσαρμοσμένο μέγεθος σελίδας (πλάτος × ύψος σε points) και ενημερώστε τον renderer αν πρέπει να επεκταθεί αυτόματα στην πιο πλατιά σελίδα. Ορίζοντας το `adjustToWidestPage` σε `false` διατηρεί τις ακριβείς διαστάσεις που καθορίζετε.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

### Βήμα 5: Απόδοση του Αποτελέσματος

Τέλος, δημιουργήστε ένα `XpsDevice` με τις ρυθμισμένες επιλογές και αποδώστε το έγγραφο HTML. Το αποτέλεσμα είναι ένα πλήρως σχηματισμένο αρχείο XPS με τις προσαρμοσμένες διαστάσεις σελίδας που ορίσατε.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Συνηθισμένα Προβλήματα και Λύσεις

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενό XPS αποτέλεσμα** | Η ροή εισόδου δεν κλείνει ή το HTMLDocument δείχνει σε λάθος αρχείο. | Βεβαιωθείτε ότι το `FileInputStream` είναι σωστά τυλιγμένο σε μπλοκ try‑with‑resources και ότι η διαδρομή του αρχείου είναι ακριβής. |
| **Το μέγεθος σελίδας δεν εφαρμόζεται** | Το `adjustToWidestPage` παραμένει `true`. | Ορίστε `pageSetup.setAdjustToWidestPage(false);` όπως φαίνεται στο Βήμα 4. |
| **Μη υποστηριζόμενο CSS** | Το Aspose.HTML υποστηρίζει ένα υποσύνολο του CSS. | Περιοριστείτε σε βασική διάταξη, γραμματοσειρές και χρώματα· αποφύγετε σύνθετους selectors ή CSS Grid. |
| **LicenseException** | Εκτέλεση χωρίς έγκυρη άδεια σε παραγωγή. | Εφαρμόστε την προσωρινή ή αγορασμένη άδεια πριν από την απόδοση (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Συχνές Ερωτήσεις

**Ε: Τι είναι το Aspose.HTML for Java;**  
Α: Το Aspose.HTML for Java είναι μια βιβλιοθήκη Java που επιτρέπει στους προγραμματιστές να χειρίζονται και να μετατρέπουν έγγραφα HTML σε διάφορες μορφές, όπως XPS, PDF και εικόνες.

**Ε: Πού μπορώ να κατεβάσω το Aspose.HTML for Java;**  
Α: Μπορείτε να κατεβάσετε τη βιβλιοθήκη Aspose.HTML for Java από [αυτόν τον σύνδεσμο](https://releases.aspose.com/html/java/).

**Ε: Υπάρχει δωρεάν δοκιμή για το Aspose.HTML for Java;**  
Α: Ναι, μπορείτε να αποκτήσετε δωρεάν δοκιμή του Aspose.HTML for Java από [εδώ](https://releases.aspose.com/).

**Ε: Πώς μπορώ να αποκτήσω προσωρινή άδεια για το Aspose.HTML for Java;**  
Α: Για να λάβετε προσωρινή άδεια για το Aspose.HTML for Java, επισκεφθείτε [αυτή τη σελίδα](https://purchase.aspose.com/temporary-license/).

**Ε: Μπορώ να λάβω υποστήριξη για το Aspose.HTML for Java;**  
Α: Ναι, μπορείτε να ζητήσετε βοήθεια και υποστήριξη από την κοινότητα Aspose στο [Aspose Forum](https://forum.aspose.com/).

**Ε: Μπορώ να μετατρέψω HTML σε XPS σε headless server;**  
Α: Απόλυτα. Το Aspose.HTML λειτουργεί σε περιβάλλοντα χωρίς GUI· απλώς βεβαιωθείτε ότι το Java runtime είναι σωστά ρυθμισμένο.

**Ε: Υποστηρίζει η βιβλιοθήκη προσαρμοσμένα περιθώρια σελίδας;**  
Α: Ναι. Χρησιμοποιήστε `PageSetup.setMarginTop()`, `setMarginBottom()`, κλπ., πριν αναθέσετε το `PageSetup` στις επιλογές απόδοσης.

## Συμπέρασμα

Διασχίσαμε τη πλήρη διαδικασία **μετατροπής HTML σε XPS** και προσαρμογής του μεγέθους σελίδας με το Aspose.HTML για Java. Ακολουθώντας αυτά τα βήματα μπορείτε να δημιουργήσετε έγγραφα XPS έτοιμα για εκτύπωση που ταιριάζουν ακριβώς στις απαιτήσεις διάταξης σας. Μη διστάσετε να πειραματιστείτε με διαφορετικές διαστάσεις σελίδας, στυλ ή ακόμη και να προσθέσετε κεφαλίδες και υποσέλιδα ώστε να εξυπηρετούν τις ανάγκες του έργου σας.

Αν έχετε ερωτήσεις ή χρειάζεστε περαιτέρω βοήθεια, εξερευνήστε την [τεκμηρίωση Aspose.HTML for Java](https://reference.aspose.com/html/java/) ή συμμετέχετε στη συζήτηση στο [Aspose Forum](https://forum.aspose.com/).

---

**Τελευταία ενημέρωση:** 2026-03-18  
**Δοκιμή με:** Aspose.HTML for Java 24.11 (τελευταία έκδοση τη στιγμή της συγγραφής)  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}