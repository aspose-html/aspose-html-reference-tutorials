---
category: general
date: 2026-10-28
description: Aprenda a rasterizar SVG em Python e converter SVG para PNG com um script
  simples usando CairoSVG. Salve SVG como PNG em segundos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rasterize svg
- convert svg to png
- save svg as png
- svg to png python
- export svg as png
language: pt
lastmod: 2026-10-28
og_description: 'Como rasterizar SVG em Python: este guia mostra como converter SVG
  para PNG usando CairoSVG, abordando instalação, código e solução de problemas.'
og_image_alt: Screenshot of Python code that rasterizes SVG to PNG
og_title: Como rasterizar SVG em Python – guia rápido de SVG para PNG
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  headline: How to rasterize SVG in Python – convert SVG to PNG easily
  type: TechArticle
- description: Learn how to rasterize SVG in Python and convert SVG to PNG with a
    simple script using CairoSVG. Save SVG as PNG in seconds.
  name: How to rasterize SVG in Python – convert SVG to PNG easily
  steps:
  - name: Why CairoSVG?
    text: '- **Pure Python**: No need for external command‑line tools once the package
      is installed. - **SVG‑compliant**: Supports most SVG 1.1 features, including
      gradients, masks, and text. - **Flexible output**: Besides PNG, you can export
      to PDF, PS, or even raw bytes.'
  - name: Step‑by‑step breakdown
    text: 1. **Install the library** – `pip install cairosvg` pulls in the compiled
      Cairo bindings. 2. **Import the module** – `import cairosvg` gives you access
      to the `svg2png` helper. 3. **Call `svg2png`** – Pass the SVG file path (or
      a URL) and the destination PNG path. Optional `output_width`, `output_he
  - name: Edge cases you might encounter
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | **Large SVG (megapixel dimensions)** | Increase `dpi` or set explicit `output_width`/`output_height`
      to avoid memory spikes. | | **Missing fonts** | Install the required fonts on
      the system or em'
  type: HowTo
tags:
- svg
- python
- image processing
- cairosvg
title: Como rasterizar SVG em Python – converta SVG para PNG facilmente
url: /pt/python/general/how-to-rasterize-svg-in-python-convert-svg-to-png-easily/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como rasterizar SVG em Python – converta SVG para PNG facilmente

Se você precisa **como rasterizar svg** para um web‑app, um relatório ou uma build automatizada, este guia oferece uma solução pronta‑para‑usar. Você verá como **converter svg para png** com apenas algumas linhas de Python, e o resultado será um PNG nítido que pode ser armazenado ou servido instantaneamente.

O tutorial cobre tudo, desde a instalação da biblioteca necessária até o tratamento de casos extremos, como arquivos grandes ou configurações de DPI personalizadas. Ao final, você será capaz de **salvar svg como png**, **exportar svg como png** e integrar o processo em qualquer fluxo de trabalho Python.

## O que você precisará

- Python 3.8+ (o código funciona em 3.9, 3.10 e versões mais recentes)
- `pip` para instalar pacotes
- Um arquivo SVG local (por exemplo, `logo.svg`) que você deseja rasterizar
- Opcional: ambiente virtual para gerenciamento limpo de dependências

> **Dica profissional:** Usar um ambiente virtual (`python -m venv .venv`) isola a dependência CairoSVG dos seus pacotes Python globais.

## Como rasterizar SVG em Python

A maneira mais direta de **como rasterizar svg** é com a biblioteca **CairoSVG**. CairoSVG lê o XML do SVG, renderiza-o com o motor gráfico Cairo e grava a imagem rasterizada em PNG, PDF ou outros formatos bitmap.

```bash
# Install CairoSVG and its binary dependencies
pip install cairosvg
```

```python
# rasterize_svg.py
import sys
from pathlib import Path
import cairosvg

