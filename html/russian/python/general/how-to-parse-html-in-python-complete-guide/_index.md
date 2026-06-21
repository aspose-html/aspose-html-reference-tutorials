---
category: general
date: 2026-05-28
description: Как быстро парсить HTML в Python — загрузить HTML‑файл, использовать
  CSS‑селектор и извлечь атрибуты href с примером XPath contains.
draft: false
keywords:
- how to parse html
- get href attribute
- load html file
- use css selector
- xpath contains example
language: ru
og_description: 'Как парсить HTML в Python: научитесь загружать HTML‑файл, использовать
  CSS‑селекторы и получать атрибуты href с помощью примера XPath contains.'
og_title: Как парсить HTML в Python — пошагово
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  headline: How to Parse HTML in Python – Complete Guide
  type: TechArticle
- description: How to parse HTML in Python quickly—load HTML file, use CSS selector,
    and extract href attributes with an XPath contains example.
  name: How to Parse HTML in Python – Complete Guide
  steps:
  - name: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
    text: '**Missing `href` attribute** – XPath will still return the `<a>` node even
      if `href` is absent. Guard against `None`:'
  - name: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
    text: '**Relative vs. absolute URLs** – If your links are relative, you may want
      to resolve them against the base URL:'
  - name: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
    text: '**Malformed HTML** – `lxml` is forgiving, but extremely broken markup can
      cause `html.parse` to raise an `XMLSyntaxError`. Wrap the parse call in a `try/except`
      block to log and skip problematic files.'
  - name: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
    text: '**Performance with large files** – For multi‑megabyte pages, consider streaming
      with `iterparse` instead of loading the whole DOM into memory.'
  type: HowTo
tags:
- html parsing
- python
- web scraping
title: Как парсить HTML в Python — Полное руководство
url: /ru/python/general/how-to-parse-html-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как парсить HTML в Python – Полное руководство

Когда‑то задавались вопросом, **как парсить HTML** в скрипте Python без тяжёлого браузера? Вы не одиноки. Большинству из нас достаточно **загрузить HTML‑файл**, собрать несколько заголовков и, возможно, вытащить пару ссылок для скачивания. В этом руководстве я покажу именно это — используя крошечную библиотеку, CSS‑селектор и пример XPath contains для **получения значений атрибута href**.

Мы пройдём весь процесс, от чтения локального HTML‑документа до вывода нужных данных. Без лишних слов, только практический, готовый к запуску пример, который вы можете сразу вставить в свой проект.

## Что вы узнаете

- Как **загрузить HTML‑файл** с помощью лёгкого парсера.  
- Как **использовать синтаксис CSS‑селекторов** для получения элементов, например заголовков статей.  
- Как создать **пример XPath contains**, который фильтрует ссылки.  
- Как безопасно **получать значения атрибута href** из найденных узлов.  
- Советы по работе с некорректной разметкой и расширению скрипта.

Вам понадобится только Python 3.8+ и пакеты `lxml` и `cssselect` — их можно установить одной командой `pip`.

---

## Шаг 1: Загрузка HTML‑файла

Прежде чем что‑то делать, нужно загрузить содержимое HTML в память. Модуль `lxml.html` предоставляет удобный помощник `fromstring`, но когда у вас есть файл на диске, функция `parse` выглядит ещё проще.

```python
# Step 1: Load the HTML file
from lxml import html

# Replace the path with the location of your HTML document
html_path = "YOUR_DIRECTORY/news.html"
doc = html.parse(html_path)

# The root element gives us access to CSS and XPath methods
root = doc.getroot()
```

> **Почему это важно:** Загрузка файла один раз снижает потребление памяти и даёт вам единый объект `root`, поддерживающий как CSS‑селекторы, так и XPath‑запросы. Если файл отсутствует или недоступен, `html.parse` выбросит понятный `OSError`, который можно перехватить позже.

### Pro tip
Если вы работаете со строкой, а не с файлом, замените `html.parse` на `html.fromstring(your_html_string)`.

---

## Шаг 2: Используем CSS‑селектор для получения заголовков

CSS‑селекторы лаконичны и знакомы каждому, кто писал стили. Давайте получим каждый `<h2>` внутри `<article>` — идеально подходит для новостных заголовков.

```python
# Step 2: Find all article headlines using a CSS selector
headline_nodes = root.cssselect("article h2")

# Print each headline's text content
for node in headline_nodes:
    print(node.text_content().strip())
```

**Ожидаемый вывод** (при условии, что пример HTML содержит две статьи):

```
Breaking News: Python Takes Over the World
Local Developer Solves HTML Parsing Puzzle
```

> **Почему CSS?** Он читаем, быстр и работает «из коробки» с `lxml`. Метод `cssselect` под капотом переводит селектор в XPath‑выражение, давая вам лучшее из обоих миров.

