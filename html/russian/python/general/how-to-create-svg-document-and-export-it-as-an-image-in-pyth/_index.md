---
category: general
date: 2026-10-02
description: Узнайте, как создать SVG‑документ в Python, сохранить SVG в файл и экспортировать
  SVG‑изображение с помощью короткого полного скрипта.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create SVG document
- save SVG to file
- how to generate SVG
- export SVG image
- SVG Python tutorial
language: ru
lastmod: 2026-10-02
og_description: Создайте SVG‑документ на Python и экспортируйте SVG‑изображение с
  помощью этого практического руководства. Следуйте скрипту, сохраните SVG в файл
  и сразу используйте векторную графику.
og_image_alt: Screenshot of a Python script that creates an SVG document
og_title: Создание SVG‑документа в Python — пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-10-02'
  description: Learn how to create SVG document in Python, save SVG to file, and export
    SVG image with a short, complete script.
  headline: How to create SVG document and export it as an image in Python
  type: TechArticle
tags:
- SVG
- Python
- graphics
title: Как создать SVG‑документ и экспортировать его как изображение в Python
url: /ru/python/general/how-to-create-svg-document-and-export-it-as-an-image-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как создать SVG‑документ и экспортировать его как изображение в Python

Если вам нужно **создать SVG‑документ** программно, этот учебник покажет, как это сделать с помощью Python. Вы увидите полный скрипт, который рисует простой круг, сохраняет SVG в файл и генерирует экспортируемое SVG‑изображение, которое можно вставлять куда угодно.

Генерация масштабируемой векторной графики из кода избавляет от ручного рисования фигур в графическом редакторе. К концу руководства вы сможете интегрировать создание SVG в конвейеры визуализации данных, автоматические генераторы отчетов или любой проект, требующий четкой графики без зависимости от разрешения.

## Требования

Прежде чем начать, убедитесь, что у вас есть:

- Python 3.8 или новее
- Библиотека `svgwrite` (устанавливается командой `pip install svgwrite`)
- Права на запись в каталог, где будет сохраняться SVG

Эти требования делают пример лёгким и совместимым с большинством окружений.

## Шаг 1: Установите и импортируйте библиотеку SVG

Первый шаг — добавить стороннюю библиотеку, предоставляющую удобный API для создания SVG.

```python
# Install the library (run once in your terminal)
# pip install svgwrite

import svgwrite  # Provides the SVGDocument class and element helpers
```

`svgwrite` абстрагирует XML‑структуру SVG‑файла, позволяя сосредоточиться на геометрии, а не на разметке.

## Шаг 2: Создайте объект SVG‑документа

Теперь вы можете **создать SVG‑документ**, создав экземпляр `svgwrite.Drawing`. Этот объект представляет корневой элемент `<svg>` и содержит все последующие фигуры.

```python
# Step 2: Initialize the SVG document
dwg = svgwrite.Drawing(
    filename="circle.svg",     # Desired output file name
    size=("100px", "100px"),   # Width and height of the canvas
    viewBox=("0 0 100 100")    # Coordinate system for drawing
)
```

Аргумент `size` задаёт размеры в пикселях, а `viewBox` определяет систему координат, соответствующую будущей геометрии.

## Шаг 3: Добавьте элемент круга

Круг определяется центром (`cx`, `cy`) и радиусом (`r`). Используйте вспомогательный метод `circle`, чтобы задать эти атрибуты.

```python
# Step 3: Create a <circle> element
circle = dwg.circle(
    center=("50", "50"),   # cx = 50, cy = 50
    r="40",                # radius = 40
    fill="lightcoral",     # Fill color for visual clarity
    stroke="black",        # Outline color
    stroke_width="2"
)

# Append the circle to the SVG root
dwg.add(circle)
```

Круг расположен в центре канвы 100 × 100, оставляя по 10 пикселей отступа со всех сторон. Настройте `fill` и `stroke` под ваш дизайн.

## Шаг 4: Сохраните SVG в файл

После того как графика собрана, вы можете **сохранить SVG в файл** с помощью метода `save`. Это записывает корректный XML, который понимают браузеры и векторные редакторы.

