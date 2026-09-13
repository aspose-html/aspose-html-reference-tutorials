---
category: general
date: 2026-09-13
description: Изучите, как разбирать HTML и загружать HTML‑документ, ограничивая глубину,
  чтобы предотвратить бесконечную рекурсию в Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to parse html
- load html document
- how to limit depth
- prevent infinite recursion
language: ru
lastmod: 2026-09-13
og_description: Как безопасно парсить HTML и загружать HTML‑документ. Это руководство
  показывает, как ограничить глубину и предотвратить бесконечную рекурсию.
og_image_alt: Diagram showing HTML parsing flow with depth‑limit control
og_title: Как парсить HTML с ограничением глубины — учебник по Python
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to parse HTML and load HTML document while limiting depth
    to prevent infinite recursion in Python.
  headline: How to parse HTML with depth limiting using Python
  type: TechArticle
- description: Learn how to parse HTML and load HTML document while limiting depth
    to prevent infinite recursion in Python.
  name: How to parse HTML with depth limiting using Python
  steps:
  - name: Create resource handling options
    text: The `ResourceHandlingOptions` object tells the parser when to stop following
      nested resources such as `<iframe>` tags or linked CSS files.
  - name: Load HTML document with the configured options
    text: Now you load the file while supplying the options you just defined. This
      is the **load html document** step that respects the depth limit.
  - name: Parse the document safely
    text: With the document loaded, you can now traverse the DOM. The example below
      extracts all headings (`<h1>`‑`<h3>`) without exceeding the depth limit.
  type: HowTo
tags:
- html parsing
- python
- recursion
- resource handling
title: Как парсить HTML с ограничением глубины с помощью Python
url: /ru/python/general/how-to-parse-html-with-depth-limiting-using-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как парсить HTML с ограничением глубины с помощью Python

Если вам нужно **how to parse html** из большого отчёта, первым шагом является загрузка HTML‑документа с защитой, которая останавливает глубокое вложение. В этом руководстве показано, как загрузить HTML‑документ, установить максимальную глубину обработки и **prevent infinite recursion**, когда ресурсы ссылаются друг на друга.

Вы увидите полный, исполняемый пример, использующий `ResourceHandlingOptions` и `HTMLDocument`. К концу руководства вы сможете безопасно парсить любой HTML‑файл, не исчерпывая память и не вызывая переполнение стека.

## Требования

* Python 3.9 или новее установлен.
* Библиотека обработки HTML, предоставляющая `ResourceHandlingOptions` и `HTMLDocument`. (Для этого руководства мы предполагаем, что библиотека называется `htmlhandler`; установите её с помощью `pip install htmlhandler`.)
* Базовое понимание рекурсии и структуры HTML.

Дополнительная настройка системы не требуется.

## Как парсить HTML с ограничением глубины

Суть решения состоит в создании экземпляра `ResourceHandlingOptions`, настройке его `max_handling_depth` и передаче его в `HTMLDocument`. Ниже приведены шаги, которые проведут вас через процесс.

### Шаг 1: Создать параметры обработки ресурсов

`ResourceHandlingOptions` объект указывает парсеру, когда прекращать следовать вложенным ресурсам, таким как теги `<iframe>` или связанные CSS‑файлы.

```python
# Step 1: Create resource handling options
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after 3 levels of nested resources
```

*Почему это важно*: Без ограничения глубины вредоносный или некорректный документ может встраивать ресурсы, которые ссылаются друг на друга бесконечно. Установка `max_handling_depth` в 3 гарантирует, что парсер остановится после трёх уровней, чего достаточно для большинства легитимных документов, одновременно защищая среду выполнения.

### Шаг 2: Загрузить HTML‑документ с настроенными параметрами

Теперь вы загружаете файл, передавая только что определённые параметры. Это шаг **load html document**, который учитывает ограничение глубины.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument(
    "YOUR_DIRECTORY/big_report.html",
    resource_handling_options=resource_options
)
```

*Почему это важно*: Передача `resource_handling_options` в `HTMLDocument` интегрирует ограничение глубины непосредственно в движок парсинга. Парсер автоматически прекратит обход, как только будет достигнут предел, что **prevents infinite recursion**.

### Шаг 3: Безопасно парсить документ

После загрузки документа вы можете обходить DOM. Пример ниже извлекает все заголовки (`<h1>`‑`<h3>`), не превышая ограничение глубины.

```python
def extract_headings(node, current_depth=0):
    """
    Recursively collect heading text while respecting the max handling depth.
    """
    if current_depth > resource_options.max_handling_depth:
        return []  # Prevent infinite recursion by aborting deeper calls

    headings = []
    if node.tag_name in ("h1", "h2", "h3"):
        headings.append(node.text_content.strip())

    for child in node.children:
        headings.extend(extract_headings(child, current_depth + 1))
    return headings

