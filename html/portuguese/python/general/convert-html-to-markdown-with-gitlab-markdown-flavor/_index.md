---
category: general
date: 2026-09-07
description: Converter HTML para Markdown usando o sabor de markdown do GitLab. Siga
  este guia para habilitar os recursos de markdown do GitLab e converter um arquivo
  HTML em Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab markdown flavor
- gitlab markdown features
- how to convert html
- convert html file
language: pt
lastmod: 2026-09-07
og_description: Converter HTML para Markdown usando o sabor de markdown do GitLab.
  Este tutorial mostra como habilitar os recursos de markdown do GitLab e converter
  um arquivo HTML com Aspose.HTML para Python.
og_image_alt: Screenshot of converted HTML to Markdown using GitLab markdown flavor
og_title: Converter HTML para Markdown com o sabor de markdown do GitLab – guia passo
  a passo
schemas:
- author: Aspose
  dateModified: '2026-09-07'
  description: Convert HTML to Markdown using GitLab markdown flavor. Follow this
    guide to enable GitLab markdown features and convert an HTML file in Python.
  headline: Convert HTML to Markdown with GitLab markdown flavor
  type: TechArticle
tags:
- markdown
- gitlab
- html conversion
title: Converter HTML para Markdown com o sabor de markdown do GitLab
url: /pt/python/general/convert-html-to-markdown-with-gitlab-markdown-flavor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter HTML para Markdown com o sabor de markdown do GitLab

Se você precisa **converter HTML para Markdown**, este guia mostra uma solução completa que ativa o **sabor de markdown do GitLab**. Você aprenderá como habilitar recursos de markdown específicos do GitLab e transformar um arquivo HTML em um `README.md` limpo, pronto para repositórios GitLab.

O tutorial cobre tudo o que você precisa: instalar a biblioteca necessária, configurar as opções de markdown do GitLab, carregar uma fonte HTML, executar a conversão e lidar com casos comuns, como imagens e tabelas. Ao final do guia, você poderá executar a conversão com confiança em qualquer documento HTML.

## Pré-requisitos

* Python 3.8 ou mais recente instalado.
* Acesso ao `pip` para instalar pacotes de terceiros.
* Um entendimento básico da sintaxe Markdown.

A única dependência externa é **Aspose.HTML for Python via .NET**. Instale-a com:

```bash
pip install aspose-html
```

> **Dica:** Verifique a instalação executando `python -c "import aspose.html"`; nenhum erro significa que o pacote está pronto.

## Etapa 1: Criar opções de salvamento Markdown e habilitar o sabor de markdown do GitLab

O primeiro passo é criar um objeto `MarkdownSaveOptions` e ativar os recursos de markdown específicos do GitLab. Definir `git = True` indica ao conversor que ele deve gerar sintaxe compatível com o GitLab, como listas de tarefas e blocos de código delimitados.

```python
from aspose.html import MarkdownSaveOptions

# Step 1: Create Markdown save options and enable GitLab flavour
md_options = MarkdownSaveOptions()
md_options.git = True   # activates GitLab‑specific markdown features
```

Habilitar o **sabor de markdown do GitLab** garante que o Markdown gerado siga as mesmas regras de renderização que você vê no GitLab.com. Sem essa flag, a saída seguiria a especificação padrão CommonMark, o que pode gerar diferenças sutis em tabelas ou listas de tarefas.

## Etapa 2: Carregar o documento HTML de origem

Em seguida, carregue o arquivo HTML que você deseja converter. A classe `HTMLDocument` analisa o arquivo e constrói um DOM que o conversor pode percorrer.

```python
from aspose.html import HTMLDocument

# Step 2: Load the source HTML document
source_path = "YOUR_DIRECTORY/readme.html"
source_doc = HTMLDocument(source_path)
```

Substitua `YOUR_DIRECTORY/readme.html` pelo caminho real do seu arquivo HTML. O construtor `HTMLDocument` resolve automaticamente URLs relativas, de modo que quaisquer imagens locais referenciadas no HTML estarão disponíveis para a etapa de conversão.

## Etapa 3: Converter o documento HTML para Markdown usando as opções configuradas

Agora execute a conversão. O método estático `Converter.convert` recebe o documento de origem, o caminho do arquivo de destino e o `MarkdownSaveOptions` que você configurou anteriormente.

```python
from aspose.html import Converter

# Step 3: Convert the HTML document to Markdown using the configured options
target_path = "YOUR_DIRECTORY/README.md"
Converter.convert(source_doc, target_path, md_options)
```

Quando a chamada terminar, `README.md` conterá a representação Markdown do HTML original, renderizada com **recursos de markdown do GitLab**, como:

* Sintaxe de lista de tarefas (`- [ ]` e `- [x]`).
* Tabelas no estilo GitLab (linhas separadas por pipe com alinhamento de cabeçalho).
* Blocos de código delimitados com indicação de linguagem (` ```python `).

### Expected output

Assuming the source HTML contains a simple heading, a paragraph, and a task list, the resulting `README.md` will look like:

```markdown
# Project Overview

This project demonstrates how to convert HTML to Markdown.

- [ ] Install dependencies
- [x] Write conversion script
- [ ] Publish to GitLab
```

The output matches what GitLab renders in its web UI, thanks to the **gitlab markdown flavor** you enabled.

## Handling images and relative links

When your HTML includes `<img>` tags or relative hyperlinks, the converter rewrites them to standard Markdown syntax. However, you must ensure that the referenced assets are accessible from the repository where the Markdown file will live.

```python
# Example: Preserve image paths relative to the target markdown file
md_options.images_folder = "images"   # optional: specify a folder for extracted images
md_options.embed_images = False       # keep images as external files, not base64
```

* `images_folder` tells the converter where to copy extracted images.
* `embed_images = False` keeps the Markdown clean and lets GitLab serve the images directly.

If you prefer embedding images as Base64 (useful for single‑file documentation), set `embed_images = True`. This choice influences the **convert html file** step and may increase the size of the generated Markdown.

## Converting multiple HTML files in a batch

Often you need to **convert HTML files** in bulk, for example when migrating a static site to a GitLab wiki. The same logic applies; you just loop over the files:

```python
import os
from aspose.html import MarkdownSaveOptions, HTMLDocument, Converter

def batch_convert(src_dir: str, dst_dir: str):
    md_options = MarkdownSaveOptions()
    md_options.git = True

    for filename in os.listdir(src_dir):
        if filename.lower().endswith(".html"):
            html_path = os.path.join(src_dir, filename)
            md_path = os.path.join(dst_dir, os.path.splitext(filename)[0] + ".md")
            doc = HTMLDocument(html_path)
            Converter.convert(doc, md_path, md_options)
            print(f"Converted {filename} → {os.path.basename(md_path)}")

# Example usage
batch_convert("YOUR_DIRECTORY/html_pages", "YOUR_DIRECTORY/markdown_pages")
```

The function respects the **gitlab markdown features** for each file, giving you a ready‑to‑commit collection of `.md` files.

## Verifying the conversion

After conversion, open the generated Markdown in a local editor that supports GitLab preview (e.g., VS Code with the *GitLab Workflow* extension) or push it to a temporary GitLab branch. Verify that:

* Tables render with proper column alignment.
* Task lists retain their checkboxes.
* Images display correctly.
* Links point to the expected locations.

If you notice missing assets, double‑check the `images_folder` setting and ensure the image files were copied to the target repository.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Images appear as broken links | `embed_images` set to `False` but the `images_folder` was not added to the repository | Add the `images` folder to GitLab or switch `embed_images = True`. |
| Tables lose alignment | GitLab markdown requires a header separator line (`---`) | The converter adds it automatically when `git = True`; ensure you didn’t overwrite `md_options` later. |
| Unicode characters become escaped | The source HTML uses a different encoding | Open the HTML with `HTMLDocument(source_path, encoding="utf-8")`. |
| Large HTML files cause memory errors | The library loads the whole DOM into memory | Process the file in chunks or increase the Python memory limit (`PYTHONHASHSEED`). |

Addressing these issues early saves time when you **how to convert HTML** for production use.

## Full script – ready to run

Below is a single‑file script that puts all the steps together. Save it as `convert_html_to_md.py` and run it from the command line.

```python
"""
convert_html_to_md.py

A complete example that converts an HTML file to Markdown using
GitLab markdown flavor. This script demonstrates:
* Enabling GitLab markdown features
* Loading an HTML document
* Converting to Markdown
* Optional handling of images and batch conversion
"""

import os
from aspose.html import MarkdownSaveOptions, HTMLDocument, Converter

def convert_single(html_path: str, md_path: str, embed_images: bool = False):
    """Convert one HTML file to GitLab‑compatible Markdown."""
    md_options = MarkdownSaveOptions()
    md_options.git = True                # enable GitLab markdown flavor
    md_options.embed_images = embed_images
    if not embed_images:
        md_options.images_folder = os.path.dirname(md_path)  # keep images next to .md

    doc = HTMLDocument(html_path)
    Converter.convert(doc, md_path, md_options)
    print(f"Converted: {html_path} → {md_path}")

def batch_convert(src_dir: str, dst_dir: str, embed_images: bool = False):
    """Convert every .html file in src_dir to .md in dst_dir."""
    os.makedirs(dst_dir, exist_ok=True)
    for file in os.listdir(src_dir):
        if file.lower().endswith(".html"):
            src = os.path.join(src_dir, file)
            dst = os.path.join(dst_dir, os.path.splitext(file)[0] + ".md")
            convert_single(src, dst, embed_images)

if __name__ == "__main__":
    # Example usage – edit paths as needed
    SOURCE_HTML = "YOUR_DIRECTORY/readme.html"
    TARGET_MD = "YOUR_DIRECTORY/README.md"

    # Convert a single file
    convert_single(SOURCE_HTML, TARGET_MD)

    # Uncomment to run a batch conversion
    # batch_convert("YOUR_DIRECTORY/html_pages", "YOUR_DIRECTORY/markdown_pages")
```

Executar o script produz `README.md` que respeita **recursos de markdown do GitLab** e pode ser commitado diretamente em um repositório GitLab.

## Conclusão

Agora você sabe como **converter HTML para Markdown** preservando o **sabor de markdown do GitLab**. O guia abordou a habilitação de recursos específicos do GitLab, o carregamento de HTML, a execução da conversão, o tratamento de imagens e a execução de trabalhos em lote. Use o script fornecido como base para seus pipelines de documentação, processos CI/CD ou projetos de migração.

Em seguida, explore tópicos relacionados, como **automatizar linting de Markdown no GitLab CI**, **personalizar a renderização de Markdown com extensões**, ou **converter outros formatos (Word, PDF) para Markdown compatível com GitLab**. Cada um desses se baseia nos mesmos princípios de conversão que você acabou de dominar. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Converter HTML para Markdown em Aspose.HTML para Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Converter HTML para Markdown em .NET com Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Markdown para HTML Java - Converter com Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}