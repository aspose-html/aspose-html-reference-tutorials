---
category: general
date: 2026-10-12
description: Μάθετε πώς να δημιουργείτε πίνακα από δεδομένα και να τον γεμίζετε από
  JSON χρησιμοποιώντας Handlebars. Οδηγός βήμα‑βήμα για την επανάληψη γραμμών πίνακα
  σε δυναμικούς HTML πίνακες.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: el
lastmod: 2026-10-12
og_description: Δημιουργήστε πίνακα από δεδομένα και γεμίστε τον πίνακα από JSON χρησιμοποιώντας
  Handlebars. Ακολουθήστε αυτό το σεμινάριο για να δημιουργήσετε δυναμικούς πίνακες
  HTML με επαναλαμβανόμενες γραμμές πίνακα.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Δημιουργία πίνακα από δεδομένα με Handlebars – πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-10-12'
  description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  headline: How to generate table from data with HTML and Handlebars
  type: TechArticle
- description: Learn how to generate table from data and populate table from JSON
    using Handlebars. Step‑by‑step guide for repeat table rows in dynamic HTML tables.
  name: How to generate table from data with HTML and Handlebars
  steps:
  - name: 1. Empty data sets
    text: 'If the JSON array is empty, Handlebars will still render the header row
      but no data rows. To display a friendly message, wrap the table in a conditional
      block:'
  - name: 2. Nested loops (e.g., multiple addresses per person)
    text: 'When a person can have several addresses, you can nest another `{{#foreach}}`
      inside the row:'
  - name: 3. Using a real API
    text: 'Replace the static `<script id="people-data">` with a fetch call:'
  - name: 4. Accessibility considerations
    text: '* Add `scope="col"` to `<th>` elements. * Use `<caption>` to describe the
      table purpose. * Ensure sufficient color contrast if you apply custom CSS.'
  type: HowTo
tags:
- HTML
- Handlebars
- JSON
- templating
title: Πώς να δημιουργήσετε πίνακα από δεδομένα με HTML και Handlebars
url: /el/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να δημιουργήσετε πίνακα από δεδομένα με HTML και Handlebars

Αν χρειάζεστε **δημιουργία πίνακα από δεδομένα** σε μια ιστοσελίδα, αυτό το tutorial σας δείχνει ακριβώς πώς. Χρησιμοποιώντας έναν απλό βρόχο Handlebars μπορείτε **να γεμίσετε τον πίνακα από JSON**, να δημιουργήσετε **επαναλαμβανόμενες γραμμές πίνακα**, και να καταλήξετε σε έναν πλήρως **δυναμικό HTML πίνακα** που ενημερώνεται κάθε φορά που αλλάζει η πηγή.

Στα επόμενα λεπτά θα δείτε ένα πλήρες, εκτελέσιμο παράδειγμα, θα καταλάβετε γιατί κάθε μέρος είναι σημαντικό, και θα μάθετε πώς να προσαρμόσετε το μοτίβο για πιο σύνθετα σενάρια όπως υπό-συνθήκες στήλες ή ένθετα αντικείμενα.

## Τι θα δημιουργήσετε

Θα φτιάξουμε έναν HTML πίνακα που:

* Διαβάζει ένα JSON payload που περιέχει μια λίστα ατόμων.
* Επαναλαμβάνει μια γραμμή πίνακα για κάθε άτομο (`repeat table rows`).
* Εισάγει το όνομα, το επώνυμο και τη διεύθυνση του κάθε ατόμου στα αντίστοιχα κελιά.
* Λειτουργεί χωρίς καμία server‑side rendering – όλη η διαδικασία γίνεται στον περιηγητή.

**Προαπαιτούμενα**

* Βασικές γνώσεις HTML και JavaScript.
* Ένας σύγχρονος περιηγητής (Chrome, Edge, Firefox ή Safari).
* Handlebars.js – θα το φορτώσουμε από CDN, οπότε δεν απαιτούνται εργαλεία κατασκευής.

---

## Βήμα 1: Προετοιμασία της πηγής δεδομένων JSON

Το πρώτο βήμα είναι να ορίσετε ένα αντικείμενο JavaScript που μιμείται το JSON που θα λάβετε από ένα API. Το Handlebars δουλεύει με απλά αντικείμενα, οπότε μπορείτε να ενσωματώσετε τα δεδομένα απευθείας σε μια ετικέτα `<script>` για σκοπούς επίδειξης.

```html
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>
```

**Γιατί είναι σημαντικό** – Κρατώντας τα δεδομένα σε ξεχωριστό στοιχείο `<script>` μπορείτε εύκολα να το αντικαταστήσετε με πραγματική κλήση AJAX αργότερα. Η δομή (`Persons.Person`) ταιριάζει με τη διαδρομή που χρησιμοποιείται στο Handlebars `{{#foreach Persons.Person}}` block, κάτι που είναι απαραίτητο για **populate table from JSON**.

