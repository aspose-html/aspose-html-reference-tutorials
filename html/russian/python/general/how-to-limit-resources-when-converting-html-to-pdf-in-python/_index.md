---
category: general
date: 2026-08-15
description: Как ограничить ресурсы при преобразовании HTML в PDF с помощью Python.
  Узнайте, как экспортировать HTML в PDF с контролируемой глубиной ресурсов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to limit resources
- convert html to pdf
- export html to pdf
- save html as pdf
- how to convert html
language: ru
lastmod: 2026-08-15
og_description: Как ограничить ресурсы при конвертации HTML в PDF на Python. Это руководство
  покажет, как безопасно экспортировать HTML в PDF, ограничивая глубину связанных
  ресурсов.
og_image_alt: Screenshot of Python code converting an HTML file to a PDF with limited
  resource handling
og_title: Как ограничить ресурсы при конвертации HTML в PDF на Python
schemas:
- author: Aspose
  dateModified: '2026-08-15'
  description: How to limit resources while converting HTML to PDF using Python. Learn
    to export HTML to PDF with controlled resource depth.
  headline: How to limit resources when converting HTML to PDF in Python
  type: TechArticle
tags:
- HTML to PDF
- Python
- Resource handling
title: Как ограничить ресурсы при конвертации HTML в PDF на Python
url: /ru/python/general/how-to-limit-resources-when-converting-html-to-pdf-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как ограничить ресурсы при конвертации HTML в PDF на Python

Если вам нужно **ограничить ресурсы** во время преобразования HTML‑в‑PDF, это руководство предоставляет готовое решение, готовое к запуску. Настраивая обработку ресурсов, вы предотвращаете глубокое скачивание ссылок, загрузку больших изображений или бесконечное выполнение скриптов, что делает конвертацию быстрой и предсказуемой.

Вы также узнаете, как **конвертировать HTML в PDF**, **экспортировать HTML в PDF** и **сохранить HTML как PDF** с помощью единого, хорошо структурированного скрипта. Внешняя документация не требуется — просто следуйте инструкциям ниже.

## Что понадобится

* Python 3.9 или новее  
* Пакет `aspose.html` (библиотека, предоставляющая `HTMLDocument`, `ResourceHandlingOptions` и `PdfSaveOptions`)  
* HTML‑файл, который вы хотите конвертировать (например, `big_page.html`)  

Наличие этих предварительных условий гарантирует, что код выполнится без дополнительной настройки.

## Шаг 1: Установите пакет Aspose.HTML

```bash
pip install aspose-html
```

Пакет `aspose-html` поставляет классы, используемые для загрузки, конфигурирования и сохранения документов. Установив его один раз, вы удовлетворяете все последующие импорты.

## Шаг 2: Загрузите HTML‑документ, который хотите конвертировать

```python
from aspose.html import HTMLDocument

# Load the source HTML file
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

`HTMLDocument` разбирает файл и создает DOM в памяти. Этот объект является точкой входа для любой конвертации, будь то **конвертация HTML в PDF** или отображение в браузере.

## Шаг 3: Настройте обработку ресурсов (как ограничить ресурсы)

```python
from aspose.html.drawing import ResourceHandlingOptions

# Create a resource handling options object
res_opts = ResourceHandlingOptions()
# Limit the depth of linked resources to three levels
res_opts.max_handling_depth = 3
```

Установка `max_handling_depth` сообщает движку прекращать следовать по ссылкам после трёх переходов. Это и есть ядро **ограничения ресурсов**: более глубокие ресурсы игнорируются, предотвращая бесконтрольные сетевые запросы или огромные затраты памяти. Регулируйте значение в соответствии с политиками безопасности или производительности вашего проекта.

### Почему стоит ограничивать ресурсы?

* **Безопасность** — Предотвращает загрузку внешних скриптов, которые могут выполнить нежелательный код.  
* **Производительность** — Сокращает трафик и нагрузку на CPU, когда исходная страница ссылается на множество изображений или таблиц стилей.  
* **Предсказуемость** — Гарантирует завершение конвертации в известный временной интервал.

## Шаг 4: Привяжите параметры ресурсов к настройкам сохранения PDF

```python
from aspose.html.saving import PdfSaveOptions

