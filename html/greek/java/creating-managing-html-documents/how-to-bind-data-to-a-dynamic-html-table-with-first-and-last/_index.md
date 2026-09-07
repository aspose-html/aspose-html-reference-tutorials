---
category: general
date: 2026-09-07
description: πώς να δεσμεύσετε δεδομένα σε έναν δυναμικό πίνακα HTML – μάθετε πώς
  να δημιουργείτε σειρές πίνακα και να γεμίζετε τα πεδία όνομα και επώνυμο αποδοτικά
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: el
lastmod: 2026-09-07
og_description: πώς να δεσμεύσετε δεδομένα σε έναν δυναμικό πίνακα HTML. Αυτό το σεμινάριο
  δείχνει πώς να δημιουργήσετε γραμμές πίνακα, να εμφανίσετε το όνομα και το επώνυμο,
  και να γεμίσετε τις γραμμές του πίνακα με JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Πώς να δεσμεύσετε δεδομένα σε έναν δυναμικό πίνακα HTML – βήμα‑βήμα οδηγός
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: how to bind data in a dynamic HTML table – learn how to generate table
    rows and populate first and last name fields efficiently
  headline: How to bind data to a dynamic HTML table with first and last name columns
  type: TechArticle
tags:
- data binding
- html table
- templating
title: Πώς να δεσμεύσετε δεδομένα σε έναν δυναμικό πίνακα HTML με στήλες Όνομα και
  Επώνυμο
url: /el/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δεσμεύσετε δεδομένα σε έναν δυναμικό πίνακα HTML με στήλες όνομα και επώνυμο

Αν χρειάζεστε **πώς να δεσμεύσετε δεδομένα** σε έναν πίνακα που μεγαλώνει με κάθε εγγραφή, αυτός ο οδηγός παρουσιάζει μια πλήρη λύση. Θα δείτε πώς να δημιουργήσετε έναν δυναμικό πίνακα HTML, να γεμίσετε τις γραμμές του πίνακα και να εμφανίσετε το όνομα και το επώνυμο κάθε ατόμου χωρίς να γράψετε επαναλαμβανόμενο markup.

Το παράδειγμα χρησιμοποιεί μια ελαφριά σύνταξη templating που λειτουργεί σε οποιονδήποτε σύγχρονο περιηγητή, αλλά οι έννοιες ισχύουν και για Handlebars, Mustache ή server‑side μηχανές. Στο τέλος του tutorial μπορείτε να αντιγράψετε τον κώδικα στο έργο σας και να αρχίσετε να δεσμεύετε δεδομένα αμέσως.

## Τι καλύπτει αυτό το tutorial

* Πώς να δομήσετε μια πηγή δεδομένων που περιέχει πολλούς ανθρώπους  
* Πώς να δημιουργήσετε ένα επαναχρησιμοποιήσιμο πρότυπο πίνακα που επαναλαμβάνεται για κάθε καταχώρηση  
* Πώς να δεσμεύσετε τα δεδομένα και να δημιουργήσετε το τελικό markup HTML  
* Συνηθισμένα προβλήματα κατά τη γεμίσματος των γραμμών του πίνακα και πώς να τα αποφύγετε  

Δεν απαιτούνται εξωτερικές βιβλιοθήκες, αν και το ίδιο μοτίβο λειτουργεί με δημοφιλή frameworks templating. Η μόνη προαπαιτούμενη γνώση είναι βασικά HTML και JavaScript.

## Προαπαιτούμενα

* Ένας σύγχρονος περιηγητής (Chrome, Edge, Firefox ή Safari)  
* Ένας επεξεργαστής για αρχεία HTML/JavaScript  
* Προαιρετικά: ένα αρχείο JSON ή αντικείμενο JavaScript που αντιπροσωπεύει τη συλλογή των ατόμων  

## Βήμα 1: Ορίστε την πηγή δεδομένων

Πρώτα, δημιουργήστε ένα αντικείμενο JavaScript που αντικατοπτρίζει τη δομή που χρησιμοποιείται στο πρότυπο. Κάθε άτομο έχει όνομα, επώνυμο και ένα αντικείμενο διεύθυνσης.

```html
<script>
  // Data source – an array of person objects
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: {
            Street: "Maple",
            Number: "12A",
            City: "Springfield"
          }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: {
            Street: "Oak",
            Number: "34B",
            City: "Riverdale"
          }
        }
        // Add more person objects as needed
      ]
    }
  };
</script>
```

