---
category: general
date: 2026-05-31
description: Узнайте, как извлекать SVG из HTML с помощью Python. Этот пошаговый учебник
  показывает, как читать HTML‑документ, сохранять SVG‑файлы и эффективно сохранять
  встроенный SVG.
draft: false
keywords:
- how to extract svg
- read html document
- save svg files
- save inline svg
- extract svg from html
language: ru
og_description: Как извлечь SVG из HTML с помощью Python. Следуйте этому руководству,
  чтобы прочитать HTML‑документ, сохранить SVG‑файлы и легко работать с встроенным
  SVG.
og_title: Как извлечь SVG из HTML с помощью Python – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  headline: How to extract SVG from HTML with Python – Complete Guide
  type: TechArticle
- description: Learn how to extract SVG from HTML using Python. This step‑by‑step
    tutorial shows how to read HTML document, save SVG files and save inline SVG efficiently.
  name: How to extract SVG from HTML with Python – Complete Guide
  steps:
  - name: Reads an HTML file.
    text: Reads an HTML file.
  - name: Collects inline <svg> markup.
    text: Collects inline <svg> markup.
  - name: Finds external SVG references (<img> and <object> tags).
    text: Finds external SVG references (<img> and <object> tags).
  - name: Saves each SVG to a separate .svg file.
    text: Saves each SVG to a separate .svg file.
  type: HowTo
tags:
- Python
- SVG
- HTML parsing
- Aspose
title: Как извлечь SVG из HTML с помощью Python — Полное руководство
url: /ru/python/general/how-to-extract-svg-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как извлечь SVG из HTML с помощью Python – Полное руководство

Когда‑нибудь задавались вопросом, **как извлечь SVG** из запутанной HTML‑страницы, не теряя волосы? Вы не одиноки. Независимо от того, создаёте ли вы веб‑скрейпер, конвейер дизайна или просто нужно пакетно экспортировать иконки, знание **как извлечь SVG** — полезный приём, экономящий время и нервы.

В этом руководстве мы покажем вам точно **как извлечь SVG** с помощью библиотеки Aspose.HTML для Python. Мы прочитаем HTML‑документ, извлечём как встроенную разметку `<svg>`, так и внешние ссылки на SVG, а затем **сохраним SVG‑файлы** на диск — всё в аккуратном, переиспользуемом скрипте. К концу вы получите готовое решение, которое можно адаптировать под свои проекты.

> **Pro tip:** Если вам нужен лишь быстрый «нюх» страницы, подойдёт и `BeautifulSoup`, но Aspose.HTML предоставляет полноценный DOM, что делает извлечение как встроенных, так и связанных SVG простым делом.

## Что вам понадобится

Прежде чем погрузиться, убедитесь, что у вас есть:

* Python 3.8+ (код использует f‑строки, так что минимум 3.6)
* `pip install aspose-html` – коммерческая библиотека, обеспечивающая наш парсинг HTML
* Папка с файлом `input.html`, содержащим SVG, которые нужно извлечь
* Права записи в каталог вывода (мы назовём его `YOUR_DIRECTORY`)

И всё — никаких дополнительных бинарных файлов, без безголовых браузеров. Просто, верно?

## Шаг 1: Прочитать HTML‑документ с Aspose.HTML

Первое, что нужно сделать, — **прочитать HTML‑документ**, чтобы пройтись по его DOM‑дереву. Aspose.HTML предоставляет объект `HTMLDocument`, который ведёт себя как `document` в браузере.

```python
from aspose.html import HTMLDocument

# Load the HTML file – replace YOUR_DIRECTORY with the actual path
doc = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Почему это важно:* Загрузив HTML в корректный DOM, вы избегаете подводных камней парсинга с помощью регулярных выражений и получаете такие методы, как `get_elements_by_tag_name` и `query_selector_all`, «бесплатно».

## Шаг 2: Собрать все встроенные элементы <svg>

Встроенные SVG — это блоки `<svg>…</svg>`, находящиеся непосредственно внутри HTML. Чтобы **сохранить встроенный SVG**, нам нужен лишь их внешний HTML.

```python
svg_contents = []  # We'll collect both markup and file paths here

