---
category: general
date: 2026-11-27
description: Создайте SVG‑документ и сохраните SVG‑файл с помощью Python. Научитесь
  экспортировать вектор в SVG и быстро генерировать SVG‑изображение.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG file
- export vector as SVG
- save SVG image
- how to create SVG
language: ru
lastmod: 2026-11-27
og_description: Создайте SVG‑документ и сохраните SVG‑файл с помощью Python. Это руководство
  покажет, как экспортировать вектор в SVG и создать SVG‑изображение за несколько
  минут.
og_image_alt: Screenshot of a red circle saved as an SVG document
og_title: Создайте SVG‑документ и сохраните SVG‑файл с помощью Python
schemas:
- author: Aspose
  dateModified: '2026-11-27'
  description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  headline: Create SVG document and save SVG file with Python
  type: TechArticle
- description: Create SVG document and save SVG file using Python. Learn to export
    vector as SVG and generate a SVG image quickly.
  name: Create SVG document and save SVG file with Python
  steps:
  - name: Expected output
    text: 'The resulting `circle.svg` contains:'
  - name: Exporting more complex vectors
    text: 'If you need to **export vector as SVG** for multi‑shape illustrations,
      simply repeat the `dwg.add()` pattern with other primitives (`rect`, `line`,
      `path`, etc.). For example:'
  - name: Handling Unicode and text
    text: "SVG supports text elements with full Unicode support. Use `dwg.text(\"Hello,
      \U0001F30D\", insert=(5, 95), fill=\"black\")` to embed multilingual labels."
  - name: Saving to a different location
    text: 'When **save SVG image** to a user‑specified folder, validate the path to
      avoid permission errors:'
  - name: Minifying the output
    text: 'For production pipelines, you might want a smaller file size. Pass `pretty=False`
      to `dwg.tostring()` and write the result manually:'
  type: HowTo
tags:
- SVG
- Python
- Vector graphics
title: Создать SVG‑документ и сохранить SVG‑файл с помощью Python
url: /ru/python/general/create-svg-document-and-save-svg-file-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать SVG‑документ и сохранить SVG‑файл с помощью Python

Если вам нужно **create SVG document** с нуля, это руководство проведёт вас через весь процесс. Вы увидите, как **save SVG file** на диск, экспортировать вектор как SVG и получить готовое к использованию SVG‑изображение всего за несколько строк кода.

Генерация масштабируемой графики программно полезна для отчётов, иконок UI или любой ситуации, когда нужны изображения, независимые от разрешения. К концу этого руководства вы сможете ответить на вопрос «**how to create SVG**?», создавая простые формы и расширяя шаблон до сложных векторных иллюстраций.

## Что понадобится

- Python 3.8 или новее  
- Пакет `svgwrite` (устанавливается через `pip`)  
- Доступный для записи каталог для выходного файла  

Внешние графические редакторы не требуются; всё работает из командной строки.

## Шаг 1: Установить библиотеку `svgwrite`

`svgwrite` предоставляет чистый, Python‑подобный API для построения SVG‑разметки. Установите её один раз с помощью:

```bash
pip install svgwrite
```

> **Pro tip:** Используйте виртуальное окружение (`python -m venv .venv`), чтобы изолировать зависимости.

## Шаг 2: Создать SVG‑документ

Теперь мы действительно **create SVG document** объекты. Класс `Drawing` представляет корневой элемент `<svg>` и автоматически обрабатывает пространства имён.

```python
import pathlib
import svgwrite

# Define where the file will be saved
output_path = pathlib.Path("output/circle.svg")
output_path.parent.mkdir(parents=True, exist_ok=True)

# Initialize a new SVG document with a 100×100 viewport
dwg = svgwrite.Drawing(
    filename=str(output_path),
    size=("100px", "100px"),
    profile="tiny"  # tiny profile keeps the file lightweight
)
```

Экземпляр `Drawing` является точкой входа для всех последующих SVG‑операций. Указывая `size`, мы задаём размеры холста, что влияет на то, как браузеры отображают изображение.

## Шаг 3: Добавить элемент красного круга

