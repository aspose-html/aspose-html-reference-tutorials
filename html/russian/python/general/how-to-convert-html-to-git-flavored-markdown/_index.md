---
category: general
date: 2026-11-17
description: Как быстро преобразовать HTML в Markdown в стиле Git, извлекая заголовки,
  ссылки и таблицы, при этом эффективно обрабатывая большие HTML‑файлы.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to convert html
- extract headings from html
- html to git markdown
- convert large html
language: ru
lastmod: 2026-11-17
og_description: Как конвертировать HTML в Markdown в стиле Git, извлекать заголовки,
  ссылки и таблицы, а также обрабатывать большие HTML‑файлы с правильным управлением
  ресурсами.
og_image_alt: Screenshot showing how to convert HTML to Git‑flavored Markdown using
  code options
og_title: Как конвертировать HTML в Markdown в стиле Git – полное руководство
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: How to convert HTML to Git‑flavored Markdown quickly, extracting headings,
    links, and tables while handling large HTML files efficiently.
  headline: How to convert HTML to Git‑flavored Markdown
  type: TechArticle
- description: How to convert HTML to Git‑flavored Markdown quickly, extracting headings,
    links, and tables while handling large HTML files efficiently.
  name: How to convert HTML to Git‑flavored Markdown
  steps:
  - name: '**`HTMLDocument`** – loads the source HTML while respecting a maximum resource‑handling
      depth.'
    text: '**`HTMLDocument`** – loads the source HTML while respecting a maximum resource‑handling
      depth.'
  - name: '**`MarkdownSaveOptions`** – tells the converter which markdown features
      to keep and which formatter to use.'
    text: '**`MarkdownSaveOptions`** – tells the converter which markdown features
      to keep and which formatter to use.'
  - name: '**`ResourceHandlingOptions`** – controls how external assets such as images
      are saved.'
    text: '**`ResourceHandlingOptions`** – controls how external assets such as images
      are saved.'
  type: HowTo
tags:
- HTML conversion
- Markdown
- Git‑flavored markdown
- Resource handling
title: Как преобразовать HTML в Markdown, поддерживаемый Git
url: /ru/python/general/how-to-convert-html-to-git-flavored-markdown/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как конвертировать HTML в Git‑flavored Markdown

Если вам нужно **how to convert html** в чистый файл Git‑flavored Markdown, это руководство покажет вам точные шаги. Вы узнаете, как оставить только заголовки, ссылки и таблицы, ограничить глубину вложения ресурсов для огромных страниц и сохранять внешние изображения в отдельной папке.

В этом руководстве рассматривается всё, что необходимо для конвертации больших HTML‑документов, извлечения заголовков из HTML и создания markdown, который безупречно работает с рендерингом GitHub‑flavored.

## Как конвертировать HTML в Git‑flavored Markdown

Процесс конвертации вращается вокруг трёх объектов:

1. **`HTMLDocument`** – загружает исходный HTML, учитывая максимальную глубину обработки ресурсов.
2. **`MarkdownSaveOptions`** – указывает конвертеру, какие функции markdown сохранять и какой форматтер использовать.
3. **`ResourceHandlingOptions`** – управляет тем, как сохраняются внешние ресурсы, такие как изображения.

Настраивая эти объекты перед вызовом `Converter.convert`, вы получаете детерминированный markdown‑вывод, содержащий только те элементы, которые вам нужны.

```python
# Step 1: Limit resource nesting depth while loading the HTML document
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 3
html_doc = HTMLDocument(
    "YOUR_DIRECTORY/huge_page.html",
    ResourceHandlingOptions=resource_opts
)
```

**Почему это важно:**  
Большие HTML‑страницы часто содержат скрипты, iframe или глубоко вложенный CSS, что может привести к бесконечной рекурсии парсера. Установка `max_handling_depth` в небольшое значение (например, 3) предотвращает неконтролируемое использование памяти и ускоряет фазу загрузки, что особенно важно при **convert large html** файлах.

