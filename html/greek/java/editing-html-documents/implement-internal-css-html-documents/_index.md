---
date: 2026-02-15
description: Μάθετε πώς να δημιουργήσετε έγγραφο HTML Java και να προσθέσετε στοιχείο
  style Java χρησιμοποιώντας το Aspose.HTML for Java σε αυτόν τον οδηγό βήμα‑βήμα.
linktitle: Implement Internal CSS in HTML Documents with Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Δημιουργία εγγράφου HTML Java με εσωτερικό CSS χρησιμοποιώντας το Aspose.HTML
url: /el/java/editing-html-documents/implement-internal-css-html-documents/
weight: 16
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία εγγράφου html java με εσωτερικό CSS χρησιμοποιώντας το Aspose.HTML

## Εισαγωγή
Αν χρειάζεστε να **δημιουργήσετε αρχεία html java** που φαίνονται επαγγελματικά αμέσως, το εσωτερικό CSS είναι ο γρηγορότερος τρόπος να μορφοποιήσετε μια σελίδα χωρίς να ασχοληθείτε με εξωτερικά φύλλα στυλ. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία — από τη δημιουργία του HTML εγγράφου σε Java, την προσθήκη ενός στοιχείου `<style>`, την αποθήκευση του αρχείου, μέχρι την απόδοση του αποτελέσματος ως PDF. Στο τέλος θα είστε άνετοι με κάθε βήμα και θα καταλάβετε γιατί το Aspose.HTML κάνει τη ροή εργασίας αδιάκοπη.

## Γρήγορες Απαντήσεις
- **Ποια βιβλιοθήκη διαχειρίζεται HTML σε Java;** Aspose.HTML for Java  
- **Μπορώ να προσθέσω ένα στοιχείο style προγραμματιστικά;** Ναι – χρησιμοποιήστε `document.createElement("style")`  
- **Πώς αποθηκεύεται το αποτέλεσμα;** Κλήστε `document.save("yourfile.html")`  
- **Υποστηρίζεται η μετατροπή σε PDF;** Απόλυτα, μέσω `PdfDevice` και `document.renderTo()`  
- **Χρειάζεται άδεια για παραγωγική χρήση;** Ναι, απαιτείται εμπορική άδεια για χρήση εκτός δοκιμής  

## Τι είναι το “create html document java”;
Η δημιουργία ενός HTML εγγράφου σε Java σημαίνει την δημιουργία ενός αντικειμένου `HTMLDocument`, την προσθήκη περιεχομένου markup και, προαιρετικά, την προσάρτηση CSS ή JavaScript. Το Aspose.HTML αφαιρεί την ανάγκη για χαμηλού επιπέδου ανάλυση, επιτρέποντάς σας να εστιάσετε στο περιεχόμενο και τη μορφοποίηση.

## Γιατί να χρησιμοποιήσετε εσωτερικό CSS με το Aspose.HTML;
- **Αυτοσυγκρατημένη μορφοποίηση:** Όλα τα στυλ ζουν μέσα στο ίδιο αρχείο, ιδανικό για πρότυπα email ή αναφορές μιας σελίδας.  
- **Χωρίς επιπλέον αιτήματα δικτύου:** Ταχύτερο φόρτωμα επειδή ο φυλλομετρητής δεν χρειάζεται να κατεβάσει εξωτερικά αρχεία CSS.  
- **Εύκολη μετατροπή σε PDF:** Όταν το HTML περιέχει τα δικά του στυλ, το παραγόμενο PDF ταιριάζει ακριβώς με την εμφάνιση στην οθόνη.  

## Προαπαιτούμενα
Πριν ξεκινήσετε, βεβαιωθείτε ότι έχετε τα εξής:

