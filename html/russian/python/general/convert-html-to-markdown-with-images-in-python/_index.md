---
category: general
date: 2026-11-17
description: Преобразуйте HTML в markdown с изображениями в Python — узнайте, как
  быстро конвертировать HTML, сохраняя изображения без изменений.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to convert html
- export html with images
- markdown conversion with images
language: ru
lastmod: 2026-11-17
og_description: Преобразуйте HTML в markdown с изображениями на Python. Этот учебник
  показывает, как конвертировать HTML, экспортируя изображения, предоставляя вам полное
  готовое к использованию решение.
og_image_alt: Diagram showing convert html to markdown workflow with image extraction
og_title: Преобразовать HTML в markdown с изображениями в Python — быстрое руководство
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Convert HTML to markdown with images in Python – learn how to convert
    HTML quickly while exporting images intact.
  headline: Convert HTML to markdown with images in Python
  type: TechArticle
tags:
- HTML
- Markdown
- Python
- Image extraction
title: Преобразовать HTML в markdown с изображениями в Python
url: /ru/python/general/convert-html-to-markdown-with-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в markdown с изображениями в Python

Если вам нужно **преобразовать HTML в markdown**, сохранив изображения отдельными файлами, это руководство покажет, как это сделать. Вы получите полностью готовый пример, который обрабатывает внешние ресурсы, так что ваш markdown‑файл будет правильно ссылаться на оригинальные изображения.

Экспорт HTML с изображениями часто сбивает простые конвертеры, потому что они либо удаляют изображения, либо встраивают их как строки base64. Настроив параметры обработки ресурсов, вы сохраняете оригинальные файлы изображений и получаете чистый markdown, который можно контролировать версиями или редактировать позже.

В этом уроке вы:

* Загрузите HTML‑документ с диска.  
* Настроите конвертер для **экспорта HTML с изображениями** в виде отдельных файлов.  
* Сохраните результат как markdown, используя параметры **markdown conversion with images**.  

Единственное требование — актуальная версия библиотеки Aspose.HTML for Python (или любой совместимый API, предоставляющий `HTMLDocument`, `ResourceHandlingOptions`, `MarkdownSaveOptions` и `Converter`). Также нужен Python 3.8+ и права записи в папку вывода.

---

## Предварительные требования и установка

1. Установите пакет Aspose.HTML:

   ```bash
   pip install aspose-html
   ```

2. Проверьте установку:

   ```python
   import aspose.html as ah
   print(ah.__version__)   # should print the installed version, e.g., 22.9
   ```

> **Совет:** Используйте виртуальное окружение, чтобы избежать конфликтов версий с другими проектами.

---

## Шаг 1: Загрузка исходного HTML‑документа

Первый шаг — создать объект `HTMLDocument`, представляющий исходный файл. Этот объект разбирает разметку и строит дерево DOM, которое конвертер может обходить.

```python
from aspose.html import HTMLDocument

# Load the HTML file you want to convert
html_path = "YOUR_DIRECTORY/sample.html"
html_doc = HTMLDocument(html_path)
```

*Почему это важно* — загрузка документа дает библиотеке полный контроль над разметкой, позволяя разрешать относительные URL‑ы и позже применять обработку ресурсов.

---

## Шаг 2: Настройка обработки внешних ресурсов

Когда вы **экспортируете HTML с изображениями**, обычно требуется сохранять изображения рядом с markdown‑файлом, а не встраивать их. Класс `ResourceHandlingOptions` позволяет задать такое поведение.

```python
from aspose.html import ResourceHandlingOptions

resource_options = ResourceHandlingOptions()
resource_options.save_external_resources = True   # keep images as separate files
```

Установка `save_external_resources` в `True` инструктирует конвертер копировать каждый внешний ресурс (изображения, CSS, шрифты) в папку рядом с выводом markdown. Файл markdown будет содержать относительные ссылки, указывающие на эти копии.

---

## Шаг 3: Привязка конфигурации обработки ресурсов к параметрам markdown

`MarkdownSaveOptions` управляет процессом преобразования в markdown. Присвоив свойству `resource_handling_options` нужный объект, вы включаете функцию **markdown conversion with images**.

```python
from aspose.html import MarkdownSaveOptions

markdown_options = MarkdownSaveOptions()
markdown_options.resource_handling_options = resource_options
```

Если пропустить этот шаг, конвертер удалит ссылки на изображения или встроит их как data URI, что нейтрализует цель экспорта изображений.

