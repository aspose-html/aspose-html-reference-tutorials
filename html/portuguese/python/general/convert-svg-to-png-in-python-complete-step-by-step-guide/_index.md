---
category: general
date: 2026-06-19
description: Converta SVG para PNG em Python de forma rápida e fácil. Aprenda como
  salvar SVG como PNG, lidar com a conversão de SVG para PNG e exportar SVG para PNG
  com um script simples.
draft: false
keywords:
- convert svg to png
- save svg as png
- svg to png conversion
- svg to png python
- export svg to png
language: pt
og_description: Converta SVG para PNG em Python com este tutorial prático. Aprenda
  todo o processo de conversão de SVG para PNG e como exportar SVG para PNG de forma
  eficiente.
og_title: Converter SVG para PNG em Python – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Convert SVG to PNG in Python quickly and easily. Learn how to save
    SVG as PNG, handle svg to png conversion, and export SVG to PNG with a simple
    script.
  headline: Convert SVG to PNG in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert SVG to PNG in Python quickly and easily. Learn how to save
    SVG as PNG, handle svg to png conversion, and export SVG to PNG with a simple
    script.
  name: Convert SVG to PNG in Python – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - An SVG file you want to transform (we’ll use `logo.svg`
      as an example).'
  - name: Why This Approach Works
    text: '- **Explicit I/O handling:** By reading the SVG as bytes, we avoid issues
      with Unicode encodings that sometimes crop up on Windows. - **Custom DPI:**
      Scaling is often required when the target PNG must match a specific pixel density
      (think print vs. screen). - **Optional background:** Some SVGs have '
  - name: Expected Result
    text: '- `output/logo.png` – a 1:1 raster of the original SVG, preserving any
      transparency. - `output/logo_highres.png` – a 300 DPI version with a white background,
      perfect for print.'
  - name: 1. **What if the SVG uses external fonts?**
    text: '`cairosvg` tries to embed referenced fonts, but it only sees files on the
      local filesystem. Copy the font files next to the SVG or embed them directly
      in the SVG with `<style>` tags. Otherwise you’ll get fallback fonts in the PNG.'
  - name: 2. **How do I keep the original aspect ratio when scaling?**
    text: Pass only `dpi` and let Cairo compute the pixel dimensions from the SVG’s
      viewBox. If you need a fixed width/height, calculate the appropriate DPI yourself
      or use the `output_width`/`output_height` arguments provided by `svg2png`.
  - name: 3. **Can I convert large SVGs without exhausting memory?**
    text: Yes. `cairosvg` streams the rasterization, but you should avoid loading
      massive SVGs into memory all at once. Process them one by one, as shown in the
      batch example.
  - name: 4. **Is the conversion thread‑safe?**
    text: The underlying Cairo library is not fully thread‑safe on all platforms.
      If you plan to run conversions in parallel, wrap calls in a multiprocessing
      pool rather than threading.
  - name: What’s Next?
    text: '- Explore **svg to png conversion** with alternative libraries like `svglib`
      + `reportlab` for PDF‑first workflows. - Combine this script with image‑optimization
      tools (e.g., `pngquant`) to shrink file size for the web. - Add a CLI wrapper
      using `argparse` or `click` so you can run `python -m conver'
  type: HowTo
tags:
- Python
- Image Processing
- SVG
title: Converter SVG para PNG em Python – Guia Completo Passo a Passo
url: /pt/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter SVG para PNG em Python – Guia Completo Passo a Passo

Já precisou **convert SVG to PNG** mas não tinha certeza de qual biblioteca escolher? Você não está sozinho—muitos desenvolvedores encontram esse obstáculo ao tentar incorporar gráficos vetoriais em ativos web ou gerar miniaturas em tempo real. A boa notícia? Com apenas algumas linhas de Python você pode **save SVG as PNG** e manter seu pipeline de build fluido.

Neste tutorial vamos percorrer uma prática **svg to png conversion** usando uma biblioteca popular, cobrir as nuances do código **svg to png python** e mostrar como **export SVG to PNG** com tratamento de erros adequado. Ao final, você terá uma função reutilizável que pode inserir em qualquer projeto, seja construindo uma ferramenta CLI ou um serviço de imagens server‑side.

## O que você aprenderá

- As dependências mínimas necessárias para **convert svg to png** em Python.  
- Como carregar um arquivo SVG, configurar opções de exportação PNG e gravar a imagem de saída.  
- Armadilhas comuns (fundos transparentes, dimensões grandes) e como evitá‑las.  
- Um script pronto‑para‑executar que você pode adaptar para processamento em lote ou integrar a um endpoint Flask/Django.

### Pré‑requisitos

- Python 3.8+ instalado na sua máquina.  
- Familiaridade básica com pip e ambientes virtuais.  
- Um arquivo SVG que você deseja transformar (usaremos `logo.svg` como exemplo).

Se você já tem isso, ótimo—vamos mergulhar.

## Etapa 1: Instalar a Biblioteca Necessária

A maneira mais direta de **convert SVG to PNG** em Python é com o pacote `cairosvg`. Ele encapsula a biblioteca gráfica Cairo e lida com a rasterização vetorial nos bastidores.

```bash
pip install cairosvg
```

> **Dica profissional:** Fixe a versão (por exemplo, `cairosvg==2.7.0`) no seu `requirements.txt` para evitar quebras inesperadas quando uma nova versão major for lançada.

## Etapa 2: Escrever uma Função de Conversão Simples

Agora que a biblioteca está instalada, vamos criar um pequeno helper que faz o trabalho pesado. Esta função encapsula a lógica **svg to png python**, facilitando a reutilização.

```python
# convert_svg_to_png.py
import os
from cairosvg import svg2png

