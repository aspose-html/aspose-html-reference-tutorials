---
category: general
date: 2026-08-06
description: Конвертировать HTML в PDF на Python с полным примером. Узнайте, как генерировать
  PDF из HTML, сохранять HTML как PDF и обрабатывать типичные граничные случаи.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to pdf
- generate pdf from html
- save html as pdf
- create pdf from html file
- how to convert html to pdf
language: ru
lastmod: 2026-08-06
og_description: Преобразуйте HTML в PDF с помощью Python и автоматизируйте создание
  документов. Следуйте этому руководству, чтобы генерировать PDF из HTML, сохранять
  HTML как PDF и настраивать вывод.
og_image_alt: Example of convert html to pdf script in Python
og_title: Преобразование HTML в PDF в Python – подробный учебник
schemas:
- author: Aspose
  dateModified: '2026-08-06'
  description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  headline: Convert HTML to PDF in Python – step‑by‑step guide
  type: TechArticle
- description: Convert HTML to PDF in Python with a complete example. Learn to generate
    PDF from HTML, save HTML as PDF, and handle common edge cases.
  name: Convert HTML to PDF in Python – step‑by‑step guide
  steps:
  - name: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
    text: '**Preparation** – install the converter and ensure the `wkhtmltopdf` binary
      is reachable.'
  - name: '**Input handling** – read the HTML file or build the markup programmatically.'
    text: '**Input handling** – read the HTML file or build the markup programmatically.'
  - name: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
    text: '**Output generation** – invoke the converter, write the PDF file, and confirm
      the result.'
  type: HowTo
tags:
- HTML to PDF
- Python
- Document conversion
title: Конвертировать HTML в PDF в Python — пошаговое руководство
url: /ru/python/general/convert-html-to-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в PDF на Python – пошаговое руководство

Если вам нужно **быстро преобразовать HTML в PDF**, это руководство показывает полное решение на Python. Вы увидите, как генерировать PDF из HTML, сохранять HTML как PDF и управлять процессом конвертации, не покидая ваш код.

В руководстве рассматривается установка надёжной библиотеки, загрузка HTML‑документа, выполнение конвертации и проверка результата. К концу вы сможете создавать PDF из HTML‑файла в любом Python‑проекте, независимо от того, статическая это страница или динамически генерируемая разметка.

## Что вы узнаете

* Установите зависимости `pdfkit` и `wkhtmltopdf`, необходимые для конвертации HTML‑в‑PDF.  
* Загрузите HTML‑документ с диска или из строки.  
* Сгенерируйте PDF из HTML с пользовательскими параметрами размера страницы, полей и кодировки.  
* Сохраните HTML как PDF одним вызовом функции.  
* Обработайте типичные крайние случаи, такие как отсутствие ресурсов, Unicode‑символы и большие файлы.  

**Предварительные требования** – Python 3.8+ и базовое знакомство с вводом‑выводом файлов. Внешние сервисы не требуются.

## Преобразование HTML в PDF – общая схема работы

Процесс конвертации состоит из трёх логических фаз:

1. **Подготовка** – установить конвертер и убедиться, что бинарный файл `wkhtmltopdf` доступен.  
2. **Обработка входных данных** – прочитать HTML‑файл или построить разметку программно.  
3. **Генерация вывода** – вызвать конвертер, записать PDF‑файл и подтвердить результат.

Каждая фаза подробно описана в соответствующем шаге ниже.

## Шаг 1: Установите необходимые библиотеки

`pdfkit` предоставляет лёгкую оболочку Python вокруг широко используемого движка `wkhtmltopdf`. Установите оба пакета с помощью `pip` и проверьте путь к бинарному файлу.

```bash
# Install the Python wrapper
pip install pdfkit

# On Ubuntu/Debian install wkhtmltopdf package
sudo apt-get install wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf
```

