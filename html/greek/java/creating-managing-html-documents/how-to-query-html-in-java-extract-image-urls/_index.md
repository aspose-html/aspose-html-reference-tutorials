---
category: general
date: 2026-03-05
description: Πώς να κάνετε ερώτημα HTML σε Java για να διαβάσετε ένα αρχείο HTML και
  να εξάγετε εικόνες. Μάθετε πώς να διαβάζετε αρχείο HTML με Java, να λαμβάνετε URLs
  εικόνων με Java και να επαναλαμβάνετε το NodeList με Java.
draft: false
keywords:
- how to query html
- read html file java
- how to extract images
- iterate over nodelist java
- get image urls java
language: el
og_description: Πώς να κάνετε ερωτήματα σε HTML με Java και να ανακτήσετε URLs εικόνων.
  Αυτός ο οδηγός δείχνει πώς να διαβάσετε αρχείο HTML σε Java, να εντοπίσετε εικόνες
  και να επαναλάβετε το NodeList σε Java.
og_title: Πώς να κάνετε ερωτήματα σε HTML με Java – Εξαγωγή URL εικόνων
tags:
- html parsing
- java
- aspose-html
- xpath
- css selector
title: Πώς να ερωτήσετε HTML σε Java – Εξαγωγή URL εικόνων
url: /el/java/creating-managing-html-documents/how-to-query-html-in-java-extract-image-urls/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Αναζητήσετε HTML σε Java – Εξαγωγή URLs Εικόνων

Έχετε αναρωτηθεί ποτέ **πώς να αναζητήσετε HTML** σε Java για να εξάγετε κάθε εικόνα από μια σελίδα; Δεν είστε οι μόνοι—οι προγραμματιστές χρειάζονται συνεχώς να διαβάζουν αρχεία HTML, να «σκάβουν» εικόνες και στη συνέχεια να κάνουν κάτι χρήσιμο με τα URLs. Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει ακριβώς **πώς να αναζητήσετε HTML**, να διαβάσετε ένα αρχείο HTML με στυλ Java και να λάβετε URLs εικόνων με τρόπο Java‑wise.

Θα χρησιμοποιήσουμε το Aspose.HTML for Java, αλλά οι έννοιες—XPath, CSS selectors, και η επανάληψη πάνω σε ένα `NodeList`—εφαρμόζονται σε οποιαδήποτε βιβλιοθήκη DOM. Στο τέλος αυτού του οδηγού θα είστε άνετοι με **πώς να εξάγετε εικόνες**, θα ξέρετε πώς να **επανεξετάζετε NodeList Java**, και θα έχετε ένα έτοιμο‑για‑εκτέλεση απόσπασμα κώδικα που μπορείτε να ενσωματώσετε στο πρόγραμμά σας.