# Start traversal from the root element
all_headings = extract_headings(html_doc.root)
print("Collected headings:", all_headings)
```

**Ожидаемый вывод (пример)**:

```
Collected headings: ['Executive Summary', 'Methodology', 'Results', 'Conclusion']
```

Защита `if current_depth > resource_options.max_handling_depth` является механизмом **how to limit depth**, который останавливает дальнейшую рекурсию. Этот шаблон работает с любыми данными в виде дерева, а не только с HTML.

## Как загрузить HTML‑документ с пользовательскими параметрами

Если вам необходимо изменить глубину для конкретного файла, просто измените `max_handling_depth` перед созданием `HTMLDocument`.

```python
resource_options.max_handling_depth = 5   # Allow deeper nesting for this file
html_doc = HTMLDocument("another_report.html", resource_handling_options=resource_options)
```

Изменение предела полезно, когда вы знаете, что документ содержит легитимное глубокое вложение (например, вложенные таблицы). Тот же код всё равно **prevent infinite recursion**, поскольку предел применяется во время выполнения.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Missing `resource_handling_options`** | Парсер следует каждому ресурсу, что приводит к неограниченной рекурсии. | Всегда передавайте экземпляр `ResourceHandlingOptions` при создании `HTMLDocument`. |
| **Setting `max_handling_depth` too low** | Важный контент может быть пропущен, потому что парсер останавливается слишком рано. | Протестируйте на репрезентативном образце и выберите глубину, балансирующую безопасность и полноту. |
| **Recursive function without depth check** | Пользовательские обходы могут всё ещё рекурсировать бесконечно, даже если парсер останавливается. | Включите ту же проверку глубины (`if current_depth > max_depth: return`) в каждый рекурсивный вспомогательный метод. |
| **Assuming all nodes have `children`** | Текстовые узлы могут не иметь атрибута `children`, вызывая ошибки атрибутов. | Защищайте проверкой `hasattr(node, "children")` или используйте блок try/except. |

Устранение этих проблем гарантирует, что ваше решение **how to parse html** останется надёжным при работе с разнообразными входными данными.

## Полный, исполняемый пример

Ниже представлен полный скрипт, который вы можете скопировать и вставить в файл с именем `parse_report.py`. Он демонстрирует весь процесс от создания параметров до извлечения заголовков.

```python
# parse_report.py
from htmlhandler import ResourceHandlingOptions, HTMLDocument

def main():
    # ---- Step 1: configure depth limit ----
    resource_options = ResourceHandlingOptions()
    resource_options.max_handling_depth = 3   # adjust as needed

    # ---- Step 2: load the HTML document ----
    html_path = "YOUR_DIRECTORY/big_report.html"
    html_doc = HTMLDocument(html_path, resource_handling_options=resource_options)

    # ---- Step 3: recursive extraction with safety guard ----
    def extract_headings(node, current_depth=0):
        if current_depth > resource_options.max_handling_depth:
            return []  # stop deeper recursion

        headings = []
        if node.tag_name in ("h1", "h2", "h3"):
            headings.append(node.text_content.strip())

        # Safely iterate over children if they exist
        if hasattr(node, "children"):
            for child in node.children:
                headings.extend(extract_headings(child, current_depth + 1))
        return headings

    # Run extraction starting from the document root
    headings = extract_headings(html_doc.root)
    print("Collected headings:", headings)

if __name__ == "__main__":
    main()
```

Запустите скрипт:

```bash
python parse_report.py
```

Вы должны увидеть список заголовков, выведенный в консоль, что подтверждает, что парсер учёл ограничение глубины и **prevented infinite recursion**.

## Следующие шаги

* **Parse other elements** – адаптируйте `extract_headings` для сбора таблиц, ссылок или изображений.
* **Stream large files** – используйте инкрементный парсинг (`HTMLDocument.stream`) при работе с многогигабайтными отчётами.
* **Integrate with asyncio** – оберните шаг загрузки в асинхронную функцию, если требуется неблокирующий ввод‑вывод.

Изучение этих тем углубит вашу способность эффективно **load html document** объектов, сохраняя полный контроль над глубиной рекурсии.

---

Следуя этому руководству, вы теперь знаете, как безопасно **how to parse html**, как **load html document** с пользовательским ограничением глубины и как **prevent infinite recursion** в любой рекурсивной обходе. Применяйте этот шаблон в своих проектах и подстраивайте настройку глубины под сложность ваших исходных файлов. Счастливого кодинга!

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, основанные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Как парсить HTML на Java – загрузка, запрос и подсчёт элементов](/html/english/java/creating-managing-html-documents/how-to-parse-html-java-load-query-count-elements/)
- [как запросить html в Java – загрузка HTML, CSS‑селектор и извлечение заголовков](/html/english/java/css-html-form-editing/how-to-query-html-in-java-load-html-css-selector-and-extract/)
- [Как редактировать дерево HTML‑документа в Aspose.HTML для Java](/html/english/java/editing-html-documents/edit-html-document-tree/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}