# Create PDF save options and attach the resource handling configuration
pdf_opts = PdfSaveOptions()
pdf_opts.resource_handling_options = res_opts
```

`PdfSaveOptions` объединяет все параметры для окончательного экспорта. Связывая `resource_handling_options`, вы обеспечиваете, что шаг **экспорта HTML в PDF** учитывает установленный лимит глубины.

## Шаг 5: Экспортируйте HTML в PDF (сохраните HTML как PDF)

```python
# Save the document as a PDF file using the configured options
doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_opts)
```

Вызов `save` записывает PDF на диск. Эта строка демонстрирует **как конвертировать HTML** в переносимый документ, соблюдая ограничения ресурсов. Полученный файл `big_page.pdf` содержит только ресурсы, попавшие в разрешённую глубину.

## Шаг 6: Проверьте сгенерированный PDF

Откройте `big_page.pdf` в любом PDF‑просмотрщике. Вы должны увидеть оригинальное расположение страницы, но внешние ресурсы за пределами трёх переходов будут отсутствовать. Если заметите недостающие изображения или стили, рассмотрите возможность увеличения `max_handling_depth` или встраивания этих ресурсов непосредственно в HTML.

### Общий чек‑лист проверки

| Проверка | Ожидаемый результат |
|----------|----------------------|
| Текст отображается корректно | Весь текстовый контент из исходного HTML присутствует |
| Основные изображения загружаются | Изображения, указанные в пределах трех уровней, видимы |
| Нет сетевых запросов после конвертации | Используйте сетевой монитор, чтобы убедиться, что дополнительных запросов не происходит |

## Пограничные случаи и практические советы

| Ситуация | Рекомендованное решение |
|----------|--------------------------|
| **Отсутствует локальный файл** | Оберните создание `HTMLDocument` в блок `try/except FileNotFoundError` и выведите понятное сообщение об ошибке. |
| **Очень большие изображения** | Сочетайте `max_handling_depth` с `max_image_resolution` в `PdfSaveOptions`, чтобы уменьшить разрешение громоздких графических файлов. |
| **Динамический JavaScript‑контент** | Установите `pdf_opts.enable_javascript = False`, если нужен чисто статический экспорт без выполнения скриптов. |
| **Относительные URL** | Убедитесь, что `doc.base_url` указывает на каталог, содержащий HTML‑файл, чтобы относительные ссылки разрешались корректно. |

## Полный скрипт, который можно скопировать и вставить

```python
# -------------------------------------------------------------
# Full example: limit resources while converting HTML to PDF
# -------------------------------------------------------------
# pip install aspose-html   # Run once before execution
# -------------------------------------------------------------

from aspose.html import HTMLDocument
from aspose.html.drawing import ResourceHandlingOptions
from aspose.html.saving import PdfSaveOptions

def convert_html_to_pdf(
    html_path: str,
    pdf_path: str,
    max_depth: int = 3
) -> None:
    """
    Converts an HTML file to PDF while limiting the depth of linked resources.

    Args:
        html_path: Path to the source .html file.
        pdf_path: Destination path for the generated .pdf file.
        max_depth: Maximum depth for resource handling (default = 3).
    """
    # Load the HTML document
    doc = HTMLDocument(html_path)

    # Configure resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = max_depth

    # Attach resource options to PDF save settings
    pdf_opts = PdfSaveOptions()
    pdf_opts.resource_handling_options = res_opts

    # Export HTML to PDF
    doc.save(pdf_path, pdf_opts)

if __name__ == "__main__":
    # Example usage
    convert_html_to_pdf(
        html_path="YOUR_DIRECTORY/big_page.html",
        pdf_path="YOUR_DIRECTORY/big_page.pdf",
        max_depth=3
    )
```

Запуск этого скрипта создаст `big_page.pdf` в том же каталоге, применяя правило **ограничения ресурсов**, которое вы задали. Функцию `convert_html_to_pdf` можно переиспользовать в более крупных проектах, упрощая **сохранение HTML как PDF** с едиными настройками.

## Заключение

Теперь вы знаете, **как ограничить ресурсы** при **конвертации HTML в PDF** с помощью Python. В руководстве рассмотрены установка библиотеки, загрузка HTML, настройка `ResourceHandlingOptions`, привязка этих параметров к `PdfSaveOptions` и, наконец, **экспорт HTML в PDF**. Управляя `max_handling_depth`, вы защищаете приложение от избыточного сетевого трафика и непредсказуемого времени конвертации.

Далее изучайте связанные темы, такие как **как конвертировать HTML** с пользовательским CSS, встраивание шрифтов или массовая генерация PDF‑файлов. Настройка других параметров `PdfSaveOptions` (например, размер страницы, сжатие) позволяет точно подогнать вывод под счета, отчёты или электронные книги.

Не бойтесь экспериментировать с различными значениями глубины, комбинировать этот подход с безголовыми браузерами или интегрировать его в веб‑сервис, который возвращает PDF‑файлы по запросу. Приятного кодинга!

## Что изучать дальше?

Следующие учебные материалы охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [How to Save HTML in C# – Complete Guide Using a Custom Resource Handler](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Create HTML Document with Styled Text and Export to PDF – Full Guide](/html/english/net/html-extensions-and-conversions/create-html-document-with-styled-text-and-export-to-pdf-full/)
- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}