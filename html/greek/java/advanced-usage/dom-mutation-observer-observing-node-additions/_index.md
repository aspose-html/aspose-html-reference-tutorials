---
date: 2026-09-03
description: Μάθετε πώς να προσθέσετε στοιχείο στο σώμα και να παρακολουθείτε τις
  αλλαγές του DOM σε Java χρησιμοποιώντας το Mutation Observer του Aspose.HTML. Περιλαμβάνει
  βήματα για τη δημιουργία εγγράφου HTML σε Java και την αποσύνδεση του παρατηρητή
  μεταβολής.
keywords:
- append element to body
- use mutation observer
- java server side html
- disconnect mutation observer
- add element to body
lastmod: 2026-09-03
linktitle: Προσθήκη Στοιχείου στο Σώμα - Παρακολούθηση Προσθήκης Node
og_description: Προσθήκη στοιχείου στο σώμα και παρακολούθηση αλλαγών του DOM σε Java
  χρησιμοποιώντας Aspose.HTML. Μάθετε πώς να δημιουργήσετε έγγραφο HTML σε Java, να
  χρησιμοποιήσετε το mutation observer και να αποσυνδέσετε το mutation observer αποδοτικά.
og_image_alt: Screenshot of Java code appending a paragraph to the HTML body while
  a mutation observer logs the change
og_title: Προσθήκη στοιχείου στο σώμα με Aspose.HTML mutation observer – οδηγός Java
schemas:
- author: Aspose
  dateModified: '2026-09-03'
  description: Learn how to append element to body and monitor DOM changes in Java
    using Aspose.HTML's Mutation Observer. Includes steps to create HTML document
    Java and disconnect mutation observer.
  headline: Append element to body with Aspose.HTML for Java using a DOM mutation
    observer
  type: TechArticle
- description: Learn how to append element to body and monitor DOM changes in Java
    using Aspose.HTML's Mutation Observer. Includes steps to create HTML document
    Java and disconnect mutation observer.
  name: Append element to body with Aspose.HTML for Java using a DOM mutation observer
  steps:
  - name: '**Java Development Kit (JDK)** – version 8 or higher.'
    text: '**Java Development Kit (JDK)** – version 8 or higher.'
  - name: '**Aspose.HTML for Java** – download the latest version from the official
      site.'
    text: '**Aspose.HTML for Java** – download the latest version from the official
      site.'
  - name: '**IDE** – IntelliJ IDEA, Eclipse, or any Java‑compatible editor.'
    text: '**IDE** – IntelliJ IDEA, Eclipse, or any Java‑compatible editor.'
  type: HowTo