# Find every <svg> element in the document
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)   # Store the raw markup
```

Обратите внимание, что мы добавляем необработанную разметку напрямую в `svg_contents`. Позже решим, является ли каждый элемент разметкой или путём к файлу.

## Шаг 3: Найти внешние ссылки на SVG (теги img и object)

Многие страницы ссылаются на внешние SVG‑файлы через `<img src="icon.svg">` или `<object data="logo.svg">`. Чтобы **извлечь SVG из HTML**, необходимо также захватить эти URL‑адреса.

```python
# CSS selector: img or object whose src/data ends with .svg (case‑insensitive)
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    # For <img> we read the src attribute, for <object> the data attribute
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:                                   # Guard against missing attribute
        svg_contents.append(src)
```

*Внимание к краевому случаю:* Если URL SVG относительный, его следует объединить с базовым путём HTML‑файла. Для краткости будем считать, что HTML находится рядом с SVG‑файлами.

## Шаг 4: Записать каждый SVG в отдельный файл

Теперь, когда у нас есть смешанный список строк разметки и путей к файлам, мы пройдём его и **сохраним SVG‑файлы**. Скрипт автоматически различает встроенную разметку и ссылку на существующий файл.

```python
import os
import shutil

for index, content in enumerate(svg_contents):
    output_path = f"YOUR_DIRECTORY/svg_{index}.svg"

    # Trim leading whitespace and check if it looks like markup
    if content.lstrip().startswith("<svg"):
        # Inline SVG – write the markup directly
        with open(output_path, "w", encoding="utf-8") as file:
            file.write(content)
        print(f"Saved inline SVG to {output_path}")
    else:
        # External reference – copy the source file's contents
        src_path = os.path.abspath(content)  # Resolve relative paths
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, output_path)
            print(f"Copied external SVG from {src_path} to {output_path}")
        else:
            print(f"⚠️  Warning: referenced SVG not found: {src_path}")
```

**Что вы увидите:** После завершения скрипта в `YOUR_DIRECTORY` появятся файлы `svg_0.svg`, `svg_1.svg`, … каждый из которых содержит либо оригинальную встроенную разметку, либо копию внешнего SVG.

### Ожидаемый вывод

```
Saved inline SVG to YOUR_DIRECTORY/svg_0.svg
Saved inline SVG to YOUR_DIRECTORY/svg_1.svg
Copied external SVG from /path/to/logo.svg to YOUR_DIRECTORY/svg_2.svg
...
```

Если какой‑то файл отсутствует, скрипт выведет предупреждение, но продолжит работу — один битый линк не остановит весь процесс извлечения.

## Обработка распространённых подводных камней

| Проблема | Почему происходит | Быстрое решение |
|----------|-------------------|-----------------|
| **Относительные URL‑ы ломаются** | Атрибут `src` может быть `"../assets/icon.svg"` | Используйте `os.path.join(os.path.dirname(html_path), src)` для разрешения пути. |
| **Дублирующиеся имена файлов** | Два SVG с одинаковым именем перезаписывают друг друга | Добавьте хеш содержимого в имя файла (`hashlib.md5(content.encode()).hexdigest()[:8]`). |
| **Большие встроенные SVG вызывают всплеск памяти** | Хранение всей разметки в списке перед записью | Записывайте каждый элемент сразу в файл, а не буферизуйте. |
| **Проходят не‑SVG изображения** | Некоторые теги `<img>` заканчиваются на `.svg?version=1` | Удаляйте строку запроса перед проверкой расширения (`src.split('?')[0]`). |

## Полный скрипт, который можно скопировать и вставить

Ниже представлен полностью готовый к запуску код. Сохраните его как `extract_svg.py`, отредактируйте `YOUR_DIRECTORY` и запустите `python extract_svg.py`.

```python
"""
extract_svg.py – How to extract SVG from HTML using Aspose.HTML for Python

This script:
1. Reads an HTML file.
2. Collects inline <svg> markup.
3. Finds external SVG references (<img> and <object> tags).
4. Saves each SVG to a separate .svg file.

Author: Your Name
Date: 2026-05-31
"""