## Извлечение заголовков из HTML с помощью MarkdownSaveOptions

Следующий шаг указывает конвертеру сохранять только необходимые функции markdown. Для большинства процессов документирования вам нужны заголовки, ссылки и таблицы.

```python
# Step 2: Set up Markdown conversion to Git‑flavored format and keep only headings, links, and tables
markdown_opts = MarkdownSaveOptions()
markdown_opts.formatter = MarkdownSaveOptions.Formatter.GIT
markdown_opts.features = (
    MarkdownSaveOptions.Feature.HEADER |
    MarkdownSaveOptions.Feature.LINK |
    MarkdownSaveOptions.Feature.TABLE
)
```

**Почему это важно:**  
`features`‑флаг работает как фильтр. Включив `HEADER`, вы автоматически **extract headings from html** и преобразуете их в `#`, `##` и т.д., что является ядром любой markdown‑структуры. Добавление `LINK` и `TABLE` гарантирует сохранение навигации и данных, в то время как всё остальное (скрипты, стили, комментарии) удаляется.

## Эффективная конвертация больших HTML

При работе с массивными страницами вы можете опасаться, что конвертация завершится тайм‑аутом или создаст огромный markdown‑файл. Приведённая выше конфигурация уже устраняет большинство проблем с производительностью, но несколько дополнительных советов помогут оставаться в безопасности:

* **Process in chunks** – Если исходный HTML превышает несколько сотен мегабайт, разбейте его на логические секции перед конвертацией.
* **Use streaming I/O** – Метод `Converter.convert` записывает напрямую в целевой файл, избегая копии всего markdown в памяти.
* **Monitor resource usage** – Включите логирование в `ResourceHandlingOptions`, чтобы увидеть, сколько внешних файлов обрабатывается.

Эти практики делают процесс надёжным для сценария **convert large html**.

## Настройка обработки внешних изображений

Git‑flavored markdown отображает изображения, находящиеся в репозитории. Чтобы markdown оставался чистым, сохраняйте каждое внешнее изображение как отдельный файл в папке `assets` и ссылайтесь на него относительным путём.

```python
# Step 3: Configure external image handling – save them as separate files in the "assets" folder
markdown_resource_opts = ResourceHandlingOptions()
markdown_resource_opts.save_external_resources = True
markdown_opts.resource_handling_options = markdown_resource_opts
```

**Почему это важно:**  
Когда `save_external_resources` установлено в `True`, конвертер загружает каждый тег `<img>`, сохраняет файл изображения в `assets/` и соответственно переписывает markdown‑ссылку на изображение. Это создаёт автономный репозиторий, который работает на GitHub, GitLab или любом генераторе статических сайтов.

## Выполнение конвертации

После подготовки всех параметров окончательный вызов записывает markdown‑файл.

```python
# Step 4: Convert the HTML document to Markdown using the configured options
Converter.convert(html_doc, "YOUR_DIRECTORY/output.md", markdown_opts)
```

**Ожидаемый вывод:**  

```markdown
# Main Title

## Section One

Some introductory text with a [link](https://example.com).

| Header 1 | Header 2 |
|----------|----------|
| Cell A1  | Cell B1  |

![Image description](assets/image1.png)
```

Файл содержит только заголовки, ссылки и таблицы, а каждое внешнее изображение находится в папке `assets/`.

## Полный рабочий пример

Ниже представлен единый скрипт, который вы можете добавить в свой проект. Замените пути‑заполнители на свои реальные каталоги.

