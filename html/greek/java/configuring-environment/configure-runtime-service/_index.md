---
date: 2026-05-14
description: Μάθετε πώς να ορίσετε χρόνο λήξης στο Aspose.HTML for Java, να διαμορφώσετε
  το Runtime Service για τη μετατροπή html σε png, να αποτρέψετε άπειρους βρόχους
  και να βελτιώσετε την απόδοση.
keywords:
- html to png conversion
- convert html to png
- java html processing
- prevent infinite loops java
- control script execution
linktitle: Διαμόρφωση του Runtime Service στο Aspose.HTML
schemas:
- author: Aspose
  dateModified: '2026-05-14'
  description: Learn how to set timeout in Aspose.HTML for Java, configure the Runtime
    Service for html to png conversion, prevent infinite loops, and boost performance.
  headline: How to Set Timeout for html to png conversion in Aspose.HTML for Java
    Runtime Service
  type: TechArticle
- description: Learn how to set timeout in Aspose.HTML for Java, configure the Runtime
    Service for html to png conversion, prevent infinite loops, and boost performance.
  name: How to Set Timeout for html to png conversion in Aspose.HTML for Java Runtime
    Service
  steps:
  - name: '**Java Development Kit (JDK)** – install it from [Oracle''s website](https://www.oracle.com/java/technologies/javase-downloads.html).'
    text: '**Java Development Kit (JDK)** – install it from [Oracle''s website](https://www.oracle.com/java/technologies/javase-downloads.html).'
  - name: '**Aspose.HTML for Java Library** – grab the newest build from the [Aspose
      releases page](https://releases.aspose.com/html/java/).'
    text: '**Aspose.HTML for Java Library** – grab the newest build from the [Aspose
      releases page](https://releases.aspose.com/html/java/).'
  - name: '**IDE** – IntelliJ IDEA, Eclipse, or NetBeans will work fine.'
    text: '**IDE** – IntelliJ IDEA, Eclipse, or NetBeans will work fine.'
  - name: '**Basic Java & HTML knowledge** – essential for following the code snippets.'
    text: '**Basic Java & HTML knowledge** – essential for following the code snippets.'
  type: HowTo
- questions:
  - answer: It lets you control script execution time, helping to **prevent infinite
      loops** and keep conversions responsive.
    question: What is the purpose of the Runtime Service in Aspose.HTML for Java?
  - answer: Get the latest version from the [releases page](https://releases.aspose.com/html/java/).
    question: How can I download Aspose.HTML for Java?
  - answer: Yes, disposing releases native resources and prevents memory leaks.
    question: Is it necessary to dispose of the `document` and `configuration` objects?
  - answer: Absolutely – change the `TimeSpan.fromSeconds()` argument to whatever
      limit fits your scenario.
    question: Can I set the JavaScript timeout to a value other than 5 seconds?
  - answer: Visit the [Aspose.HTML forum](https://forum.aspose.com/c/html/29) for
      community and staff assistance.
    question: Where can I find help if I run into issues?
  type: FAQPage
second_title: Java HTML Processing with Aspose.HTML
title: Πώς να ορίσετε χρόνο λήξης για τη μετατροπή html σε png στο Aspose.HTML for
  Java Runtime Service
url: /el/java/configuring-environment/configure-runtime-service/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ορίσετε χρονικό όριο για τη μετατροπή html σε png στο Aspose.HTML για Java Runtime Service

## Εισαγωγή
Αν ψάχνετε να **ορίσετε ένα χρονικό όριο** για τα σενάρια όταν εργάζεστε με το Aspose.HTML για Java, βρίσκεστε στο σωστό μέρος. Ο έλεγχος της εκτέλεσης των σεναρίων όχι μόνο αποτρέπει τα άπειρα βρόχους, αλλά επίσης επιταχύνει τη **μετατροπή html σε png** και διατηρεί την εφαρμογή σας ανταποκρινόμενη. Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα τις ακριβείς διαδικασίες για τη διαμόρφωση του Runtime Service, τον περιορισμό της εκτέλεσης των σεναρίων, και τελικά την παραγωγή μιας εικόνας PNG από HTML χωρίς να κρεμάει το πρόγραμμα σας.

## Γρήγορες Απαντήσεις
- **Τι κάνει το Runtime Service;** Σας επιτρέπει να ελέγχετε το χρόνο εκτέλεσης των σεναρίων και να διαχειρίζεστε πόρους κατά την επεξεργασία HTML.  
- **Πώς να ορίσετε χρονικό όριο για JavaScript;** Ανακτήστε το `IRuntimeService` από τη διαμόρφωση και καλέστε `setJavaScriptTimeout(TimeSpan.fromSeconds(...))`.  
- **Μπορώ να αποτρέψω άπειρους βρόχους;** Ναι – το χρονικό όριο σταματά βρόχους που υπερβαίνουν το καθορισμένο όριο.  
- **Επηρεάζει αυτή η ρύθμιση τη μετατροπή html σε png;** Όχι, η μετατροπή προχωρά μόλις το σενάριο ολοκληρωθεί ή τερματιστεί από το χρονικό όριο.  
- **Ποια έκδοση του Aspose.HTML απαιτείται;** Η πιο πρόσφατη έκδοση από τη σελίδα λήψεων του Aspose.

## Πώς να ορίσετε χρονικό όριο για τη μετατροπή html σε png στο Aspose.HTML Runtime Service
Φορτώστε το Runtime Service, ορίστε ένα `TimeSpan` (π.χ., 5 δευτερόλεπτα) χρησιμοποιώντας το `TimeSpan.fromSeconds`, και εφαρμόστε το μέσω `setJavaScriptTimeout`. Αυτό περιορίζει την εκτέλεση του JavaScript, σταματά τους ανεξέλεγκτους βρόχους και εξασφαλίζει ότι η μετατροπή ολοκληρώνεται προβλέψιμα χωρίς να καταναλώνει απεριόριστους πόρους CPU, ενώ εξακολουθεί να επιτρέπει στα τυπικά σενάρια να τρέξουν μέχρι το τέλος.

## Προαπαιτούμενα
Πριν προχωρήσουμε στις λεπτομέρειες, βεβαιωθείτε ότι έχετε τα εξής:

1. **Java Development Kit (JDK)** – εγκαταστήστε το από την [ιστοσελίδα της Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java Library** – κατεβάστε την πιο πρόσφατη έκδοση από τη [σελίδα κυκλοφοριών του Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse ή NetBeans θα λειτουργήσουν καλά.  
4. **Βασικές γνώσεις Java & HTML** – απαραίτητες για την κατανόηση των αποσπασμάτων κώδικα.

## Εισαγωγή Πακέτων
Οι δηλώσεις εισαγωγής φέρνουν τις απαιτούμενες κλάσεις από τη Java και το Aspose.HTML στο πεδίο ορατότητας, επιτρέποντας τη διαχείριση αρχείων και τη διαμόρφωση της υπηρεσίας. `java.io.IOException` είναι μια εξαίρεση που ρίχνεται όταν μια λειτουργία I/O αποτυγχάνει ή διακόπτεται.

```java
import java.io.IOException;
```

## Βήμα 1: Δημιουργία αρχείου HTML με κώδικα JavaScript
Η δημιουργία ενός αρχείου HTML με έναν βρόχο JavaScript δείχνει ένα πιθανό σενάριο άπειρου κώδικα, το οποίο θα σταματήσουμε αργότερα χρησιμοποιώντας χρονικό όριο. `java.io.FileWriter` είναι μια κλάση για τη γραφή αρχείων χαρακτήρων στο δίσκο.

```java
String code = "<h1>Runtime Service</h1>\r\n" +
        "<script> while(true) {} </script>\r\n" +
        "<p>The Runtime Service optimizes your system by helping it start apps and programs faster.</p>\r\n";
try (java.io.FileWriter fileWriter = new java.io.FileWriter("runtime-service.html")) {
    fileWriter.write(code);
}
```

- Το σενάριο `while(true) {}` αντιπροσωπεύει έναν πιθανό άπειρο βρόχο.  
- Το `FileWriter` γράφει το περιεχόμενο HTML στο **runtime-service.html**.

## Βήμα 2: Ρύθμιση του αντικειμένου Configuration
Η κλάση `Configuration` κρατά τις ρυθμίσεις για όλες τις υπηρεσίες Aspose.HTML, συμπεριλαμβανομένου του Runtime Service, και λειτουργεί ως κεντρικός κόμβος για προσαρμοσμένες επιλογές.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
```

## Βήμα 3: Διαμόρφωση του Runtime Service
Το `IRuntimeService` παρέχει έλεγχο της εκτέλεσης των σεναρίων, όπως ορισμός χρονικών ορίων, για την προστασία του περιβάλλοντος φιλοξενίας από ανεξέλεγκτο κώδικα.

```java
try {
    com.aspose.html.services.IRuntimeService runtimeService = configuration.getService(com.aspose.html.services.IRuntimeService.class);
    runtimeService.setJavaScriptTimeout(com.aspose.html.utils.TimeSpan.fromSeconds(5));
```

- Το `setJavaScriptTimeout` περιορίζει την εκτέλεση του σεναρίου σε **5 δευτερόλεπτα**, αποτρέποντας αποτελεσματικά **άπειρους βρόχους**.  
- Αυτό επίσης **περιορίζει την εκτέλεση σεναρίων** για οποιονδήποτε βαρύ κώδικα στην πλευρά του πελάτη.

## Βήμα 4: Φόρτωση του εγγράφου HTML με τη διαμόρφωση
Η κλάση `Document` φορτώνει και αντιπροσωπεύει μια σελίδα HTML με τη δοθείσα διαμόρφωση, διασφαλίζοντας ότι ο κανόνας χρονικού ορίου εφαρμόζεται κατά την ανάλυση.

```java
    com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("runtime-service.html", configuration);
```

- Το έγγραφο σέβεται το χρονικό όριο που ορίστηκε νωρίτερα, έτσι ο ατελείωτος βρόχος θα σταματήσει μετά από 5 δευτερόλεπτα.

## Βήμα 5: Μετατροπή του HTML σε PNG
Το `ImageSaveOptions` καθορίζει τη μορφή εξόδου και τις επιλογές απόδοσης για τη μετατροπή εικόνας, επιτρέποντας μια καθαρή **μετατροπή html σε png** μόλις το σενάριο ολοκληρωθεί ή διακοπεί.

```java
    com.aspose.html.converters.Converter.convertHTML(
        document,
        new com.aspose.html.saving.ImageSaveOptions(),
        "runtime-service_out.png"
    );
```

- Το `ImageSaveOptions` λέει στο Aspose.HTML να εξάγει μια εικόνα PNG.  
- Το παραγόμενο αρχείο, **runtime-service_out.png**, εμφανίζει το αποδομένο HTML χωρίς κρέμασμα.

## Βήμα 6: Καθαρισμός Πόρων
Η κλήση του `dispose()` απελευθερώνει τους εγγενείς πόρους που χρησιμοποιούν τα αντικείμενα Aspose.HTML, αποτρέποντας διαρροές μνήμης σε εφαρμογές μακράς διάρκειας.

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

- Η σωστή απελευθέρωση είναι απαραίτητη για εφαρμογές μακράς διάρκειας.

## Γιατί είναι σημαντικό
Ένα χρονικό όριο προστατεύει τη γραμμή μετατροπής σας τερματίζοντας σενάρια που τρέχουν πολύ ώρα, αποτρέποντας το μπλοκάρισμα νήματος και μειώνοντας το συνολικό χρόνο επεξεργασίας, ειδικά σε υπηρεσίες πολλαπλών ενοικιαστών. Με όριο 5 δευτερολέπτων διατηρείτε τη φυσιολογική συμπεριφορά της σελίδας ενώ αποκόπτετε καταχρηστικά ή ελαττωματικά σενάρια, οδηγώντας σε πιο προβλέψιμη απόδοση της μετατροπής html σε png.

## Συχνά προβλήματα & αντιμετώπιση
- **Το χρονικό όριο είναι πολύ σύντομο** – Πολύπλοκες σελίδες με πολλούς πόρους μπορεί να χρειάζονται μεγαλύτερο όριο. Αυξήστε την τιμή του `TimeSpan` αν παρατηρήσετε πρόωρους τερματισμούς.  
- **Λείπει η απελευθέρωση** – Η παράλειψη κλήσης του `dispose()` μπορεί να οδηγήσει σε διαρροές μνήμης, ειδικά όταν επεξεργάζεστε πολλά έγγραφα σε βρόχο.  
- **Λανθασμένο αντικείμενο διαμόρφωσης** – Πάντα να ανακτάτε το `IRuntimeService` από το ίδιο αντικείμενο `Configuration` που χρησιμοποιείτε για τη φόρτωση του εγγράφου· διαφορετικά το χρονικό όριο δεν θα εφαρμοστεί.

## Συχνές Ερωτήσεις

**Ε: Ποιος είναι ο σκοπός του Runtime Service στο Aspose.HTML για Java;**  
Α: Σας επιτρέπει να ελέγχετε το χρόνο εκτέλεσης των σεναρίων, βοηθώντας στην **αποτροπή άπειρων βρόχων** και διατηρώντας τις μετατροπές ανταποκρινόμενες.

**Ε: Πώς μπορώ να κατεβάσω το Aspose.HTML για Java;**  
Α: Λάβετε την πιο πρόσφατη έκδοση από τη [σελίδα κυκλοφοριών](https://releases.aspose.com/html/java/).

**Ε: Είναι απαραίτητο να απελευθερώσω τα αντικείμενα `document` και `configuration`;**  
Α: Ναι, η απελευθέρωση απελευθερώνει εγγενείς πόρους και αποτρέπει διαρροές μνήμης.

**Ε: Μπορώ να ορίσω το χρονικό όριο JavaScript σε τιμή διαφορετική από 5 δευτερόλεπτα;**  
Α: Απόλυτα – αλλάξτε το όρισμα του `TimeSpan.fromSeconds()` σε όποιο όριο ταιριάζει στο σενάριό σας.

**Ε: Πού μπορώ να βρω βοήθεια αν αντιμετωπίσω προβλήματα;**  
Α: Επισκεφθείτε το [φόρουμ Aspose.HTML](https://forum.aspose.com/c/html/29) για βοήθεια από την κοινότητα και το προσωπικό.

{{< blocks/products/products-backtop-button >}}

## Σχετικά Μαθήματα

- [Δημιουργία αρχείου HTML Java & Ρύθμιση Network Service (Aspose.HTML)](/html/java/configuring-environment/setup-network-service/)
- [Πώς να ορίσετε χρονικό όριο – Διαχείριση Network Timeout στο Aspose.HTML για Java](/html/java/message-handling-networking/network-timeout/)
- [Μετατροπή HTML σε PNG με Aspose.HTML για Java](/html/java/conversion-html-to-various-image-formats/convert-html-to-png/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}