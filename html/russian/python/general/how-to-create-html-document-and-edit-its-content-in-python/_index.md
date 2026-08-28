---
category: general
date: 2026-08-25
description: Узнайте, как создать HTML‑документ, выбрать элемент CSS, изменить HTML‑текст
  и сохранить HTML‑файл с помощью простого скрипта на Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create html document
- select element css
- modify html text
- save html file
- how to edit html
language: ru
lastmod: 2026-08-25
og_description: Создайте HTML‑документ, выберите элемент CSS, измените текст HTML
  и сохраните HTML‑файл в несколько строк кода на Python. Следуйте этому полному руководству.
og_image_alt: Screenshot of a Python script that creates and updates an HTML file
og_title: Создайте HTML‑документ и отредактируйте его содержимое с помощью Python
  — пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-08-25'
  description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  headline: How to create html document and edit its content in Python
  type: TechArticle
- description: Learn how to create html document, select element css, modify html
    text and save html file using a simple Python script.
  name: How to create html document and edit its content in Python
  steps:
  - name: Full script for quick copy‑paste
    text: '```python # ------------------------------------------------- # File: edit_html.py
      # ------------------------------------------------- # Purpose: Demonstrate how
      to create html document, # select an element with CSS, modify its text, # and
      save the result to a file. # -------------------------------'
  - name: Selecting multiple elements
    text: If you need to **select element css** selectors that match several tags
      (e.g., `"div.note"`), use `doc.select("div.note")` which returns a list. Iterate
      over the list to apply changes to each element.
  - name: Preserving existing attributes
    text: 'When you replace the text, BeautifulSoup retains any attributes on the
      tag. For example:'
  - name: Handling missing elements gracefully
    text: In production scripts, you often encounter malformed HTML. Wrap the selection
      in a conditional or try‑except block, as shown in Step 4, to avoid crashes.
  - name: Writing to a specific directory
    text: 'Replace `output_path` with an absolute or relative path:'
  type: HowTo
tags:
- Python
- HTML manipulation
- CSS selectors
- File I/O
title: Как создать HTML‑документ и редактировать его содержимое в Python
url: /ru/python/general/how-to-create-html-document-and-edit-its-content-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать html документ и редактировать его содержимое в Python

Если вам нужно **create html document** с нуля и программно изменять его элементы, это руководство покажет вам, как это сделать. Вы увидите короткий, исполняемый скрипт, который создает файл, выбирает абзац с помощью CSS‑селектора, обновляет текст и записывает результат обратно на диск.

Работа с HTML в Python распространена при генерации отчетов, шаблонов электронных писем или статического контента сайта. К концу этого руководства вы сможете **select element css**, **modify html text** и **save html file** не выходя из удобства вашей IDE.

## Предварительные требования

* Установлен Python 3.9 или новее.
* Пакеты `beautifulsoup4` и `lxml` (установить с помощью `pip install beautifulsoup4 lxml`).
* Права записи в каталог, где планируется сохранять выходной файл.

Дополнительные инструменты не требуются; стандартная библиотека обрабатывает ввод‑вывод файлов.

## Шаг 1: Установите необходимые библиотеки

```bash
pip install beautifulsoup4 lxml
```

`beautifulsoup4` предоставляет удобный API для разбора и манипуляции HTML, а `lxml` обеспечивает быстрый парсер, понимающий CSS‑селекторы.

## Шаг 2: Создайте начальный HTML‑документ

```python
from bs4 import BeautifulSoup

# Define the initial markup as a string
initial_html = "<p>Old</p>"

# Parse the markup into a BeautifulSoup object
doc = BeautifulSoup(initial_html, "lxml")
```

Конструктор `BeautifulSoup` создает объект **create html document** в памяти. Использование парсера `"lxml"` обеспечивает полную поддержку CSS‑селекторов.

## Шаг 3: Выберите элемент абзаца с помощью CSS‑селектора

```python
# Use the CSS selector "p" to locate the first <p> element
para = doc.select_one("p")
```

Метод `select_one` реализует логику **select element css**, возвращая первый подходящий тег. Если селектор ничего не находит, `para` будет `None`, поэтому в производственном коде рекомендуется выполнить проверку.

## Шаг 4: Измените текстовое содержимое абзаца

```python
if para is not None:
    # Replace the existing text with new content
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")
```

