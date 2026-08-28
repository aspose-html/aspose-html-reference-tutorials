---
category: general
date: 2026-06-16
description: Как быстро изменить размер SVG в Python – загрузить SVG‑файл в Python,
  отредактировать SVG‑файл в Python и даже пакетно изменять размер SVG‑файлов с помощью
  небольшого скрипта.
draft: false
keywords:
- how to resize svg
- batch resize svg files
- load svg file python
- edit svg file python
language: ru
og_description: Как изменить размер SVG в Python? Узнайте, как загрузить SVG‑файл
  в Python, отредактировать SVG‑файл в Python и пакетно изменять размер SVG‑файлов,
  используя понятный, готовый к запуску пример.
og_title: Как изменить размер SVG в Python – Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  headline: How to Resize SVG in Python – Step‑by‑Step Guide
  type: TechArticle
- description: How to resize SVG in Python quickly – load SVG file Python, edit SVG
    file Python, and even batch resize SVG files with a tiny script.
  name: How to Resize SVG in Python – Step‑by‑Step Guide
  steps:
  - name: '**Collects** every `.svg` file in the source folder.'
    text: '**Collects** every `.svg` file in the source folder.'
  - name: '**Loads** each file using the same routine we used for a single SVG.'
    text: '**Loads** each file using the same routine we used for a single SVG.'
  - name: '**Resizes** to the desired width while keeping the aspect ratio.'
    text: '**Resizes** to the desired width while keeping the aspect ratio.'
  - name: '**Writes** the result to a new folder, leaving originals untouched.'
    text: '**Writes** the result to a new folder, leaving originals untouched.'
  type: HowTo
tags:
- Python
- SVG
- Automation
title: Как изменить размер SVG в Python – пошаговое руководство
url: /ru/python/general/how-to-resize-svg-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как изменить размер SVG в Python – Полный учебник

Когда‑нибудь задумывались **как изменить размер SVG** без открытия графического редактора? Возможно, у вас есть логотип, которому нужно задать ширину 200 px для веб‑баннера, или вы готовите десятки иконок для мобильного приложения. Хорошая новость: всё это можно сделать в Python — без Photoshop, без пользовательского интерфейса Inkscape, всего лишь несколькими строками кода.

В этом руководстве мы пройдёмся по загрузке SVG‑файла в Python, изменению его размеров и даже масштабированию целой папки SVG‑файлов сразу. К концу вы сможете **загрузить SVG файл Python**, **редактировать SVG файл Python** и **массово изменить размер SVG файлов** с уверенностью.

## Требования

- Python 3.8+ установлен (команда `python` работает)
- Библиотека `svgwrite` или `lxml` — мы будем использовать `lxml`, потому что она даёт прямой доступ к DOM.
- Папка с SVG‑файлами, которые нужно изменить (например, `assets/icons/`)

GUI‑инструменты не нужны; всё работает из терминала.

---

## Шаг 1: Установите необходимую библиотеку

Сначала получим `lxml` из PyPI. Она небольшая, быстрая и позволяет напрямую менять атрибуты XML.

```bash
pip install lxml
```

> **Совет:** Если вы работаете в виртуальном окружении, активируйте его перед запуском команды. Это поможет поддерживать зависимости проекта в порядке.

## Шаг 2: Загрузите SVG‑файл в Python

Теперь мы **загрузим SVG файл Python**‑стилем — прочитаем XML, получим корневой элемент `<svg>` и выведем его текущий размер.

```python
from lxml import etree

def load_svg(path: str) -> etree._ElementTree:
    """
    Load an SVG document and return the parsed XML tree.
    """
    parser = etree.XMLParser(remove_blank_text=True)
    tree = etree.parse(path, parser)
    return tree

# Example usage
svg_path = "assets/logo.svg"
svg_tree = load_svg(svg_path)
root = svg_tree.getroot()
print(f"Original width: {root.get('width')}, height: {root.get('height')}")
```

**Почему это важно:** `lxml` предоставляет настоящий DOM, поэтому мы можем запросить или изменить любой атрибут — идеально для задач **редактировать SVG файл Python**.

## Шаг 3: Измените ширину (и высоту) — как изменить размер SVG

SVG — векторный формат, поэтому можно задать либо ширину, либо высоту, либо оба параметра. Если менять только ширину, `viewBox` сохранит соотношение сторон, но многие инструменты также учитывают соответствующий атрибут высоты. Ниже helper, который меняет размер, сохраняя исходное соотношение сторон:

```python
def resize_svg(tree: etree._ElementTree, new_width: int) -> None:
    """
    Resize the root <svg> element to `new_width` while preserving aspect ratio.
    """
    root = tree.getroot()
    # Grab original dimensions (they may be in px, pt, or just numbers)
    orig_width = float(root.get("width").replace("px", ""))
    orig_height = float(root.get("height").replace("px", ""))

    # Compute scale factor and new height
    scale = new_width / orig_width
    new_height = round(orig_height * scale, 2)

    # Update attributes
    root.set("width", f"{new_width}px")
    root.set("height", f"{new_height}px")

    # Optional: ensure viewBox exists for better scaling in browsers
    if "viewBox" not in root.attrib:
        viewbox = f"0 0 {orig_width} {orig_height}"
        root.set("viewBox", viewbox)

# Resize to 200 px wide
resize_svg(svg_tree, 200)
```

