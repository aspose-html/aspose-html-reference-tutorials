---
category: general
date: 2026-09-26
description: Конвертировать HTML в Markdown с помощью Python, извлекать ссылки из
  HTML и сохранять HTML в виде Markdown. Узнайте, как конвертировать HTML шаг за шагом.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- extract links from html
- save html as markdown
- how to convert html
- extract paragraphs from html
language: ru
lastmod: 2026-09-26
og_description: Преобразуйте HTML в Markdown с помощью Python, извлекая ссылки из
  HTML и сохраняйте HTML в формате Markdown. Следуйте этому полному руководству.
og_image_alt: Screenshot of Python code converting HTML to Markdown and showing extracted
  links
og_title: Преобразовать HTML в Markdown на Python — извлекать ссылки и абзацы
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
title: Преобразовать HTML в Markdown в Python — легко извлекать ссылки и абзацы
url: /ru/python/general/convert-html-to-markdown-in-python-extract-links-and-paragra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в Markdown в Python – легко извлекать ссылки и абзацы

Если вам нужно **convert HTML to Markdown**, оставляя только полезные части, это руководство покажет, как сделать это всего несколькими строками кода на Python. Независимо от того, собираете ли вы блоги, архивируете документацию или очищаете тело писем, вы узнаете надёжный способ извлекать ссылки из HTML и сохранять HTML в виде Markdown.

В руководстве рассматривается всё: от установки необходимого пакета до обработки граничных случаев, таких как пустые теги `<a>` или вложенные абзацы. К концу вы получите готовый к запуску скрипт, который **converts HTML to Markdown**, извлекает ссылки из HTML и даже извлекает абзацы из HTML, когда это необходимо.

---

## Предварительные требования

Перед началом убедитесь, что у вас есть:

* Установлен Python 3.8 или новее  
* Доступ к Python‑пакету `groupdocs-conversion` (библиотека, предоставляющая `HTMLDocument`, `MarkdownSaveOptions` и `Converter`)  
* Локальный HTML‑файл, который вы хотите обработать (например, `article.html`)

Вы можете установить библиотеку с помощью pip:

```bash
pip install groupdocs-conversion
```

> **Pro tip:** Используйте виртуальное окружение (`python -m venv venv`), чтобы изолировать зависимости.

---

## Шаг 1: Загрузить исходный HTML‑документ

Первая операция – создать объект `HTMLDocument`, указывающий на ваш исходный файл. Этот объект абстрагирует сырой HTML и предоставляет конвертеру чистую точку входа.

```python
from groupdocs.conversion import HTMLDocument

# Load the HTML file you want to transform
html_doc = HTMLDocument("YOUR_DIRECTORY/article.html")
```

*Почему это важно:* Загрузка документа таким способом позволяет библиотеке один раз разобрать DOM, поэтому последующие операции (например, извлечение ссылок или абзацев) выполняются быстро и экономно по памяти.

---

## Шаг 2: Создать параметры сохранения Markdown и выбрать нужные функции

`MarkdownSaveOptions` позволяет решить, какие HTML‑элементы сохраняются после конвертации. Флаг `features` использует побитовое ИЛИ для комбинирования опций.

```python
from groupdocs.conversion import MarkdownSaveOptions, MarkdownFeatures

# Keep only links and paragraphs in the resulting Markdown
md_options = MarkdownSaveOptions()
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS
```

*Почему это важно:* Указывая `LINKS` и `PARAGRAPHS`, вы **extract links from HTML** и **extract paragraphs from HTML**, отбрасывая всё остальное (стили, скрипты, изображения). Если позже нужны только ссылки, замените `MarkdownFeatures.PARAGRAPHS` на `0` (или опустите его).

---

## Шаг 3: Преобразовать HTML в Markdown, используя настроенные параметры

Теперь вызовите статический метод `convert_html`, передав исходный документ, путь назначения и только что построенные параметры.

```python
from groupdocs.conversion import Converter

# Perform the conversion and write the Markdown file
Converter.convert_html(html_doc, "YOUR_DIRECTORY/article_links.md", md_options)
```

