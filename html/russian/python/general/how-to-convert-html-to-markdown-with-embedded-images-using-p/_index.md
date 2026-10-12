---
category: general
date: 2026-10-12
description: Быстро преобразуйте HTML в markdown и узнайте, как вставлять изображения
  в markdown. Это руководство подробно рассматривает конвертацию HTML в markdown с
  помощью Python, включая полный код.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to markdown
- how to embed images in markdown
- html to markdown conversion python
- how to convert html page to markdown
language: ru
lastmod: 2026-10-12
og_description: Конвертируйте HTML в markdown и встраивайте изображения в markdown
  с помощью Python. Следуйте этому полному руководству для надёжного преобразования
  HTML в markdown на Python.
og_image_alt: Screenshot showing a Python script that converts an HTML file to a markdown
  file with base64‑encoded images
og_title: Конвертировать HTML в markdown с встроенными изображениями в Python — пошаговое
  руководство
schemas:
- author: GroupDocs
  dateModified: '2026-10-12'
  description: convert HTML to markdown quickly and learn how to embed images in markdown.
    This guide walks through html to markdown conversion python with full code.
  headline: How to convert HTML to markdown with embedded images using Python
  type: TechArticle
tags:
- markdown
- html
- python
- document conversion
title: Как конвертировать HTML в markdown с встроенными изображениями с помощью Python
url: /ru/python/general/how-to-convert-html-to-markdown-with-embedded-images-using-p/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как конвертировать HTML в markdown с вложенными изображениями с помощью Python

Если вам нужно **конвертировать HTML в markdown** с сохранением всех изображений, это руководство покажет, как это сделать. Настроив движок конвертации на встраивание изображений в формате Base64, вы получаете один самодостаточный файл `.md`, который работает везде — от README‑ов на GitHub до статических генераторов сайтов.

Вы также узнаете **как встраивать изображения в markdown**, почему встроенные параметры обработки ресурсов являются самым надёжным выбором, и как выполнить **html to markdown conversion python** всего в несколько строк кода.

## Что вы получите

- Преобразовать любую локальную HTML‑страницу в чистый документ Markdown.  
- Встроить каждое изображение непосредственно в файл Markdown в виде строки Base64, устраняя битые ссылки.  
- Запустить процесс на любой платформе, поддерживающей Python 3.9+ и библиотеку GroupDocs Conversion.

## Предварительные требования

| Требование | Причина |
|------------|--------|
| Python 3.9 или новее | Требуется SDK GroupDocs Conversion. |
| `groupdocs-conversion` пакет | Предоставляет `Converter`, `HTMLDocument`, `MarkdownSaveOptions` и `ResourceHandlingOptions`. |
| Существующий HTML‑файл (например, `page.html`) | Исходный файл, который вы хотите конвертировать. |
| Права записи в папку вывода | Для сохранения сгенерированного файла `.md`. |

Install the SDK with pip:

```bash
pip install groupdocs-conversion
```

> **Совет:** Используйте виртуальное окружение (`python -m venv .venv`), чтобы изолировать зависимости.

## Шаг 1: Настройте обработку ресурсов для встраивания изображений в markdown

Когда движок конвертации встречает тег `<img>`, он может либо скопировать изображение в отдельную папку, либо встроить его напрямую. Встраивание создаёт закодированный в Base64 data URI, что именно требуется для **how to embed images in markdown**.

```python
from groupdocs.conversion import ResourceHandlingOptions

# Create a resource handling configuration
resource_options = ResourceHandlingOptions()
# Enable embedding of images as Base64 data URIs
resource_options.embed_images = True   # Embeds images directly in the Markdown file
```

**Почему это важно:**  
Встраивание гарантирует, что файл Markdown остаётся портативным. Если вы поделитесь файлом `.md` без сопутствующей папки с изображениями, изображения всё равно будут корректно отображаться на любой платформе, поддерживающей data URI (GitHub, GitLab, предпросмотр VS Code и т.д.).

## Шаг 2: Настройте параметры сохранения Markdown, используя конфигурацию ресурсов

Класс `MarkdownSaveOptions` позволяет передать `resource_options`, созданные выше. Он также позволяет точно настроить окончания строк, стили заголовков и многое другое, но в большинстве случаев значения по умолчанию работают отлично.

```python
from groupdocs.conversion import MarkdownSaveOptions

# Attach the resource handling to the markdown save options
markdown_options = MarkdownSaveOptions(resource_handling_options=resource_options)
```

**Что происходит под капотом:**  
Во время конвертации движок сканирует DOM HTML, преобразует каждый элемент в его эквивалент в Markdown и заменяет `<img src="...">` на `![alt text](data:image/...;base64,...)`. Флаг `resource_options.embed_images` инициирует это поведение.