Присваивание `para.string` выполняет операцию **modify html text**. BeautifulSoup обновляет базовое дерево DOM, поэтому изменение отражается при сериализации документа.

## Шаг 5: Сохраните обновлённый HTML в файл

```python
output_path = "updated.html"

# Write the prettified HTML to disk
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())
print(f"HTML file saved to {output_path}")
```

Вызов `open` вместе с `write` реализует функциональность **save html file**. Использование `prettify()` создаёт красиво отформатированный вывод, что полезно при отладке.

### Полный скрипт для быстрого копирования‑вставки

```python
# -------------------------------------------------
# File: edit_html.py
# -------------------------------------------------
# Purpose: Demonstrate how to create html document,
#          select an element with CSS, modify its text,
#          and save the result to a file.
# -------------------------------------------------

from bs4 import BeautifulSoup

# 1️⃣ Create an HTML document with initial content
initial_html = "<p>Old</p>"
doc = BeautifulSoup(initial_html, "lxml")

# 2️⃣ Locate the paragraph element using a CSS selector
para = doc.select_one("p")

# 3️⃣ Update the text inside the paragraph
if para is not None:
    para.string = "New"
else:
    raise ValueError("Paragraph element not found – cannot modify html text")

# 4️⃣ Save the modified document to a file
output_path = "updated.html"
with open(output_path, "w", encoding="utf-8") as f:
    f.write(doc.prettify())

print(f"HTML file saved to {output_path}")
# -------------------------------------------------
```

Запуск `python edit_html.py` создаёт `updated.html`, содержащий:

```html
<p>
 New
</p>
```

## Распространённые варианты и крайние случаи

### Выбор нескольких элементов

Если вам нужны **select element css** селекторы, которые совпадают с несколькими тегами (например, `"div.note"`), используйте `doc.select("div.note")`, который возвращает список. Итеративно обрабатывайте список, чтобы применить изменения к каждому элементу.

```python
for note in doc.select("div.note"):
    note.string = "Updated note"
```

### Сохранение существующих атрибутов

При замене текста BeautifulSoup сохраняет любые атрибуты тега. Например:

```python
initial_html = '<p class="intro">Old</p>'
doc = BeautifulSoup(initial_html, "lxml")
para = doc.select_one("p.intro")
para.string = "New"
# Result: <p class="intro">New</p>
```

### Обработка отсутствующих элементов без сбоев

В производственных скриптах вы часто сталкиваетесь с некорректным HTML. Оберните выбор в условный оператор или блок try‑except, как показано в Шаге 4, чтобы избежать сбоев.

### Запись в конкретный каталог

Замените `output_path` на абсолютный или относительный путь:

```python
output_path = r"C:\Temp\updated.html"   # Windows
# or
output_path = "/home/user/updated.html"  # Linux/macOS
```

Убедитесь, что каталог существует; иначе Python выбросит `FileNotFoundError`.

## Профессиональные советы

* **Performance** – Для больших HTML‑файлов предпочтительно использовать `lxml.etree` напрямую; BeautifulSoup добавляет тонкий слой абстракции, который удобен, но немного медленнее.
* **Encoding** – Всегда открывайте файлы с `encoding="utf-8"`, чтобы сохранять символы, не входящие в ASCII.
* **Testing** – После изменения вы можете проверить результат с помощью `assert "New" in open(output_path).read()` в юнит‑тесте.

## Заключение

Теперь вы знаете, как **create html document**, использовать запрос **select element css** для поиска узла, **modify html text**, и, наконец, **save html file** с помощью Python. Этот подход масштабируется на более сложные преобразования, такие как массовые обновления, изменение атрибутов или генерация шаблонов.

Далее изучайте связанные темы, такие как **how to edit html** с использованием XPath‑выражений, генерация полных HTML‑страниц с Jinja2 или автоматизация пакетной обработки нескольких файлов. Каждая из них опирается на основные шаги, продемонстрированные здесь, и расширяет ваш набор инструментов для программной манипуляции HTML.

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создать HTML‑документ с Aspose.HTML – пошаговое руководство](/html/english/net/html-document-manipulation/create-html-document-with-aspose-html-step-by-step-guide/)
- [Как редактировать дерево HTML‑документа в Aspose.HTML для Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Сохранить HTML‑документ в Aspose.HTML для Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}