---

## Βήμα 2: Γράψτε το πρότυπο Handlebars που επαναλαμβάνει γραμμές

Στη συνέχεια, δημιουργήστε ένα block `<script type="text/x-handlebars-template">` που περιέχει το markup του πίνακα. Το Handlebars θα αντικαταστήσει τα placeholders με τις πραγματικές τιμές και θα επαναλάβει το `<tr>` για κάθε άτομο.

```html
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <!-- Header row describing the columns -->
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <!-- Data row – this block is repeated for each Person -->
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
</table>
</script>
```

**Επεξήγηση των βασικών τμημάτων**

* `{{#foreach Persons.Person}}` λέει στο Handlebars να **repeat table rows** για κάθε στοιχείο του πίνακα `Persons.Person`.
* Οι εκφράσεις `{{FirstName}} {{LastName}}` και `{{Address.*}}` αντλούν τιμές από το τρέχον στοιχείο του πίνακα.
* Η περιτύλιξη ολόκληρου του πίνακα σε attribute `data_merge` είναι προαιρετική· μπορεί να φανεί χρήσιμη για επεξεργασία downstream ή για selectors CSS.

---

## Βήμα 3: Φορτώστε το Handlebars και συνθέστε το πρότυπο

Θα φορτώσουμε το Handlebars από CDN, θα αναλύσουμε το JSON, θα συνθέσουμε το πρότυπο και θα ενσωματώσουμε το τελικό HTML στη σελίδα.

```html
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  // Parse the JSON stored in the <script id="people-data">
  const rawData = document.getElementById('people-data').textContent;
  const context = JSON.parse(rawData);

  // Grab the template markup and compile it
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);

  // Generate the final HTML by applying the context
  const html = template(context);

  // Insert the generated table into the DOM
  document.getElementById('output').innerHTML = html;
</script>
```

**Γιατί να συνθέτετε τη στιγμή της εκτέλεσης;** – Η σύνθεση του προτύπου μία φορά και η επαναχρησιμοποίησή του κρατά τη σελίδα γρήγορη, ειδικά όταν τα δεδομένα αλλάζουν συχνά. Αυτό το μοτίβο κάνει επίσης εύκολο το **populate table from JSON** πολλές φορές χωρίς επαναφόρτωση της σελίδας.

---

## Βήμα 4: Κρατήστε έναν χώρο για τον παραγόμενο πίνακα

Προσθέστε ένα placeholder `<div>` όπου θα εμφανιστεί ο δυναμικός πίνακας. Αυτό διατηρεί το markup καθαρό και χωρίζει τις ανησυχίες μεταξύ του στατικού layout και του παραγόμενου περιεχομένου.

```html
<div id="output"></div>
```

Όταν εκτελεστεί το script από το Βήμα 3, το `<div id="output">` θα περιέχει ένα πλήρως διαμορφωμένο στοιχείο `<table>`, έτοιμο για στυλ ή περαιτέρω επεξεργασία.

---

## Βήμα 5: Επαληθεύστε το αποτέλεσμα και στυλιζάτε τον πίνακα (προαιρετικά)

Ανοίξτε τη σελίδα σε έναν περιηγητή και θα πρέπει να δείτε έναν πίνακα όπως ο παρακάτω:

![Screenshot showing generated table from data](image.png "Screenshot showing generated table from data")

```html
<table border="1" data_merge="true">
  <tr>
    <th>Person</th>
    <th>Address</th>
  </tr>
  <tr>
    <td>Alice Anderson</td>
    <td>Maple 123, Springfield</td>
  </tr>
  <tr>
    <td>Bob Baker</td>
    <td>Oak 456, Rivertown</td>
  </tr>
</table>
```

**Προαιρετικό στυλ** – Αν θέλετε πιο καθαρό αποτέλεσμα, προσθέστε μερικούς κανόνες CSS:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Διαχείριση ειδικών περιπτώσεων και κοινών παραλλαγών

### 1. Κενά σύνολα δεδομένων

Αν ο πίνακας JSON είναι κενός, το Handlebars θα αποδώσει ακόμα τη γραμμή κεφαλίδας αλλά όχι γραμμές δεδομένων. Για να εμφανίσετε ένα φιλικό μήνυμα, τυλίξτε τον πίνακα σε ένα conditional block:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Ενθέτες βρόχοι (π.χ., πολλαπλές διευθύνσεις ανά άτομο)

Όταν ένα άτομο μπορεί να έχει πολλές διευθύνσεις, μπορείτε να ενσωματώσετε έναν ακόμη `{{#foreach}}` μέσα στη γραμμή:

```handlebars
{{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>
      {{#foreach Address}}
        {{Street}} {{Number}}, {{City}}<br>
      {{/foreach}}
    </td>
  </tr>
{{/foreach}}
```

