---
category: general
date: 2026-11-24
description: Преобразуйте HTML в Markdown на Python, используя опции в стиле GitLab,
  и легко извлекайте ссылки.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- gitlab flavored markdown
- save html as markdown
- html to markdown conversion
- extract links to markdown
language: ru
lastmod: 2026-11-24
og_description: Преобразуйте HTML в Markdown в Python, используя опции в стиле GitLab,
  сохраняйте HTML как markdown и извлекайте ссылки в markdown с полным примером.
og_image_alt: Screenshot of a Python script converting HTML to GitLab‑flavored Markdown
og_title: Преобразование HTML в Markdown с выводом в стиле GitLab — руководство по
  Python
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Convert HTML to Markdown in Python using GitLab‑flavored options and
    extract links easily.
  headline: How to convert HTML to Markdown with GitLab‑flavored output in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Conversion
- GitLab
title: Как преобразовать HTML в Markdown с выводом в стиле GitLab на Python
url: /ru/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как конвертировать HTML в Markdown с поддержкой GitLab‑flavored в Python

Если вам нужно **конвертировать HTML в Markdown**, это руководство покажет готовое решение, готовое к запуску. Вы увидите, как сохранять html как markdown с форматированием GitLab‑flavored и как извлекать ссылки в markdown, не покидая код.

Подход работает с библиотекой Aspose.HTML for Python, которая предоставляет одно‑строчный API конвертации и тонкую настройку вкуса Markdown. К концу урока у вас будет скрипт, генерирующий чистые файлы markdown в стиле GitLab и список извлечённых ссылок.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* Python 3.8 или новее.
* Доступ к `pip` для установки пакетов.
* Локальный HTML‑файл (например, `article.html`), который нужно конвертировать.
* Базовое знакомство с запуском Python‑скриптов из командной строки.

Дополнительные инструменты не требуются; библиотека сама обрабатывает парсинг, конвертацию и извлечение ссылок.

## Установите библиотеку Aspose.HTML for Python

API конвертации находится в пакете `aspose.html`. Установите его через `pip`:

```bash
pip install aspose-html
```

Пакет включает классы `HTMLDocument`, `MarkdownSaveOptions` и `Converter`, которые используются дальше в скрипте. Установка занимает секунды и не требует отдельного runtime.

## Загрузите HTML‑документ

Создание объекта `HTMLDocument` загружает исходный файл в память. Конструктор принимает путь к файлу или URL.

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert.
doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

Экземпляр `doc` теперь представляет полное дерево DOM, позволяя конвертеру читать каждый элемент, включая ссылки и теги абзацев.

## Настройте параметры GitLab‑flavored Markdown

GitLab‑flavored markdown отличается от стандартного CommonMark тем, как обрабатываются ссылки и абзацы. Класс `MarkdownSaveOptions` позволяет указать форматтер и набор функций, которые вам нужны.

```python
from aspose.html import MarkdownSaveOptions

# Configure options for GitLab‑flavored output.
#   formatter="GIT"  -> GitLab markdown
#   features=["Link", "Paragraph"] -> keep only links and paragraphs.
opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])
```

Установка `features` в `["Link", "Paragraph"]` гарантирует, что конвертация сосредоточится на извлечении ссылок, сохраняя структуру абзацев — идеально для документации или генерации changelog‑ов.

## Выполните конвертацию и сохраните как Markdown

После загрузки документа и настройки параметров вызовите статический метод `Converter.convert`. Он записывает результат напрямую в целевой файл.

```python
from aspose.html import Converter

# Perform the conversion and write the markdown file.
Converter.convert(doc, "YOUR_DIRECTORY/article.md", opts)
```

После выполнения `article.md` будет содержать GitLab‑flavored markdown, отражающий оригинальные ссылки и абзацы HTML.

## Проверьте результат и извлеките ссылки в markdown

Откройте сгенерированный файл, чтобы убедиться в корректности конвертации. Вы должны увидеть синтаксис ссылок (`[text](url)`) и разрывы абзацев, соответствующие исходному коду.

```python
# Quick verification: read and print the first 10 lines.
with open("YOUR_DIRECTORY/article.md", "r", encoding="utf-8") as f:
    for i, line in enumerate(f):
        if i >= 10:
            break
        print(line.rstrip())
```

