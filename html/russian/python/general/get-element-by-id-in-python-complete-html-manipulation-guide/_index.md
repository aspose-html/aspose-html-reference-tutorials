---
category: general
date: 2026-05-31
description: Узнайте, как получить элемент по id, изменить цвет фона в HTML, прочитать
  текст HTML и установить атрибут HTML с помощью Python. Пошаговое руководство.
draft: false
keywords:
- get element by id
- change background colour html
- how to read html text
- how to set html attribute
- manipulate html with python
language: ru
og_description: Получите элемент по id, прочитайте HTML‑текст, установите HTML‑атрибут
  и измените цвет фона HTML с помощью Python в одном простом руководстве.
og_title: Получить элемент по id в Python — Полный учебник по манипуляции HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  headline: Get element by id in Python – Complete HTML Manipulation Guide
  type: TechArticle
- description: Learn how to get element by id, change background colour HTML, read
    HTML text and set HTML attribute using Python. Step‑by‑step tutorial.
  name: Get element by id in Python – Complete HTML Manipulation Guide
  steps:
  - name: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
    text: '**Imports** `lxml.html` for parsing and `pathlib` for OS‑independent paths.'
  - name: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
    text: '**Loads** `sample.html` and aborts with a clear error if the file is missing.'
  - name: '**Retrieves** the element using **get element by id**.'
    text: '**Retrieves** the element using **get element by id**.'
  - name: '**Prints** the element’s text—showing **how to read HTML text**.'
    text: '**Prints** the element’s text—showing **how to read HTML text**.'
  - name: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
    text: '**Adds** a custom attribute, illustrating **how to set HTML attribute**.'
  - name: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
    text: '**Changes** the background colour, fulfilling the **change background colour
      html** requirement.'
  - name: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
    text: '**Writes** the updated markup to `sample_modified.html`, so you can open
      it in a browser and see the changes.'
  type: HowTo
tags:
- python
- html
- web‑scraping
title: Получить элемент по id в Python — Полное руководство по работе с HTML.
url: /ru/python/general/get-element-by-id-in-python-complete-html-manipulation-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Получить элемент по id в Python – Полное руководство по манипуляции HTML

Когда‑то вам нужно **получить элемент по id** со страницы HTML, пиша быстрый скрипт на Python? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда начинают сканировать сайты или править локальные отчёты. Хорошая новость: всего несколькими строками кода можно вывести текст элемента, изменить его цвет фона и даже задать новые атрибуты, не выходя из редактора.

В этом уроке мы пройдём реальный пример: загрузим локальный `sample.html`, получим элемент с ID `main‑content`, выведем его внутренний текст и, наконец, поменяем цвет фона на светло‑серый. К концу вы также узнаете **как читать текст HTML**, **как задавать атрибут HTML** и почему **манипулировать HTML с помощью Python** — полезный навык в любой автоматизации.

## Что понадобится

Прежде чем начать, убедитесь, что у вас есть:

- **Python 3.9+** (подойдёт любая современная версия)
- Библиотека **`lxml`** (или **BeautifulSoup**, если предпочитаете) — мы будем использовать `lxml.html`, потому что она предоставляет удобный API в стиле `get_element_by_id`.
- Небольшой HTML‑файл `sample.html` в папке `YOUR_DIRECTORY`. Скопируйте ниже приведённый фрагмент в этот файл:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Demo Page</title>
</head>
<body>
    <div id="main-content">
        Hello, world! This is the original text.
    </div>
</body>
</html>
```

И всё — никаких сложных фреймворков, только чистый Python и статический HTML‑файл.

## Шаг 1: Установить требуемую библиотеку

Если `lxml` ещё не установлен, откройте терминал и выполните:

```bash
pip install lxml
```

*Совет:* использовать виртуальное окружение, чтобы не захламлять глобальную установку Python, особенно когда работаете с несколькими проектами.

## Шаг 2: Загрузить HTML‑документ

Теперь прочитаем файл в объект документа `lxml.html`. Это как превратить сырой текст в дерево, по которому можно перемещаться.

```python
from lxml import html
import pathlib

# Resolve the path to the sample file
html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")

# Parse the file into an HTML document
doc = html.parse(str(html_path)).getroot()
print("Document loaded successfully.")
```

При запуске вы увидите сообщение «Document loaded successfully». Если файл не найден, Python бросит `FileNotFoundError` — это удобно отловить сразу, пока вы не ищете «призрачный» элемент.

## Шаг 3: Получить элемент по id

Суть дела. `lxml` предоставляет удобный метод `get_element_by_id`, аналогичный DOM‑API в JavaScript.

```python
# Retrieve the element with the specific ID
elem = doc.get_element_by_id("main-content")

if elem is not None:
    print("Element found!")
else:
    print("No element with that ID.")
```

Если элемент существует, в консоль будет выведено «Element found!». Это и есть **get element by id**, на котором основаны все дальнейшие манипуляции.

## Шаг 4: Как читать текст HTML

Получив элемент, извлечь его видимый текст проще простого. Метод `text_content()` возвращает всё, что находится внутри, без тегов.

```python
if elem is not None:
    # Show the element's current inner text
    inner_text = elem.text_content()
    print("Inner text:", inner_text)
