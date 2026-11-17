---
category: general
date: 2026-11-17
description: converta svg para png usando Python em poucas linhas. aprenda a salvar
  SVG como PNG com configurações de conversão opcionais.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert svg to png
- save svg as png
- export svg as png
- svg to raster image
- how to convert svg to png
language: pt
lastmod: 2026-11-17
og_description: converter svg para png em Python com um exemplo conciso. siga os passos
  para exportar svg como png de forma eficiente.
og_image_alt: Diagram illustrating convert svg to png workflow in Python
og_title: converter svg para png em Python – guia rápido
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: convert svg to png using Python in a few lines. Learn to save SVG as
    PNG with optional conversion settings.
  headline: How to convert SVG to PNG in Python – step‑by‑step guide
  type: TechArticle
tags:
- svg
- png
- python
- image conversion
title: Como converter SVG para PNG em Python – guia passo a passo
url: /pt/python/general/how-to-convert-svg-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como converter SVG para PNG em Python – guia passo a passo

Se você precisa **converter svg para png**, este guia mostra uma solução completa que você pode executar hoje. Você também verá como **salvar svg como png** com configurações opcionais de tamanho e cor de fundo.

Gerar imagens raster a partir de arquivos SVG vetoriais é comum quando você serve gráficos para navegadores, cria miniaturas ou incorpora imagens em PDFs. O tutorial cobre tudo, desde a instalação da biblioteca necessária até o tratamento de casos extremos, como arquivos ausentes ou SVGs muito grandes.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Python 3.8 ou mais recente instalado.
* Acesso a um terminal ou prompt de comando.
* O pacote `cairosvg`, que realiza o trabalho pesado da conversão **svg para imagem raster**.

Você pode instalar o pacote com um único comando pip:

```bash
pip install cairosvg
```

> **Dica profissional:** Use um ambiente virtual para manter as dependências isoladas de outros projetos.

## Como converter SVG para PNG em Python

O núcleo do processo consiste em três ações: carregar o SVG, ajustar opcionalmente os parâmetros de conversão e gravar o arquivo PNG. O código abaixo implementa as três etapas em uma função reutilizável.

```python
import cairosvg
from pathlib import Path

def convert_svg_to_png(svg_path: str, png_path: str) -> None:
    """
    Convert an SVG file to a PNG raster image.

    Parameters
    ----------
    svg_path : str
        Path to the source SVG file.
    png_path : str
        Destination path for the generated PNG file.
    """
    # Verify that the SVG file exists
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    # Perform the conversion using default settings
    cairosvg.svg2png(url=svg_path, write_to=png_path)

# Example usage
if __name__ == "__main__":
    svg_file = "YOUR_DIRECTORY/image.svg"
    png_file = "YOUR_DIRECTORY/image.png"
    convert_svg_to_png(svg_file, png_file)
    print(f"Converted {svg_file} to {png_file}")
```

### Por que isso funciona

* `cairosvg.svg2png` lê o arquivo SVG (`url=svg_path`) e grava um arquivo PNG (`write_to=png_path`).  
* A função gera um erro claro se o SVG de origem não for encontrado, o que ajuda a depurar problemas de caminho de arquivo logo no início.  
* Manter a lógica de conversão dentro de uma função facilita a reutilização em vários scripts ou a integração em aplicações maiores.

## Opcional: ajuste fino da conversão

Se você precisar de um tamanho de saída específico ou de um fundo diferente, `cairosvg.svg2png` aceita argumentos adicionais. A seguir, uma variante que define largura de 300 px e fundo branco.

```python
def convert_svg_to_png_custom(svg_path: str, png_path: str,
                              width: int = 300,
                              background_color: str = "white") -> None:
    """
    Convert an SVG to PNG with custom dimensions and background.

    Parameters
    ----------
    width : int
        Desired width of the PNG in pixels; height scales proportionally.
    background_color : str
        Hex or named color for the PNG background.
    """
    if not Path(svg_path).is_file():
        raise FileNotFoundError(f"SVG file not found: {svg_path}")

    cairosvg.svg2png(
        url=svg_path,
        write_to=png_path,
        output_width=width,
        background_color=background_color
    )
```

Você pode chamar esta função da mesma forma que a versão básica, passando qualquer largura ou cor que preferir.

## Perguntas comuns e casos extremos

**E se o SVG contiver fontes externas?**  
`cairosvg` incorpora fontes referenciadas automaticamente, mas os arquivos de fonte devem estar acessíveis a partir da localização do SVG. Coloque os arquivos de fonte ao lado do SVG ou use URLs absolutas.

**Como lidar com SVGs muito grandes?**  
Arquivos grandes podem consumir memória significativa. Você pode transmitir o conteúdo do SVG em vez de carregá‑lo do disco:

```python
with open(svg_path, "rb") as svg_stream:
    cairosvg.svg2png(file_obj=svg_stream, write_to=png_path)
```

**Posso converter vários arquivos em lote?**  
Envolva a chamada de conversão em um loop e use `Path.glob("*.svg")` para descobrir todos os SVGs em um diretório.

## Saída esperada

Executar o script de exemplo imprime uma única linha confirmando a conversão:

```
Converted YOUR_DIRECTORY/image.svg to YOUR_DIRECTORY/image.png
```

O arquivo resultante `image.png` fica no mesmo diretório e pode ser aberto com qualquer visualizador de imagens.

## Conclusão

Agora você sabe como **converter svg para png** em Python, como **salvar svg como png** e como **exportar svg como png** com dimensões personalizadas. A mesma abordagem funciona para qualquer arquivo SVG, transformando gráficos vetoriais em um formato **svg para imagem raster** adequado para páginas web, relatórios ou miniaturas.

Próximos passos podem incluir:

* Explorar os parâmetros de `export svg as png` para controle de DPI.  
* Integrar a função de conversão em um endpoint Flask ou Django para gerar imagens sob demanda.  
* Usar a palavra‑chave secundária **how to convert svg to png** para buscar casos de uso mais avançados, como processamento em lote ou pipelines CI/CD.

Sinta‑se à vontade para experimentar diferentes configurações e compartilhar seus resultados com a comunidade!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Convert SVG to PNG in Python – High‑Resolution Export Guide](/html/english/python/general/convert-svg-to-png-in-python-high-resolution-export-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)
- [Convert SVG to PNG in Python – Complete Step‑by‑Step Guide](/html/english/python/general/convert-svg-to-png-in-python-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}