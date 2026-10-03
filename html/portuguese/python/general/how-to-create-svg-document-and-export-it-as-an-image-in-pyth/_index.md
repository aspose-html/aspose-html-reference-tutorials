---
category: general
date: 2026-10-02
description: Aprenda a criar documentos SVG em Python, salvar SVG em um arquivo e
  exportar a imagem SVG com um script curto e completo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: pt
lastmod: 2026-10-02
og_description: Crie um documento SVG em Python e exporte a imagem SVG com este tutorial
  prático. Siga o script, salve o SVG em um arquivo e reutilize o gráfico vetorial
  instantaneamente.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Crie um documento SVG em Python – guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Como criar um documento SVG e exportá-lo como imagem em Python
url: /pt/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como criar documento SVG e exportá-lo como imagem em Python

Se você precisar **create SVG document** programaticamente, este tutorial mostra exatamente como fazer isso com Python. Você verá um script completo que cria um círculo simples, salva o SVG em um arquivo e produz uma imagem SVG exportável que pode ser incorporada em qualquer lugar.

Gerar gráficos vetoriais escaláveis a partir de código elimina o esforço manual de desenhar formas em um editor GUI. Ao final deste guia, você poderá integrar a criação de SVG em pipelines de visualização de dados, geradores de relatórios automatizados ou qualquer projeto que exija gráficos nítidos e independentes de resolução.

## Pré-requisitos

- Python 3.8 ou superior instalado
- A biblioteca `svgwrite` (instale com `pip install svgwrite`)
- Permissão de escrita no diretório onde o SVG será salvo

Esses requisitos mantêm o exemplo leve e compatível com a maioria dos ambientes.

## Etapa 1: Instalar e importar a biblioteca SVG

O primeiro passo é adicionar a biblioteca de terceiros que fornece uma API conveniente para a criação de SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` abstrai a estrutura XML de um arquivo SVG, permitindo que você se concentre na geometria em vez de marcação bruta.

## Etapa 2: Criar um objeto de documento SVG

Agora você pode **create SVG document** instanciando `svgwrite.Drawing`. Este objeto representa o elemento raiz `<svg>` e contém todas as formas subsequentes.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

O argumento `size` define as dimensões em pixels renderizadas, enquanto `viewBox` estabelece um sistema de coordenadas que corresponde à geometria que você definirá mais tarde.

## Etapa 3: Adicionar um elemento círculo

Um círculo é definido por seu centro (`cx`, `cy`) e raio (`r`). Use o helper `circle` para atribuir esses atributos.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

O círculo fica no meio da tela de 100 × 100, deixando uma margem de 10 pixels em cada lado. Ajuste `fill` e `stroke` para combinar com a linguagem de design.

## Etapa 4: Salvar o SVG em arquivo

Com o gráfico montado, você pode **save SVG to file** usando o método `save`. Isso grava XML bem‑formado que navegadores e editores vetoriais entendem.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

O arquivo `circle.svg` agora está no diretório de trabalho atual. Você pode abri‑lo em um navegador web, Inkscape ou qualquer ferramenta que suporte o formato SVG.

## Etapa 5: Verificar a imagem SVG exportada

Abra o arquivo salvo em um navegador para confirmar o resultado. Você deve ver um círculo centralizado com as cores especificadas. O XML bruto se parece com isto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Como o SVG é baseado em vetores, você pode escalar a imagem sem perda de qualidade, tornando‑a ideal para designs web responsivos ou impressão de alta resolução.

## Dica profissional: Exportar SVG como PNG ou JPEG

Se você precisar de uma versão raster, combine o arquivo SVG com uma ferramenta de conversão como **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Esta etapa demonstra **export SVG image** para um formato bitmap, útil quando sistemas downstream não podem renderizar SVG diretamente.

## Variações comuns e casos de borda

| Variação | Como lidar |
|-----------|---------------|
| Multiple shapes | Call `dwg.add()` for each new element (rect, line, path). |
| Dynamic dimensions | Compute `size` and `viewBox` from data before creating `Drawing`. |
| Text labels | Use `dwg.text("Label", insert=("10", "20"))` and style with `font_size` and `fill`. |
| Re‑using the document | Keep the `Drawing` object in memory and call `save()` whenever you need an updated file. |
| Large files | Stream the output using `dwg.tostring()` and write to a file object manually to avoid memory spikes. |

Abordar esses cenários garante que seu script **how to generate SVG** escale de ícones simples a diagramas complexos.

## Recapitulação do script completo

Abaixo está o exemplo completo e executável que incorpora todas as etapas e a conversão opcional:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Executar este script produz `circle.svg` e, se `cairosvg` estiver instalado, `circle.png`. Ambos os arquivos estão prontos para inclusão em páginas web, relatórios ou processamento adicional.

## Conclusão

Agora você sabe como **create SVG document** em Python, **save SVG to file**, e **export SVG image** para uso mais amplo. O exemplo cobre as chamadas de API essenciais, explica por que cada etapa é importante e oferece extensões para gráficos mais complexos.

Em seguida, explore tópicos adicionais do **SVG Python tutorial**, como desenhar caminhos, aplicar gradientes e animar elementos. Integrar essas técnicas permitirá que você gere gráficos vetoriais dinâmicos e orientados por dados diretamente de suas aplicações Python. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar e Gerenciar Documentos SVG no Aspose.HTML para Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Salvar Documento SVG no Aspose.HTML para Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Converter SVG para Imagem com Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}