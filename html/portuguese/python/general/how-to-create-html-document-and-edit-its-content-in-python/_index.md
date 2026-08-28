---
category: general
date: 2026-08-25
description: Aprenda a criar um documento HTML, selecionar elementos CSS, modificar
  texto HTML e salvar o arquivo HTML usando um script Python simples.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: pt
lastmod: 2026-08-25
og_description: Crie um documento HTML, selecione o elemento CSS, modifique o texto
  HTML e salve o arquivo HTML em algumas linhas de Python. Siga este tutorial completo.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Crie um documento HTML e edite seu conteúdo com Python – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: Como criar documento HTML e editar seu conteúdo em Python
url: /pt/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar documento html e editar seu conteúdo em Python

Se você precisa **create html document** do zero e alterar seus elementos programaticamente, este guia mostra exatamente como fazer. Você verá um script curto e executável que cria um arquivo, seleciona um parágrafo com um seletor CSS, atualiza o texto e grava o resultado de volta no disco.

Trabalhar com HTML em Python é comum ao gerar relatórios, modelos de e‑mail ou conteúdo de sites estáticos. Ao final deste tutorial, você será capaz de **select element css**, **modify html text** e **save html file** sem sair do conforto da sua IDE.

## Pré-requisitos

* Python 3.9 ou mais recente instalado.
* Os pacotes `beautifulsoup4` e `lxml` (instale com `pip install beautifulsoup4 lxml`).
* Permissão de escrita no diretório onde você pretende armazenar o arquivo de saída.

Nenhuma ferramenta adicional é necessária; a biblioteca padrão lida com I/O de arquivos.

## Etapa 1: Instalar as bibliotecas necessárias

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` fornece uma API conveniente para analisar e manipular HTML, enquanto `lxml` oferece um analisador rápido que entende seletores CSS.

## Etapa 2: Criar o documento HTML inicial

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

O construtor `BeautifulSoup` cria um objeto **create html document** na memória. Usar o analisador `"lxml"` garante suporte total a seletores CSS.

## Etapa 3: Selecionar o elemento parágrafo usando um seletor CSS

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

O método `select_one` implementa a lógica de **select element css**, retornando a primeira tag correspondente. Se o seletor não corresponder a nada, `para` será `None`, portanto uma verificação defensiva é recomendável em código de produção.

## Etapa 4: Modificar o conteúdo de texto do parágrafo

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

Atribuir a `para.string` realiza uma operação de **modify html text**. O BeautifulSoup atualiza a árvore DOM subjacente, de modo que a alteração seja refletida quando o documento for serializado.

## Etapa 5: Salvar o HTML atualizado em um arquivo

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

A chamada `open` juntamente com `write` implementa a funcionalidade de **save html file**. Usar `prettify()` produz uma saída bem indentada, o que é útil durante a depuração.

### Script completo para copiar‑e‑colar rápido

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

Executar `python edit_html.py` cria `updated.html` contendo:

```html
<p>
 New
</p>
```

## Variações comuns e casos de borda

### Selecionando múltiplos elementos

Se você precisar de seletores **select element css** que correspondam a várias tags (por exemplo, `"div.note"`), use `doc.select("div.note")` que retorna uma lista. Itere sobre a lista para aplicar alterações a cada elemento.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### Preservando atributos existentes

Ao substituir o texto, o BeautifulSoup mantém quaisquer atributos na tag. Por exemplo:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### Lidando com elementos ausentes de forma elegante

Em scripts de produção, você frequentemente encontra HTML malformado. Envolva a seleção em uma condicional ou bloco try‑except, como mostrado na Etapa 4, para evitar falhas.

### Gravando em um diretório específico

Substitua `output_path` por um caminho absoluto ou relativo:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

Certifique‑se de que o diretório exista; caso contrário, o Python lançará `FileNotFoundError`.

## Dicas profissionais

* **Performance** – Para arquivos HTML grandes, prefira usar `lxml.etree` diretamente; o BeautifulSoup adiciona uma camada de abstração fina que é conveniente, mas um pouco mais lenta.
* **Encoding** – Sempre abra arquivos com `encoding="utf-8"` para preservar caracteres não‑ASCII.
* **Testing** – Após a modificação, você pode verificar a saída com `assert "New" in open(output_path).read()` em um teste unitário.

## Conclusão

Agora você sabe como **create html document**, usar uma consulta **select element css** para localizar um nó, **modify html text**, e finalmente **save html file** com Python. Esse padrão escala para transformações mais complexas, como atualizações em massa, alterações de atributos ou geração de templates.

Em seguida, explore tópicos relacionados como **how to edit html** usando expressões XPath, gerar páginas HTML completas com Jinja2 ou automatizar o processamento em lote de vários arquivos. Cada um desses se baseia nas etapas principais demonstradas aqui e expande seu conjunto de ferramentas para manipulação programática de HTML.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Create HTML Document with Aspose.HTML – Step‑by‑Step Guide](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}