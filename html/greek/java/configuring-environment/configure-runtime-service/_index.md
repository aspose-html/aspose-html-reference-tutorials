---
date: 2026-02-10
description: Μάθετε πώς να ορίσετε χρονικό όριο στο Aspose.HTML για Java, να διαμορφώσετε
  την Υπηρεσία Εκτέλεσης για τη μετατροπή HTML σε PNG, να αποτρέψετε άπειρους βρόχους
  και να βελτιώσετε την απόδοση.
linktitle: Configure Runtime Service in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Πώς να ορίσετε χρονικό όριο στην υπηρεσία χρόνου εκτέλεσης Aspose.HTML για
  Java
url: /el/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε Timeout στο Aspose.HTML για Java Runtime Service

## Εισαγωγή
Αν ψάχνετε **πώς να ορίσετε timeout** για σενάρια όταν εργάζεστε με το Aspose.HTML για Java, βρίσκεστε στο σωστό μέρος. Ο έλεγχος της εκτέλεσης των σεναρίων όχι μόνο αποτρέπει άπειρους βρόχους, αλλά και βοηθά να **μετατρέψετε html σε png** πιο γρήγορα και να διατηρήσετε την εφαρμογή σας ανταποκρινόμενη. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς ρυθμίσεις του Runtime Service, τον περιορισμό της εκτέλεσης σεναρίων και, τελικά, την παραγωγή μιας εικόνας PNG από HTML χωρίς να «κολλάει» το πρόγραμμα σας.

## Πώς να ορίσετε timeout στο Aspose.HTML Runtime Service
Η κατανόηση του σκοπού του Runtime Service κάνει πιο εύκολο το γιατί ένα timeout είναι απαραίτητο. Η υπηρεσία λειτουργεί ως «αυλή» για κώδικα client‑side, δίνοντάς σας τη δυνατότητα να σταματήσετε ανεξέλεγκτο JavaScript πριν καταναλώσει όλους τους κύκλους CPU. Ορίζοντας ένα timeout προστατεύετε τον διακομιστή σας από σενάρια άρνησης υπηρεσίας (DoS) και εξασφαλίζετε ότι η **μετατροπή html σε png** ολοκληρώνεται σε προβλέψιμο χρόνο.

