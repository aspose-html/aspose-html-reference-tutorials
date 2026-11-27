---
category: general
date: 2026-11-27
description: Converta HTML para Markdown usando Python e gere Markdown a partir de
  HTML com suporte ao Markdown no estilo GitLab. Aprenda como definir o formatador
  de Markdown e exportar HTML como Markdown.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- export html as markdown
- generate markdown from html
- set markdown formatter
language: pt
lastmod: 2026-11-27
og_description: Converta HTML para Markdown com Python e Markdown no estilo do GitLab.
  Este guia mostra como configurar o formatador de Markdown e exportar HTML como Markdown
  em poucos passos.
og_image_alt: Diagram illustrating how to convert html to markdown using a Python
  script
og_title: Converter HTML para Markdown com Markdown no estilo GitLab em Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Convert html to markdown using Python and generate markdown from html
    with GitLab‑flavored markdown support. Learn how to set markdown formatter and
    export html as markdown.
  headline: Convert html to markdown with GitLab‑flavored Markdown using Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
title: Converter HTML para Markdown com Markdown ao estilo GitLab usando Python
url: /pt/python/general/convert-html-to-markdown-with-gitlab-flavored-markdown-using/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converter html para markdown com GitLab‑flavored Markdown usando Python

Se você precisa **converter html para markdown**, este guia mostra uma solução completa e pronta‑para‑usar. Você verá como **exportar html como markdown**, escolher o formato **GitLab‑flavored markdown**, e **set markdown formatter** opções para que a saída corresponda às regras de renderização do seu repositório.

Nas seções a seguir, percorreremos cada linha de código, explicaremos por que cada configuração importa e abordaremos variações comuns, como manter apenas links e parágrafos ou mudar para o sabor padrão. Ao final, você será capaz de **generate markdown from html** em uma única chamada de função.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* Python 3.8+ instalado  
* O `aspose.words` (ou uma biblioteca similar que fornece `HTMLDocument`, `MarkdownSaveOptions` e `Converter`) instalado via `pip install aspose-words`  
* Um pequeno arquivo HTML que você deseja converter, por exemplo, `sample.html` em um diretório conhecido  

Nenhuma ferramenta adicional é necessária; o tutorial usa apenas o mecanismo de conversão interno da biblioteca.

## Etapa 1: Carregar o documento HTML que você deseja converter

O pipeline de conversão começa carregando o arquivo de origem em um objeto `HTMLDocument`. Esse objeto analisa a marcação HTML e a prepara para a transformação.

```python
from aspose.words import HTMLDocument, MarkdownSaveOptions, MarkdownFeatures, Converter

# Load the HTML file you wish to convert
html_doc = HTMLDocument("YOUR_DIRECTORY/sample.html")
```

*Por que esta etapa importa*: `HTMLDocument` normaliza a estrutura HTML, resolve URLs relativas e cria um DOM que o motor de markdown pode percorrer. Pular esta etapa forçaria o conversor a ler texto bruto, resultando em tags ausentes ou links quebrados.

## Etapa 2: Criar opções de salvamento Markdown e configurar o sabor e os recursos desejados

Aqui definimos as opções **set markdown formatter**. A propriedade `format` seleciona o sabor do markdown—`"GIT"` produz **GitLab‑flavored markdown**, enquanto `"DEFAULT"` gera o CommonMark padrão.

```python
# Create a MarkdownSaveOptions instance
md_options = MarkdownSaveOptions()

# Set the formatter to GitLab‑flavored markdown
md_options.formatter = "GIT"  # alternatives: "DEFAULT", "MARKDOWN"

# Choose which markdown features to keep.
# In this example we keep only links and paragraphs.
md_options.features = (
    MarkdownFeatures.LINK |
    MarkdownFeatures.PARAGRAPH
)
```

*Por que isso importa*: Diferentes plataformas (GitHub, GitLab, Bitbucket) interpretam markdown de forma ligeiramente diferente. Ao **setting markdown formatter** para `"GIT"` você garante que tabelas, listas de tarefas e outras sintaxes específicas do GitLab sejam renderizadas corretamente. O sinalizador `features` permite **export html as markdown** enquanto remove elementos indesejados, mantendo a saída limpa para documentação ou arquivos read‑me.

## Etapa 3: Converter o documento HTML para Markdown usando as opções configuradas

Com a fonte carregada e as opções preparadas, invoque o método estático `convert`. Esta única chamada realiza o trabalho pesado.

```python
# Perform the conversion and write the result to a .md file
Converter.convert(html_doc, md_options, "YOUR_DIRECTORY/sample.md")
```

