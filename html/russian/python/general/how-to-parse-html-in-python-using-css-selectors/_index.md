---
category: general
date: 2026-10-21
description: Узнайте, как парсить HTML в Python, загружать HTML‑документ, использовать
  CSS‑селекторы и быстро извлекать гиперссылки из HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- how to use selector
- extract hyperlinks from html
- load html document python
language: ru
lastmod: 2026-10-21
og_description: Как парсить HTML в Python с помощью CSS‑селекторов. Загрузить HTML‑документ,
  выбрать ссылки и извлечь гиперссылки из HTML чистым кодом.
og_image_alt: Screenshot showing how to parse HTML in Python with CSS selectors
og_title: Как парсить HTML в Python – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to parse HTML in Python, load an HTML document, use CSS selectors,
    and extract hyperlinks from HTML quickly.
  headline: How to parse HTML in Python using CSS selectors
  type: TechArticle
tags:
- python
- html-parsing
- css-selectors
title: Как парсить HTML в Python с помощью CSS‑селекторов
url: /ru/python/general/how-to-parse-html-in-python-using-css-selectors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как парсить HTML в Python с помощью CSS‑селекторов

Если вам нужно **парсить HTML** в скрипте Python, это руководство покажет, как это сделать. Вы узнаете, как загрузить HTML‑документ, как использовать синтаксис селекторов для поиска элементов и как извлекать гиперссылки из HTML без написания собственного парсера.

Парсинг HTML — распространённая задача для веб‑скрейперов, конвейеров анализа данных или автоматизированного тестирования. К концу этого урока у вас будет переиспользуемая функция, которая загружает HTML‑документ, выбирает все теги `<a>` с помощью CSS‑селектора и возвращает чистый список URL‑ов.

## Что понадобится

- Python 3.8+ (код работает на любой современной версии)  
- Библиотека **lxml** (`pip install lxml`) — обеспечивает быстрое парсирование HTML и поддержку CSS‑селекторов  
- HTML‑файл, который вы хотите проанализировать (например, `sample.html`)  

Дополнительные инструменты не требуются; всё работает со стандартной библиотекой и одной сторонней зависимостью.

## Шаг 1: Как парсить HTML — загрузка документа

Первый шаг любого рабочего процесса с HTML — чтение файла в память. Использование **lxml.html** даёт вам объект дерева, поддерживающий CSS‑селекторы.

```python
# step_1_load.py
from lxml import html

def load_html(path: str) -> html.HtmlElement:
    """
    Load an HTML document from the given file path.
    Returns an lxml HtmlElement that can be queried with CSS selectors.
    """
    with open(path, "r", encoding="utf-8") as f:
        content = f.read()
    # Parse the raw HTML string into a tree
    return html.fromstring(content)

# Example usage
doc = load_html("sample.html")
print("Document loaded – ready for selector queries.")
```

**Почему это важно:**  
`load_html` абстрагирует boilerplate чтения файла и гарантирует, что документ будет разобран tolerant‑HTML‑парсером. Это самый надёжный способ **загрузить HTML‑документ в Python** без опасений о некорректной разметке.

## Шаг 2: Как использовать селектор — поиск всех ссылок

После загрузки документа вы можете применить CSS‑селектор, чтобы найти каждый тег `<a>`. Селектор `"a"` совпадает со всеми элементами‑якорями, но его можно уточнить (например, `"a.external"` или `"nav a"`).

```python
# step_2_selector.py
def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    """
    Return a list of <a> elements using a CSS selector.
    This demonstrates how to use selector syntax with lxml.
    """
    # The CSS selector "a" selects every anchor tag
    return doc.cssselect("a")

# Example usage
links = select_links(doc)
print(f"Found {len(links)} <a> elements.")
```

**Почему это важно:**  
Подход **как использовать селектор** позволяет выразить сложные запросы одной читаемой строкой, избегая ручного обхода дерева. Он работает с любым CSS‑шаблоном, поддерживаемым `lxml.cssselect`.

## Шаг 3: Извлечение гиперссылок из HTML и их обработка

Теперь, когда у вас есть список элементов `<a>`, можно получить атрибут `href` у каждого из них. Ниже‑приведённый помощник также нормализует относительные URL‑ы относительно базового URL (если вы его укажете).

```python
# step_3_extract.py
from urllib.parse import urljoin
from typing import Optional

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    """
    Return a list of href values from the given <a> elements.
    If base_url is supplied, relative URLs are resolved to absolute URLs.
    """
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            # Skip <a> tags without an href attribute
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

# Example usage
hyperlinks = extract_hyperlinks(links, base_url="https://example.com")
for url in hyperlinks:
    print(url)
```