### 3. Χρήση πραγματικού API

Αντικαταστήστε το στατικό `<script id="people-data">` με μια κλήση fetch:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Αυτό δείχνει την ίδια τεχνική **dynamic table rows** ενώ αντλεί ζωντανά δεδομένα.

### 4. Σκέψεις προσβασιμότητας

* Προσθέστε `scope="col"` στα στοιχεία `<th>`.
* Χρησιμοποιήστε `<caption>` για να περιγράψετε τον σκοπό του πίνακα.
* Εξασφαλίστε επαρκή αντίθεση χρωμάτων αν εφαρμόζετε προσαρμοσμένο CSS.

---

## Πλήρες, εκτελέσιμο παράδειγμα

Αντιγράψτε το παρακάτω block σε ένα αρχείο `index.html` και ανοίξτε το σε έναν περιηγητή. Η σελίδα θα **generate table from data**, **populate table from JSON**, και θα επαναλαμβάνει τις γραμμές αυτόματα.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dynamic table from JSON</title>
  <style>
    table { border-collapse: collapse; width: 100%; }
    th, td { padding: 8px; text-align: left; border: 1px solid #ddd; }
    th { background-color: #f2f2f2; }
  </style>
</head>
<body>

<!-- Step 1: JSON data source -->
<script id="people-data" type="application/json">
{
  "Persons": {
    "Person": [
      {
        "FirstName": "Alice",
        "LastName": "Anderson",
        "Address": {
          "Street": "Maple",
          "Number": "123",
          "City": "Springfield"
        }
      },
      {
        "FirstName": "Bob",
        "LastName": "Baker",
        "Address": {
          "Street": "Oak",
          "Number": "456",
          "City": "Rivertown"
        }
      }
    ]
  }
}
</script>

<!-- Step 2: Handlebars template -->
<script id="table-template" type="text/x-handlebars-template">
<table border="1" data_merge="{{#foreach Persons.Person}}">
  <tr>
    <th scope="col">Person</th>
    <th scope="col">Address</th>
  </tr>
  {{#foreach Persons.Person}}
  <tr>
    <td>{{FirstName}} {{LastName}}</td>
    <td>{{Address.Street}} {{Address.Number}}, {{Address.City}}</td>
  </tr>
  {{/foreach}}
</table>
</script>

<!-- Step 4: Container for the generated table -->
<div id="output"></div>

<!-- Step 3: Load Handlebars, compile, and render -->
<script src="https://cdn.jsdelivr.net/npm/handlebars@4.7.7/dist/handlebars.min.js"></script>
<script>
  const raw = document.getElementById('people-data').textContent;
  const context = JSON.parse(raw);
  const source = document.getElementById('table-template').innerHTML;
  const template = Handlebars.compile(source);
  document.getElementById('output').innerHTML = template(context);
</script>

</body>
</html>
```

**Αναμενόμενο αποτέλεσμα**

Ένας πίνακας δύο γραμμών (συν κεφαλίδα) που εμφανίζει “Alice Anderson” και “Bob Baker” με τις αντίστοιχες διευθύνσεις τους. Η σελίδα λειτουργεί offline, αποδεικνύοντας ότι μπορείτε να **generate table from data** χωρίς κανένα server component.

---

## Συμπέρασμα

Τώρα ξέρετε πώς να **generate table from data** χρησιμοποιώντας ένα πρότυπο Handlebars, **populate table from JSON**, και να δημιουργήσετε **repeat table rows** που σχηματίζουν έναν **dynamic HTML table**. Το μοτίβο κλιμακώνεται σε μεγαλύτερα σύνολα δεδομένων, ένθετες δομές και ζωντανές κλήσεις API, παρέχοντάς σας μια ισχυρή βάση για οποιοδήποτε client‑side reporting ή admin UI.

**Επόμενα βήματα**

* Εξερευνήστε Handlebars helpers για μορφοποίηση ημερομηνιών ή αριθμών.
* Συνδυάστε αυτή την προσέγγιση με CSS Grid ή Flexbox για responsive διατάξεις πινάκων.
* Ενσωματώστε βιβλιοθήκες σελιδοποίησης ή ταξινόμησης για να διαχειριστείτε πολύ μεγάλα σύνολα δεδομένων.

Μη διστάσετε να πειραματιστείτε με διαφορετικά σχήματα JSON, να προσθέσετε υπό‑συνθήκες στήλες, ή να αντικαταστήσετε το Handlebars με άλλη μηχανή templating – οι νέες σας δεξιότητες θα σας επιτρέψουν να χτίζετε γρήγορα και αξιόπιστα ευέλικτες, data‑driven διεπαφές.

## Τι πρέπει να μάθετε στη συνέχεια;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}