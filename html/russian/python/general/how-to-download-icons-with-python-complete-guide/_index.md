---
category: general
date: 2026-05-31
description: Узнайте, как загружать иконки с помощью Python. Мы также расскажем, как
  извлекать favicon, читать HTML‑документы в Python и записывать бинарные файлы в
  Python в одном учебнике.
draft: false
keywords:
- how to download icons
- how to extract favicon
- write binary file python
- read html document python
- load html python
language: ru
og_description: 'Как скачивать иконки с помощью Python: пошаговое руководство. Научитесь
  извлекать favicon, читать HTML‑документ в Python и записывать бинарный файл в Python.'
og_title: Как скачать иконки с помощью Python — Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to download icons using Python. We'll also cover how to extract
    favicon, read HTML document Python, and write binary file python in a single tutorial.
  headline: How to Download Icons with Python – Complete Guide
  type: TechArticle
tags:
- python
- web-scraping
- favicon
- file-io
title: Как скачать иконки с помощью Python — Полное руководство
url: /ru/python/general/how-to-download-icons-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как скачать иконки с помощью Python – Полное руководство

Когда‑то задавались вопросом **как скачать иконки** с сайта без ручного клика правой кнопкой мыши по каждой? Вы не одиноки. Будь то создание инструмента аудита бренда или просто желание иметь локальную копию каждого favicon, с которым вы сталкиваетесь, освоение этой задачи экономит время и усилия.

В этом руководстве мы пройдемся по **как скачать иконки** из HTML‑файла, используя чистый Python. Мы также покажем, **как извлечь favicon**, продемонстрируем **read html document python**, и объясним **write binary file python**, чтобы в итоге у вас получилась аккуратная папка с .ico‑файлами, готовыми к использованию в любом проекте.

---

## Что вам понадобится

- Python 3.8+ (достаточно стандартной библиотеки)
- Локальная копия HTML‑страницы, которую нужно просканировать (или URL, который можно получить)
- Базовое знакомство с вводом‑выводом файлов в Python  
- Внешних пакетов не требуется, но `beautifulsoup4` может упростить работу, если хотите (по желанию)

Все готово? Отлично — приступаем.