**Ожидаемый вывод** (при условии, что `sample.html` содержит три ссылки):

```
https://example.com/page1.html
https://example.com/page2.html
https://external.org/resource
```

**Почему это важно:**  
`extract_hyperlinks` — ядро **извлечения гиперссылок из HTML**. Он аккуратно обрабатывает отсутствие атрибута `href`, разрешает относительные ссылки и возвращает обычный список Python, который можно передать в дальнейшую обработку (например, `requests`, `pandas` или базу данных).

## Полный сквозной пример

Объединив три функции, получаем скрипт, который загружает файл, выбирает все якоря и выводит каждую гиперссылку.

```python
# parse_links.py
from lxml import html
from urllib.parse import urljoin
from typing import Optional

def load_html(path: str) -> html.HtmlElement:
    with open(path, "r", encoding="utf-8") as f:
        return html.fromstring(f.read())

def select_links(doc: html.HtmlElement) -> list[html.HtmlElement]:
    return doc.cssselect("a")

def extract_hyperlinks(
    links: list[html.HtmlElement],
    base_url: Optional[str] = None
) -> list[str]:
    hrefs = []
    for link in links:
        href = link.get("href")
        if not href:
            continue
        if base_url:
            href = urljoin(base_url, href)
        hrefs.append(href)
    return hrefs

if __name__ == "__main__":
    # 1️⃣ Load the HTML document
    document = load_html("sample.html")
    # 2️⃣ Use selector to grab all <a> tags
    anchor_elements = select_links(document)
    # 3️⃣ Extract and print each hyperlink
    for url in extract_hyperlinks(anchor_elements, base_url="https://example.com"):
        print(url)
```

Запуск `python parse_links.py` выводит в консоль каждую гиперссылку, полностью разрешённую. Этот скрипт демонстрирует **как парсить HTML**, **как использовать селектор** и **извлекать гиперссылки из HTML** в едином переиспользуемом потоке.

## Распространённые варианты и обработка граничных случаев

| Ситуация | Что изменить | Причина |
|-----------|----------------|--------|
| **Требуются только абсолютные URL** | Не передавать аргумент `base_url` в `extract_hyperlinks` | Оставляет относительные URL без изменений |
| **Нужен также текст ссылки** | Возвращать кортеж `(href, link.text_content())` из `extract_hyperlinks` | Позволяет сохранять и URL, и текст якоря |
| **Большие HTML‑файлы** | Использовать `lxml.etree.iterparse` с фильтром CSS‑селектора | Снижает потребление памяти за счёт потоковой обработки |
| **Другой селектор** | Заменить `"a"` на `"nav a[href]"` или `"div.content a.external"` | Выбирает подмножество ссылок, полезно для **как использовать селектор** на сложных страницах |

**Совет:** Всегда проверяйте извлечённые URL перед выполнением сетевых запросов. Быстрая проверка `urlparse` поможет отфильтровать некорректные строки и защитит ваш скрейпер от сбоев.

## Заключение

Теперь вы знаете, **как парсить HTML** в Python, как **загружать HTML‑документ в Python**, как **использовать селектор** для выбора элементов и как **извлекать гиперссылки из HTML** эффективно. Полный пример выше готов к копированию и вставке в ваш проект, а каждую функцию можно адаптировать под более сложные сценарии, такие как пагинация, контент, генерируемый JavaScript, или многопоточный обход.

Дальнейшие шаги, которые стоит изучить:

- Использовать **requests‑html** или **Playwright** для получения страниц, требующих выполнения JavaScript.  
- Сохранять извлечённые URL в CSV‑файл или базу SQLite для последующего анализа.  
- Добавлять обработку ошибок для таймаутов сети и HTTP‑кодов статуса.

Приятного парсинга, экспериментируйте с разными селекторами, чтобы раскрыть весь потенциал CSS‑ориентированных запросов к HTML в Python!

## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to configure HTML resource handling in Python and load an HTML document](/html/english/python/general/how-to-configure-html-resource-handling-in-python-and-load-a/)
- [How to Parse HTML in Python – Complete Guide](/html/english/python/general/how-to-parse-html-in-python-complete-guide/)
- [How to Load HTML in Python – Step‑by‑Step Guide](/html/english/python/general/how-to-load-html-in-python-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}