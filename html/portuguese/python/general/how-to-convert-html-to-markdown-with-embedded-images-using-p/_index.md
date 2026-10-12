---
category: general
date: 2026-10-12
description: Converta HTML para markdown rapidamente e aprenda como incorporar imagens
  em markdown. Este guia percorre a conversão de HTML para markdown em Python com
  código completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to embed images in markdown
- html to markdown conversion python
- how to convert html page to markdown
language: pt
lastmod: 2026-10-12
og_description: Converta HTML para markdown e incorpore imagens no markdown usando
  Python. Siga este tutorial completo para uma conversão confiável de HTML para markdown
  em Python.
og_image_alt: Screenshot showing a Python script that converts an HTML file to a markdown
  file with base64‑encoded images
og_title: Converter HTML para markdown com imagens incorporadas em Python – guia passo
  a passo
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: convert HTML to markdown quickly and learn how to embed images in markdown.
    This guide walks through html to markdown conversion python with full code.
  headline: How to convert HTML to markdown with embedded images using Python
  type: TechArticle
tags:
- markdown
- html
- python
- document conversion
title: Como converter HTML para markdown com imagens incorporadas usando Python
url: /pt/python/general/how-to-convert-html-to-markdown-with-embedded-images-using-p/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como converter HTML para markdown com imagens incorporadas usando Python

Se você precisa **converter HTML para markdown** preservando todas as imagens, este guia mostra exatamente como fazer isso. Ao configurar o motor de conversão para incorporar imagens como Base64, você obtém um único arquivo `.md` auto‑contido que funciona em qualquer lugar — de READMEs no GitHub a geradores de sites estáticos.

Você também aprenderá **como incorporar imagens no markdown**, por que as opções integradas de manipulação de recursos são a escolha mais confiável e como realizar uma **html to markdown conversion python** em apenas algumas linhas de código.

## O que você vai alcançar

- Transformar qualquer página HTML local em um documento Markdown limpo.  
- Incorporar cada imagem diretamente no arquivo Markdown como uma string Base64, eliminando links quebrados.  
- Executar o processo em qualquer plataforma que suporte Python 3.9+ e a biblioteca GroupDocs Conversion.

## Pré‑requisitos

| Requisito | Motivo |
|------------|--------|
| Python 3.9 ou mais recente | Necessário para o GroupDocs Conversion SDK. |
| Pacote `groupdocs-conversion` | Fornece `Converter`, `HTMLDocument`, `MarkdownSaveOptions` e `ResourceHandlingOptions`. |
| Um arquivo HTML existente (ex.: `page.html`) | A fonte que você deseja converter. |
| Permissão de escrita na pasta de saída | Para salvar o arquivo `.md` gerado. |

Instale o SDK com pip:

```bash
pip install groupdocs-conversion
```

> **Dica:** Use um ambiente virtual (`python -m venv .venv`) para manter as dependências isoladas.

## Etapa 1: Configurar o tratamento de recursos para incorporar imagens no markdown

Quando o motor de conversão encontra uma tag `<img>`, ele pode copiar a imagem para uma pasta separada ou incorporá‑la diretamente. Incorporar produz um URI de dados codificado em Base64, que é exatamente o que **how to embed images in markdown** requer.

```python
from groupdocs.conversion import ResourceHandlingOptions

# Create a resource handling configuration
resource_options = ResourceHandlingOptions()
# Enable embedding of images as Base64 data URIs
resource_options.embed_images = True   # Embeds images directly in the Markdown file
```

**Por que isso importa:**  
Incorporar garante que o arquivo Markdown permaneça portátil. Se você compartilhar o arquivo `.md` sem a pasta de imagens correspondente, as imagens ainda serão renderizadas corretamente em qualquer plataforma que suporte URIs de dados (GitHub, GitLab, visualização do VS Code, etc.).

## Etapa 2: Definir as opções de salvamento Markdown usando a configuração de recursos

A classe `MarkdownSaveOptions` permite passar o `resource_options` criado acima. Ela também permite ajustar quebras de linha, estilos de cabeçalhos e mais, mas na maioria dos casos os padrões funcionam bem.

```python
from groupdocs.conversion import MarkdownSaveOptions

# Attach the resource handling to the markdown save options
markdown_options = MarkdownSaveOptions(resource_handling_options=resource_options)
```

**O que acontece nos bastidores:**  
Durante a conversão, o motor analisa o DOM HTML, converte cada elemento para seu equivalente Markdown e substitui `<img src="...">` por `![alt text](data:image/...;base64,...)`. O sinalizador `resource_options.embed_images` aciona esse comportamento.