1. **Java Development Kit (JDK)** – Κατεβάστε το από την [ιστοσελίδα της Oracle](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) ή το [OpenJDK](https://openjdk.java.net/).  
2. **Aspose.HTML for Java library** – Κατεβάστε την τελευταία έκδοση από την [ιστοσελίδα της Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse ή οποιονδήποτε επεξεργαστή προτιμάτε.  
4. **Βασικές γνώσεις Java** – Πρέπει να είστε άνετοι με κλάσεις, αντικείμενα και κλήσεις μεθόδων.  

## Εισαγωγή Πακέτων
Πρώτα, προσθέστε τις απαιτούμενες εισαγωγές ώστε ο μεταγλωττιστής να γνωρίζει πού βρίσκονται οι κλάσεις του Aspose.HTML.

```java
import java.io.IOException;
```

## Οδηγός Βήμα‑Βήμα

### Βήμα 1: Δημιουργία ενός Αντικειμένου HTML Document
Ξεκινάμε δημιουργώντας το HTML έγγραφο που θα μορφοποιήσουμε αργότερα.

```java
String content = "<div><p>Internal CSS</p><p>An internal CSS is used to define a style for a single HTML page</p></div>";
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument(content, ".");
```

### Βήμα 2: Προσθήκη Στοιχείου Style (add style element java)
Τώρα δημιουργούμε μια ετικέτα `<style>` και ορίζουμε δύο κλάσεις CSS.

```java
com.aspose.html.dom.Element style = document.createElement("style");
style.setTextContent(".frame1 { margin-top:50px; margin-left:50px; padding:20px; width:360px; height:90px; background-color:#a52a2a; font-family:verdana; color:#FFF5EE;}" +
                      ".frame2 { margin-top:-90px; margin-left:160px; text-align:center; padding:20px; width:360px; height:100px; background-color:#ADD8E6;}");
```

### Βήμα 3: Προσάρτηση του Στοιχείου Style στην Επικεφαλίδα του Εγγράφου
Συνδέουμε το νεοδημιουργημένο στοιχείο style με την ενότητα `<head>`.

```java
com.aspose.html.dom.Element head = document.getElementsByTagName("head").get_Item(0);
head.appendChild(style);
```

### Βήμα 4: Ανάθεση CSS Κλάσεων σε Στοιχεία HTML
Εδώ συνδέουμε τις κλάσεις CSS με τα στοιχεία παραγράφου.

```java
com.aspose.html.HTMLElement paragraph = (com.aspose.html.HTMLElement) document.getElementsByTagName("p").get_Item(0);
paragraph.setClassName("frame1");
HTMLElement lastParagraph = (HTMLElement) document.getElementsByTagName("p").get_Item(document.getElementsByTagName("p").getLength() - 1);
lastParagraph.setClassName("frame2");
```

### Βήμα 5: Προσαρμογή Ιδιοτήτων Στυλ (render html to pdf java preparation)
Πέρα από τους κανόνες σε επίπεδο κλάσης, ρυθμίζουμε μεμονωμένα χαρακτηριστικά στυλ.

```java
paragraph.getStyle().setFontSize("250%");
paragraph.getStyle().setTextAlign("center");
lastParagraph.getStyle().setColor("#434343");
lastParagraph.getStyle().setFontSize("150%");
lastParagraph.getStyle().setFontFamily("verdana");
```

### Βήμα 6: Αποθήκευση του HTML Εγγράφου (save html file java)
Αποθηκεύουμε το μορφοποιημένο markup σε φυσικό αρχείο στο δίσκο.

```java
document.save("edit-internal-css.html");
```

### Βήμα 7: Απόδοση του HTML Εγγράφου σε PDF (generate pdf from html java, convert html to pdf aspose)
Τέλος, μετατρέπουμε το HTML αρχείο σε PDF — χρήσιμο για αναφορές ή διανομή.

```java
com.aspose.html.rendering.pdf.PdfDevice device = new com.aspose.html.rendering.pdf.PdfDevice("edit-internal-css.pdf");
document.renderTo(device);
```

## Συνηθισμένα Προβλήματα & Pro Tips
- **Απουσία ετικέτας `<head>`:** Αν ξεκινήσετε με ακατέργαστο HTML που δεν περιέχει `<head>`, το Aspose.HTML θα δημιουργήσει αυτόματα μία, αλλά είναι καλή πρακτική να την συμπεριλάβετε.  
- **Συγκρούσεις εξειδίκευσης CSS:** Το εσωτερικό CSS υπερισχύει των εξωτερικών στυλ, αλλά τα inline στυλ έχουν πάντα προτεραιότητα. Κρατήστε τους επιλογείς σας αρκετά συγκεκριμένους.  
- **Μεγάλα έγγραφα & ταχύτητα PDF:** Για πολύ μεγάλα HTML αρχεία, σκεφτείτε να απλοποιήσετε το CSS ή να χωρίσετε το έγγραφο σε ενότητες πριν από την απόδοση.  

## Συχνές Ερωτήσεις

**Ε: Ποιο είναι το πλεονέκτημα της χρήσης εσωτερικού CSS;**  
Α: Το εσωτερικό CSS σας επιτρέπει να μορφοποιήσετε ένα μόνο HTML έγγραφο χωρίς να επηρεάσετε άλλες σελίδες, καθιστώντας το ιδανικό για μοναδικά σχέδια ή πρότυπα email.

**Ε: Μπορεί το Aspose.HTML να διαχειριστεί εξωτερικά αρχεία CSS;**  
Α: Ναι, μπορείτε να συνδέσετε εξωτερικά φύλλα στυλ με τον ίδιο τρόπο όπως σε κανονικό περιβάλλον φυλλομετρητή.

**Ε: Είναι το Aspose.HTML ανοιχτού κώδικα;**  
Α: Όχι, είναι εμπορική βιβλιοθήκη, αλλά διατίθεται δωρεάν δοκιμαστική έκδοση για αξιολόγηση.

**Ε: Πώς μπορώ να επικοινωνήσω με την υποστήριξη αν αντιμετωπίσω προβλήματα;**  
Α: Επισκεφθείτε το [φόρουμ υποστήριξης της Aspose](https://forum.aspose.com/c/html/29) για βοήθεια από την κοινότητα και τους μηχανικούς της Aspose.

**Ε: Υπάρχουν ζητήματα απόδοσης κατά την απόδοση HTML σε PDF;**  
Α: Πολύπλοκες διατάξεις και βαριά CSS μπορούν να αυξήσουν το χρόνο απόδοσης. Η βελτιστοποίηση εικόνων και η απλοποίηση στυλ βοηθούν στη βελτίωση της ταχύτητας.

## Συμπέρασμα
Τώρα έχετε ένα πλήρες, ολοκληρωμένο παράδειγμα για το πώς να **δημιουργήσετε html document java**, **να προσθέσετε στοιχείο style java**, **να αποθηκεύσετε html file java** και **να αποδώσετε html σε pdf java** χρησιμοποιώντας το Aspose.HTML. Πειραματιστείτε με τους κανόνες CSS, δοκιμάστε διαφορετικές δομές HTML και εξερευνήστε τις πλούσιες επιλογές απόδοσης που προσφέρει το Aspose. Καλό προγραμματισμό!

---

**Τελευταία ενημέρωση:** 2026-02-15  
**Δοκιμάστηκε με:** Aspose.HTML for Java 23.12  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}