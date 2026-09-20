---
category: general
date: 2026-09-19
description: Узнайте, как изменить заголовок в HTML‑файле с помощью Python. Это руководство
  охватывает чтение HTML, обновление тега <title> и сохранение изменённого HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to change title
- update html title
- read html with python
- load html file python
- save modified html
language: ru
lastmod: 2026-09-19
og_description: Как изменить заголовок в HTML‑файле с помощью Python. Следуйте этому
  полному примеру, чтобы прочитать HTML, обновить тег <title> и сохранить изменённый
  документ.
og_image_alt: Diagram showing how to change title in an HTML file using Python
og_title: Как изменить заголовок в HTML‑файле с помощью Python – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Learn how to change title in an HTML file with Python. This guide covers
    reading HTML, updating the title tag, and saving the modified HTML.
  headline: How to change title in an HTML file using Python
  type: TechArticle
tags:
- Python
- HTML
- Web scraping
title: Как изменить заголовок в HTML‑файле с помощью Python
url: /ru/python/general/how-to-change-title-in-an-html-file-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как изменить заголовок в HTML‑файле с помощью Python

Если вам нужно **как изменить заголовок** в HTML‑документе программно, Python делает эту задачу простой. В этом руководстве вы прочитаете HTML‑файл, обновите элемент `<title>` и сохраните изменённый HTML обратно на диск — все это с понятным, готовым к запуску кодом.

Изменение заголовка страницы — обычный шаг при генерации статических сайтов, кастомизации собранных страниц или автоматизации SEO‑обновлений. К концу этого руководства вы будете знать, как **update html title**, как **read html with python**, и как **save modified html** безопасно.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- Python 3.8 или новее  
- Пакет `beautifulsoup4` (`pip install beautifulsoup4`)  
- HTML‑файл, который нужно отредактировать (в примере используется `index.html` в выбранной вами папке)  

Никакие внешние сервисы не требуются; всё работает локально.

## Шаг 1: Загрузить HTML‑файл с помощью Python  

Первая задача — **load html file python**‑style. Использование `BeautifulSoup` даёт гибкий парсер, который работает с некорректной разметкой.

```python
from pathlib import Path
from bs4 import BeautifulSoup

# Define the directory that holds the original HTML
html_dir = Path("YOUR_DIRECTORY")
original_path = html_dir / "index.html"

# Read the file contents (this is how you **read html with python**)
with original_path.open(encoding="utf-8") as f:
    html_content = f.read()

# Parse the document
soup = BeautifulSoup(html_content, "html.parser")
```

*Почему этот шаг важен:*  
`BeautifulSoup` строит дерево, позволяя выполнять запросы и модификацию элементов без ручной работы со строками. Встроенный `html.parser` быстрый и не требует дополнительных бинарных файлов.

## Шаг 2: Найти элемент `<title>`  

HTML‑документы обычно содержат один тег `<title>` внутри `<head>`. Мы получаем первое вхождение, что удовлетворяет требованию **update html title**.

```python
# Find the first <title> element; BeautifulSoup returns None if missing
title_tag = soup.find("title")

if title_tag is None:
    # If the document lacks a <title>, create one inside <head>
    head_tag = soup.find("head")
    if head_tag is None:
        # As a safety net, add a <head> element at the top
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

# Show the current title (useful for debugging)
print("Current title:", title_tag.string)
```

*Почему проверяем `None`:*  
Некоторые фрагменты HTML могут не содержать заголовка. Автоматическое добавление предотвращает ошибки позже и делает скрипт надёжным.

## Шаг 3: Изменить текст заголовка  

Теперь мы **update html title**, присваивая новое значение строке тега. Это ядро операции **how to change title**.

```python
new_title = "New Title"

# Replace the existing title text
title_tag.string = new_title

print("Updated title:", title_tag.string)
```

Атрибут `string` представляет текстовый узел внутри `<title>`. Перезапись обновляет DOM в памяти.

## Шаг 4: Сохранить изменённый HTML  

Наконец, записываем изменённый документ в новый файл. Это реализует шаг **save modified html** и оставляет оригинал нетронутым.

```python
# Define the output path
modified_path = html_dir / "index_modified.html"

# Write the prettified HTML back to disk
with modified_path.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_path}")
```

