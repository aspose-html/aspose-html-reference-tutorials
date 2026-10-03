---
category: general
date: 2026-10-02
description: Converta HTML para Markdown em Python com um exemplo completo. Aprenda
  como salvar HTML como Markdown, escolher formatadores e habilitar recursos específicos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- save html as markdown
- how to convert html
- html to markdown conversion
- html to markdown python
language: pt
lastmod: 2026-10-02
og_description: Converta HTML para Markdown em Python com código prático, opções de
  formatador e flags de recursos. Siga este guia para salvar HTML como Markdown rapidamente.
og_image_alt: Screenshot of Python code converting HTML to Markdown
og_title: Converter HTML para Markdown em Python – tutorial completo
schemas:
- author: GroupDocs
  dateModified: '2026-10-02'
  description: convert HTML to Markdown in Python with a complete example. Learn how
    to save HTML as Markdown, choose formatters, and enable specific features.
  headline: How to convert HTML to Markdown in Python – step‑by‑step guide
  type: TechArticle
- description: convert HTML to Markdown in Python with a complete example. Learn how
    to save HTML as Markdown, choose formatters, and enable specific features.
  name: How to convert HTML to Markdown in Python – step‑by‑step guide
  steps:
  - name: Enabling only the needed features
    text: You can fine‑tune the output by turning on specific feature flags. In this
      example we keep **links** and **paragraphs** while disabling images, tables,
      and other constructs.
  - name: Expected output (`output.md`)
    text: '```markdown # Project Overview'
  - name: Missing or malformed `href` attributes
    text: 'If an `<a>` tag lacks a valid `href`, the converter inserts the link text
      without a URL. To preserve readability, you may want to post‑process the Markdown:'
  - name: Converting large HTML files
    text: 'For multi‑megabyte HTML files, stream the input to avoid loading the entire
      markup into memory:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
title: Como converter HTML para Markdown em Python – guia passo a passo
url: /pt/python/general/how-to-convert-html-to-markdown-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como converter HTML para Markdown em Python – guia passo a passo

Se você precisa **converter HTML para Markdown**, este guia mostra uma solução completa e executável em Python. Você verá como **salvar HTML como Markdown**, escolher o formatador correto e habilitar apenas os recursos que lhe interessam.

Converter HTML para Markdown é uma tarefa comum quando se deseja documentação leve, conteúdo para sites estáticos ou arquivos de texto versionados. Este tutorial cobre tudo, desde a instalação da biblioteca até o tratamento de casos extremos, para que você possa aplicar a técnica a qualquer fonte HTML.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Python 3.8 ou mais recente instalado.
* Acesso ao `pip` para instalar pacotes de terceiros.
* Familiaridade básica com tags HTML e sintaxe Markdown.

Nenhuma dependência de sistema adicional é necessária porque a biblioteca de conversão é pura Python.

## Instalar a biblioteca GroupDocs Conversion

O exemplo de código usa o pacote Python **GroupDocs.Conversion**, que fornece `HTMLDocument`, `MarkdownSaveOptions` e `Converter`. Instale‑o com:

```bash
pip install groupdocs-conversion
```

> **Dica profissional:** Use um ambiente virtual (`python -m venv venv`) para manter o pacote isolado de outros projetos.

## Etapa 1: Criar um `HTMLDocument` a partir de uma string

O primeiro passo é envolver seu HTML bruto em uma instância de `HTMLDocument`. Esse objeto abstrai a origem, seja ela uma string, um arquivo ou uma URL remota.

```python
from groupdocs.conversion import HTMLDocument

# Example HTML – you can replace this with any valid markup
html_content = "<h1>Title</h1><p>Hello <a href='https://example.com'>world</a></p>"
html_doc = HTMLDocument(html_content)
```

*Por que isso importa:* `HTMLDocument` analisa a marcação uma única vez, permitindo que o conversor trabalhe com uma representação normalizada em vez de texto bruto.

## Etapa 2: Configurar `MarkdownSaveOptions`

`MarkdownSaveOptions` permite controlar o formato de saída e quais recursos do Markdown são emitidos. A biblioteca oferece dois formatadores:

* **DEFAULT** – Markdown padrão compatível com CommonMark.
* **GIT** – Markdown com recursos do Git (adiciona tabelas, tachado, etc.).

Para a maioria dos cenários de controle de versão, o formatador **GIT** é o preferido.

```python
from groupdocs.conversion import MarkdownSaveOptions

md_opts = MarkdownSaveOptions()
md_opts.formatter = MarkdownSaveOptions.Formatter.GIT
```

### Habilitando apenas os recursos necessários

Você pode ajustar a saída ativando flags de recursos específicos. Neste exemplo mantemos **links** e **parágrafos** enquanto desativamos imagens, tabelas e outras construções.