import os
import shutil
from aspose.html import HTMLDocument

# ----------------------------------------------------------------------
# Configuration – change these paths to suit your environment
# ----------------------------------------------------------------------
HTML_PATH = "YOUR_DIRECTORY/input.html"          # Path to source HTML
OUTPUT_DIR = "YOUR_DIRECTORY"                    # Where SVGs will be written

# Ensure output directory exists
os.makedirs(OUTPUT_DIR, exist_ok=True)

# ----------------------------------------------------------------------
# Step 1: Load the HTML document (read html document)
# ----------------------------------------------------------------------
doc = HTMLDocument(HTML_PATH)

# ----------------------------------------------------------------------
# Step 2: Collect inline <svg> elements (save inline svg)
# ----------------------------------------------------------------------
svg_contents = []
for element in doc.get_elements_by_tag_name("svg"):
    svg_contents.append(element.outer_html)

# ----------------------------------------------------------------------
# Step 3: Collect external SVG references (extract svg from html)
# ----------------------------------------------------------------------
selector = "img[src$='.svg'], object[data$='.svg']"
for element in doc.query_selector_all(selector):
    src = element.get_attribute("src") or element.get_attribute("data")
    if src:
        # Resolve relative paths relative to the HTML file location
        src_path = os.path.join(os.path.dirname(HTML_PATH), src)
        svg_contents.append(src_path)

# ----------------------------------------------------------------------
# Step 4: Save each gathered SVG (save svg files)
# ----------------------------------------------------------------------
for idx, content in enumerate(svg_contents):
    out_path = os.path.join(OUTPUT_DIR, f"svg_{idx}.svg")

    # Detect inline markup vs file path
    if isinstance(content, str) and content.lstrip().startswith("<svg"):
        # Inline SVG – write directly
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(content)
        print(f"[✓] Inline SVG saved → {out_path}")
    else:
        # External file – copy its contents
        src_path = os.path.abspath(content)
        if os.path.isfile(src_path):
            shutil.copyfile(src_path, out_path)
            print(f"[✓] External SVG copied → {out_path}")
        else:
            print(f"[⚠] Missing SVG file: {src_path}")

print("\n✅ Extraction complete. Check the", OUTPUT_DIR, "folder for your SVGs.")
```

## Итоги – Как извлечь SVG в двух словах

* **Прочитать HTML‑документ** с помощью `HTMLDocument`.
* **Собрать встроенные `<svg>`** через `get_elements_by_tag_name`.
* **Найти внешние SVG** с помощью CSS‑селектора, оканчивающегося на `.svg`.
* **Сохранить каждый элемент** — записать разметку напрямую в файл или скопировать внешний файл.
* **Обработать краевые случаи**: относительные пути, дубли, отсутствующие файлы.

Это и есть полный ответ на вопрос **как извлечь SVG** из HTML‑страницы, упакованный в один простой для модификации скрипт.

## Что дальше?

Теперь, когда вы умеете **извлекать SVG** надёжно, рассмотрите следующие идеи:

* **Пакетная обработка:** Пробегайте каталог HTML‑файлов, собирая библиотеку иконок.
* **Оптимизация:** Пропускайте каждый сохранённый SVG через SVGO (оптимизатор на Node.js), чтобы уменьшить размер.
* **Конверсия:** Используйте `cairosvg` или `svglib` для преобразования SVG в PNG для устаревших браузеров.
* **Извлечение метаданных:** Парсите теги `<title>` или `<desc>` внутри каждого SVG для создания поисковых меток.

Все эти темы связаны с нашими вторичными ключевыми словами — **read HTML document**, **save svg files**, **save inline svg**, **extract svg from html** — так что вам найдётся много материала для дальнейшего изучения.

---

*Счастливого хакерства! Если возникнут проблемы, оставляйте комментарий ниже или пишите мне на GitHub. Мир SVG огромен, но с правильными инструментами его извлечение — проще простого.*

## Что стоит изучить дальше?

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)
- [Rendre un document SVG au format PNG dans .NET avec Aspose.HTML](/html/french/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}