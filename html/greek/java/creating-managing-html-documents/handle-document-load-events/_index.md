---
date: 2026-04-23
description: Μάθετε πώς να λαμβάνετε το εξωτερικό HTML και να περιμένετε τη φόρτωση
  του εγγράφου χρησιμοποιώντας το Aspose.HTML για Java σε αυτόν τον οδηγό βήμα‑βήμα.
keywords:
- get outer html
- wait for document load
- java html processing
- navigate html document
- aspose html example
linktitle: Διαχείριση συμβάντων φόρτωσης εγγράφου στο Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Λήψη εξωτερικού HTML & Διαχείριση συμβάντων φόρτωσης στο Aspose.HTML για Java
url: /el/java/creating-managing-html-documents/handle-document-load-events/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόκτηση εξωτερικού HTML & Διαχείριση συμβάντων φόρτωσης στο Aspose.HTML για Java

## Εισαγωγή
Όταν χρειάζεται να **get outer html** από μια απομακρυσμένη σελίδα και να αντιδράσετε αμέσως μόλις το έγγραφο ολοκληρώσει τη φόρτωση, η διαχείριση των συμβάντων φόρτωσης του εγγράφου γίνεται απαραίτητη. Στη Java, το Aspose.HTML σας παρέχει ένα καθαρό API για να πλοηγηθείτε σε μια URL και να ακούσετε το συμβάν `OnLoad`, επιτρέποντάς σας να έχετε ασφαλή πρόσβαση στο HTML μόλις είναι έτοιμο. Αυτό το tutorial σας καθοδηγεί σε όλη τη διαδικασία — από τη ρύθμιση του περιβάλλοντος μέχρι την εκτύπωση του εξωτερικού HTML μιας φορτωμένης σελίδας — ώστε να το ενσωματώσετε σε οποιαδήποτε εφαρμογή Java προσανατολισμένη στο web.

## Σύντομες Απαντήσεις
- **What does “get outer html” mean?** Επιστρέφει το πλήρες HTML markup του ριζικού στοιχείου του εγγράφου.  
- **Which library handles load events?** Το Aspose.HTML for Java παρέχει το συμβάν `OnLoad`.  
- **Do I need a license for testing?** Διατίθεται δωρεάν δοκιμαστική έκδοση· απαιτείται εμπορική άδεια για παραγωγή.  
- **How can I wait for the document to load?** Χρησιμοποιήστε τον χειριστή `OnLoad` ή ένα απλό sleep για σκοπούς επίδειξης.  
- **Is this approach async‑safe?** Ναι, το συμβάν ενεργοποιείται μετά το τέλος της φόρτωσης του εγγράφου, εξασφαλίζοντας ότι το HTML είναι έτοιμο.

## Τι είναι το “get outer html”;
`document.getDocumentElement().getOuterHTML()` επιστρέφει το πλήρες HTML string του ριζικού στοιχείου του εγγράφου, συμπεριλαμβανομένων των ανοικτών και κλειστών ετικετών. Αυτό είναι χρήσιμο όταν χρειάζεστε το ακατέργαστο markup για περαιτέρω επεξεργασία, αποθήκευση ή μετατροπή.

## Γιατί να χρησιμοποιήσετε το Aspose.HTML για Java;
- **Robust HTML parsing** χωρίς την ανάγκη μηχανής προγράμματος περιήγησης.  
- **Event‑driven model** σας επιτρέπει να αντιδράτε ακριβώς όταν το έγγραφο είναι έτοιμο.  
- **Cross‑platform** υποστήριξη για Windows, Linux και macOS.  
- **Rich API** για πλοήγηση, μετασχηματισμό και μετατροπή σε PDF, εικόνα κ.λπ.

## Προαπαιτούμενα
Πριν προχωρήσουμε στον κώδικα, βεβαιωθείτε ότι έχετε τα εξής:

1. **Java Development Kit (JDK)** – Εγκατάσταση από [Oracle's website](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html).  
2. **Aspose.HTML for Java** – Λήψη του τελευταίου JAR από τη [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse ή οποιονδήποτε επεξεργαστή προτιμάτε.  
4. **Basic Java knowledge** – Κατανόηση κλάσεων, μεθόδων και διαχείρισης συμβάντων.  
5. **Internet connection** – Το παράδειγμα φορτώνει μια online HTML σελίδα.

Μόλις όλα είναι έτοιμα, μπορείτε να ξεκινήσετε τον κώδικα!

## Οδηγός Βήμα‑βήμα

### Βήμα 1: Αρχικοποίηση ενός HTML Document
Πρώτα, δημιουργήστε μια παρουσία του `HTMLDocument`. Επίσης, ρυθμίζουμε ένα `AtomicBoolean` για να παρακολουθούμε την κατάσταση φόρτωσης.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument();
java.util.concurrent.atomic.AtomicBoolean isLoading = new java.util.concurrent.atomic.AtomicBoolean(false);
```

### Βήμα 2: Εγγραφή στο συμβάν **OnLoad**
Συνδέστε έναν χειριστή που αλλάζει τη σημαία `isLoading` μόλις το έγγραφο ολοκληρώσει τη φόρτωση. Εδώ θα ξέρουμε πότε είναι ασφαλές να καλέσουμε **get outer html**.

```java
document.OnLoad.add(new DOMEventHandler() {
    @Override
    public void invoke(Object o, Event event) {
        isLoading.set(true);
    }
});
```

### Βήμα 3: Πλοήγηση στο Έγγραφο (φόρτωση html από url)
Δώστε στο `HTMLDocument` τη σελίδα που πρέπει να ανακτήσει. Σε αυτό το παράδειγμα φορτώνουμε μια δημόσια σελίδα τεκμηρίωσης του Aspose.

```java
document.navigate("https://docs.aspose.com/html/net/creating-a-document/document.html");
```

### Βήμα 4: Αναμονή για τη Φόρτωση του Εγγράφου
Η φόρτωση μιας απομακρυσμένης σελίδας είναι ασύγχρονη. Για επίδειξη, παύουμε το νήμα για λίγα δευτερόλεπτα· σε παραγωγή θα βασιζόσασταν στη σημαία `OnLoad` ή σε πιο εξελιγμένη τεχνική συγχρονισμού.

```java
Thread.sleep(5000);
```

### Βήμα 5: Πρόσβαση στο Φορτωμένο Έγγραφο και **Get Outer HTML**
Τώρα που το `isLoading` είναι αληθές, ανακτήστε το πλήρες markup του ριζικού στοιχείου του εγγράφου.

```java
System.out.println("outerHTML = " + document.getDocumentElement().getOuterHTML());
```

Θα πρέπει να δείτε το πλήρες HTML της φορτωμένης σελίδας να εκτυπώνεται στην κονσόλα.

## Συχνά Προβλήματα και Λύσεις
| Πρόβλημα | Αιτία | Διόρθωση |
|----------|-------|----------|
| **`isLoading` never becomes true** | Ο χειριστής `OnLoad` δεν είχε προσαρτηθεί πριν από το `navigate()` | Προσαρτήστε τον χειριστή **πριν** καλέσετε το `navigate()`. |
| **`NullPointerException` on `getDocumentElement()`** | Το έγγραφο δεν είναι πλήρως φορτωμένο όταν προσπελάστηκε | Χρησιμοποιήστε έναν κατάλληλο μηχανισμό αναμονής (π.χ., βρόχο στο `isLoading.get()` ή ένα `CountDownLatch`). |
| **SSLHandshakeException** when loading HTTPS URLs | Λείπουν αξιόπιστα πιστοποιητικά | Προσθέστε το κατάλληλο πιστοποιητικό στο Java keystore ή χρησιμοποιήστε `-Djsse.enableSNIExtension=false`. |
| **Slow loading causing timeout** | Μεγάλη σελίδα ή καθυστέρηση δικτύου | Αυξήστε τη διάρκεια του sleep ή υλοποιήστε έναν listener που λαμβάνει υπόψη το timeout. |

## Συχνές Ερωτήσεις

**Q: What is Aspose.HTML for Java?**  
**A:** Το Aspose.HTML for Java είναι μια βιβλιοθήκη που επιτρέπει στους προγραμματιστές να δημιουργούν, να επεξεργάζονται και να μετατρέπουν έγγραφα HTML σε εφαρμογές Java.

**Q: How do I download Aspose.HTML for Java?**  
**A:** Μπορείτε να το κατεβάσετε από τη [Aspose releases page](https://releases.aspose.com/html/java/).

**Q: Can I use Aspose.HTML for free?**  
**A:** Ναι, μπορείτε να δοκιμάσετε το Aspose.HTML δωρεάν κατεβάζοντας μια δοκιμαστική έκδοση από την [Aspose website](https://releases.aspose.com/).

**Q: Is there any support available for Aspose.HTML?**  
**A:** Ναι, μπορείτε να βρείτε υποστήριξη και να θέσετε ερωτήσεις στο [Aspose forum](https://forum.aspose.com/c/html/29).

**Q: How do I get a temporary license for Aspose.HTML?**  
**A:** Μπορείτε να ζητήσετε προσωρινή άδεια επισκεπτόμενοι τη [Aspose temporary license page](https://purchase.aspose.com/temporary-license/).

---

**Τελευταία ενημέρωση:** 2026-04-23  
**Δοκιμή με:** Aspose.HTML for Java 24.11  
**Συγγραφέας:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}