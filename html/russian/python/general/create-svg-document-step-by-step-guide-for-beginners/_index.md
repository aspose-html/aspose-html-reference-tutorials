---
category: general
date: 2026-07-02
description: Быстро создавайте SVG‑документ с помощью Python. Узнайте, как сохранять
  SVG‑файл, генерировать базовое SVG‑изображение и экспортировать SVG из кода всего
  за несколько строк.
draft: false
keywords:
- create svg document
- save svg file
- how to generate svg
- export svg from code
- create basic svg image
language: ru
og_description: Создавайте SVG‑документы легко. Это руководство показывает, как генерировать
  SVG, сохранять SVG‑файл и экспортировать SVG из кода с помощью чистого примера на
  Python.
og_title: Создание SVG‑документа — быстрый учебник по Python
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  headline: Create SVG Document – Step‑by‑Step Guide for Beginners
  type: TechArticle
- description: Create SVG document quickly with Python. Learn to save SVG file, generate
    a basic SVG image, and export SVG from code in just a few lines.
  name: Create SVG Document – Step‑by‑Step Guide for Beginners
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: How can I add text or other shapes?
    text: Just call `svg.create_element("text", {...})` or `svg.create_element("circle",
      {...})` and append them just like the rectangle. The same **how to generate
      SVG** logic applies.
  - name: What if I need to **export SVG from code** with a transparent background?
    text: Remove any `fill` attribute from the root `<svg>` element or set `fill="none"`
      on shapes that should be transparent. The XML stays valid; browsers will render
      the transparency automatically.
  - name: Can I **save SVG file** with pretty‑printed formatting?
    text: '`ElementTree` writes compact XML by default. For a human‑readable version,
      you can use `xml.dom.minidom` to re‑format:'
  - name: What about performance for large SVGs?
    text: When generating thousands of elements, consider building a list of `ET.Element`
      objects first and then extending the root in one go. This reduces the number
      of tree mutations and speeds up the **save SVG file** operation.
  type: HowTo
tags:
- SVG
- Python
- Graphics
- File I/O
title: Создание SVG‑документа — пошаговое руководство для начинающих
url: /ru/python/general/create-svg-document-step-by-step-guide-for-beginners/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание SVG‑документа – пошаговое руководство для начинающих

Вы когда‑нибудь задумывались, как **create SVG document** без открытия графического редактора? Вы не одиноки. Независимо от того, нужен ли вам крошечный значок для веб‑страницы или динамический график, генерируемый на лету, возможность программно **create SVG document** экономит время и позволяет держать всё под контролем версий.

В этом руководстве мы пройдем полный, исполняемый пример, который покажет вам точно, как **create SVG document**, **save SVG file**, и даже ответит на назревающий вопрос «**how to generate SVG**», возникающий при автоматизации графики. К концу вы получите красный квадрат, сохранённый на диске, и будете знать, как **export SVG from code** для любого будущего проекта.

## Что понадобится

* Python 3.9 или новее (стандартная библиотека делает всю тяжелую работу)
* Текстовый редактор или IDE по вашему вкусу — VS Code, PyCharm или даже Notepad подойдут
* Права записи в папку, где вы будете **save SVG file** (мы будем использовать каталог `output/`)

Внешние пакеты не требуются, поэтому настройка займет буквально пару минут.

## Шаг 1: Настройка вспомогательных функций SVG (Create the Document)

Сначала самое главное: нам нужен небольшой помощник, который создает XML‑структуру за SVG. Считайте это холстом, на котором позже будем добавлять элементы **create basic SVG image**.

```python
import pathlib
import xml.etree.ElementTree as ET

# ----------------------------------------------------------------------
# Helper class that mimics a minimal SVG library.
# ----------------------------------------------------------------------
class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        # Register the SVG namespace so the output looks clean
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        """Create an SVG element with the given attributes."""
        return ET.Element(tag, attrib=attributes)
    
    def append_child(self, element: ET.Element):
        """Append a child element to the root <svg> node."""
        self.root.append(element)
    
    def save(self, file_path: str):
        """Write the SVG XML to a file, creating directories as needed."""
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)
```

**Почему этот шаг важен:** Класс `SVGDocument` абстрагирует низкоуровневую работу с XML. Обернув его в класс, мы сохраняем остальной код чистым, что является лучшей практикой, когда вы **export SVG from code** в более крупных приложениях.

## Шаг 2: Добавление прямоугольника — ядро примера **Create Basic SVG Image**

Теперь, когда у нас есть объект документа, давайте добавим красный квадрат. Это сердце части урока, посвященной **create basic SVG image**.

```python
# ----------------------------------------------------------------------
# Step 2: Build the SVG content
# ----------------------------------------------------------------------
svg = SVGDocument(width=120, height=120)   # canvas size a little larger than the square

# Define rectangle attributes: 100x100 size, red fill, positioned at (10,10)
rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}

# Create the <rect> element and attach it to the SVG root
rect_element = svg.create_element("rect", rect_attrs)
svg.append_child(rect_element)
```

**Explanation:**  
* Координаты `x` и `y` прямоугольника задают отступ в 10 пикселей, чтобы он не прилегал к краю.  
* Использование словаря для атрибутов делает код читаемым и отражает то, как вы бы **save SVG file** атрибуты в любом XML‑формате.  
* Если вам когда‑нибудь понадобится **how to generate SVG** другие фигуры, кроме прямоугольников, просто измените тег на `"circle"` или `"path"` и соответственно поправьте словарь атрибутов.

