---
category: general
date: 2026-07-18
description: Быстро преобразуйте HTML в EPUB на Python. Узнайте, как загрузить HTML‑файл
  в Python и также конвертировать HTML в MHTML с помощью простых библиотек.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to epub
- load html file in python
- convert html to mhtml
language: ru
lastmod: 2026-07-18
og_description: Конвертируйте HTML в EPUB на Python с понятным, готовым к запуску
  примером. Также узнайте, как загрузить HTML‑файл в Python и за несколько минут преобразовать
  HTML в MHTML.
og_image_alt: Diagram showing convert html to epub workflow
og_title: Преобразовать HTML в EPUB на Python – Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  headline: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Convert HTML to EPUB in Python quickly. Learn how to load HTML file
    in Python and also convert HTML to MHTML using simple libraries.
  name: Convert HTML to EPUB in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Python 3.9+** – the syntax used here works on any recent version.'
    text: '**Python 3.9+** – the syntax used here works on any recent version.'
  - name: '**pip** – to install third‑party packages.'
    text: '**pip** – to install third‑party packages.'
  - name: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
    text: A simple HTML file, e.g., `sample.html`, placed in a folder you control.
  type: HowTo
tags:
- python
- html
- epub
- mhtml
- file conversion
title: Преобразовать HTML в EPUB с помощью Python — Полное пошаговое руководство
url: /ru/python/general/convert-html-to-epub-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в EPUB на Python – Полное пошаговое руководство

Ever wondered how to **конвертировать HTML в EPUB** without pulling your hair out? You're not the only one—developers constantly need to turn web pages into e‑books for offline reading, and doing it in Python is surprisingly painless. In this tutorial we'll walk through loading an HTML file in Python, converting that HTML to EPUB, and even turning the same source into MHTML for email‑friendly archives.

By the end of the guide you'll have a ready‑to‑run script that takes a single `sample.html` file and spits out both `sample.epub` and `sample.mhtml`. No mystery, just clear code and explanations.

---

