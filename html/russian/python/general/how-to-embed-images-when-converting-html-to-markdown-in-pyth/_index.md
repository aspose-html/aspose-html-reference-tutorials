---
category: general
date: 2026-10-09
description: Узнайте, как встраивать изображения при преобразовании HTML в Markdown
  в Python с помощью Aspose.HTML. Включает встраивание изображений в виде Base64 и
  markdown с встроенными изображениями.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed images
- convert html to markdown
- html to markdown python
- embed images as base64
- markdown with embedded images
language: ru
lastmod: 2026-10-09
og_description: Как встраивать изображения при конвертации HTML в Markdown на Python.
  Это руководство показывает, как встраивать изображения в виде Base64 и генерировать
  markdown с встроенными изображениями.
og_image_alt: Screenshot of a Markdown file that contains embedded images generated
  by a Python HTML‑to‑Markdown conversion
og_title: Как вставлять изображения при конвертации HTML в Markdown на Python
schemas:
- author: Aspose
  dateModified: '2026-10-09'
  description: Learn how to embed images while converting HTML to Markdown in Python
    using Aspose.HTML. Includes embed images as Base64 and markdown with embedded
    images.
  headline: How to embed images when converting HTML to Markdown in Python
  type: TechArticle
- description: Learn how to embed images while converting HTML to Markdown in Python
    using Aspose.HTML. Includes embed images as Base64 and markdown with embedded
    images.
  name: How to embed images when converting HTML to Markdown in Python
  steps:
  - name: '**Resize images before conversion** – Use Pillow (`pip install pillow`)
      to shrink images to a reasonable resolution (e.g., 800 px width) before embedding.'
    text: '**Resize images before conversion** – Use Pillow (`pip install pillow`)
      to shrink images to a reasonable resolution (e.g., 800 px width) before embedding.'
  - name: '**Limit embedding to specific formats** – If you only need PNGs embedded,
      adjust `resource_opts` to filter by MIME type:'
    text: '**Limit embedding to specific formats** – If you only need PNGs embedded,
      adjust `resource_opts` to filter by MIME type:'
  - name: Import Aspose.HTML classes and create `MarkdownSaveOptions`.
    text: Import Aspose.HTML classes and create `MarkdownSaveOptions`.
  - name: Set `ResourceHandlingOptions.embed_resources` and `embed_images_as_base64`
      to `True`.
    text: Set `ResourceHandlingOptions.embed_resources` and `embed_images_as_base64`
      to `True`.
  - name: Attach those options to the markdown save settings.
    text: Attach those options to the markdown save settings.
  - name: Call `Converter.convert` with the source HTML and destination Markdown paths.
    text: Call `Converter.convert` with the source HTML and destination Markdown paths.
  type: HowTo
tags:
- Python
- Aspose.HTML
- Markdown conversion
- Image embedding
title: Как встраивать изображения при конвертации HTML в Markdown на Python
url: /ru/python/general/how-to-embed-images-when-converting-html-to-markdown-in-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как внедрять изображения при конвертации HTML в Markdown на Python

Если вам нужно **внедрять изображения** во время конвертации HTML‑в‑Markdown, это руководство предоставляет готовое решение, которое можно сразу запустить. С помощью Aspose.HTML for Python вы можете внедрять изображения как строки Base‑64, поэтому полученный файл Markdown будет содержать изображения встроенными. Это устраняет битые ссылки и делает документ переносимым.

Помимо внедрения изображений, в руководстве показано, как **конвертировать HTML в Markdown** в «питонистском» стиле, охватывая процесс *html to markdown python*, настройку **embed images as Base64** и создание **markdown with embedded images**, который работает в любом просмотрщике Markdown.

К концу этой статьи у вас будет один скрипт, который:

* Считывает HTML‑файл с диска.  
* Встраивает каждое упомянутое изображение непосредственно в вывод Markdown в виде Base‑64 data URI.  
* Сохраняет готовый файл Markdown, готовый к распространению или контролю версий.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

* Python 3.8 или новее.  
* Действующая лицензия Aspose.HTML for Python (бесплатная пробная версия подходит для оценки).  
* Выполненная команда `pip install aspose-html` в вашем виртуальном окружении.  
* HTML‑файл (`input.html`), содержащий ссылки на локальные или удалённые изображения.

Если чего‑то не хватает, установите это сейчас, чтобы избежать ошибок во время выполнения.

## Шаг 1: Настройка окружения Aspose.HTML

Сначала импортируйте необходимые классы и создайте экземпляр `MarkdownSaveOptions`. Объект `MarkdownSaveOptions` хранит параметры конвертации, включая опции обработки ресурсов, которые мы настроим позже.

```python
# Step 1: Import required Aspose.HTML classes
from aspose.html import Converter, ResourceHandlingOptions, MarkdownSaveOptions

# Initialize Markdown save options (you can customize other settings here)
markdown_opts = MarkdownSaveOptions()
```

**Почему этот шаг важен:**  
`Converter` выполняет основную работу, а `MarkdownSaveOptions` указывает конвертеру, как обращаться с ресурсами, такими как изображения, скрипты и таблицы стилей. Без инициализации `markdown_opts` вы не сможете прикрепить конфигурацию обработки ресурсов, которая позволяет внедрять изображения.

## Шаг 2: Настройка обработки ресурсов для внедрения изображений как Base64

Aspose.HTML предоставляет `ResourceHandlingOptions`. Установка `embed_resources = True` сообщает конвертеру заменять внешние ссылки на изображения Base‑64 data URI.

```python
# Step 2: Create and configure resource handling options
resource_opts = ResourceHandlingOptions()
resource_opts.embed_resources = True          # Embed images directly in the output
resource_opts.embed_images_as_base64 = True   # Explicitly request Base64 encoding for images

# Attach the resource options to the markdown save options
markdown_opts.resource_handling_options = resource_opts
```

