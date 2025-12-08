---
date: 2025-12-08
description: Μάθετε πώς να μετατρέπετε HTML σε PNG με το Aspose.HTML for Java, ενώ
  διαχειρίζεστε σπασμένους συνδέσμους και εντοπίζετε ελλείποντες πόρους χρησιμοποιώντας
  προσαρμοσμένους χειριστές μηνυμάτων.
language: el
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Πώς να μετατρέψετε HTML σε PNG και να χρησιμοποιήσετε διαχειριστές μηνυμάτων
  στο Aspose.HTML για Java
url: /java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή HTML σε PNG με Aspose.HTML για Java – Χρήση Message Handlers

## Introduction  
Σε αυτό το tutorial θα μάθετε **πώς να μετατρέψετε HTML σε PNG** χρησιμοποιώντας Aspose.HTML για Java και, ταυτόχρονα, **πώς να διαχειριστείτε σπασμένους συνδέσμους** ή ελλιπείς πόρους με έναν προσαρμοσμένο message handler. Θα περάσουμε από τη δημιουργία ενός απλού αρχείου HTML, τη γραφή του στο δίσκο, τη φόρτωσή του και την αντιμετώπιση τυχόν σφαλμάτων δικτύου—ιδανικό για προγραμματιστές που χρειάζονται αξιόπιστη **μετατροπή html σε εικόνα** σε εφαρμογές Java επιπέδου παραγωγής.

## Quick Answers
- **Τι καλύπτει το tutorial;** Μετατροπή HTML σε PNG και διαχείριση ελλιπών πόρων με ένα message handler.  
- **Ποια βιβλιοθήκη χρησιμοποιείται;** Aspose.HTML for Java.  
- **Χρειάζομαι άδεια;** Συνιστάται προσωρινή άδεια για δοκιμαστικές εκδόσεις.  
- **Μπορώ να γράψω το αρχείο HTML από Java;** Ναι – δείτε το βήμα «write html file java».  
- **Θα εντοπίσει ο handler σπασμένους συνδέσμους;** Απόλυτα· καταγράφει οποιεσδήποτε απαντήσεις μη‑200.

## What is a Message Handler in Aspose.HTML?  
Ένας message handler είναι ένα hook στο network stack που σας επιτρέπει να **πιάσετε ελλιπείς πόρους** (όπως ένα σπασμένο URL εικόνας) πριν προκαλέσουν εξαίρεση. Εξετάζοντας τον κωδικό κατάστασης της απάντησης, μπορείτε να καταγράψετε, να αντικαταστήσετε ή να επαναλάβετε το αίτημα—παρέχοντάς σας πλήρη έλεγχο των δικτυακών λειτουργιών.

## Why Convert HTML to PNG?  
Η μετατροπή HTML σε εικόνα είναι χρήσιμη για τη δημιουργία μικρογραφιών, προεπισκοπήσεων email ή στιγμιότυπων τύπου PDF όταν δεν χρειάζεστε πλήρη μετατροπή PDF. Το Aspose.HTML παρέχει μια γρήγορη, server‑side **μετατροπή html σε εικόνα** μηχανή που λειτουργεί χωρίς πρόγραμμα περιήγησης.