## Etapa 3: Converter o documento HTML para markdown e salvar o resultado

Agora você reúne tudo: carrega o HTML de origem, aplica as opções de salvamento e grava o arquivo de saída.

```python
from groupdocs.conversion import Converter, HTMLDocument

# Path to the source HTML file
source_path = "YOUR_DIRECTORY/page.html"
# Desired output path for the markdown file
output_path = "YOUR_DIRECTORY/page.md"

# Perform the conversion
Converter.convert_html(
    HTMLDocument(source_path),
    markdown_options,
    output_path
)

print(f"✅ Conversion complete! Markdown saved to: {output_path}")
```

**Saída esperada:**  

- `page.md` contém texto Markdown, cabeçalhos, listas e **imagens incorporadas** como strings Base64.  
- Abrir `page.md` em um visualizador de Markdown exibe o layout HTML original, incluindo todas as imagens, sem nenhum recurso externo.

### Script completo para copiar‑e‑colar rapidamente

```python
# convert_html_to_markdown.py
from groupdocs.conversion import (
    Converter,
    HTMLDocument,
    MarkdownSaveOptions,
    ResourceHandlingOptions,
)

def convert_html_to_markdown(src_html: str, dst_md: str) -> None:
    """Convert an HTML file to markdown with images embedded as Base64."""
    # 1️⃣ Embed images
    resource_opts = ResourceHandlingOptions()
    resource_opts.embed_images = True

    # 2️⃣ Prepare markdown options
    md_opts = MarkdownSaveOptions(resource_handling_options=resource_opts)

    # 3️⃣ Run conversion
    Converter.convert_html(
        HTMLDocument(src_html),
        md_opts,
        dst_md
    )
    print(f"✅ Markdown file created at: {dst_md}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    convert_html_to_markdown(
        src_html="YOUR_DIRECTORY/page.html",
        dst_md="YOUR_DIRECTORY/page.md"
    )
```

Execute o script:

```bash
python convert_html_to_markdown.py
```

## Tratando casos de borda comuns

| Situação | Solução |
|-----------|----------|
| **Imagens grandes geram arquivos markdown enormes** | Limite o tamanho da imagem antes de incorporar redimensionando‑as no HTML ou usando uma biblioteca de otimização de imagens (ex.: Pillow) antes da conversão. |
| **URLs de imagens relativas apontam para fora do projeto** | Garanta que as referências HTML sejam acessíveis, ou copie essas imagens para a mesma pasta antes da conversão. |
| **Você precisa de arquivos de imagem separados em vez de incorporação** | Defina `resource_options.embed_images = False` e forneça um caminho `resource_folder` onde as imagens serão salvas. |
| **A conversão falha em HTML malformado** | Pré‑procese o HTML com `BeautifulSoup` (parser `html5lib`) para limpar tags quebradas antes de enviá‑lo ao conversor. |

## Verificando o resultado

Abra o `page.md` gerado em qualquer visualizador de Markdown:

```bash
code YOUR_DIRECTORY/page.md   # VS Code preview
```

Você deve ver os cabeçalhos, parágrafos e imagens originais renderizados corretamente. Se uma imagem aparecer como link quebrado, verifique se `embed_images` está definido como `True` e se o HTML de origem contém tags `<img>` válidas.

## Próximos passos e tópicos relacionados

- **Exportar para outros formatos** – A mesma classe `Converter` pode gerar PDF, DOCX ou texto simples. Troque `MarkdownSaveOptions` por `PdfSaveOptions` ou `DocxSaveOptions`.  
- **Processamento em lote** – Percorra um diretório de arquivos HTML para produzir uma coleção de documentos Markdown.  
- **Manipulação personalizada de imagens** – Implemente um callback via `ResourceHandlingOptions` para armazenar imagens em um CDN e substituir o URI de dados por uma URL do CDN.  
- **Recursos avançados de markdown** – Habilite markdown com recursos do GitHub (tabelas, listas de tarefas) ajustando as propriedades `markdown_options`.

Ao dominar **html to markdown conversion python**, você agora possui um fluxo de trabalho repetível e pronto para produção que garante que as imagens permaneçam junto ao conteúdo. Sinta‑se à vontade para experimentar as opções acima e adaptar o script aos seus próprios pipelines de conteúdo.

---


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Convert HTML to Markdown in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Convert HTML to Markdown in Aspose.HTML for Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Create PDF from Markdown using Aspose HTML Converter (Java)](/html/english/java/conversion-html-to-other-formats/create-pdf-from-markdown-using-aspose-html-converter-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}