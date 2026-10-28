---
category: general
date: 2026-10-28
description: Μάθετε πώς να ανοίγετε συνδέσμους σε νέα καρτέλα αναλύοντας HTML σε Java,
  εντοπίζοντας εξωτερικούς συνδέσμους και προσθέτοντας target='_blank'.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- open links new tab
- find external links
- add target blank
- parse html in java
- save modified html
language: el
lastmod: 2026-10-28
og_description: 'Άνοιγμα συνδέσμων σε νέα καρτέλα χρησιμοποιώντας Java: ανάλυση HTML,
  εύρεση εξωτερικών συνδέσμων, προσθήκη target="_blank" και αποθήκευση του τροποποιημένου
  HTML.'
og_image_alt: Screenshot of Java code that parses HTML and updates external links
  to open in a new tab
og_title: Άνοιγμα συνδέσμων σε νέα καρτέλα με Java – οδηγός βήμα‑βήμα
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to open links in a new tab by parsing HTML in Java, finding
    external links and adding target blank.
  headline: How to open links in a new tab with Java
  type: TechArticle
tags:
- Java
- HTML parsing
- jsoup
- web automation
title: Πώς να ανοίξετε συνδέσμους σε νέα καρτέλα με τη Java
url: /el/java/editing-html-documents/how-to-open-links-in-a-new-tab-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να ανοίξετε συνδέσμους σε νέα καρτέλα με Java

Αν χρειάζεστε να **open links in a new tab** από ένα στατικό αρχείο HTML, αυτός ο οδηγός σας δείχνει ακριβώς πώς να το κάνετε. Θα μάθετε να **parse HTML in Java**, **find external links**, **add target blank**, και **save modified HTML** χωρίς να αφήσετε το IDE σας.

Το άνοιγμα εξωτερικών συνδέσμων σε νέα καρτέλα του προγράμματος περιήγησης βελτιώνει την εμπειρία του χρήστη και κρατά τους επισκέπτες στη αρχική σελίδα. Η παρακάτω λύση λειτουργεί με οποιοδήποτε έγγραφο HTML, απαιτεί μόνο τη δημοφιλή βιβλιοθήκη jsoup και εκτελείται σε Java 8 ή νεότερη.

## Προαπαιτούμενα

* JDK 8 + εγκατεστημένο  
* Ένα εργαλείο κατασκευής (Maven ή Gradle) για να τραβήξει την εξάρτηση **jsoup**  
* Ένα αρχείο HTML που περιέχει ετικέτες άγκυρας με την κλάση `external`

Δεν χρειάζεστε διακομιστή web ή πρόσθετα πλαίσια—η jsoup διαχειρίζεται τα πάντα τοπικά.

## Βήμα 1: Ρυθμίστε τη jsoup στο έργο σας

Προσθέστε τη jsoup ως εξάρτηση. Αν χρησιμοποιείτε Maven, τοποθετήστε αυτό στο `pom.xml`:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.17.2</version>
</dependency>
```

Για Gradle, προσθέστε την ακόλουθη γραμμή στο `build.gradle`:

```gradle
implementation 'org.jsoup:jsoup:1.17.2'
```

Αυτές οι συντεταγμένες κατεβάζουν την πιο πρόσφατη σταθερή έκδοση (ως Οκτώβριο 2026). Μετά το συγχρονισμό, μπορείτε να εισάγετε τις κλάσεις `org.jsoup` στα αρχεία πηγαίου κώδικα Java.

## Βήμα 2: Αναλύστε το έγγραφο HTML

Η ανάλυση του αρχείου είναι το πρώτο βήμα προς το **open links new tab**. Η μέθοδος `Jsoup.parse` διαβάζει το αρχείο σε μια μεταβλητή δομή τύπου DOM.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;

public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // Load the HTML document from disk
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");
        
        // Continue with link processing...
    }
}
```

*Γιατί είναι σημαντικό*: Το `Document` σας παρέχει επιλεκτές σε στυλ CSS, καθιστώντας εύκολο τον εντοπισμό των στοιχείων που χρειάζεστε.

## Βήμα 3: Βρείτε εξωτερικούς συνδέσμους

Τώρα εντοπίστε κάθε στοιχείο `<a>` που φέρει την κλάση `external`. Αυτό ταιριάζει με την απαίτηση **find external links**.

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

// Inside main after parsing:
Elements externalLinks = doc.select("a.external");
```

Το `Elements` είναι μια συλλογή των αντιστοιχούντων κόμβων. Αν ο επιλεκτής επιστρέψει ένα κενό σύνολο, το HTML σας είτε δεν έχει την κλάση είτε χρησιμοποιεί διαφορετική ονομασία—προσαρμόστε τον επιλεκτή αναλόγως.

## Βήμα 4: Προσθέστε `target="_blank"` σε κάθε σύνδεσμο

Για κάθε κόμβο που επιστρέφεται από το **find external links**, ορίστε το χαρακτηριστικό `target` σε `_blank`. Αυτό ικανοποιεί το βήμα **add target blank** και εξασφαλίζει ότι τα προγράμματα περιήγησης ανοίγουν το σύνδεσμο σε νέα καρτέλα.

```java
for (Element link : externalLinks) {
    link.attr("target", "_blank");
}
```

Η μέθοδος `attr` αντικαθιστά οποιαδήποτε υπάρχουσα τιμή `target`, εξασφαλίζοντας συνεπή συμπεριφορά σε όλα τα εξωτερικά άγκυρα.

## Βήμα 5: Αποθηκεύστε το τροποποιημένο HTML

Αφού ενημερώσετε το DOM, γράψτε τις αλλαγές πίσω σε ένα αρχείο. Αυτό ολοκληρώνει το τμήμα **save modified html** του οδηγού.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

// Still inside main:
Path output = Path.of("YOUR_DIRECTORY/updated.html");
Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
System.out.println("Updated file written to " + output);
```

