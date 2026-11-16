---
category: general
date: 2026-07-31
description: Aprenda a criar um documento SVG, adicionar um círculo e salvar o arquivo
  SVG rapidamente. Exporte o gráfico como SVG com algumas linhas de código Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: pt
lastmod: 2026-07-31
og_description: Crie um documento SVG, adicione um círculo e salve o arquivo SVG em
  segundos. Este guia mostra como exportar o gráfico como SVG com código claro e executável.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Criar documento SVG – Adicionar um círculo e salvar como SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: Criar documento SVG – Adicionar um círculo e salvar como SVG
url: /pt/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Documento SVG – Adicionar um Círculo e Salvar como SVG

Já precisou **create SVG document** a partir de código mas não sabia por onde começar? Você não está sozinho; muitos desenvolvedores encontram essa barreira quando começam a brincar com gráficos vetoriais. Neste tutorial vamos percorrer um pequeno exemplo autônomo que mostra como **add circle to SVG**, então **save SVG file** para que você possa **export graphic as SVG** para uso na web ou em ferramentas de design.

Manteremos as coisas leves: apenas algumas linhas de Python, uma biblioteca auxiliar SVG popular e um pouco de explicação. Ao final, você terá um `circle.svg` pronto para uso na sua pasta, e entenderá por que cada passo importa — sem atalhos vagos de “see docs”.

## O que você precisará

- Python 3.8+ (qualquer versão recente funciona)
- O pacote `svgwrite` – instale‑o com `pip install svgwrite`
- Um editor de texto ou IDE (VS Code, PyCharm, ou até o Notepad serve)
- Permissão de escrita no diretório onde você deseja salvar o arquivo

É isso. Sem dependências pesadas, sem serviços externos.

## Etapa 1: Configurar o Documento SVG

Criar um documento SVG é tão simples quanto instanciar um objeto `Drawing` de `svgwrite`. Pense neste objeto como a tela em branco onde cada forma vive.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Por que isso importa:** A classe `Drawing` cuida de todo o boilerplate XML para você — namespaces, cabeçalhos e o elemento raiz `<svg>`. Ao especificar um nome de arquivo antecipadamente já sabemos onde o arquivo será salvo, o que torna a etapa posterior de **save svg file** trivial.

### Dica profissional
Se você planeja gerar muitos arquivos em um loop, dê a cada `Drawing` um nome único ou use `io.BytesIO` para manter tudo na memória até estar pronto para gravar.

## Etapa 2: Adicionar um Círculo ao SVG

Agora que o documento existe, vamos **add circle to SVG**. O método `add()` aceita qualquer objeto de forma; um `Circle` é perfeito para um ponto vermelho simples no centro.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Por que usamos as variáveis `center` e `radius`:** Codificar números diretamente torna o código mais difícil de ler e manter. Ao nomear os valores, esclarecemos a intenção — este círculo está exatamente no meio de uma tela de 200 × 200 e é grande o suficiente para ser notado.

### Caso de borda – Fundo transparente
Se você precisar de um fundo transparente (padrão para SVG), pode pular a definição de `fill` na raiz. Para um fundo branco, adicione:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Coloque isso antes de adicionar o círculo para que o retângulo fique por baixo.

## Etapa 3: Salvar o Arquivo SVG

Com a forma no lugar, o ato final é **save SVG file**. O método `save()` grava o XML no disco, e como já fornecemos um nome de arquivo ao `Drawing`, uma única chamada resolve tudo.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **O que acontece nos bastidores?** `svgwrite` serializa a árvore de elementos para uma string, adiciona a declaração XML e a grava usando codificação UTF‑8. Se o diretório de destino não existir, o Python lançará um `FileNotFoundError`; certifique‑se de que o caminho seja válido ou crie‑o com `os.makedirs()`.

### Bônus: Exportar gráfico como SVG programaticamente
Se você precisar do conteúdo SVG como string — por exemplo, para incorporá‑lo em um e‑mail HTML — pode chamar `dwg.tostring()` ao invés de `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Exemplo Completo Funcional

Juntando tudo, aqui está um script completo, pronto‑para‑executar:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Saída esperada:** Depois de executar o script, você verá um arquivo `circle.svg` na mesma pasta. Abrindo‑o em um navegador ou em qualquer editor vetorial, aparece um círculo vermelho centralizado em um quadrado branco — exatamente o que programamos.

## Perguntas Frequentes & Armadilhas

- **E se eu quiser uma forma diferente?** Troque `dwg.circle` por `dwg.rect`, `dwg.ellipse` ou até uma string `<path>` personalizada. A API é consistente entre as formas.
- **Posso incorporar o SVG diretamente no HTML?** Absolutamente. O arquivo que você acabou de criar pode ser referenciado com `<img src="circle.svg" alt="Red circle">` ou inserido inline com tags `<svg>`.
- **Por que não escrever XML puro?** Você poderia, mas bibliotecas como `svgwrite` lidam com peculiaridades de namespaces e tornam o código muito mais fácil de manter — especialmente quando você começa a adicionar gradientes ou animações.

## Conclusão

Agora você sabe como **create SVG document**, **add circle to SVG**, e **save SVG file** para que possa **export graphic as SVG** com apenas algumas linhas de Python. O padrão escala: substitua o círculo por qualquer forma vetorial, faça loop sobre dados para gerar gráficos, ou processe em lote ativos para um sistema de design.

Próximos passos? Tente adicionar rótulos de texto, experimentar gradientes ou gerar uma galeria inteira de ícones em um único script. Se você estiver curioso sobre recursos mais avançados, confira a documentação do `svgwrite` sobre grupos (`<g>`), transformações e suporte a animações.

Feliz codificação, e que seus vetores permaneçam sempre nítidos!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Salvar Documento SVG no Aspose.HTML para Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Criar e Gerenciar Documentos SVG no Aspose.HTML para Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Converter SVG para Imagem com Aspose.HTML para Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}