![Как скачать иконки пример](https://example.com/placeholder.png "как скачать иконки пример")

---

## Шаг 1: Загрузить HTML‑документ в Python  

Прежде всего, нам нужно **load html python**‑стилем — прочитать файл в память, чтобы проанализировать его теги `<link>`. Самый простой способ — открыть файл встроенной функцией `open` и считать его как текст.

```python
# Step 1: Load the HTML document
HTML_PATH = "YOUR_DIRECTORY/sample.html"

# Using the built‑in open() to read the file as a string
with open(HTML_PATH, "r", encoding="utf-8") as f:
    html_content = f.read()
```

*Зачем этот шаг?*  
Чтение HTML даёт нам сырую строку, которую можно парсить. Если пропустить этот шаг и попытаться работать напрямую с путём, парсер не получит данных для анализа.

---

## Шаг 2: Разобрать документ и найти ссылки на иконки  

Теперь нам нужно **read html document python**‑стилем. Хотя можно использовать регулярные выражения, небольшой HTML‑парсер обеспечивает надёжность. В Python есть `html.parser`, который мы можем унаследовать для нашей задачи.

```python
from html.parser import HTMLParser

class IconLinkParser(HTMLParser):
    """Collects href attributes from <link rel='icon'> tags."""
    def __init__(self):
        super().__init__()
        self.icon_hrefs = []

    def handle_starttag(self, tag, attrs):
        if tag.lower() != "link":
            return
        attrs_dict = dict(attrs)
        # Look for rel="icon" (or rel="shortcut icon")
        rel = attrs_dict.get("rel", "").lower()
        if "icon" in rel:
            href = attrs_dict.get("href")
            if href:
                self.icon_hrefs.append(href)

# Instantiate and feed the HTML content
parser = IconLinkParser()
parser.feed(html_content)

# Now we have a list of all icon URLs
icon_hrefs = parser.icon_hrefs
print(f"Found {len(icon_hrefs)} icon link(s):", icon_hrefs)
```

**Объяснение**  
- `handle_starttag` вызывается для каждого открывающего тега.  
- Мы отфильтровываем элементы `<link>`, у которых атрибут `rel` содержит слово *icon*. Это охватывает как `rel="icon"`, так и старый `rel="shortcut icon"`.  
- Значения `href` сохраняются в `icon_hrefs`, готовые к следующему шагу.

---

## Шаг 3: Преобразовать относительные пути (по желанию, но полезно)

Если в HTML используются относительные URL, их нужно превратить в абсолютные пути файловой системы. Здесь **load html python** встречается с `urllib.parse`.

```python
import os
from urllib.parse import urljoin

# Base directory where the HTML file lives
BASE_DIR = os.path.dirname(os.path.abspath(HTML_PATH))

def resolve_path(href):
    # If href already looks like an absolute path, return it unchanged
    if os.path.isabs(href):
        return href
    # Otherwise, join it with the base directory
    return os.path.normpath(os.path.join(BASE_DIR, href))

resolved_icon_paths = [resolve_path(h) for h in icon_hrefs]
print("Resolved paths:", resolved_icon_paths)
```

*Зачем это нужно?*  
Когда позже вы будете **write binary file python**, понадобится реальный путь к файлу. Относительные URL вроде `images/favicon.ico` иначе вызовут `FileNotFoundError`.

---

## Шаг 4: Записать каждую иконку в локальный бинарный файл  

Это сердце **how to download icons**. Мы пройдемся по найденным путям, прочитаем каждую иконку как бинарные данные и запишем её в новый файл в отдельной папке `icons/`.

```python
import shutil

OUTPUT_DIR = "YOUR_DIRECTORY/icons"
os.makedirs(OUTPUT_DIR, exist_ok=True)

for index, icon_path in enumerate(resolved_icon_paths):
    # Guard against missing files
    if not os.path.isfile(icon_path):
        print(f"⚠️  Icon file not found: {icon_path}")
        continue

    # Destination filename: icon_0.ico, icon_1.ico, …
    dest_path = os.path.join(OUTPUT_DIR, f"icon_{index}.ico")

    # **write binary file python** – copy the binary data
    with open(icon_path, "rb") as src_file, open(dest_path, "wb") as dst_file:
        shutil.copyfileobj(src_file, dst_file)

    print(f"✅ Saved {dest_path}")
```

**Что происходит?**  

- `os.makedirs(..., exist_ok=True)` гарантирует, что папка вывода существует.  
- `shutil.copyfileobj` передаёт байты от источника к назначению, что является самым экономичным способом **write binary file python**.  
- Мы именуем каждый файл `icon_<index>.ico`, чтобы избежать конфликтов.

**Ожидаемый вывод**

```
Found 2 icon link(s): ['images/favicon.ico', 'icons/custom.ico']
Resolved paths: ['/path/to/YOUR_DIRECTORY/images/favicon.ico',
                '/path/to/YOUR_DIRECTORY/icons/custom.ico']
✅ Saved YOUR_DIRECTORY/icons/icon_0.ico
✅ Saved YOUR_DIRECTORY/icons/icon_1.ico
```

После завершения скрипта у вас будет чистая коллекция файлов‑иконок, готовая к использованию в любых последующих задачах.

---

## Шаг 5: Бонус — скачивание иконок напрямую из удалённого URL  

Если ваш HTML находится в сети, замените часть чтения файла небольшим вызовом `requests`. Это демонстрирует **how to extract favicon** с любой живой страницы.

```python
import requests

REMOTE_URL = "https://example.com"

# Grab the HTML
response = requests.get(REMOTE_URL)
response.raise_for_status()
html_content = response.text

# Re‑run the parser (same as before) to get icon URLs
parser = IconLinkParser()
parser.feed(html_content)
icon_hrefs = parser.icon_hrefs

# Download each icon via HTTP
for index, href in enumerate(icon_hrefs):
    # Resolve relative URLs against the page URL
    icon_url = urljoin(REMOTE_URL, href)
    r = requests.get(icon_url, stream=True)
    r.raise_for_status()
    dest_path = os.path.join(OUTPUT_DIR, f"remote_icon_{index}.ico")
    with open(dest_path, "wb") as out_file:
        shutil.copyfileobj(r.raw, out_file)
    print(f"✅ Downloaded {icon_url} → {dest_path}")
```

**Зачем это нужно?**  
Многие реальные проекты требуют извлекать фавиконы с живых сайтов. Этот фрагмент показывает, как расширить логику **how to download icons** для работы в интернете, добавив всего пару строк.

---

## Распространённые подводные камни и профессиональные советы

- **Отсутствует `rel="icon"`** — Некоторые сайты внедряют иконки через теги `<meta>` или CSS. Если нужны такие, расширьте парсер, чтобы искать `<meta name="msapplication‑TileImage">` или URL‑ы в `background-image`.  
- **Форматы, отличные от ICO** — Современные фавиконы часто используют `.png` или `.svg`. Приведённый код работает с любым бинарным изображением; просто скорректируйте расширение в `dest_path`, если хотите сохранять оригинальный формат.  
- **Ошибки доступа** — При записи файлов убедитесь, что скрипт имеет права записи в целевую папку. Использование `os.makedirs(..., exist_ok=True)` избавляет от сбоев «каталог не найден».  
- **Большие HTML‑файлы** — Для огромных страниц рассмотрите построчное чтение вместо загрузки всей строки в память. Встроенный `HTMLParser` умеет обрабатывать поступающие данные по частям.  

---

## Заключение

Вы только что узнали **how to download icons** из HTML‑документа с помощью чистого Python. Путём **reading html document python**, парсинга тегов `<link rel="icon">`, преобразования относительных путей и окончательного **write binary file python** для локального сохранения каждой иконки, вы получили переиспользуемый скрипт, работающий как с локальными, так и с удалёнными страницами.  

Что дальше? Попробуйте расширить парсер, чтобы захватывать Apple touch icons (`rel="apple-touch-icon"`), или интегрировать скрипт в более крупный пайплайн веб‑сканирования, собирающий фавиконы для сотен доменов. Основы, рассмотренные здесь — парсинг HTML, разрешение путей и работа с бинарными файлами — являются строительными блоками для множества задач веб‑автоматизации.

Есть вопросы или хотите поделиться интересным кейсом? Оставляйте комментарий ниже, и удачной охоты за иконками!

## Что изучать дальше?

- [Как редактировать дерево HTML‑документа в Aspose.HTML для Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Как конвертировать HTML в PDF на Java – используя Aspose.HTML для Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Как конвертировать HTML в JPEG с помощью Aspose.HTML для Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}