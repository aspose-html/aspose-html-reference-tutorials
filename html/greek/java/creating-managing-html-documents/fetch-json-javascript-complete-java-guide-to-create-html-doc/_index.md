---
category: general
date: 2026-05-25
description: Μάθετε πώς να ανακτάτε JSON με JavaScript και να εμφανίζετε JSON HTML
  σε μια σελίδα που δημιουργείται από Java. Οδηγός βήμα‑προς‑βήμα για τη δημιουργία
  του στοιχείου body και την εμφάνιση των ανακτημένων δεδομένων.
draft: false
keywords:
- fetch json javascript
- display json html
- display fetched data
- create body element
- create html document java
language: el
og_description: Ανάκτηση JSON με JavaScript εύκολη. Αυτό το σεμινάριο δείχνει πώς
  να δημιουργήσετε ένα έγγραφο HTML με Java, να προσθέσετε ένα στοιχείο body και να
  εμφανίσετε τα ανακτημένα δεδομένα σε HTML.
og_title: Ανάκτηση JSON με JavaScript – Εκπαιδευτικό Java για Δημιουργία HTML
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to fetch json javascript and display json html in a Java‑generated
    page. Step‑by‑step guide to create body element and show fetched data.
  headline: fetch json javascript – Complete Java Guide to Create HTML Document
  type: TechArticle
- description: Learn how to fetch json javascript and display json html in a Java‑generated
    page. Step‑by‑step guide to create body element and show fetched data.
  name: fetch json javascript – Complete Java Guide to Create HTML Document
  steps:
  - name: Why This Works
    text: '- **`fetch`** is the modern, promise‑based API for HTTP requests in browsers.
      It replaces the older `XMLHttpRequest`. - The response is parsed as JSON with
      `r.json()`. - We create a `<pre>` element so the JSON appears nicely formatted
      (thanks to `JSON.stringify` with indentation). - Finally, we **di'
  - name: 1. Network Errors
    text: 'Even with the `.catch` we added, a failed request leaves the page empty.
      You might want a fallback UI:'
  - name: 2. Asynchronous Loading
    text: 'Our example runs the script as soon as the document is closed, which is
      fine for a demo. In production you might defer execution until `DOMContentLoaded`:'
  - name: 3. Styling the Output
    text: 'If you want the JSON to look prettier, add a quick CSS rule:'
  - name: 4. Multiple Requests
    text: Want to pull several endpoints? Wrap the fetch logic in a function and call
      it multiple times, or use `Promise.all` to run them in parallel.
  - name: Expected Result
    text: Open `scripted.html` and you should see a neatly formatted JSON block, exactly
      as shown earlier. The page itself contains no other content—just the **display
      json html** we programmed.
  type: HowTo
tags:
- Java
- Aspose.HTML
- JSON
- Web Scraping
title: fetch json javascript – Πλήρης Οδηγός Java για τη Δημιουργία Εγγράφου HTML
url: /el/java/creating-managing-html-documents/fetch-json-javascript-complete-java-guide-to-create-html-doc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fetch json javascript – Πλήρης Οδηγός Java για Δημιουργία Εγγράφου HTML

Έχετε αναρωτηθεί ποτέ πώς να **fetch json javascript** από ένα δημόσιο API και να ενσωματώσετε το αποτέλεσμα απευθείας σε ένα στατικό αρχείο HTML που δημιουργείται από τη Java; Δεν είστε ο μόνος που σκεπάζεστε το κεφάλι σας γι' αυτό. Σε πολλά έργα—σκεφτείτε γρήγορα‑πρωτότυπα dashboards ή αυτοματοποιημένους δημιουργούς αναφορών—πρέπει να τραβήξετε δεδομένα JSON και **display json html** χωρίς να ξεκινήσετε έναν πλήρη web server.

Αυτό είναι ακριβώς αυτό που θα λύσουμε τώρα. Στο τέλος αυτού του οδηγού θα ξέρετε πώς να **create html document java**, να προσθέσετε ένα **create body element**, να ενσωματώσετε ένα `<script>` που **fetch json javascript**, και τελικά να **display fetched data** μέσα σε ένα καλαίσθητα μορφοποιημένο `<pre>` μπλοκ. Καμία μυστική, μόνο ένα λειτουργικό παράδειγμα που μπορείτε να αντιγράψετε‑επικολλήσετε.

## Τι Καλύπτει Αυτό το Σεμινάριο

