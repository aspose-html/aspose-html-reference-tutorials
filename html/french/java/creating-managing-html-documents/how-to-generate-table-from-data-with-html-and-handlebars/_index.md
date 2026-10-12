---
category: general
date: 2026-10-12
description: Apprenez à générer un tableau à partir de données et à le remplir à partir
  de JSON en utilisant Handlebars. Guide étape par étape pour répéter les lignes de
  tableau dans des tableaux HTML dynamiques.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: fr
lastmod: 2026-10-12
og_description: Générez un tableau à partir de données et remplissez-le à partir de
  JSON en utilisant Handlebars. Suivez ce tutoriel pour créer des tableaux HTML dynamiques
  avec des lignes de tableau répétées.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Générer un tableau à partir de données avec Handlebars – guide complet
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
title: Comment générer un tableau à partir de données avec HTML et Handlebars
url: /fr/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment générer un tableau à partir de données avec HTML et Handlebars

Si vous devez **générer un tableau à partir de données** dans une page web, ce tutoriel vous montre exactement comment faire. En utilisant une simple boucle Handlebars, vous pouvez **remplir le tableau à partir de JSON**, créer des **lignes de tableau répétées**, et obtenir un **tableau HTML dynamique** qui se met à jour chaque fois que la source change.

Dans les quelques minutes qui suivent, vous verrez un exemple complet et exécutable, comprendrez pourquoi chaque élément est important, et apprendrez à adapter le modèle à des scénarios plus complexes tels que des colonnes conditionnelles ou des objets imbriqués.

## Ce que vous allez créer

Nous créerons un tableau HTML qui :

* Lit une charge JSON contenant une liste de personnes.
* Répète une ligne de tableau pour chaque personne (`repeat table rows`).
* Insère le prénom, le nom de famille et l’adresse de chaque personne dans les cellules appropriées.
* Fonctionne sans aucun rendu côté serveur — tout le processus se déroule dans le navigateur.

**Pré‑requis**

* Connaissances de base en HTML et JavaScript.
* Un navigateur moderne (Chrome, Edge, Firefox ou Safari).
* Handlebars.js — nous le chargerons depuis un CDN, aucune chaîne de construction n’est requise.

---

## Étape 1 : Préparer la source de données JSON

La première étape consiste à définir un objet JavaScript qui imite le JSON que vous recevriez d’une API. Handlebars fonctionne avec des objets simples, vous pouvez donc intégrer les données directement dans une balise `<script>` à des fins de démonstration.

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

**Pourquoi c’est important** — En conservant les données dans un élément `<script>` séparé, vous pouvez facilement le remplacer plus tard par un appel AJAX réel. La structure (`Persons.Person`) correspond au chemin utilisé dans le bloc Handlebars `{{#foreach Persons.Person}}`, ce qui est essentiel pour **remplir le tableau à partir de JSON**.

---

## Étape 2 : Écrire le modèle Handlebars qui répète les lignes

Ensuite, créez un bloc `<script type="text/x-handlebars-template">` contenant le balisage du tableau. Handlebars remplacera les espaces réservés par les valeurs réelles et répétera le `<tr>` pour chaque personne.

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

**Explication des parties clés**

* `{{#foreach Persons.Person}}` indique à Handlebars de **répéter les lignes du tableau** pour chaque entrée du tableau `Persons.Person`.
* Les expressions `{{FirstName}} {{LastName}}` et `{{Address.*}}` extraient les valeurs de l’élément de tableau courant.
* Envelopper tout le tableau dans un attribut `data_merge` est optionnel ; cela peut être utile pour un traitement en aval ou pour des sélecteurs CSS.

---

## Étape 3 : Charger Handlebars et compiler le modèle

Nous allons récupérer Handlebars depuis un CDN, analyser le JSON, compiler le modèle et injecter le HTML final dans la page.

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