*Почему это важно:* Конвертация выполняется за один проход, применяя указанный фильтр функций. Полученный файл (`article_links.md`) содержит только ссылки и абзацы в формате Markdown, что именно то, что нужно, когда вы хотите **save HTML as Markdown** для дальнейшей обработки.

---

## Полный скрипт – всё вместе

Ниже представлен полностью готовый к запуску скрипт, который вы можете скопировать в файл с именем `html_to_md.py`. Подкорректируйте пути под вашу среду.

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

### Ожидаемый вывод

Запуск скрипта генерирует файл, похожий на следующий (точное содержание зависит от исходного HTML):

```markdown
[OpenAI](https://openai.com)

This is the first paragraph of the article.

[GitHub](https://github.com)

Another paragraph that explains the next topic.
```

Появляются только текст ссылки и текст абзаца; все остальные HTML‑элементы удаляются.

---

## Извлечение только ссылок или только абзацев (расширенные варианты)

Иногда вам нужно **how to convert HTML** в файл Markdown, содержащий только один тип элементов.

### 1. Извлечение только ссылок

```python
md_options.features = MarkdownFeatures.LINKS   # No paragraphs
```

### 2. Извлечение только абзацев

```python
md_options.features = MarkdownFeatures.PARAGRAPHS   # No links
```

Оба варианта используют один и тот же вызов `convert_html`, поэтому нет необходимости писать отдельную логику конвертации.

---

## Обработка граничных случаев

| Ситуация                               | Рекомендуемое решение |
|----------------------------------------|-----------------------|
| HTML‑файл содержит пустые теги `<a>`    | Конвертер автоматически пропускает пустые ссылки. Если вы видите лишние `[]()` записи, установите `md_options.removeEmptyLinks = True`. |
| Вложенные абзацы (`<p>` внутри `<div>`) | Библиотека расплющивает вложенные абзацы, сохраняя порядок текста. Дополнительный код не требуется. |
| Не‑ASCII символы в названиях ссылок    | Убедитесь, что ваш Python‑файл сохранён в кодировке UTF‑8 и открывайте выходной файл с параметром `encoding="utf-8"`, если читаете его позже. |
| Очень большие HTML‑файлы (≥ 50 MB)        | Обрабатывайте файл кусками, используя `HTMLDocument(stream=io.BytesIO(...))`, чтобы избежать загрузки всего файла в память. |

---

## Часто задаваемые вопросы

**Q: Работает ли это с фрагментами HTML (без корневого тега `<html>`)?**  
A: Да. `HTMLDocument` принимает любой корректно сформированный фрагмент; конвертер рассматривает фрагмент как тело документа.

**Q: Можно ли сохранить изображения в синтаксисе Markdown?**  
A: Добавьте `MarkdownFeatures.IMAGES` к флагу `features`:  
```python
md_options.features = MarkdownFeatures.LINKS | MarkdownFeatures.PARAGRAPHS | MarkdownFeatures.IMAGES
```

**Q: Как конвертировать множество файлов в каталоге?**  
A: Оберните `convert_html_to_markdown` в цикл, который проходит по каталогу с помощью `os.listdir` или `pathlib.Path.rglob("*.html")`.

---

## Заключение

Теперь вы знаете, как **convert HTML to Markdown** в Python, выбирая только **extract links from HTML** и **extract paragraphs from HTML**. Скрипт демонстрирует стандартный подход — загрузить документ, настроить `MarkdownSaveOptions` и запустить `Converter.convert_html`. С небольшими изменениями вы также сможете **save HTML as Markdown**, содержащий только ссылки, только абзацы или полное точное представление.

Далее вы можете изучить:

* Добавление `MarkdownFeatures.HEADINGS` для сохранения заголовков разделов.  
* Использование полученного Markdown в качестве входных данных для статических генераторов сайтов, таких как MkDocs или Hugo.  
* Автоматизацию массового преобразования для всего репозитория документации.

Удачной конвертации!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Преобразовать HTML в Markdown в .NET с Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Преобразовать HTML в Markdown в Aspose.HTML для Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Как установить смещение при преобразовании HTML в Markdown в Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}