- Προαπαιτήσεις: Java 8+, Maven και η βιβλιοθήκη Aspose.HTML for Java.
- Δημιουργία βήμα‑βήμα ενός εγγράφου HTML από το μηδέν.
- Προσθήκη ενός στοιχείου body και ενός script που εκτελεί ένα αίτημα `fetch`.
- Αποθήκευση του παραγόμενου αρχείου και επαλήθευση ότι το JSON εμφανίζεται στον περιηγητή.
- Προαιρετικές προσαρμογές: διαχείριση σφαλμάτων, εκτέλεση async vs. sync, και συμβουλές στυλ.

Αν έχετε προσπαθήσει ποτέ να δημιουργήσετε HTML εν κινήσει μόνο για να καταλήξετε με μια κενή σελίδα, αυτός ο οδηγός θα σας εξοικονομήσει ώρες. Ας ξεκινήσουμε.

---

## Βήμα 1: Ρυθμίστε το Έργο σας και Εισάγετε το Aspose.HTML

Πριν μπορέσουμε να **create html document java**, χρειαζόμαστε τη βιβλιοθήκη Aspose.HTML στο classpath. Ο πιο εύκολος τρόπος είναι να χρησιμοποιήσετε Maven:

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-html</artifactId>
        <version>23.10</version> <!-- Check for the latest version -->
    </dependency>
</dependencies>
```

> **Pro tip:** Αν δεν χρησιμοποιείτε Maven, κατεβάστε το JAR από την ιστοσελίδα της Aspose και προσθέστε το στο build path του IDE σας.

Μόλις επιλυθεί η εξάρτηση, μπορείτε να αρχίσετε τον κώδικα. Ανοίξτε τον αγαπημένο σας επεξεργαστή—IntelliJ IDEA, Eclipse ή ακόμη και VS Code—και δημιουργήστε μια νέα κλάση Java με όνομα `JsExecution`.

## Βήμα 2: **create html document java** – Αρχικοποίηση Κενής Εγγράφου

Το πρώτο πράγμα που κάνουμε είναι να δημιουργήσουμε ένα κενό `HTMLDocument`. Σκεφτείτε το ως έναν φρέσκο καμβά, όπως το άνοιγμα ενός νέου αρχείου Notepad.

```java
import com.aspose.html.dom.*;
import com.aspose.html.services.*;

public class JsExecution {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new empty HTML document
        HTMLDocument doc = new HTMLDocument();
```

Γιατί να μην γράψουμε απλώς μια συμβολοσειρά HTML; Επειδή το DOM API μας παρέχει μεθόδους τύπου‑ασφαλούς για τη διαχείριση στοιχείων, εξασφαλίζοντας ότι δεν θα δημιουργήσουμε κατά λάθος λανθασμένο markup.

## Βήμα 3: **create body element** – Προσθήκη Ετικέτας `<body>`

Ένα έγγραφο χωρίς `<body>` είναι σχεδόν αόρατο σε έναν περιηγητή. Ας προσθέσουμε ένα:

```java
        // Step 3: Add a <body> element to the document
        Element body = doc.createElement("body");
        doc.appendChild(body);
```

Παρατηρήστε ότι χρησιμοποιούμε `createElement` αντί για ακατέργαστο HTML. Αυτό εγγυάται ότι το στοιχείο ανήκει στο ίδιο έγγραφο και αποφεύγει προβλήματα namespace που μερικές φορές προκαλούν προβλήματα στις προσεγγίσεις με συμβολοσειρές.

## Βήμα 4: **fetch json javascript** – Εισαγωγή `<script>` που Ανάγει Δεδομένα

Τώρα έρχεται το νόστιμο μέρος: το απόσπασμα JavaScript που **fetch json javascript** και **display fetched data**. Θα ενσωματώσουμε το script απευθείας στο DOM.

```java
        // Step 4: Insert a <script> element that fetches JSON data and displays it
        Element script = doc.createElement("script");
        script.setAttribute("type", "text/javascript");
        script.appendChild(doc.createTextNode(
                "fetch('https://jsonplaceholder.typicode.com/todos/1')\n" +
                "  .then(r => r.json())\n" +
                "  .then(data => {\n" +
                "    const pre = document.createElement('pre');\n" +
                "    pre.textContent = JSON.stringify(data, null, 2);\n" +
                "    document.body.appendChild(pre);\n" +
                "  })\n" +
                "  .catch(err => console.error('Fetch error:', err));"));
        body.appendChild(script);
```

### Γιατί Αυτό Λειτουργεί

- **`fetch`** είναι το σύγχρονο, βασισμένο σε promises API για HTTP αιτήματα σε browsers. Αντικαθιστά το παλιό `XMLHttpRequest`.
- Η απάντηση αναλύεται ως JSON με `r.json()`.
- Δημιουργούμε ένα στοιχείο `<pre>` ώστε το JSON να εμφανίζεται ωραία μορφοποιημένο (ευχαριστώντας το `JSON.stringify` με εσοχές).
- Τέλος, **display json html** προσθέτοντας το `<pre>` στο `document.body`.

Η πρόταση `.catch` είναι ένα δίχτυ ασφαλείας: αν η κλήση δικτύου αποτύχει, θα δείτε ένα σφάλμα στην κονσόλα αντί για σιωπηρή διακοπή.

## Βήμα 5: Ενεργοποίηση Εκτέλεσης Script και Αποθήκευση του Αρχείου

Το Aspose.HTML αντιμετωπίζει το έγγραφο ως εικονικό πρόγραμμα περιήγησης. Για να βεβαιωθούμε ότι το script εκτελείται (ακόμα και αν δεν χρειαζόμαστε το αποτέλεσμα άμεσα), κλείνουμε το ρεύμα του εγγράφου, το οποίο εξαναγκάζει την εκτέλεση.

```java
        // Step 5: Trigger script execution (synchronous for demonstration)
        doc.getWindow().getDocument().close();