---

## Шаг 3: Пример XPath contains – поиск ссылок «download»

Иногда требуется более тонкий контроль, чем может предложить CSS. Функция XPath `contains()` блестяще подходит, когда нужно найти подстроку в атрибуте, например все ссылки, указывающие на скачивание.

```python
# Step 3: Find all links that contain the word "download" using XPath
download_link_nodes = root.xpath("//a[contains(@href, 'download')]")

# Extract and print the href attribute from each matching node
for node in download_link_nodes:
    href = node.get("href")
    print(href)
```

**Пример вывода**:

```
/files/report_download.pdf
https://example.com/downloads/setup.exe
```

> **Почему XPath contains?** Он позволяет фильтровать сразу по значениям атрибутов без дополнительных циклов Python. Это классический **xpath contains example**, часто встречающийся в руководствах, но здесь он соединён с реальным кейсом.

---

## Шаг 4: Объединяем всё в переиспользуемую функцию

Хард‑кодить пути и `print`‑ы удобно для быстрого теста, но в продакшене лучше использовать функции. Ниже — компактный помощник, который возвращает и заголовки, и ссылки для скачивания.

```python
def parse_news_html(file_path):
    """
    Parse a news HTML file and return headlines plus download URLs.

    Parameters
    ----------
    file_path : str
        Path to the local HTML document.

    Returns
    -------
    dict
        {
            "headlines": list of strings,
            "download_links": list of href strings
        }
    """
    doc = html.parse(file_path)
    root = doc.getroot()

    # Headlines via CSS selector
    headlines = [
        node.text_content().strip()
        for node in root.cssselect("article h2")
    ]

    # Download links via XPath contains
    download_links = [
        node.get("href")
        for node in root.xpath("//a[contains(@href, 'download')]")
    ]

    return {"headlines": headlines, "download_links": download_links}
```

Теперь вы можете вызвать функцию и красиво вывести результаты:

```python
if __name__ == "__main__":
    results = parse_news_html("YOUR_DIRECTORY/news.html")
    print("Headlines:")
    for h in results["headlines"]:
        print(f"- {h}")

    print("\nDownload Links:")
    for link in results["download_links"]:
        print(f"- {link}")
```

Запуск скрипта даст тот же вывод, что и раньше, но теперь всё упаковано для повторного использования.

---

## Шаг 5: Обработка граничных случаев и типичных подводных камней

1. **Отсутствующий атрибут `href`** – XPath всё равно вернёт узел `<a>`, даже если `href` нет. Защищайтесь от `None`:

   ```python
   href = node.get("href")
   if href:
       download_links.append(href)
   ```

2. **Относительные vs. абсолютные URL** – Если ссылки относительные, их стоит преобразовать к полным, используя базовый URL:

   ```python
   from urllib.parse import urljoin
   base_url = "https://example.com"
   absolute = urljoin(base_url, href)
   ```

3. **Некорректный HTML** – `lxml` прощает многое, но сильно сломанная разметка может вызвать `XMLSyntaxError` при `html.parse`. Оберните вызов парсинга в `try/except`, чтобы логировать и пропускать проблемные файлы.

4. **Производительность при больших файлах** – Для страниц в несколько мегабайт лучше использовать потоковый парсинг через `iterparse`, а не загружать весь DOM в память.

---

## Визуальный обзор (по желанию)

![Как выглядит процесс парсинга HTML: загрузка файла → CSS‑селектор → XPath contains → получение атрибута href](how-to-parse-html-flow.png "Диаграмма процесса парсинга HTML")

*Alt‑текст включает основной ключевой запрос для SEO.*

---

## Заключение

Мы рассмотрели **как парсить HTML** в Python от начала до конца: загрузка HTML‑файла, использование CSS‑селектора для извлечения заголовков статей, создание примера XPath contains для поиска ссылок на скачивание и безопасное **получение атрибута href**. Переиспользуемая функция `parse_news_html` демонстрирует чистый, поддерживаемый подход, который можно адаптировать под любую задачу скрейпинга.

Готовы к следующему вызову? Попробуйте расширить скрипт, чтобы:

- Парсить таблицы с помощью XPath‑запросов `//table//tr`.  
- Извлекать атрибуты `src` изображений, используя ещё один **xpath contains example**.  
- Перейти к асинхронному получению страниц с `aiohttp` для живых веб‑страниц.

Приятного парсинга, и помните — освоив эти основы, остальное будет проще простого. Если возникнут проблемы, оставляйте комментарий ниже — разберём вместе!

## Связанные руководства

- [Load HTML Documents from File in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [How to Add CSS – Inline CSS to HTML Documents in Aspose.HTML for Java](/html/english/java/editing-html-documents/add-inline-css-html-documents/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}