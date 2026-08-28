---
category: general
date: 2026-07-02
description: Crie documentos SVG rapidamente com Python. Aprenda a salvar arquivos
  SVG, gerar uma imagem SVG básica e exportar SVG a partir do código em apenas algumas
  linhas.
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: pt
og_description: Crie documentos SVG facilmente. Este guia mostra como gerar SVG, salvar
  arquivos SVG e exportar SVG a partir do código com um exemplo limpo em Python.
og_title: Criar Documento SVG – Tutorial Rápido de Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: Criar Documento SVG – Guia Passo a Passo para Iniciantes
url: /pt/python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Documento SVG – Guia Passo a Passo para Iniciantes

Já se perguntou como **criar documento SVG** sem abrir um editor gráfico? Você não está sozinho. Seja porque precisa de um ícone pequeno para uma página web ou de um gráfico dinâmico gerado na hora, poder **criar documento SVG** programaticamente economiza tempo e mantém tudo sob controle de versão.

Neste tutorial vamos percorrer um exemplo completo e executável que mostra exatamente como **criar documento SVG**, **salvar arquivo SVG**, e ainda responder àquela pergunta persistente “**como gerar SVG**” que surge quando você automatiza gráficos. Ao final você terá um quadrado vermelho salvo em disco e saberá como **exportar SVG a partir do código** para qualquer projeto futuro.

## O que Você Precisa

Antes de mergulharmos, certifique‑se de que tem:

* Python 3.9 ou mais recente (a biblioteca padrão faz todo o trabalho pesado)
* Um editor de texto ou IDE de sua preferência — VS Code, PyCharm ou até o Bloco de Notas serve
* Permissão de escrita em uma pasta onde você vai **salvar arquivo SVG** (usaremos um diretório `output/`)

Nenhum pacote externo é necessário, então a configuração leva literalmente alguns minutos.

## Etapa 1: Configurar as Funções Auxiliares de SVG (Criar o Documento)

Primeiro de tudo: precisamos de um pequeno helper que construa a estrutura XML por trás de um SVG. Pense nisso como a tela onde vamos **criar imagem SVG básica** mais tarde.

```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**Por que esta etapa importa:** A classe `SVGDocument` abstrai a manipulação de XML de baixo nível. Ao encapsulá‑la em uma classe, mantemos o restante do código limpo, o que é uma boa prática quando você **exporta SVG a partir do código** em aplicações maiores.

## Etapa 2: Adicionar um Retângulo – O Núcleo de um Exemplo de **Criar Imagem SVG Básica**

Agora que temos um objeto de documento, vamos acrescentar um quadrado vermelho. Este é o coração da parte **criar imagem SVG básica** do tutorial.

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**Explicação:**  
* As coordenadas `x` e `y` do retângulo dão a ele uma margem de 10 pixels para que não fique colado na borda.  
* Usar um dicionário para atributos torna o código legível e reflete como você **salva arquivo SVG** atributos em qualquer formato baseado em XML.  
* Se precisar **gerar SVG** de formas diferentes de retângulos, basta mudar a tag para `"circle"` ou `"path"` e ajustar o dicionário de atributos conforme necessário.

## Etapa 3: Persistir o SVG – Finalmente **Salvar Arquivo SVG** no Disco

Construímos o documento na memória; agora vamos gravá‑lo. Este é o momento em que o abstrato **criar documento SVG** se transforma em um arquivo tangível que você pode abrir em um navegador.

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**O que você verá:** Abrir `output/square.svg` no Chrome, Firefox ou qualquer visualizador que suporte SVG exibirá um simples quadrado vermelho com uma fina borda branca (o fundo da tela SVG). Essa é a prova de que conseguimos **exportar SVG a partir do código** com sucesso.

## Script Completo – Solução de Um Único Arquivo

Abaixo está o script inteiro, pronto para ser copiado e colado em `create_svg.py`. Executar `python create_svg.py` gerará o arquivo descrito acima.

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### Saída Esperada

Executar o script imprime:

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

E o `square.svg` gerado se parece com isto (visualização simplificada):

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

Abrir o arquivo renderiza um quadrado vermelho nítido — exatamente o que nos propusemos a **criar imagem SVG básica**.

## Expandindo o Exemplo – Perguntas Frequentes Respondidas

### Como posso adicionar texto ou outras formas?

Basta chamar `svg.create_element("text", {...})` ou `svg.create_element("circle", {...})` e adicioná‑los assim como o retângulo. A mesma lógica de **como gerar SVG** se aplica.

### E se eu precisar **exportar SVG a partir do código** com fundo transparente?

Remova qualquer atributo `fill` do elemento raiz `<svg>` ou defina `fill="none"` nas formas que devem ser transparentes. O XML permanece válido; os navegadores renderizarão a transparência automaticamente.

### Posso **salvar arquivo SVG** com formatação “pretty‑printed”?

`ElementTree` grava XML compacto por padrão. Para uma versão legível, você pode usar `xml.dom.minidom` para reformatar:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

Substitua `svg.save(output_path)` por `pretty_save(svg, output_path)`.

### E quanto ao desempenho para SVGs grandes?

Ao gerar milhares de elementos, considere construir uma lista de objetos `ET.Element` primeiro e depois estender a raiz de uma só vez. Isso reduz o número de mutações na árvore e acelera a operação de **salvar arquivo SVG**.

## Dicas Profissionais & Armadilhas

* **Dica profissional:** Sempre use caminhos absolutos (ou `pathlib.Path`) ao **salvar arquivo SVG**; caminhos relativos podem quebrar quando seu script for executado a partir de outro diretório de trabalho.  
* **Cuidado com:** Esquecer de registrar o namespace SVG. Sem `ET.register_namespace("", SVGDocument.SVG_NS)`, a saída conterá um prefixo redundante `ns0` que alguns navegadores interpretam incorretamente.  
* **Erro comum:** Misturar tipos inteiro e string nos valores dos atributos. XML espera strings, então convertemos tudo com `str()` — a classe helper faz isso por você, mas se você contornar, pode receber um `TypeError`.  

## Conclusão

Acabamos de percorrer um exemplo completo, de ponta a ponta, que mostra como **criar documento SVG**, **salvar arquivo SVG**, e responder

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}