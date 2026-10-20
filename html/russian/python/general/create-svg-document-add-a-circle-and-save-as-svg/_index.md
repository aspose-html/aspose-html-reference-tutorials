---
category: general
date: 2026-07-31
description: Узнайте, как быстро создать SVG‑документ, добавить круг и сохранить файл
  SVG. Экспортируйте графику в SVG с помощью нескольких строк кода на Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create svg document
- save svg file
- export graphic as svg
- add circle to svg
language: ru
lastmod: 2026-07-31
og_description: Создайте SVG‑документ, добавьте круг и сохраните файл SVG за секунды.
  Это руководство покажет, как экспортировать графику в SVG с понятным, исполняемым
  кодом.
og_image_alt: Screenshot of a red circle inside an SVG file named circle.svg
og_title: Создать SVG‑документ – добавить круг и сохранить как SVG
schemas:
- author: Aspose
  dateModified: '2026-07-31'
  description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  headline: Create SVG Document – Add a Circle and Save as SVG
  type: TechArticle
- description: Learn how to create SVG document, add a circle, and save SVG file quickly.
    Export graphic as SVG with a few lines of Python code.
  name: Create SVG Document – Add a Circle and Save as SVG
  steps:
  - name: Pro tip
    text: If you plan to generate many files in a loop, give each `Drawing` a unique
      name or use `io.BytesIO` to keep everything in memory until you’re ready to
      write.
  - name: Edge case – Transparent background
    text: 'If you need a transparent background (the default for SVG), you can skip
      setting a `fill` on the root. For a white background, add:'
  - name: 'Bonus: Export graphic as SVG programmatically'
    text: 'If you need the SVG content as a string—for example, to embed it in an
      HTML email—you can call `dwg.tostring()` instead of `save()`:'
  type: HowTo
- questions:
  - answer: Swap `dwg.circle` for `dwg.rect`, `dwg.ellipse`, or even a custom `<path>`
      string. The API is consistent across shapes.
    question: What if I want a different shape?
  - answer: Absolutely. The file you just created can be referenced with `<img src="circle.svg"
      alt="Red circle">` or inlined with `<svg>` tags.
    question: Can I embed the SVG directly in HTML?
  - answer: You could, but libraries like `svgwrite` handle namespace quirks and make
      the code far more maintainable—especially when you start adding gradients or
      animations.
    question: Why not write raw XML?
  type: FAQPage
tags:
- svg
- python
- vector-graphics
- programming-tutorial
title: Создать SVG‑документ – добавить круг и сохранить как SVG
url: /ru/python/general/create-svg-document-add-a-circle-and-save-as-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать SVG‑документ – Добавить круг и сохранить как SVG

Когда‑нибудь вам нужно было **create SVG document** из кода, но вы не знали, с чего начать? Вы не одиноки; многие разработчики сталкиваются с этим, когда впервые пробуют работать с векторной графикой. В этом руководстве мы пройдём через небольшой, автономный пример, который покажет, как **add circle to SVG**, затем **save SVG file**, чтобы вы могли **export graphic as SVG** для использования в вебе или в инструментах дизайна.

Мы будем держать всё лёгким: всего несколько строк Python, популярная библиотека‑помощник для SVG и небольшое объяснение. К концу у вас будет готовый к использованию `circle.svg` в вашей папке, и вы поймёте, почему каждый шаг важен — без расплывчатых «см. документацию» ухищрений.

## Что понадобится

- Python 3.8+ (любая современная версия подходит)
- Пакет `svgwrite` — установите его с помощью `pip install svgwrite`
- Текстовый редактор или IDE (VS Code, PyCharm или даже Notepad подойдёт)
- Права записи в каталог, где вы хотите сохранить файл

Вот и всё. Никаких тяжёлых зависимостей, никаких внешних сервисов.

## Шаг 1: Создание SVG‑документа

Создание SVG‑документа так же просто, как создание объекта `Drawing` из `svgwrite`. Представьте этот объект как чистый холст, на котором живут все формы.

```python
import svgwrite

# Step 1: Create a new SVG document (canvas) 800×800 pixels
dwg = svgwrite.Drawing(filename="circle.svg", size=("200px", "200px"))
```

> **Почему это важно:** Класс `Drawing` обрабатывает всю XML‑обёртку за вас — пространства имён, заголовки и корневой элемент `<svg>`. Указав имя файла заранее, мы уже знаем, куда он будет сохранён, что делает последующий шаг **save svg file** тривиальным.

### Совет профессионала
Если вы планируете генерировать много файлов в цикле, дайте каждому `Drawing` уникальное имя или используйте `io.BytesIO`, чтобы держать всё в памяти до момента записи.

## Шаг 2: Добавление круга в SVG

Теперь, когда документ существует, давайте **add circle to SVG**. Метод `add()` принимает любой объект формы; `Circle` идеально подходит для простого красного пятна в центре.

