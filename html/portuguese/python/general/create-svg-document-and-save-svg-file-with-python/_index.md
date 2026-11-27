---
category: general
date: 2026-11-27
description: Criar documento SVG e salvar arquivo SVG usando Python. Aprenda a exportar
  vetor como SVG e gerar uma imagem SVG rapidamente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: pt
lastmod: 2026-11-27
og_description: Crie um documento SVG e salve o arquivo SVG com Python. Este guia
  mostra como exportar vetores como SVG e produzir uma imagem SVG em minutos.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Criar documento SVG e salvar arquivo SVG usando Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Criar documento SVG e salvar arquivo SVG com Python
url: /pt/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar documento SVG e salvar arquivo SVG com Python

Se você precisar **criar documento SVG** do zero, este guia o conduzirá por todo o processo. Você verá como **salvar arquivo SVG** no disco, exportar o vetor como SVG e obter uma imagem SVG pronta‑para‑uso em apenas algumas linhas de código.

Gerar gráficos escaláveis programaticamente é útil para relatórios, ícones de UI ou qualquer situação em que você queira imagens independentes de resolução. Ao final deste tutorial você será capaz de responder “**como criar SVG**?” para formas simples e estender o padrão para arte vetorial complexa.

## O que você precisará

- Python 3.8 ou mais recente  
- O pacote `svgwrite` (instalável via `pip`)  
- Um diretório gravável para o arquivo de saída  

Nenhum editor gráfico externo é necessário; tudo roda a partir da linha de comando.

## Etapa 1: Instalar a biblioteca `svgwrite`

`svgwrite` fornece uma API limpa e Pythonic para construir marcação SVG. Instale-a uma vez com:

```bash
pip install svgwrite
```

> **Dica profissional:** Use um ambiente virtual (`python -m venv .venv`) para manter as dependências isoladas.

## Etapa 2: Criar documento SVG

Agora realmente **criamos objetos de documento SVG**. A classe `Drawing` representa o elemento raiz `<svg>` e lida com namespaces automaticamente.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

A instância `Drawing` é o ponto de entrada para todas as operações SVG subsequentes. Ao especificar `size` definimos as dimensões da tela, o que influencia como os navegadores renderizam a imagem.

## Etapa 3: Adicionar um elemento círculo vermelho

Adicionar formas é simples. O método `circle` cria um elemento `<circle>`; então o anexamos à raiz.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Por que escolhemos um círculo: círculos são primitivas vetoriais que demonstram escalabilidade sem perda de qualidade, tornando a saída ideal para testar fluxos de trabalho de **exportar vetor como SVG**.

## Etapa 4: Salvar arquivo SVG

Finalmente, escreva a marcação no disco. Esta etapa cumpre o requisito de **salvar arquivo SVG** e produz um arquivo que você pode abrir em qualquer navegador ou editor vetorial.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Ao executar o script, você verá uma mensagem no console confirmando a localização do arquivo gerado.

### Saída esperada

O `circle.svg` resultante contém:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Abrir o arquivo em um navegador exibe um círculo vermelho nítido e, como é baseado em vetor, você pode ampliar indefinidamente sem pixelização.

## Etapa 5: Variações comuns e casos de borda

### Exportando vetores mais complexos

Se você precisar **exportar vetor como SVG** para ilustrações com múltiplas formas, basta repetir o padrão `dwg.add()` com outras primitivas (`rect`, `line`, `path`, etc.). Por exemplo:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Lidando com Unicode e texto

SVG suporta elementos de texto com suporte total a Unicode. Use `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` para incorporar rótulos multilíngues.

### Salvando em um local diferente

Ao **salvar imagem SVG** em uma pasta especificada pelo usuário, valide o caminho para evitar erros de permissão:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Minificando a saída

Para pipelines de produção, você pode querer um tamanho de arquivo menor. Passe `pretty=False` para `dwg.tostring()` e escreva o resultado manualmente:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## Como criar SVG com bibliotecas alternativas (opcional)

Embora `svgwrite` seja leve e puro‑Python, outros ecossistemas existem:

- **cairosvg** – converte PNG, PDF ou HTML para SVG.  
- **lxml** – permite construir marcação SVG manualmente usando APIs XML.  

Escolher uma biblioteca depende da complexidade do seu projeto e das dependências existentes.

## Conclusão

Agora você sabe como **criar documento SVG**, adicionar formas vetoriais e **salvar arquivo SVG** usando Python. A solução completa demonstra os passos para **exportar vetor como SVG**, gerar uma **imagem SVG** e responder à pergunta comum **como criar SVG** programaticamente.

A partir daqui você pode:

- Estender o script com loops para gerar gráficos ou ícones automaticamente.  
- Integrar a saída SVG em aplicações web ou modelos de email.  
- Explorar animação adicionando elementos `<animate>` com `svgwrite`.  

Experimente diferentes formas, cores e gradientes para aproveitar ao máximo o poder dos gráficos vetoriais escaláveis em seus projetos Python. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Criar Documento SVG – Adicionar um Círculo e Salvar como SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Criar Documento SVG em Python – Guia de Conversão de SVG para PNG](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Carregar Arquivo SVG Python – Guia Completo de Exportação, Incorporação e Conversão](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}