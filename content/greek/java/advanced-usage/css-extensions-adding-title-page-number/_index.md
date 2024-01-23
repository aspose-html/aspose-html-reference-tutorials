---
title: Προσαρμόστε τα περιθώρια σελίδας HTML με το Aspose.HTML
linktitle: Επεκτάσεις CSS - Προσθήκη τίτλου και αριθμού σελίδας
second_title: Επεξεργασία Java HTML με Aspose.HTML
description: Μάθετε πώς να προσαρμόζετε τα περιθώρια σελίδων, να προσθέτετε αριθμούς σελίδων και τίτλους σε έγγραφα HTML χρησιμοποιώντας το Aspose.HTML για Java.
type: docs
weight: 10
url: /el/java/advanced-usage/css-extensions-adding-title-page-number/
---
Το Aspose.HTML για Java είναι μια ισχυρή βιβλιοθήκη για την επεξεργασία εγγράφων HTML σε εφαρμογές Java. Σε αυτό το σεμινάριο, θα διερευνήσουμε πώς να δημιουργήσετε προσαρμοσμένα περιθώρια σελίδας και να προσθέσετε αριθμούς σελίδων και τίτλους στα έγγραφά σας HTML χρησιμοποιώντας το Aspose.HTML για Java. Αυτός ο οδηγός βήμα προς βήμα θα αναλύσει τη διαδικασία σε διαχειρίσιμα βήματα για να σας βοηθήσει να ενσωματώσετε εύκολα αυτές τις δυνατότητες στα έγγραφά σας HTML.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:

1. Περιβάλλον ανάπτυξης Java: Βεβαιωθείτε ότι έχετε ρυθμίσει ένα περιβάλλον ανάπτυξης Java στον υπολογιστή σας.

2.  Aspose.HTML για Java: Κατεβάστε και εγκαταστήστε τη βιβλιοθήκη Aspose.HTML για Java από[εδώ](https://releases.aspose.com/html/java/).

## Εισαγωγή πακέτων

Για να ξεκινήσετε, πρέπει να εισαγάγετε τα απαραίτητα πακέτα από το Aspose.HTML για Java. Προσθέστε τις ακόλουθες δηλώσεις εισαγωγής στον κώδικα Java σας:

```java
// Εισαγωγή πακέτων Aspose.HTML
import com.aspose.html.Configuration;
import com.aspose.html.services.IUserAgentService;
import com.aspose.html.HTMLDocument;
import com.aspose.html.rendering.xps.XpsDevice;
```

Τώρα, ας αναλύσουμε τη διαδικασία προσθήκης προσαρμοσμένων περιθωρίων, αριθμών σελίδων και τίτλων σε διαχειρίσιμα βήματα:

## Βήμα 1: Αρχικοποίηση διαμόρφωσης και περιθωρίων σελίδας

```java
// Αρχικοποιήστε το αντικείμενο διαμόρφωσης και ορίστε τα περιθώρια σελίδας για το έγγραφο
Configuration configuration = new Configuration();
try {
    // Αποκτήστε την υπηρεσία User Agent
    IUserAgentService userAgent = configuration.getService(IUserAgentService.class);
    // Ορίστε το στυλ των προσαρμοσμένων περιθωρίων και δημιουργήστε σημάδια σε αυτό
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

Σε αυτό το βήμα, αρχικοποιούμε το αντικείμενο διαμόρφωσης και ρυθμίζουμε προσαρμοσμένα περιθώρια σελίδας, συμπεριλαμβανομένης της θέσης του μετρητή σελίδας και του τίτλου της σελίδας.

## Βήμα 2: Αρχικοποιήστε ένα έγγραφο HTML

```java
// Αρχικοποιήστε ένα έγγραφο HTML
HTMLDocument document = new HTMLDocument("<div>Hello World!!!</div>", ".", configuration);
```

Εδώ, δημιουργούμε ένα έγγραφο HTML με δείγμα περιεχομένου (σε αυτήν την περίπτωση, ένα μήνυμα "Hello World") και εφαρμόζουμε τη διαμόρφωση από το Βήμα 1.

## Βήμα 3: Αρχικοποιήστε μια συσκευή εξόδου και αποδώστε το έγγραφο

```java
// Αρχικοποιήστε μια συσκευή εξόδου
XpsDevice device = new XpsDevice(Resources.output("output.xps"));
try {
    //Στείλτε το έγγραφο στη συσκευή εξόδου
    document.renderTo(device);
} finally {
    if (device != null) {
        device.dispose();
    }
}
```

Σε αυτό το βήμα, ρυθμίζουμε μια συσκευή εξόδου και αποδίδουμε το έγγραφο HTML. Το έγγραφο θα υποβληθεί σε επεξεργασία και θα αποθηκευτεί ως αρχείο XPS με τα καθορισμένα περιθώρια σελίδας, τους αριθμούς σελίδων και τον τίτλο.

## συμπέρασμα

Συγχαρητήρια! Έχετε μάθει με επιτυχία πώς να δημιουργείτε προσαρμοσμένα περιθώρια σελίδας και να προσθέτετε αριθμούς και τίτλους σελίδων στα έγγραφά σας HTML χρησιμοποιώντας το Aspose.HTML για Java. Αυτή η προσαρμογή σάς επιτρέπει να δημιουργείτε πιο επαγγελματικά και οπτικά ελκυστικά έγγραφα.

 Εάν έχετε οποιεσδήποτε ερωτήσεις ή αντιμετωπίζετε προβλήματα, μη διστάσετε να επισκεφθείτε το[Aspose.HTML για τεκμηρίωση Java](https://reference.aspose.com/html/java/) ή ζητήστε βοήθεια για το[Aspose forum υποστήριξης](https://forum.aspose.com/).

## Συχνές ερωτήσεις

### Ε1: Τι είναι το Aspose.HTML για Java;

A1: Το Aspose.HTML για Java είναι μια βιβλιοθήκη Java που παρέχει ισχυρά εργαλεία για εργασία με έγγραφα HTML σε εφαρμογές Java.

### Ε2: Μπορώ να προσαρμόσω περαιτέρω τα περιθώρια της σελίδας;

A2: Ναι, μπορείτε να τροποποιήσετε τα στυλ CSS στο Βήμα 1 για να προσαρμόσετε τα περιθώρια σελίδας σύμφωνα με τις απαιτήσεις σας.

### Ε3: Πώς μπορώ να προσθέσω περισσότερο περιεχόμενο στο έγγραφο HTML;

A3: Μπορείτε να τροποποιήσετε το περιεχόμενο HTML στο Βήμα 2 αντικαθιστώντας το δείγμα περιεχομένου με το δικό σας.

### Ε4: Είναι το Aspose.HTML για Java συμβατό με άλλες μορφές εγγράφων;

A4: Ναι, το Aspose.HTML για Java μπορεί να χρησιμοποιηθεί για τη μετατροπή εγγράφων HTML σε διάφορες μορφές, συμπεριλαμβανομένων των PDF, XPS και εικόνων.

### Ε5: Χρειάζομαι άδεια χρήσης για τη χρήση του Aspose.HTML για Java;

 A5: Ναι, μπορείτε να αποκτήσετε άδεια ή δωρεάν δοκιμή από[εδώ](https://purchase.aspose.com/buy) ή[εδώ](https://releases.aspose.com/).