```

Ожидаемый вывод:

```
Inner text: Hello, world! This is the original text.
```

Может возникнуть вопрос: *а что если элемент содержит вложенные теги?* `text_content()` всё равно работает — он конкатенирует все дочерние текстовые узлы, давая чистую строку, которую можно логировать, сохранять или передавать в другой алгоритм.

## Шаг 5: Как задать атрибут HTML

Изменять или добавлять атрибуты так же просто. Метод `set` позволяет задать любое имя атрибута.

```python
if elem is not None:
    # Set a custom data attribute
    elem.set("data-modified", "true")
    # Verify it was added
    print("New attribute value:", elem.get("data-modified"))
```

Вывод:

```
New attribute value: true
```

Эта строка демонстрирует **how to set HTML attribute** «на лету». Вместо `"data-modified"` можно указать `"class"`, `"title"` или любой другой поддерживаемый элементом атрибут.

## Шаг 6: Изменить цвет фона HTML

Теперь визуальная правка. Чтобы поменять цвет фона, добавим атрибут `style`, переопределяющий значение по умолчанию.

```python
if elem is not None:
    # Change the background colour via a style attribute
    elem.set("style", "background:#f0f0f0")
    print("Background style applied.")
```

После выполнения скрипта `div` в `sample.html` будет выглядеть так при открытии в браузере:

```html
<div id="main-content" data-modified="true" style="background:#f0f0f0">
    Hello, world! This is the original text.
</div>
```

Это техника **change background colour html**, которую можно применять к любому элементу — просто замените код цвета.

## Шаг 7: Манипулировать HTML с помощью Python — объединяем всё вместе

Ниже полная, готовая к запуску программа, объединяющая все шаги. Сохраните её как `modify_html.py` и запустите из той же директории, где находится папка `YOUR_DIRECTORY`.

```python
#!/usr/bin/env python3
"""
Complete example: load an HTML file, get element by id,
read its text, set a new attribute, and change its background colour.
"""

from lxml import html
import pathlib
import sys

def main():
    # 1️⃣ Load the document
    html_path = pathlib.Path("YOUR_DIRECTORY/sample.html")
    try:
        doc = html.parse(str(html_path)).getroot()
    except OSError as e:
        sys.exit(f"Failed to read HTML file: {e}")

    # 2️⃣ Get element by id
    elem = doc.get_element_by_id("main-content")
    if elem is None:
        sys.exit("Element with ID 'main-content' not found.")

    # 3️⃣ Read HTML text
    print("🗒️  Inner text:", elem.text_content())

    # 4️⃣ Set a new attribute
    elem.set("data-modified", "true")
    print("✅  data-modified attribute set to:", elem.get("data-modified"))

    # 5️⃣ Change background colour HTML
    elem.set("style", "background:#f0f0f0")
    print("🎨  Background colour changed to #f0f0f0")

    # 6️⃣ Write the modified HTML back to disk
    output_path = pathlib.Path("YOUR_DIRECTORY/sample_modified.html")
    output_path.write_text(html.tostring(doc, pretty_print=True, encoding="unicode"))
    print(f"💾  Modified file saved as {output_path}")

if __name__ == "__main__":
    main()
```

### Что делает скрипт, построчно

1. **Импортирует** `lxml.html` для парсинга и `pathlib` для кроссплатформенных путей.  
2. **Загружает** `sample.html` и останавливается с понятной ошибкой, если файл отсутствует.  
3. **Получает** элемент с помощью **get element by id**.  
4. **Выводит** текст элемента — показывая **how to read HTML text**.  
5. **Добавляет** пользовательский атрибут, иллюстрируя **how to set HTML attribute**.  
6. **Меняет** цвет фона, реализуя требование **change background colour html**.  
7. **Записывает** изменённую разметку в `sample_modified.html`, чтобы вы могли открыть её в браузере и увидеть изменения.

Запуск скрипта даст консольный вывод, похожий на:

```
🗒️  Inner text: Hello, world! This is the original text.
✅  data-modified attribute set to: true
🎨  Background colour changed to #f0f0f0
💾  Modified file saved as YOUR_DIRECTORY/sample_modified.html
```

Откройте `sample_modified.html`, и вы заметите серый фон за текстом — доказательство того, что **manipulate HTML with python** действительно работает.

## Частые ошибки и как их избежать

- **Отсутствующий ID** — если целевой элемент не найден, `get_element_by_id` вернёт `None`. Всегда проверяйте на `None` перед доступом к свойствам; иначе получите `AttributeError`.  
- **Проблемы с кодировкой** — при чтении страниц с не‑ASCII символами передайте `encoding='utf-8'` в `html.parse` или убедитесь, что файл сохранён в UTF‑8.  
- **Перезапись существующих стилей** — установка атрибута `style` заменяет любые предыдущие inline‑стили. Если нужно сохранить их, сначала прочитайте текущий `style`, добавьте новое правило и запишите обратно.  
- **Разрешения файлов** — запись в ту же папку может не работать на системах с только‑для‑чтения правами. Выберите путь, доступный для записи, как мы сделали с `sample_modified.html`.

## Как расширить пример

Теперь, когда базовые навыки под контролем, можно попробовать следующее:

- **Обрабатывать несколько ID** — создайте список ID и пройдитесь по нему в цикле `for`, чтобы пакетно обрабатывать разделы страницы.  
- **Заменять текстовое содержимое** — вызовите `elem.text = "Новый текст"` для изменения видимой строки.  
- **Добавлять дочерние элементы** — используйте `

## Что изучать дальше?

- [How to Edit HTML Using Aspose.HTML for Java](/html/english/java/editing-html-documents/advanced-html-document-tree-editing/)
- [How to Query HTML in Java – Complete Tutorial](/html/english/java/creating-managing-html-documents/how-to-query-html-in-java-complete-tutorial/)
- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}