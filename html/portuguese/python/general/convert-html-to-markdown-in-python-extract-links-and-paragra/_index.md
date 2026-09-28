---
category: general
date: 2026-09-26
description: Converta HTML para Markdown com Python, extraindo links do HTML e salvando
  HTML como Markdown. Aprenda como converter HTML passo a passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: pt
lastmod: 2026-09-26
og_description: Converta HTML para Markdown com Python, extraindo links do HTML e
  salvando HTML como Markdown. Siga este guia completo.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: Converter HTML para Markdown em Python – extrair links e parágrafos
schemas:
- author: GroupDocs
  dateModified: '2026-09-26'
  description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  headline: Convert HTML to Markdown in Python – extract links and paragraphs easily
  type: TechArticle
- description: Convert HTML to Markdown with Python, extracting links from HTML and
    saving HTML as Markdown. Learn how to convert HTML step‑by‑step.
  name: Convert HTML to Markdown in Python – extract links and paragraphs easily
  steps:
  - name: Expected output
    text: 'Running the script generates a file similar to the following (the exact
      content depends on the source HTML):'
  - name: 1. Extract only links
    text: '```python md_options.features = MarkdownFeatures.LINKS # No paragraphs
      ```'
  - name: 2. Extract only paragraphs
    text: '```python md_options.features = MarkdownFeatures.PARAGRAPHS # No links
      ```'
  type: HowTo
- questions:
  - answer: Yes. `HTMLDocument` accepts any well‑formed fragment; the converter treats
      the fragment as the document body.
    question: Does this work with HTML fragments (no `<html>` root tag)?
  - answer: 'Add `MarkdownFeatures.IMAGES` to the `features` flag: ```python md_options.features
      = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
      ```'
    question: Can I keep images as Markdown image syntax?
  - answer: 'Wrap `convert_html_to_markdown` in a loop that walks the directory with
      `os.listdir` or `pathlib.Path.rglob("*.html")`. --- ## Conclusion You now know
      how to **convert HTML to Markdown** in Python while selectively **extracting
      links from HTML** and **extracting paragraphs from HTML**. The script de'
    question: How do I convert many files in a directory?
  type: FAQPage
tags:
- html
- markdown
- python
- data‑extraction
title: Converter HTML para Markdown em Python – extraia links e parágrafos facilmente
url: /pt/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter HTML para Markdown em Python – extraia links e parágrafos facilmente

Se você precisa **converter HTML para Markdown** mantendo apenas as partes úteis, este guia mostra como fazer isso com apenas algumas linhas de Python. Seja você quem está raspando posts de blog, arquivando documentação ou limpando corpos de e‑mail, aprenderá um método confiável para extrair links de HTML e salvar HTML como Markdown.

O tutorial cobre tudo, desde a instalação do pacote necessário até o tratamento de casos extremos, como tags `<a>` vazias ou parágrafos aninhados. Ao final, você terá um script pronto‑para‑executar que **converte HTML para Markdown**, extrai links de HTML e ainda extrai parágrafos de HTML quando precisar.

---

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* Python 3.8 ou superior instalado  
* Acesso ao pacote Python `groupdocs-conversion` (a biblioteca que fornece `HTMLDocument`, `MarkdownSaveOptions` e `Converter`)  
* Um arquivo HTML local que você deseja processar (por exemplo, `article.html`)

Você pode instalar a biblioteca com pip:

```bash
pip install groupdocs-conversion
```

> **Dica profissional:** Use um ambiente virtual (`python -m venv venv`) para manter as dependências isoladas.

---

## Etapa 1: Carregar o documento HTML de origem

A primeira operação é criar um objeto `HTMLDocument` que aponta para o seu arquivo de origem. Esse objeto abstrai o HTML bruto e fornece ao conversor um ponto de entrada limpo.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Por que isso importa:* Carregar o documento dessa forma permite que a biblioteca analise o DOM uma única vez, de modo que operações subsequentes (como extrair links ou parágrafos) sejam rápidas e eficientes em memória.

---

## Etapa 2: Criar opções de salvamento em Markdown e selecionar os recursos que você precisa

`MarkdownSaveOptions` permite decidir quais elementos HTML sobrevivem à conversão. O sinalizador `features` usa um OR bit a bit para combinar opções.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Por que isso importa:* Ao especificar `LINKS` e `PARAGRAPHS` você **extrai links de HTML** e **extrai parágrafos de HTML** enquanto descarta todo o resto (estilos, scripts, imagens). Se mais tarde precisar apenas de links, substitua `MarkdownFeatures.PARAGRAPHS` por `0` (ou omita‑o).

---

## Etapa 3: Converter o HTML para Markdown usando as opções configuradas

Agora chame o método estático `convert_html`, passando o documento de origem, o caminho de destino e as opções que você acabou de montar.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Por que isso importa:* A conversão ocorre em uma única passagem, aplicando o filtro de recursos que você definiu. O arquivo resultante (`article_links.md`) contém apenas links e parágrafos formatados em Markdown, que é exatamente o que você precisa quando deseja **salvar HTML como Markdown** para processamento posterior.

---

## Script completo – tudo junto

Abaixo está um script completo e executável que você pode copiar‑colar em um arquivo chamado `html_to_md.py`. Ajuste os caminhos para corresponder ao seu ambiente.

```python
# html_to_md.py
# -------------------------------------------------
# Convert HTML to Markdown, keeping only links and paragraphs.
# -------------------------------------------------