Если вы предпочитаете портативный бинарный файл, скачайте соответствующий релиз со [страницы wkhtmltopdf на GitHub](https://github.com/wkhtmltopdf/wkhtmltopdf/releases) и разместите его в каталоге, который добавлен в ваш `PATH`. Скрипт позже проверит путь автоматически.

## Шаг 2: Загрузите HTML‑документ

Вы можете прочитать статический файл, получить удалённый контент или построить HTML «на лету». Пример ниже загружает локальный файл `sample.html`, расположенный в указанном вами каталоге.

```python
import pathlib
import pdfkit

# Define the directory that holds the HTML source
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")

# Resolve the full path to the HTML file
html_path = BASE_DIR / "sample.html"

# Read the file content as a UTF‑8 string
with html_path.open(encoding="utf-8") as f:
    html_content = f.read()
```

Чтение файла как строки Unicode гарантирует, что такие символы, как «é», «ß» или азиатские глифы, сохранятся при конвертации. Этот шаг необходим, когда вы **генерируете PDF из HTML**, содержащего международный текст.

## Шаг 3: Сгенерируйте PDF из HTML

`pdfkit.from_string` преобразует строку, содержащую HTML‑разметку, в PDF‑файл. Вы можете передать словарь параметров для управления размером страницы, полями и поведением заголовков/подвалов.

```python
# Define the output PDF path
pdf_path = BASE_DIR / "sample.pdf"

# Conversion options – adjust as needed
options = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left": "0.75in",
    "encoding": "UTF-8",
    "enable-local-file-access": None,  # Allows loading local images/CSS
}

# Perform the conversion
pdfkit.from_string(html_content, str(pdf_path), options=options)
```

Вызов выше **создаёт PDF из HTML‑файла**, сохранённого как `sample.pdf`. Если исходный HTML ссылается на локальные CSS или изображения, флаг `enable‑local‑file‑access` позволяет `wkhtmltopdf` находить эти ресурсы.

### Почему этот подход работает

* `pdfkit` делегирует тяжёлую работу `wkhtmltopdf`, который рендерит HTML с помощью движка WebKit, обеспечивая высокую точность оригинального макета.  
* Передача словаря параметров позволяет точно настроить вывод без изменения самого HTML.  
* Использование `from_string` сохраняет весь процесс в памяти, что удобно, когда HTML генерируется «на лету».

## Шаг 4: Сохраните HTML как PDF и проверьте результат

После конвертации вы, возможно, захотите убедиться, что PDF существует и читаем. Ниже приведён фрагмент, проверяющий размер файла и открывающий PDF в стандартном просмотрщике системы (зависит от платформы).

```python
import os
import subprocess
import sys

# Verify that the PDF file was created
if pdf_path.is_file() and pdf_path.stat().st_size > 0:
    print(f"✅ PDF generated successfully: {pdf_path}")

    # Open the PDF for visual verification (optional)
    if sys.platform.startswith("darwin"):      # macOS
        subprocess.run(["open", str(pdf_path)])
    elif os.name == "nt":                      # Windows
        os.startfile(str(pdf_path))
    else:                                      # Linux and others
        subprocess.run(["xdg-open", str(pdf_path)])
else:
    raise FileNotFoundError("PDF generation failed – file not found or empty.")
```

Запуск скрипта выводит сообщение об успехе и открывает просмотрщик PDF, чтобы вы могли мгновенно убедиться, что макет соответствует исходному HTML. Этот шаг завершает цикл **save html as pdf**.

## Шаг 5: Расширенные параметры – создание PDF из HTML‑файла с пользовательскими настройками

Иногда у вас есть физический HTML‑файл на диске, и удобнее использовать `pdfkit.from_file`, а не загружать содержимое вручную. Этот метод полезен, когда HTML уже содержит сложные относительные пути.

```python
# Directly convert a file path to PDF
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Вы также можете добавить обложку, оглавление или флаги выполнения JavaScript, расширив словарь `options`. Например, чтобы добавить обложку:

```python
options.update({
    "cover": str(BASE_DIR / "cover.html"),
    "toc": None,  # Generates a table of contents
})
pdfkit.from_file(str(html_path), str(pdf_path), options=options)
```

Эти настройки демонстрируют **как преобразовать HTML в PDF** для более сложных издательских конвейеров.

## Распространённые подводные камни и как их избежать

| Проблема | Причина | Решение |
|----------|---------|---------|
| Изображения или CSS не отображаются | `wkhtmltopdf` по умолчанию блокирует доступ к локальным файлам | Добавьте `"enable-local-file-access": None` в словарь параметров |
| Unicode‑символы искажаются | Отсутствует параметр `encoding` или файл читается с неверной кодировкой | Всегда указывайте `"encoding": "UTF-8"` и читайте HTML‑файл в UTF‑8 |
| PDF пустой | Неправильный путь к бинарному файлу `wkhtmltopdf` | Укажите путь явно: `pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")` |
| Большие HTML‑файлы вызывают тайм‑аут | Стандартный тайм‑аут слишком короткий | Установите `"javascript-delay": "2000"` или увеличьте тайм‑аут с помощью `"timeout": "60"` |

Устранение этих проблем обеспечивает надёжный процесс **generate pdf from html** в разных окружениях.

## Полный скрипт – пример от начала до конца

Сохраните следующее как `html_to_pdf.py` и запустите командой `python html_to_pdf.py`. Замените `YOUR_DIRECTORY` на путь к вашей папке проекта.

```python
#!/usr/bin/env python3
"""
Convert HTML to PDF in Python – complete, runnable example.
"""

import pathlib
import pdfkit
import os
import subprocess
import sys

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
BASE_DIR = pathlib.Path("YOUR_DIRECTORY")          # <-- change this
HTML_FILE = BASE_DIR / "sample.html"
PDF_FILE = BASE_DIR / "sample.pdf"

# wkhtmltopdf configuration (optional – only needed if binary is not on PATH)
# config = pdfkit.configuration(wkhtmltopdf="/usr/local/bin/wkhtmltopdf")

# Conversion options – customize as required
OPTIONS = {
    "page-size": "A4",
    "margin-top": "0.75in",
    "margin-right": "0.75in",
    "margin-bottom": "0.75in",
    "margin-left":


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы реализации в собственных проектах.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [How to Convert HTML to PDF Java - Set Page Margins with Aspose.HTML](/html/english/java/advanced-usage/css-extensions-adding-title-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}