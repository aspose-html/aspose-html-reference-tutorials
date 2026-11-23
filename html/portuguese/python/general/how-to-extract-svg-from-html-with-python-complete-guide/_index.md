---
category: general
date: 2026-05-31
description: Aprenda como extrair SVG de HTML usando Python. Este tutorial passo a
  passo mostra como ler documentos HTML, salvar arquivos SVG e salvar SVG embutido
  de forma eficiente.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: pt
og_description: Como extrair SVG de HTML usando Python. Siga este tutorial para ler
  documentos HTML, salvar arquivos SVG e manipular SVG embutido com facilidade.
og_title: Como extrair SVG de HTML com Python – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Como extrair SVG de HTML com Python – Guia Completo
url: /pt/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como extrair SVG de HTML com Python – Guia Completo

Já se perguntou **como extrair SVG** de uma página HTML bagunçada sem perder a cabeça? Você não está sozinho. Seja construindo um web‑scraper, um pipeline de design ou apenas precisando exportar ícones em lote, saber **como extrair SVG** é um truque útil que economiza tempo e dores de cabeça.

Neste tutorial vamos mostrar exatamente **como extrair SVG** usando a biblioteca Aspose.HTML para Python. Vamos ler o documento HTML, extrair tanto o markup `<svg>` inline **quanto** as referências externas a SVG, e então **salvar arquivos SVG** no disco — tudo em um script limpo e reutilizável. Ao final, você terá uma solução pronta‑para‑executar que pode adaptar aos seus próprios projetos.

> **Dica de especialista:** Se você só precisa de uma rápida inspeção da página, `BeautifulSoup` também funciona, mas Aspose.HTML fornece um DOM completo, tornando a extração tanto de SVGs inline quanto vinculados muito simples.

## O que você vai precisar

Antes de mergulharmos, certifique‑se de que tem:

* Python 3.8+ (o código usa f‑strings, então 3.6+ é o mínimo absoluto)
* `pip install aspose-html` – a biblioteca comercial que alimenta nossa análise de HTML
* Uma pasta com um arquivo `input.html` que contém os SVGs que você quer extrair
* Permissão de escrita no diretório de saída (vamos chamá‑lo de `YOUR_DIRECTORY`)

É só isso — sem binários extras, sem navegadores headless. Simples, né?

## Etapa 1: Ler o documento HTML com Aspose.HTML

A primeira coisa que você precisa fazer é **ler o documento HTML** para poder percorrer sua árvore DOM. Aspose.HTML fornece um objeto `HTMLDocument` que se comporta como o `document` de um navegador.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Por que isso importa:* Ao carregar o HTML em um DOM adequado, você evita as armadilhas da análise baseada em regex e ganha métodos como `get_elements_by_tag_name` e `query_selector_all` gratuitamente.

## Etapa 2: Coletar todos os elementos <svg> inline

SVGs inline são aqueles blocos `<svg>…</svg>` que ficam diretamente dentro do HTML. Para **salvar SVG inline** basta obter o HTML externo deles.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Observe que estamos adicionando o markup bruto diretamente em `svg_contents`. Mais tarde decidiremos se cada entrada é markup ou um caminho de arquivo.

## Etapa 3: Encontrar referências SVG externas (tags img e object)

Muitas páginas vinculam arquivos SVG externos via `<img src="icon.svg">` ou `<object data="logo.svg">`. Para **extrair SVG de HTML** precisamos capturar essas URLs também.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Alerta de caso extremo:* Se a URL do SVG for relativa, você deverá juntá‑la com o caminho base do arquivo HTML. Para simplificar, assumimos que o HTML está ao lado dos arquivos SVG.

## Etapa 4: Gravar cada SVG em um arquivo separado

Agora que temos uma lista mista de strings de markup e caminhos de arquivo, vamos iterar e **salvar arquivos SVG**. O script distingue automaticamente entre markup inline e referência a um arquivo existente.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**O que você verá:** Depois que o script terminar, `YOUR_DIRECTORY` conterá arquivos nomeados `svg_0.svg`, `svg_1.svg`, … cada um contendo ou o markup inline original ou uma cópia do SVG externo.

### Saída esperada

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Se um arquivo referenciado estiver ausente, o script imprime um aviso mas continua — então um link quebrado não interrompe toda a extração.

## Lidando com armadilhas comuns

| Problema | Por que acontece | Correção rápida |
|----------|------------------|-----------------|
| **URLs relativas quebram** | O atributo `src` pode ser `"../assets/icon.svg"` | Use `os.path.join(os.path.dirname(html_path), src)` para resolver. |
| **Nomes de arquivo duplicados** | Dois SVGs com o mesmo nome são sobrescritos | Inclua um hash do conteúdo no nome do arquivo (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **SVGs inline grandes causam picos de memória** | Armazenar todo o markup em uma lista antes de gravar | Transmita cada elemento diretamente para um arquivo em vez de fazer buffer. |
| **Imagens não‑SVG passam despercebidas** | Algumas tags `<img>` terminam com `.svg?version=1` | Remova a string de consulta antes da verificação da extensão (`src.split('?')[0]`). |

## Script completo que você pode copiar‑colar

Abaixo está o programa completo, pronto‑para‑executar. Salve como `extract_svg.py`, ajuste `YOUR_DIRECTORY` e execute `python extract_svg.py`.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## Recapitulando – Como extrair SVG em poucas palavras

* **Ler documento HTML** com `HTMLDocument`.
* **Coletar SVG inline** via `get_elements_by_tag_name`.
* **Localizar SVGs externos** usando um seletor CSS que termina em `.svg`.
* **Salvar cada parte** — gravar markup direto em um arquivo ou copiar o arquivo referenciado.
* **Tratar casos extremos** como caminhos relativos, duplicatas e arquivos ausentes.

Essa é a resposta completa para **como extrair SVG** de uma página HTML, encapsulada em um único script fácil de modificar.

## O que vem a seguir?

Agora que você pode **extrair SVG** de forma confiável, considere estas ideias de continuação:

* **Processamento em lote:** Percorra um diretório de arquivos HTML para construir uma biblioteca de ícones.
* **Otimização:** Execute cada SVG salvo através do SVGO (um otimizador Node.js) para reduzir o tamanho do arquivo.
* **Conversão:** Use `cairosvg` ou `svglib` para transformar os SVGs em PNGs para navegadores legados.
* **Extração de metadados:** Analise tags `<title>` ou `<desc>` dentro de cada SVG para obter rótulos pesquisáveis.

Cada um desses tópicos toca nas nossas palavras‑chave secundárias — **read HTML document**, **save svg files**, **save inline svg**, **extract svg from html** — então você encontrará muito material para explorar.

---

*Feliz hacking! Se encontrar algum obstáculo, deixe um comentário abaixo ou me chame no GitHub. O mundo dos SVGs é vasto, mas com as ferramentas certas, extraí‑los é mamão com açúcar.*

## O que você deve aprender a seguir?

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendre un document SVG au format PNG dans .NET avec Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}