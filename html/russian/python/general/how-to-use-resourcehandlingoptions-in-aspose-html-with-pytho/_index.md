---
category: general
date: 2026-11-24
description: Узнайте, как использовать ResourceHandlingOptions в Aspose.HTML для Python,
  чтобы управлять обработкой ресурсов HTML, ограничивать глубину рекурсии и сохранять
  обработанный файл.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use resourcehandlingoptions in aspose
- Aspose.HTML Python
- HTMLDocument processing
- limit recursion depth
- resource handling options
- save processed HTML
language: ru
lastmod: 2026-11-24
og_description: Используйте ResourceHandlingOptions в Aspose.HTML для Python, чтобы
  безопасно обрабатывать большие HTML‑файлы, ограничивать глубину рекурсии и сохранять
  очищенный результат.
og_image_alt: Diagram showing use ResourceHandlingOptions in Aspose to control HTML
  resource handling
og_title: Как использовать ResourceHandlingOptions в Aspose.HTML с Python
schemas:
- author: Aspose
  dateModified: '2026-11-24'
  description: Learn how to use ResourceHandlingOptions in Aspose.HTML for Python
    to control HTML resource handling, limit recursion depth, and save a processed
    file.
  headline: How to use ResourceHandlingOptions in Aspose.HTML with Python
  type: TechArticle
tags:
- Aspose
- Python
- HTML processing
title: Как использовать ResourceHandlingOptions в Aspose.HTML с Python
url: /ru/python/general/how-to-use-resourcehandlingoptions-in-aspose-html-with-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать ResourceHandlingOptions в Aspose.HTML с Python

Если вам нужно **использовать ResourceHandlingOptions в Aspose** для Python, это руководство покажет вам полное, готовое к запуску решение. Управление обработкой ресурсов предотвращает бесконтрольную рекурсию при обработке больших или сложных HTML‑страниц, а нижеописанные шаги позволяют безопасно применить эту опцию и проверить результат.

Вы узнаете, как настроить **resource handling options**, загрузить HTML‑документ с этими настройками и сохранить обработанный вывод. В руководстве также рассматриваются распространённые подводные камни, такие как циклические ссылки и отсутствующие ресурсы, чтобы вы могли адаптировать код к любому проекту, использующему **HTMLDocument processing**.

## Предварительные требования

Перед началом убедитесь, что у вас есть:

- Установлен Python 3.8 или новее.
- Действительная лицензия Aspose.HTML for Python (бесплатная оценочная версия подходит для тестирования).
- Выполнена команда `pip install aspose-html` в вашем виртуальном окружении.
- HTML‑файл (`big.html`), который вы хотите обработать.

Эти требования гарантируют, что пример запустится без дополнительной настройки.

## Шаг 1: Установить Aspose.HTML для Python

```bash
pip install aspose-html
```

Выполнение команды устанавливает пакет **Aspose.HTML Python** и все его зависимости. Библиотека предоставляет `HTMLDocument`, `ResourceHandlingOptions` и другие классы, необходимые для **HTMLDocument processing**.

## Шаг 2: Импортировать необходимые классы

```python
# Import the core classes needed for resource handling and document loading
from aspose.html import ResourceHandlingOptions, HTMLDocument
```

Импорт `ResourceHandlingOptions` даёт доступ к объекту **resource handling options**, а `HTMLDocument` является точкой входа для загрузки и сохранения HTML‑файлов.

## Шаг 3: Настроить ResourceHandlingOptions

```python
# Create an options instance that limits how deep the engine will follow linked resources
resource_options = ResourceHandlingOptions(max_handling_depth=5)
```

**Почему это важно:**  
Когда HTML‑страница ссылается на другие страницы, изображения или скрипты, Aspose.HTML может рекурсивно следовать этим ссылкам. Без ограничения злоумышленный или плохо построенный сайт может вызвать бесконечный цикл. Установка `max_handling_depth` в `5` (или любое значение, подходящее вашему сценарию) **ограничивает глубину рекурсии**, защищая приложение от чрезмерного потребления памяти.

> **Pro tip:** Если вы знаете, что ваши документы никогда не вложены глубже трёх уровней, установите `max_handling_depth=3`, чтобы сократить время обработки.

## Шаг 4: Загрузить HTML‑документ с настроенными параметрами

```python
# Load the source HTML file while applying the resource handling options
doc = HTMLDocument(
    "YOUR_DIRECTORY/big.html",
    resource_handling_options=resource_options
)
```

Передача `resource_handling_options` в конструктор сообщает Aspose.HTML учитывать ограничение глубины при разборе. Этот шаг необходим для **использования ResourceHandlingOptions в Aspose**; без него по‑умолчанию может сохраняться неограниченная рекурсия.

## Шаг 5: Сохранить обработанный документ

