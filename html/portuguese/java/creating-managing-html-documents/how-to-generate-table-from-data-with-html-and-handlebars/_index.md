---
category: general
date: 2026-10-12
description: Aprenda a gerar tabelas a partir de dados e a preencher tabelas a partir
  de JSON usando Handlebars. Guia passo a passo para repetir linhas de tabela em tabelas
  HTML dinâmicas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate table from data
- populate table from json
- repeat table rows
- dynamic html table
- dynamic table rows
language: pt
lastmod: 2026-10-12
og_description: Gere a tabela a partir de dados e preencha-a a partir de JSON usando
  Handlebars. Siga este tutorial para criar tabelas HTML dinâmicas com linhas de tabela
  repetidas.
og_image_alt: Screenshot showing generated table from data in a web page
og_title: Gerar tabela a partir de dados com Handlebars – guia completo
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
title: Como gerar tabela a partir de dados com HTML e Handlebars
url: /pt/java/creating-managing-html-documents/how-to-generate-table-from-data-with-html-and-handlebars/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como gerar tabela a partir de dados com HTML e Handlebars

Se você precisa **gerar tabela a partir de dados** em uma página web, este tutorial mostra exatamente como fazer. Usando um loop simples do Handlebars, você pode **preencher tabela a partir de JSON**, criar **linhas de tabela repetidas** e obter uma **tabela HTML dinâmica** completa que se atualiza sempre que a fonte mudar.

Nos próximos minutos você verá um exemplo completo e executável, entenderá por que cada parte é importante e aprenderá a adaptar o padrão para cenários mais complexos, como colunas condicionais ou objetos aninhados.

## O que você vai construir

Criar‑emos uma tabela HTML que:

* Lê um payload JSON contendo uma lista de pessoas.
* Repete uma linha de tabela para cada pessoa (`repeat table rows`).
* Insere o nome, sobrenome e endereço de cada pessoa nas células apropriadas.
* Funciona sem renderização no lado do servidor – todo o processo ocorre no navegador.

**Pré‑requisitos**

* Conhecimento básico de HTML e JavaScript.
* Um navegador moderno (Chrome, Edge, Firefox ou Safari).
* Handlebars.js – vamos carregá‑lo de um CDN, portanto nenhuma ferramenta de build é necessária.

---

## Etapa 1: Preparar a fonte de dados JSON

O primeiro passo é definir um objeto JavaScript que imita o JSON que você receberia de uma API. Handlebars funciona com objetos simples, então você pode incorporar os dados diretamente em uma tag `<script>` para fins de demonstração.

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

**Por que isso importa** – Ao manter os dados em um elemento `<script>` separado, você pode substituí‑los facilmente por uma chamada AJAX real mais tarde. A estrutura (`Persons.Person`) corresponde ao caminho usado no bloco Handlebars `{{#foreach Persons.Person}}`, o que é essencial para **preencher tabela a partir de JSON**.

---

## Etapa 2: Escrever o template Handlebars que repete linhas

Em seguida, crie um bloco `<script type="text/x-handlebars-template">` que contém a marcação da tabela. Handlebars substituirá os placeholders pelos valores reais e repetirá o `<tr>` para cada pessoa.

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

**Explicação das partes principais**

* `{{#foreach Persons.Person}}` indica ao Handlebars para **repeat table rows** para cada entrada no array `Persons.Person`.
* As expressões `{{FirstName}} {{LastName}}` e `{{Address.*}}` extraem valores do elemento atual do array.
* Envolver toda a tabela em um atributo `data_merge` é opcional; pode ser útil para processamento posterior ou seletores CSS.

---

## Etapa 3: Carregar Handlebars e compilar o template

Vamos puxar o Handlebars de um CDN, analisar o JSON, compilar o template e injetar o HTML final na página.

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

**Por que compilar em tempo de execução?** – Compilar o template uma única vez e reutilizá‑lo mantém a página rápida, especialmente quando os dados mudam com frequência. Esse padrão também torna trivial **preencher tabela a partir de JSON** várias vezes sem recarregar a página.

