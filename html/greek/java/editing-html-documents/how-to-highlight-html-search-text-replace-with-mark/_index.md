---
category: general
date: 2026-03-04
description: Πώς να επισημάνετε HTML αναζητώντας κείμενο στο HTML και τυλίγοντας κάθε
  αντιστοιχία με μια ετικέτα <mark>. Οδηγός Java βήμα‑βήμα για την αντικατάσταση κειμένου
  με στοιχεία <mark>.
draft: false
keywords:
- how to highlight html
- search text in html
- highlight word in html
- highlight occurrences of word
- replace text with mark
language: el
og_description: Πώς να επισημάνετε HTML αναζητώντας κείμενο στο HTML και τυλίγοντας
  τις αντιστοιχίες με ετικέτα <mark>. Πλήρες παράδειγμα Java για αντικατάσταση κειμένου
  με mark.
og_title: Πώς να επισημάνετε HTML – Αναζήτηση κειμένου & αντικατάσταση με <mark>
tags:
- Aspose.HTML
- Java
- Text Processing
title: Πώς να επισημάνετε HTML – Αναζήτηση κειμένου & αντικατάσταση με <mark>
url: /el/java/editing-html-documents/how-to-highlight-html-search-text-replace-with-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Επισημάνετε HTML – Αναζήτηση Κειμένου & Αντικατάσταση με `<mark>`

Έχετε αναρωτηθεί ποτέ **πώς να επισημάνετε HTML** όταν μια συγκεκριμένη λέξη εμφανίζεται πολλές φορές; Ίσως να δημιουργείτε έναν ιστότοπο τεκμηρίωσης, μια μηχανή blog, ή απλώς χρειάζεστε να τονίσετε ένα εμπορικό όνομα σε μια στατική σελίδα. Τα καλά νέα; Είναι αρκετά απλό μόλις ξέρετε πώς να αναζητήσετε κείμενο σε HTML και να τυλίξετε τα αποτελέσματα με ένα στοιχείο `<mark>`.

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα μια πλήρη λύση Java που φορτώνει ένα αρχείο HTML, αναζητά μια λέξη-στόχο, αντικαθιστά κάθε εμφάνιση με μια ετικέτα `<mark>` και τελικά αποθηκεύει την επισημασμένη έκδοση. Στο τέλος θα μπορείτε να **highlight word in HTML**, **highlight occurrences of word**, και ακόμη **replace text with mark** χωρίς να σπάσετε το περιβάλλον markup.

> **Τι θα χρειαστείτε**  
> • Java 17 ή νεότερη (ο κώδικας λειτουργεί και με παλαιότερες εκδόσεις)  
> • Βιβλιοθήκη Aspose.HTML for Java (δωρεάν δοκιμή ή αδειοδοτημένο αντίγραφο)  
> • Ένα απλό αρχείο HTML που θέλετε να επεξεργαστείτε  

Αν έχετε καλύψει αυτά τα βασικά, ας βουτήξουμε.

![Στιγμιότυπο οθόνης που δείχνει το επισημασμένο αποτέλεσμα HTML – πώς να επισημάνετε html](/images/highlight-html-example.png "how to highlight html example")

## Βήμα 1 – Φόρτωση του Εγγράφου HTML (How to Highlight HTML)

Πρώτα πρέπει να φορτώσουμε το αρχείο προέλευσης στη μνήμη. Η κλάση `Document` του Aspose.HTML κάνει όλη τη βαριά δουλειά, αναλύοντας το markup σε μια δομή τύπου DOM που μπορούμε να ερωτήσουμε.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Load the original HTML file
        Document document = new Document("YOUR_DIRECTORY/article.html");
```

**Γιατί είναι σημαντικό:** Η φόρτωση του εγγράφου μας παρέχει ένα καθαρό μοντέλο αντικειμένων, ώστε να μπορούμε να χειριζόμαστε με ασφάλεια τους κόμβους κειμένου χωρίς να ανησυχούμε για σπασμένα tags ή attributes. Επίσης, κανονικοποιεί τα κενά, κάτι που κάνει το επόμενο βήμα **search text in html** πιο αξιόπιστο.

## Βήμα 2 – Αναζήτηση Κειμένου σε HTML για τη Λέξη-Στόχο

Τώρα που το έγγραφο είναι έτοιμο, θα ψάξουμε για κάθε εμφάνιση της λέξης που θέλουμε να τονίσουμε. Η μέθοδος `searchText` επιστρέφει μια λίστα από αντικείμενα `TextMatch`, το καθένα περιγράφει πού βρίσκεται η αντιστοίχιση στο DOM.

```java
        // Define what we want to highlight
        String searchTerm = "Aspose";

        // Find all matches – this is the core of "search text in html"
        List<TextMatch> matches = document.searchText(searchTerm);
