---
category: general
date: 2026-09-23
description: Измените текст элемента в HTML‑файле с помощью Python. Узнайте, как загрузить
  HTML‑файл, отредактировать тег <title> и эффективно обновить заголовок HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- change element text
- how to change title
- edit title tag
- load html file
- update html title
language: ru
lastmod: 2026-09-23
og_description: Измените текст элемента в HTML‑документе с помощью Python. Этот учебник
  показывает, как загрузить HTML‑файл, отредактировать тег <title> и обновить заголовок
  HTML всего за несколько строк кода.
og_image_alt: Screenshot showing change element text in HTML using Python code
og_title: Изменение текста элемента в HTML с помощью Python — краткое руководство
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  headline: Change element text in HTML with Python – step‑by‑step guide
  type: TechArticle
- description: Change element text in an HTML file using Python. Learn how to load
    HTML file, edit title tag, and update HTML title efficiently.
  name: Change element text in HTML with Python – step‑by‑step guide
  steps:
  - name: 'Edge case: Multiple `<title>` tags'
    text: 'HTML standards allow only one `<title>` element, but malformed files sometimes
      contain more. If you need to handle that situation, iterate over all matches:'
  - name: Editing other elements (e.g., `<h1>`)
    text: 'If you need to **change element text** for a heading instead of the title,
      adjust the XPath:'
  - name: Preserving existing whitespace
    text: 'When the original HTML uses indentation inside tags, `pretty_print` may
      reformat it. To keep the original formatting, omit `pretty_print`:'
  - name: Working with Unicode characters
    text: '`lxml` handles Unicode automatically. Ensure the source file is saved with
      UTF‑8 encoding; otherwise, specify the correct encoding when opening the file.'
  type: HowTo
tags:
- Python
- HTML manipulation
- Web scraping
title: Изменение текста элемента в HTML с помощью Python — пошаговое руководство
url: /ru/python/general/change-element-text-in-html-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Изменение текста элемента в HTML с помощью Python – пошаговое руководство

Если вам нужно **изменить текст элемента** в HTML‑документе, это руководство покажет, как сделать это с помощью Python. Независимо от того, исправляете ли вы устаревший тег `<title>` или обновляете любой другой элемент, вы научитесь **загружать HTML‑файл**, изменять текст и **обновлять заголовок HTML** (или любой элемент) безопасно.

Изменение заголовка веб‑страницы — распространённая задача при очистке собранных данных, генерации статических страниц сайта или автоматизации обновлений SEO. В этом руководстве вы:

* Загрузить HTML‑файл с диска.
* Найти элемент `<title>` и **отредактировать тег title**.
* Сохранить изменённый документ, фактически **обновив заголовок HTML**.

Весь необходимый код включён, и каждый шаг объясняет **почему** операция важна, а не только **что** нужно ввести.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

* Установленный Python 3.9 или новее.
* Библиотека `lxml` (`pip install lxml`).  
  `lxml` обеспечивает быстрое, соответствующее стандартам парсинг и манипуляцию HTML.
* Каталог, содержащий HTML‑файл, который вы хотите отредактировать (замените `YOUR_DIRECTORY` на фактический путь).

## Шаг 1: Загрузка HTML‑файла

Первый шаг — **загрузить HTML‑файл** в дерево DOM (Document Object Model), с которым может работать Python. Использование `lxml.html` даёт поддержку XPath и надёжную работу с элементами.

```python
from pathlib import Path
from lxml import html

# Path to the source HTML document
source_path = Path("YOUR_DIRECTORY/page.html")

# Parse the file into an HTML tree
doc = html.parse(str(source_path))
```

**Почему это важно:**  
Парсинг создаёт структурированное представление страницы, позволяя напрямую запрашивать элементы. Без загрузки файла вы не сможете безопасно **изменить текст элемента**, так как будете работать с сырыми строками, что подвержено ошибкам.

## Шаг 2: Поиск элемента `<title>` и **изменение текста элемента**

Теперь, когда документ загружен, вы можете **отредактировать тег title**. Выражение XPath `".//title"` находит первый элемент `<title>` в иерархии документа.

```python
# Find the <title> element (the first occurrence)
title_elem = doc.find(".//title")

# Guard against missing <title>
if title_elem is None:
    raise ValueError("The document does not contain a <title> element.")

# Change the text inside the <title> tag
title_elem.text = "New Title"
```

**Почему это важно:**  
Прямое присваивание `title_elem.text` **изменяет текст элемента** без изменения окружающей разметки. Такой подход сохраняет пробелы, комментарии и другие теги, гарантируя, что результат останется корректным HTML.

