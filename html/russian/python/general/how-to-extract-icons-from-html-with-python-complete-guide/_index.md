---
category: general
date: 2026-07-02
description: Как извлечь иконки из HTML‑файла с помощью Python. Научитесь читать HTML‑файл
  в Python, разбирать HTML‑документ и извлекать атрибут href, чтобы получить URL‑адреса
  фавиконов.
draft: false
keywords:
- how to extract icons
- read html file python
- parse html document
- extract href attribute
- extract favicon urls
language: ru
og_description: Как извлечь иконки из HTML‑страницы с помощью Python. Этот учебник
  покажет, как читать HTML‑файл в Python, разбирать документ и извлекать URL‑адреса
  фавиконок.
og_title: Как извлечь иконки из HTML — руководство по Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: How to extract icons from an HTML file using Python. Learn to read
    HTML file python, parse HTML document, and extract href attribute to get favicon
    URLs.
  headline: How to Extract Icons from HTML with Python – Complete Guide
  type: TechArticle
- questions:
  - answer: Some sites embed icons via `<meta itemprop="image">`. Extend `is_icon_link`
      to also check for `meta` with `itemprop="image"` and pull its `content` attribute.
    question: What if the HTML uses `<meta>` tags for icons?
  - answer: Yes—just feed each URL into `requests.get(url, stream=True)` and write
      the content to a file. Remember to handle relative URLs with `urljoin`.
    question: Can I fetch the icons automatically?
  - answer: 'Absolutely. Replace the file‑reading step with `requests.get(page_url).text`
      and pass the HTML string to BeautifulSoup. Just be mindful of robots.txt and
      rate limits. --- ## Wrap‑Up We’ve covered **how to extract icons** from any
      static HTML using Python, from reading the file to printing out each f'
    question: Does this work on remote pages?
  type: FAQPage
tags:
- python
- html-parsing
- web‑scraping
- favicon
title: Как извлечь иконки из HTML с помощью Python — полное руководство
url: /ru/python/general/how-to-extract-icons-from-html-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как извлечь иконки из HTML с помощью Python – Полное руководство

Когда‑нибудь задумывались **как извлечь иконки** со страницы без открытия браузера? Возможно, вы создаёте каталог сайта, инструмент SEO‑аудита или просто интересуетесь крошечными фавиконами, которые появляются во вкладках. Хорошая новость: это можно сделать в несколько строк кода на Python — без Selenium, без headless Chrome, просто из обычного HTML‑файла.

В этом руководстве мы пройдем процесс чтения HTML‑файла python, парсинга HTML‑документа и, наконец, **извлечения атрибута href** из тегов `<link rel="icon">`, чтобы получить URL‑ы фавиконов. К концу вы получите переиспользуемый фрагмент кода, который работает с любой статической HTML‑страницей, а также узнаете, как обрабатывать особые случаи, такие как относительные пути или несколько объявлений иконок.

## Что вы узнаете

- Загрузка локального HTML‑файла с помощью Python (read html file python)  
- Использование лёгкого парсера для **parse html document** безопасно  
- Поиск элементов `<link>`, объявляющих иконку  
- **Extract href attribute** и преобразование их в абсолютные URL‑ы  
- Сбор и вывод всех найденных **favicon URLs**  

Никаких внешних сервисов — только стандартная библиотека и популярный пакет **BeautifulSoup**.

---