Если вам нужен простой список URL для дальнейшей обработки, вы можете извлечь их из `HTMLDocument` до конвертации:

```python
# Extract all anchor href attributes.
links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
print("Extracted links:", links)
```

Этот шаг демонстрирует **извлечение ссылок в markdown** с использованием уже построенного DOM, избегая повторного парсинга.

## Полный скрипт

Объединив всё вместе, получаем единый автономный скрипт, который можно добавить в любой проект:

```python
# convert_html_to_gitlab_md.py
from aspose.html import HTMLDocument, MarkdownSaveOptions, Converter

def convert_html_to_markdown(src_path: str, dst_path: str) -> list:
    """
    Convert an HTML file to GitLab‑flavored Markdown and return a list of extracted links.

    Args:
        src_path: Path to the source HTML file.
        dst_path: Path where the Markdown file will be saved.

    Returns:
        A list of URLs found in the HTML document.
    """
    # Load the HTML document.
    doc = HTMLDocument(src_path)

    # Configure GitLab‑flavored Markdown options (links and paragraphs only).
    opts = MarkdownSaveOptions(formatter="GIT", features=["Link", "Paragraph"])

    # Convert and save as Markdown.
    Converter.convert(doc, dst_path, opts)

    # Extract links for additional processing.
    links = [a.get_attribute("href") for a in doc.get_elements_by_tag_name("a")]
    return links

if __name__ == "__main__":
    source = "YOUR_DIRECTORY/article.html"
    target = "YOUR_DIRECTORY/article.md"
    extracted_links = convert_html_to_markdown(source, target)

    print(f"Conversion complete. Markdown saved to {target}")
    print("Extracted links:", extracted_links)
```

Запуск скрипта:

```bash
python convert_html_to_gitlab_md.py
```

создаёт `article.md` с GitLab‑flavored markdown и выводит список извлечённых URL.

## Распространённые варианты и граничные случаи

| Сценарий                              | Корректировка                                                               |
|--------------------------------------|-----------------------------------------------------------------------------|
| **Полный HTML (изображения, таблицы и т.д.)** | Добавьте `"Image"` или `"Table"` в `features`, чтобы сохранить эти элементы. |
| **Другой вкус Markdown**             | Измените `formatter="GIT"` на `"COMMONMARK"` или `"GFM"` для других платформ. |
| **Большие файлы (> 50 MB)**           | Используйте потоковые API (`HTMLDocument.open`), чтобы не загружать весь файл. |
| **Unicode‑символы**                  | Убедитесь, что исходный файл в кодировке UTF‑8; библиотека сохраняет кодировку.   |

Эти варианты позволяют переиспользовать тот же шаблон для **save html as markdown** в разных контекстах.

## Полезные советы

* **Переиспользуйте параметры:** Создайте один экземпляр `MarkdownSaveOptions` и передавайте его, если конвертируете несколько файлов в пакетной задаче.
* **Проверяйте ссылки:** После извлечения выполните простую проверку `requests.head(url)`, чтобы выявить битые URL.
* **Фиксация версии:** Зафиксируйте версию Aspose.HTML (`aspose-html==23.10`), чтобы избежать неожиданных изменений API.

## Заключение

Теперь вы знаете, как **конвертировать HTML в markdown** с помощью форматтера GitLab‑flavored, **save html as markdown** и **извлекать ссылки в markdown** с помощью лаконичного Python‑скрипта. Решение работает «из коробки», обрабатывает типичные граничные случаи и может быть расширено под другие вкусы Markdown или дополнительные возможности HTML.

### Следующие шаги

* Исследуйте список `features`, чтобы добавить изображения, таблицы или блоки кода.
* Интегрируйте этот скрипт в CI‑конвейер для автоматической генерации документации из HTML‑источников.
* Скомбинируйте извлечённые ссылки с сервисом проверки ссылок, чтобы поддерживать здоровые референсы.

Не стесняйтесь адаптировать скрипт под свои рабочие процессы и делиться результатами с сообществом!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Convert HTML to Markdown Python – extract links & paragraphs](/html/english/python/general/convert-html-to-markdown-python-extract-links-paragraphs/)
- [How to convert HTML to Markdown with GitLab‑flavored markdown in Python](/html/english/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-markdow/)
- [convert html to markdown python – save markdown file with python](/html/english/python/general/convert-html-to-markdown-python-save-markdown-file-with-pyth/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}