**Pourquoi compiler à l’exécution ?** — Compiler le modèle une fois et le réutiliser garde la page rapide, surtout lorsque les données changent fréquemment. Ce modèle rend également trivial le **remplissage du tableau à partir de JSON** plusieurs fois sans recharger la page.

---

## Étape 4 : Réserver un conteneur pour le tableau généré

Ajoutez un `<div>` de remplacement où le tableau dynamique apparaîtra. Cela maintient le balisage propre et sépare les préoccupations entre la mise en page statique et le contenu généré.

```html
<div id="output"></div>
```

Lorsque le script de l’Étape 3 s’exécute, le `<div id="output">` contiendra un élément `<table>` entièrement formé, prêt à être stylisé ou manipulé davantage.

---

## Étape 5 : Vérifier le rendu et styliser le tableau (facultatif)

Ouvrez la page dans un navigateur et vous devriez voir un tableau similaire à celui ci‑dessous :

![Capture d’écran montrant le tableau généré à partir de données](image.png "Capture d’écran montrant le tableau généré à partir de données")

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

**Style optionnel** — Si vous souhaitez un rendu plus épuré, ajoutez quelques règles CSS :

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Gestion des cas limites et variations courantes

### 1. Jeux de données vides

Si le tableau JSON est vide, Handlebars affichera toujours la ligne d’en‑tête mais aucune ligne de données. Pour afficher un message convivial, enveloppez le tableau dans un bloc conditionnel :

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Boucles imbriquées (par ex., plusieurs adresses par personne)

Lorsqu’une personne peut avoir plusieurs adresses, vous pouvez imbriquer un autre `{{#foreach}}` à l’intérieur de la ligne :

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

### 3. Utiliser une API réelle

Remplacez le `<script id="people-data">` statique par un appel `fetch` :

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Cela montre la même technique de **lignes de tableau dynamiques** tout en récupérant des données en temps réel.

### 4. Considérations d’accessibilité

* Ajoutez `scope="col"` aux éléments `<th>`.
* Utilisez `<caption>` pour décrire l’objectif du tableau.
* Assurez‑vous d’un contraste de couleur suffisant si vous appliquez du CSS personnalisé.

---

## Exemple complet, exécutable

Copiez le bloc suivant dans un fichier `index.html` et ouvrez‑le dans un navigateur. La page **générera un tableau à partir de données**, **remplira le tableau à partir de JSON**, et répétera les lignes automatiquement.

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

**Résultat attendu**

Un tableau de deux lignes (plus l’en‑tête) affichant « Alice Anderson » et « Bob Baker » avec leurs adresses respectives. La page fonctionne hors ligne, prouvant que vous pouvez **générer un tableau à partir de données** sans aucun composant serveur.

---

## Conclusion

Vous savez maintenant comment **générer un tableau à partir de données** en utilisant un modèle Handlebars, **remplir le tableau à partir de JSON**, et créer des **lignes de tableau répétées** qui forment un **tableau HTML dynamique**. Le modèle s’adapte à des ensembles de données plus volumineux, à des structures imbriquées et à des appels d’API en direct, vous offrant une base solide pour tout reporting côté client ou interface d’administration.

**Prochaines étapes**

* Explorez les helpers Handlebars pour formater les dates ou les nombres.
* Combinez cette approche avec CSS Grid ou Flexbox pour des mises en page de tableau réactives.
* Intégrez des bibliothèques de pagination ou de tri pour gérer des ensembles de données très volumineux.

N’hésitez pas à expérimenter avec différentes formes de JSON, à ajouter des colonnes conditionnelles, ou à remplacer Handlebars par un autre moteur de templates — vos nouvelles compétences vous permettront de créer rapidement des interfaces flexibles et pilotées par les données.

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Create HTML Document with Java – Fetch JSON and Generate Content](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Data Handling and Stream Management in Aspose.HTML for Java](/html/english/java/data-handling-stream-management/)
- [How to Load HTML in Java – Step‑by‑Step Guide](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}