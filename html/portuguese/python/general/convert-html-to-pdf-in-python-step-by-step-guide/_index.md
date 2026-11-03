---
category: general
date: 2026-08-06
description: Converter HTML em PDF em Python com um exemplo completo. Aprenda a gerar
  PDF a partir de HTML, salvar HTML como PDF e lidar com casos de borda comuns.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: pt
lastmod: 2026-08-06
og_description: Converta HTML em PDF usando Python e automatize a criação de documentos.
  Siga este guia para gerar PDF a partir de HTML, salvar HTML como PDF e personalizar
  a saída.
og_image_alt: Example of convert html to pdf script in Python
og_title: Converter HTML para PDF em Python – tutorial abrangente
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: Converter HTML em PDF com Python – guia passo a passo
url: /pt/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter HTML para PDF em Python – guia passo a passo

Se você precisa **converter HTML para PDF** rapidamente, este tutorial mostra uma solução completa em Python. Você verá como gerar PDF a partir de HTML, salvar HTML como PDF e controlar o processo de conversão sem sair do seu código.

O guia orienta você na instalação de uma biblioteca confiável, no carregamento de um documento HTML, na execução da conversão e na verificação do resultado. Ao final, você poderá criar PDF a partir de um arquivo HTML em qualquer projeto Python, seja a origem uma página estática ou marcação gerada dinamicamente.

## O que você aprenderá

* Instalar as dependências `pdfkit` e `wkhtmltopdf` necessárias para a conversão de HTML para PDF.  
* Carregar um documento HTML a partir do disco ou de uma string.  
* Gerar PDF a partir de HTML com opções personalizadas de tamanho de página, margem e codificação.  
* Salvar HTML como PDF usando uma única chamada de função.  
* Tratar casos típicos, como recursos ausentes, caracteres Unicode e arquivos grandes.  

**Pré‑requisitos** – Python 3.8+ e familiaridade básica com I/O de arquivos. Nenhum serviço externo é necessário.

## Converter HTML para PDF – fluxo de trabalho geral

O processo de conversão consiste em três fases lógicas:

1. **Preparação** – instalar o conversor e garantir que o binário `wkhtmltopdf` esteja acessível.  
2. **Manipulação de entrada** – ler o arquivo HTML ou construir a marcação programaticamente.  
3. **Geração de saída** – invocar o conversor, gravar o arquivo PDF e confirmar o resultado.  

Cada fase é abordada em uma etapa dedicada abaixo.

## Etapa 1: Instalar as bibliotecas necessárias

`pdfkit` fornece um wrapper Python leve em torno do amplamente usado motor `wkhtmltopdf`. Instale ambos com `pip` e verifique o caminho do binário.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Se preferir um binário portátil, faça o download da versão apropriada na [página do wkhtmltopdf no GitHub](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) e coloque-a em um diretório que esteja incluído no seu `PATH`. O script verifica o caminho automaticamente mais tarde.

## Etapa 2: Carregar o documento HTML

Você pode ler um arquivo estático, buscar conteúdo remoto ou construir HTML dinamicamente. O exemplo abaixo carrega um arquivo local chamado `sample.html` localizado em um diretório que você definir.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

Ler o arquivo como uma string Unicode garante que caracteres como “é”, “ß” ou glifos asiáticos sejam preservados durante a conversão. Esta etapa é essencial quando você **gera PDF a partir de HTML** que contém texto internacional.

## Etapa 3: Gerar PDF a partir de HTML

`pdfkit.from_string` converte uma string contendo marcação HTML em um arquivo PDF. Você pode passar um dicionário de opções para controlar o tamanho da página, margens e comportamento de cabeçalho/rodapé.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

A chamada acima **cria PDF a partir de um arquivo HTML** armazenado em `sample.pdf`. Se o HTML de origem referenciar CSS ou imagens locais, a flag `enable‑local‑file‑access` permite que o `wkhtmltopdf` resolva esses recursos.

### Por que esta abordagem funciona

* `pdfkit` delega o trabalho pesado ao `wkhtmltopdf`, que renderiza HTML com o motor WebKit, garantindo alta fidelidade ao layout original.  
* Fornecer um dicionário de opções permite ajustar finamente a saída sem modificar o próprio HTML.  
* Usar `from_string` mantém o fluxo de trabalho na memória, o que é útil quando o HTML é gerado dinamicamente.

## Etapa 4: Salvar HTML como PDF e verificar a saída

Após a conversão, você pode querer confirmar que o PDF existe e pode ser lido. O trecho abaixo verifica o tamanho do arquivo e abre o PDF com o visualizador padrão do sistema (específico da plataforma).

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

Executar o script imprime uma mensagem de sucesso e abre o visualizador de PDF para que você possa confirmar instantaneamente que o layout corresponde ao HTML original. Esta etapa completa o ciclo de **salvar html como pdf**.

## Etapa 5: Opções avançadas – criar PDF a partir de arquivo HTML com configurações personalizadas

Às vezes você tem um arquivo HTML físico no disco e prefere `pdfkit.from_file` em vez de carregar o conteúdo manualmente. Este método é útil quando o HTML já inclui caminhos relativos complexos.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Você também pode incorporar uma página de capa, índice ou flags de execução de JavaScript estendendo o dicionário `options`. Por exemplo, para adicionar uma página de capa:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Essas ajustes demonstram **como converter HTML para PDF** para pipelines de publicação mais sofisticados.

## Armadilhas comuns e como evitá‑las

| Problema | Causa | Solução |
|----------|-------|---------|
| Imagens ou CSS não aparecem | `wkhtmltopdf` bloqueia o acesso a arquivos locais por padrão | Adicione `"enable-local-file-access": None` ao dicionário de opções |
| Caracteres Unicode ficam corrompidos | Falta a opção `encoding` ou leitura do arquivo com charset errado | Sempre defina `"encoding": "UTF-8"` e leia o arquivo HTML com UTF‑8 |
| PDF fica em branco | Caminho incorreto para o binário `wkhtmltopdf` | Forneça o caminho explicitamente: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Arquivos HTML grandes causam timeout | Timeout padrão muito curto | Defina `"javascript-delay": "2000"` ou aumente o timeout com `"timeout": "60"` |

Resolver esses problemas garante um processo confiável de **gerar pdf a partir de html** em diferentes ambientes.

## Script completo – exemplo de ponta a ponta

Salve o seguinte como `html_to_pdf.py` e execute‑o com `python html_to_pdf.py`. Ajuste `YOUR_DIRECTORY` para apontar para a pasta do seu projeto.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como converter HTML para PDF em Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Converter HTML para PDF em .NET com Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Como converter HTML para PDF em Java – Definir margens de página com Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}