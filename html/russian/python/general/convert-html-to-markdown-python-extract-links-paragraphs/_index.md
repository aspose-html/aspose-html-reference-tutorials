---
category: general
date: 2026-08-03
description: Преобразуйте HTML в Markdown с помощью Python. Узнайте, как извлекать
  ссылки из HTML и извлекать абзацы из HTML в рамках единого, эффективного преобразования.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- extract paragraphs from html
language: ru
lastmod: 2026-08-03
og_description: Конвертировать HTML в Markdown на Python с кратким примером, показывающим,
  как извлекать ссылки из HTML и извлекать абзацы из HTML, сохраняя результат в файл
  Markdown.
og_image_alt: Screenshot of Python code converting an HTML file to Markdown with selected
  links and paragraphs
og_title: Преобразование HTML в Markdown в Python — полное руководство по извлечению
schemas:
- author: GroupDocs
  dateModified: '2026-08-03'
  description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  headline: Convert HTML to Markdown Python – extract links & paragraphs
  type: TechArticle
- description: Convert HTML to Markdown using Python. Learn how to extract links from
    HTML and extract paragraphs from HTML in a single, efficient conversion.
  name: Convert HTML to Markdown Python – extract links & paragraphs
  steps:
  - name: Load the HTML document you want to convert
    text: '```python from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions,
      Converter'
  - name: Create a feature set that includes only the elements you need
    text: '```python # Instantiate the feature collection. selected_features = MarkdownSaveOptions.Features()'
  - name: Attach the feature set to the Markdown save options
    text: '```python md_options = MarkdownSaveOptions() md_options.features = selected_features
      ```'
  - name: Perform the conversion and save the result as a Markdown file
    text: '```python output_path = "YOUR_DIRECTORY/links_and_paragraphs.md" Converter.convert_html(html_doc,
      md_options, output_path) print(f"Conversion complete. Markdown saved to {output_path}")
      ```'
  type: HowTo
tags:
- HTML conversion
- Markdown
- Python
title: Конвертировать HTML в Markdown с помощью Python — извлечение ссылок и абзацев
url: /ru/python/general/convert-html-to-markdown-python-extract-links-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в Markdown с помощью Python – извлечение ссылок и абзацев

Если вам необходимо **преобразовать HTML в Markdown**, этот учебник покажет практический способ сделать это на Python, одновременно избирательно **извлекая ссылки из HTML** и **извлекая абзацы из HTML**. Вы увидите полный, исполняемый пример, который сохраняет отфильтрованное содержимое в чистый файл Markdown.

Преобразование HTML в Markdown — распространённый шаг, когда вам нужна лёгкая, версионируемая документация, контент для статических сайтов или просто текстовое представление веб‑страницы. К концу этого руководства у вас будет скрипт, который:

1. Загружает HTML‑документ с диска.  
2. Настраивает набор функций, оставляющий только ссылки и элементы абзацев.  
3. Выполняет преобразование с использованием GroupDocs Conversion SDK для Python.  
4. Записывает результат в файл с расширением `.md`.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

| Требование | Почему это важно |
|-------------|----------------|
| Python 3.9+ | SDK ориентирован на современные версии Python. |
| `groupdocs-conversion` package | Предоставляет классы `HTMLDocument`, `MarkdownSaveOptions` и `Converter`, используемые в примере. |
| HTML‑файл для тестирования (например, `sample.html`) | Исходный файл, который вы будете преобразовывать. |

Установите SDK с помощью pip:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** Используйте виртуальное окружение (`python -m venv .venv`), чтобы изолировать зависимости.

## Преобразование HTML в Markdown с помощью Python

Суть преобразования состоит из нескольких простых шагов. Каждый шаг объясняется ниже, а полный скрипт приведён в конце статьи.

### Шаг 1: Загрузите HTML‑документ, который хотите преобразовать

```python
from groupdocs.conversion import HTMLDocument, MarkdownSaveOptions, Converter

# Replace YOUR_DIRECTORY with the path that contains your HTML file.
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*Почему этот шаг?*  
`HTMLDocument` разбирает исходный файл и создаёт внутреннее представление DOM, с которым может работать конвертер. Без предварительной загрузки документа SDK нечего обрабатывать.

### Шаг 2: Создайте набор функций, включающий только необходимые элементы

```python
# Instantiate the feature collection.
selected_features = MarkdownSaveOptions.Features()

# Keep only hyperlinks.
selected_features.add(MarkdownSaveOptions.Features.LINK)

# Keep only paragraph tags.
selected_features.add(MarkdownSaveOptions.Features.PARAGRAPH)
```

*Почему мы добавляем эти функции*  
`MarkdownSaveOptions.Features` выступает в качестве фильтра. Добавляя `LINK` и `PARAGRAPH`, мы говорим конвертеру **извлекать ссылки из HTML** и **извлекать абзацы из HTML**, игнорируя изображения, таблицы, скрипты и другую разметку, которая может не понадобиться в конечном Markdown.

### Шаг 3: Привяжите набор функций к параметрам сохранения Markdown

```python
md_options = MarkdownSaveOptions()
md_options.features = selected_features
```

*Почему этот шаг?*  
`MarkdownSaveOptions` хранит все параметры преобразования. Присвоение ранее построенного `selected_features` гарантирует, что преобразование учитывает нашу конфигурацию фильтра.

### Шаг 4: Выполните преобразование и сохраните результат в файл Markdown

```python
output_path = "YOUR_DIRECTORY/links_and_paragraphs.md"
Converter.convert_html(html_doc, md_options, output_path)
print(f"Conversion complete. Markdown saved to {output_path}")
```

*Почему мы вызываем `convert_html`*  
`Converter.convert_html` — точка входа SDK для преобразования HTML в Markdown. Он читает `HTMLDocument`, применяет `md_options` и записывает отфильтрованный результат в `output_path`.

#### Ожидаемый вывод

Полученный файл `links_and_paragraphs.md` будет содержать только Markdown‑представления гиперссылок и текста абзацев, например:

```markdown
[Visit the homepage](https://example.com)

This is the first paragraph of the article, describing the main topic.

Another paragraph with more details.
```

Все остальные элементы HTML, такие как `<img>`, `<table>` или `<script>`, исключаются, делая файл лёгким и удобным для редактирования.

## Извлечение ссылок из HTML (опциональное углубление)

Если ваша цель — **только извлечь ссылки из HTML**, отбрасывая всё остальное, вы можете упростить набор функций:

```python
link_only_features = MarkdownSaveOptions.Features()
link_only_features.add(MarkdownSaveOptions.Features.LINK)

md_options.features = link_only_features
```

Запуск преобразования с этой конфигурацией создаёт файл Markdown, где каждая ссылка находится на отдельной строке, например:

```markdown


## Что стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Преобразование HTML в Markdown в Aspose.HTML для Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Преобразование HTML в Markdown в .NET с Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Как преобразовать HTML в PDF на Java – используя Aspose.HTML для Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}