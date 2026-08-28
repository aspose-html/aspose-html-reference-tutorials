---
category: general
date: 2026-07-18
description: Converta HTML para EPUB em Python rapidamente. Aprenda como carregar
  um arquivo HTML em Python e também converter HTML para MHTML usando bibliotecas
  simples.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: pt
lastmod: 2026-07-18
og_description: Converta HTML para EPUB em Python com um exemplo claro e executável.
  Também aprenda como carregar um arquivo HTML em Python e converter HTML para MHTML
  em minutos.
og_image_alt: Diagram showing convert html to epub workflow
og_title: Converter HTML para EPUB em Python – Tutorial Completo
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: Converter HTML para EPUB em Python – Guia Completo Passo a Passo
url: /pt/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converta HTML para EPUB em Python – Guia Completo Passo a Passo

Já se perguntou como **converter HTML para EPUB** sem perder a cabeça? Você não está sozinho — desenvolvedores precisam constantemente transformar páginas da web em e‑books para leitura offline, e fazer isso em Python é surpreendentemente simples. Neste tutorial vamos percorrer o carregamento de um arquivo HTML em Python, a conversão desse HTML para EPUB e até a transformação da mesma fonte em MHTML para arquivos de e‑mail.

Ao final do guia você terá um script pronto‑para‑executar que recebe um único arquivo `sample.html` e gera tanto `sample.epub` quanto `sample.mhtml`. Sem mistério, apenas código claro e explicações.

---

![Diagrama do pipeline de conversão](https://example.com/images/convert-html-epub.png "Diagrama mostrando o fluxo de conversão de html para epub")

## O Que Você Vai Construir

- **Carregar um arquivo HTML em Python** usando os módulos internos `pathlib` e `io`.  
- **Converter HTML para EPUB** com a biblioteca `ebooklib`, que cuida do formato de contêiner EPUB para você.  
- **Converter HTML para MHTML** (também conhecido como MHT) usando o pacote `email`, criando um arquivo web de arquivo único que os navegadores podem abrir diretamente.  

Também abordaremos:

- Dependências necessárias e como instalá‑las.  
- Tratamento de erros para que seu script falhe de forma elegante.  
- Como personalizar metadados como título e autor para o arquivo EPUB.  

Pronto? Vamos mergulhar.

---

## Pré‑requisitos

Antes de começarmos a codificar, certifique‑se de que você tem:

1. **Python 3.9+** – a sintaxe usada aqui funciona em qualquer versão recente.  
2. **pip** – para instalar pacotes de terceiros.  
3. Um arquivo HTML simples, por exemplo, `sample.html`, colocado em uma pasta que você controla.  

Se já tem tudo isso, ótimo — pule para a próxima seção.  

> **Dica de especialista:** Mantenha seu HTML bem‑formado (seções `<head>` e `<body>` corretas). Embora o `ebooklib` tente corrigir pequenos problemas, uma fonte limpa evita dores de cabeça depois.

---

## Etapa 1 – Instale as Bibliotecas Necessárias

Precisamos de dois pacotes externos:

- **ebooklib** – para geração de EPUB.  
- **beautifulsoup4** – opcional, mas útil para limpar o HTML antes da conversão.

Execute isso no seu terminal:

```bash
pip install ebooklib beautifulsoup4
```

> **Por que essas bibliotecas?** `ebooklib` cria a estrutura ZIP‑based do EPUB para você, cuidando da pasta `META‑INF`, do `content.opf` e do `toc.ncx` automaticamente. `beautifulsoup4` nos permite organizar o HTML, garantindo que o e‑book final seja renderizado corretamente em todos os leitores.

---

## Etapa 2 – Carregue o Arquivo HTML em Python

Carregar um arquivo HTML é simples, mas vamos encapsular isso em uma pequena função auxiliar que devolve um objeto **BeautifulSoup** para processamento posterior.

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**Explicação:**  
- `Path` nos fornece manipulação de arquivos independente do SO.  
- Usar `read_text` evita o boilerplate de `open`/`close`.  
- Retornar um objeto `BeautifulSoup` significa que podemos, mais tarde, remover scripts, corrigir tags quebradas ou injetar uma folha de estilos antes de **converter HTML para EPUB**.

---

## Etapa 3 – Converta HTML para EPUB

Agora que podemos **carregar o arquivo HTML em Python**, vamos transformá‑lo em um EPUB limpo. A função abaixo aceita um objeto `BeautifulSoup`, um caminho de destino e metadados opcionais.

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**Por que isso funciona:**  
- `ebooklib.epub.EpubBook` abstrai o contêiner ZIP e os arquivos de manifesto necessários.  
- Geramos um UUID como identificador para evitar IDs duplicados se você criar muitos livros.  
- O `spine` indica aos leitores a ordem dos capítulos; um livro de um único capítulo costuma ser suficiente para fontes HTML simples.  

**Executando a conversão:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

Ao executar o script, você verá uma marca de verificação verde confirmando a localização do arquivo EPUB.

---

## Etapa 4 – Converta HTML para MHTML

MHTML (ou MHT) agrupa o HTML e todos os seus recursos (imagens, CSS) em um único arquivo MIME. O pacote `email` do Python pode construir esse formato sem dependências externas.

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**Pontos principais:**  

- O tipo MIME `multipart/related` informa aos navegadores que a parte HTML e seus recursos pertencem juntos.  
- Percorremos as tags `<img>` para incorporar imagens; se você não precisar de imagens, pode pular esse bloco.  
- `Content-Location` usa um URI `file://` para que os navegadores resolvam os recursos internamente.  

**Chamando a função:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Agora você tem tanto `sample.epub` quanto `sample.mhtml` lado a lado.

---

## Script Completo – Todas as Etapas em Um Arquivo

Abaixo está o script completo, pronto‑para‑executar, que combina tudo. Salve‑o como `convert_html.py` e substitua `YOUR_DIRECTORY` pelo caminho que contém seu `sample.html`.

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
convert_html.py

A tiny utility that demonstrates:
- How to load an HTML file in Python
- How to convert HTML to EPUB (convert html to epub)
- How to convert HTML to MHTML (convert html to mhtml)

Author: Your Name
Date: 2026‑07‑18
"""

from pathlib import Path
import uuid
import mimetypes


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [How to Convert EPUB to Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}