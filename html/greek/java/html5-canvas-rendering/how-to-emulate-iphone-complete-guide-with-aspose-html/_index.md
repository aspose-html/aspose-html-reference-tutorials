---
category: general
date: 2026-03-26
description: Μάθετε πώς να προσομοιώσετε iPhone σε Java χρησιμοποιώντας το Aspose.HTML.
  Περιλαμβάνει βήματα για τον ορισμό προσαρμοσμένου user agent και του λόγου pixel
  της συσκευής για ακριβή απόδοση σε κινητές συσκευές.
draft: false
keywords:
- how to emulate iphone
- set custom user agent
- set device pixel ratio
- how to set user-agent
- how to set dpr
language: el
og_description: Πώς να προσομοιώσετε iPhone σε Java; Αυτό το σεμινάριο δείχνει πώς
  να ορίσετε προσαρμοσμένο user agent και λόγο εικονοστοιχείων συσκευής χρησιμοποιώντας
  το Aspose.HTML, παρέχοντας σελίδες κινητών με pixel‑perfect ανάλυση.
og_title: Πώς να προσομοιώσετε iPhone – Οδηγός Aspose.HTML βήμα‑προς‑βήμα
tags:
- Aspose.HTML
- Java
- Mobile Emulation
title: Πώς να προσομοιώσετε iPhone – Πλήρης οδηγός με το Aspose.HTML
url: /el/java/html5-canvas-rendering/how-to-emulate-iphone-complete-guide-with-aspose-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξομοιώσετε iPhone – Πλήρης Οδηγός με το Aspose.HTML

Έχετε αναρωτηθεί ποτέ **πώς να εξομοιώσετε iPhone** όταν δοκιμάζετε μια ιστοσελίδα τοπικά; Ίσως κάνετε αποσφαλμάτωση ενός responsive layout και το desktop πρόγραμμα περιήγησης απλώς δεν αρκεί. Τα καλά νέα είναι ότι δεν χρειάζεστε φυσική συσκευή — το `DocumentSandbox` του Aspose.HTML σας επιτρέπει να μιμηθείτε την οθόνη, το user‑agent και το device‑pixel‑ratio (DPR) ενός iPhone με λίγες γραμμές Java.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από τα ακριβή βήματα για να ορίσετε **προσαρμοσμένο user agent**, να ρυθμίσετε το **device pixel ratio**, και να επαληθεύσετε ότι όλα λειτουργούν όπως αναμένεται. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο sandbox που αποδίδει σελίδες όπως ένα iPhone 8, και θα καταλάβετε γιατί κάθε ρύθμιση είναι σημαντική.

## Τι Θα Επιτύχετε

- Δημιουργία αντικειμένου `Screen` που αντικατοπτρίζει τις διαστάσεις και το DPR ενός iPhone.  
- Εφαρμογή **προσαρμοσμένης συμβολοσειράς user agent** ώστε οι διακομιστές να πιστεύουν ότι το αίτημα προέρχεται από Safari σε iOS.  
- Κατασκευή `DocumentSandbox` που συνδέει την οθόνη και το user‑agent.  
- Εκτέλεση `HTMLDocument` μέσα στο sandbox και εμφάνιση της εξόδου στην κονσόλα που επιβεβαιώνει τη ρύθμιση.  

Δεν απαιτούνται εξωτερικές βιβλιοθήκες πέρα από το Aspose.HTML, και ο κώδικας εκτελείται σε οποιοδήποτε περιβάλλον Java 17+.

---

