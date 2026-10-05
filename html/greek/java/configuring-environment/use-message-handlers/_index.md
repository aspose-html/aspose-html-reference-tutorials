---
date: 2026-02-10
description: Μάθετε πώς να χρησιμοποιείτε το Aspose για να διαχειρίζεστε σπασμένους
  συνδέσμους Java, να μετατρέπετε HTML σε PNG και να φορτώνετε έγγραφο HTML Java με
  το Aspose.HTML για Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Μετατροπή HTML σε PNG με τους Διαχειριστές Μηνυμάτων Aspose.HTML σε Java
url: /el/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PNG με Message Handlers του Aspose.HTML σε Java

## Εισαγωγή
Σε αυτό το tutorial θα ανακαλύψετε **πώς να μετατρέψετε HTML σε PNG** ενώ διαχειρίζεστε με χάρη τους ελλιπείς πόρους χρησιμοποιώντας το Aspose.HTML για Java. Θα περάσουμε από τη δημιουργία μιας μικρής σελίδας HTML που παραπέμπει σε μια μη‑υπάρχουσα εικόνα, τη σύνδεση ενός **custom message handler** για **παρεμβολή σε network requests**, τη διαμόρφωση του **network service**, τη φόρτωση του εγγράφου και, τέλος, την εκτέλεση της **μετατροπής html σε εικόνα**. Στο τέλος θα έχετε ένα σταθερό μοτίβο τόσο για **handle broken links java** όσο και για παραγωγή PNG υψηλής ποιότητας — ιδανικό για αναφορές, μικρογραφίες ή προεπισκοπήσεις email.

## Γρήγορες Απαντήσεις
- **Τι κάνει ένας message handler;** Παρεμβάλλεται σε network operations (όπως αιτήματα εικόνας) και σας επιτρέπει να αντιδράτε σε κωδικούς κατάστασης όπως 404.  
- **Μπορεί το Aspose.HTML να μετατρέψει HTML σε PNG;** Ναι—`Converter.convertHTML` εκτελεί τη μετατροπή σε μία κλήση.  
- **Χρειάζομαι άδεια για αυτό το παράδειγμα;** Μια προσωρινή άδεια αφαιρεί τους περιορισμούς αξιολόγησης· απαιτείται μόνιμη άδεια για παραγωγική χρήση.  
- **Ποια έκδοση της Java λειτουργεί;** Οποιοδήποτε JDK 8+ (το παράδειγμα εκτελείται σε JDK 11).  
- **Μπορώ να διαμορφώσω το network service;** Απόλυτα—χρησιμοποιήστε `configuration.getService(INetworkService.class)` για να προσθέσετε τον handler σας.

## Προαπαιτούμενα
Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω έτοιμα:

1. **Java Development Kit (JDK)** – κατεβάστε από την [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – αποκτήστε τη βιβλιοθήκη από τη [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse ή NetBeans λειτουργούν καλά.  
4. **Basic Java knowledge** – πρέπει να είστε άνετοι με κλάσεις, try‑with‑resources και διαχείριση εξαιρέσεων.  
5. **Temporary License** – εάν χρησιμοποιείτε δοκιμαστική έκδοση, αποκτήστε μια [temporary license](https://purchase.aspose.com/temporary-license/) για να αποφύγετε τα υδατογραφήματα.

## Εισαγωγή Πακέτων
Πρώτα, εισάγετε την κλάση Java I/O που θα χρειαστούμε για τη διαχείριση αρχείων. Οι υπόλοιπες κλάσεις του Aspose αναφέρονται με πλήρη ονόματα αργότερα, διατηρώντας τη λίστα imports καθαρή.

```java
import java.io.IOException;
```

## Βήμα 1: Προετοιμασία του κώδικα HTML
Δημιουργούμε ένα ελάχιστο απόσπασμα HTML που σκόπιμα αναφέρει μια ελλιπή εικόνα. Αυτό θα ενεργοποιήσει τον handler μας όταν η μηχανή προσπαθήσει να φορτώσει τον πόρο.

```java
String code = "<img src='missing.jpg'>";
```

## Βήμα 2: Εγγραφή του κώδικα HTML σε αρχείο
Στη συνέχεια, αποθηκεύουμε το απόσπασμα στο *document.html*. Η χρήση ενός μπλοκ try‑with‑resources εγγυάται ότι το `FileWriter` κλείνει σωστά.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Βήμα 3: Δημιουργία προσαρμοσμένου Message Handler
Τώρα δημιουργούμε έναν **custom message handler** που ελέγχει την κατάσταση HTTP κάθε network request. Εάν η απάντηση δεν είναι `200`, καταγράφουμε μια φιλική προειδοποίηση. Παρατηρήστε την κλήση στο `invoke(context);` στο τέλος—αυτό προωθεί το αίτημα στον επόμενο handler στην αλυσίδα, αποτρέποντας την αναδρομή.

```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```

## Βήμα 4: Διαμόρφωση του Network Service
Για να κάνει το Aspose.HTML συνειδητό τον handler μας, ανακτούμε το **network service** από ένα αντικείμενο `Configuration` και προσθέτουμε τον handler στη συλλογή του. Αυτό είναι το βήμα όπου **διαμορφώνουμε το network service** για προσαρμοσμένη συμπεριφορά.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Βήμα 5: Φόρτωση του εγγράφου HTML
Με τη διαμόρφωση έτοιμη, φορτώνουμε το *document.html*. Η μηχανή χρησιμοποιεί τώρα το network service μας, έτσι το αίτημα για την ελλιπή εικόνα παρεμποδίζεται από τον handler που προσθέσαμε.

```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```

## Βήμα 6: Μετατροπή HTML σε PNG
Αυτή είναι η καρδιά της διαδικασίας **html to image conversion**. Η μέθοδος `Converter.convertHTML` παίρνει το φορτωμένο `HTMLDocument`, προαιρετικά `ImageSaveOptions` (όπου μπορείτε να ρυθμίσετε DPI ή ποιότητα) και το όνομα του αρχείου εξόδου.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Βήμα 7: Καθαρισμός Πόρων
Καλή πρακτική στη Java απαιτεί να απελευθερώνουμε όλους τους εγγενείς πόρους. Το μπλοκ `finally` εξασφαλίζει ότι το `Configuration` απορρίπτεται ακόμη και αν προκύψει εξαίρεση.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Γιατί να χρησιμοποιήσετε Message Handlers;
Οι message handlers σας παρέχουν **λεπτομερή έλεγχο** σε κάθε network request—είτε είναι εικόνα, CSS, JavaScript ή αρχείο γραμματοσειράς. Αντί να αφήνετε τη βιβλιοθήκη να αποτυγχάνει σιωπηλά, μπορείτε να καταγράψετε ελλιπή πόρους, να παρέχετε εναλλακτικό περιεχόμενο ή ακόμη και να επαναλάβετε το αίτημα. Αυτό κάνει τη διαδικασία επεξεργασίας HTML **αξιόπιστη**, **έτοιμη για παραγωγή**, και πιο εύκολη στην αποσφαλμάτωση.

## Κοινά Προβλήματα και Λύσεις
- **Αναδρομή handler** – Καλέστε `invoke(context);` μόνο μία φορά για να αποφύγετε άπειρους βρόχους.  
- **Έλλειψη άδειας** – Χωρίς έγκυρη άδεια το PNG εξόδου θα περιέχει υδατογράφημα.  
- **Λανθασμένες διαδρομές αρχείων** – Χρησιμοποιήστε απόλυτες διαδρομές ή ορίστε σωστά τον τρέχοντα φάκελο κατά τη φόρτωση του `document.html`.  
- **Μη υποστηριζόμενοι τύποι πόρων** – Βεβαιωθείτε ότι ο πόρος που θέλετε να παρεμβάλετε (εικόνα, CSS, κλπ.) ζητείται πραγματικά από τη μηχανή HTML.

## Συχνές Ερωτήσεις

**Q: Μπορώ να αλυσίδω πολλαπλούς message handlers;**  
A: Ναι, μπορείτε να προσθέσετε πολλούς handlers στη συλλογή `network.getMessageHandlers()`· θα εκτελεστούν με τη σειρά που προστέθηκαν.

**Q: Λειτουργεί ο handler και για πόρους CSS ή script;**  
A: Απόλυτα—οποιοδήποτε network request που κάνει η μηχανή HTML (εικόνες, CSS, JS, γραμματοσειρές) περνάει από τον handler.

**Q: Πώς μπορώ να αλλάξω το HTTP request πριν σταλεί;**  
A: Υλοποιήστε έναν handler που τροποποιεί το `context.getRequest()` πριν καλέσετε `invoke(context)`.

**Q: Υπάρχει τρόπος να καταστέλλετε την προειδοποίηση για συγκεκριμένα URLs;**  
A: Μέσα στον handler, ελέγξτε το `context.getRequest().getRequestUri()` και παραλείψτε την καταγραφή κατά περίπτωση.

**Q: Ποια έκδοση του Aspose.HTML απαιτείται για αυτά τα API;**  
A: Ο κώδικας λειτουργεί με το Aspose.HTML for Java 22.10 και νεότερες εκδόσεις.

## Συμπέρασμα
Τώρα έχετε ένα πλήρες, ολοκληρωμένο παράδειγμα του **πώς να μετατρέψετε HTML σε PNG** χρησιμοποιώντας έναν **custom message handler** για **παρεμβολή σε network requests** και **handle broken links java**. Διαμορφώνοντας το network service, φορτώνοντας το έγγραφο και καλώντας τον converter, μπορείτε αξιόπιστα να δημιουργήσετε μικρογραφίες PNG ή πλήρεις στιγμιότυπα σελίδας σε οποιαδήποτε εφαρμογή Java.

---

**Τελευταία ενημέρωση:** 2026-02-10  
**Δοκιμή με:** Aspose.HTML for Java 24.11  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}