## Γρήγορες Απαντήσεις
- **Τι κάνει το Runtime Service;** Σας επιτρέπει να ελέγχετε το χρόνο εκτέλεσης σεναρίων και να διαχειρίζεστε πόρους κατά την επεξεργασία HTML.  
- **Πώς να ορίσετε timeout για JavaScript;** Χρησιμοποιήστε `runtimeService.setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Μπορώ να αποτρέψω άπειρους βρόχους;** Ναι – το timeout σταματά βρόχους που υπερβαίνουν το καθορισμένο όριο.  
- **Επηρεάζει αυτό τη μετατροπή HTML‑σε‑PNG;** Όχι, η μετατροπή προχωρά μόλις το σενάριο ολοκληρωθεί ή τερματιστεί από το timeout.  
- **Ποια έκδοση του Aspose.HTML απαιτείται;** Η πιο πρόσφατη έκδοση από τη σελίδα λήψεων του Aspose.  

## Προαπαιτούμενα
Πριν βουτήξουμε στις λεπτομέρειες, βεβαιωθείτε ότι έχετε τα εξής:

1. **Java Development Kit (JDK)** – εγκαταστήστε το από την [ιστοσελίδα της Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java Library** – κατεβάστε την πιο πρόσφατη έκδοση από τη [σελίδα releases του Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse ή NetBeans θα δουλέψουν άψογα.  
4. **Βασικές γνώσεις Java & HTML** – απαραίτητες για την κατανόηση των αποσπασμάτων κώδικα.

## Εισαγωγή Πακέτων
Πρώτα, εισάγετε τις κλάσεις που θα χρειαστείτε. Η εισαγωγή `java.io.IOException` είναι απαραίτητη για τη διαχείριση αρχείων.

```java
import java.io.IOException;
```

## Βήμα 1: Δημιουργία αρχείου HTML με κώδικα JavaScript
Θα ξεκινήσουμε δημιουργώντας ένα απλό αρχείο HTML που περιέχει έναν βρόχο JavaScript. Αυτός ο βρόχος θα τρέχει για πάντα αν δεν επιβληθεί timeout, καθιστώντας το τέλειο παράδειγμα για το Runtime Service.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- Το σενάριο `while(true) {}` αντιπροσωπεύει έναν πιθανό άπειρο βρόχο.  
- Η `FileWriter` γράφει το περιεχόμενο HTML στο αρχείο **runtime-service.html**.

## Βήμα 2: Δημιουργία αντικειμένου Configuration
Στη συνέχεια, δημιουργήστε μια παρουσία `Configuration`. Αυτό το αντικείμενο αποτελεί τη ραχοκοκαλιά για όλες τις υπηρεσίες Aspose.HTML, συμπεριλαμβανομένου του Runtime Service.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Βήμα 3: Ρύθμιση του Runtime Service
Εδώ είναι που πραγματικά **πώς να ορίσετε timeout**. Ανακτώντας το `IRuntimeService` από τη διαμόρφωση, μπορούμε να ορίσουμε ένα όριο εκτέλεσης JavaScript.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- Η `setJavaScriptTimeout` περιορίζει την εκτέλεση σεναρίου στα **5 δευτερόλεπτα**, αποτρέποντας έτσι **άπειρους βρόχους**.  
- Αυτό επίσης **περιορίζει την εκτέλεση σεναρίου** για οποιονδήποτε βαρύ κώδικα client‑side.

## Βήμα 4: Φόρτωση του εγγράφου HTML με τη διαμόρφωση
Τώρα φορτώστε το αρχείο HTML χρησιμοποιώντας τη διαμόρφωση που περιέχει τον κανόνα timeout.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Το έγγραφο σέβεται το timeout που ορίστηκε νωρίτερα, οπότε ο ατελείωτος βρόχος θα σταματήσει μετά από 5 δευτερόλεπτα.

## Βήμα 5: Μετατροπή HTML σε PNG
Με το έγγραφο ασφαλώς φορτωμένο, μπορούμε να **μετατρέψουμε html σε png**. Η μετατροπή πραγματοποιείται μόνο αφού το σενάριο ολοκληρωθεί ή τερματιστεί από το timeout.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- Η `ImageSaveOptions` λέει στο Aspose.HTML να αποδώσει μια εικόνα PNG.  
- Το παραγόμενο αρχείο, **runtime-service_out.png**, εμφανίζει το αποδομένο HTML χωρίς να «κολλάει».

## Βήμα 6: Καθαρισμός Πόρων
Τέλος, απελευθερώστε τα αντικείμενα για να ελευθερώσετε μνήμη και να αποφύγετε διαρροές.

```java
} finally {
    if (document != null) {
        document.dispose();
    }
    if (configuration != null) {
        configuration.dispose();
    }
}
```

- Η σωστή απελευθέρωση είναι ουσιώδης για εφαρμογές μεγάλης διάρκειας.

## Γιατί είναι σημαντικό
Η ρύθμιση ενός timeout δεν είναι μόνο ένα δίχτυ ασφαλείας· βελτιώνει άμεσα την αξιοπιστία των **pipeline μετατροπής html σε png**. Όταν ενσωματώνετε το Aspose.HTML σε μια υπηρεσία web που επεξεργάζεται HTML που δημιουργείται από χρήστες, ένα κακόβουλο σενάριο θα μπορούσε διαφορετικά να «κλειδώσει» ένα νήμα επ' άπειρο. Ένα μέτριο timeout (π.χ. 5 δευτερόλεπτα) δίνει στα νόμιμα σενάρια αρκετό χρόνο για εκτέλεση, ενώ αποκόπτει την κακόβουλη συμπεριφορά.

## Συχνά προβλήματα & αντιμετώπιση
- **Timeout πολύ μικρό** – Πολύπλοκες σελίδες με πολλούς πόρους μπορεί να χρειάζονται μεγαλύτερο όριο. Αυξήστε την τιμή του `TimeSpan` αν δείτε πρόωρες τερματισμούς.  
- **Λείπει η απελευθέρωση** – Η παράλειψη κλήσης `dispose()` μπορεί να οδηγήσει σε διαρροές μνήμης native, ειδικά όταν επεξεργάζεστε πολλά έγγραφα σε βρόχο.  
- **Λανθασμένο αντικείμενο διαμόρφωσης** – Πάντα ανακτάτε το `IRuntimeService` από την ίδια παρουσία `Configuration` που χρησιμοποιείτε για τη φόρτωση του εγγράφου· διαφορετικά το timeout δεν θα εφαρμοστεί.

## Συχνές Ερωτήσεις

**Ε: Ποιος είναι ο σκοπός του Runtime Service στο Aspose.HTML για Java;**  
Α: Σας επιτρέπει να ελέγχετε το χρόνο εκτέλεσης σεναρίων, βοηθώντας στην **αποτροπή άπειρων βρόχων** και διατηρώντας τις μετατροπές ανταποκρινόμενες.

**Ε: Πώς μπορώ να κατεβάσω το Aspose.HTML για Java;**  
Α: Λάβετε την πιο πρόσφατη έκδοση από τη [σελίδα releases](https://releases.aspose.com/html/java/).

**Ε: Είναι απαραίτητο να απελευθερώσω τα αντικείμενα `document` και `configuration`;**  
Α: Ναι, η απελευθέρωση απελευθερώνει native πόρους και αποτρέπει διαρροές μνήμης.

**Ε: Μπορώ να ορίσω το timeout JavaScript σε τιμή διαφορετική από 5 δευτερόλεπτα;**  
Α: Φυσικά – αλλάξτε το όρισμα της `TimeSpan.fromSeconds()` στην τιμή που ταιριάζει στο σενάριό σας.

**Ε: Πού μπορώ να βρω βοήθεια αν αντιμετωπίσω προβλήματα;**  
Α: Επισκεφθείτε το [φόρουμ Aspose.HTML](https://forum.aspose.com/c/html/29) για υποστήριξη από την κοινότητα και το προσωπικό.

---

**Τελευταία ενημέρωση:** 2026-02-10  
**Δοκιμασμένο με:** Aspose.HTML for Java 24.11 (τελευταία)  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}