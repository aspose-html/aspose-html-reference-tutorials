---
category: general
date: 2026-10-25
description: salve SVG como PNG rapidamente com Python. Aprenda a converter SVG para
  PNG, exportar SVG para PNG e obtenha código pronto‑para‑usar de SVG para PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save svg as png
- convert svg to png
- how to convert svg
- export svg to png
- svg to png code
language: pt
lastmod: 2026-10-25
og_description: salvar SVG como PNG usando Python. Este tutorial mostra como converter
  SVG para PNG com código claro, opções e dicas de solução de problemas.
og_image_alt: Diagram illustrating saving an SVG file as a PNG image with Python
og_title: Salvar SVG como PNG em Python – guia completo
schemas:
- author: Aspose
  dateModified: '2026-10-25'
  description: save SVG as PNG quickly with Python. Learn to convert SVG to PNG, export
    SVG to PNG, and get ready‑to‑use svg to png code.
  headline: How to save SVG as PNG in Python – step‑by‑step guide
  type: TechArticle
- description: save SVG as PNG quickly with Python. Learn to convert SVG to PNG, export
    SVG to PNG, and get ready‑to‑use svg to png code.
  name: How to save SVG as PNG in Python – step‑by‑step guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Reason | |------------|--------| | Python 3.8+ | Modern
      syntax and type hints. | | `aspose.svg` package (or any library that provides
      `SVGDocument` and `PngSaveOptions`) | Supplies the `SVGDocument` class used
      in the example. | | An SVG file you own or have permission to use | The so'
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: Convert SVG to PNG – create save options
    text: '```python from aspose.svg import PngSaveOptions'
  - name: Export SVG to PNG
    text: '```python # Destination file for the PNG image png_path = "YOUR_DIRECTORY/vector.png"
      svg_doc.save(png_path, png_options) ```'
  - name: Verify the output (optional but recommended)
    text: '```python from PIL import Image'
  type: HowTo
tags:
- SVG
- PNG
- Python
title: Como salvar SVG como PNG em Python – guia passo a passo
url: /pt/python/general/how-to-save-svg-as-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar SVG como PNG em Python – guia passo a passo

Se você precisa **salvar SVG como PNG** rapidamente, este guia fornece uma solução completa e executável. Você verá como **converter SVG para PNG**, definir parâmetros de exportação opcionais e executar o script em qualquer plataforma que suporte Python.  

O tutorial cobre tudo, desde a instalação da biblioteca necessária até a verificação da imagem gerada, para que você possa copiar‑colar o código e obter resultados imediatamente. Nenhuma documentação externa é necessária — basta seguir os passos abaixo.

## O que você aprenderá

* O código **svg to png** exato que você precisa para uma conversão em uma única linha.  
* Como **exportar SVG para PNG** com DPI ou cor de fundo personalizados.  
* Armadilhas comuns ao converter SVGs complexos e como evitá‑las.  
* Como integrar a conversão em projetos Python maiores.

### Pré‑requisitos

| Requisito | Motivo |
|------------|--------|
| Python 3.8+ | Sintaxe moderna e dicas de tipo. |
| `aspose.svg` package (or any library that provides `SVGDocument` and `PngSaveOptions`) | Fornece a classe `SVGDocument` usada no exemplo. |
| An SVG file you own or have permission to use | O gráfico vetorial de origem. |

Instale a biblioteca com pip antes de começar:

```bash
pip install aspose.svg
```

> **Dica profissional:** Se você preferir uma dependência mais leve, `cairosvg` também oferece `svg2png`, mas a API mostrada aqui corresponde ao trecho original e funciona tanto para SVGs simples quanto complexos.

## Como salvar SVG como PNG com Python

### Etapa 1: Carregar o documento SVG

```python
from aspose.svg import SVGDocument

# Replace the path with your actual SVG file location
svg_path = "YOUR_DIRECTORY/vector.svg"
svg_doc = SVGDocument(svg_path)
```

*Por que esta etapa importa* – Carregar o arquivo cria uma representação em memória que a biblioteca pode manipular. Sem uma instância adequada de `SVGDocument`, chamadas subsequentes de exportação falharão.

### Etapa 2: Converter SVG para PNG – criar opções de salvamento

```python
from aspose.svg import PngSaveOptions

# Default options work for most cases; you can customize them later
png_options = PngSaveOptions()
```

`PngSaveOptions` permite controlar o tamanho de saída, DPI, cor de fundo e mais. A configuração padrão preserva as dimensões originais do SVG e produz um PNG sem perdas.

### Etapa 3: Exportar SVG para PNG

```python
# Destination file for the PNG image
png_path = "YOUR_DIRECTORY/vector.png"
svg_doc.save(png_path, png_options)
```

