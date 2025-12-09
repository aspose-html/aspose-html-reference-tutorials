---
date: 2025-11-29
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

# Μετατροπή HTML σε XPS και Προσαρμογή Μεγέθους Σελίδας XPS με το Aspose.HTML για Java

Σε αυτό το tutorial θα ανακαλύψετε **πώς να μετατρέψετε HTML σε XPS** και να ρυθμίσετε με ακρίβεια το μέγεθος της σελίδας που προκύπτει χρησιμοποιώντας το Aspose.HTML για Java. Είτε δημιουργείτε εκτυπώσιμες αναφορές, τιμολόγια ή αρχειακά έγγραφα, ο έλεγχος των διαστάσεων του XPS εξασφαλίζει ότι το αποτέλεσμα φαίνεται ακριβώς όπως το περιμένετε. Θα περάσουμε από κάθε βήμα — από τη ρύθμιση του περιβάλλοντος μέχρι την απόδοση του τελικού αρχείου XPS — ώστε να μπορείτε να ενσωματώσετε αυτή τη δυνατότητα στις Java εφαρμογές σας αμέσως.

## Γρήγορες Απαντήσεις
- **Τι σημαίνει “μετατροπή HTML σε XPS”;** Αποδίδει ένα έγγραφο HTML σε αρχείο XPS, διατηρώντας τη διάταξη και το στυλ.  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για ανάπτυξη· απαιτείται εμπορική άδεια για παραγωγή.  
- **Ποια έκδοση Java υποστηρίζεται;** Java 8 ή νεότερη (συνιστάται JDK 11+).  
- **Μπορώ να αλλάξω το μέγεθος της σελίδας;** Ναι – το Aspose.HTML σας επιτρέπει να ορίσετε προσαρμοσμένες διαστάσεις πριν από την απόδοση.  
- **Πόσο διαρκεί η μετατροπή;** Συνήθως κάτω από ένα δευτερόλεπτο για τυπικές σελίδες· μεγαλύτερα έγγραφα μπορεί να χρειαστούν περισσότερο χρόνο.

## Τι είναι η μετατροπή HTML σε XPS;
Η μετατροπή HTML σε XPS σημαίνει ότι παίρνετε ένα αρχείο σήμανσης προσανατολισμένο στο web και παράγετε ένα έγγραφο XPS (XML Paper Specification) — μια μορφή σταθερής διάταξης, έτοιμη για εκτύπωση, παρόμοια με το PDF. Αυτό είναι χρήσιμο όταν χρειάζεστε έγγραφα υψηλής πιστότητας, ανεξάρτητα από τη συσκευή, για αρχειοθέτηση ή εκτύπωση από Java εφαρμογές.

## Γιατί να προσαρμόσετε το μέγεθος της σελίδας XPS;
Η προσαρμογή του μεγέθους της σελίδας σας δίνει έλεγχο πάνω στις φυσικές διαστάσεις του τελικού εγγράφου (π.χ. A4, Letter, προσαρμοσμένες ετικέτες). Αποτρέπει ανεπιθύμητη κλιμάκωση, εξασφαλίζει ότι το περιεχόμενο ταιριάζει τέλεια και μπορεί να μειώσει το μέγεθος του αρχείου αφαιρώντας περιττό λευκό χώρο.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω προαπαιτούμενα:

