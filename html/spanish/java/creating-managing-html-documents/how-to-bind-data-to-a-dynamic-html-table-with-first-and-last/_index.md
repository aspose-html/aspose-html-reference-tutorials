---
category: general
date: 2026-09-07
description: cómo enlazar datos en una tabla HTML dinámica – aprende a generar filas
  de tabla y a rellenar los campos de nombre y apellido de manera eficiente
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: es
lastmod: 2026-09-07
og_description: cómo vincular datos en una tabla HTML dinámica. Este tutorial muestra
  cómo generar filas de tabla, mostrar el nombre y el apellido, y rellenar las filas
  de la tabla con JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Cómo enlazar datos a una tabla HTML dinámica – guía paso a paso
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
title: Cómo enlazar datos a una tabla HTML dinámica con columnas de nombre y apellido
url: /es/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo enlazar datos a una tabla HTML dinámica con columnas de nombre y apellido

Si necesitas **cómo enlazar datos** en una tabla que crece con cada registro, esta guía muestra una solución completa. Verás cómo generar una tabla HTML dinámica, rellenar filas de tabla y mostrar el nombre y apellido de cada persona sin escribir marcado repetitivo.

El ejemplo usa una sintaxis de plantillas ligera que funciona en cualquier navegador moderno, pero los conceptos se aplican igualmente a Handlebars, Mustache o motores del lado del servidor. Al final del tutorial podrás copiar el código a tu proyecto y comenzar a enlazar datos al instante.

## Qué cubre este tutorial

* Cómo estructurar una fuente de datos que contiene múltiples personas  
* Cómo crear una plantilla de tabla reutilizable que se repite para cada entrada  
* Cómo enlazar los datos y generar el marcado HTML final  
* Trampas comunes al poblar filas de tabla y cómo evitarlas  

No se requieren bibliotecas externas, aunque el mismo patrón funciona con los frameworks de plantillas más populares. El único requisito previo es conocimientos básicos de HTML y JavaScript.

## Requisitos previos

* Un navegador moderno (Chrome, Edge, Firefox o Safari)  
* Un editor para archivos HTML/JavaScript  
* Opcional: un archivo JSON o un objeto JavaScript que represente la colección de personas  

## Paso 1: Definir la fuente de datos

Primero, crea un objeto JavaScript que refleje la estructura usada en la plantilla. Cada persona tiene un nombre, un apellido y un objeto de dirección.

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

**Por qué es importante:** La jerarquía del objeto (`Persons.Person`) coincide con el bucle `{{#foreach Persons.Person}}` en la plantilla, lo que permite al motor iterar automáticamente sobre cada entrada.

## Paso 2: Escribir la plantilla de tabla con un bloque de repetición

La plantilla a continuación usa una sintaxis estilo Mustache (`{{#foreach}}`) para repetir el `<tr>` por cada persona. Coloca la plantilla dentro de una etiqueta `<script type="text/template">` para que el navegador la ignore hasta que la proceses.

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

**Por qué es importante:** La directiva `{{#foreach Persons.Person}}` indica al motor que repita todo lo que está entre las etiquetas de apertura y cierre para cada objeto persona. Dentro de la fila puedes referenciar cualquier propiedad (`{{FirstName}}`, `{{LastName}}`, etc.) para **poblar filas de tabla** dinámicamente.

## Paso 3: Implementar una pequeña función de renderizado

Como el tutorial debe ser autosuficiente, escribiremos un renderizador mínimo que sustituya los marcadores estilo Mustache por valores reales. La función recorre el objeto de datos, expande el bloque de repetición e inyecta el HTML final en la página.

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

**Por qué es importante:** El renderizador demuestra **cómo generar la tabla** programáticamente sin cargar una biblioteca completa. También aclara la transformación de la plantilla al HTML final, lo que te ayuda a adaptar el código a otros motores de plantillas más adelante.

## Paso 4: Añadir un marcador donde aparecerá la tabla generada

Crea un `<div>` vacío que el script rellenará después del renderizado.

```html
<div id="output"></div>
```

Cuando la página se cargue, el script reemplazará el contenido de este `<div>` con la tabla completamente poblada.

## Paso 5: Verificar el resultado

Abre el archivo HTML en un navegador. Deberías ver una tabla que lista el nombre completo y la dirección de cada persona:

| Persona          | Dirección                         |
|------------------|-----------------------------------|
| Alice Johnson    | Maple 12A, Springfield            |
| Bob Smith        | Oak 34B, Riverdale                |

Si añades más objetos al arreglo `data.Persons.Person`, la tabla crecerá automáticamente, cumpliendo con el requisito de **poblar filas de tabla**.

## Consejo profesional: manejo de colecciones vacías

Cuando el arreglo de datos está vacío, el renderizador actualmente genera solo el encabezado de la tabla. Para ofrecer una experiencia de usuario más clara, añade una protección:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Este pequeño cambio evita que aparezca una tabla vacía y brinda retroalimentación inmediata al usuario.

## Variaciones comunes y casos límite

| Situación                                 | Ajuste                                                                 |
|-------------------------------------------|------------------------------------------------------------------------|
| Usar un motor del lado del servidor (p. ej., Handlebars) | Reemplazar `renderTemplate` personalizado por `Handlebars.compile` y pasar el mismo objeto de datos. |
| Necesidad de ordenar filas alfabéticamente | Ordenar `data.Persons.Person` antes de llamar a `renderTemplate`. |
| Añadir una columna para número de teléfono | Extender el `<tr>` con `<td>{{Phone}}</td>` e incluir `Phone` en cada objeto persona. |
| Conjuntos de datos grandes (cientos de filas) | Renderizar filas en bloques o usar desplazamiento virtual para mantener la UI responsiva. |

## Ejemplo completo funcionando

A continuación tienes el archivo HTML completo que puedes copiar‑pegar en `index.html`. Contiene todas las piezas discutidas anteriormente.

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

**Salida esperada**

La página muestra una tabla con dos filas, cada una exhibiendo el nombre completo y la dirección formateada de una persona. Añadir más objetos al arreglo `Person` agrega automáticamente nuevas filas, demostrando **cómo generar elementos de tabla** a partir de datos.

## Conclusión

Ahora sabes **cómo enlazar datos** a una **tabla HTML dinámica**, generar filas para cada registro y mostrar los valores de nombre y apellido junto a la dirección.

## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funcionalidades adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Enable JavaScript in Aspose HTML – Load HTML & Get Text](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}