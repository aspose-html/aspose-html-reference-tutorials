---
category: general
date: 2026-09-07
description: como vincular dados em uma tabela HTML dinâmica – aprenda a gerar linhas
  de tabela e preencher os campos de nome e sobrenome de forma eficiente
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to bind data
- dynamic html table
- first and last name
- how to generate table
- populate table rows
language: pt
lastmod: 2026-09-07
og_description: como vincular dados em uma tabela HTML dinâmica. este tutorial mostra
  como gerar linhas de tabela, exibir nome e sobrenome e preencher linhas de tabela
  com JavaScript.
og_image_alt: Screenshot of a dynamic HTML table populated with first and last names
  after binding data
og_title: Como vincular dados a uma tabela HTML dinâmica – guia passo a passo
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
title: Como vincular dados a uma tabela HTML dinâmica com colunas de nome e sobrenome
url: /pt/java/creating-managing-html-documents/how-to-bind-data-to-a-dynamic-html-table-with-first-and-last/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como vincular dados a uma tabela HTML dinâmica com colunas de nome e sobrenome

Se você precisa **how to bind data** em uma tabela que cresce a cada registro, este guia mostra uma solução completa. Você verá como gerar uma tabela HTML dinâmica, preencher linhas da tabela e exibir o nome e sobrenome de cada pessoa sem escrever marcação repetitiva.

O exemplo usa uma sintaxe de template leve que funciona em qualquer navegador moderno, mas os conceitos se aplicam ao Handlebars, Mustache ou a mecanismos server‑side semelhantes. Ao final do tutorial você pode copiar o código para o seu projeto e começar a vincular dados instantaneamente.

## O que este tutorial cobre

* Como estruturar uma fonte de dados que contém várias pessoas  
* Como criar um template de tabela reutilizável que se repete para cada entrada  
* Como vincular os dados e gerar o markup HTML final  
* Armadilhas comuns ao preencher linhas de tabela e como evitá‑las  

Nenhuma biblioteca externa é necessária, embora o mesmo padrão funcione com frameworks de templating populares. O único pré‑requisito é conhecimento básico de HTML e JavaScript.

## Pré‑requisitos

* Um navegador moderno (Chrome, Edge, Firefox ou Safari)  
* Um editor para arquivos HTML/JavaScript  
* Opcional: um arquivo JSON ou objeto JavaScript que represente a coleção de pessoas  

## Etapa 1: Definir a fonte de dados

Primeiro, crie um objeto JavaScript que espelhe a estrutura usada no template. Cada pessoa tem um nome, sobrenome e um objeto de endereço.

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

**Por que isso importa:** A hierarquia do objeto (`Persons.Person`) corresponde ao loop `{{#foreach Persons.Person}}` no template, permitindo que o motor itere sobre cada entrada automaticamente.

## Etapa 2: Escrever o template da tabela com um bloco de repetição

O template abaixo usa uma sintaxe simples no estilo Mustache (`{{#foreach}}`) para repetir o `<tr>` para cada pessoa. Coloque o template dentro de uma tag `<script type="text/template">` para que o navegador o ignore até que você o processe.

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

**Por que isso importa:** A diretiva `{{#foreach Persons.Person}}` indica ao motor que repita tudo entre as tags de abertura e fechamento para cada objeto pessoa. Dentro da linha você pode referenciar qualquer propriedade (`{{FirstName}}`, `{{LastName}}`, etc.) para **populate table rows** dinamicamente.

## Etapa 3: Implementar uma pequena função de renderização

Como o tutorial deve ser autocontido, escreveremos um renderizador mínimo que substitui os placeholders no estilo Mustache por valores reais. A função percorre o objeto de dados, expande o bloco de repetição e injeta o HTML final na página.

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

**Por que isso importa:** O renderizador demonstra **how to generate table** markup programaticamente sem precisar de uma biblioteca completa. Ele também esclarece a transformação do template para o HTML final, o que ajuda a adaptar o código a outros motores de templating no futuro.

## Etapa 4: Adicionar um placeholder onde a tabela gerada aparecerá

Crie um `<div>` vazio que o script preencherá após a renderização.

```html
<div id="output"></div>
```

Quando a página carregar, o script substitui o conteúdo desse `<div>` pela tabela totalmente preenchida.

## Etapa 5: Verificar o resultado

Abra o arquivo HTML em um navegador. Você deverá ver uma tabela que lista o nome completo e o endereço de cada pessoa:

| Pessoa          | Endereço                         |
|-----------------|---------------------------------|
| Alice Johnson   | Maple 12A, Springfield          |
| Bob Smith       | Oak 34B, Riverdale              |

Se você adicionar mais objetos ao array `data.Persons.Person`, a tabela crescerá automaticamente — atendendo ao requisito de **populate table rows**.

## Dica profissional: lidando com coleções vazias

Quando o array de dados está vazio, o renderizador atualmente gera apenas o cabeçalho da tabela. Para oferecer uma experiência de usuário mais clara, adicione uma proteção:

```javascript
if (items.length === 0) {
  return '<p>No records found.</p>';
}
```

Essa pequena alteração impede que uma tabela vazia apareça e fornece feedback imediato ao usuário.

## Variações comuns e casos de borda

| Situação                               | Ajuste                                                                 |
|----------------------------------------|------------------------------------------------------------------------|
| Usando um motor server‑side (ex.: Handlebars) | Substitua o `renderTemplate` customizado por `Handlebars.compile` e passe o mesmo objeto de dados. |
| Necessidade de ordenar linhas alfabeticamente       | Ordene `data.Persons.Person` antes de chamar `renderTemplate`.               |
| Adicionando uma coluna para número de telefone       | Expanda o `<tr>` com `<td>{{Phone}}</td>` e inclua `Phone` em cada objeto pessoa. |
| Conjuntos de dados grandes (centenas de linhas)     | Renderize linhas em blocos ou use rolagem virtual para manter a UI responsiva. |

## Exemplo completo em funcionamento

Abaixo está o arquivo HTML completo que você pode copiar‑colar em `index.html`. Ele contém todas as peças discutidas acima.

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

**Saída esperada**

A página renderiza uma tabela com duas linhas, cada uma mostrando o nome completo e o endereço formatado de uma pessoa. Adicionar mais objetos ao array `Person` adiciona automaticamente novas linhas — demonstrando **how to generate table** elements a partir dos dados.

## Conclusão

Agora você sabe **how to bind data** a uma **dynamic HTML table**, gerar linhas para cada registro e exibir os valores de nome e sobrenome ao lado do endereço.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Enable JavaScript in Aspose HTML – Load HTML & Get Text](/html/english/java/advanced-usage/how-to-enable-javascript-in-aspose-html-load-html-get-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}