Эта функция — ядро **как изменить размер SVG**. Она читает текущий размер, вычисляет пропорциональную высоту и записывает новые атрибуты обратно в файл.

## Шаг 4: Сохраните изменённый SVG

После редактирования нужно записать изменения на диск. Это завершает цикл **редактировать SVG файл Python**.

```python
def save_svg(tree: etree._ElementTree, destination: str) -> None:
    """
    Write the modified SVG tree to `destination`.
    """
    tree.write(
        destination,
        pretty_print=True,
        xml_declaration=True,
        encoding="UTF-8"
    )
    print(f"Saved resized SVG to {destination}")

# Save as a new file so the original stays untouched
output_path = "assets/logo_resized.svg"
save_svg(svg_tree, output_path)
```

Запустите весь скрипт, и вы получите новый `logo_resized.svg`, точно шириной 200 px.

## Шаг 5: Массово изменить размер SVG файлов — масштабировать всю папку

Теперь, когда мы умеем **загрузить SVG файл Python**, **редактировать SVG файл Python** и сохранять его, давайте пройдемся по каталогу и применим то же преобразование к каждому файлу. Это ответ на задачу **массово изменить размер SVG файлов**.

```python
import pathlib

def batch_resize(source_dir: str, target_dir: str, width: int) -> None:
    """
    Resize every .svg file in `source_dir` to `width` pixels and store
    the results in `target_dir`.
    """
    src = pathlib.Path(source_dir)
    tgt = pathlib.Path(target_dir)
    tgt.mkdir(parents=True, exist_ok=True)

    svg_files = list(src.glob("*.svg"))
    if not svg_files:
        print("No SVG files found.")
        return

    for svg_path in svg_files:
        try:
            tree = load_svg(str(svg_path))
            resize_svg(tree, width)
            out_path = tgt / svg_path.name
            save_svg(tree, str(out_path))
        except Exception as e:
            print(f"Failed on {svg_path.name}: {e}")

# Example: resize everything in 'assets/icons' to 64 px wide
batch_resize("assets/icons", "assets/icons_resized", 64)
```

### Что делает этот скрипт:

1. **Собирает** каждый файл с расширением `.svg` в исходной папке.
2. **Загружает** каждый файл тем же способом, что и один SVG.
3. **Изменяет размер** до нужной ширины, сохраняя соотношение сторон.
4. **Записывает** результат в новую папку, оставляя оригиналы нетронутыми.

Теперь у вас есть готовый конвейер для **массово изменить размер SVG файлов**.

## Шаг 6: Особые случаи и распространённые подводные камни

| Проблема | Почему происходит | Решение |
|----------|-------------------|----------|
| Отсутствуют атрибуты `width`/`height` | Некоторые SVG используют только `viewBox`. | Если атрибутов нет, используйте размеры из `viewBox` (`viewBox="0 0 w h"`). |
| Единицы измерения отличные от `px` (например, `pt`, `%`) | Скрипт удаляет только `px`. | Расширьте вызов `replace` или используйте регулярное выражение для захвата любой единицы. |
| Сложные элементы `<symbol>` или `<use>` | Изменение корневого элемента может не затронуть вложенные символы. | Примените те же изменения атрибутов к каждому тегу `<symbol>`, либо используйте CSS `transform: scale()`. |
| Юникод или специальные символы в именах файлов | `pathlib` обрабатывает большинство случаев, но Windows может «потянуть» на некоторых символах. | Убедитесь, что имена файлов безопасны в UTF‑8, либо переименуйте их перед обработкой. |

Учёт этих нюансов заранее избавит вас от неожиданно сломанных иконок позже.

## Шаг 7: Проверьте результат

Быстрая проверка может быть выполнена с помощью небольшого HTML‑фрагмента:

```html
<!DOCTYPE html>
<html>
<head><title>SVG Test</title></head>
<body>
  <h3>Original</h3>
  <img src="assets/logo.svg" alt="original logo">
  <h3>Resized</h3>
  <img src="assets/logo_resized.svg" alt="resized logo">
</body>
</html>
```

Откройте файл в браузере — оба изображения должны выглядеть одинаково, но у изменённого будет ширина **200 px**, видимая в инструментах разработчика.

---

## Заключение

Теперь вы знаете **как изменить размер SVG** с помощью чистого Python, от отдельного файла до целой директории. Рабочий процесс охватывает **загрузить SVG файл Python**, **редактировать SVG файл Python** и **массово изменить размер SVG файлов** — всё это с помощью нескольких функций.

Попробуйте: задайте разные ширины, поэкспериментируйте с изменением только высоты или добавьте интерфейс командной строки с помощью `argparse`. Возможности безграничны, а скрипт достаточно лёгок, чтобы встроить его в сборки, CI‑задачи или настольные утилиты.

Есть вопросы о работе с градиентами, встроенными шрифтами или интеграции в Flask‑приложение? Оставьте комментарий, и мы разберём эти детали вместе. Приятного кодинга!

## Что изучать дальше?

Следующие учебники покрывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Преобразовать SVG в изображение с помощью Aspose.HTML в .NET](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-image/)
- [Преобразовать SVG в PDF с помощью Aspose.HTML в .NET](/html/hindi/net/canvas-and-image-manipulation/convert-svg-to-pdf/)
- [Отобразить SVG‑документ как PNG с помощью Aspose.HTML в .NET](/html/hindi/net/rendering-html-documents/render-svg-doc-as-png/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}