Добавление фигур простое. Метод `circle` создаёт элемент `<circle>`; затем мы присоединяем его к корню.

```python
# Create a red circle with radius 40 centered at (50, 50)
circle = dwg.circle(
    center=(50, 50),
    r=40,
    fill="red"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Почему мы выбираем круг: круги — векторные примитивы, демонстрирующие масштабируемость без потери качества, что делает результат идеальным для тестирования процессов **export vector as SVG**.

## Шаг 4: Сохранить SVG‑файл

Наконец, запишите разметку на диск. Этот шаг удовлетворяет требование **save SVG file** и создаёт файл, который можно открыть в любом браузере или векторном редакторе.

```python
# Persist the SVG document to the filesystem
dwg.save()
print(f"SVG saved to {output_path.resolve()}")
```

Когда вы запустите скрипт, вы увидите сообщение в консоли, подтверждающее местоположение сгенерированного файла.

### Ожидаемый вывод

Полученный `circle.svg` содержит:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg height="100px" version="1.1" width="100px" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40" fill="red"/>
</svg>
```

Открытие файла в браузере отображает чёткий красный круг, и поскольку он векторный, вы можете масштабировать его бесконечно без пикселизации.

## Шаг 5: Распространённые варианты и граничные случаи

### Экспорт более сложных векторов

Если вам нужно **export vector as SVG** для многофигурных иллюстраций, просто повторите шаблон `dwg.add()` с другими примитивами (`rect`, `line`, `path` и т.д.). Например:

```python
dwg.add(dwg.rect(insert=(10, 10), size=(30, 30), fill="blue"))
dwg.add(dwg.line(start=(0, 0), end=(100, 100), stroke="black", stroke_width=2))
```

### Работа с Unicode и текстом

SVG поддерживает текстовые элементы с полной поддержкой Unicode. Используйте `dwg.text("Hello, 🌍", insert=(5, 95), fill="black")` для встраивания многоязычных меток.

### Сохранение в другое место

При **save SVG image** в пользовательскую папку проверьте путь, чтобы избежать ошибок доступа:

```python
if not output_path.parent.exists():
    raise PermissionError(f"Cannot write to {output_path.parent}")
dwg.save()
```

### Минификация вывода

Для производственных конвейеров может потребоваться меньший размер файла. Передайте `pretty=False` в `dwg.tostring()` и запишите результат вручную:

```python
minified = dwg.tostring(pretty=False)
output_path.write_text(minified)
```

## Как создать SVG с альтернативными библиотеками (необязательно)

Хотя `svgwrite` лёгок и написан полностью на Python, существуют и другие экосистемы:

- **cairosvg** – преобразует PNG, PDF или HTML в SVG.  
- **lxml** – позволяет вручную строить SVG‑разметку с помощью XML‑API.  

Выбор библиотеки зависит от сложности вашего проекта и существующих зависимостей.

## Заключение

Теперь вы знаете, как **create SVG document**, добавлять векторные формы и **save SVG file** с помощью Python. Полное решение демонстрирует шаги для **export vector as SVG**, создания **SVG image** и ответа на распространённый вопрос **how to create SVG** программно.

Отсюда вы можете:

- Расширить скрипт с помощью циклов для автоматической генерации диаграмм или иконок.  
- Интегрировать вывод SVG в веб‑приложения или шаблоны электронных писем.  
- Исследовать анимацию, добавляя элементы `<animate>` с помощью `svgwrite`.

Экспериментируйте с различными формами, цветами и градиентами, чтобы полностью раскрыть возможности масштабируемой векторной графики в ваших Python‑проектах. Приятного кодинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, опирающиеся на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и изучить альтернативные подходы к реализации в собственных проектах.

- [Create SVG Document – Add a Circle and Save as SVG](/html/english/python/general/create-svg-document-add-a-circle-and-save-as-svg/)
- [Create SVG Document in Python – Convert SVG to PNG Guide](/html/english/python/general/create-svg-document-in-python-convert-svg-to-png-guide/)
- [Load SVG File Python – Complete Guide to Export, Embed & Convert](/html/english/python/general/load-svg-file-python-complete-guide-to-export-embed-convert/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}