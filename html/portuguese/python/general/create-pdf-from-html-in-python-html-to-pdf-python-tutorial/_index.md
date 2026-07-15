---
category: general
date: 2026-07-15
description: Crie PDF a partir de HTML usando Python. Aprenda como converter HTML
  em PDF rapidamente com um script simples e etapas claras.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: pt
lastmod: 2026-07-15
og_description: Crie PDF a partir de HTML com Python. Este guia mostra como converter
  HTML em PDF, salvar HTML como PDF e lidar com recursos de forma eficiente.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Criar PDF a partir de HTML em Python – Tutorial Prático
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: Criar PDF a partir de HTML em Python – Tutorial de HTML para PDF em Python
url: /pt/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF a partir de HTML em Python – Tutorial Completo

Já precisou **criar PDF a partir de HTML** mas não tinha certeza de qual biblioteca Python escolher? Você não está sozinho—muitos desenvolvedores se deparam com esse obstáculo ao tentar transformar um relatório web, fatura ou página de marketing em um PDF imprimível.  

A boa notícia é que, com apenas algumas linhas de código, você pode **converter HTML em PDF** de forma confiável, e o script funciona no Windows, macOS e Linux. Neste guia, percorreremos um exemplo completo e executável, explicaremos por que cada etapa é importante e mostraremos como **salvar HTML como PDF** sem deixar pontas soltas.

---

## O que você aprenderá

- Instalar o pacote Python correto para conversão de HTML‑para‑PDF.  
- Carregar um arquivo HTML com opções personalizadas de tratamento de recursos (para evitar importações infinitas de CSS).  
- Gerar um arquivo PDF limpo no disco.  
- Lidar com casos de borda comuns, como imagens externas, caminhos relativos e documentos grandes.  

Ao final deste **tutorial de HTML para PDF**, você terá uma função reutilizável que pode inserir em qualquer projeto.

---

## Pré-requisitos

- Python 3.9+ (o código funciona também com 3.8, mas 3.9+ oferece os recursos mais recentes do `pathlib`).  
- Familiaridade básica com a linha de comando e ambientes virtuais.  
- Um arquivo HTML que você deseja transformar em PDF—qualquer página estática serve.

> **Dica profissional:** Se você estiver usando um ambiente virtual, ative-o antes de instalar a biblioteca; isso mantém seu Python global organizado.

---

## Etapa 1 – Instalar WeasyPrint (o motor por trás da conversão)

WeasyPrint é uma biblioteca pura‑Python que renderiza HTML e CSS em PDF. Ela lida com a maioria dos recursos web modernos e oferece controle granular sobre o carregamento de recursos.

```bash
pip install weasyprint
```

Executar o comando acima traz `cairocffi`, `tinycss2` e algumas outras dependências. Se você encontrar um erro relacionado ao `cairo` no Windows, obtenha as wheels pré‑compiladas no [site do WeasyPrint](https://weasyprint.org/docs/install/).

---

## Etapa 2 – Preparar um pequeno auxiliar para tratamento de recursos

Ao carregar um documento HTML que referencia folhas de estilo ou imagens externas, a biblioteca seguirá esses links. Em alguns casos isso leva a aninhamentos profundos ou até loops infinitos (pense em um arquivo CSS que `@import` a si mesmo). Para manter as coisas organizadas, limitamos a profundidade do tratamento de recursos.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

A classe acima não é exigida pelo WeasyPrint, mas espelha o padrão que você viu no trecho original e fornece um ponto de extensão para interromper importações descontroladas. Você a verá em uso na próxima etapa.

---

## Etapa 3 – Carregar o documento HTML usando as opções personalizadas

Agora realmente lemos o arquivo HTML. A classe `HTML` aceita um argumento `base_url`, que definimos como o diretório que contém o arquivo fonte—isso faz com que links relativos funcionem sem um servidor web.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Por que isso importa:** Se seu HTML inclui uma cascata de arquivos CSS, cada `@import` acionará outro carregamento. A proteção de profundidade impede que o script saia de controle.

---

## Etapa 4 – Salvar o documento processado como PDF

Com o objeto `HTML` em mãos, gerar um PDF é uma única linha de código. Também passamos um trecho CSS simples que força um tamanho de página limpo (A4) e adiciona uma pequena margem—sinta-se à vontade para ajustar.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Chamar `write_pdf` grava o PDF no disco, de modo que você obtém um arquivo pronto‑para‑compartilhar.

---

## Etapa 5 – Juntar Tudo

Abaixo está um script compacto que você pode copiar‑colar em `convert.py`. Substitua os caminhos de placeholder pelos seus diretórios reais.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Saída esperada** – após executar `python convert.py` você deverá ver:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Abra o arquivo gerado com qualquer visualizador de PDF; você verá o layout original da página, o estilo CSS e as imagens (desde que estejam acessíveis a partir do arquivo HTML).  

Se notar imagens ausentes, verifique novamente se os atributos `src` são URLs absolutas ou caminhos relativos que existam em `YOUR_DIRECTORY`.

---

## Perguntas Frequentes & Tratamento de Casos Limítrofes

| Pergunta | Resposta |
|----------|----------|
| *E se meu HTML referenciar fontes externas?* | WeasyPrint baixará os arquivos de fonte automaticamente, mas você pode querer colocar em lista branca os domínios para evitar tempos de download longos. |
| *Posso converter uma string de HTML em vez de um arquivo?* | Sim—use `HTML(string=my_html_string)` e ignore o `base_url` ou defina‑o para uma pasta temporária. |
| *Como controlo os metadados do PDF (título, autor)?* | Passe um dicionário `metadata` para `write_pdf`, por exemplo, `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *Recebo um erro “cairo‑cffi” no Linux.* | Instale o pacote do sistema `libcairo2-dev` (`apt-get install libcairo2-dev` no Debian/Ubuntu) antes de instalar o WeasyPrint via pip. |

---

## Conclusão

Acabamos de **criar PDF a partir de HTML** usando um fluxo de trabalho Python limpo, cobrimos a mecânica de **converter HTML em PDF** e mostramos como **salvar HTML como PDF** com tratamento robusto de recursos. O script é pequeno o suficiente para ser inserido em pipelines de CI, mas flexível o bastante para ser expandido com cabeçalhos, rodapés ou marcas d'água personalizados.

Próximos passos que você pode explorar:

- Use a biblioteca **html to pdf python** `pdfkit` para uma abordagem baseada em wkhtmltopdf (boa para CSS legado).  
- Adicione uma interface CLI com `argparse` para que o script aceite argumentos de entrada/saída.  
- Gere PDFs sob demanda dentro de um endpoint Flask ou FastAPI para relatórios instantâneos.  

Sinta-se à vontade para experimentar, quebrar coisas e depois voltar a este guia para uma rápida revisão. Se encontrar problemas, a documentação do WeasyPrint e os fóruns da comunidade são excelentes recursos.

Feliz codificação, e aproveite transformar essas páginas web em PDFs elegantes!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá-lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Converter HTML para PDF com Aspose.HTML – Guia Completo de Manipulação](/html/english/)
- [Converter HTML para PDF em .NET com Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Criar PDF a partir de HTML – Guia passo a passo em C#](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}