`prettify()` форматирует вывод с отступами, делая файл удобочитаемым после изменения.

### Ожидаемый вывод

Запуск скрипта на примере `index.html`, который изначально содержит:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Old Title</title>
</head>
<body>
    <h1>Welcome</h1>
</body>
</html>
```

даёт вывод в консоль, похожий на:

```
Current title: Old Title
Updated title: New Title
Modified HTML saved to YOUR_DIRECTORY/index_modified.html
```

Сохранённый `index_modified.html` теперь начинается с:

```html
<!DOCTYPE html>
<html>
 <head>
  <title>
   New Title
  </title>
 </head>
 <body>
  <h1>
   Welcome
  </h1>
 </body>
</html>
```

## Полный скрипт для быстрого копирования‑вставки

Ниже полностью готовая к запуску программа, объединяющая все четыре шага. Сохраните её как `change_title.py` и при необходимости измените `YOUR_DIRECTORY`.

```python
# change_title.py
from pathlib import Path
from bs4 import BeautifulSoup

# ----------------------------------------------------------------------
# Configuration – change these values to match your environment
# ----------------------------------------------------------------------
html_dir = Path("YOUR_DIRECTORY")          # Folder containing index.html
original_file = html_dir / "index.html"
modified_file = html_dir / "index_modified.html"
new_title = "New Title"                    # Desired title text
# ----------------------------------------------------------------------

# 1️⃣ Load the HTML file (read html with python)
with original_file.open(encoding="utf-8") as f:
    html_content = f.read()

soup = BeautifulSoup(html_content, "html.parser")

# 2️⃣ Locate or create the <title> element
title_tag = soup.find("title")
if title_tag is None:
    head_tag = soup.find("head")
    if head_tag is None:
        head_tag = soup.new_tag("head")
        soup.insert(0, head_tag)
    title_tag = soup.new_tag("title")
    head_tag.append(title_tag)

print("Current title:", title_tag.string)

# 3️⃣ Update the title (how to change title)
title_tag.string = new_title
print("Updated title:", title_tag.string)

# 4️⃣ Save the modified HTML (save modified html)
with modified_file.open("w", encoding="utf-8") as f:
    f.write(soup.prettify())

print(f"Modified HTML saved to {modified_file}")
```

Запустите скрипт:

```bash
python change_title.py
```

Вы увидите сообщения в консоли и новый файл `index_modified.html` с обновлённым заголовком.

## Дополнительные советы и особые случаи

| Ситуация | Что делать |
|-----------|------------|
| **Несколько тегов `<title>`** | `soup.find_all("title")` возвращает список; обновите первый элемент или пройдитесь по всем, если нужно изменить каждый. |
| **Проблемы с кодировкой** | Открывайте файлы с `encoding="utf-8-sig"`, если присутствует BOM, или определяйте кодировку с помощью `chardet`. |
| **Большие HTML‑файлы** | Используйте парсер `lxml` (`BeautifulSoup(html_content, "lxml")`) для лучшей производительности. |
| **Сохранение оригинального форматирования** | Если необходимо сохранить точные пробелы, пишите `str(soup)` вместо `prettify()`. |
| **Автоматизация для множества файлов** | Оберните логику в функцию и пройдитесь по `Path.rglob("*.html")`. |

Эти варианты сохраняют основную логику **how to change title**, адаптируя её к реальным проектам.

## Заключение

Теперь вы знаете, как **how to change title** в любом HTML‑документе с помощью Python. Руководство охватило чтение HTML, поиск тега `<title>`, обновление его текста и **saving modified html** безопасно. С полным скриптом вы можете внедрить этот шаблон в генераторы статических сайтов, SEO‑конвейеры или любую автоматизацию, требующую динамического изменения заголовков.

Далее изучайте связанные темы, такие как **read html with python** для извлечения метатегов, или техники **load html file python** для работы с некорректной разметкой. Поэкспериментируйте с пакетной обработкой, чтобы менять заголовки на всём сайте — ваше новое умение станет фундаментом для множества веб‑автоматизаций. Приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Save HTML with Aspose.Html – Complete C# Guide](/html/english/net/working-with-html-documents/how-to-save-html-with-aspose-html-complete-c-guide/)
- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [How to Render HTML to PNG – Complete Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-render-html-to-png-complete-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}