---
category: general
date: 2026-09-29
description: Как сохранить SVG с помощью Python и экспортировать SVG в PNG. Научитесь
  конвертировать SVG в PNG с тонко настроенными параметрами за считанные минуты.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save svg
- convert svg to png
- save svg as png
- export svg to png
- vector svg to png
language: ru
lastmod: 2026-09-29
og_description: Как сохранить SVG с помощью Python и экспортировать SVG в PNG. Следуйте
  этому руководству, чтобы преобразовать SVG в PNG с полным контролем над параметрами.
og_image_alt: Screenshot of Python code converting a vector SVG file to a PNG image
og_title: Как сохранить SVG в PNG с помощью Python — пошагово
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  headline: How to save SVG as PNG with Python – complete guide
  type: TechArticle
- description: How to save SVG using Python and export SVG to PNG. Learn to convert
    SVG to PNG with fine‑tuned options in minutes.
  name: How to save SVG as PNG with Python – complete guide
  steps:
  - name: Load the SVG document
    text: '```python from aspose.svg import SVGDocument'
  - name: (Optional) Create image‑save options
    text: '```python from aspose.svg import ImageSaveOptions'
  - name: Save the SVG as PNG
    text: '```python # Export the SVG to a PNG file using the options defined above
      svg_doc.save("YOUR_DIRECTORY/vector.png", options) ```'
  - name: Full script
    text: 'Putting the pieces together yields a complete, runnable program:'
  - name: Missing file or invalid path
    text: 'If `src_path` does not exist, `SVGDocument` raises a `FileNotFoundError`.
      Wrap the call in a `try/except` block to provide a friendly error message:'
  - name: Preserving aspect ratio
    text: When only one dimension (width **or** height) is set, the library automatically
      scales the other dimension to maintain the original aspect ratio. If you set
      both dimensions, the image may stretch. Choose the approach that matches your
      UI requirements.
  - name: Transparent backgrounds
    text: 'If the original SVG relies on transparency (e.g., icons), you can keep
      the PNG transparent by omitting `background_color`:'
  type: HowTo
tags:
- Python
- SVG
- Image conversion
title: Как сохранить SVG в PNG с помощью Python — полное руководство
url: /ru/python/general/how-to-save-svg-as-png-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как сохранить SVG как PNG с помощью Python – полное руководство

Если вам нужно **как сохранить SVG** как растровое изображение, этот учебник покажет готовое к запуску решение. Вы узнаете, как загрузить векторный файл SVG, при необходимости настроить параметры сохранения изображения и экспортировать результат в PNG всего в три строки кода.

Сохранение файлов SVG в PNG часто требуется, когда нужно встроить графику в веб‑страницы, создать миниатюры или передать растровые изображения в конвейеры машинного обучения. Описанный подход работает в Windows, macOS и Linux без дополнительных нативных зависимостей.

## Требования

Перед началом убедитесь, что у вас есть:

* Python 3.9 или новее установленный
* Пакет `aspose.svg` (официальный Aspose SVG for Python via .NET). Установите его с помощью:

```bash
pip install aspose-svg
```

* Действительный SVG‑файл на диске (например, `vector.svg`)

Эти требования делают пример автономным и позволяют избежать внешних инструментов, таких как CairoSVG.

## Как сохранить SVG с помощью Python

Суть процесса состоит из трёх шагов: загрузка, настройка и сохранение. Ниже каждый шаг разобран подробно.

### Шаг 1: Загрузка SVG‑документа

```python
from aspose.svg import SVGDocument

# Load the SVG file from the local filesystem
svg_doc = SVGDocument("YOUR_DIRECTORY/vector.svg")
```

`SVGDocument` разбирает XML‑код SVG и создает представление в памяти. Загрузка файла обязана происходить первой; иначе операция сохранения не будет иметь исходных данных.

### Шаг 2: (Опционально) Создание параметров сохранения изображения

```python
from aspose.svg import ImageSaveOptions

# Create default options; you can tweak width, height, and background
options = ImageSaveOptions()
options.width = 800          # Desired output width in pixels
options.height = 600         # Desired output height in pixels
options.background_color = "#FFFFFF"  # Force a white background for transparent SVGs
```

`ImageSaveOptions` позволяет точно настроить вывод PNG. Регулировка ширины и высоты сохраняет соотношение сторон, если не задать оба параметра явно. Установка цвета фона полезна, когда оригинальный SVG содержит прозрачность, а вам нужен непрозрачный PNG.

### Шаг 3: Сохранение SVG как PNG

```python
# Export the SVG to a PNG file using the options defined above
svg_doc.save("YOUR_DIRECTORY/vector.png", options)
```

Метод `save` записывает PNG‑файл по указанному пути. Если опустить аргумент `options`, библиотека использует размеры по умолчанию, полученные из `viewBox` SVG.

### Полный скрипт

Собрав все части вместе, получаем полностью готовую к запуску программу:

```python
# -*- coding: utf-8 -*-
"""
How to save SVG as PNG with Python.
This script loads an SVG file, applies optional image‑save settings,
and exports the result to PNG.
"""