---

## Etapa 4: Reservar um contêiner para a tabela gerada

Adicione um placeholder `<div>` onde a tabela dinâmica aparecerá. Isso mantém a marcação limpa e separa as preocupações entre layout estático e conteúdo gerado.

```html
<div id="output"></div>
```

Quando o script da Etapa 3 for executado, o `<div id="output">` conterá um elemento `<table>` totalmente formado, pronto para estilização ou manipulação adicional.

---

## Etapa 5: Verificar a saída e estilizar a tabela (opcional)

Abra a página em um navegador e você deverá ver uma tabela como a abaixo:

![Captura de tela mostrando tabela gerada a partir de dados](image.png "Captura de tela mostrando tabela gerada a partir de dados")

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

**Estilização opcional** – Se quiser um visual mais limpo, adicione algumas regras CSS:

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
```

---

## Tratamento de casos de borda e variações comuns

### 1. Conjuntos de dados vazios

Se o array JSON estiver vazio, Handlebars ainda renderizará a linha de cabeçalho, mas nenhuma linha de dados. Para exibir uma mensagem amigável, envolva a tabela em um bloco condicional:

```handlebars
{{#if Persons.Person.length}}
  {{!-- existing table markup --}}
{{else}}
  <p>No persons found.</p>
{{/if}}
```

### 2. Loops aninhados (por exemplo, múltiplos endereços por pessoa)

Quando uma pessoa pode ter vários endereços, você pode aninhar outro `{{#foreach}}` dentro da linha:

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

### 3. Usando uma API real

Substitua o `<script id="people-data">` estático por uma chamada fetch:

```javascript
fetch('/api/persons')
  .then(r => r.json())
  .then(context => {
    const html = template(context);
    document.getElementById('output').innerHTML = html;
  });
```

Isso demonstra a mesma técnica de **dynamic table rows** enquanto obtém dados ao vivo.

### 4. Considerações de acessibilidade

* Adicione `scope="col"` aos elementos `<th>`.
* Use `<caption>` para descrever o propósito da tabela.
* Garanta contraste de cores suficiente se você aplicar CSS personalizado.

---

## Exemplo completo e executável

Copie o bloco a seguir para um arquivo `index.html` e abra-o em um navegador. A página **gerará tabela a partir de dados**, **preencherá tabela a partir de JSON** e repetirá as linhas automaticamente.

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

Uma tabela de duas linhas (mais o cabeçalho) mostrando “Alice Anderson” e “Bob Baker” com seus respectivos endereços. A página funciona offline, provando que você pode **gerar tabela a partir de dados** sem nenhum componente de servidor.

---

## Conclusão

Agora você sabe como **gerar tabela a partir de dados** usando um template Handlebars, **preencher tabela a partir de JSON** e criar **repeat table rows** que formam uma **tabela HTML dinâmica**. O padrão escala para conjuntos de dados maiores, estruturas aninhadas e chamadas de API ao vivo, oferecendo uma base robusta para qualquer relatório ou UI administrativa do lado do cliente.

**Próximos passos**

* Explore os helpers do Handlebars para formatar datas ou números.
* Combine esta abordagem com CSS Grid ou Flexbox para layouts de tabela responsivos.
* Integre bibliotecas de paginação ou ordenação para lidar com conjuntos de dados muito grandes.

Sinta‑se à vontade para experimentar diferentes formatos de JSON, adicionar colunas condicionais ou trocar Handlebars por outro motor de templates – suas novas habilidades permitirão construir interfaces flexíveis e orientadas a dados rapidamente e de forma confiável.

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar documento HTML com Java – Buscar JSON e gerar conteúdo](/html/english/java/creating-managing-html-documents/create-html-document-with-java-fetch-json-and-generate-conte/)
- [Manipulação de Dados e Gerenciamento de Streams no Aspose.HTML para Java](/html/english/java/data-handling-stream-management/)
- [Como carregar HTML em Java – Guia passo a passo](/html/english/java/creating-managing-html-documents/how-to-load-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}