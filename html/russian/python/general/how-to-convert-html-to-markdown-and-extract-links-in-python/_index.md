---
category: general
date: 2026-10-28
description: 'Конвертировать HTML в Markdown с помощью Python: научитесь извлекать
  ссылки из HTML и сохранять их в Markdown в стиле GitLab всего за три шага.'
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- how to convert html document
language: ru
lastmod: 2026-10-28
og_description: Быстро преобразуйте HTML в Markdown с помощью Python. Это руководство
  показывает, как извлекать ссылки из HTML и создавать Markdown в стиле GitLab в три
  простых шага.
og_image_alt: Screenshot of Python script converting HTML to GitLab‑flavored Markdown
  with extracted links
og_title: Преобразовать HTML в Markdown и извлечь ссылки с помощью Python
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: 'convert html to markdown using Python: learn to extract links from
    HTML and save as GitLab‑flavored Markdown in just three steps.'
  headline: How to convert HTML to Markdown and extract links in Python
  type: TechArticle
- description: 'convert html to markdown using Python: learn to extract links from
    HTML and save as GitLab‑flavored Markdown in just three steps.'
  name: How to convert HTML to Markdown and extract links in Python
  steps:
  - name: Multiple input sources
    text: 'If you need to batch‑process a folder of HTML files, wrap the conversion
      in a loop:'
  - name: Missing links
    text: When an HTML document contains no `<a>` elements, the converter still creates
      a valid Markdown file containing only the permitted paragraphs. No additional
      error handling is required, but you can check `save_options.features` if you
      need to enforce the presence of links.
  - name: Custom output encoding
    text: 'If your target system expects UTF‑8 with a BOM, set the encoding on the
      `MarkdownSaveOptions`:'
  type: HowTo
tags:
- HTML
- Markdown
- Python
- Conversion
title: Как конвертировать HTML в Markdown и извлекать ссылки в Python
url: /ru/python/general/how-to-convert-html-to-markdown-and-extract-links-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как конвертировать HTML в Markdown и извлекать ссылки в Python

Если вам нужно **конвертировать HTML в Markdown**, этот учебник предоставляет полное готовое решение. Вы увидите, как извлекать ссылки из HTML, выбрать форматировщик Markdown в стиле GitLab и сохранить результат всего несколькими строками кода.

В руководстве охвачено всё, что вам нужно: необходимые пакеты, загрузка HTML из разных источников, настройка `MarkdownSaveOptions` и обработка граничных случаев, таких как отсутствие ссылок или пользовательские каталоги вывода. К концу вы сможете ответить на вопрос *как конвертировать HTML‑документ* в чистый Markdown с богатыми ссылками для любого последующего рабочего процесса.

## Требования

- Python 3.8 или новее
- пакет `aspose-html` (официальная библиотека Aspose.HTML для Python)
- Базовое знакомство со скриптами Python и вводом‑выводом файлов

You can install the library with:

```bash
pip install aspose-html
```

> **Совет:** Используйте виртуальное окружение, чтобы изолировать зависимости.

## Шаг 1: Загрузка HTML‑содержимого

Первый шаг — создать объект `HTMLDocument`. Aspose.HTML принимает строку, путь к файлу или URL, поэтому вы можете выбрать источник, соответствующий вашему проекту.

```python
from aspose.html import HTMLDocument

# Example 1: Load from a raw HTML string
html_string = "<h1>Title</h1><p>Sample <a href='https://example.com'>link</a></p>"
html_doc = HTMLDocument(html_string)

# Example 2: Load from a local file
# html_doc = HTMLDocument("input.html")

# Example 3: Load from a remote URL
# html_doc = HTMLDocument("https://www.example.com")
```

> **Почему это важно:** Загрузка документа один раз дает вам объект, похожий на DOM, который конвертер может обходить, гарантируя, что все ссылки и узлы абзацев доступны для извлечения.

## Шаг 2: Настройка параметров сохранения Markdown

`MarkdownSaveOptions` позволяет управлять форматом вывода и тем, какие функции HTML переводятся. Чтобы **извлекать ссылки из HTML**, сохраняя абзацы, включите функции `LINK` и `PARAGRAPH` и выберите форматировщик GitLab.

```python
from aspose.html import MarkdownSaveOptions

save_options = MarkdownSaveOptions()
# Use GitLab‑flavored Markdown (supports task lists, tables, etc.)
save_options.formatter = MarkdownSaveOptions.Formatter.GIT

# Export only links and paragraphs – other tags (e.g., images) are ignored
save_options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)
```

