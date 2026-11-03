---
category: general
date: 2026-05-31
description: Aprenda como obter um elemento por ID, mudar a cor de fundo em HTML,
  ler o texto HTML e definir atributos HTML usando Python. Tutorial passo a passo.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: pt
og_description: Obtenha o elemento por ID, leia o texto HTML, defina o atributo HTML
  e altere a cor de fundo do HTML usando Python em um guia único e fácil de seguir.
og_title: Obtenha o elemento por ID em Python – Tutorial completo de manipulação de
  HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: Obtenha o elemento por ID em Python – Guia completo de manipulação de HTML
url: /pt/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obter elemento por id em Python – Guia Completo de Manipulação de HTML

Já precisou **obter elemento por id** de uma página HTML enquanto escrevia um script rápido em Python? Você não está sozinho — a maioria dos desenvolvedores encontra esse obstáculo ao começar a rastrear sites ou ajustar relatórios locais. A boa notícia? Com algumas linhas de código você pode ler o texto do elemento, mudar sua cor de fundo e até definir novos atributos, tudo sem sair do seu editor.

Neste tutorial vamos percorrer um exemplo do mundo real: carregar um `sample.html` local, extrair o elemento cujo ID é `main‑content`, imprimir seu texto interno e, por fim, trocar a cor de fundo para um cinza claro. Ao final, você também saberá **como ler texto HTML**, **como definir atributo HTML** e por que **manipular HTML com Python** é uma habilidade útil em qualquer caixa de ferramentas de automação.

## O que você vai precisar

Antes de mergulharmos, certifique‑se de que tem:

- **Python 3.9+** (qualquer versão recente funciona)
- A biblioteca **`lxml`** (ou **BeautifulSoup** se preferir) — usaremos `lxml.html` porque oferece uma API limpa no estilo `get_element_by_id`.
- Um pequeno arquivo HTML chamado `sample.html` dentro de uma pasta chamada `YOUR_DIRECTORY`. Sinta‑se à vontade para copiar o trecho abaixo para esse arquivo:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

É só isso — sem frameworks sofisticados, apenas Python puro e um arquivo HTML estático.

## Etapa 1: Instalar a biblioteca necessária

Se ainda não instalou `lxml`, abra um terminal e execute:

```bash
pip install lxml
```

*Dica de especialista:* usar um ambiente virtual mantém seu Python global organizado, especialmente quando você começa a lidar com vários projetos.

## Etapa 2: Carregar o documento HTML

Agora vamos ler o arquivo em um objeto de documento `lxml.html`. Pense nisso como transformar o texto bruto em uma árvore navegável.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

Ao executar isso, será impresso “Document loaded successfully.” Se o arquivo não for encontrado, o Python levantará um `FileNotFoundError` — é bom capturá‑lo cedo antes de perseguir um elemento fantasma.

## Etapa 3: Obter elemento por id

Aqui está o ponto central. `lxml` nos fornece o conveniente método `get_element_by_id` que espelha a API DOM que você usaria em JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

Quando o elemento existe, você verá “Element found!” impresso no console. Esta é a etapa **obter elemento por id** que alimenta a maioria das manipulações posteriores.

## Etapa 4: Como ler texto HTML

Depois de ter o elemento, extrair seu texto visível é muito fácil. O método `text_content()` devolve tudo que está dentro, sem as tags.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Saída esperada:

```
Inner text: Hello, world! This is the original text.
```

Você pode se perguntar, *e se o elemento contiver tags aninhadas?* `text_content()` ainda funciona — ele concatena todos os nós de texto descendentes, fornecendo uma string limpa que você pode registrar, armazenar ou alimentar a outro algoritmo.

## Etapa 5: Como definir atributo HTML

Alterar ou adicionar atributos é igualmente simples. O método `set` permite atribuir qualquer nome de atributo que desejar.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Saída:

```
New attribute value: true
```

Essa linha demonstra **como definir atributo HTML** em tempo real. Você pode substituir `"data-modified"` por `"class"`, `"title"` ou qualquer outro atributo suportado pelo elemento.

## Etapa 6: Alterar cor de fundo HTML

Agora a mudança visual. Para mudar a cor de fundo, inserimos um atributo `style` que sobrescreve o padrão.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

Depois de executar o script, a `div` em `sample.html` ficará assim ao ser aberta em um navegador:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

Essa é a técnica de **alterar cor de fundo html** que você pode reutilizar em qualquer elemento — basta trocar o código da cor.

## Etapa 7: Manipular HTML com Python – Juntando tudo

A seguir está o script completo e executável que combina todas as etapas. Salve‑o como `modify_html.py` e execute‑o a partir do mesmo diretório da sua pasta `YOUR_DIRECTORY`.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### O que o script faz, linha por linha

1. **Imports** `lxml.html` para parsing e `pathlib` para caminhos independentes de SO.  
2. **Loads** `sample.html` e aborta com um erro claro se o arquivo estiver ausente.  
3. **Retrieves** o elemento usando **obter elemento por id**.  
4. **Prints** o texto do elemento — mostrando **como ler texto HTML**.  
5. **Adds** um atributo customizado, ilustrando **como definir atributo HTML**.  
6. **Changes** a cor de fundo, atendendo ao requisito de **alterar cor de fundo html**.  
7. **Writes** o markup atualizado para `sample_modified.html`, para que você possa abri‑lo no navegador e ver as mudanças.

Executar o script gera uma saída no console semelhante a:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Abra `sample_modified.html` e você notará o fundo cinza atrás do texto — prova de que **manipular HTML com python** realmente funciona.

## Armadilhas comuns & como evitá‑las

- **ID ausente** – Se o elemento alvo não existir, `get_element_by_id` retorna `None`. Sempre verifique `None` antes de acessar propriedades; caso contrário, você encontrará um `AttributeError`.  
- **Problemas de codificação** – Ao ler páginas não‑ASCII, passe `encoding='utf-8'` para `html.parse` ou garanta que seu arquivo esteja salvo em UTF‑8.  
- **Sobrescrever estilos existentes** – Definir o atributo `style` substitui quaisquer estilos inline anteriores. Se precisar preservar regras existentes, leia o valor atual de `style` primeiro, anexe sua nova regra e então grave de volta.  
- **Permissões de arquivo** – Escrever de volta na mesma pasta pode falhar em sistemas somente‑leitura. Escolha um caminho de saída gravável, como fizemos com `sample_modified.html`.

## Expandindo o exemplo

Agora que você dominou o básico, considere os próximos passos:

- **Iterar sobre múltiplos IDs** – Use uma lista de IDs e itere com um `for` loop para processar em lote seções de uma página.  
- **Substituir conteúdo de texto** – Chame `elem.text = "New text"` para alterar a string visível.  
- **Adicionar elementos filhos** – Use `

## O que você deve aprender a seguir?

- [Como editar HTML usando Aspose.HTML para Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [Como consultar HTML em Java – Tutorial completo](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [Como converter HTML para PDF em Java – Usando Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}