![How to query HTML in Java example](https://example.com/placeholder.png "Πώς να αναζητήσετε HTML σε Java")

---

## Τι Θα Μάθετε

- Φόρτωση ενός εγγράφου HTML από δίσκο (read HTML file Java)  
- Εντοπισμός ετικετών `<img>` χρησιμοποιώντας τόσο XPath όσο και CSS selectors (how to extract images)  
- Επανάληψη πάνω στο προκύπτον `NodeList` (iterate over NodeList Java)  
- Εκτύπωση του χαρακτηριστικού `src` κάθε εικόνας (get image URLs Java)

Χωρίς εξωτερικές υπηρεσίες, χωρίς σύνθετα εργαλεία κατασκευής—μόνο καθαρή Java και μια εξάρτηση Maven.

---

## Προαπαιτούμενα

- Java 8 ή νεότερη εγκατεστημένη  
- Maven ή Gradle για διαχείριση εξαρτήσεων  
- Βασική εξοικείωση με τη δομή του HTML  
- Προαιρετικό αλλά χρήσιμο: ένα απλό αρχείο HTML (`sample.html`) που περιέχει κάποια στοιχεία `<figure><img …></figure>`

Αν έχετε όλα αυτά, μπορούμε να ξεκινήσουμε αμέσως.

---

## Βήμα 1: Read HTML File Java – Φόρτωση του Εγγράφου

Πρώτο πράγμα: πρέπει να φέρουμε το HTML στη μνήμη. Η κλάση `HTMLDocument` του Aspose.HTML κάνει το σκληρό κομμάτι. Σκεφτείτε το σαν το άνοιγμα ενός βιβλίου ώστε να μπορείτε να γυρίσετε σε οποιαδήποτε σελίδα.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.NodeList;
import com.aspose.html.dom.Element;

/**
 * Demonstrates how to query HTML in Java and extract image URLs.
 */
public class QueryExample {
    public static void main(String[] args) throws Exception {

        // ① Load the HTML document from a local file.
        // Replace "YOUR_DIRECTORY/sample.html" with the actual path.
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/sample.html");
```

**Γιατί είναι σημαντικό:** Η φόρτωση του αρχείου σας δίνει ένα δέντρο DOM που μπορείτε να ερωτήσετε. Αν η διαδρομή είναι λανθασμένη, θα λάβετε `FileNotFoundException`, γι’ αυτό ελέγξτε ξανά τη θέση πριν τρέξετε.

---

## Βήμα 2: Εντοπισμός Εικόνων με XPath – Πώς να Εξάγετε Εικόνες

Το XPath είναι μια ισχυρή γλώσσα ερωτημάτων που σας επιτρέπει να εντοπίζετε κόμβους με ακρίβεια λέιζερ. Εδώ ζητάμε κάθε `<img>` μέσα σε ένα `<figure>` που επίσης έχει χαρακτηριστικό `alt`.

```java
        // ② Use XPath to find <img> elements that have an "alt" attribute.
        NodeList xpathImages = document.evaluateXPath("//figure/img[@alt]");
        System.out.println("XPath found " + xpathImages.getLength() + " images.");
```

**Γιατί XPath;** Είναι σύντομο και λειτουργεί ακόμη και όταν το HTML είναι ακατάστατο. Η έκφραση `//figure/img[@alt]` μεταφράζεται σε: «οποιοδήποτε `<img>` κάτω από ένα `<figure>` που φέρει χαρακτηριστικό `alt`». Αν χρειαστεί να φιλτράρετε με άλλα χαρακτηριστικά, απλώς τροποποιήστε τις αγκύλες.

---

## Βήμα 3: Εντοπισμός Εικόνων με CSS Selector – Εναλλακτικός Τρόπος για Εξαγωγή Εικόνων

Μερικές φορές προτιμάτε τη σύνταξη CSS επειδή αντικατοπτρίζει αυτό που γράφετε σε φύλλα στυλ. Η `querySelectorAll` δέχεται τον ίδιο selector που θα χρησιμοποιούσατε σε έναν περιηγητή.

```java
        // ③ Same query using a CSS selector.
        NodeList cssImages = document.querySelectorAll("figure img[alt]");
        System.out.println("CSS selector found " + cssImages.getLength() + " images.");
```

**Γιατί και τα δύο;** Η παρουσία και των δύο δείχνει ότι μπορείτε να επιλέξετε το εργαλείο που σας βολεύει περισσότερο. Στην πράξη θα χρησιμοποιήσετε ένα από τα δύο, αλλά η ύπαρξη και των δύο παραδειγμάτων κάνει το tutorial πιο ολοκληρωμένο.

---

## Βήμα 4: Iterate Over NodeList Java – Λήψη URLs Εικόνων Java

Τώρα που έχουμε μια συλλογή, πρέπει να την περάσουμε. Εδώ μπαίνει η **iterate over NodeList Java**. Θα εξάγουμε το χαρακτηριστικό `src` κάθε εικόνας και θα το εκτυπώσουμε.

```java
        // ④ Loop through the NodeList returned by the CSS query.
        for (int i = 0; i < cssImages.getLength(); i++) {
            Element imageElement = (Element) cssImages.item(i);
            // Extract the "src" attribute – that’s the image URL.
            System.out.println("Image src: " + imageElement.getAttribute("src"));
        }
    }
}
```

**Γιατί κλασικός βρόχος `for`;** Το `NodeList` του Aspose δεν υλοποιεί το `Iterable`, οπότε η σύνταξη `for‑each` δεν θα μεταγλωττιστεί. Η χρήση βρόχου με δείκτη είναι ο αξιόπιστος τρόπος για **iterate over NodeList Java**.

---

## Αναμενόμενο Αποτέλεσμα

Τρέχοντας το πρόγραμμα έναντι ενός δείγματος HTML όπως:

```html
<figure>
    <img src="images/pic1.jpg" alt="First picture">
</figure>
<figure>
    <img src="images/pic2.png" alt="Second picture">
</figure>
```

Θα παραχθεί κάτι παρόμοιο με:

```
XPath found 2 images.
CSS selector found 2 images.
Image src: images/pic1.jpg
Image src: images/pic2.png
```

Αν το αρχείο σας περιέχει περισσότερες ετικέτες `<img>` που ικανοποιούν τα κριτήρια, οι αριθμοί θα αυξηθούν αντίστοιχα.

---

## Συνηθισμένα Προβλήματα & Pro Tips

- **Θέματα διαδρομής αρχείου:** Χρησιμοποιήστε απόλυτη διαδρομή ή τοποθετήστε το `sample.html` σχετικό με τον τρέχοντα φάκελο εργασίας του έργου σας.  
- **Απουσία χαρακτηριστικού `alt`:** Τα ερωτήματα XPath/CSS μας φιλτράρουν με `[@alt]`. Αν χρειάζεστε *όλες* τις εικόνες, αφαιρέστε το φίλτρο (`//figure/img` ή `figure img`).  
- **Απόδοση:** Για τεράστια έγγραφα, σκεφτείτε streaming parsers, αλλά για τις περισσότερες εργασίες web‑scraping η προσέγγιση DOM είναι επαρκής.  
- **Προβλήματα κωδικοποίησης:** Το Aspose.HTML σέβεται το charset που δηλώνεται στο HTML. Αν δείτε ακατανόητους χαρακτήρες, βεβαιωθείτε ότι το αρχείο είναι αποθηκευμένο ως UTF‑8.  

---

## Επέκταση του Παραδείγματος

Τώρα που μπορείτε να **λάβετε URLs εικόνων Java**, ίσως θελήσετε να:

1. **Κατεβάσετε τις εικόνες** χρησιμοποιώντας `java.net.URL` και `Files.copy`.  
2. **Αποθηκεύσετε τα URLs σε βάση δεδομένων** για μετέπειτα επεξεργασία.  
3. **Φιλτράρετε κατά επέκταση αρχείου** (`src.endsWith(".png")`).  

Όλα αυτά είναι απλές επεκτάσεις του βρόχου που φαίνεται στο Βήμα 4.

---

## Συμπέρασμα

Σε αυτόν τον οδηγό καλύψαμε **πώς να αναζητήσετε HTML** σε Java από την αρχή μέχρι το τέλος: φόρτωση του αρχείου, εντοπισμός εικόνων με XPath και CSS selectors, και **iterate over NodeList Java** για εκτύπωση του `src` κάθε εικόνας. Τώρα έχετε μια σταθερή βάση για **πώς να εξάγετε εικόνες**, και ξέρετε ακριβώς **πώς να διαβάσετε αρχείο HTML Java** χρησιμοποιώντας το Aspose.HTML.

Μη διστάσετε να προσαρμόσετε τον κώδικα στις δικές σας ανάγκες scraping—είτε πρόκειται για εξαγωγή άλλων χαρακτηριστικών, διαχείριση ετικετών `<a>`, ή τροφοδοσία των URLs σε downloader. Το μοτίβο παραμένει το ίδιο: φόρτωση, ερώτημα, επανάληψη, και δράση.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε ένα ενδιαφέρον use‑case; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}