Quando `save` termina, `vector.png` conterá uma versão rasterizada do SVG original. A conversão é realizada totalmente em memória, sendo rápida mesmo para arquivos grandes.

### Etapa 4: Verificar a saída (opcional, mas recomendado)

```python
from PIL import Image

with Image.open(png_path) as img:
    print(f"PNG size: {img.size} – mode: {img.mode}")
    img.show()  # Opens the image in the default viewer
```

Executar este trecho imprime as dimensões em pixels e abre o PNG, confirmando que a conversão foi bem‑sucedida.

## Personalizando a conversão (como converter SVG com mais controle)

Se você precisar de um DPI específico ou de um fundo sólido para SVGs transparentes, ajuste o `PngSaveOptions` antes de chamar `save`:

```python
png_options = PngSaveOptions()
png_options.dpi = 300                     # High‑resolution output
png_options.background_color = "#FFFFFF" # White background for transparency
```

Essas configurações são úteis quando o PNG será impresso ou incorporado em documentos que não suportam canais alfa.

## Script completo – código **svg to png** pronto‑para‑executar

Abaixo está o programa completo que inclui tratamento de erros e configurações opcionais personalizadas. Copie‑o para um arquivo chamado `svg_to_png.py` e execute `python svg_to_png.py`.

```python
"""
Complete script to save SVG as PNG using the Aspose.SVG library.
It demonstrates the basic flow and optional customizations.
"""

import sys
from aspose.svg import SVGDocument, PngSaveOptions
from PIL import Image

def convert_svg_to_png(
    svg_path: str,
    png_path: str,
    dpi: int = 96,
    background: str = None,
) -> None:
    """
    Loads an SVG file, applies PNG save options, and writes the PNG file.
    
    Args:
        svg_path: Path to the source SVG file.
        png_path: Desired output PNG file path.
        dpi: Dots per inch for the rasterized image (default 96).
        background: Hex color (e.g., "#FFFFFF") for the PNG background.
                     If None, the original SVG transparency is kept.
    """
    try:
        # Load SVG
        svg_doc = SVGDocument(svg_path)

        # Prepare PNG options
        png_options = PngSaveOptions()
        png_options.dpi = dpi
        if background:
            png_options.background_color = background

        # Save as PNG
        svg_doc.save(png_path, png_options)

        # Verify result
        with Image.open(png_path) as img:
            print(f"Successfully saved PNG → {png_path}")
            print(f"Image size: {img.size} (pixels), mode: {img.mode}")

    except Exception as e:
        print(f"Error during conversion: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    # Example usage – replace paths as needed
    SVG_INPUT = "YOUR_DIRECTORY/vector.svg"
    PNG_OUTPUT = "YOUR_DIRECTORY/vector.png"

    convert_svg_to_png(
        svg_path=SVG_INPUT,
        png_path=PNG_OUTPUT,
        dpi=300,               # High‑resolution export
        background="#FFFFFF", # White background for transparent SVGs
    )
```

**Saída esperada**

```
Successfully saved PNG → YOUR_DIRECTORY/vector.png
Image size: (800, 600) (pixels), mode: RGB
```

As dimensões da imagem refletem o `viewBox` do SVG ou o DPI que você especificou.

## Armadilhas comuns e como evitá‑las

| Sintoma | Causa | Correção |
|---------|-------|----------|
| PNG está em branco ou totalmente transparente | `background_color` não definido para um SVG que depende de transparência | Defina `png_options.background_color` para um valor hexadecimal sólido. |
| Saída está borrada | DPI deixado no padrão 96 para um SVG de alta detalhe | Aumente `png_options.dpi` para 300 ou mais. |
| Script falha com `FileNotFoundError` | Caminho errado para o arquivo SVG | Use caminhos absolutos ou verifique `os.path.exists(svg_path)`. |
| Desvio de cor no PNG | O SVG usa perfis ICC não suportados pela biblioteca | Rasterize com outra biblioteca (por exemplo, `cairosvg`) ou achate as cores antes da exportação. |

## Próximos passos

* **Conversão em lote** – Percorra um diretório de SVGs e reutilize `convert_svg_to_png`.  
* **Integrar com serviços web** – Exponha a função como um endpoint Flask para converter uploads em tempo real.  
* **Explorar outros formatos** – `PngSaveOptions` tem irmãos como `JpegSaveOptions` e `BmpSaveOptions` para necessidades de exportação adicionais.

Ao dominar o fluxo de trabalho **save svg as png**, você pode automatizar pipelines de ativos, gerar miniaturas para galerias ou preparar gráficos para relatórios PDF — tudo a partir de um único script Python.

---


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Converter SVG para PNG em Python – Guia de Exportação em Alta Resolução](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Converter SVG para PNG em Python – Guia Completo Passo a Passo](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)
- [Converter SVG para PNG em Python usando Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}