Η `doc.outerHtml()` σειριοποιεί ολόκληρο το έγγραφο, διατηρώντας την εσοχή και τη μορφοποίηση όπως η jsoup το ανάλυσε αρχικά.

## Πλήρες λειτουργικό παράδειγμα

Συνδυάζοντας όλα τα βήματα δημιουργείται ένα αυτόνομο πρόγραμμα που μπορείτε να αντιγράψετε, επικολλήσετε και εκτελέσετε.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;

/**
 * Updates all external links so they open in a new tab.
 */
public class LinkUpdater {
    public static void main(String[] args) throws IOException {
        // 1️⃣ Parse the HTML file
        File input = new File("YOUR_DIRECTORY/sample.html");
        Document doc = Jsoup.parse(input, "UTF-8");

        // 2️⃣ Find external links (a.external)
        Elements externalLinks = doc.select("a.external");

        // 3️⃣ Add target="_blank" to each link
        for (Element link : externalLinks) {
            link.attr("target", "_blank");
        }

        // 4️⃣ Save the modified HTML
        Path output = Path.of("YOUR_DIRECTORY/updated.html");
        Files.writeString(output, doc.outerHtml(), StandardOpenOption.CREATE);
        System.out.println("Updated file written to " + output);
    }
}
```

### Αναμενόμενη έξοδος

Υποθέτουμε ότι το `sample.html` περιέχει:

```html
<a href="https://example.com" class="external">Example</a>
<a href="/internal/page.html">Internal</a>
```

Μετά την εκτέλεση του προγράμματος, το `updated.html` θα περιέχει:

```html
<a href="https://example.com" class="external" target="_blank">Example</a>
<a href="/internal/page.html">Internal</a>
```

Μόνο ο εξωτερικός σύνδεσμος έλαβε το χαρακτηριστικό `target="_blank"`, πράγμα που σημαίνει ότι τα προγράμματα περιήγησης θα το ανοίξουν τώρα σε νέα καρτέλα.

## Επαγγελματικές συμβουλές και κοινά προβλήματα

* **Pro tip:** Εάν χρειάζεται να θεωρήσετε συνδέσμους που ξεκινούν με `http://` ή `https://` ως εξωτερικούς ακόμη και χωρίς κλάση CSS, επεκτείνετε τον επιλεκτή: `doc.select("a[href^=http]")`.  
* **Edge case:** Κάποιες σελίδες ήδη καθορίζουν `target="_self"`; η κλήση `attr` το αντικαθιστά, εξασφαλίζοντας συνεπή συμπεριφορά.  
* **Performance:** Για πολύ μεγάλα αρχεία HTML, σκεφτείτε τη ροή ανάλυσης (`Jsoup.parse(File, String, String, Parser.htmlParser())`) για να μειώσετε τη χρήση μνήμης.  
* **Testing:** Επαληθεύστε το αποτέλεσμα ανοίγοντας το `updated.html` σε πρόγραμμα περιήγησης και εξετάζοντας το σύνδεσμο με τα εργαλεία προγραμματιστή—αναζητήστε το χαρακτηριστικό `target`.

## Συμπέρασμα

Τώρα έχετε μια πλήρη, εκτελέσιμη λύση για **open links in a new tab** χρησιμοποιώντας Java. Ο οδηγός κάλυψε πώς να **parse html in java**, **find external links**, **add target blank**, και **save modified html**, όλα με τη ελαφριά βιβλιοθήκη jsoup. 

Από εδώ μπορείτε:

* Επεκτείνετε τον επιλεκτή για να διαχειρίζεται άλλα μοτίβα συνδέσμων (π.χ., `rel="external"`).  
* Συνδυάστε αυτή τη λογική με ένα βήμα κατασκευής που επεξεργάζεται όλα τα αρχεία HTML σε ένα έργο.  
* Ενσωματώστε τον κώδικα σε μια μεγαλύτερη αλυσίδα διαχείρισης περιεχομένου.

Μη διστάσετε να πειραματιστείτε με διαφορετικούς επιλεκτές ή μορφές εξόδου, και να μοιραστείτε τα αποτελέσματά σας με την κοινότητα!

## Τι Θα Μάθετε Στη Σύντομη Επόμενη Φάση;

Τα παρακάτω tutorials καλύπτουν στενά σχετικό θέματα που βασίζονται στις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετες δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Πώς να χρησιμοποιήσετε CSS σε Java – Φόρτωση HTML, Καταμέτρηση Συνδέσμων & Αξιολόγηση XPath](/html/english/java/css-html-form-editing/how-to-use-css-in-java-load-html-count-links-evaluate-xpath/)
- [Πώς να Αναλύσετε HTML σε Java – Εξαγωγή Κειμένου από Άρθρα HTML](/html/english/java/creating-managing-html-documents/how-to-parse-html-in-java-extract-text-from-html-articles/)
- [Δημιουργία νέου στοιχείου html με Java – Πλήρης Οδηγός Aspose.HTML](/html/english/java/editing-html-documents/create-new-html-element-with-java-full-aspose-html-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}