def convert_svg_to_png(
    input_path: str,
    output_path: str,
    dpi: int = 96,
    background_color: str = None,
) -> None:
    """
    Convert an SVG file to a PNG image.

    Parameters
    ----------
    input_path : str
        Path to the source SVG file.
    output_path : str
        Destination path for the generated PNG.
    dpi : int, optional
        Dots per inch for the rasterized image (default: 96).
    background_color : str, optional
        Hex color (e.g., "#FFFFFF") to use as background.
        If None, the SVG's own transparency is preserved.

    Raises
    ------
    FileNotFoundError
        If the input SVG does not exist.
    ValueError
        If the output directory cannot be created.
    """
    # Validate input file
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"SVG file not found: {input_path}")

    # Ensure output directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Read the SVG content
    with open(input_path, "rb") as svg_file:
        svg_bytes = svg_file.read()

    # Perform the conversion
    svg2png(
        bytestring=svg_bytes,
        write_to=output_path,
        dpi=dpi,
        background_color=background_color,
    )
    print(f"✅ Successfully saved PNG to {output_path}")
```

### Por que esta abordagem funciona

- **Manipulação explícita de I/O:** Ao ler o SVG como bytes, evitamos problemas com codificações Unicode que às vezes surgem no Windows.  
- **DPI personalizado:** O dimensionamento costuma ser necessário quando o PNG de destino deve corresponder a uma densidade de pixels específica (pense em impressão vs. tela).  
- **Fundo opcional:** Alguns SVGs têm regiões transparentes; passar uma cor hex permite **export SVG to PNG** com um fundo sólido, o que é útil para miniaturas de UI.

## Etapa 3: Executar o Script de Conversão

Com a função pronta, vamos converter um arquivo real. Coloque `logo.svg` em uma pasta chamada `assets/` e execute o script a partir da raiz do projeto.

```python
# demo_conversion.py
from convert_svg_to_png import convert_svg_to_png

if __name__ == "__main__":
    INPUT_SVG = "assets/logo.svg"
    OUTPUT_PNG = "output/logo.png"

    # Simple call – defaults keep transparency and 96 DPI
    convert_svg_to_png(INPUT_SVG, OUTPUT_PNG)

    # Example with a white background and higher DPI for sharper output
    convert_svg_to_png(
        INPUT_SVG,
        "output/logo_highres.png",
        dpi=300,
        background_color="#FFFFFF",
    )
```

Run it:

```bash
python demo_conversion.py
```

You should see console output confirming the files were written:

```
✅ Successfully saved PNG to output/logo.png
✅ Successfully saved PNG to output/logo_highres.png
```

### Resultado esperado

- `output/logo.png` – um raster 1:1 do SVG original, preservando qualquer transparência.  
- `output/logo_highres.png` – uma versão de 300 DPI com fundo branco, perfeita para impressão.

![exemplo de saída de conversão de svg para png](example.png){alt="exemplo de saída de conversão de svg para png"}

*(A captura de tela mostra os arquivos PNG abertos em um visualizador de imagens, confirmando que a conversão foi bem‑sucedida.)*

## Etapa 4: Processar em Lote Vários SVGs (Opcional)

Se precisar **save SVG as PNG** para um diretório inteiro, um pequeno loop resolve. Este trecho também demonstra tratamento de erros elegante—útil quando alguns SVGs podem estar malformados.

```python
import glob
from pathlib import Path

