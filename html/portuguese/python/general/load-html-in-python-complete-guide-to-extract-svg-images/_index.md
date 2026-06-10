---
category: general
date: 2026-06-10
description: Carregue HTML em Python para extrair imagens SVG das suas páginas — código
  passo a passo, dicas e tratamento de casos extremos.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: pt
og_description: Carregue HTML em Python e extraia imagens SVG com um exemplo claro
  e executável. Aprenda a pesquisar elementos SVG em HTML e a lidar com casos de borda.
og_title: Carregar HTML em Python – Extrair Imagens SVG de Forma Eficiente
schemas:
- author: Aspose
  dateModified: '2026-06-10'
  description: Load HTML in Python to extract SVG images from your pages—step-by-step
    code, tips, and edge‑case handling.
  headline: Load HTML in Python – Complete Guide to Extract SVG Images
  type: TechArticle
tags:
- python
- html-parsing
- svg
title: Carregar HTML em Python – Guia Completo para Extrair Imagens SVG
url: /pt/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Carregar HTML em Python – Guia Completo para Extrair Imagens SVG

Já precisou **carregar HTML em Python** apenas para extrair todos os gráficos SVG de uma página? Você não está sozinho. Seja construindo um web‑scraper, gerando um relatório de ativos, ou apenas curioso sobre os ícones que um site usa, saber como **extrair imagens SVG** economiza muito trabalho manual.

Neste tutorial vamos percorrer uma solução prática, de ponta a ponta, que **carrega HTML em Python**, depois **procura elementos HTML SVG**, **encontra SVG embutido**, e ainda captura arquivos SVG externos referenciados por tags `<img>`. Ao final, você terá um script reutilizável, algumas dicas para os pontos mais complicados e uma visão clara de como é a saída.

## O que Você Vai Levar

* Um script Python totalmente executável que analisa um arquivo HTML local (ou uma página obtida) e lista todos os SVGs que conseguir encontrar.  
* Compreensão da diferença entre **SVG embutido** (`<svg>…</svg>`) e **SVG externo** (`<img src="… .svg">`).  
* Estratégias para lidar com marcação malformada, arquivos ausentes e peculiaridades de namespaces.  
* Ideias para expandir o código — salvar os SVGs, convertê‑los para PNG ou inseri‑los em um banco de dados.

### Pré‑requisitos

* Python 3.8+ instalado.  
* Familiaridade básica com as bibliotecas `requests` e `BeautifulSoup` do Python (as importaremos, sem necessidade de aprofundamento).  
* Um arquivo HTML local ou uma URL que você deseja analisar.  

Agora, vamos mergulhar.

## Carregar HTML em Python – Configurando o Parser

O primeiro passo é **carregar HTML em Python**. Você pode ler um arquivo do disco ou buscar uma página remota. Abaixo está um helper minimalista, porém robusto, que faz ambos:

```python
import os
import requests
from bs4 import BeautifulSoup

def load_html(source: str) -> BeautifulSoup:
    """
    Load HTML content from a file path or a URL and return a BeautifulSoup object.
    """
    if os.path.isfile(source):
        # Load from local file
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        # Assume it's a URL and fetch it
        response = requests.get(source)
        response.raise_for_status()
        html = response.text

    # Use the html.parser for speed; switch to 'lxml' if you need extra robustness
    soup = BeautifulSoup(html, "html.parser")
    return soup
```

> **Por que isso importa:** Usar `BeautifulSoup` abstrai as peculiaridades da análise de strings brutas, e a função lida graciosamente tanto com arquivos locais quanto com URLs remotas. Ela também lança uma exceção se uma requisição de rede falhar — assim você saberá instantaneamente quando algo deu errado.

## Extrair Imagens SVG – Encontrando Elementos SVG Embutidos

Uma vez que o documento está carregado, a próxima etapa lógica é **encontrar tags SVG embutidas**. SVG embutido é inserido diretamente no markup HTML, o que significa que você pode obtê‑lo diretamente do DOM.

```python
def collect_inline_svg(soup: BeautifulSoup) -> list:
    """
    Return a list of all inline <svg> elements as strings.
    """
    inline_svgs = []
    for svg in soup.find_all("svg"):
        # Preserve the original markup; .decode() gives us a string representation
        inline_svgs.append(str(svg))
    return inline_svgs
```