![Conversion pipeline diagram](https://example.com/images/convert-html-epub.png "Diagram showing convert html to epub workflow")

## Что вы создадите

- **Загрузить HTML‑файл в Python** с помощью встроенных модулей `pathlib` и `io`.  
- **Конвертировать HTML в EPUB** с помощью библиотеки `ebooklib`, которая обрабатывает формат контейнера EPUB за вас.  
- **Конвертировать HTML в MHTML** (также известный как MHT) с использованием пакета `email`, создавая одностраничный веб‑архив, который браузеры могут открыть напрямую.  

Мы также рассмотрим:

- Необходимые зависимости и способы их установки.  
- Обработку ошибок, чтобы ваш скрипт завершался корректно.  
- Как настроить метаданные, такие как название и автор, для EPUB‑файла.  

Готовы? Погрузимся.

---

## Предварительные требования

Прежде чем начать писать код, убедитесь, что у вас есть:

1. **Python 3.9+** – синтаксис, используемый здесь, работает в любой современной версии.  
2. **pip** – для установки сторонних пакетов.  
3. Простой HTML‑файл, например `sample.html`, размещённый в папке, которой вы управляете.  

Если у вас уже есть всё это, отлично — переходите к следующему разделу.  

> **Pro tip:** Держите ваш HTML правильно сформированным (корректные секции `<head>` и `<body>`). Хотя `ebooklib` попытается исправить небольшие проблемы, чистый исходный код сэкономит вам головную боль позже.

## Шаг 1 – Установите необходимые библиотеки

Нам нужны два внешних пакета:

- **ebooklib** – для генерации EPUB.  
- **beautifulsoup4** – опционально, но удобно для очистки HTML перед конвертацией.

Run this in your terminal:

```bash
pip install ebooklib beautifulsoup4
```

> **Why these libraries?** `ebooklib` создает ZIP‑основанную структуру EPUB за вас, автоматически обрабатывая папку `META‑INF`, файлы `content.opf` и `toc.ncx`. `beautifulsoup4` позволяет нам привести HTML в порядок, гарантируя корректное отображение конечной электронной книги на всех ридерах.

## Шаг 2 – Загрузите HTML‑файл в Python

Загрузка HTML‑файла проста, но мы обернём её в небольшую вспомогательную функцию, которая возвращает объект **BeautifulSoup** для дальнейшей обработки.

```python
from pathlib import Path
from bs4 import BeautifulSoup

def load_html(filepath: str) -> BeautifulSoup:
    """
    Load an HTML file from disk and return a BeautifulSoup object.
    Raises FileNotFoundError if the file does not exist.
    """
    path = Path(filepath)
    if not path.is_file():
        raise FileNotFoundError(f"HTML file not found: {filepath}")

    # Read the file using UTF‑8 encoding (most common for web content)
    html_content = path.read_text(encoding="utf-8")
    # Parse with BeautifulSoup for optional cleaning later
    soup = BeautifulSoup(html_content, "html.parser")
    return soup
```

**Объяснение:**  
- `Path` предоставляет независимую от ОС работу с файлами.  
- Использование `read_text` избавляет от ручного шаблона `open`/`close`.  
- Возврат объекта `BeautifulSoup` позволяет позже удалить скрипты, исправить сломанные теги или внедрить таблицу стилей перед тем, как **конвертировать HTML в EPUB**.

## Шаг 3 – Конвертировать HTML в EPUB

Теперь, когда мы можем **загрузить HTML‑файл в Python**, давайте преобразуем его в чистый EPUB. Функция ниже принимает объект `BeautifulSoup`, путь назначения и необязательные метаданные.

```python
import uuid
from ebooklib import epub

def html_to_epub(soup: BeautifulSoup,
                 output_path: str,
                 title: str = "Untitled Book",
                 author: str = "Anonymous") -> None:
    """
    Convert a BeautifulSoup HTML document to an EPUB file.
    """
    # Create a new EPUB book instance
    book = epub.EpubBook()

    # Set basic metadata – this is what shows up in e‑reader libraries
    book.set_identifier(str(uuid.uuid4()))
    book.set_title(title)
    book.set_language('en')
    book.add_author(author)

    # Convert the soup back to a string; we could also clean it here
    html_str = str(soup)

    # Create a chapter (EPUB requires at least one)
    chapter = epub.EpubHtml(title=title,
                            file_name='chap_01.xhtml',
                            lang='en')
    chapter.content = html_str
    book.add_item(chapter)

    # Define the spine (reading order) and table of contents
    book.toc = (epub.Link('chap_01.xhtml', title, 'intro'),)
    book.spine = ['nav', chapter]

    # Add default navigation files
    book.add_item(epub.EpubNcx())
    book.add_item(epub.EpubNav())

    # Write the final EPUB file
    epub.write_epub(output_path, book, {})

    print(f"✅ EPUB created at: {output_path}")
```

**Почему это работает:**  
- `ebooklib.epub.EpubBook` абстрагирует ZIP‑контейнер и необходимые файлы манифеста.  
- Мы генерируем UUID в качестве идентификатора, чтобы избежать дублирования ID при создании множества книг.  
- `spine` указывает читателям порядок глав; одноглавная книга достаточно для большинства простых HTML‑источников.

**Запуск конвертации:**

```python
if __name__ == "__main__":
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_epub(html_doc,
                 "YOUR_DIRECTORY/sample.epub",
                 title="My Sample eBook",
                 author="Jane Developer")
```

Когда вы выполните скрипт, вы увидите зелёную галочку, подтверждающую расположение файла EPUB.

## Шаг 4 – Конвертировать HTML в MHTML

MHTML (или MHT) упаковывает HTML и все его ресурсы (изображения, CSS) в один MIME‑файл. Пакет `email` в Python может создавать этот формат без внешних зависимостей.

```python
import mimetypes
import base64
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.base import MIMEBase
from email import encoders

def html_to_mhtml(soup: BeautifulSoup,
                  output_path: str,
                  base_url: str = "") -> None:
    """
    Convert a BeautifulSoup HTML document to an MHTML file.
    `base_url` is used to resolve relative resource links.
    """
    # Create the multipart/related container required for MHTML
    mhtml = MIMEMultipart('related')
    mhtml['Subject'] = 'Converted MHTML document'
    mhtml['Content-Type'] = 'multipart/related; type="text/html"'

    # Main HTML part
    html_part = MIMEText(str(soup), 'html', 'utf-8')
    html_part.add_header('Content-Location', 'file://index.html')
    mhtml.attach(html_part)

    # Optional: embed images referenced in the HTML
    for img in soup.find_all('img'):
        src = img.get('src')
        if not src:
            continue

        # Resolve absolute path if needed
        img_path = Path(base_url) / src if base_url else Path(src)
        if not img_path.is_file():
            continue  # skip missing files

        # Guess MIME type; default to octet-stream
        mime_type, _ = mimetypes.guess_type(img_path)
        mime_type = mime_type or 'application/octet-stream'

        with img_path.open('rb') as f:
            img_data = f.read()

        img_part = MIMEBase(*mime_type.split('/'))
        img_part.set_payload(img_data)
        encoders.encode_base64(img_part)
        img_part.add_header('Content-Location', f'file://{src}')
        img_part.add_header('Content-Transfer-Encoding', 'base64')
        mhtml.attach(img_part)

    # Write the MHTML file
    with open(output_path, 'wb') as out_file:
        out_file.write(mhtml.as_bytes())

    print(f"✅ MHTML created at: {output_path}")
```

**Ключевые моменты:**  

- MIME‑тип `multipart/related` сообщает браузерам, что HTML‑часть и её ресурсы принадлежат вместе.  
- Мы проходим по тегам `<img>`, чтобы внедрить изображения; если изображения не нужны, можно пропустить этот блок.  
- `Content-Location` использует URI `file://`, чтобы браузеры могли разрешать ресурсы внутри.  

**Вызов функции:**

```python
if __name__ == "__main__":
    # Re‑use the previously loaded soup
    html_doc = load_html("YOUR_DIRECTORY/sample.html")
    html_to_mhtml(html_doc, "YOUR_DIRECTORY/sample.mhtml", base_url="YOUR_DIRECTORY")
```

Теперь у вас есть как `sample.epub`, так и `sample.mhtml`, расположенные рядом.

## Полный скрипт – все шаги в одном файле

Ниже приведён полный готовый к запуску скрипт, объединяющий всё. Сохраните его как `convert_html.py` и замените `YOUR_DIRECTORY` на путь, где находится ваш `sample.html`.

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
convert_html.py

A tiny utility that demonstrates:
- How to load an HTML file in Python
- How to convert HTML to EPUB (convert html to epub)
- How to convert HTML to MHTML (convert html to mhtml)

Author: Your Name
Date: 2026‑07‑18
"""

from pathlib import Path
import uuid
import mimetypes


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Convert EPUB to PDF with Java – Using Aspose.HTML](/html/english/java/converting-epub-to-pdf/convert-epub-to-pdf/)
- [How to Convert EPUB to Images with Aspose.HTML for Java](/html/english/java/conversion-epub-to-image-and-pdf/convert-epub-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}