```python
# Step 2: Add a red circle element to the SVG root
center = (100, 100)          # x, y coordinates (half of 200px canvas)
radius = 80                  # radius in pixels
circle = dwg.circle(center=center, r=radius, fill='red')
dwg.add(circle)
```

> **Почему мы используем переменные `center` и `radius`:** Жёстко зашитые числа усложняют чтение и поддержку кода. Присваивая значениям имена, мы уточняем намерение — этот круг находится точно в центре канвы 200 × 200 и достаточно велик, чтобы его было заметно.

### Пограничный случай — Прозрачный фон
Если вам нужен прозрачный фон (по умолчанию для SVG), вы можете не задавать `fill` у корня. Для белого фона добавьте:

```python
dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))
```

Разместите это перед добавлением круга, чтобы прямоугольник оказался под ним.

## Шаг 3: Сохранение SVG‑файла

С формой на месте, последний шаг — **save SVG file**. Метод `save()` записывает XML на диск, и поскольку мы уже задали `Drawing` имя файла, один вызов справляется с задачей.

```python
# Step 3: Save the SVG document to a file
dwg.save()
print("✅ circle.svg has been created in the current directory.")
```

> **Что происходит «под капотом»?** `svgwrite` сериализует дерево элементов в строку, добавляет объявление XML и записывает его в кодировке UTF‑8. Если целевой каталог не существует, Python выбросит `FileNotFoundError`; убедитесь, что путь корректен, или создайте его с помощью `os.makedirs()`.

### Бонус: Программный экспорт графики как SVG
Если вам нужен SVG‑контент в виде строки — например, чтобы встроить его в HTML‑письмо — вы можете вызвать `dwg.tostring()` вместо `save()`:

```python
svg_content = dwg.tostring()
# Now you can send svg_content over a network, store it in a DB, etc.
```

## Полный рабочий пример

Собрав всё вместе, представляем полностью готовый к запуску скрипт:

```python
import svgwrite
import os

def create_svg_with_circle(output_path: str):
    """
    Creates an SVG file containing a single red circle.
    Parameters
    ----------
    output_path: str
        Full path where the SVG file will be saved.
    """
    # Ensure the directory exists
    os.makedirs(os.path.dirname(output_path), exist_ok=True)

    # Initialise the SVG document (800×800 canvas)
    dwg = svgwrite.Drawing(filename=output_path, size=("200px", "200px"))

    # Optional: add a white background rectangle
    dwg.add(dwg.rect(insert=(0, 0), size=("200px", "200px"), fill='white'))

    # Add a red circle in the centre
    center = (100, 100)
    radius = 80
    circle = dwg.circle(center=center, r=radius, fill='red')
    dwg.add(circle)

    # Save the file – this is the key step to **save svg file**
    dwg.save()
    print(f"✅ SVG saved to {output_path}")

if __name__ == "__main__":
    # Change this path to wherever you want the file
    output_file = os.path.join(os.getcwd(), "circle.svg")
    create_svg_with_circle(output_file)
```

**Ожидаемый результат:** После запуска скрипта вы увидите файл `circle.svg` в той же папке. Открыв его в браузере или любом векторном редакторе, вы увидите красный круг, центрированный на белом квадрате — точно то, что мы запрограммировали.

## Часто задаваемые вопросы и подводные камни

- **Что если я хочу другую форму?** Замените `dwg.circle` на `dwg.rect`, `dwg.ellipse` или даже на пользовательскую строку `<path>`. API последователен для всех форм.
- **Можно ли встроить SVG напрямую в HTML?** Конечно. Созданный файл можно ссылаться с помощью `<img src="circle.svg" alt="Red circle">` или встроить с помощью тегов `<svg>`.
- **Почему не писать чистый XML?** Можно, но такие библиотеки, как `svgwrite`, управляют особенностями пространств имён и делают код гораздо более поддерживаемым — особенно когда вы начинаете добавлять градиенты или анимацию.

## Заключение

Теперь вы знаете, как **create SVG document**, **add circle to SVG** и **save SVG file**, чтобы вы могли **export graphic as SVG** всего несколькими строками Python. Этот подход масштабируется: замените круг любой векторной формой, пройдитесь по данным для генерации диаграмм или пакетно обработайте ресурсы для дизайн‑системы.

Следующие шаги? Попробуйте добавить текстовые метки, поэкспериментировать с градиентами или сгенерировать целую галерею иконок в одном скрипте. Если вам интересны более продвинутые возможности, ознакомьтесь с документацией `svgwrite` о группах (`<g>`), трансформациях и поддержке анимации.

Счастливого кодинга, и пусть ваши векторы всегда остаются чёткими!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Сохранить SVG‑документ в Aspose.HTML для Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Создание и управление SVG‑документами в Aspose.HTML для Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Конвертация SVG в изображение с помощью Aspose.HTML для Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}