```python
# Save the processed HTML to a new file; the output reflects any resources that were trimmed
doc.save("YOUR_DIRECTORY/big_processed.html")
```

Метод `save` записывает очищенную разметку на диск. Полученный файл (`big_processed.html`) содержит только те ресурсы, которые были успешно обработаны в пределах указанной глубины, что делает его безопасным для публикации или дальнейшей обработки.

## Шаг 6: Проверить результат (необязательно, но рекомендуется)

```python
# Quick verification: read the saved file and print the first 200 characters
with open("YOUR_DIRECTORY/big_processed.html", "r", encoding="utf-8") as f:
    print(f.read()[:200])
```

Запуск этого фрагмента подтверждает, что файл создан и содержимое выглядит ожидаемо. Если вывод пустой или в нём отсутствуют важные элементы, рассмотрите возможность увеличения `max_handling_depth` или проверьте исходный HTML на предмет битых ссылок.

## Распространённые граничные случаи и как с ними работать

| Ситуация                              | Рекомендуемая настройка                                 |
|----------------------------------------|--------------------------------------------------------|
| **Циклические ссылки** (A → B → A)    | Установите `max_handling_depth` в небольшое значение (например, 2).     |
| **Отсутствующие внешние ресурсы**         | Используйте `resource_options.ignore_missing_resources = True`, чтобы пропустить ошибки. |
| **Большие HTML‑файлы (> 100 MB)**         | Увеличьте лимит памяти процесса с помощью `ResourceHandlingOptions(max_memory_usage=…)`. |
| **Требуется обрабатывать только встроенный CSS/JS** | Отключите обработку внешних ресурсов: `resource_options.handle_external_resources = False`. |

Эти варианты демонстрируют гибкость **resource handling options** и помогают адаптировать решение под различные требования проекта.

## Полный рабочий пример

Ниже приведён полный скрипт, который можно скопировать в файл с именем `process_html.py`. Замените `YOUR_DIRECTORY` реальным путём к вашим файлам.

```python
# process_html.py
# Complete example showing how to use ResourceHandlingOptions in Aspose.HTML for Python

from aspose.html import ResourceHandlingOptions, HTMLDocument

# ----------------------------------------------------------------------
# Step 1: Configure resource handling – limit recursion depth to 5 levels
# ----------------------------------------------------------------------
resource_options = ResourceHandlingOptions(max_handling_depth=5)

# ----------------------------------------------------------------------
# Step 2: Load the source HTML document with the configured options
# ----------------------------------------------------------------------
doc = HTMLDocument(
    "YOUR_DIRECTORY/big.html",               # Path to the original HTML file
    resource_handling_options=resource_options
)

# ----------------------------------------------------------------------
# Step 3: Save the processed HTML to a new location
# ----------------------------------------------------------------------
doc.save("YOUR_DIRECTORY/big_processed.html")

# ----------------------------------------------------------------------
# Optional verification step
# ----------------------------------------------------------------------
if __name__ == "__main__":
    with open("YOUR_DIRECTORY/big_processed.html", "r", encoding="utf-8") as f:
        print("First 200 characters of the processed file:")
        print(f.read()[:200])
```

Запуск `python process_html.py` создаёт `big_processed.html`, при этом безопасно соблюдая установленный вами предел рекурсии с помощью **ResourceHandlingOptions**.

## Заключение

Теперь вы знаете, как **использовать ResourceHandlingOptions в Aspose** для контроля обработки HTML‑ресурсов, ограничения глубины рекурсии и **надёжного сохранения обработанных HTML**‑файлов. Такой подход защищает приложение от бесконечных циклов, снижает потребление памяти и даёт тонкий контроль над тем, как внешние ресурсы обрабатываются во время **HTMLDocument processing**.

### Что дальше?

- Поэкспериментировать с другими **resource handling options**, такими как `ignore_missing_resources` или `handle_external_resources`.
- Сочетать эту технику с возможностями **CSS/JS inlining** Aspose.HTML для создания полностью автономных страниц.
- Изучить API **Aspose.HTML Python** для конвертации в PDF, рендеринга изображений или манипуляций DOM, чтобы расширить рабочий процесс.

Не стесняйтесь адаптировать пример для пакетной обработки нескольких файлов или интегрировать его в веб‑службу, которая очищает пользовательский HTML. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Ограничение глубины ресурсов HTML с Aspose.HTML для Python – Полное руководство](/html/english/python/general/limit-html-resource-depth-with-aspose-html-for-python-comple/)
- [Как установить max_handling_depth в Aspose.HTML Python – Полное руководство](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [Как ограничить вложенные ресурсы при обработке HTML с Aspose.HTML для Python](/html/english/python/general/how-to-limit-nested-resources-when-processing-html-with-aspo/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}