```

**Συμβουλή:** Η αναζήτηση είναι ευαίσθητη σε πεζά/κεφαλαία από προεπιλογή. Αν χρειάζεστε αναζήτηση χωρίς διάκριση πεζών/κεφαλαίων, μετατρέψτε τόσο το κείμενο του εγγράφου όσο και το `searchTerm` στο ίδιο case πριν καλέσετε το `searchText`, ή χρησιμοποιήστε μια προσέγγιση βασισμένη σε κανονικές εκφράσεις που παρέχεται από τη βιβλιοθήκη.

## Βήμα 3 – Αντικατάσταση Κειμένου με `<mark>` (Highlight Word in HTML)

Για κάθε αντιστοίχιση θα ανασυνθέσουμε το κείμενο του κόμβου που το περιέχει, ενσωματώνοντας ένα στοιχείο `<mark>` γύρω από την ακριβή λέξη. Αυτό εξασφαλίζει ότι επηρεάζουμε μόνο το κείμενο-στόχο και αφήνουμε το υπόλοιπο HTML ανέπαφο.

```java
        // Iterate over each match and wrap it with <mark>
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();

            // Preserve text before and after the match
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;

            // Replace the node's content with the new fragment
            parentNode.setTextContent(highlightedFragment);
        }
```

**Εξήγηση:**  
- `getStartOffset`/`getEndOffset` μας δίνουν τις ακριβείς θέσεις χαρακτήρων της αντιστοίχισης μέσα στον γονικό κόμβο.  
- Κόβοντας το αρχικό κείμενο (`textBefore` και `textAfter`) διατηρούμε τα υπόλοιπα ακριβώς όπως ήταν.  
- Η περιτύλιξη της αντιστοίχισης με `<mark>` είναι ο κανονικός τρόπος για **replace text with mark** και να αποκτήσετε εγγενή επισήμανση του προγράμματος περιήγησης χωρίς επιπλέον CSS.

### Περιπτώσεις Άκρων & Συμβουλές

- **Multiple matches in the same node:** Ο βρόχος επεξεργάζεται κάθε `TextMatch` διαδοχικά. Επειδή αντικαθιστούμε ολόκληρο το περιεχόμενο του κόμβου κάθε φορά, οι μεταγενέστερες θέσεις μετατοπίζονται. Το Aspose.HTML επιστρέφει τις αντιστοιχίσεις με τη σειρά του εγγράφου, έτσι η απλή αντικατάσταση λειτουργεί στις περισσότερες περιπτώσεις. Αν συναντήσετε επικαλυπτόμενες αντιστοιχίσεις, σκεφτείτε να συλλέξετε πρώτα όλες τις αντιστοιχίσεις και μετά να ξαναχτίσετε τον κόμβο σε μία διαδρομή.  
- **Elements that can’t contain raw HTML:** Αν ο γονικός κόμβος είναι ένα μπλοκ `<script>` ή `<style>`, η εισαγωγή `<mark>` θα σπάσει τη σελίδα. Μπορείτε να παραλείψετε αυτούς τους κόμβους ελέγχοντας το `parentNode.getNodeName()` πριν από την αντικατάσταση.

## Βήμα 4 – Αποθήκευση του Επισημασμένου Εγγράφου (Highlight Occurrences of Word)

Αφού ολοκληρωθούν όλες οι αντικαταστάσεις, αποθηκεύουμε το τροποποιημένο DOM ξανά στο δίσκο. Το αρχείο εξόδου θα περιέχει το αρχικό markup συν τα νέα tags `<mark>`, επισημαίνοντας αποτελεσματικά **highlighting occurrences of word** “Aspose”.

```java
        // Write the modified HTML back to a new file
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

Ανοίξτε το `highlighted.html` σε οποιοδήποτε πρόγραμμα περιήγησης, και θα δείτε κάθε “Aspose” τυλιγμένο σε ένα κίτρινο‑όπως φόντο (το προεπιλεγμένο στυλ για `<mark>`). Αν προτιμάτε προσαρμοσμένη εμφάνιση, προσθέστε έναν μικρό κανόνα CSS:

```html
<style>
    mark { background-color: #fffa8b; color: #000; }
</style>
```

## Συχνές Ερωτήσεις (Search Text in HTML – FAQs)

**Q: Τι γίνεται αν η λέξη εμφανίζεται μέσα σε τιμή attribute;**  
A: Το `searchText` εξετάζει μόνο το περιεχόμενο κειμένου των κόμβων, όχι τις συμβολοσειρές των attributes. Για να επισημάνετε τιμές attribute, θα πρέπει να επαναλάβετε τα στοιχεία και να ελέγξετε χειροκίνητα τα attributes.

**Q: Μπορώ να επισημάνω πολλαπλές διαφορετικές λέξεις σε μία εκτέλεση;**  
A: Απόλυτα. Δημιουργήστε μια λίστα όρων, επαναλάβετε για κάθε έναν, και εκτελέστε την ίδια λογική αντικατάστασης. Απλώς προσέξτε τις επικαλυπτόμενες αντιστοιχίσεις.

**Q: Λειτουργεί αυτό με tags που υπάρχουν μόνο σε HTML5 όπως `<section>` ή `<article>`;**  
A: Ναι. Το Aspose.HTML υποστηρίζει πλήρως τα σύγχρονα στοιχεία HTML5, έτσι η διέλευση του DOM λειτουργεί ανεξάρτητα από τον τύπο του tag.

## Πλήρες Παράδειγμα Εργασίας (All Steps Combined)

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα Java που δείχνει ολόκληρη τη ροή εργασίας — από τη φόρτωση του αρχείου μέχρι την αποθήκευση του επισημασμένου αποτελέσματος.

```java
import com.aspose.html.*;
import com.aspose.html.dom.*;
import java.util.List;

public class HighlightAspose {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document
        Document document = new Document("YOUR_DIRECTORY/article.html");

        // Step 2: Search for the word "Aspose"
        String searchTerm = "Aspose";
        List<TextMatch> matches = document.searchText(searchTerm);

        // Step 3: Wrap each found occurrence with a <mark> element
        for (TextMatch match : matches) {
            Node parentNode = match.getNode();
            String textBefore = parentNode.getTextContent()
                                          .substring(0, match.getStartOffset());
            String textAfter  = parentNode.getTextContent()
                                          .substring(match.getEndOffset());

            // Build the highlighted HTML fragment
            String highlightedFragment = textBefore
                    + "<mark>" + match.getText() + "</mark>"
                    + textAfter;
            parentNode.setTextContent(highlightedFragment);
        }

        // Step 4: Save the highlighted document
        document.save("YOUR_DIRECTORY/highlighted.html");
    }
}
```

**Αναμενόμενο αποτέλεσμα:** Ανοίξτε το `highlighted.html` και θα δείτε κάθε εμφάνιση του “Aspose” επισημασμένη. Κανένα άλλο τμήμα της σελίδας δεν τροποποιείται, και το αρχείο παραμένει έγκυρο έγγραφο HTML.

## Συμπέρασμα

Συζητήσαμε **how to highlight HTML** προγραμματιστικά **searching text in HTML**, τυλίγοντας κάθε αντιστοίχιση με μια ετικέτα `<mark>` και τελικά αποθηκεύοντας τις αλλαγές. Αυτή η προσέγγιση σας επιτρέπει να **highlight word in HTML**, **highlight occurrences of word**, και **replace text with mark** χωρίς να γράφετε ευαίσθητο κώδικα χειρισμού συμβολοσειρών.

Επόμενα βήματα; Δοκιμάστε να επεκτείνετε το script για:

- Να δέχεται τη λέξη-κλειδί ως όρισμα γραμμής εντολών.  
- Να δημιουργεί ένα αρχείο CSS που ορίζει προσαρμοσμένο χρώμα επισήμανσης.  
- Να επεξεργάζεται ολόκληρο φάκελο αρχείων HTML σε μία παρτίδα.  

Αυτές οι παραλλαγές θα ενισχύσουν την κατανόησή σας τόσο του Aspose.HTML API όσο και των γενικών προτύπων επεξεργασίας κειμένου.

Αν αντιμετωπίσετε δυσκολίες ή έχετε ιδέες για περαιτέρω βελτιώσεις, αφήστε ένα σχόλιο παρακάτω. Καλή επισήμανση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}