**Почему этот шаг важен:**  
Когда `embed_resources` равно `True`, конвертер сканирует HTML в поисках тегов `<img>`, загружает каждое изображение, кодирует его и вставляет URI вида `data:image/...;base64,` в Markdown. Это создаёт **markdown with embedded images**, что идеально подходит для документации, которой необходимо перемещаться вместе с исходным файлом (например, в репозитории Git).

## Шаг 3: Выполнение конвертации из HTML в Markdown

Теперь можно вызвать `Converter.convert`, передав путь к исходному HTML, путь к целевому Markdown и настроенный `markdown_opts`.

```python
# Step 3: Define source and destination paths
html_path = "YOUR_DIRECTORY/input.html"
markdown_path = "YOUR_DIRECTORY/with_images.md"

# Step 4: Convert HTML to Markdown, embedding images
Converter.convert(html_path, markdown_path, markdown_opts)
```

**Почему этот шаг важен:**  
`Converter.convert` читает HTML, обрабатывает все ресурсы согласно заданным опциям и записывает файл Markdown, содержащий тот же визуальный контент — включая изображения — без внешних зависимостей.

## Шаг 4: Проверка сгенерированного Markdown

Откройте `with_images.md` в любом просмотрщике Markdown (VS Code, GitHub, Typora и т.д.). Вы должны увидеть изображения, отрендеренные точно так же, как в оригинальном HTML. Ссылки на изображения будут выглядеть примерно так:

```markdown
![Alt text](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA...)
```

Если в просмотрщике отображаются битые изображения, проверьте следующее:

* В оригинальном HTML ссылки на изображения доступны (локальные файлы существуют, удалённые URL‑адреса доступны).  
* Флаг `embed_images_as_base64` установлен в `True`.  

## Шаг 5: Работа с большими изображениями и вопросы производительности

Внедрение очень больших изображений может значительно увеличить размер файла Markdown. Вот два практических совета:

1. **Измените размер изображений перед конвертацией** — используйте Pillow (`pip install pillow`), чтобы уменьшить изображения до разумного разрешения (например, ширина 800 px) перед внедрением.  
2. **Ограничьте внедрение определёнными форматами** — если нужны только PNG, скорректируйте `resource_opts`, чтобы фильтровать по MIME‑типу:

```python
resource_opts.allowed_image_formats = ["png"]  # Only embed PNG images
```

Эти настройки позволяют сохранять Markdown лёгким, одновременно обеспечивая необходимую портативность.

## Распространённые подводные камни и способы их устранения

| Проблема | Причина | Решение |
|----------|---------|----------|
| Изображения отображаются как битые ссылки | `embed_resources` оставлен `False` | Убедитесь, что `resource_opts.embed_resources = True`. |
| Размер файла Markdown > 10 МБ | Очень большие изображения высокого разрешения | Уменьшите размер изображений или внедряйте только необходимые. |
| Удалённые изображения не внедряются | Таймаут сети или заблокированный URL | Проверьте подключение к интернету или скачайте изображения локально перед конвертацией. |
| Неправильные символы в строке Base64 | Бинарный файл считан некорректно | Убедитесь, что файлы изображений не повреждены и имеют правильные права доступа. |

## Расширение решения: пакетная конвертация нескольких HTML‑файлов

Если нужно обработать папку с HTML‑файлами, оберните логику конвертации в цикл:

```python
import os

input_dir = "YOUR_DIRECTORY/html_files"
output_dir = "YOUR_DIRECTORY/markdown_output"

for filename in os.listdir(input_dir):
    if filename.lower().endswith(".html"):
        src_path = os.path.join(input_dir, filename)
        dst_path = os.path.join(output_dir, os.path.splitext(filename)[0] + ".md")
        Converter.convert(src_path, dst_path, markdown_opts)
        print(f"Converted {filename} → {os.path.basename(dst_path)}")
```

Этот фрагмент демонстрирует **convert html to markdown** в масштабе, сохраняя поведение **embed images as base64** для каждого файла.

## Итоги

Теперь вы знаете, **как внедрять изображения**, когда **конвертируете HTML в Markdown** с помощью Python. Ключевые шаги:

1. Импортировать классы Aspose.HTML и создать `MarkdownSaveOptions`.  
2. Установить `ResourceHandlingOptions.embed_resources` и `embed_images_as_base64` в `True`.  
3. Привязать эти опции к настройкам сохранения Markdown.  
4. Вызвать `Converter.convert`, указав путь к исходному HTML и путь к целевому Markdown.  

В результате вы получаете **markdown with embedded images**, который можно распространять без опасений о недостающих ресурсах.

## Следующие шаги

* Исследуйте другие параметры `ResourceHandlingOptions`, такие как `embed_stylesheets`, если нужны встроенные CSS.  
* Скомбинируйте этот рабочий процесс со статическим генератором сайтов (например, MkDocs) для построения конвейеров документации.  
* Поэкспериментируйте с различными форматами изображений и уровнями сжатия, чтобы найти баланс между качеством и размером файла.

Не стесняйтесь адаптировать скрипт под требования вашего проекта, и приятного кодинга!

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы реализации в ваших проектах.

- [Как задать смещение при конвертации HTML в Markdown на Java](/html/english/java/conversion-html-to-other-formats/how-to-set-offset-when-converting-html-to-markdown-in-java/)
- [Конвертация markdown в html – руководство для Java с выводом PDF](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html-java-guide-with-pdf-output/)
- [Markdown в HTML на Java — конвертация с Aspose.HTML](/html/english/java/conversion-html-to-other-formats/convert-markdown-to-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}