### Пограничный случай: несколько тегов `<title>`

Стандарты HTML допускают только один элемент `<title>`, но в некорректных файлах иногда встречается больше. Если нужно обработать такую ситуацию, переберите все найденные совпадения:

```python
for t in doc.findall(".//title"):
    t.text = "New Title"
```

## Шаг 3: Сохранение изменённого документа – **обновление заголовка HTML**

После изменения запишите дерево обратно на диск. Параметр `pretty_print=True` сохраняет файл читаемым.

```python
# Destination path for the updated file
output_path = Path("YOUR_DIRECTORY/updated.html")

# Write the updated HTML back to a file
doc.write(str(output_path), encoding="utf-8", pretty_print=True)
print(f"HTML saved to {output_path}")
```

**Почему это важно:**  
Сохранение создаёт новый файл, отражающий операцию **изменения текста элемента**. Если нужно перезаписать оригинальный файл, просто используйте тот же путь для `output_path`.

## Полный скрипт в одном блоке

Объединив всё вместе, получаем самостоятельный скрипт, который **загружает HTML‑файл**, **изменяет текст элемента** и **обновляет заголовок HTML**:

```python
"""Change element text in an HTML document – update the <title> tag."""

from pathlib import Path
from lxml import html

def change_title(source: str, new_title: str, destination: str) -> None:
    """Load an HTML file, edit its title, and save the result."""
    # Load the HTML document
    doc = html.parse(source)

    # Locate the <title> element
    title_elem = doc.find(".//title")
    if title_elem is None:
        raise ValueError("No <title> element found in the document.")

    # Change element text
    title_elem.text = new_title

    # Save the updated document
    doc.write(destination, encoding="utf-8", pretty_print=True)

if __name__ == "__main__":
    src = "YOUR_DIRECTORY/page.html"
    dst = "YOUR_DIRECTORY/updated.html"
    change_title(src, "New Title", dst)
    print(f"Updated title saved to {dst}")
```

Запуск этого скрипта создаёт файл `updated.html`, в котором `<title>` теперь содержит **New Title**.

## Распространённые варианты техники

### Редактирование других элементов (например, `<h1>`)

Если нужно **изменить текст элемента** для заголовка вместо title, скорректируйте XPath:

```python
heading = doc.find(".//h1")
if heading is not None:
    heading.text = "Updated Heading"
```

### Сохранение существующего пробельного пространства

Когда оригинальный HTML использует отступы внутри тегов, `pretty_print` может их переоформить. Чтобы сохранить исходное форматирование, опустите `pretty_print`:

```python
doc.write(destination, encoding="utf-8")
```

### Работа с символами Unicode

`lxml` автоматически обрабатывает Unicode. Убедитесь, что исходный файл сохранён в кодировке UTF‑8; иначе укажите правильную кодировку при открытии файла.

## Профессиональные советы и подводные камни

* **Pro tip:** Используйте `doc.xpath("//title/text()")`, если вам нужен только текст без изменения элемента.
* **Watch out for:** HTML‑файлы, содержащие `<title>` внутри `<svg>` или другого не‑HTML пространства имён. В таких случаях уточните XPath, чтобы нацелиться на раздел `<head>`: `doc.find(".//head/title")`.
* **Performance tip:** При пакетной обработке тысяч файлов переиспользуйте один экземпляр парсера, чтобы снизить накладные расходы.

## Заключение

Теперь вы знаете, как **изменить текст элемента** в HTML‑документе с помощью Python, а именно как **загрузить HTML‑файл**, **отредактировать тег title** и **обновить заголовок HTML**. Полный пример демонстрирует надёжный, основанный на библиотеке подход, который работает как с корректным, так и с слегка некорректным HTML.

Отсюда вы можете:

* Применить тот же шаблон к другим тегам (`<h2>`, `<meta>` и т.д.).
* Скомбинировать этот скрипт с конвейером веб‑скрейпинга для очистки больших коллекций страниц.
* Исследовать более богатый API `lxml` для работы с атрибутами, CSS‑селекторами и сериализацией HTML.

Счастливого кодинга, и не стесняйтесь экспериментировать с различными элементами, чтобы освоить манипуляцию HTML в Python!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Загрузка HTML‑документов из файла в Aspose.HTML для Java](/html/english/java/creating-managing-html-documents/load-html-documents-from-file/)
- [Как редактировать дерево HTML‑документа в Aspose.HTML для Java](/html/english/java/editing-html-documents/edit-html-document-tree/)
- [Как парсить HTML в Java – загрузка, запрос и подсчёт элементов](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}