from aspose.svg import SVGDocument, ImageSaveOptions

def convert_svg_to_png(
    src_path: str,
    dst_path: str,
    width: int = 800,
    height: int = 600,
    background: str = "#FFFFFF"
) -> None:
    """Convert an SVG file to PNG with custom dimensions and background."""
    # Load the SVG document
    svg_doc = SVGDocument(src_path)

    # Prepare save options
    options = ImageSaveOptions()
    options.width = width
    options.height = height
    options.background_color = background

    # Save as PNG
    svg_doc.save(dst_path, options)


if __name__ == "__main__":
    # Example usage
    convert_svg_to_png(
        src_path="YOUR_DIRECTORY/vector.svg",
        dst_path="YOUR_DIRECTORY/vector.png",
        width=1024,
        height=768,
        background="#FFFFFF"
    )
    print("SVG successfully saved as PNG.")
```

Запуск скрипта выводит **«SVG successfully saved as PNG.»** и создаёт `vector.png` в той же папке.

## Конвертация SVG в PNG – обработка распространённых проблем

### Отсутствующий файл или неверный путь

Если `src_path` не существует, `SVGDocument` генерирует `FileNotFoundError`. Оберните вызов в блок `try/except`, чтобы вывести понятное сообщение об ошибке:

```python
try:
    svg_doc = SVGDocument(src_path)
except FileNotFoundError:
    raise SystemExit(f"File not found: {src_path}")
```

### Сохранение соотношения сторон

Когда задаётся только одна измерение (ширина **или** высота), библиотека автоматически масштабирует другое измерение, чтобы сохранить оригинальное соотношение сторон. Если задать оба измерения, изображение может растянуться. Выберите подход, соответствующий требованиям вашего интерфейса.

### Прозрачные фоны

Если оригинальный SVG полагается на прозрачность (например, иконки), вы можете оставить PNG прозрачным, опустив `background_color`:

```python
options.background_color = None   # PNG will retain transparency
```

Этот вариант полезен, когда PNG будет накладываться поверх другой графики.

## Экспорт SVG в PNG – советы по производительности

* **Повторное использование `ImageSaveOptions`** при конвертации большого количества файлов пакетно. Создание нового объекта параметров для каждого файла добавляет незначительные накладные расходы, но повторное использование избавляет от повторных аллокаций памяти.
* **Пакетная обработка**: пройдитесь по каталогу SVG‑файлов и вызовите `convert_svg_to_png` для каждого. Библиотека обрабатывает каждый файл независимо, поэтому вы можете распараллелить цикл с помощью `concurrent.futures.ThreadPoolExecutor` для ускорения конвертации на многоядерных машинах.

```python
import os
from concurrent.futures import ThreadPoolExecutor

svg_folder = "YOUR_DIRECTORY"
png_folder = "YOUR_DIRECTORY/pngs"
os.makedirs(png_folder, exist_ok=True)

def batch_convert(file_name):
    src = os.path.join(svg_folder, file_name)
    dst = os.path.join(png_folder, file_name.replace('.svg', '.png'))
    convert_svg_to_png(src, dst)

with ThreadPoolExecutor(max_workers=8) as executor:
    executor.map(batch_convert, [f for f in os.listdir(svg_folder) if f.endswith('.svg')])
```

## Проверка сохранения SVG как PNG

После конвертации вы можете программно проверить результат:

```python
from PIL import Image

with Image.open("YOUR_DIRECTORY/vector.png") as img:
    print(f"PNG size: {img.size}, mode: {img.mode}")
```

Типичный вывод:

```
PNG size: (1024, 768), mode: RGBA
```

Режим `RGBA` подтверждает, что изображение содержит альфа‑канал (прозрачность). Если вы задали цвет фона, режим будет `RGB`.

## Заключение

Теперь вы знаете, **как сохранить SVG** как PNG с помощью Python, **как конвертировать SVG в PNG** и **как экспортировать SVG в PNG** с пользовательскими размерами и настройками фона. Полный скрипт демонстрирует весь рабочий процесс от загрузки векторного SVG‑файла до получения растрового PNG‑изображения.

Далее изучайте связанные темы, такие как **сохранение SVG как PNG** пакетно, использование альтернативных библиотек, например **CairoSVG**, или генерацию многостраничных PDF из SVG‑источников. Экспериментируйте с различными настройками `ImageSaveOptions`, чтобы точно подобрать качество, DPI и степень сжатия под ваш конкретный сценарий.

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [svg to png java – Конвертация SVG в изображение с помощью Aspose.HTML для Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)
- [Отображение SVG‑документа как PNG в .NET с помощью Aspose.HTML](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)
- [Как установить DPI при конвертации SVG в PNG с помощью Java](/html/english/java/conversion-html-to-various-image-formats/how-to-set-dpi-when-converting-svg-to-png-with-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}