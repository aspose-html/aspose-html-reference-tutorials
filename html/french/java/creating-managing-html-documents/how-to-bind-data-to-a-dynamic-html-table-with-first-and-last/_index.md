---
category: general
date: 2026-09-07
description: Comment lier des données dans un tableau HTML dynamique – apprenez à
  générer des lignes de tableau et à remplir efficacement les champs prénom et nom.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: fr
lastmod: 2026-09-07
og_description: Comment lier des données dans un tableau HTML dynamique. Ce tutoriel
  montre comment générer des lignes de tableau, afficher le prénom et le nom, et remplir
  les lignes du tableau avec JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Comment lier des données à un tableau HTML dynamique – guide étape par étape
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
title: Comment lier des données à un tableau HTML dynamique avec les colonnes prénom
  et nom
url: /fr/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment lier des données à un tableau HTML dynamique avec des colonnes prénom et nom de famille

Si vous avez besoin de **comment lier des données** dans un tableau qui s’agrandit à chaque enregistrement, ce guide propose une solution complète. Vous verrez comment générer un tableau HTML dynamique, remplir les lignes du tableau et afficher le prénom et le nom de chaque personne sans écrire de balisage répétitif.

L’exemple utilise une syntaxe de templating légère qui fonctionne dans n’importe quel navigateur moderne, mais les concepts s’appliquent également à Handlebars, Mustache ou aux moteurs côté serveur. À la fin du tutoriel, vous pourrez copier le code dans votre projet et commencer à lier les données immédiatement.

## Ce que couvre ce tutoriel

* Comment structurer une source de données contenant plusieurs personnes  
* Comment créer un modèle de tableau réutilisable qui se répète pour chaque entrée  
* Comment lier les données et générer le balisage HTML final  
* Pièges courants lors du remplissage des lignes du tableau et comment les éviter  

Aucune bibliothèque externe n’est requise, bien que le même schéma fonctionne avec les frameworks de templating populaires. La seule condition préalable est une connaissance de base en HTML et JavaScript.

## Prérequis

* Un navigateur moderne (Chrome, Edge, Firefox ou Safari)  
* Un éditeur pour les fichiers HTML/JavaScript  
* Facultatif : un fichier JSON ou un objet JavaScript représentant la collection de personnes  

## Étape 1 : Définir la source de données

Tout d’abord, créez un objet JavaScript qui reflète la structure utilisée dans le modèle. Chaque personne possède un prénom, un nom de famille et un objet adresse.

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

**Pourquoi c’est important :** La hiérarchie d’objets (`Persons.Person`) correspond à la boucle `{{#foreach Persons.Person}}` du modèle, ce qui permet au moteur d’itérer automatiquement sur chaque entrée.

## Étape 2 : Écrire le modèle de tableau avec un bloc de répétition

Le modèle ci‑dessous utilise une syntaxe de type Mustache (`{{#foreach}}`) pour répéter le `<tr>` pour chaque personne. Placez le modèle à l’intérieur d’une balise `<script type="text/template">` afin que le navigateur l’ignore jusqu’à ce que vous le traitiez.

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

**Pourquoi c’est important :** La directive `{{#foreach Persons.Person}}` indique au moteur de répéter tout ce qui se trouve entre les balises d’ouverture et de fermeture pour chaque objet personne. À l’intérieur de la ligne, vous pouvez référencer n’importe quelle propriété (`{{FirstName}}`, `{{LastName}}`, etc.) pour **remplir les lignes du tableau** dynamiquement.

## Étape 3 : Implémenter une petite fonction de rendu

Comme le tutoriel doit être autonome, nous allons écrire un rendu minimal qui remplace les espaces réservés de type Mustache par les vraies valeurs. La fonction parcourt l’objet de données, développe le bloc de répétition et injecte le HTML final dans la page.

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

**Pourquoi c’est important :** Le rendu montre **comment générer le tableau** de façon programmatique sans faire appel à une bibliothèque complète. Il clarifie également la transformation du modèle vers le HTML final, ce qui vous aide à adapter le code à d’autres moteurs de templating ultérieurement.

## Étape 4 : Ajouter un espace réservé où le tableau généré apparaîtra

Créez un `<div>` vide que le script remplira après le rendu.

```html
<div id="output"></div>
```

Lorsque la page se charge, le script remplace le contenu de ce `<div>` par le tableau entièrement rempli.

## Étape 5 : Vérifier le résultat

Ouvrez le fichier HTML dans un navigateur. Vous devriez voir un tableau listant le nom complet et l’adresse de chaque personne :

| Personne         | Adresse                         |
|------------------|---------------------------------|
| Alice Johnson    | Maple 12A, Springfield          |
| Bob Smith        | Oak 34B, Riverdale              |

Si vous ajoutez d’autres objets au tableau `data.Persons.Person`, le tableau s’agrandit automatiquement — satisfaisant ainsi l’exigence de **remplir les lignes du tableau**.

## Astuce : gérer les collections vides

Lorsque le tableau de données est vide, le rendu produit actuellement un en‑tête de tableau vide. Pour offrir une meilleure expérience utilisateur, ajoutez une protection :

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Ce petit changement empêche l’affichage d’un tableau vide et fournit un retour immédiat à l’utilisateur.

## Variations courantes et cas limites

| Situation                               | Ajustement                                                                 |
|----------------------------------------|----------------------------------------------------------------------------|
| Utilisation d’un moteur côté serveur (p. ex. Handlebars) | Remplacez le `renderTemplate` personnalisé par `Handlebars.compile` et passez le même objet de données. |
| Besoin de trier les lignes alphabétiquement       | Triez `data.Persons.Person` avant d’appeler `renderTemplate`.               |
| Ajout d’une colonne pour le numéro de téléphone       | Étendez le `<tr>` avec `<td>{{Phone}}</td>` et incluez `Phone` dans chaque objet personne. |
| Jeux de données volumineux (des centaines de lignes)     | Rendre les lignes par blocs ou utiliser le défilement virtuel pour garder l’interface réactive. |

## Exemple complet fonctionnel

Voici le fichier HTML complet que vous pouvez copier‑coller dans `index.html`. Il contient toutes les pièces abordées ci‑dessus.

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

**Résultat attendu**

La page rend un tableau avec deux lignes, chacune affichant le nom complet et l’adresse formatée d’une personne. Ajouter davantage d’objets au tableau `Person` ajoute automatiquement de nouvelles lignes — démontrant **comment générer des éléments de tableau** à partir de données.

## Conclusion

Vous savez maintenant **comment lier des données** à un **tableau HTML dynamique**, générer des lignes pour chaque enregistrement et afficher les valeurs de prénom et de nom de famille aux côtés de l’adresse.

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités d’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment ajouter du CSS – CSS en ligne aux documents HTML dans Aspose.HTML pour Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [Comment modifier l’arbre du document HTML dans Aspose.HTML pour Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Comment activer JavaScript dans Aspose HTML – Charger le HTML & obtenir le texte](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}