        // Step 6: Save the generated HTML file
        doc.save("scripted.html");
        System.out.println("HTML with fetched data saved as scripted.html");
    }
}
```

Όταν ανοίξετε το `scripted.html` σε οποιονδήποτε σύγχρονο περιηγητή, θα δείτε ένα ωραία μορφοποιημένο μπλοκ που περιέχει κάτι όπως:

```json
{
  "userId": 1,
  "id": 1,
  "title": "delectus aut autem",
  "completed": false
}
```

Αυτή είναι η ενέργεια του **display fetched data**.

## Βήμα 6: Εκτελέστε το Πρόγραμμα και Επαληθεύστε το Αποτέλεσμα

Συγκεντρώστε και εκτελέστε:

```bash
mvn compile exec:java -Dexec.mainClass=JsExecution
```

Θα πρέπει να δείτε το μήνυμα στην κονσόλα που επιβεβαιώνει τη δημιουργία του αρχείου. Ανοίξτε το `scripted.html` με Chrome, Firefox ή Edge. Αν όλα πήγαν καλά, το JSON εμφανίζεται μέσα σε ένα `<pre>` μπλοκ ακριβώς κάτω από το body.

> **Note:** Ορισμένες ρυθμίσεις ασφαλείας (π.χ., άνοιγμα αρχείου μέσω `file://`) μπορεί να μπλοκάρουν το `fetch` λόγω CORS. Αν δείτε κενή σελίδα, δοκιμάστε να σερβίρετε το αρχείο μέσω ενός απλού τοπικού HTTP server:

```bash
python -m http.server 8080
# Then navigate to http://localhost:8080/scripted.html
```

## Διαχείριση Ακραίων Περιπτώσεων και Συνηθισμένων Παγίδων

### 1. Σφάλματα Δικτύου

Ακόμη και με το `.catch` που προσθέσαμε, μια αποτυχημένη αίτηση αφήνει τη σελίδα κενή. Μπορεί να θέλετε ένα εναλλακτικό UI:

```javascript
.catch(err => {
    const msg = document.createElement('p');
    msg.textContent = 'Unable to load data. Please try again later.';
    document.body.appendChild(msg);
    console.error(err);
});
```

### 2. Ασύγχρονη Φόρτωση

Το παράδειγμά μας εκτελεί το script μόλις κλείσει το έγγραφο, κάτι που είναι εντάξει για μια επίδειξη. Σε παραγωγή μπορεί να θέλετε να καθυστερήσετε την εκτέλεση μέχρι το `DOMContentLoaded`:

```javascript
document.addEventListener('DOMContentLoaded', () => {
    // fetch logic here
});
```

### 3. Στυλ του Αποτελέσματος

Αν θέλετε το JSON να φαίνεται πιο ωραίο, προσθέστε έναν γρήγορο κανόνα CSS:

```java
Element style = doc.createElement("style");
style.appendChild(doc.createTextNode(
    "pre { background:#f4f4f4; padding:10px; border-radius:4px; font-family:monospace; }"));
head.appendChild(style);
```