![Скриншот, показывающий скрипт Python, извлекающий иконки – how to extract icons](https://example.com/images/extract-icons-python.png "how to extract icons")

*Текст alt изображения: "how to extract icons using a Python script"*

## Предварительные требования

- Python 3.8+ установлен  
- Библиотека `beautifulsoup4` (`pip install beautifulsoup4`)  
- Локальный HTML‑файл, который вы хотите просканировать (например, `sample.html`)  

Если всё уже готово, приступим.

## Шаг 1: Чтение HTML‑файла Python – загрузка документа

Первое, что нужно сделать, — открыть файл и передать его содержимое парсеру. Использование `with open(..., "r", encoding="utf‑8")` гарантирует автоматическое закрытие файла, а кодировка UTF‑8 обрабатывает большинство современных страниц.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Step 1: Load the HTML document from disk
html_path = Path("sample.html")          # adjust the path as needed
html_content = html_path.read_text(encoding="utf-8")
```

**Почему это важно:** Открытие файла с правильной кодировкой предотвращает появление загадочных символов `�`, которые могут сломать парсер позже. Использование `Path` из стандартной библиотеки также делает код кросс‑платформенным.

## Шаг 2: Парсинг HTML‑документа – поиск всех ссылок на иконки

Теперь передаём сырой HTML **BeautifulSoup**, который строит навигационное дерево. Мы будем искать каждый тег `<link>`, у которого атрибут `rel` содержит слово `icon`. Учтите, что `rel` может быть списком, разделённым пробелами (`rel="shortcut icon"`), поэтому нужна гибкая проверка.

```python
# Step 2: Parse the HTML and locate <link> tags that declare an icon
soup = BeautifulSoup(html_content, "html.parser")

def is_icon_link(tag):
    """Return True if a <link> tag declares an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    # BeautifulSoup may return a list or a string; handle both
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

icon_links = [tag for tag in soup.find_all(is_icon_link)]
```

**Почему этот шаг критичен:** Наивный `soup.find_all("link", rel="icon")` пропустит варианты вроде `rel="shortcut icon"` или `rel="apple-touch-icon"`. Наш вспомогательный `is_icon_link` покрывает эти случаи, делая извлечение надёжным.

## Шаг 3: Извлечение атрибута href – получение URL‑ов

Собрав нужные теги, мы извлекаем из каждого атрибут `href`. На некоторых страницах `href` может отсутствовать (редко, но возможно), поэтому проверяем на `None`. Кроме того, фавиконы часто указываются относительными URL‑ами, поэтому мы разрешаем их относительно базового URL страницы, если он известен. Для локального файла оставляем путь как есть.

```python
# Step 3: Grab the href attribute from each icon link
icon_urls = []
for tag in icon_links:
    href = tag.get("href")
    if href:
        icon_urls.append(href.strip())
```

**Почему мы удаляем пробелы:** Авторы HTML иногда случайно добавляют пробелы вокруг URL‑ов, что ломает последующие запросы. Обрезка гарантирует чистые строки.

## Шаг 4: Извлечение URL‑ов фавиконов – вывод результатов

Наконец, выводим (или возвращаем) список найденных URL‑ов. В реальном скрипте их можно записать в CSV, скачать иконки или передать в другой сервис. Ниже простой цикл, который показывает результат в консоли.

```python
# Step 4: Display each discovered favicon URL
if not icon_urls:
    print("No icon links found in the document.")
else:
    for url in icon_urls:
        print("Favicon URL:", url)
```

### Обработка особых случаев

- **Несколько значений rel:** Наш проверочный `is_icon_link` уже ловит `rel="shortcut icon"` и `rel="apple-touch-icon"`.  
- **Относительные пути:** Если позже понадобятся абсолютные URL‑ы, используйте `urllib.parse.urljoin(base_url, href)`.  
- **Отсутствующий href:** Защита `if href:` пропускает некорректные теги, избегая ошибок `NoneType`.  
- **Дублирующиеся записи:** Можно выполнить `icon_urls = list(dict.fromkeys(icon_urls))` для удаления дубликатов.

---

## Полный скрипт – готовое решение

Объединив всё вместе, получаем полностью готовую к запуску программу. Сохраните её как `extract_icons.py` и укажите `html_path` на любой файл.

```python
#!/usr/bin/env python3
"""
How to extract icons from an HTML file using Python.

This script:
- Reads an HTML file (read html file python)
- Parses the HTML document (parse html document)
- Finds <link> tags with rel containing "icon"
- Extracts the href attribute (extract href attribute)
- Prints each favicon URL (extract favicon urls)
"""

from pathlib import Path
from bs4 import BeautifulSoup

def is_icon_link(tag):
    """Detect <link> tags that declare an icon."""
    if tag.name != "link":
        return False
    rel = tag.get("rel")
    if isinstance(rel, list):
        rel = " ".join(rel)
    return rel and "icon" in rel.lower()

def extract_favicon_urls(html_path: Path):
    """Return a list of favicon URLs found in the given HTML file."""
    html_content = html_path.read_text(encoding="utf-8")
    soup = BeautifulSoup(html_content, "html.parser")
    icon_links = [t for t in soup.find_all(is_icon_link)]

    urls = []
    for tag in icon_links:
        href = tag.get("href")
        if href:
            urls.append(href.strip())
    # Remove duplicates while preserving order
    return list(dict.fromkeys(urls))

if __name__ == "__main__":
    # Adjust the path to point to your HTML file
    html_file = Path("sample.html")
    favicon_urls = extract_favicon_urls(html_file)

    if not favicon_urls:
        print("No icon links found in the document.")
    else:
        for url in favicon_urls:
            print("Favicon URL:", url)
```

**Ожидаемый вывод** (при условии, что `sample.html` содержит две иконки):

```
Favicon URL: /images/favicon.ico
Favicon URL: https://example.com/assets/apple-touch-icon.png
```

Запустите её командой `python extract_icons.py`, и вы увидите URL‑ы, выведенные в консоль.

---

## Часто задаваемые вопросы

**В: Что делать, если HTML использует теги `<meta>` для иконок?**  
О: Некоторые сайты встраивают иконки через `<meta itemprop="image">`. Расширьте `is_icon_link`, чтобы также проверять `meta` с `itemprop="image"` и извлекать его атрибут `content`.

**В: Можно ли автоматически скачивать иконки?**  
О: Да — просто передайте каждый URL в `requests.get(url, stream=True)` и запишите содержимое в файл. Не забудьте обрабатывать относительные URL‑ы с помощью `urljoin`.

**В: Работает ли это с удалёнными страницами?**  
О: Конечно. Замените шаг чтения файла на `requests.get(page_url).text` и передайте полученную строку в BeautifulSoup. Только учитывайте robots.txt и ограничения по частоте запросов.

---

## Итоги

Мы рассмотрели **как извлечь иконки** из любой статической HTML‑страницы с помощью Python, от чтения файла до вывода каждого URL‑а фавикона. Основные идеи — чтение файла, парсинг документа, поиск нужных тегов и извлечение атрибута `href` — являются переиспользуемыми шаблонами, встречающимися во многих задачах веб‑скрейпинга.

Что дальше? Попробуйте расширить скрипт, чтобы:

- Преобразовывать относительные URL‑ы в абсолютные относительно базового URL страницы  
- Скачивать каждую иконку и сохранять её локально  
- Поддерживать дополнительные форматы иконок (`rel="mask-icon"` для Safari)  

Экспериментируйте, и если столкнётесь с трудностями, оставляйте комментарий ниже. Приятного парсинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Edit HTML Document Tree in Aspose.HTML for Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Save HTML Document to File in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-html-to-file/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}