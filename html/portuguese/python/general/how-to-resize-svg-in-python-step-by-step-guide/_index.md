---
category: general
date: 2026-06-16
description: Como redimensionar SVG em Python rapidamente – carregar arquivo SVG em
  Python, editar arquivo SVG em Python e até redimensionar em lote arquivos SVG com
  um pequeno script.
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: pt
og_description: Como redimensionar SVG em Python? Aprenda a carregar arquivos SVG
  em Python, editar arquivos SVG em Python e redimensionar em lote arquivos SVG usando
  um exemplo claro e executável.
og_title: Como redimensionar SVG em Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  headline: How to Resize SVG in Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  name: How to Resize SVG in Python – Step‑by‑Step Guide
  steps:
  - name: '**Collects** every `.svg` file in the source folder.'
    text: '**Collects** every `.svg` file in the source folder.'
  - name: '**Loads** each file using the same routine we used for a single SVG.'
    text: '**Loads** each file using the same routine we used for a single SVG.'
  - name: '**Resizes** to the desired width while keeping the aspect ratio.'
    text: '**Resizes** to the desired width while keeping the aspect ratio.'
  - name: '**Writes** the result to a new folder, leaving originals untouched.'
    text: '**Writes** the result to a new folder, leaving originals untouched.'
  type: HowTo
tags:
- Python
- SVG
- Automation
title: Como Redimensionar SVG em Python – Guia Passo a Passo
url: /pt/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Redimensionar SVG em Python – Tutorial Completo

Já se perguntou **como redimensionar SVG** sem abrir um editor gráfico? Talvez você tenha um logotipo que precise ter 200 px de largura para um banner web, ou esteja preparando dezenas de ícones para um aplicativo móvel. A boa notícia? Você pode fazer tudo em Python — sem Photoshop, sem interface do Inkscape, apenas algumas linhas de código.

Neste guia vamos percorrer o carregamento de um arquivo SVG em Python, a edição de suas dimensões e até a escala de uma pasta inteira de SVGs de uma só vez. Ao final, você será capaz de **load SVG file Python**, **edit SVG file Python** e **batch resize SVG files** com confiança.

## Pré‑requisitos

- Python 3.8+ instalado (o comando padrão `python` funciona)
- A biblioteca `svgwrite` ou `lxml` – usaremos `lxml` porque oferece acesso direto ao DOM.
- Uma pasta de SVGs que você deseja redimensionar (por exemplo, `assets/icons/`)

Você não precisa de nenhuma ferramenta GUI; tudo roda a partir do terminal.

---

## Passo 1: Instalar a Biblioteca Necessária

Primeiro, obtenha o `lxml` do PyPI. É pequeno, rápido e nos permite manipular atributos XML diretamente.

```bash
pip install lxml
```

> **Dica:** Se você estiver trabalhando em um ambiente virtual, ative‑o antes de executar o comando. Isso mantém as dependências do seu projeto organizadas.

## Passo 2: Carregar um Arquivo SVG em Python

Agora vamos **load SVG file Python** — ler o XML, obter o elemento raiz `<svg>` e imprimir seu tamanho atual.

```python
from lxml import etree

def load_svg(path: str) -> etree._ElementTree:
    """
    Load an SVG document and return the parsed XML tree.
    """
    parser = etree.XMLParser(remove_blank_text=True)
    tree = etree.parse(path, parser)
    return tree

# Example usage
svg_path = "assets/logo.svg"
svg_tree = load_svg(svg_path)
root = svg_tree.getroot()
print(f"Original width: {root.get('width')}, height: {root.get('height')}")
```

**Por que isso importa:** `lxml` nos fornece um DOM real, então podemos consultar ou alterar qualquer atributo — perfeito para tarefas de **edit SVG file Python**.

## Passo 3: Alterar a Largura (e Altura) – Como Redimensionar SVG

SVGs são vetoriais, então você pode definir largura, altura ou ambos. Se mudar apenas a largura, o `viewBox` manterá a proporção, mas muitas ferramentas também respeitam um atributo de altura correspondente. Aqui está um helper que redimensiona preservando a proporção original:

```python
def resize_svg(tree: etree._ElementTree, new_width: int) -> None:
    """
    Resize the root <svg> element to `new_width` while preserving aspect ratio.
    """
    root = tree.getroot()
    # Grab original dimensions (they may be in px, pt, or just numbers)
    orig_width = float(root.get("width").replace("px", ""))
    orig_height = float(root.get("height").replace("px", ""))

    # Compute scale factor and new height
    scale = new_width / orig_width
    new_height = round(orig_height * scale, 2)

    # Update attributes
    root.set("width", f"{new_width}px")
    root.set("height", f"{new_height}px")

    # Optional: ensure viewBox exists for better scaling in browsers
    if "viewBox" not in root.attrib:
        viewbox = f"0 0 {orig_width} {orig_height}"
        root.set("viewBox", viewbox)

# Resize to 200 px wide
resize_svg(svg_tree, 200)
```

A função acima é o núcleo de **how to resize SVG**. Ela lê o tamanho atual, calcula uma altura proporcional e grava os novos atributos de volta no arquivo.