---

## Шаг 4: Выполнение преобразования

Наконец, вызовите `Converter.convert`, передав исходный документ, путь назначения и подготовленные параметры.

```python
from aspose.html import Converter

output_path = "YOUR_DIRECTORY/sample.md"
Converter.convert(html_doc, output_path, markdown_options)
```

После завершения вызова вы получите:

* `sample.md` — markdown‑версия оригинального HTML.  
* Подпапку `sample_files` (или аналогичную) с каждым изображением, указанным в HTML.

---

## Полный рабочий скрипт

Собрав все части вместе, вы получаете единый скрипт, который можно запустить из командной строки:

```python
# convert_html_to_markdown.py
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, MarkdownSaveOptions, Converter

def convert_html_to_markdown(html_file: str, markdown_file: str):
    """
    Convert an HTML file to markdown while exporting images as separate files.
    """
    # 1. Load the HTML document
    html_doc = HTMLDocument(html_file)

    # 2. Set up resource handling to keep images external
    res_opts = ResourceHandlingOptions()
    res_opts.save_external_resources = True

    # 3. Attach resource handling to markdown options
    md_opts = MarkdownSaveOptions()
    md_opts.resource_handling_options = res_opts

    # 4. Convert and save
    Converter.convert(html_doc, markdown_file, md_opts)
    print(f"Conversion complete: {markdown_file}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    src_html = os.path.abspath("YOUR_DIRECTORY/sample.html")
    dst_md   = os.path.abspath("YOUR_DIRECTORY/sample.md")

    convert_html_to_markdown(src_html, dst_md)
```

**Ожидаемый вывод**

```
Conversion complete: /absolute/path/YOUR_DIRECTORY/sample.md
```

После выполнения откройте `sample.md` в любом markdown‑редакторе. Ссылки на изображения будут выглядеть так:

```markdown
![Alt text](sample_files/image1.png)
```

Сами изображения находятся в папке `sample_files`, готовой к контролю версий или дальнейшей обработке.

---

## Обработка распространённых граничных случаев

| Ситуация                              | Рекомендуемый подход |
|----------------------------------------|----------------------|
| **Отсутствующие файлы изображений**    | Конвертер выводит предупреждение и оставляет битую ссылку. Убедитесь, что все атрибуты `<img src>` указывают на доступные ресурсы перед конвертацией. |
| **Относительные URL, выходящие за пределы проекта** | Используйте `ResourceHandlingOptions.base_url`, чтобы задать базовый URL и позволить конвертеру правильно разрешать пути. |
| **Большие HTML‑файлы с множеством изображений** | Установите `resource_options.max_resource_size` (если доступно), чтобы ограничить размер копируемых ресурсов. |
| **Форматы изображений, отличные от PNG/JPEG** | Библиотека автоматически копирует оригинальный формат. Убедитесь, что целевой markdown‑просмотрщик поддерживает этот формат (например, SVG). |
| **Ошибки прав записи**                | Запустите скрипт с нужными правами или выберите директорию вывода, где у вас есть права записи. |

---

## Советы для гладкой **markdown conversion with images**

* Держите папку вывода чистой: удаляйте директорию `*_files` перед каждой запуском, если хотите получить свежий набор изображений.  
* Используйте осмысленные атрибуты `alt` в исходном HTML; они автоматически становятся подписью к изображениям в markdown.  
* Если нужно встроить изображения как base64 (для единого markdown‑файла), установите `resource_options.save_external_resources = False`. Это противоположно **export html with images**, но полезно для email‑сообщений или встраиваемой документации.  
* При конвертации пакета файлов оберните скрипт в цикл и настройте `resource_options.resource_folder`, чтобы избежать конфликтов имён.

---

## Часто задаваемые вопросы

**В: Работает ли это с HTML‑фрагментами, у которых нет полного `<html>`‑обёртки?**  
О: Да. `HTMLDocument` может парсить фрагменты; конвертер обрабатывает их как обычный документ.

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to embed images in HTML to Markdown conversion using Python](/html/english/python/general/how-to-embed-images-in-html-to-markdown-conversion-using-pyt/)
- [Convert HTML to Markdown – Complete Guide with CSS & Images](/html/english/python/general/convert-html-to-markdown-complete-guide-with-css-images/)
- [Convert HTML to Markdown with Aspose – Complete Python Guide](/html/english/python/general/convert-html-to-markdown-with-aspose-complete-python-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}