## Prerequisites
1. **Java Development Kit (JDK)** – κατεβάστε από το [ιστότοπο Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – αποκτήστε τα τελευταία JAR από τη [σελίδα κυκλοφοριών Aspose](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse ή NetBeans.  
4. **Βασικές γνώσεις Java** – θα πρέπει να είστε άνετοι με το try‑with‑resources και την απελευθέρωση αντικειμένων.  
5. **Προσωρινή άδεια** (προαιρετικό) – αποφύγετε τους περιορισμούς δοκιμής μέσω μιας [προσωρινής άδειας](https://purchase.aspose.com/temporary-license/).

## Import Packages
Before we begin, import the required Java classes:

```java
import java.io.IOException;
```

These imports give us access to file I/O and the Aspose.HTML networking APIs.

## Step 1: Write the HTML File (write html file java)  
First, create a tiny HTML snippet that references an image that **does not exist**. This will let us test the handler.

```java
String code = "<img src='missing.jpg'>";
```

## Step 2: Persist the HTML to Disk  
Save the snippet to a file called `document.html`. This file will later be loaded with the Aspose.HTML engine.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Step 3: Create a Custom Message Handler (catch missing resource)  
Now we define a handler that checks the HTTP status code. If it isn’t `200`, we log a friendly message.

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

## Step 4: Register the Handler with the Network Service  
Add the custom handler to Aspose.HTML’s network service so it participates in every request.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Step 5: Load the HTML Document (load html document java)  
With the configuration ready, load the HTML file. The missing image will trigger the handler we just added.

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

## Step 6: Convert HTML to PNG (convert html to png)  
Finally, convert the loaded document to a PNG image. This demonstrates the full **html to image conversion** workflow.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Step 7: Clean Up Resources  
Always dispose of the `Configuration` object to free native resources and avoid memory leaks.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Common Pitfalls & Tips
- **Recursive invoke call:** Ο προσαρμοσμένος handler πρέπει να καλέσει `invoke(context);` *μετά* τη λογική σας για να συνεχίσει την αλυσίδα. Η παράλειψη μπορεί να σταματήσει άλλους handlers.  
- **Missing license warnings:** Χωρίς έγκυρη άδεια, η μετατροπή μπορεί να προσθέσει υδατογράφημα ή να περιορίσει το μέγεθος εξόδου.  
- **Path issues:** Βεβαιωθείτε ότι το `document.html` γράφεται στον τρέχοντα φάκελο εργασίας ή δώστε απόλυτη διαδρομή.  

## Frequently Asked Questions

**Q: What is Aspose.HTML for Java?**  
A: It’s a robust library that lets Java developers create, manipulate, and convert HTML documents without a browser.

**Ε: Τι είναι το Aspose.HTML για Java;**  
Α: Είναι μια ισχυρή βιβλιοθήκη που επιτρέπει σε προγραμματιστές Java να δημιουργούν, να χειρίζονται και να μετατρέπουν έγγραφα HTML χωρίς πρόγραμμα περιήγησης.

**Q: Why use message handlers in Aspose.HTML for Java?**  
A: They let you **handle broken links**, log missing resources, or modify requests/responses on the fly.

**Ε: Γιατί να χρησιμοποιήσετε message handlers στο Aspose.HTML για Java;**  
Α: Σας επιτρέπουν να **διαχειρίζεστε σπασμένους συνδέσμους**, να καταγράφετε ελλιπείς πόρους ή να τροποποιείτε αιτήματα/απαντήσεις άμεσα.

**Q: Can I chain multiple message handlers?**  
A: Yes—add each handler to the `network.getMessageHandlers()` list; they execute in the order added.

**Ε: Μπορώ να αλυσίδω πολλαπλούς message handlers;**  
Α: Ναι—προσθέστε κάθε handler στη λίστα `network.getMessageHandlers()`· εκτελούνται με τη σειρά που προστέθηκαν.

**Q: Is disposing of Configuration and HTMLDocument objects required?**  
A: Absolutely; disposing releases native memory and prevents leaks in long‑running applications.

**Ε: Απαιτείται η απελευθέρωση των αντικειμένων Configuration και HTMLDocument;**  
Α: Απόλυτα· η απελευθέρωση απελευθερώνει τη φυσική μνήμη και αποτρέπει διαρροές σε εφαρμογές μεγάλης διάρκειας.

**Q: Besides missing images, what other errors can handlers manage?**  
A: Any non‑200 HTTP response—timeouts, 404 pages, authentication failures, etc.—can be intercepted and handled.

**Ε: Εκτός από ελλιπείς εικόνες, ποια άλλα σφάλματα μπορούν να διαχειριστούν οι handlers;**  
Α: Οποιαδήποτε απάντηση HTTP μη‑200—χρονικά όρια, σελίδες 404, αποτυχίες πιστοποίησης κ.λπ.—μπορεί να συλληφθεί και να αντιμετωπιστεί.

## Conclusion  
Τώρα έχετε ένα πλήρες, έτοιμο για παραγωγή παράδειγμα **μετατροπής HTML σε PNG** ενώ **διαχειρίζεστε σπασμένους συνδέσμους** και **πιάτε ελλιπείς πόρους** χρησιμοποιώντας Aspose.HTML για Java. Ενσωματώστε αυτό το μοτίβο σε μεγαλύτερα έργα για να αποκτήσετε λεπτομερή έλεγχο των δικτυακών λειτουργιών και να δημιουργήσετε αξιόπιστα στιγμιότυπα εικόνας του περιεχομένου HTML σας.

**Τελευταία ενημέρωση:** 2025-12-08  
**Δοκιμή με:** Aspose.HTML for Java 24.12 (latest)  
**Συγγραφέας:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}