## Шаг 3: Сохранение SVG — наконец **Save SVG File** на диск

Мы создали документ в памяти; теперь запишем его на диск. Это момент, когда абстрактный **create SVG document** превращается в реальный файл, который можно открыть в браузере.

```python
# ----------------------------------------------------------------------
# Step 3: Persist the SVG to the filesystem
# ----------------------------------------------------------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

**Что вы увидите:** Открытие `output/square.svg` в Chrome, Firefox или любом просмотрщике, поддерживающем SVG, покажет простой красный квадрат с тонкой белой рамкой (фон холста SVG). Это доказательство того, что мы успешно **exported SVG from code**.

## Полный скрипт — решение в одном файле

Ниже представлен полный скрипт, готовый к копированию в `create_svg.py`. Запуск `python create_svg.py` создаст файл, описанный выше.

```python
import pathlib
import xml.etree.ElementTree as ET

class SVGDocument:
    """Simple wrapper to generate an SVG document using ElementTree."""
    SVG_NS = "http://www.w3.org/2000/svg"
    def __init__(self, width: int = 200, height: int = 200):
        ET.register_namespace("", self.SVG_NS)
        self.root = ET.Element(
            "svg",
            attrib={
                "xmlns": self.SVG_NS,
                "width": str(width),
                "height": str(height),
                "version": "1.1"
            }
        )
    def create_element(self, tag: str, attributes: dict) -> ET.Element:
        return ET.Element(tag, attrib=attributes)
    def append_child(self, element: ET.Element):
        self.root.append(element)
    def save(self, file_path: str):
        path = pathlib.Path(file_path)
        path.parent.mkdir(parents=True, exist_ok=True)
        tree = ET.ElementTree(self.root)
        tree.write(str(path), encoding="utf-8", xml_declaration=True)

# -------------------- Build the SVG --------------------
svg = SVGDocument(width=120, height=120)

rect_attrs = {
    "x": "10",
    "y": "10",
    "width": "100",
    "height": "100",
    "fill": "red"
}
svg.append_child(svg.create_element("rect", rect_attrs))

# -------------------- Save the file --------------------
output_path = "output/square.svg"
svg.save(output_path)

print(f"✅ SVG saved! Open {output_path} in any browser to see the red square.")
```

### Ожидаемый вывод

Запуск скрипта выводит:

```
✅ SVG saved! Open output/square.svg in any browser to see the red square.
```

А сгенерированный `square.svg` выглядит так (упрощённый вид):

```xml
<?xml version='1.0' encoding='utf-8'?>
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" version="1.1">
  <rect x="10" y="10" width="100" height="100" fill="red" />
</svg>
```

Открытие файла отображает чёткий красный квадрат — именно то, что мы планировали **create basic SVG image**.

## Расширение примера — ответы на часто задаваемые вопросы

### Как добавить текст или другие фигуры?

Просто вызовите `svg.create_element("text", {...})` или `svg.create_element("circle", {...})` и добавьте их так же, как прямоугольник. Применяется та же логика **how to generate SVG**.

### Что если мне нужно **export SVG from code** с прозрачным фоном?

Удалите любой атрибут `fill` из корневого элемента `<svg>` или задайте `fill="none"` для фигур, которые должны быть прозрачными. XML останется валидным; браузеры автоматически отобразят прозрачность.

### Можно ли **save SVG file** с красивым форматированием?

`ElementTree` пишет компактный XML по умолчанию. Для человекочитаемой версии вы можете использовать `xml.dom.minidom` для повторного форматирования:

```python
import xml.dom.minidom as minidom

def pretty_save(svg_doc, path):
    rough_string = ET.tostring(svg_doc.root, 'utf-8')
    reparsed = minidom.parseString(rough_string)
    with open(path, 'w', encoding='utf-8') as f:
        f.write(reparsed.toprettyxml(indent="  "))
```

Замените `svg.save(output_path)` на `pretty_save(svg, output_path)`.

### Как насчёт производительности при больших SVG?

При генерации тысяч элементов рекомендуется сначала собрать список объектов `ET.Element`, а затем одним вызовом добавить их к корню. Это уменьшает количество модификаций дерева и ускоряет операцию **save SVG file**.

## Профессиональные советы и подводные камни

* **Pro tip:** Всегда используйте абсолютные пути (или `pathlib.Path`) при **saving SVG file**; относительные пути могут сломаться, если скрипт запускается из другой рабочей директории.  
* **Watch out for:** Забвение регистрации пространства имён SVG. Без `ET.register_namespace("", SVGDocument.SVG_NS)` вывод будет содержать лишний префикс `ns0`, который некоторые браузеры неправильно интерпретируют.  
* **Typical mistake:** Смешивание целочисленных и строковых типов в значениях атрибутов. XML ожидает строки, поэтому мы приводим всё к `str()` — вспомогательный класс делает это за вас, но если обойти его, можно получить `TypeError`.  

## Заключение

Мы только что прошли полный пример от начала до конца, показывающий, как **create SVG document**, **save SVG file**, и ответить

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Save SVG Document in Aspose.HTML for Java](/html/english/java/saving-html-documents/save-svg-document/)
- [Create and Manage SVG Documents in Aspose.HTML for Java](/html/english/java/creating-managing-html-documents/create-manage-svg-documents/)
- [svg to png java – Convert SVG to Image with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-svg-to-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}