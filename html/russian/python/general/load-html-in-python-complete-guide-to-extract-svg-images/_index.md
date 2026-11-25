---
category: general
date: 2026-06-10
description: Загружайте HTML в Python, чтобы извлекать SVG‑изображения со своих страниц
  — пошаговый код, советы и обработка крайних случаев.
draft: false
keywords:
- load html python
- extract svg images
- extract svg from html
- search html svg
- find inline svg
language: ru
og_description: Загружайте HTML в Python и извлекайте SVG‑изображения с понятным,
  исполняемым примером. Узнайте, как искать SVG‑элементы в HTML и обрабатывать граничные
  случаи.
og_title: Загрузка HTML в Python – эффективное извлечение SVG‑изображений
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
title: Загрузка HTML в Python — Полное руководство по извлечению SVG‑изображений
url: /ru/python/general/load-html-in-python-complete-guide-to-extract-svg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Загрузка HTML в Python – Полное руководство по извлечению SVG‑изображений

Когда‑то вам нужно было **загрузить HTML в Python**, чтобы вытащить все SVG‑графики со страницы? Вы не одиноки. Будь то создание веб‑скрейпера, генерация отчёта об ассетах или просто интерес к иконкам, которые использует сайт, умение **извлекать SVG‑изображения** экономит кучу ручной работы.

В этом руководстве мы пройдем практическое решение от начала до конца, которое **загружает HTML в Python**, затем **ищет HTML SVG** элементы, **находит встроенный SVG** и даже получает внешние SVG‑файлы, указанные в тегах `<img>`. К концу вы получите переиспользуемый скрипт, несколько советов для сложных моментов и чёткое представление о том, как выглядит результат.

## Что вы получите

* Полностью рабочий скрипт на Python, который парсит локальный HTML‑файл (или полученную страницу) и выводит список всех найденных SVG.  
* Понимание разницы между **inline SVG** (`<svg>…</svg>`) и **external SVG** (`<img src="… .svg">`).  
* Стратегии обработки некорректной разметки, отсутствующих файлов и особенностей пространств имён.  
* Идеи для расширения кода — сохранение SVG, конвертация их в PNG или загрузка в базу данных.

### Предварительные требования

* Установлен Python 3.8+.  
* Базовое знакомство с библиотеками Python `requests` и `BeautifulSoup` (мы их импортируем, глубокого погружения не требуется).  
* Локальный HTML‑файл или URL, который вы хотите просканировать.  

Итак, приступим.

## Загрузка HTML в Python — настройка парсера

Первый шаг — **загрузить HTML в Python**. Вы можете либо прочитать файл с диска, либо получить удалённую страницу. Ниже представлен минимальный, но надёжный помощник, который делает и то, и другое:

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

> **Почему это важно:** Использование `BeautifulSoup` скрывает особенности парсинга сырых строк, а функция элегантно обрабатывает как локальные файлы, так и удалённые URL. Она также генерирует исключение при неудачном сетевом запросе — так вы сразу узнаете, когда что‑то пошло не так.

## Извлечение SVG‑изображений — поиск встроенных SVG‑элементов

После загрузки документа следующий логичный шаг — **найти теги inline SVG**. Встроенный SVG размещён непосредственно в разметке HTML, что позволяет получить его сразу из DOM.

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

*Совет:* Если страница использует пространства имён SVG (`<svg xmlns="http://www.w3.org/2000/svg">`), `BeautifulSoup` всё равно находит тег, потому что по умолчанию игнорирует пространства имён. Это удобно, когда вы просто **ищете HTML SVG**.

## Поиск HTML SVG — обработка внешних ссылок `<img>`

Многие сайты не встраивают SVG напрямую; они ссылаются на внешние файлы через `<img src="icon.svg">`. Чтобы их захватить, нужно пройтись по каждому тегу `<img>`, проверить его `src` и убедиться, что он заканчивается на `.svg`.

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

> **Внимание к краевому случаю:** На некоторых страницах используются строки запроса (`icon.svg?v=2`) или фрагменты (`icon.svg#layer`). Проверка `endswith(".svg")` всё равно работает, потому что мы смотрим только на нижний регистр конца строки. Если нужна более строгая проверка, рассмотрите использование `urllib.parse` для удаления параметров.

## Поиск встроенного SVG — отчёт о результатах

Теперь, когда у нас есть два списка — один с разметкой inline SVG, а другой с внешними ссылками на файлы — мы можем объединить их и вывести общее количество. Это отражает оригинальный фрагмент, который вы разместили, но добавляет немного контекста.

```python
def report_svg_counts(inline_svgs: list, external_svgs: list) -> None:
    total = len(inline_svgs) + len(external_svgs)
    print(f"Found {len(inline_svgs)} inline SVG element(s).")
    print(f"Found {len(external_svgs)} external SVG reference(s).")
    print(f"Overall, {total} SVG item(s) detected.")
```

## Сводим всё вместе — полный скрипт

Ниже представлен полный, готовый к запуску, скрипт. Сохраните его как `extract_svg.py` и укажите путь к локальному HTML‑файлу или URL.

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

### Ожидаемый вывод

Запуск скрипта на примере `sample.html` может вывести:

```
Found 3 inline SVG element(s).
Found 2 external SVG reference(s).
Overall, 5 SVG item(s) detected.
Saved inline SVG #1 to inline_svg_1.svg
Saved inline SVG #2 to inline_svg_2.svg
Saved inline SVG #3 to inline_svg_3.svg
```

Если раскомментировать блок загрузки, внешний SVG

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и изучить альтернативные подходы к реализации в ваших проектах.

- [svg to png java – Конвертация SVG в изображение с помощью Aspose.HTML для Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Convert SVG to Image in .NET with Aspose.HTML](/html/english/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [How to Convert SVG to XPS with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-xps/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}