*Por que isso importa*: A classe `Converter` abstrai todo o pipeline de transformação. Ela lê o DOM de `HTMLDocument`, aplica o formatador que você **set markdown formatter**, respeita os `features` selecionados e grava o arquivo markdown final. O resultado é um arquivo `.md` limpo e compatível com GitLab, pronto para controle de versão.

## Saída esperada

Assumindo que `sample.html` contém um parágrafo simples com um link:

```html
<p>Check out the <a href="https://example.com">example site</a> for more info.</p>
```

O `sample.md` gerado ficará assim:

```markdown
Check out the [example site](https://example.com) for more info.
```

Como limitamos os recursos a `LINK` e `PARAGRAPH`, quaisquer imagens, tabelas ou scripts do HTML original são omitidos. Se precisar de uma conversão mais rica, ajuste `md_options.features` conforme necessário (por exemplo, adicione `MarkdownFeatures.IMAGE`).

## Etapa 4: Verificar a conversão e lidar com casos de borda

É uma boa prática ler o arquivo de saída novamente no Python e verificar se a conversão foi bem‑sucedida, especialmente ao processar muitos arquivos em lote.

```python
# Verify the markdown file exists and print its first lines
import pathlib

output_path = pathlib.Path("YOUR_DIRECTORY/sample.md")
if output_path.is_file():
    print("Conversion succeeded. First 3 lines:")
    print("\n".join(output_path.read_text().splitlines()[:3]))
else:
    raise FileNotFoundError("The markdown file was not created.")
```

**Common edge cases**

| Situação | Como resolver |
|-----------|-------------------|
| **URLs de imagens relativas** – tornam‑se quebradas no markdown | Use `md_options.features |= MarkdownFeatures.IMAGE` e então pós‑procese o markdown para reescrever os caminhos das imagens. |
| **Tabelas complexas** – o GitLab tem suporte limitado a tabelas | Mantenha o formatador padrão (`"DEFAULT"`) ou ajuste manualmente a sintaxe da tabela após a conversão. |
| **Caracteres Unicode** – podem aparecer como sequências escapadas | Garanta que seu script Python abra arquivos com `encoding="utf-8"` e defina `md_options.encoding = "UTF-8"` se a biblioteca expô-lo. |

## Dica profissional: Conversão em lote para uma pasta inteira

Se você precisar **generate markdown from html** para dezenas de arquivos, envolva as três etapas em um loop:

```python
import os

source_dir = "YOUR_DIRECTORY"
target_dir = "YOUR_DIRECTORY/markdown"

os.makedirs(target_dir, exist_ok=True)

for filename in os.listdir(source_dir):
    if filename.lower().endswith(".html"):
        html_path = os.path.join(source_dir, filename)
        md_path = os.path.join(target_dir, os.path.splitext(filename)[0] + ".md")

        html_doc = HTMLDocument(html_path)
        md_options = MarkdownSaveOptions()
        md_options.formatter = "GIT"
        md_options.features = MarkdownFeatures.LINK | MarkdownFeatures.PARAGRAPH

        Converter.convert(html_doc, md_options, md_path)
        print(f"Converted {filename} → {os.path.basename(md_path)}")
```

Este script **exports html as markdown** para cada arquivo `.html`, preservando o sabor GitLab ao longo do lote.

## Conclusão

Agora você tem um método completo e pronto para produção para **convert html to markdown**, escolher a saída **GitLab‑flavored markdown**, e definir opções **set markdown formatter** que correspondam às necessidades do seu projeto. Seguindo as etapas acima, você pode de forma confiável **export html as markdown**, **generate markdown from html**, e adaptar o pipeline para processamento em massa ou conjuntos de recursos personalizados.

Em seguida, considere explorar:

* Adicionar `MarkdownFeatures.IMAGE` para manter imagens embutidas quando você **export html as markdown** para documentação mais rica.
* Trocar o formatador para `"DEFAULT"` se precisar de um arquivo markdown mais genérico.
* Integrar essa conversão em um pipeline CI/CD para que cada relatório HTML se torne automaticamente um artefato Markdown.

Feliz codificação, e aproveite a transição perfeita de HTML para markdown limpo e pronto para GitLab!

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como converter HTML para Markdown com um formatador personalizado em Python](/html/english/python/general/how-to-convert-html-to-markdown-with-a-custom-formatter-in-p/)
- [Como converter HTML para markdown com imagens usando Python](/html/english/python/general/how-to-convert-html-to-markdown-with-images-using-python/)
- [Como converter HTML para Markdown com Python – guia completo](/html/english/python/general/how-to-convert-html-to-markdown-with-python-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}