from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

def convert_html_to_markdown(source_path: str, target_path: str) -> None:
    """
    Convert an HTML file to Markdown, extracting only links and paragraphs.

    Args:
        source_path: Path to the source HTML file.
        target_path: Path where the Markdown file will be saved.
    """
    # Load the HTML document
    html_doc = HTMLDocument(source_path)

    # Configure conversion to keep links and paragraphs
    md_options = MarkdownSaveOptions()
    md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS

    # Run the conversion
    Converter.convert_html(html_doc, target_path, md_options)
    print(f"✅ Conversion complete – Markdown saved to: {target_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    src = "YOUR_DIRECTORY/article.html"
    dst = "YOUR_DIRECTORY/article_links.md"
    convert_html_to_markdown(src, dst)
```

### Saída esperada

Executar o script gera um arquivo semelhante ao seguinte (o conteúdo exato depende do HTML de origem):

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Apenas o texto dos links e o texto dos parágrafos aparecem; todos os demais elementos HTML são removidos.

---

## Extrair apenas links ou apenas parágrafos (variações avançadas)

Às vezes você precisa **converter HTML** para um arquivo Markdown que contenha apenas um tipo de elemento.

### 1. Extrair apenas links

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Extrair apenas parágrafos

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Ambas as variações reutilizam a mesma chamada `convert_html`, portanto você não precisa escrever lógica de conversão separada.

---

## Tratamento de casos extremos

| Situação                                 | Correção recomendada |
|------------------------------------------|----------------------|
| O arquivo HTML contém tags `<a>` vazias  | O conversor ignora automaticamente links vazios. Se aparecerem entradas `[]()` indesejadas, defina `md_options.removeEmptyLinks = True`. |
| Parágrafos aninhados (`<p>` dentro de `<div>`) | A biblioteca achata parágrafos aninhados, preservando a ordem do texto. Nenhum código extra é necessário. |
| Caracteres não‑ASCII nos títulos dos links | Garanta que seu arquivo Python esteja salvo com codificação UTF‑8 e abra o arquivo de saída com `encoding="utf-8"` caso o leia depois. |
| Arquivos HTML muito grandes (≥ 50 MB)    | Processe o arquivo em blocos usando `HTMLDocument(stream=io.BytesIO(...))` para evitar carregar todo o conteúdo na memória. |

---

## Perguntas frequentes

**P: Isso funciona com fragmentos de HTML (sem a tag `<html>` raiz)?**  
R: Sim. `HTMLDocument` aceita qualquer fragmento bem‑formado; o conversor trata o fragmento como o corpo do documento.

**P: Posso manter imagens usando a sintaxe de imagem do Markdown?**  
R: Adicione `MarkdownFeatures.IMAGES` ao sinalizador `features`:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**P: Como converto muitos arquivos em um diretório?**  
R: Envolva `convert_html_to_markdown` em um loop que percorra o diretório com `os.listdir` ou `pathlib.Path.rglob("*.html")`.

---

## Conclusão

Agora você sabe como **converter HTML para Markdown** em Python enquanto extrai seletivamente **links de HTML** e **parágrafos de HTML**. O script demonstra a abordagem padrão — carregar o documento, configurar `MarkdownSaveOptions` e executar `Converter.convert_html`. Com alguns ajustes, você também pode **salvar HTML como Markdown** contendo apenas links, apenas parágrafos ou uma representação fiel completa.

Próximos passos sugeridos:

* Adicionar `MarkdownFeatures.HEADINGS` para preservar títulos de seção.  
* Usar o Markdown resultante como entrada para geradores de sites estáticos como MkDocs ou Hugo.  
* Automatizar conversões em massa para um repositório inteiro de documentação.

Boa conversão!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Converter HTML para Markdown em .NET com Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Converter HTML para Markdown em Aspose.HTML para Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Como definir deslocamento ao converter HTML para Markdown em Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}