def rasterize_svg(input_path: str, output_path: str,
                  width: int | None = None,
                  height: int | None = None,
                  dpi: int = 96) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the PNG file.
    width : int | None
        Desired output width in pixels (maintains aspect ratio if height is None).
    height : int | None
        Desired output height in pixels (maintains aspect ratio if width is None).
    dpi : int
        Dots per inch for the rasterization. Higher DPI yields larger files but more detail.
    """
    try:
        # CairoSVG can read from a file path directly
        cairosvg.svg2png(url=Path(input_path).as_uri(),
                         write_to=output_path,
                         output_width=width,
                         output_height=height,
                         dpi=dpi)
        print(f"✅ Successfully saved PNG to {output_path}")
    except Exception as e:
        print(f"❌ Failed to rasterize {input_path}: {e}", file=sys.stderr)
        raise

if __name__ == "__main__":
    # Example usage:
    # python rasterize_svg.py ./assets/logo.svg ./output/logo.png 300 300
    if len(sys.argv) < 3:
        print("Usage: python rasterize_svg.py <input_svg> <output_png> [width] [height] [dpi]")
        sys.exit(1)

    input_svg = sys.argv[1]
    output_png = sys.argv[2]
    w = int(sys.argv[3]) if len(sys.argv) > 3 else None
    h = int(sys.argv[4]) if len(sys.argv) > 4 else None
    d = int(sys.argv[5]) if len(sys.argv) > 5 else 96

    rasterize_svg(input_svg, output_png, width=w, height=h, dpi=d)
```

### Por que CairoSVG?

- **Pure Python**: Não há necessidade de ferramentas externas de linha de comando depois que o pacote está instalado.
- **Compatível com SVG**: Suporta a maioria dos recursos do SVG 1.1, incluindo gradientes, máscaras e texto.
- **Saída flexível**: Além de PNG, você pode exportar para PDF, PS ou até mesmo bytes crus.

### Divisão passo a passo

1. **Instale a biblioteca** – `pip install cairosvg` traz as ligações compiladas do Cairo.
2. **Importe o módulo** – `import cairosvg` lhe dá acesso ao helper `svg2png`.
3. **Chame `svg2png`** – Passe o caminho do arquivo SVG (ou uma URL) e o caminho de destino PNG. Os parâmetros opcionais `output_width`, `output_height` e `dpi` permitem controlar tamanho e resolução.
4. **Trate erros** – O bloco `try/except` imprime uma mensagem clara se o SVG estiver malformado ou se o diretório de saída for não gravável.

## Converta SVG para PNG com CairoSVG

Se você precisa apenas de uma linha única para conversão rápida, o trecho a seguir faz o trabalho sem a função wrapper:

```python
import cairosvg

cairosvg.svg2png(url="logo.svg", write_to="logo.png")
```

Esta é a ilustração mais concisa de **convert svg to png**. Ele lê `logo.svg` do diretório atual e grava `logo.png` ao lado.

## Salve SVG como PNG – verifique o resultado

Após executar o script, você deverá ver um arquivo PNG no caminho de destino. Abra-o com qualquer visualizador de imagens para confirmar:

```bash
# Linux/macOS
xdg-open ./output/logo.png   # or open on macOS
# Windows
start ./output/logo.png
```

Se o PNG aparecer borrado, aumente o argumento `dpi` (por exemplo, `dpi=300`) para gerar um raster de resolução mais alta.

## Exporte SVG como PNG em diferentes formatos

CairoSVG também pode gerar **PDF**, **PostScript** ou bytes crus de **PNG**. Abaixo está um exemplo de exportação para um objeto `BytesIO` quando você precisa da imagem em memória (por exemplo, para uma resposta Flask):

```python
import io
import cairosvg

svg_path = "logo.svg"
png_bytes = io.BytesIO()
cairosvg.svg2png(url=Path(svg_path).as_uri(), write_to=png_bytes)
png_bytes.seek(0)  # Ready for sending over HTTP
```

### Casos extremos que você pode encontrar

| Situação                                 | Tratamento recomendado |
|------------------------------------------|------------------------|
| **SVG grande (dimensões megapixel)**     | Aumente `dpi` ou defina `output_width`/`output_height` explícitos para evitar picos de memória. |
| **Fontes ausentes**                      | Instale as fontes necessárias no sistema ou incorpore‑as no SVG usando tags `<style>`. |
| **Problemas de transparência**           | PNG preserva alfa por padrão; se precisar de fundo sólido, passe `background_color="#FFFFFF"` para `svg2png`. |
| **Processamento em lote**                | Percorra um diretório de SVGs e chame `rasterize_svg` para cada arquivo. |

## Exemplo completo funcional

Abaixo está um script mínimo e autocontido que você pode copiar‑colar em um arquivo chamado `svg_to_png.py` e executar imediatamente.

```python
# svg_to_png.py
import cairosvg
from pathlib import Path

def main():
    src = Path("example.svg")
    dst = Path("example.png")
    if not src.is_file():
        raise FileNotFoundError(f"Source SVG not found: {src}")

    # Convert with default DPI (96) and keep original dimensions
    cairosvg.svg2png(url=src.as_uri(), write_to=dst)
    print(f"✅ {src.name} → {dst.name} created successfully.")

if __name__ == "__main__":
    main()
```

Executando `python svg_to_png


## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [How to Rasterize SVG in Python – Complete Guide](/html/english/python/general/how-to-rasterize-svg-in-python-complete-guide/)
- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}