**Γιατί είναι σημαντικό:** Η ιεραρχία του αντικειμένου (`Persons.Person`) ταιριάζει με το βρόχο `{{#foreach Persons.Person}}` στο πρότυπο, επιτρέποντας στη μηχανή να επαναλάβει αυτόματα κάθε καταχώρηση.

## Βήμα 2: Γράψτε το πρότυπο πίνακα με μπλοκ επανάληψης

Το παρακάτω πρότυπο χρησιμοποιεί μια απλή σύνταξη τύπου Mustache (`{{#foreach}}`) για να επαναλάβει το `<tr>` για κάθε άτομο. Τοποθετήστε το πρότυπο μέσα σε μια ετικέτα `<script type="text/template">` ώστε ο περιηγητής να το αγνοήσει μέχρι να το επεξεργαστείτε.

```html
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Table header -->
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <!-- Row populated with each person's data -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**Γιατί είναι σημαντικό:** Η οδηγία `{{#foreach Persons.Person}}` λέει στη μηχανή να επαναλάβει όλα μεταξύ των εναρκτήριων και κλειστικών ετικετών για κάθε αντικείμενο ατόμου. Μέσα στη γραμμή μπορείτε να αναφερθείτε σε οποιαδήποτε ιδιότητα (`{{FirstName}}`, `{{LastName}}` κ.λπ.) για **να γεμίσετε δυναμικά τις γραμμές του πίνακα**.

## Βήμα 3: Υλοποιήστε μια μικρή συνάρτηση απόδοσης

Επειδή το tutorial πρέπει να είναι αυτόνομο, θα γράψουμε έναν ελάχιστο renderer που αντικαθιστά τα placeholders τύπου Mustache με πραγματικές τιμές. Η συνάρτηση διασχίζει το αντικείμενο δεδομένων, επεκτείνει το μπλοκ επανάληψης και ενθέτει το τελικό HTML στη σελίδα.

```html
<script>
  /**
   * Renders a template that contains a single {{#foreach}} block.
   * This implementation is intentionally simple and works for the
   * specific structure used in this tutorial.
   *
   * @param {string} tmpl   The raw template string.
   * @param {object} ctx    The data context (e.g., the `data` object).
   * @returns {string}      The rendered HTML.
   */
  function renderTemplate(tmpl, ctx) {
    // Extract the foreach expression and the block to repeat
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl; // No foreach found

    const path = match[1].trim(); // e.g., "Persons.Person"
    const block = match[2];       // HTML that repeats

    // Resolve the array from the context (supports dot notation)
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items)) return tmpl;

    // Render each item
    const renderedBlocks = items.map(item => {
      // Replace each {{property}} with the corresponding value
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });

    // Replace the whole foreach section with the concatenated rows
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  // When the DOM is ready, render the table
  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>
```

**Γιατί είναι σημαντικό:** Ο renderer δείχνει **πώς να δημιουργήσετε markup πίνακα** προγραμματιστικά χωρίς να ενσωματώσετε μια πλήρη βιβλιοθήκη. Επίσης διευκρινίζει τη μετατροπή από το πρότυπο στο τελικό HTML, κάτι που σας βοηθά να προσαρμόσετε τον κώδικα σε άλλες μηχανές templating αργότερα.

## Βήμα 4: Προσθέστε ένα placeholder όπου θα εμφανιστεί ο παραγόμενος πίνακας

Δημιουργήστε ένα κενό `<div>` που το script θα γεμίσει μετά την απόδοση.

```html
<div id="output"></div>
```

Όταν η σελίδα φορτωθεί, το script αντικαθιστά το περιεχόμενο αυτού του `<div>` με τον πλήρως γεμισμένο πίνακα.

## Βήμα 5: Επαληθεύστε το αποτέλεσμα

Ανοίξτε το αρχείο HTML σε έναν περιηγητή. Θα πρέπει να δείτε έναν πίνακα που καταγράφει το πλήρες όνομα και τη διεύθυνση κάθε ατόμου:

| Person          | Address                         |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Αν προσθέσετε περισσότερα αντικείμενα στον πίνακα `data.Persons.Person`, ο πίνακας μεγαλώνει αυτόματα—ικανοποιώντας την απαίτηση **γέμισης γραμμών πίνακα**.

## Pro tip: διαχείριση κενών συλλογών

Όταν ο πίνακας δεδομένων είναι κενός, ο renderer αυτή τη στιγμή παράγει μόνο την κεφαλίδα του πίνακα. Για καλύτερη εμπειρία χρήστη, προσθέστε έναν έλεγχο:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Αυτή η μικρή αλλαγή αποτρέπει την εμφάνιση ενός κενού πίνακα και παρέχει άμεση ανατροφοδότηση στον χρήστη.

## Συνηθισμένες παραλλαγές και edge cases

| Situation                               | Adjustment                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| Using a server‑side engine (e.g., Handlebars) | Replace the custom `renderTemplate` with `Handlebars.compile` and pass the same data object. |
| Need to sort rows alphabetically       | Sort `data.Persons.Person` before calling `renderTemplate`.               |
| Adding a column for phone number       | Extend the `<tr>` with `<td>{{Phone}}</td>` and include `Phone` in each person object. |
| Large data sets (hundreds of rows)     | Render rows in chunks or use virtual scrolling to keep the UI responsive. |

## Πλήρες λειτουργικό παράδειγμα

Παρακάτω βρίσκεται το πλήρες αρχείο HTML που μπορείτε να αντιγράψετε‑επικολλήσετε στο `index.html`. Περιέχει όλα τα στοιχεία που συζητήθηκαν παραπάνω.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to bind data to a dynamic HTML table</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<h1>Dynamic HTML table bound to JavaScript data</h1>

<!-- Step 2: Table template -->
<script type="text/template" id="table-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th>Person</th><th>Address</th>
  </tr>
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>

<!-- Step 1: Data source -->
<script>
  const data = {
    Persons: {
      Person: [
        {
          FirstName: "Alice",
          LastName: "Johnson",
          Address: { Street: "Maple", Number: "12A", City: "Springfield" }
        },
        {
          FirstName: "Bob",
          LastName: "Smith",
          Address: { Street: "Oak", Number: "34B", City: "Riverdale" }
        }
        // Add more entries as needed
      ]
    }
  };
</script>

<!-- Step 4: Output container -->
<div id="output"></div>

<!-- Step 3: Rendering logic -->
<script>
  function renderTemplate(tmpl, ctx) {
    const foreachRegex = /{{#foreach\s+([^}]+)}}([\s\S]*?){{\/foreach}}/;
    const match = tmpl.match(foreachRegex);
    if (!match) return tmpl;
    const path = match[1].trim();
    const block = match[2];
    const items = path.split('.').reduce((obj, key) => obj && obj[key], ctx);
    if (!Array.isArray(items) || items.length === 0) {
      return '<p>No records found.</p>';
    }
    const renderedBlocks = items.map(item => {
      return block.replace(/{{([^}]+)}}/g, (_, prop) => {
        const value = prop.trim().split('.').reduce((obj, key) => obj && obj[key], item);
        return value !== undefined ? value : '';
      });
    });
    return tmpl.replace(foreachRegex, renderedBlocks.join(''));
  }

  document.addEventListener('DOMContentLoaded', () => {
    const tmpl = document.getElementById('table-template').innerHTML;
    const html = renderTemplate(tmpl, data);
    document.getElementById('output').innerHTML = html;
  });
</script>

</body>
</html>
```

**Αναμενόμενο αποτέλεσμα**

Η σελίδα εμφανίζει έναν πίνακα με δύο γραμμές, η καθεμία δείχνοντας το πλήρες όνομα και τη μορφοποιημένη διεύθυνση ενός ατόμου. Η προσθήκη περισσότερων αντικειμένων στον πίνακα `Person` προσθέτει αυτόματα νέες γραμμές—δείχνοντας **πώς να δημιουργήσετε στοιχεία πίνακα** από δεδομένα.

## Συμπέρασμα

Τώρα ξέρετε **πώς να δεσμεύσετε δεδομένα** σε έναν **δυναμικό πίνακα HTML**, να δημιουργήσετε γραμμές για κάθε εγγραφή και να εμφανίσετε τις τιμές του ονόματος και του επωνύμου μαζί με τη διεύθυνση.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Enable JavaScript in Aspose HTML – Load HTML & Get Text](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}