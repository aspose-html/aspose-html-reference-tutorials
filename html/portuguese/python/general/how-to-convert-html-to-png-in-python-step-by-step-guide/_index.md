---
category: general
date: 2026-10-21
description: Aprenda a converter HTML para PNG rapidamente. Este tutorial também aborda
  exportar página da web para PNG e converter arquivo HTML para PNG com Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: pt
lastmod: 2026-10-21
og_description: Converta HTML em PNG com Python. Siga este guia claro para exportar
  a página da web para PNG, lidar com casos extremos e automatizar a geração de imagens.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: Converter HTML para PNG em Python – guia completo de programação
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: Como converter HTML para PNG em Python – guia passo a passo
url: /pt/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter HTML para PNG em Python – guia completo de programação

Se você precisa **converter HTML para PNG**, este guia mostra uma maneira confiável de fazer isso com Python puro. Seja exportando um relatório estático, gerando miniaturas para uma galeria ou automatizando capturas de tela para testes, você obterá uma solução completa e executável em minutos.

Você também verá como **exportar página da web para PNG**, entenderá a diferença entre converter um arquivo HTML e uma URL ao vivo, e aprenderá as melhores práticas para lidar com páginas grandes ou conteúdo dinâmico. Nenhum serviço externo é necessário — apenas alguns pacotes Python e um script curto.

## Pré-requisitos

- Python 3.9+ instalado (o código funciona no Windows, macOS e Linux)
- Acesso a um terminal ou prompt de comando
- Familiaridade básica com o gerenciador de pacotes do Python (`pip`)

Você precisará do pacote `imgkit` (um wrapper leve em torno do `wkhtmltoimage`) e do binário `wkhtmltoimage` propriamente dito. Ambos são gratuitos e de código aberto.

## Etapa 1: Instalar as ferramentas necessárias

O primeiro passo é instalar o `wkhtmltoimage` e o wrapper Python que se comunica com ele.

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **Por que esta etapa importa** – `wkhtmltoimage` renderiza HTML usando o motor WebKit, produzindo PNGs pixel‑perfeitos. `imgkit` simplesmente encaminha suas opções para o binário, então você obtém a mesma qualidade que teria em um navegador.

## Etapa 2: Verificar a instalação

Execute uma verificação rápida para confirmar que o binário está acessível a partir do Python.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Se o script imprimir o caminho para `wkhtmltoimage`, você está pronto para converter HTML para PNG. Se receber um `OSError`, verifique novamente se o binário está no `PATH` do seu sistema.

## Etapa 3: Escrever uma função de conversão reutilizável

Encapsular a lógica em uma função facilita **converter arquivo HTML para PNG** ou **exportar página da web para PNG** a partir de qualquer lugar do seu projeto.

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **Por que encapsulamos tanto `from_file` quanto `from_url`** – A mesma função agora suporta **como converter HTML para imagem** para arquivos locais e páginas da web ao vivo, mantendo seu código DRY (Don’t Repeat Yourself).

## Etapa 4: Converter um arquivo HTML local para PNG

Coloque um arquivo HTML chamado `sample.html` em uma pasta chamada `assets`. Em seguida, chame a função auxiliar que acabamos de definir:

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### Saída esperada

Executar o script imprime:

```
✅ Successfully saved PNG to: output/sample.png
```

Um novo arquivo `output/sample.png` agora contém uma captura pixel‑perfeita de `sample.html`. Abrindo-o em qualquer visualizador de imagens mostra a página renderizada exatamente como apareceria em um navegador.

## Etapa 5: Exportar uma página da web ao vivo para PNG

Se você precisar **exportar página da web para PNG** para uma URL que muda frequentemente (por exemplo, um painel), basta passar a string da URL em vez de um caminho de arquivo.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Por que ajustar o tamanho da viewport?

Páginas da web projetadas para telas de desktop frequentemente parecem apertadas se renderizadas em uma largura pequena. Ao aumentar as opções `width` e `height`, você captura o layout completo, o que é especialmente útil para tarefas de **exportar página da web para PNG**.

## Etapa 6: Lidar com casos de borda comuns

### 6.1 Páginas grandes ou rolagem infinita

Para páginas que carregam conteúdo de forma preguiçosa (por exemplo, rolagem infinita), aumente o atraso do JavaScript e, opcionalmente, defina uma viewport maior:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Páginas protegidas por autenticação

Se uma página requer um cookie de sessão, você pode incorporar o cabeçalho do cookie:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Imagens ou fontes ausentes

`wkhtmltoimage` respeita a flag `--disable-local-file-access` por segurança. Se seu HTML referencia ativos locais, habilite-os explicitamente:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Etapa 7: Verificar o resultado programaticamente (opcional)

Às vezes você precisa confirmar que o PNG foi gerado corretamente (por exemplo, em pipelines de CI). O trecho a seguir verifica o tamanho do arquivo e as dimensões:

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

Se o PNG passar nessas verificações, você pode usá-lo com segurança em processos subsequentes, como geração de PDF, anexos de e‑mail ou pipelines de aprendizado de máquina.

## Conclusão

Agora você tem um método completo e pronto para produção para **converter HTML para PNG** usando Python. O guia abordou:

- Instalando `wkhtmltoimage` e `imgkit`
- Verificando o ambiente
- Uma função reutilizável `convert_html_to_png` que lida tanto com arquivos locais quanto com URLs
- Exemplos reais para **exportar página da web para PNG**, **como converter HTML para imagem**, e **converter arquivo HTML para PNG**
- Tratamento de casos de borda para páginas grandes, autenticação e ativos locais
- Etapas de verificação opcionais para pipelines CI/CD

Sinta-se à vontade para experimentar opções adicionais do `imgkit` — como `zoom`, `crop-h` ou `crop-w` — para ajustar finamente a saída para seu caso de uso específico. Como próximos passos, você pode explorar:

- Converter os PNGs em um relatório PDF (`img2pdf` library)
- Automatizar a conversão em lote de uma pasta inteira de arquivos HTML
- Usar Selenium para páginas que requerem renderização completa do navegador (por exemplo, frameworks JavaScript pesados)

Feliz codificação, e aproveite as capturas de tela pixel‑perfeitas!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Converter HTML para PNG – Guia Python Completo](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Converter HTML para PNG em Python – Guia Completo de Salvamento em Streaming](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Converter SVG para PNG em Python usando Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}