Μην ξεχάσετε να δημιουργήσετε πρώτα ένα στοιχείο `<head>` αν δεν το έχετε κάνει ήδη.

### 4. Πολλαπλά Αιτήματα

Θέλετε να τραβήξετε πολλά endpoints; Τυλίξτε τη λογική του fetch σε μια συνάρτηση και καλέστε την πολλές φορές, ή χρησιμοποιήστε `Promise.all` για να τα εκτελέσετε παράλληλα.

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση αρχείο πηγαίου κώδικα. Αντιγράψτε το στο `src/main/java/JsExecution.java` και εκτελέστε το όπως φαίνεται παραπάνω.

```java
import com.aspose.html.dom.*;
import com.aspose.html.services.*;

public class JsExecution {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new empty HTML document
        HTMLDocument doc = new HTMLDocument();

        // 2️⃣ Add a <head> (optional but useful for CSS)
        Element head = doc.createElement("head");
        doc.appendChild(head);

        // 3️⃣ Insert simple CSS to make the JSON look nice
        Element style = doc.createElement("style");
        style.appendChild(doc.createTextNode(
                "pre { background:#f9f9f9; padding:12px; border:1px solid #ddd; " +
                "border-radius:4px; font-family:monospace; overflow:auto; }"));
        head.appendChild(style);

        // 4️⃣ Add a <body> element – the place where we’ll inject data
        Element body = doc.createElement("body");
        doc.appendChild(body);

        // 5️⃣ <script> that **fetch json javascript** and **display fetched data**
        Element script = doc.createElement("script");
        script.setAttribute("type", "text/javascript");
        script.appendChild(doc.createTextNode(
                "fetch('https://jsonplaceholder.typicode.com/todos/1')\n" +
                "  .then(r => r.json())\n" +
                "  .then(data => {\n" +
                "    const pre = document.createElement('pre');\n" +
                "    pre.textContent = JSON.stringify(data, null, 2);\n" +
                "    document.body.appendChild(pre);\n" +
                "  })\n" +
                "  .catch(err => {\n" +
                "    const p = document.createElement('p');\n" +
                "    p.textContent = 'Failed to load data.';\n" +
                "    document.body.appendChild(p);\n" +
                "    console.error(err);\n" +
                "  });"));
        body.appendChild(script);

        // 6️⃣ Force execution and save the file
        doc.getWindow().getDocument().close();
        doc.save("scripted.html");
        System.out.println("HTML with fetched data saved as scripted.html");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Ανοίξτε το `scripted.html` και θα πρέπει να δείτε ένα ωραία μορφοποιημένο μπλοκ JSON, ακριβώς όπως φαίνεται παραπάνω. Η σελίδα δεν περιέχει άλλο περιεχόμενο—μόνο το **display json html** που προγραμματίσαμε.

## Συμπέρασμα

Μόλις διασχίσαμε μια πλήρη ροή εργασίας **fetch json javascript** χρησιμοποιώντας καθαρή Java και Aspose.HTML. Ξεκινώντας από μια κενή σελίδα, **create html document java**, **create body element**, ενσωματώσαμε ένα script που τραβά δεδομένα από ένα δημόσιο API, και τελικά **display fetched data** σε αναγνώσιμη μορφή. Η προσέγγιση είναι ελαφριά, δεν απαιτεί εξωτερική μηχανή templating, και μπορεί να επεκταθεί για τη δημιουργία αναφορών, dashboards ή ακόμη και στατικών ιστοσελίδων.

Τι ακολουθεί; Δοκιμάστε να αντικαταστήσετε το endpoint με τη δική σας υπηρεσία REST, προσθέστε σελιδοποίηση, ή δημιουργήστε πολλαπλές σελίδες σε μία εκτέλεση. Μπορείτε επίσης να εξερευνήσετε βιβλιοθήκες server‑side rendering αν χρειάζεστε πιο σύνθετες διατάξεις.

Έχετε ερωτήσεις σχετικά με τη διαχείριση σφαλμάτων ή το στυλ;

## Σχετικά Σεμινάρια

- [Δημιουργία Εγγράφων HTML Ασύγχρονα στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/create-html-documents-async/)
- [Δημιουργία Εγγράφων HTML από String στο Aspose.HTML για Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Δημιουργία Αρχείου HTML Java & Ρύθμιση Υπηρεσίας Δικτύου (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}