```python
md_opts.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

*Por que isso importa:* Limitar os recursos reduz o tamanho do arquivo gerado e impede a inclusão de elementos Markdown inesperados que ferramentas subsequentes podem não suportar.

## Etapa 3: Converter o documento

Com o `HTMLDocument` de origem e o `MarkdownSaveOptions` configurado, a conversão é feita com uma única chamada a `Converter.convert`. Forneça um caminho absoluto ou relativo para o arquivo de saída.

```python
from groupdocs.conversion import Converter

output_path = "output.md"
Converter.convert(html_doc, output_path, md_opts)
```

Após a chamada terminar, `output.md` contém a representação Markdown do HTML original.

## Script completo que você pode executar hoje

Abaixo está o script completo e autocontido que incorpora todas as etapas anteriores. Salve‑o como `html_to_md.py` e execute `python html_to_md.py`.

```python
# html_to_md.py
# Complete example that converts HTML to Markdown using GroupDocs.Conversion

from groupdocs.conversion import Converter, HTMLDocument, MarkdownSaveOptions

# 1️⃣  Create the HTMLDocument – replace the string with your own HTML source
html_content = """
<h1>Project Overview</h1>
<p>Welcome to the <a href="https://github.com/example">example repo</a>.</p>
<ul>
  <li>Feature A</li>
  <li>Feature B</li>
</ul>
"""
html_doc = HTMLDocument(html_content)

# 2️⃣  Prepare Markdown save options
md_opts = MarkdownSaveOptions()
md_opts.formatter = MarkdownSaveOptions.Formatter.GIT  # Git‑flavored Markdown
md_opts.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH |
    MarkdownSaveOptions.Features.LIST      # include lists for this example
)

# 3️⃣  Perform the conversion
output_path = "output.md"
Converter.convert(html_doc, output_path, md_opts)

print(f"Conversion complete – Markdown saved to {output_path}")
```

### Saída esperada (`output.md`)

```markdown
# Project Overview

Welcome to the [example repo](https://github.com/example).

- Feature A
- Feature B
```

A saída corresponde à estrutura original do HTML enquanto expõe apenas os recursos que habilitamos (links, parágrafos e listas).

## Tratamento de casos extremos comuns

### Atributos `href` ausentes ou malformados

Se uma tag `<a>` não possuir um `href` válido, o conversor insere o texto do link sem URL. Para preservar a legibilidade, você pode querer pós‑processar o Markdown:

```python
import re

def fix_broken_links(md_text):
    # Replace stray brackets like [text]() with just the text
    return re.sub(r'\[([^\]]+)\]\(\)', r'\1', md_text)

with open(output_path, "r+", encoding="utf-8") as f:
    content = f.read()
    f.seek(0)
    f.write(fix_broken_links(content))
    f.truncate()
```

### Convertendo arquivos HTML grandes

Para arquivos HTML de vários megabytes, faça streaming da entrada para evitar carregar toda a marcação na memória:

```python
with open("large_input.html", "r", encoding="utf-8") as src:
    html_doc = HTMLDocument(src.read())
```

O processo de conversão em si permanece inalterado porque `HTMLDocument` abstrai o tamanho da fonte.

## Formatadores alternativos

Se você preferir CommonMark puro em vez da saída com recursos do Git, altere o formatador:

```python
md_opts.formatter = MarkdownSaveOptions.Formatter.DEFAULT
```

Isso gera um arquivo Markdown mais minimalista, útil quando você mira plataformas que não suportam extensões do Git.

## Tarefas relacionadas que você pode explorar a seguir

* **Converter Markdown de volta para HTML** – útil para pré‑visualizar documentação.
* **Exportar HTML para PDF** – outro fluxo de trabalho comum adjacente à **conversão de html para markdown**.
* **Processar em lote uma pasta de arquivos HTML** – iterar sobre arquivos e reutilizar a mesma instância de `MarkdownSaveOptions`.

Todas essas seguem o mesmo padrão: criar um documento de origem, configurar as opções de salvamento e chamar `Converter.convert`.

## Conclusão

Agora você sabe como **converter HTML para Markdown** em Python, como **salvar HTML como Markdown** com controle preciso de recursos e por que selecionar o formatador correto é importante para as ferramentas subsequentes. O exemplo demonstra uma abordagem limpa e reutilizável que funciona para strings individuais, arquivos ou URLs, e inclui dicas para lidar com links ausentes e entradas grandes.

Sinta‑se à vontade para experimentar recursos adicionais de `MarkdownSaveOptions.Features` (por exemplo, `IMAGE`, `TABLE`) para adaptar a saída às necessidades do seu projeto. Se este guia foi útil, compartilhe‑o com colegas ou vincule‑o à documentação do seu projeto. Boa conversão!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}