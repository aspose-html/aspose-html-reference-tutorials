---
category: general
date: 2026-08-03
description: Converta HTML para Markdown usando Python. Aprenda como extrair links
  de HTML e extrair parágrafos de HTML em uma única conversão eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- extract paragraphs from html
language: pt
lastmod: 2026-08-03
og_description: Converta HTML para Markdown em Python com um exemplo conciso que mostra
  como extrair links do HTML e extrair parágrafos do HTML ao salvar o resultado como
  um arquivo Markdown.
og_image_alt: Screenshot of Python code converting an HTML file to Markdown with selected
  links and paragraphs
og_title: Converter HTML para Markdown em Python – guia completo de extração
schemas:
- author: GroupDocs
  dateModified: '2026-08-03'
  description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  headline: Convert HTML to Markdown Python – extract links & paragraphs
  type: TechArticle
- description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  name: Convert HTML to Markdown Python – extract links & paragraphs
  steps:
  - name: Load the HTML document you want to convert
    text: '```python from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions,
      Converter'
  - name: Create a feature set that includes only the elements you need
    text: '```python # Instantiate the feature collection. selected_features = MarkdownSaveOptions.Features()'
  - name: Attach the feature set to the Markdown save options
    text: '```python md_options = MarkdownSaveOptions() md_options.features = selected_features
      ```'
  - name: Perform the conversion and save the result as a Markdown file
    text: '```python output_path = "YOUR_DIRECTORY/links_and_paragraphs.md" Converter.convert_html(html_doc,
      md_options, output_path) print(f"Conversion complete. Markdown saved to {output_path}")
      ```'
  type: HowTo
tags:
- HTML conversion
- Markdown
- Python
title: Converter HTML para Markdown em Python – extrair links e parágrafos
url: /pt/python/general/convert-html-to-markdown-python-extract-links-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter HTML para Markdown Python – extrair links e parágrafos

Se você precisa **converter HTML para Markdown**, este tutorial mostra uma maneira prática de fazer isso em Python enquanto extrai seletivamente **links do HTML** e **parágrafos do HTML**. Você verá um exemplo completo e executável que salva o conteúdo filtrado como um arquivo Markdown limpo.

Converter HTML para Markdown é uma etapa comum quando você deseja documentação leve, versionada, conteúdo para sites estáticos ou simplesmente uma representação em texto puro de uma página web. Ao final deste guia você terá um script que:

1. Carrega um documento HTML a partir do disco.  
2. Configura um conjunto de recursos que mantém apenas links e elementos de parágrafo.  
3. Executa a conversão usando o GroupDocs Conversion SDK para Python.  
4. Grava o resultado em um arquivo `.md`.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

| Requisito | Por que é importante |
|-----------|----------------------|
| Python 3.9+ | O SDK tem como alvo versões modernas do Python. |
| Pacote `groupdocs-conversion` | Fornece as classes `HTMLDocument`, `MarkdownSaveOptions` e `Converter` usadas no exemplo. |
| Um arquivo HTML para teste (por exemplo, `sample.html`) | A fonte que você converterá. |

Instale o SDK com pip:

```bash
pip install groupdocs-conversion
```

> **Dica profissional:** Use um ambiente virtual (`python -m venv .venv`) para manter as dependências isoladas.

## Converter HTML para Markdown com Python

O núcleo da conversão está em alguns passos simples. Cada passo é explicado abaixo, e o script completo aparece ao final do artigo.

### Etapa 1: Carregar o documento HTML que você deseja converter

```python
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, Converter

# Replace YOUR_DIRECTORY with the path that contains your HTML file.
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*Por que este passo?*  
`HTMLDocument` analisa o arquivo de origem e constrói uma representação DOM interna que o conversor pode usar. Sem carregar o documento primeiro, o SDK não tem nada para processar.

### Etapa 2: Criar um conjunto de recursos que inclua apenas os elementos que você precisa

```python
# Instantiate the feature collection.
selected_features = MarkdownSaveOptions.Features()

# Keep only hyperlinks.
selected_features.add(MarkdownSaveOptions.Features.LINK)

# Keep only paragraph tags.
selected_features.add(MarkdownSaveOptions.Features.PARAGRAPH)
```

*Por que adicionamos esses recursos*  
`MarkdownSaveOptions.Features` funciona como um filtro. Ao adicionar `LINK` e `PARAGRAPH` informamos ao conversor para **extrair links do HTML** e **extrair parágrafos do HTML**, ignorando imagens, tabelas, scripts e outras marcações que você pode não precisar no Markdown final.

### Etapa 3: Anexar o conjunto de recursos às opções de salvamento em Markdown

```python
md_options = MarkdownSaveOptions()
md_options.features = selected_features
```

*Por que este passo?*  
`MarkdownSaveOptions` contém todas as preferências de conversão. Atribuir o `selected_features` previamente construído garante que a conversão respeite nossa configuração de filtro.

### Etapa 4: Executar a conversão e salvar o resultado como um arquivo Markdown

```python
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert_html(html_doc, md_options, output_path)
print(f"Conversion complete. Markdown saved to {output_path}")
```

*Por que chamamos `convert_html`*  
`Converter.convert_html` é o ponto de entrada do SDK para transformações de HTML → Markdown. Ele lê o `HTMLDocument`, aplica `md_options` e grava a saída filtrada em `output_path`.

#### Saída esperada

O arquivo resultante `links_and_paragraphs.md` conterá apenas representações Markdown de hyperlinks e texto de parágrafos, por exemplo:

```markdown
[Visit the homepage](https://example.com)

This is the first paragraph of the article, describing the main topic.

Another paragraph with more details.
```

Todos os demais elementos HTML, como `<img>`, `<table>` ou `<script>`, são omitidos, mantendo o arquivo leve e fácil de editar.

## Extrair links do HTML (aprofundamento opcional)

Se o seu objetivo é **apenas extrair links do HTML** descartando todo o resto, você pode simplificar o conjunto de recursos:

```python
link_only_features = MarkdownSaveOptions.Features()
link_only_features.add(MarkdownSaveOptions.Features.LINK)

md_options.features = link_only_features
```

Executar a conversão com esta configuração produz um arquivo Markdown onde cada link aparece em sua própria linha, por exemplo:



## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Converter HTML para Markdown no Aspose.HTML para Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Converter HTML para Markdown em .NET com Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Como Converter HTML para PDF em Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}