def batch_convert(source_dir: str, dest_dir: str, **options):
    svg_paths = glob.glob(os.path.join(source_dir, "*.svg"))
    for svg_path in svg_paths:
        try:
            filename = Path(svg_path).stem + ".png"
            output_path = os.path.join(dest_dir, filename)
            convert_svg_to_png(svg_path, output_path, **options)
        except Exception as e:
            print(f"⚠️  Failed to convert {svg_path}: {e}")

if __name__ == "__main__":
    batch_convert(
        source_dir="assets/",
        dest_dir="output/batch/",
        dpi=150,
        background_color="#F0F0F0",
    )
```

Executar isso preencherá `output/batch/` com PNGs para cada SVG em `assets/`. Se um arquivo falhar, o script registra o erro e continua—não é necessário interromper todo o trabalho.

## Perguntas Frequentes & Casos Limite

### 1. **E se o SVG usar fontes externas?**  
`cairosvg` tenta incorporar as fontes referenciadas, mas só vê arquivos no sistema de arquivos local. Copie os arquivos de fonte ao lado do SVG ou incorpore‑os diretamente no SVG com tags `<style>`. Caso contrário, você obterá fontes de fallback no PNG.

### 2. **Como manter a proporção original ao dimensionar?**  
Passe apenas `dpi` e deixe o Cairo calcular as dimensões em pixels a partir do viewBox do SVG. Se precisar de largura/altura fixa, calcule o DPI apropriado você mesmo ou use os argumentos `output_width`/`output_height` fornecidos por `svg2png`.

### 3. **Posso converter SVGs grandes sem esgotar a memória?**  
Sim. `cairosvg` faz streaming da rasterização, mas você deve evitar carregar SVGs massivos na memória de uma só vez. Processá‑los um a um, como mostrado no exemplo em lote.

### 4. **A conversão é segura para threads?**  
A biblioteca Cairo subjacente não é totalmente segura para threads em todas as plataformas. Se você planeja executar conversões em paralelo, envolva as chamadas em um pool de multiprocessing em vez de threading.

## Dicas de Performance

- **Cache o PNG** se o SVG raramente mudar; recomputar a cada requisição desperdiça ciclos de CPU.  
- **Reutilize o mesmo DPI** entre chamadas para evitar cálculos de dimensionamento repetidos.  
- Para serviços web, considere retornar o PNG como um stream `BytesIO` em vez de gravar no disco—isso reduz a latência de I/O.

```python
from io import BytesIO
def convert_svg_to_png_bytes(svg_path: str, dpi: int = 96) -> BytesIO:
    with open(svg_path, "rb") as f:
        svg_bytes = f.read()
    png_bytes = BytesIO()
    svg2png(bytestring=svg_bytes, write_to=png_bytes, dpi=dpi)
    png_bytes.seek(0)
    return png_bytes
```

## Recapitulação

Cobrimos tudo o que você precisa para **convert SVG to PNG** usando Python:

1. Instalar `cairosvg`.  
2. Escrever uma função reutilizável `convert_svg_to_png` que trata DPI, cores de fundo e verificação de erros.  
3. Executar o script em um único arquivo ou processar em lote uma pasta inteira.  
4. Lidar com peculiaridades comuns como fontes externas, preservação da proporção e segurança de threads.

Com esse conhecimento, você agora pode **save SVG as PNG** em qualquer pipeline de automação, integrar a conversão em APIs web ou simplesmente gerar ativos para um sistema de design. 

### O que vem a seguir?

- Explore **svg to png conversion** com bibliotecas alternativas como `svglib` + `reportlab` para fluxos de trabalho PDF‑first.  
- Combine este script com ferramentas de otimização de imagens (por exemplo, `pngquant`) para reduzir o tamanho do arquivo para a web.  
- Adicione um wrapper CLI usando `argparse` ou `click` para que você possa executar `python -m convert_svg_to_png INPUT.svg OUTPUT.png` no terminal.

Tem mais perguntas? Deixe um comentário abaixo, ou faça fork do repositório e experimente diferentes configurações de exportação. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Render SVG Doc as PNG in .NET with Aspose.HTML](/html/english/net/rendering-html-documents/render-svg-doc-as-png/)
- [svg a png java – Convertir SVG a imagen con Aspose.HTML para Java](/html/spanish/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}