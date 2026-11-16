---
date: 2026-03-29
description: Μάθετε πώς να χρησιμοποιείτε το Aspose.HTML για Java για να καθορίσετε
  τις επιλογές αποθήκευσης XPS, να μετατρέψετε EPUB σε XPS και να διαχειριστείτε την
  άδεια χρήσης.
linktitle: Specifying XPS Save Options for EPUB to XPS
second_title: Java HTML Processing with Aspose.HTML
title: Πώς να χρησιμοποιήσετε τις επιλογές αποθήκευσης Aspose HTML για EPUB σε XPS
url: /el/java/converting-epub-to-xps/convert-epub-to-xps-specify-xps-save-options/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να χρησιμοποιήσετε τις επιλογές αποθήκευσης Aspose HTML για EPUB σε XPS

Σε αυτόν τον οδηγό θα δείξουμε **πώς να χρησιμοποιήσετε Aspose** HTML Save Options για να μετατρέψετε ένα έγγραφο EPUB σε XPS με πλήρη έλεγχο των διαστάσεων της σελίδας, του χρώματος φόντου και των ζητημάτων αδειοδότησης. Είτε δημιουργείτε μια αλυσίδα επεξεργασίας παρτίδων είτε ένα εργαλείο μετατροπής μίας χρήσης, αυτά τα βήματα θα σας βοηθήσουν να έχετε αξιόπιστα αποτελέσματα γρήγορα.

## Γρήγορες Απαντήσεις
- **Τι κάνει το Aspose HTML Save Options;** Σας επιτρέπει να προσαρμόσετε το μέγεθος της σελίδας, το χρώμα φόντου και άλλες ρυθμίσεις απόδοσης κατά την αποθήκευση σε μορφές όπως το XPS.  
- **Ποια βιβλιοθήκη απαιτείται;** Aspose.HTML for Java (τελευταία έκδοση).  
- **Χρειάζομαι άδεια;** Μια δωρεάν δοκιμή λειτουργεί για αξιολόγηση· απαιτείται εμπορική άδεια για παραγωγή.  
- **Μπορώ να αλλάξω τις διαστάσεις της σελίδας;** Ναι – μπορείτε να ορίσετε οποιοδήποτε πλάτος και ύψος μέσω του `PageSetup`.  
- **Είναι η μετατροπή γρήγορη;** Για τυπικά αρχεία EPUB η μετατροπή ολοκληρώνεται σε δευτερόλεπτα σε μια σύγχρονη JVM.

## Τι σημαίνει “how to use aspose” σε αυτό το πλαίσιο;
Η φράση **how to use Aspose** αναφέρεται στα πρακτικά βήματα για την αξιοποίηση της βιβλιοθήκης Aspose.HTML ώστε να χειρίζεστε και να μετατρέπετε έγγραφα βασισμένα στο web. Σε αυτό το σεμινάριο εστιάζουμε στις **aspose html save options** που σας επιτρέπουν να ρυθμίσετε λεπτομερώς την έξοδο όταν **μετατρέπετε EPUB σε XPS**.

## Γιατί να χρησιμοποιήσετε το Aspose.HTML για Java για τη μετατροπή EPUB σε XPS;
- **High fidelity** – διατηρεί σύνθετες διατάξεις, γραμματοσειρές και διανυσματικά γραφικά.  
- **Programmatic control** – αυτοματοποιήστε τις παρτίδες μετατροπής μέσα σε εφαρμογές Java.  
- **No external dependencies** – καθαρή βιβλιοθήκη Java, χωρίς εγγενή στοιχεία.  
- **Customizable output** – χάρη στις επιλογές αποθήκευσης μπορείτε να προσαρμόσετε το XPS στις ακριβείς ανάγκες σας, όπως **specify page dimensions** ή να ορίσετε προσαρμοσμένο φόντο.  

## Προαπαιτούμενα

Πριν βυθιστούμε στον κώδικα, βεβαιωθείτε ότι έχετε τα εξής:

1. **Java Development Environment** – εγκατεστημένο JDK 8 ή νεότερο.  
2. **Aspose.HTML for Java Library** – κατεβάστε το από το [download link](https://releases.aspose.com/html/java/).  
3. **EPUB File** – το πηγαίο EPUB που θέλετε να **convert EPUB to XPS**.  

Έχοντας αυτά έτοιμα, θα μπορείτε να ακολουθήσετε τα βήματα χωρίς διακοπές.

## Εισαγωγή Πακέτων

Αρχικά, εισάγετε τις απαιτούμενες κλάσεις. Τοποθετήστε τις εισαγωγές στην αρχή του αρχείου πηγαίου κώδικα Java σας:

```java
import java.io.FileInputStream;
import com.aspose.html.saving.XpsSaveOptions;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.drawing.Page;
import com.aspose.html.drawing.Size;
import com.aspose.html.drawing.Length;
import com.aspose.html.drawing.Color;
import com.aspose.html.converters.Converter;
import com.aspose.html.system.io.resources.Resources;
```

Αυτές οι εισαγωγές σας δίνουν πρόσβαση στη μηχανή μετατροπής και στις **Aspose HTML Save Options** που απαιτούνται για λεπτομερή ρύθμιση.

## Άνοιγμα του αρχείου EPUB

Στη συνέχεια, ανοίξτε το EPUB που θέλετε να μετατρέψετε. Η βοηθητική μέθοδος `Resources.input` φορτώνει ένα αρχείο από το φάκελο demo resources:

```java
try (FileInputStream fileInputStream = new FileInputStream(Resources.input("input.epub"))) {
    // Your code for the EPUB file handling goes here.
}
```

Η χρήση ενός μπλοκ try‑with‑resources εξασφαλίζει ότι η ροή κλείνει αυτόματα.

## Δημιουργία XPS Save Options (Διαμόρφωση Μεγέθους Σελίδας & Φόντου)

Τώρα δημιουργούμε μια παρουσίαση `XpsSaveOptions` και την προσαρμόζουμε. Εδώ είναι που οι **save options** πραγματικά ξεχωρίζουν:

```java
XpsSaveOptions options = new XpsSaveOptions();
PageSetup pageSetup = new PageSetup();
Page anyPage = new Page();
anyPage.setSize(new Size(Length.fromPixels(3000), Length.fromPixels(1000)));
pageSetup.setAnyPage(anyPage);
options.setPageSetup(pageSetup);
options.setBackgroundColor(Color.getAliceBlue());
```

- **Page size** – ορίζεται σε 3000 × 1000 pixel σε αυτό το παράδειγμα· προσαρμόστε το ώστε να ταιριάζει με το επιθυμητό μέγεθος χαρτιού ή χρησιμοποιήστε το `Length.fromInches` για **specify page dimensions** σε ίντσες.  
- **Background color** – το `AliceBlue` δείχνει πώς να αλλάξετε το φόντο του καμβά· μπορείτε να επιλέξετε οποιοδήποτε `Color`.  

Αυτές οι ρυθμίσεις αποτελούν μέρος των **aspose html save options** που επηρεάζουν το τελικό έγγραφο XPS.

## Μετατροπή EPUB σε XPS

Τέλος, καλέστε τον μετατροπέα με τη ροή, τις ρυθμισμένες επιλογές και μια διαδρομή εξόδου:

```java
Converter.convertEPUB(
    fileInputStream,
    options,
    Resources.output("output.xps")
);
```

Όταν εκτελεστεί αυτή η γραμμή, το Aspose.HTML διαβάζει το EPUB, εφαρμόζει τη ρύθμιση σελίδας και το χρώμα φόντου που ορίσατε, και γράφει ένα πλήρως συμβατό αρχείο XPS.

## Κοινά Προβλήματα & Συμβουλές
- **Incorrect page dimensions** – βεβαιωθείτε ότι οι διαστάσεις εκφράζονται σε pixel (ή χρησιμοποιήστε το `Length.fromInches`).  
- **Missing fonts** – ενσωματώστε τις απαιτούμενες γραμματοσειρές στο EPUB ή εγκαταστήστε τις στον κεντρικό υπολογιστή JVM για να αποφύγετε την εναλλακτική.  
- **Large files** – για πολύ μεγάλα EPUB, αυξήστε τη μνήμη heap της JVM (`-Xmx`) για να αποτρέψετε το `OutOfMemoryError`.  
- **Aspose HTML licensing** – βεβαιωθείτε ότι έχετε φορτώσει μια έγκυρη άδεια πριν από τη μετατροπή· διαφορετικά θα εμφανιστεί το υδατογράφημα δοκιμής.

## Συμπέρασμα

Με την αξιοποίηση των **Aspose HTML Save Options**, αποκτάτε ακριβή έλεγχο του τρόπου με τον οποίο ένα EPUB αποδίδεται σε XPS. Τα παραπάνω βήματα σας δείχνουν πώς να **how to convert EPUB**, ορίσετε **page dimensions**, αλλάξετε το φόντο και εκτελέσετε τη μετατροπή με λίγες μόνο γραμμές κώδικα Java. Ενσωματώστε αυτό το μοτίβο στις αλυσίδες επεξεργασίας παρτίδων σας για να αυτοματοποιήσετε τις εργασίες δημοσίευσης αποδοτικά.

## Συχνές Ερωτήσεις

**Q: Τι είναι το Aspose.HTML for Java;**  
A: Αυτή είναι μια βιβλιοθήκη Java που επιτρέπει στους προγραμματιστές να δημιουργούν, επεξεργάζονται, αποδίδουν και μετατρέπουν HTML, EPUB και άλλα έγγραφα βασισμένα στο web χωρίς την ανάγκη ενός προγράμματος περιήγησης.

**Q: Μπορώ να το χρησιμοποιήσω σε εμπορικό έργο;**  
A: Ναι. Για παραγωγική χρήση χρειάζεστε έγκυρη άδεια. Μπορείτε να αγοράσετε μία στη [purchase page](https://purchase.aspose.com/buy).

**Q: Υπάρχει διαθέσιμη δωρεάν δοκιμή;**  
A: Απόλυτα. Κατεβάστε μια δοκιμαστική έκδοση από [here](https://releases.aspose.com/).

**Q: Πού μπορώ να λάβω υποστήριξη;**  
A: Η υποστήριξη της κοινότητας και η επίσημη βοήθεια είναι διαθέσιμες μέσω των φόρουμ Aspose στο [https://forum.aspose.com/](https://forum.aspose.com/).

**Q: Ποιες είναι οι απαιτήσεις συστήματος;**  
A: Ένα Java Development Kit (JDK) 8+ και ένα λειτουργικό σύστημα που υποστηρίζεται από το runtime του Aspose. Βεβαιωθείτε ότι το περιβάλλον σας πληροί τα προαπαιτούμενα που αναφέρθηκαν παραπάνω.

---

**Τελευταία ενημέρωση:** 2026-03-29  
**Δοκιμάστηκε με:** Aspose.HTML for Java 24.12  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}