```python
# Step 4: Persist the SVG document
dwg.save()
print("SVG file saved as circle.svg")
```

Файл `circle.svg` теперь находится в текущем рабочем каталоге. Его можно открыть в веб‑браузере, Inkscape или любом другом инструменте, поддерживающем SVG.

## Шаг 5: Проверьте экспортированное SVG‑изображение

Откройте сохранённый файл в браузере, чтобы убедиться в правильности вывода. Вы должны увидеть центрированный круг с указанными цветами. Исходный XML выглядит так:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="100px" height="100px" viewBox="0 0 100 100"
     xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="40"
          fill="lightcoral" stroke="black" stroke-width="2"/>
</svg>
```

Поскольку SVG основан на векторах, изображение можно масштабировать без потери качества, что делает его идеальным для адаптивного веб‑дизайна или печати в высоком разрешении.

## Совет: экспортировать SVG в PNG или JPEG

Если нужен растровый вариант, комбинируйте SVG‑файл с инструментом конвертации, например **CairoSVG**:

```python
# Optional: Convert SVG to PNG
# pip install cairosvg
import cairosvg

cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Этот шаг демонстрирует **экспорт SVG‑изображения** в растровый формат, полезный, когда downstream‑системы не могут напрямую рендерить SVG.

## Общие варианты и граничные случаи

| Вариация | Как обработать |
|-----------|----------------|
| Несколько фигур | Вызывайте `dwg.add()` для каждого нового элемента (rect, line, path). |
| Динамические размеры | Вычисляйте `size` и `viewBox` из данных перед созданием `Drawing`. |
| Текстовые подписи | Используйте `dwg.text("Label", insert=("10", "20"))` и задавайте стиль через `font_size` и `fill`. |
| Повторное использование документа | Храните объект `Drawing` в памяти и вызывайте `save()` каждый раз, когда нужен обновлённый файл. |
| Большие файлы | Потоково выводите данные через `dwg.tostring()` и записывайте в файловый объект вручную, чтобы избежать всплесков памяти. |

Учёт этих сценариев гарантирует, что ваш **скрипт генерации SVG** масштабируется от простых иконок до сложных диаграмм.

## Полный перечень скрипта

Ниже приведён полностью готовый к запуску пример, включающий все шаги и опциональное преобразование:

```python
# Full SVG creation script – create SVG document, save SVG to file, export SVG image
import svgwrite
import cairosvg  # Optional, only needed for PNG conversion

# Initialize the drawing (SVG document)
dwg = svgwrite.Drawing(
    filename="circle.svg",
    size=("100px", "100px"),
    viewBox=("0 0 100 100")
)

# Define a circle element
circle = dwg.circle(
    center=("50", "50"),
    r="40",
    fill="lightcoral",
    stroke="black",
    stroke_width="2"
)

# Add the circle to the document
dwg.add(circle)

# Save the SVG file
dwg.save()
print("SVG file saved as circle.svg")

# Optional: convert SVG to PNG (export SVG image)
cairosvg.svg2png(url="circle.svg", write_to="circle.png")
print("PNG version saved as circle.png")
```

Запуск этого скрипта создаст `circle.svg` и, при установленном `cairosvg`, `circle.png`. Оба файла готовы к включению в веб‑страницы, отчёты или дальнейшую обработку.

## Заключение

Теперь вы знаете, как **создать SVG‑документ** в Python, **сохранить SVG в файл** и **экспортировать SVG‑изображение** для более широкого использования. Пример охватывает основные вызовы API, объясняет, почему каждый шаг важен, и предлагает расширения для более сложной графики.

Далее изучайте дополнительные темы **SVG‑учебника для Python**, такие как рисование путей, применение градиентов и анимация элементов. Интеграция этих техник позволит генерировать динамические, основанные на данных векторные графики напрямую из ваших Python‑приложений. Приятного кодинга!

## Что изучать дальше?

Следующие учебники охватывают близко связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Создание и управление SVG‑документами в Aspose.HTML для Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [Сохранение SVG‑документа в Aspose.HTML для Java](/html/english/java/saving-html-documents/save-svg-document/)
- [svg to png java – Конвертация SVG в изображение с помощью Aspose.HTML для Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}