1. **Περιβάλλον Ανάπτυξης Java** – Εγκατεστημένο Java Development Kit (JDK) στο σύστημά σας.  
2. **Βιβλιοθήκη Aspose.HTML για Java** – Κατεβάστε και συμπεριλάβετε τη βιβλιοθήκη Aspose.HTML για Java στο έργο σας. Μπορείτε να βρείτε τη βιβλιοθήκη [εδώ](https://releases.aspose.com/html/java/).  
3. **Αρχείο HTML Εισόδου** – Προετοιμάστε ένα αρχείο HTML που θέλετε να αποδώσετε και να προσαρμόσετε το μέγεθος της σελίδας XPS. Μπορείτε να χρησιμοποιήσετε το δικό σας αρχείο HTML για αυτό το tutorial.

## Εισαγωγή Πακέτων

Πρώτα, εισάγετε τις κλάσεις που θα χρειαστείτε. Αυτά τα πακέτα σας δίνουν πρόσβαση στη διαχείριση εγγράφων, απόδοση και ρυθμίσεις σελίδας.

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Βήμα 1: Ορισμός Ονόματος Αρχείου Εισόδου

Διαβάστε το αρχικό αρχείο HTML χρησιμοποιώντας ένα `FileInputStream`. Αυτό το ρεύμα τροφοδοτεί το ακατέργαστο HTML στη μηχανή Aspose.HTML.

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

## Βήμα 2: Δημιουργία HTML Document και Ορισμός Στυλ

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

## Βήμα 3: Δημιουργία XPS Rendering Options

Δημιουργήστε ένα αντικείμενο `XpsRenderingOptions` για να κρατήσετε όλες τις ρυθμίσεις που επηρεάζουν τη μετατροπή από HTML σε XPS.

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

## Βήμα 4: Προσαρμογή Μεγέθους Σελίδας

Ορίστε ένα προσαρμοσμένο μέγεθος σελίδας (πλάτος × ύψος σε points) και πείτε στον renderer αν πρέπει να επεκταθεί αυτόματα στην πιο πλατιά σελίδα. Ορίζοντας το `adjustToWidestPage` σε `false` διατηρεί τις ακριβείς διαστάσεις που καθορίζετε.

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

## Βήμα 5: Απόδοση του Αποτελέσματος

Τέλος, δημιουργήστε ένα `XpsDevice` με τις ρυθμισμένες επιλογές και αποδώστε το έγγραφο HTML. Το αποτέλεσμα είναι ένα πλήρως σχηματισμένο αρχείο XPS με τις προσαρμοσμένες διαστάσεις σελίδας που ορίσατε.

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

## Συνηθισμένα Προβλήματα και Λύσεις

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|----------------|----------|
| **Κενό XPS αποτέλεσμα** | Το ρεύμα εισόδου δεν κλείνει ή το `HTMLDocument` δείχνει σε λάθος αρχείο. | Βεβαιωθείτε ότι το `FileInputStream` είναι σωστά τυλιγμένο σε `try‑with‑resources` και ότι η διαδρομή του αρχείου είναι ακριβής. |
| **Το μέγεθος σελίδας δεν εφαρμόζεται** | Το `adjustToWidestPage` παραμένει σε `true`. | Ορίστε `pageSetup.setAdjustToWidestPage(false);` όπως φαίνεται στο Βήμα 4. |
| **Μη υποστηριζόμενο CSS** | Το Aspose.HTML υποστηρίζει μόνο ένα υποσύνολο του CSS. | Περιοριστείτε σε βασικές διατάξεις, γραμματοσειρές και χρώματα· αποφύγετε προχωρημένους επιλεκτές ή CSS Grid. |
| **LicenseException** | Εκτέλεση χωρίς έγκυρη άδεια σε παραγωγή. | Εφαρμόστε την προσωρινή ή αγορασμένη άδεια πριν από την απόδοση (`License license = new License(); license.setLicense("Aspose.Total.Java.lic");`). |

## Συχνές Ερωτήσεις

**Ε: Τι είναι το Aspose.HTML για Java;**  
Α: Το Aspose.HTML για Java είναι μια βιβλιοθήκη Java που επιτρέπει στους προγραμματιστές να χειρίζονται και να μετατρέπουν έγγραφα HTML σε διάφορες μορφές, όπως XPS, PDF και εικόνες.

**Ε: Πού μπορώ να κατεβάσω το Aspose.HTML για Java;**  
Α: Μπορείτε να κατεβάσετε τη βιβλιοθήκη Aspose.HTML για Java από [αυτόν τον σύνδεσμο](https://releases.aspose.com/html/java/).

**Ε: Υπάρχει δωρεάν δοκιμή για το Aspose.HTML για Java;**  
Α: Ναι, μπορείτε να αποκτήσετε δωρεάν δοκιμή του Aspose.HTML για Java από [εδώ](https://releases.aspose.com/).

**Ε: Πώς μπορώ να αποκτήσω προσωρινή άδεια για το Aspose.HTML για Java;**  
Α: Για να λάβετε προσωρινή άδεια για το Aspose.HTML για Java, επισκεφθείτε [αυτή τη σελίδα](https://purchase.aspose.com/temporary-license/).

**Ε: Μπορώ να λάβω υποστήριξη για το Aspose.HTML για Java;**  
Α: Ναι, μπορείτε να ζητήσετε βοήθεια και υποστήριξη από την κοινότητα Aspose στο [Φόρουμ Aspose](https://forum.aspose.com/).

**Ε: Μπορώ να μετατρέψω HTML σε XPS σε έναν headless server;**  
Α: Απολύτως. Το Aspose.HTML λειτουργεί σε περιβάλλοντα χωρίς GUI· απλώς βεβαιωθείτε ότι το Java runtime είναι σωστά διαμορφωμένο.

**Ε: Υποστηρίζει η βιβλιοθήκη προσαρμοσμένα περιθώρια σελίδας;**  
Α: Ναι. Χρησιμοποιήστε `PageSetup.setMarginTop()`, `setMarginBottom()`, κ.λπ., πριν αναθέσετε το `PageSetup` στις επιλογές απόδοσης.

## Συμπέρασμα

Διασχίσαμε τη διαδικασία **μετατροπής HTML σε XPS** και προσαρμογής του μεγέθους της σελίδας με το Aspose.HTML για Java. Ακολουθώντας αυτά τα βήματα μπορείτε να δημιουργήσετε έγγραφα XPS έτοιμα για εκτύπωση που ταιριάζουν ακριβώς στις απαιτήσεις διάταξης σας. Μη διστάσετε να πειραματιστείτε με διαφορετικές διαστάσεις σελίδας, στυλ ή ακόμη και να προσθέσετε κεφαλίδες και υποσέλιδα ώστε να ταιριάζουν στο έργο σας.

Αν έχετε ερωτήσεις ή χρειάζεστε περαιτέρω βοήθεια, εξερευνήστε την [τεκμηρίωση Aspose.HTML για Java](https://reference.aspose.com/html/java/) ή συμμετάσχετε στη συζήτηση στο [Φόρουμ Aspose](https://forum.aspose.com/).

---

**Τελευταία ενημέρωση:** 2025-11-29  
**Δοκιμασμένο με:** Aspose.HTML για Java 24.11 (τελευταία έκδοση τη στιγμή της συγγραφής)  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}