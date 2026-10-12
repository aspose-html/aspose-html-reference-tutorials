---
category: general
date: 2026-10-12
description: Aprende a generar una tabla a partir de datos y a rellenarla con JSON
  usando Handlebars. Guía paso a paso para repetir filas de tabla en tablas HTML dinámicas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: es
lastmod: 2026-10-12
og_description: Genera una tabla a partir de datos y rellena la tabla desde JSON usando
  Handlebars. Sigue este tutorial para crear tablas HTML dinámicas con filas de tabla
  repetidas.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Genera una tabla a partir de datos con Handlebars – guía completa
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
title: Cómo generar una tabla a partir de datos con HTML y Handlebars
url: /es/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo generar una tabla a partir de datos con HTML y Handlebars

Si necesitas **generar tabla a partir de datos** en una página web, este tutorial te muestra exactamente cómo. Usando un bucle simple de Handlebars puedes **poblar tabla desde JSON**, crear **filas de tabla repetidas**, y obtener una **tabla HTML dinámica** que se actualiza cada vez que la fuente cambia.

En los próximos minutos verás un ejemplo completo y ejecutable, entenderás por qué cada parte es importante y aprenderás cómo adaptar el patrón a escenarios más complejos, como columnas condicionales u objetos anidados.

## Lo que construirás

Crearemos una tabla HTML que:

* Lee una carga JSON que contiene una lista de personas.
* Repite una fila de tabla para cada persona (`repeat table rows`).
* Inserta el nombre, apellido y dirección de cada persona en las celdas correspondientes.
* Funciona sin renderizado del lado del servidor – todo el proceso ocurre en el navegador.

**Requisitos previos**

* Conocimientos básicos de HTML y JavaScript.
* Un navegador moderno (Chrome, Edge, Firefox o Safari).
* Handlebars.js – lo cargaremos desde un CDN, por lo que no se requieren herramientas de compilación.

---

## Paso 1: Preparar la fuente de datos JSON

El primer paso es definir un objeto JavaScript que imite el JSON que recibirías de una API. Handlebars funciona con objetos simples, por lo que puedes incrustar los datos directamente en una etiqueta `<script>` para fines de demostración.

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

**Por qué es importante** – Al mantener los datos en un elemento `<script>` separado, puedes cambiarlo fácilmente por una llamada AJAX real más adelante. La estructura (`Persons.Person`) coincide con la ruta usada en el bloque Handlebars `{{#foreach Persons.Person}}`, lo cual es esencial para **populate table from JSON**.

---

## Paso 2: Escribir la plantilla Handlebars que repite filas

A continuación, crea un bloque `<script type="text/x-handlebars-template">` que contenga el marcado de la tabla. Handlebars reemplazará los marcadores de posición con los valores reales y repetirá el `<tr>` para cada persona.

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

**Explicación de las partes clave**

* `{{#foreach Persons.Person}}` indica a Handlebars que **repeat table rows** para cada entrada en el arreglo `Persons.Person`.
* Las expresiones `{{FirstName}} {{LastName}}` y `{{Address.*}}` extraen valores del elemento actual del arreglo.
* Envolver toda la tabla en un atributo `data_merge` es opcional; puede ser útil para procesamiento posterior o selectores CSS.

---

## Paso 3: Cargar Handlebars y compilar la plantilla

Cargaremos Handlebars desde un CDN, analizaremos el JSON, compilaremos la plantilla e inyectaremos el HTML final en la página.

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

**¿Por qué compilar en tiempo de ejecución?** – Compilar la plantilla una vez y reutilizarla mantiene la página rápida, especialmente cuando los datos cambian con frecuencia. Este patrón también hace trivial **populate table from JSON** varias veces sin recargar la página.

---

## Paso 4: Reservar un contenedor para la tabla generada

Añade un `<div>` de marcador de posición donde aparecerá la tabla dinámica. Esto mantiene el marcado limpio y separa las preocupaciones entre el diseño estático y el contenido generado.

```html
<div id="output"></div>
```

Cuando se ejecute el script del Paso 3, el `<div id="output">` contendrá un elemento `<table>` completamente formado, listo para estilizar o manipular más.

---

## Paso 5: Verificar la salida y estilizar la tabla (opcional)

Abre la página en un navegador y deberías ver una tabla como la siguiente:

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

**Estilizado opcional** – Si deseas un aspecto más limpio, agrega algunas reglas CSS:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Manejo de casos límite y variaciones comunes

### 1. Conjuntos de datos vacíos

Si el arreglo JSON está vacío, Handlebars aún renderizará la fila de encabezado pero no filas de datos. Para mostrar un mensaje amigable, envuelve la tabla en un bloque condicional:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Bucles anidados (p. ej., varias direcciones por persona)

Cuando una persona puede tener varias direcciones, puedes anidar otro `{{#foreach}}` dentro de la fila:

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

### 3. Usar una API real

Reemplaza el `<script id="people-data">` estático con una llamada fetch:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Esto demuestra la misma técnica de **dynamic table rows** mientras se obtienen datos en vivo.

### 4. Consideraciones de accesibilidad

* Añade `scope="col"` a los elementos `<th>`.
* Usa `<caption>` para describir el propósito de la tabla.
* Asegura un contraste de color suficiente si aplicas CSS personalizado.

---

## Ejemplo completo y ejecutable

Copia el siguiente bloque en un archivo `index.html` y ábrelo en un navegador. La página **generará tabla a partir de datos**, **poblará tabla desde JSON**, y repetirá filas automáticamente.

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

**Resultado esperado**

Una tabla de dos filas (más encabezado) que muestra “Alice Anderson” y “Bob Baker” con sus respectivas direcciones. La página funciona sin conexión, demostrando que puedes **generate table from data** sin ningún componente de servidor.

---

## Conclusión

Ahora sabes cómo **generate table from data** usando una plantilla Handlebars, **populate table from JSON**, y crear **repeat table rows** que forman una **dynamic HTML table**. El patrón escala a conjuntos de datos más grandes, estructuras anidadas y llamadas a API en vivo, dándote una base robusta para cualquier informe del lado del cliente o UI de administración.

**Próximos pasos**

* Explora los helpers de Handlebars para formatear fechas o números.
* Combina este enfoque con CSS Grid o Flexbox para diseños de tabla responsivos.
* Integra bibliotecas de paginación o ordenamiento para manejar conjuntos de datos muy grandes.

Siéntete libre de experimentar con diferentes estructuras JSON, añadir columnas condicionales, o cambiar Handlebars por otro motor de plantillas—tus nuevas habilidades te permitirán crear interfaces flexibles y basadas en datos rápidamente y de forma confiable.

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear documento HTML con Java – Obtener JSON y generar contenido](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Manejo de datos y gestión de flujos en Aspose.HTML para Java](/html/english/java/data-handling-stream-management/)
- [Cómo cargar HTML en Java – Guía paso a paso](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}