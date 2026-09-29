---
category: general
date: 2026-09-29
description: Como salvar SVG usando Python e exportar SVG para PNG. Aprenda a converter
  SVG para PNG com opções ajustadas em minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: pt
lastmod: 2026-09-29
og_description: Como salvar SVG usando Python e exportar SVG para PNG. Siga este guia
  para converter SVG em PNG com controle total sobre as opções.
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: Como salvar SVG como PNG com Python – passo a passo
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  headline: How to save SVG as PNG with Python – complete guide
  type: TechArticle
- description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  name: How to save SVG as PNG with Python – complete guide
  steps:
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: (Optional) Create image‑save options
    text: '```python from aspose.svg import ImageSaveOptions'
  - name: Save the SVG as PNG
    text: '```python # Export the SVG to a PNG file using the options defined above
      svg_doc.save("YOUR_DIRECTORY/vector.png", options) ```'
  - name: Full script
    text: 'Putting the pieces together yields a complete, runnable program:'
  - name: Missing file or invalid path
    text: 'If `src_path` does not exist, `SVGDocument` raises a `FileNotFoundError`.
      Wrap the call in a `try/except` block to provide a friendly error message:'
  - name: Preserving aspect ratio
    text: When only one dimension (width **or** height) is set, the library automatically
      scales the other dimension to maintain the original aspect ratio. If you set
      both dimensions, the image may stretch. Choose the approach that matches your
      UI requirements.
  - name: Transparent backgrounds
    text: 'If the original SVG relies on transparency (e.g., icons), you can keep
      the PNG transparent by omitting `background_color`:'
  type: HowTo
tags:
- Python
- SVG
- Image conversion
title: Como salvar SVG como PNG com Python – guia completo
url: /pt/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar SVG como PNG com Python – guia completo

Se você precisa **como salvar SVG** como uma imagem raster, este tutorial mostra uma solução pronta‑para‑executar. Você aprenderá como carregar um arquivo SVG vetorial, opcionalmente ajustar as configurações de salvamento de imagem e exportar o resultado para PNG em apenas três linhas de código.

Salvar arquivos SVG como PNG é comum quando você deseja incorporar gráficos em páginas web, gerar miniaturas ou alimentar imagens raster em pipelines de aprendizado de máquina. A abordagem descrita aqui funciona no Windows, macOS e Linux sem dependências nativas adicionais.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* Python 3.9 ou mais recente instalado
* O pacote `aspose.svg` (o oficial Aspose SVG for Python via .NET). Instale‑o com:

```bash
pip install aspose-svg
```

* Um arquivo SVG válido no disco (por exemplo, `vector.svg`)

Esses requisitos mantêm o exemplo autocontido e evitam ferramentas externas como CairoSVG.

## Como salvar SVG com Python

O núcleo do processo são três etapas: carregar, configurar e salvar. As seções a seguir detalham cada etapa.

### Etapa 1: Carregar o documento SVG

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

`SVGDocument` analisa o XML do SVG e cria uma representação em memória. Carregar o arquivo primeiro é obrigatório; caso contrário, a operação de salvamento não tem dados de origem.

### Etapa 2: (Opcional) Criar opções de salvamento de imagem

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

`ImageSaveOptions` permite ajustar finamente a saída PNG. Ajustar largura e altura preserva a proporção a menos que você defina ambas explicitamente. Definir uma cor de fundo é útil quando o SVG original contém transparência, mas você precisa de um PNG opaco.

### Etapa 3: Salvar o SVG como PNG

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

O método `save` grava um arquivo PNG no caminho de destino. Se você omitir o argumento `options`, a biblioteca usa dimensões padrão derivadas da viewBox do SVG.

### Script completo

Juntando as peças resulta em um programa completo e executável:

```python
# -*- coding: utf-8 -*-
"""
How to save SVG as PNG with Python.
This script loads an SVG file, applies optional image‑save settings,
and exports the result to PNG.
"""

from aspose.svg import SVGDocument, ImageSaveOptions