```python
# -*- coding: utf-8 -*-

from aspose.html import HTMLDocument, Converter, MarkdownSaveOptions, ResourceHandlingOptions

# ----------------------------------------------------------------------
# 1. Load the HTML file with a safe resource‑handling depth
# ----------------------------------------------------------------------
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 3          # Prevent deep recursion on huge pages
html_doc = HTMLDocument(
    "YOUR_DIRECTORY/huge_page.html",
    ResourceHandlingOptions=resource_opts
)

# ----------------------------------------------------------------------
# 2. Define markdown options – Git‑flavored, keep only needed features
# ----------------------------------------------------------------------
markdown_opts = MarkdownSaveOptions()
markdown_opts.formatter = MarkdownSaveOptions.Formatter.GIT
markdown_opts.features = (
    MarkdownSaveOptions.Feature.HEADER |
    MarkdownSaveOptions.Feature.LINK |
    MarkdownSaveOptions.Feature.TABLE
)

# ----------------------------------------------------------------------
# 3. Save external images into an assets folder
# ----------------------------------------------------------------------
image_opts = ResourceHandlingOptions()
image_opts.save_external_resources = True
markdown_opts.resource_handling_options = image_opts

# ----------------------------------------------------------------------
# 4. Run the conversion
# ----------------------------------------------------------------------
Converter.convert(html_doc, "YOUR_DIRECTORY/output.md", markdown_opts)

print("Conversion complete. Markdown saved to output.md")
```

Запустите скрипт с Python 3.8+ и последней библиотекой Aspose.HTML for Python. После выполнения вы найдёте `output.md` и каталог `assets/` рядом с ним.

## Часто задаваемые вопросы и особые случаи

| Question | Answer |
|----------|--------|
| **Что если HTML содержит относительные URL изображений?** | Конвертер разрешает их относительно местоположения HTML‑файла перед загрузкой. Убедитесь, что исходный каталог доступен. |
| **Могу ли я сохранить дополнительные функции markdown (например, блоки кода)?** | Расширьте `markdown_opts.features` добавив `MarkdownSaveOptions.Feature.CODE`, чтобы сохранить секции кода в виде блоков. |
| **Как полностью убрать изображения?** | Установите `image_opts.save_external_resources = False`. Теги `<img>` будут удалены из вывода. |
| **Совместим ли вывод с другими вариантами markdown?** | `GIT`‑форматтер следует правилам GitHub‑flavored markdown, которые являются надмножеством CommonMark. Для чистого CommonMark используйте `MarkdownSaveOptions.Formatter.COMMONMARK`. |
| **Что если HTML некорректен?** | Парсер Aspose.HTML толерантен и попытается исправить повреждённую разметку. Однако сильно испорченные файлы могут потребовать предварительной обработки с помощью инструмента HTML tidy. |

## Заключение

Теперь вы знаете **how to convert html** в чистый Git‑flavored markdown, извлекаете заголовки из HTML и эффективно обрабатываете сценарии **convert large html**. Ограничивая глубину ресурсов, выбирая только необходимые функции markdown и настраивая обработку внешних изображений, конвертация становится быстрой, надёжной и готовой к рабочим процессам контроля версий.

### Следующие шаги

* Исследуйте варианты **html to git markdown**, такие как пользовательские стили маркеров или обработка сносок.  
* Объедините этот конвейер с CI‑задачей, которая автоматически конвертирует страницы документации при каждом коммите.  
* Поэкспериментируйте с флагами `ResourceHandlingOptions`, чтобы фильтровать скрипты, стили или другие нежелательные ресурсы.

Удачной конвертации, и не стесняйтесь адаптировать скрипт под конкретные нужды вашего проекта!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как конвертировать HTML в Markdown с GitLab‑flavored markdown на Python](/html/english/python/general/how-to-convert-html-to-markdown-with-gitlab-flavored-markdow/)
- [Как экспортировать ссылки при конвертации HTML в Markdown](/html/english/python/general/how-to-export-links-while-converting-html-to-markdown/)
- [Как использовать Aspose – конвертировать HTML в Markdown и извлекать ссылки](/html/english/python/general/how-to-use-aspose-convert-html-to-markdown-and-extract-links/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}