*Dica de profissional:* Se a página usa namespaces SVG (`<svg xmlns="http://www.w3.org/2000/svg">`), `BeautifulSoup` ainda encontra a tag porque ignora namespaces por padrão. Isso é uma conveniência útil quando você está apenas **procurando SVG em HTML**.

## Procurar SVG em HTML – Lidando com Referências Externas `<img>`

Muitos sites não incorporam SVG diretamente; eles referenciam arquivos externos via `<img src="icon.svg">`. Para capturá‑los, precisamos iterar sobre cada tag `<img>`, verificar seu `src` e ver se termina com `.svg`.

```python
def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    """
    Return a list of file paths or URLs that point to external SVG images.
    If base_path is provided, it will be joined with relative URLs.
    """
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            # Resolve relative paths if a base directory or URL is given
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs
```

> **Alerta de caso extremo:** Algumas páginas usam strings de consulta (`icon.svg?v=2`) ou fragmentos (`icon.svg#layer`). A verificação `endswith(".svg")` ainda funciona porque analisamos apenas a parte final da string em minúsculas. Se precisar de validação mais rigorosa, considere usar `urllib.parse` para remover os parâmetros primeiro.

## Encontrar SVG Embutido – Relatando os Resultados

Agora que temos duas listas — uma para markup SVG embutido e outra para referências de arquivos externos — podemos combiná‑las e relatar a contagem total. Isso espelha o trecho original que você postou, mas adiciona um pouco mais de contexto.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Juntando Tudo – Script Completo

Abaixo está o programa completo, pronto‑para‑executar. Salve‑o como `extract_svg.py` e aponte‑o para um arquivo HTML local ou uma URL.

```python
#!/usr/bin/env python3
import os
import sys
import requests
from bs4 import BeautifulSoup

# -------------------------------------------------
# Helper functions (see definitions above)
# -------------------------------------------------
def load_html(source: str) -> BeautifulSoup:
    if os.path.isfile(source):
        with open(source, "r", encoding="utf-8") as f:
            html = f.read()
    else:
        response = requests.get(source)
        response.raise_for_status()
        html = response.text
    return BeautifulSoup(html, "html.parser")

def collect_inline_svg(soup: BeautifulSoup) -> list:
    return [str(svg) for svg in soup.find_all("svg")]

def collect_external_svg(soup: BeautifulSoup, base_path: str = "") -> list:
    external_svgs = []
    for img in soup.find_all("img"):
        src = img.get("src")
        if src and src.lower().endswith(".svg"):
            if base_path and not src.startswith(("http://", "https://")):
                src = os.path.join(base_path, src)
            external_svgs.append(src)
    return external_svgs

def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")

# -------------------------------------------------
# Main execution
# -------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_svg.py <path-or-url-to-html>")
        sys.exit(1)

    source = sys.argv[1]
    soup = load_html(source)

    # Determine base path for relative <img> sources (only relevant for local files)
    base_dir = os.path.dirname(os.path.abspath(source)) if os.path.isfile(source) else ""

    inline_svgs = collect_inline_svg(soup)
    external_svgs = collect_external_svg(soup, base_dir)

    report_svg_counts(inline_svgs, external_svgs)

    # Optional: write inline SVGs to separate files for inspection
    for idx, svg_markup in enumerate(inline_svgs, start=1):
        out_path = f"inline_svg_{idx}.svg"
        with open(out_path, "w", encoding="utf-8") as out_file:
            out_file.write(svg_markup)
        print(f"Saved inline SVG #{idx} to {out_path}")

    # Optional: download external SVGs (uncomment if needed)
    # for url in external_svgs:
    #     try:
    #         resp = requests.get(url)
    #         resp.raise_for_status()
    #         filename = os.path.basename(url.split("?")[0])
    #         with open(filename, "wb") as f:
    #             f.write(resp.content)
    #         print(f"Downloaded {url} → {filename}")
    #     except Exception as e:
    #         print(f"Failed to download {url}: {e}")
```

### Saída Esperada

Executar o script contra um `sample.html` de exemplo pode produzir:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Se você descomentar o bloco de download, o SVG externo

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}