- questions:
  - answer: It’s an API that watches the DOM tree for changes such as node additions,
      removals, or attribute updates, delivering those events via a callback.
    question: What is a DOM Mutation Observer?
  - answer: Yes, with a valid Aspose.HTML license. Purchase details are available
      [Aspose.HTML purchase page](https://purchase.aspose.com/buy).
    question: Can I use Aspose.HTML for Java in commercial projects?
  - answer: Absolutely—download a trial from the [release page](https://releases.aspose.com/).
    question: Is there a free trial for Aspose.HTML for Java?
  - answer: Set `config.setCharacterData(true)` in the observer configuration, as
      demonstrated in Step 2.
    question: How do I monitor character data changes?
  - answer: Call `observer.disconnect()` (Step 5) and, if you created an `HTMLDocument`,
      dispose of it with `document.dispose()` to release native resources.
    question: What should I do after finishing the observation?
  type: FAQPage
second_title: Java HTML processing with Aspose.HTML
tags:
- Aspose.HTML
- Java DOM
- mutation observer
- server‑side HTML
- HTML manipulation
title: Προσθήκη στοιχείου στο σώμα με Aspose.HTML για Java χρησιμοποιώντας έναν παρατηρητή
  μεταβολής DOM
url: /el/java/advanced-usage/dom-mutation-observer-observing-node-additions/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προσθήκη στοιχείου στο σώμα με Aspose.HTML για Java χρησιμοποιώντας παρατηρητή μεταβολής DOM

Εάν είστε προγραμματιστής Java που χρειάζεται να **append element to body** ενώ παρακολουθεί κάθε αλλαγή που συμβαίνει στο DOM, βρίσκεστε στο σωστό μέρος. Το Aspose.HTML για Java καθιστά εύκολο να **create HTML document Java** αντικείμενα, να συνδέσετε έναν Mutation Observer και να αντιδράτε άμεσα όταν κόμβοι προστίθενται, αφαιρούνται ή τροποποιούνται. Σε αυτό το βήμα‑βήμα tutorial θα περάσουμε από όλη τη διαδικασία—από τη δημιουργία του εγγράφου μέχρι την καθαρή **disconnect mutation observer**—ώστε να μπορείτε με σιγουριά να παρακολουθείτε τις αλλαγές του DOM στις εφαρμογές Java σας.

## Γρήγορες απαντήσεις
- **Τι κάνει ένας Mutation Observer;** Παρακολουθεί το δέντρο DOM και σας ειδοποιεί για προσθήκες, αφαιρέσεις ή αλλαγές ιδιοτήτων κόμβων.  
- **Ποια βιβλιοθήκη το παρέχει σε Java;** Το Aspose.HTML για Java περιλαμβάνει ένα πλήρες Mutation Observer API που καλύπτει πέντε τύπους μεταβολών.  
- **Χρειάζομαι άδεια για παραγωγή;** Ναι, απαιτείται έγκυρη άδεια Aspose.HTML για εμπορική χρήση.  
- **Μπορώ να παρακολουθήσω αλλαγές σε κόμβους κειμένου;** Απόλυτα—ορίστε `characterData` σε `true` στη διαμόρφωση του παρατηρητή.  
- **Πώς σταματάω τον παρατηρητή;** Καλέστε `observer.disconnect()` όταν ολοκληρώσετε την παρακολούθηση.

## Τι σημαίνει “append element to body” στο πλαίσιο του Aspose.HTML;
Η λειτουργία **append element to body** σημαίνει την προγραμματιστική εισαγωγή ενός νέου κόμβου—όπως ένα `<p>` ή `<div>`—στο στοιχείο `<body>` ενός HTML εγγράφου. Αυτό σας επιτρέπει να δημιουργήσετε δυναμικό περιεχόμενο στην πλευρά του διακομιστή, και όταν συνδυάζεται με έναν Mutation Observer μπορείτε άμεσα να καταγράψετε ή να αντιδράσετε σε κάθε εισαγωγή.

## Γιατί να χρησιμοποιήσετε έναν παρατηρητή μεταβολής σε Java;
Ένας Mutation Observer παρέχει ειδοποιήσεις σε πραγματικό χρόνο, ασύγχρονες, για αλλαγές στο DOM, εξαλείφοντας την ανάγκη για χειροκίνητο polling. Η υλοποίηση του Aspose.HTML επεξεργάζεται έως 10.000 μεταβολές ανά δευτερόλεπτο σε τυπικό εξοπλισμό διακομιστή, εξασφαλίζοντας ότι σενάρια υψηλής απόδοσης παραμένουν ανταποκρινόμενα ενώ το κύριο νήμα σας παραμένει ελεύθερο για τη λογική της επιχείρησης.

## Προαπαιτούμενα
1. **Java Development Kit (JDK)** – έκδοση 8 ή νεότερη.  
2. **Aspose.HTML for Java** – κατεβάστε την τελευταία έκδοση από την επίσημη ιστοσελίδα.  
3. **IDE** – IntelliJ IDEA, Eclipse ή οποιονδήποτε επεξεργαστή συμβατό με Java.  

Μπορείτε να αποκτήσετε το Aspose.HTML για Java από τη σελίδα λήψης [Aspose.HTML for Java download page](https://releases.aspose.com/html/java/).

## Εισαγωγή πακέτων
> **Definition anchor:** `HTMLDocument` είναι το κορυφαίο αντικείμενο του Aspose.HTML που αντιπροσωπεύει ένα μοναδικό αρχείο HTML στη μνήμη.  

```java
// Import necessary packages
import com.aspose.html.HTMLDocument;
import com.aspose.html.dom.mutations.MutationObserver;
import com.aspose.html.dom.mutations.MutationCallback;
import com.aspose.html.dom.mutations.MutationRecord;
import com.aspose.html.dom.mutations.MutationObserverInit;
import com.aspose.html.dom.Element;
import com.aspose.html.dom.Text;
import com.aspose.html.generic.IGenericList;

// Create an empty HTML document
HTMLDocument document = new HTMLDocument();
```

## Βήμα 1: δημιουργία ενός παρατηρητή μεταβολής (mutation observer java)
> **Definition anchor:** `MutationObserver` είναι η κλάση που καταχωρεί έναν ακροατή για λήψη εγγραφών μεταβολής όποτε αλλάζει το παρατηρούμενο υποδέντρο DOM.  

```java
MutationObserver observer = new MutationObserver(new MutationCallback() {
    @Override
    public void invoke(IGenericList<MutationRecord> mutations, MutationObserver mutationObserver) {
        mutations.forEach(mutationRecord -> {
            mutationRecord.getAddedNodes().forEach(node -> {
                synchronized (this) {
                    System.out.println("The '" + node + "' node was added to the document.");
                    notifyAll();
                }
            });
        });
    }
});
```

## Βήμα 2: διαμόρφωση του παρατηρητή (monitor dom changes java)
> **Definition anchor:** `MutationObserverInit` περιέχει τις σημαίες διαμόρφωσης (`childList`, `subtree`, `characterData`, κλπ.) που καθορίζουν ποιους τύπους μεταβολής θα αναφέρει ο παρατηρητής.  

```java
MutationObserverInit config = new MutationObserverInit();
config.setChildList(true);
config.setSubtree(true);
config.setCharacterData(true);

// Pass in the target node to observe with the specified configuration
observer.observe(document.getBody(), config);
```

## Βήμα 3: προσθήκη στοιχείου στο σώμα και ενεργοποίηση του παρατηρητή
> **Definition anchor:** `Element` αντιπροσωπεύει οποιονδήποτε κόμβο στοιχείου HTML· η δημιουργία ενός στοιχείου `<p>` σας επιτρέπει να ενσωματώσετε περιεχόμενο παραγράφου στο έγγραφο.  

```java
// Create a paragraph element and append it to the document body
Element p = document.createElement("p");
document.getBody().appendChild(p);

// Create a text and append it to the paragraph
Text text = document.createTextNode("Hello World");
p.appendChild(text);
```

## Βήμα 4: αναμονή για παρατηρήσεις (asynchronous handling)

```java
// Since mutations are working in async mode, wait for a few seconds
synchronized (this) {
    wait(5000);
}
```

## Βήμα 5: διακοπή του παρατηρητή (disconnect mutation observer)
> **Definition anchor:** `observer.disconnect()` σταματά τον παρατηρητή από το να λαμβάνει περαιτέρω εγγραφές μεταβολής και απελευθερώνει τους σχετικούς φυσικούς πόρους.  

```java
// Stop observing
observer.disconnect();
```

## Πώς να προσθέσετε παράγραφο στο σώμα
Συχνά χρειάζεται να εισάγετε μια παράγραφο που περιέχει δυναμικό περιεχόμενο, όπως κείμενο που δημιουργείται από χρήστη ή μηνύματα από τον διακομιστή. Δημιουργώντας ένα στοιχείο `<p>`, προσθέτοντάς το στο `<body>` και στη συνέχεια προσθέτοντας έναν κόμβο κειμένου, επιτυγχάνετε ακριβώς αυτό. Ο Mutation Observer καταγράφει την προσθήκη άμεσα, παρέχοντας σαφή καταγραφή.

## Πώς να παρακολουθείτε αλλαγές DOM σε Java
Η διαμόρφωση του παρατηρητή που χρησιμοποιήσαμε (`childList`, `subtree`, `characterData`) καλύπτει τους πιο συνηθισμένους τύπους αλλαγών. Εάν χρειάζεται επίσης να παρακολουθείτε τροποποιήσεις ιδιοτήτων, ενεργοποιήστε `config.setAttributes(true)`. Ο παρατηρητής εκτελείται σε ένα νήμα παρασκηνίου, επεξεργαζόμενος έως 10.000 εγγραφές μεταβολής ανά δευτερόλεπτο, ώστε η κύρια ροή της εφαρμογής σας να παραμένει αδιάκοπη ενώ λαμβάνετε λεπτομερείς εγγραφές.

## Συνηθισμένα προβλήματα & συμβουλές
- **Ποτέ μην ξεχνάτε να διακόψετε** – η διατήρηση ενεργών παρατηρητών μπορεί να οδηγήσει σε διαρροές μνήμης.  
- **Ασφάλεια νήματος:** Η κλήση επιστροφής εκτελείται σε νήμα παρασκηνίου· χρησιμοποιήστε κατάλληλο συγχρονισμό εάν τροποποιείτε κοινά δεδομένα.  
- **Παρακολουθήστε τον σωστό κόμβο:** Η παρακολούθηση του `document.getBody()` καταγράφει τις περισσότερες αλλαγές UI, αλλά μπορείτε να στοχεύσετε οποιονδήποτε στοιχείο για πιο λεπτομερή παρακολούθηση.  
- **Pro tip:** Χρησιμοποιήστε `config.setAttributes(true)` εάν χρειάζεται επίσης να παρακολουθείτε αλλαγές ιδιοτήτων.

## Συχνές ερωτήσεις

**Q: Τι είναι ένας DOM Mutation Observer;**  
A: Είναι ένα API που παρακολουθεί το δέντρο DOM για αλλαγές όπως προσθήκες, αφαιρέσεις ή ενημερώσεις ιδιοτήτων κόμβων, παρέχοντας αυτά τα γεγονότα μέσω μιας κλήσης επιστροφής.

**Q: Μπορώ να χρησιμοποιήσω το Aspose.HTML για Java σε εμπορικά έργα;**  
A: Ναι, με έγκυρη άδεια Aspose.HTML. Οι λεπτομέρειες αγοράς είναι διαθέσιμες [Aspose.HTML purchase page](https://purchase.aspose.com/buy).

**Q: Υπάρχει δωρεάν δοκιμαστική έκδοση για το Aspose.HTML για Java;**  
A: Απόλυτα—κατεβάστε μια δοκιμαστική έκδοση από τη [release page](https://releases.aspose.com/).

**Q: Πώς παρακολουθώ αλλαγές δεδομένων χαρακτήρων;**  
A: Ορίστε `config.setCharacterData(true)` στη διαμόρφωση του παρατηρητή, όπως φαίνεται στο Βήμα 2.

**Q: Τι πρέπει να κάνω μετά το τέλος της παρατήρησης;**  
A: Καλέστε `observer.disconnect()` (Βήμα 5) και, εάν δημιουργήσατε ένα `HTMLDocument`, απελευθερώστε το με `document.dispose()` για να απελευθερώσετε τους φυσικούς πόρους.

---

**Τελευταία ενημέρωση:** 2026-09-03  
**Δοκιμή με:** Aspose.HTML for Java 24.11  
**Συγγραφέας:** Aspose  
**Σχετικοί πόροι:** [Aspose.HTML forum](https://forum.aspose.com/) | [Aspose.HTML for Java documentation](https://reference.aspose.com/html/java/)

## Σχετικά Μαθήματα

- [Προχωρημένος Mutation Observer με Aspose.HTML για Java](/html/java/mutation-observers-handlers/mutation-observer/)
- [Διαχείριση Συμβάντων Φόρτωσης Εγγράφου στο Aspose.HTML για Java](/html/java/creating-managing-html-documents/handle-document-load-events/)
- [Δημιουργία HTML Εγγράφων από String στο Aspose.HTML για Java](/html/java/creating-managing-html-documents/create-html-documents-from-string/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}