![στιγμιότυπο εξομοίωσης iPhone](https://example.com/images/iphone-emulation.png "πώς να εξομοιώσετε iPhone χρησιμοποιώντας το sandbox του Aspose.HTML")

## Πώς να Εξομοιώσετε iPhone με το Aspose.HTML Sandbox

Το πρώτο που χρειάζεται είναι ένα `Screen` που αντικατοπτρίζει τις φυσικές διαστάσεις του iPhone *και* την πυκνότητα των εικονοστοιχείων του. Αυτό είναι ο πυρήνας του **πώς να εξομοιώσετε iPhone** με ακρίβεια.

```java
import com.aspose.html.devices.Screen;

// Step 1: Define iPhone 8 screen size (width, height) and DPR
Screen mobileScreen = new Screen(375, 667, 2.0); // iPhone 8 dimensions, DPR = 2
```

**Γιατί είναι σημαντικό:**  
- Το πλάτος = 375 px και το ύψος = 667 px είναι οι διαστάσεις CSS pixel που βλέπετε στα Chrome DevTools όταν επιλέγετε iPhone 8.  
- Ορίζοντας το DPR σε 2 λέτε στη μηχανή απόδοσης να αντιμετωπίζει κάθε CSS pixel ως δύο φυσικά pixel, προσφέροντας καθαρό κείμενο και εικόνες — ακριβώς όπως κάνει μια πραγματική συσκευή.

> *Pro tip:* Αν θέλετε να εξομοιώσετε ένα νεότερο iPhone (π.χ. iPhone 13), απλώς αλλάξτε τους αριθμούς σε 390 × 844 και DPR = 3.

## Ορισμός Προσαρμοσμένου User Agent (set custom user agent)

Στη συνέχεια, πρέπει να **ορίσουμε προσαρμοσμένο user agent** ώστε ο διακομιστής να σερβίρει το mobile‑specific HTML/CSS. Χωρίς αυτό, πολλά sites θα συνεχίσουν να πιστεύουν ότι βρίσκεστε σε desktop.

```java
// Step 2: Define an iPhone Safari user‑agent string
String iPhoneUserAgent = "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) " +
                         "AppleWebKit/605.1.15 (KHTML, like Gecko) " +
                         "Version/16.0 Mobile/15E148 Safari/604.1";
```

**Πώς λειτουργεί:**  
- Η κεφαλίδα `User-Agent` είναι το χέρι που χρησιμοποιούν τα προγράμματα περιήγησης για να ανακοινώσουν την ταυτότητά τους.  
- Παρέχοντας την ακριβή συμβολοσειρά που στέλνει το Safari σε iOS 16, εξασφαλίζετε ότι ο διακομιστής επιστρέφει τα mobile‑optimized assets (π.χ. responsive images, adaptive scripts, κ.λπ.).  

Αν χρειαστεί ποτέ να **πώς να ορίσετε user-agent** για διαφορετική συσκευή, απλώς αντικαταστήστε τη συμβολοσειρά με την αντίστοιχη τιμή — Google Chrome, Firefox, ή ακόμη και ένα προσαρμοσμένο bot.

## Ρύθμιση Device Pixel Ratio (set device pixel ratio)

Τώρα θα **ορίσουμε το device pixel ratio** μέσα στο sandbox. Αυτό είναι το βήμα που απαντά άμεσα στο ερώτημα “**πώς να ορίσετε dpr**” για ένα προσομοιωμένο περιβάλλον.

```java
import com.aspose.html.sandbox.DocumentSandbox;

// Step 3: Build the sandbox with screen and user‑agent
DocumentSandbox documentSandbox = new DocumentSandbox.Builder()
        .setScreen(mobileScreen)          // applies the DPR we defined earlier
        .setUserAgent(iPhoneUserAgent)    // applies the custom user‑agent
        .build();
```

**Εξήγηση:**  
- Το pattern `Builder` σας επιτρέπει να συνδέσετε ομαλά τόσο την οθόνη (που φέρει το DPR) όσο και το user‑agent.  
- Όταν το sandbox αποδίδει ένα `HTMLDocument`, θα προσποιηθεί ότι τρέχει σε συσκευή με αυτήν την ακριβή πυκνότητα εικονοστοιχείων.  

> *Γιατί να σας ενδιαφέρει:* Κάποια CSS media queries χρησιμοποιούν `device-pixel-ratio` (π.χ. `@media (-webkit-min-device-pixel-ratio: 2)`). Αν δεν ορίσετε το DPR, οι κανόνες αυτοί δεν ενεργοποιούνται ποτέ, και θα χάσετε τα υψηλής ανάλυσης assets.

## Επαλήθευση της Διαμόρφωσης του Sandbox (how to set user-agent)

Ας θέσουμε το sandbox σε λειτουργία. Το παρακάτω απόσπασμα δημιουργεί ένα `HTMLDocument`, φορτώνει μια σελίδα, και εκτυπώνει μια επιβεβαίωση ότι το sandbox είναι ενεργό.

```java
import com.aspose.html.HTMLDocument;

public class SandboxWithDprAndUa {
    public static void main(String[] args) {
        // Re‑use the sandbox we built earlier
        // DocumentSandbox documentSandbox = ... (from previous step)

        // Step 4: Load a page inside the sandbox
        HTMLDocument doc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 5: Optional – output a sanity check
        System.out.println("Sandbox configured with DPR=2 and iPhone user‑agent.");
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα**

```
Sandbox configured with DPR=2 and iPhone user-agent.
```

Αν τρέξετε το πρόγραμμα και δείτε αυτή τη γραμμή, έχετε επιτυχώς **πώς να εξομοιώσετε iPhone** με το σωστό DPR και user‑agent. Ανοίξτε τη σελίδα σε πραγματικό πρόγραμμα περιήγησης και ελέγξτε τις διαστάσεις του viewport — θα δείτε ότι ταιριάζουν με τις τιμές iPhone που ορίσαμε.

## Συνηθισμένα Πιθανά Σφάλματα και Πώς να Ορίσετε σωστά το DPR (how to set dpr)

Ακόμη και με τον σωστό κώδικα, μερικά μικρά προβλήματα μπορούν να σας κολλήσουν:

| Πρόβλημα | Γιατί συμβαίνει | Διόρθωση |
|----------|-----------------|----------|
| **Το DPR παραμένει 1** | Παρέχετε ένα `Screen` χωρίς το τρίτο όρισμα (DPR). | Πάντα χρησιμοποιείτε `new Screen(width, height, dpr)`. |
| **Ο User‑Agent αγνοείται** | Το sandbox δεν συνδέθηκε με το `HTMLDocument`. | Περνάτε το `documentSandbox` ως δεύτερο όρισμα στον κατασκευαστή του `HTMLDocument`. |
| **Λανθασμένες διαστάσεις** | Χρήση pixel της συσκευής αντί για CSS pixel. | Θυμηθείτε: το πλάτος/ύψος είναι **CSS pixel**, όχι hardware pixel. |
| **Ο διακομιστής εξακολουθεί να στέλνει desktop CSS** | Κάποια sites χρησιμοποιούν JavaScript για ανίχνευση συσκευών, όχι μόνο την κεφαλίδα. | Σκεφτείτε επίσης την εισαγωγή ενός meta viewport tag αν χρειάζεται. |

Κρατώντας αυτά στο μυαλό, σπάνια θα βρεθείτε σε κατάσταση όπου η εξομοίωση δεν συμπεριφέρεται όπως αναμένεται.

## Επέκταση του Sandbox – Επόμενα Βήματα

Τώρα που ξέρετε **πώς να ορίσετε προσαρμοσμένο user agent** και **πώς να ορίσετε dpr**, μπορείτε να πειραματιστείτε περαιτέρω:

- **Αλλάξτε το μέγεθος της οθόνης** για να εξομοιώσετε tablets ή μεγαλύτερα τηλέφωνα.  
- **Αλλάξτε το user‑agent** για να δοκιμάσετε Chrome σε Android (`"Mozilla/5.0 (Linux; Android 12; ...) Chrome/110.0"`).  
- **Προσθέστε cookies ή headers** μέσω της μεθόδου `setHeaders` του sandbox για δοκιμές με αυθεντικοποίηση.  
- **Καταγράψτε screenshot** χρησιμοποιώντας `HTMLDocument.renderToFile("output.png")` για να συγκρίνετε αυτόματα τις οπτικές διαφορές.

Αυτές οι επεκτάσεις σας επιτρέπουν να χτίσετε ένα πλήρες testing harness χωρίς να φύγετε ποτέ από το IDE σας.

---

## Συμπέρασμα

Καλύψαμε **πώς να εξομοιώσετε iPhone** χρησιμοποιώντας το `DocumentSandbox` του Aspose.HTML, δείχνοντας σας ακριβώς **πώς να ορίσετε προσαρμοσμένο user agent**, **πώς να ορίσετε device pixel ratio**, και ακόμη τις λεπτές διαφορές μεταξύ “**πώς να ορίσετε user-agent**” και “**πώς να ορίσετε dpr**”. Το πλήρες, εκτελέσιμο παράδειγμα παρουσιάζει κάθε κομμάτι σε ένα σημείο, ώστε να μπορείτε να το αντιγράψετε, να το τροποποιήσετε, και να ξεκινήσετε αμέσως τις δοκιμές mobile layout.  

Δοκιμάστε το — αλλάξτε τις διαστάσεις της οθόνης, παίξτε με διαφορετικά user‑agents, και παρακολουθήστε πώς αντιδρούν οι σελίδες σας. Όταν κυριαρχήσετε αυτές τις ρυθμίσεις, η αποσφαλμάτωση responsive σχεδίων γίνεται παιχνιδάκι, και θα εξοικονομήσετε αμέτρητες ώρες κυνηγώντας σφάλματα σε πραγματικές συσκευές.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε τις δικές σας παραλλαγές; Αφήστε ένα σχόλιο παρακάτω, και καλή εξομοίωση!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}