def convert_svg_to_png(
    src_path: str,
    dst_path: str,
    width: int = 800,
    height: int = 600,
    background: str = "#FFFFFF"
) -> None:
    """Convert an SVG file to PNG with custom dimensions and background."""
    # Load the SVG document
    svg_doc = SVGDocument(src_path)

    # Prepare save options
    options = ImageSaveOptions()
    options.width = width
    options.height = height
    options.background_color = background

    # Save as PNG
    svg_doc.save(dst_path, options)


if __name__ == "__main__":
    # Example usage
    convert_svg_to_png(
        src_path="YOUR_DIRECTORY/vector.svg",
        dst_path="YOUR_DIRECTORY/vector.png",
        width=1024,
        height=768,
        background="#FFFFFF"
    )
    print("SVG successfully saved as PNG.")
```

Executar o script exibe **“SVG successfully saved as PNG.”** e cria `vector.png` na mesma pasta.

## Converter SVG para PNG – lidando com armadilhas comuns

### Arquivo ausente ou caminho inválido

Se `src_path` não existir, `SVGDocument` gera um `FileNotFoundError`. Envolva a chamada em um bloco `try/except` para fornecer uma mensagem de erro amigável:

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### Preservando a proporção

Quando apenas uma dimensão (largura **ou** altura) é definida, a biblioteca escala automaticamente a outra dimensão para manter a proporção original. Se você definir ambas as dimensões, a imagem pode esticar. Escolha a abordagem que corresponde aos requisitos da sua interface.

### Fundos transparentes

Se o SVG original depende de transparência (por exemplo, ícones), você pode manter o PNG transparente omitindo `background_color`:

```python
options.background_color = None   # PNG will retain transparency
```

Esta variação é útil quando o PNG será sobreposto a outras imagens.

## Exportar SVG para PNG – dicas de desempenho

* **Reuse `ImageSaveOptions`** ao converter muitos arquivos em lote. Criar um novo objeto de opções para cada arquivo adiciona uma sobrecarga insignificante, mas reutilizá‑lo evita alocação repetida de memória.
* **Batch processing**: Percorra um diretório de arquivos SVG e chame `convert_svg_to_png` para cada um. A biblioteca processa cada arquivo independentemente, permitindo paralelizar o loop com `concurrent.futures.ThreadPoolExecutor` para conversão mais rápida em máquinas multi‑core.

```python
import os
from concurrent.futures import ThreadPoolExecutor

svg_folder = "YOUR_DIRECTORY"
png_folder = "YOUR_DIRECTORY/pngs"
os.makedirs(png_folder, exist_ok=True)

def batch_convert(file_name):
    src = os.path.join(svg_folder, file_name)
    dst = os.path.join(png_folder, file_name.replace('.svg', '.png'))
    convert_svg_to_png(src, dst)

with ThreadPoolExecutor(max_workers=8) as executor:
    executor.map(batch_convert, [f for f in os.listdir(svg_folder) if f.endswith('.svg')])
```

## Salvar SVG como PNG – verificação

Após a conversão, você pode verificar a saída programaticamente:

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

Saída típica:

```
PNG size: (1024, 768), mode: RGBA
```

O `mode` `RGBA` confirma que a imagem contém um canal alfa (transparência). Se você definir uma cor de fundo, o modo será `RGB`.

## Conclusão

Agora você sabe **como salvar SVG** como PNG usando Python, como **converter SVG para PNG** e como **exportar SVG para PNG** com dimensões personalizadas e tratamento de fundo. O script completo demonstra todo o fluxo de trabalho, desde o carregamento de um arquivo SVG vetorial até a produção de uma imagem PNG raster.

Em seguida, explore tópicos relacionados, como **save SVG as PNG** em modo batch, usando bibliotecas alternativas como **CairoSVG**, ou gerando PDFs de várias páginas a partir de fontes SVG. Experimente diferentes configurações de `ImageSaveOptions` para ajustar finamente a qualidade, DPI e compressão para seu caso de uso específico.

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [svg para png java – Converter SVG para Imagem com Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Renderizar documento SVG como PNG no .NET com Aspose.HTML](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [Como definir DPI ao converter SVG para PNG com Java](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}