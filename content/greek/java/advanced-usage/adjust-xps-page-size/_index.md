---
title: Προσαρμόστε το μέγεθος σελίδας XPS με το Aspose.HTML για Java
linktitle: Προσαρμογή μεγέθους σελίδας XPS
second_title: Επεξεργασία Java HTML με Aspose.HTML
description: Μάθετε πώς να προσαρμόζετε το μέγεθος σελίδας XPS με το Aspose.HTML για Java. Ελέγξτε εύκολα τις διαστάσεις εξόδου των εγγράφων XPS σας.
type: docs
weight: 16
url: /el/java/advanced-usage/adjust-xps-page-size/
---

Σε αυτό το σεμινάριο, θα σας καθοδηγήσουμε στη διαδικασία προσαρμογής του μεγέθους σελίδας XPS χρησιμοποιώντας το Aspose.HTML για Java. Αυτή η ισχυρή βιβλιοθήκη σάς επιτρέπει να χειρίζεστε έγγραφα HTML και να τα αποδίδετε σε διάφορες μορφές, συμπεριλαμβανομένου του XPS. Η προσαρμογή του μεγέθους της σελίδας είναι απαραίτητη όταν πρέπει να ελέγξετε τις διαστάσεις εξόδου του εγγράφου XPS σας.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τις ακόλουθες προϋποθέσεις:

1. Περιβάλλον ανάπτυξης Java: Βεβαιωθείτε ότι έχετε εγκατεστημένο το Java Development Kit (JDK) στο σύστημά σας.

2.  Aspose.HTML for Java Library: Πρέπει να κάνετε λήψη και να συμπεριλάβετε τη βιβλιοθήκη Aspose.HTML για Java στο έργο σας Java. Μπορείτε να βρείτε τη βιβλιοθήκη[εδώ](https://releases.aspose.com/html/java/).

3. Εισαγωγή αρχείου HTML: Προετοιμάστε ένα αρχείο HTML που θέλετε να αποδώσετε και προσαρμόστε το μέγεθος σελίδας XPS. Μπορείτε να χρησιμοποιήσετε το δικό σας αρχείο HTML για αυτό το σεμινάριο.

## Εισαγωγή πακέτων

Αρχικά, πρέπει να εισαγάγετε τα απαραίτητα πακέτα για να εργαστείτε με το Aspose.HTML για Java. Συμπεριλάβετε αυτά τα πακέτα στην αρχή της τάξης Java:

```java
import com.aspose.html.drawing.Page;
import com.aspose.html.rendering.HtmlRenderer;
import com.aspose.html.rendering.PageSetup;
import com.aspose.html.rendering.xps.XpsDevice;
import com.aspose.html.rendering.xps.XpsRenderingOptions;
import com.aspose.html.HTMLDocument;
```

## Βήμα 1: Ορίστε το όνομα αρχείου εισόδου

```java
try (java.io.FileInputStream fileInputStream = new java.io.FileInputStream("YourInputFile.html")) {
    // ...
}
```

 Σε αυτό το βήμα, διαβάζουμε το αρχείο εισόδου HTML χρησιμοποιώντας a`FileInputStream`.

## Βήμα 2: Δημιουργήστε ένα έγγραφο HTML και ορίστε στυλ

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
               "<div id=id3 class=''st'' style='color: red;'>Aspose.HTML rendering Text in Red Color</div>\n";

// ...
```

 Αυτό το βήμα περιλαμβάνει τη δημιουργία ενός`HTMLDocument` και προσθέτοντας στυλ σε αυτό.

## Βήμα 3: Δημιουργήστε Επιλογές απόδοσης XPS

```java
com.aspose.html.rendering.xps.XpsRenderingOptions xps_options = new com.aspose.html.rendering.xps.XpsRenderingOptions();
```

Εδώ, δημιουργούμε επιλογές απόδοσης XPS για να διαμορφώσουμε τη διαδικασία απόδοσης.

## Βήμα 4: Προσαρμόστε το μέγεθος της σελίδας

```java
com.aspose.html.drawing.Page page = new com.aspose.html.drawing.Page(new com.aspose.html.drawing.Size(100, 100));
com.aspose.html.rendering.PageSetup pageSetup = new com.aspose.html.rendering.PageSetup();
pageSetup.setAnyPage(page);
pageSetup.setAdjustToWidestPage(false);
xps_options.setPageSetup(pageSetup);
```

Αυτό το βήμα περιλαμβάνει τον ορισμό του μεγέθους της σελίδας και τον καθορισμό εάν θα το προσαρμόσετε στην ευρύτερη σελίδα.

## Βήμα 5: Αποδώστε την έξοδο

```java
com.aspose.html.rendering.xps.XpsDevice device = new com.aspose.html.rendering.xps.XpsDevice(xps_options, "YourOutputFile.xps");

renderer.render(device, html_document);
```

Στο τελικό βήμα, αποδίδουμε την έξοδο XPS χρησιμοποιώντας τις διαμορφωμένες επιλογές.

## συμπέρασμα

Σε αυτό το σεμινάριο, σας δείξαμε πώς να προσαρμόσετε το μέγεθος σελίδας XPS χρησιμοποιώντας το Aspose.HTML για Java. Μπορείτε να ελέγξετε τις διαστάσεις εξόδου των εγγράφων XPS σας, διασφαλίζοντας ότι πληρούν τις συγκεκριμένες απαιτήσεις σας. Με τον παρεχόμενο κώδικα και τα βήματα, μπορείτε εύκολα να εφαρμόσετε αυτήν τη δυνατότητα στις εφαρμογές σας Java.

 Εάν έχετε οποιεσδήποτε ερωτήσεις ή χρειάζεστε περαιτέρω βοήθεια, μη διστάσετε να επισκεφθείτε το[Aspose.HTML για τεκμηρίωση Java](https://reference.aspose.com/html/java/) ή ζητήστε βοήθεια για το[Aspose Forum](https://forum.aspose.com/).

## Συχνές ερωτήσεις

### Ε1: Τι είναι το Aspose.HTML για Java;

A1: Το Aspose.HTML for Java είναι μια βιβλιοθήκη Java που επιτρέπει στους προγραμματιστές να χειρίζονται και να μετατρέπουν έγγραφα HTML σε διάφορες μορφές, όπως XPS, PDF και εικόνες.

### Ε2: Πού μπορώ να κατεβάσω το Aspose.HTML για Java;

 A2: Μπορείτε να κάνετε λήψη της βιβλιοθήκης Aspose.HTML για Java από[αυτός ο σύνδεσμος](https://releases.aspose.com/html/java/).

### Ε3: Υπάρχει διαθέσιμη δωρεάν δοκιμή για το Aspose.HTML για Java;

 A3: Ναι, μπορείτε να λάβετε μια δωρεάν δοκιμή του Aspose.HTML για Java από[εδώ](https://releases.aspose.com/).

### Ε4: Πώς μπορώ να αποκτήσω μια προσωρινή άδεια χρήσης για το Aspose.HTML για Java;

 A4: Για να λάβετε μια προσωρινή άδεια χρήσης για το Aspose.HTML για Java, επισκεφτείτε το[αυτή η σελίδα](https://purchase.aspose.com/temporary-license/).

### Ε5: Μπορώ να λάβω υποστήριξη για το Aspose.HTML για Java;

 A5: Ναι, μπορείτε να ζητήσετε βοήθεια και υποστήριξη από την κοινότητα Aspose στο[Aspose Forum](https://forum.aspose.com/).