## Шаг 3: Конвертировать HTML‑документ в markdown и сохранить результат

Теперь вы связываете всё вместе: загружаете исходный HTML, применяете параметры сохранения и записываете файл вывода.

```python
from groupdocs.conversion import Converter, HTMLDocument

# Path to the source HTML file
source_path = "YOUR_DIRECTORY/page.html"
# Desired output path for the markdown file
output_path = "YOUR_DIRECTORY/page.md"

# Perform the conversion
Converter.convert_html(
    HTMLDocument(source_path),
    markdown_options,
    output_path
)

print(f"✅ Conversion complete! Markdown saved to: {output_path}")
```

**Ожидаемый результат:**  

- `page.md` содержит текст Markdown, заголовки, списки и **встроенные изображения** в виде строк Base64.  
- Открытие `page.md` в просмотрщике Markdown отображает оригинальную разметку HTML, включая все изображения, без каких-либо внешних ресурсов.

### Полный скрипт для быстрого копирования

```python
# convert_html_to_markdown.py
from groupdocs.conversion import (
    Converter,
    HTMLDocument,
    MarkdownSaveOptions,
    ResourceHandlingOptions,
)

def convert_html_to_markdown(src_html: str, dst_md: str) -> None:
    """Convert an HTML file to markdown with images embedded as Base64."""
    # 1️⃣ Embed images
    resource_opts = ResourceHandlingOptions()
    resource_opts.embed_images = True

    # 2️⃣ Prepare markdown options
    md_opts = MarkdownSaveOptions(resource_handling_options=resource_opts)

    # 3️⃣ Run conversion
    Converter.convert_html(
        HTMLDocument(src_html),
        md_opts,
        dst_md
    )
    print(f"✅ Markdown file created at: {dst_md}")

if __name__ == "__main__":
    # Adjust these paths to your environment
    convert_html_to_markdown(
        src_html="YOUR_DIRECTORY/page.html",
        dst_md="YOUR_DIRECTORY/page.md"
    )
```

Run the script:

```bash
python convert_html_to_markdown.py
```

## Обработка распространённых граничных случаев

| Ситуация | Решение |
|-----------|----------|
| **Большие изображения вызывают огромные файлы markdown** | Ограничьте размер изображения перед встраиванием, изменив его размер в HTML или используя библиотеку оптимизации изображений (например, Pillow) перед конвертацией. |
| **Относительные URL‑ы изображений указывают за пределы проекта** | Убедитесь, что ссылки в HTML доступны, либо скопируйте эти изображения в ту же папку перед конвертацией. |
| **Вам нужны отдельные файлы изображений вместо встраивания** | Установите `resource_options.embed_images = False` и укажите путь `resource_folder`, куда будут сохраняться изображения. |
| **Конвертация не удаётся из‑за некорректного HTML** | Предварительно обработайте HTML с помощью `BeautifulSoup` (парсер `html5lib`), чтобы очистить битые теги перед передачей их конвертеру. |

## Проверка результата

Open the generated `page.md` in any Markdown viewer:

```bash
code YOUR_DIRECTORY/page.md   # VS Code preview
```

Вы должны увидеть оригинальные заголовки, абзацы и изображения, отрисованные корректно. Если изображение отображается как битая ссылка, проверьте, что `embed_images` установлен в `True` и что исходный HTML содержит корректные теги `<img>`.

## Следующие шаги и связанные темы

- **Экспорт в другие форматы** — тот же класс `Converter` может создавать PDF, DOCX или обычный текст. Замените `MarkdownSaveOptions` на `PdfSaveOptions` или `DocxSaveOptions`.  
- **Пакетная обработка** — пройдитесь по каталогу HTML‑файлов, чтобы создать набор документов Markdown.  
- **Настройка обработки изображений** — реализуйте обратный вызов через `ResourceHandlingOptions`, чтобы сохранять изображения в CDN и заменять data URI на URL CDN.  
- **Продвинутые возможности markdown** — включите markdown в стиле GitHub (таблицы, списки задач), настроив свойства `markdown_options`.

Освоив **html to markdown conversion python**, вы теперь имеете повторяемый, готовый к продакшену процесс, который гарантирует, что изображения остаются вместе с контентом. Не стесняйтесь экспериментировать с приведёнными выше параметрами и адаптировать скрипт под свои конвейеры контента.

---

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Конвертировать HTML в Markdown в .NET с Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-markdown/)
- [Конвертировать HTML в Markdown в Aspose.HTML для Java](/html/english/java/saving-html-documents/convert-html-to-markdown/)
- [Создать PDF из Markdown с помощью Aspose HTML Converter (Java)](/html/english/java/conversion-html-to-other-formats/create-pdf-from-markdown-using-aspose-html-converter-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}