## Passo 4: Salvar o SVG Modificado

Depois de editar, você precisa escrever as alterações de volta ao disco. Isso completa o ciclo de **edit SVG file Python**.

```python
def save_svg(tree: etree._ElementTree, destination: str) -> None:
    """
    Write the modified SVG tree to `destination`.
    """
    tree.write(
        destination,
        pretty_print=True,
        xml_declaration=True,
        encoding="UTF-8"
    )
    print(f"Saved resized SVG to {destination}")

# Save as a new file so the original stays untouched
output_path = "assets/logo_resized.svg"
save_svg(svg_tree, output_path)
```

Execute o script inteiro e você verá um novo `logo_resized.svg` com exatamente 200 px de largura.

## Passo 5: Redimensionamento em Lote de Arquivos SVG – Escalar uma Pasta Inteira

Agora que podemos **load SVG file Python**, **edit SVG file Python** e salvá‑los, vamos percorrer um diretório e aplicar a mesma transformação a cada arquivo. Esta é a resposta para **batch resize SVG files**.

```python
import pathlib

def batch_resize(source_dir: str, target_dir: str, width: int) -> None:
    """
    Resize every .svg file in `source_dir` to `width` pixels and store
    the results in `target_dir`.
    """
    src = pathlib.Path(source_dir)
    tgt = pathlib.Path(target_dir)
    tgt.mkdir(parents=True, exist_ok=True)

    svg_files = list(src.glob("*.svg"))
    if not svg_files:
        print("No SVG files found.")
        return

    for svg_path in svg_files:
        try:
            tree = load_svg(str(svg_path))
            resize_svg(tree, width)
            out_path = tgt / svg_path.name
            save_svg(tree, str(out_path))
        except Exception as e:
            print(f"Failed on {svg_path.name}: {e}")

# Example: resize everything in 'assets/icons' to 64 px wide
batch_resize("assets/icons", "assets/icons_resized", 64)
```

### O que isso faz:

1. **Coleta** todos os arquivos `.svg` na pasta de origem.
2. **Carrega** cada arquivo usando a mesma rotina que usamos para um SVG único.
3. **Redimensiona** para a largura desejada mantendo a proporção.
4. **Grava** o resultado em uma nova pasta, deixando os originais intactos.

Agora você tem um pipeline pronto‑para‑usar para **batch resize SVG files**.

## Passo 6: Casos de Borda & Armadilhas Comuns

| Problema | Por que Acontece | Solução |
|----------|------------------|---------|
| Atributos `width`/`height` ausentes | Alguns SVGs dependem apenas do `viewBox`. | Se os atributos estiverem ausentes, recorra às dimensões do viewBox (`viewBox="0 0 w h"`). |
| Unidades diferentes de `px` (ex.: `pt`, `%`) | O script remove apenas `px`. | Expanda a chamada `replace` ou use uma expressão regular para capturar qualquer unidade. |
| Elementos `<symbol>` ou `<use>` complexos | Redimensionar a raiz pode não afetar símbolos aninhados. | Aplique as mesmas alterações de atributos a cada tag `<symbol>`, ou use CSS `transform: scale()`. |
| Caracteres Unicode ou especiais nos nomes de arquivos | `pathlib` lida com a maioria dos casos, mas o Windows pode falhar com certos caracteres. | Garanta que os nomes de arquivos sejam seguros em UTF‑8, ou renomeie antes do processamento. |

Tratar esses pontos antecipadamente evita ícones quebrados inesperados mais tarde.

## Passo 7: Verificar o Resultado

Um rápido teste de sanidade pode ser feito com um pequeno trecho HTML:

```html
<!DOCTYPE html>
<html>
<head><title>SVG Test</title></head>
<body>
  <h3>Original</h3>
  <img src="assets/logo.svg" alt="original logo">
  <h3>Resized</h3>
  <img src="assets/logo_resized.svg" alt="resized logo">
</body>
</html>
```

Abra o arquivo em um navegador — ambas as imagens devem parecer idênticas, mas a redimensionada reportará uma largura de **200 px** nas ferramentas de desenvolvedor.

---

## Conclusão

Agora você sabe **how to resize SVG** usando puro Python, de um único arquivo a um diretório inteiro. O fluxo cobre **load SVG file Python**, **edit SVG file Python** e **batch resize SVG files** — tudo com apenas algumas funções.

Experimente: teste larguras diferentes, experimente redimensionar apenas a altura, ou adicione uma interface de linha de comando usando `argparse`. As possibilidades são infinitas, e o script é leve o suficiente para ser incorporado em pipelines de build, jobs de CI ou utilitários de desktop.

Tem dúvidas sobre manipulação de gradientes, fontes incorporadas ou integração com uma aplicação Flask? Deixe um comentário, e exploraremos esses cantos juntos. Feliz codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui código completo e funcional com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Converter SVG em imagem com Aspose.HTML no .NET](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Converter SVG em PDF com Aspose.HTML no .NET](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [Renderizar documento SVG como PNG com Aspose.HTML no .NET](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}