> **Почему это важно:** Ограничение функций уменьшает шум в выводе и гарантирует, что полученный Markdown содержит только те элементы, которые вам нужны — идеально для конвейеров документации или генераторов статических сайтов.

## Шаг 3: Конвертация HTML‑документа и запись файла

Теперь вызовите `Converter.convert_html`, передав документ, параметры и путь назначения.

```python
from aspose.html import Converter

output_path = "output.md"  # Change to your desired directory/file name
Converter.convert_html(html_doc, save_options, output_path)
print(f"Markdown file saved to {output_path}")
```

Запуск скрипта создаёт файл `output.md` со следующим содержимым:

```markdown
# Title

Sample [link](https://example.com)
```

Обратите внимание, что отображаются только заголовок, абзац и ссылка — именно то, что мы запросили при настройке `save_options`.

## Обработка распространённых вариантов и граничных случаев

### Несколько источников ввода

Если вам нужно пакетно обработать папку с HTML‑файлами, оберните конвертацию в цикл:

```python
import pathlib
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

input_folder = pathlib.Path("html_inputs")
output_folder = pathlib.Path("markdown_outputs")
output_folder.mkdir(exist_ok=True)

options = MarkdownSaveOptions()
options.formatter = MarkdownSaveOptions.Formatter.GIT
options.features = (
    MarkdownSaveOptions.Features.LINK |
    MarkdownSaveOptions.Features.PARAGRAPH
)

for html_path in input_folder.glob("*.html"):
    doc = HTMLDocument(str(html_path))
    md_path = output_folder / (html_path.stem + ".md")
    Converter.convert_html(doc, options, str(md_path))
    print(f"Converted {html_path.name} → {md_path.name}")
```

### Отсутствие ссылок

Когда HTML‑документ не содержит элементов `<a>`, конвертер всё равно создаёт корректный файл Markdown, содержащий только разрешённые абзацы. Дополнительная обработка ошибок не требуется, но вы можете проверить `save_options.features`, если необходимо обеспечить наличие ссылок.

### Пользовательская кодировка вывода

Если ваша целевая система ожидает UTF‑8 с BOM, задайте кодировку в `MarkdownSaveOptions`:

```python
save_options.encoding = "utf-8-sig"
```

## Полный, исполняемый пример

Объединив всё вместе, представляем автономный скрипт, который вы можете скопировать и сразу запустить:

```python
# convert_html_to_markdown.py
# -------------------------------------------------
# Demonstrates how to convert HTML to Markdown while
# extracting only links and paragraphs using Aspose.HTML.
# -------------------------------------------------

from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def main():
    # 1️⃣ Load HTML – replace this with your own source if needed
    html = "<h1>Title</h1><p>Sample <a href='https://example.com'>link</a></p>"
    document = HTMLDocument(html)

    # 2️⃣ Configure Markdown options (GitLab flavor, links + paragraphs only)
    options = MarkdownSaveOptions()
    options.formatter = MarkdownSaveOptions.Formatter.GIT
    options.features = (
        MarkdownSaveOptions.Features.LINK |
        MarkdownSaveOptions.Features.PARAGRAPH
    )

    # 3️⃣ Convert and save
    output_file = "output.md"
    Converter.convert_html(document, options, output_file)
    print(f"✅ Markdown saved to {output_file}")

if __name__ == "__main__":
    main()
```

Выполните с помощью:

```bash
python convert_html_to_markdown.py
```

Вы увидите `output.md`, содержащий ожидаемое представление в Markdown.

## Заключение

Теперь вы знаете, как **конвертировать HTML в Markdown** в Python, извлекать ссылки из HTML и управлять форматом вывода с помощью `MarkdownSaveOptions`. Этот подход работает с отдельными файлами, пакетами или даже удалёнными URL, предоставляя гибкую основу для генераторов документации, конвейеров статических сайтов или скриптов извлечения данных.

**Следующие шаги**

- Экспериментируйте с другими `MarkdownSaveOptions.Features`, такими как `TABLE` или `IMAGE`, чтобы включить больше элементов HTML.
- Переключите форматировщик на `MarkdownSaveOptions.Formatter.CommonMark`, если требуется строгая совместимость с CommonMark.
- Сочетайте эту конвертацию с генератором статических сайтов (например, MkDocs), чтобы автоматизировать публикацию контента.

Удачной разработки!

## Что вам следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Convert HTML to Markdown Python – extract links & paragraphs](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [Convert HTML to Markdown in Python – GitLab Flavored Guide](/html/english/python/general/convert-html-to-markdown-in-python-gitlab-flavored-guide/)
- [Convert HTML to Markdown with Python – Complete Guide](/html/english/python/general/convert-html-to-markdown-with-python-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}