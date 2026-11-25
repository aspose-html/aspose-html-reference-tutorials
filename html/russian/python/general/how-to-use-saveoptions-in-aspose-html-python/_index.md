---
category: general
date: 2026-07-27
description: Как использовать SaveOptions в Aspose.HTML (Python) для конвертации большой
  HTML‑страницы и эффективного управления ресурсами.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use SaveOptions
- convert large html page
- apply resource handling
- Aspose.HTML Python
- HTML resource handling
language: ru
lastmod: 2026-07-27
og_description: Как использовать SaveOptions в Aspose.HTML (Python) позволяет конвертировать
  большие HTML‑страницы, применяя обработку ресурсов для чистых и быстрых результатов.
og_image_alt: Screenshot illustrating how to use SaveOptions in Aspose.HTML for Python
og_title: Как использовать SaveOptions в Aspose.HTML — руководство по Python
schemas:
- author: Aspose
  dateModified: '2026-07-27'
  description: How to use SaveOptions in Aspose.HTML (Python) to convert large HTML
    page and apply resource handling efficiently.
  headline: How to Use SaveOptions in Aspose.HTML (Python)
  type: TechArticle
- questions:
  - answer: Aspose.HTML follows redirects but won’t send credentials automatically.
      You can pre‑download those assets or use a custom `WebRequest` handler (beyond
      this guide’s scope).
    question: What if the page references resources over HTTPS that require authentication?
  - answer: Yes—set `resource_options.max_handling_depth = 0`. This skips external
      files but leaves any `<style>` blocks intact.
    question: Can I preserve inline CSS while stripping external files?
  - answer: After saving, you can run a secondary pass with Pillow to downscale images,
      or let Aspose.HTML’s built‑in image compression options handle it (use `save_options.image_quality`).
    question: What about very large images that still bloat the output?
  - answer: The limit is global across all resource types (images, scripts, styles).
      If you need granular control, you’d have to filter resources manually after
      loading the document.
    question: Is the depth limit applied per‑resource type?
  type: FAQPage
tags:
- Aspose.HTML
- Python
- HTML processing
title: Как использовать SaveOptions в Aspose.HTML (Python)
url: /ru/python/general/how-to-use-saveoptions-in-aspose-html-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать SaveOptions в Aspose.HTML (Python)

Как использовать SaveOptions в Aspise.HTML для Python — вопрос, который задают многие разработчики, работающие с огромными HTML‑файлами. Если вам нужно **конвертировать большую HTML‑страницу**, одновременно контролируя **обработку ресурсов**, вы попали в нужное место.  

В этом руководстве мы пройдем реальный сценарий: возьмём громоздкую HTML‑страницу, ограничим глубину вложенности загружаемых ресурсов и, наконец, сохраним (или конвертируем) результат с кристально‑чётким контролем. Никаких расплывчатых ссылок, только полностью готовый пример, который вы можете скопировать‑вставить в свой проект уже сегодня.

> **Pro tip:** `SaveOptions` в Aspose.HTML работает не только для сохранения обратно в HTML, но и для конвертации в PDF, PNG или даже DOCX. Тот же шаблон, который мы рассматриваем ниже, применим ко всем этим форматам.

---

## Что понадобится

- **Python 3.8+** (код использует подсказки типов, но работает на любой современной версии)  
- **Aspose.HTML for Python via .NET** — установить через `pip install aspose-html`  
- **Большой HTML‑файл**, который вы хотите уменьшить или преобразовать (в примере используется `big_page.html`)  
- Небольшой объём свободного места на диске для выходного файла  

Вот и всё — никаких дополнительных библиотек, никаких тяжёлых инструментов сборки.

---

## Как использовать SaveOptions с параметрами обработки ресурсов

Это суть дела. Мы создаём экземпляр `SaveOptions`, прикрепляем к нему объект `ResourceHandlingOptions`, который указывает Aspose.HTML, насколько глубоко следует искать связанные ресурсы, а затем передаём всё в метод `save` документа.

```python
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

# Load the source HTML document
input_path = "YOUR_DIRECTORY/big_page.html"
doc = HTMLDocument(input_path)

# Define how deep nested resources should be processed (limit to 3 levels)
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # <-- controls depth of resource fetching

# Attach the resource handling configuration to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# Save the processed document (or convert to another format if desired)
output_path = "YOUR_DIRECTORY/big_page_processed.html"
doc.save(output_path, save_options)
```

**Почему это работает:**  
- `HTMLDocument` загружает исходный файл, разбирая каждый `<img>`, `<link>`, `<script>` и т.д.  
- `ResourceHandlingOptions.max_handling_depth` сообщает движку прекратить поиск ресурсов после трёх уровней вложенности — идеальный способ избежать бесконечных циклов на страницах, которые встраивают другие страницы.  
- `SaveOptions` — это контейнер, который несёт как формат вывода (по умолчанию HTML), так и правила обработки ресурсов.  
- Наконец, `doc.save` записывает новый файл, применяя только что заданные правила.

Запустив скрипт, вы получите новый файл `big_page_processed.html`. Откройте его в браузере; вы заметите, что все изображения, стили и скрипты до трёх уровней вложенности сохранены, а более глубокие ссылки удалены. Это резко уменьшает размер файла, не ломая базовую разметку страницы — именно то, что нужно, когда вы **конвертируете большую HTML‑страницу** для офлайн‑использования или отправки по электронной почте.

---

## Эффективно конвертировать большую HTML‑страницу

Если ваша цель — *конвертировать большую HTML‑страницу* в более лёгкую версию, приведённый выше фрагмент уже делает большую часть работы. Однако вы можете захотеть полностью изменить формат вывода. Aspose.HTML делает это одной строкой:

```python
# Convert to PDF instead of HTML
pdf_save_options = SaveOptions()
pdf_save_options.resource_handling_options = resource_options
pdf_save_options.format = "PDF"   # specify desired format

doc.save("YOUR_DIRECTORY/big_page.pdf", pdf_save_options)
```

Просто замените свойство `format` на `"PNG"`, `"JPEG"` или `"DOCX"`, и у вас будет полноценный конвертер. Те же правила **обработки ресурсов** остаются в силе, поэтому полученный PDF не будет встраивать каждый внешний CSS‑файл оригинального сайта — только те, что находятся в пределах трёхуровневой глубины, которую вы задали.

---

## Применение обработки ресурсов к вложенным ресурсам

Разберём подробнее, как эффективно использовать **обработку ресурсов**. Предположим, ваш HTML содержит таблицу стилей, которая сама импортирует другие таблицы, а те, в свою очередь, подгружают изображения. Без ограничения глубины Aspose.HTML может бесконечно следовать по цепочке, раздувая память и нагрузку на CPU.

```python
# Example: limit to 1 level for aggressive trimming
resource_options.max_handling_depth = 1
save_options.resource_handling_options = resource_options
doc.save("trimmed_page.html", save_options)
```

- **Глубина 0** — внешние ресурсы не загружаются; вы получаете голый HTML‑скелет.  
- **Глубина 1** — включаются только ресурсы первого уровня (прямые `<img>`‑теги, непосредственные CSS‑файлы).  
- **Глубина 2+** — учитывается более глубокая вложенность, полезно для сложных сайтов, где стили зависят от других стилей.

Выберите глубину, соответствующую вашему сценарию **конвертации большой HTML‑страницы**. Для email‑рассылок часто достаточно глубины 1. Для локального архива глубина 3 (как в основном примере) обеспечивает хороший баланс.

---

## Полный рабочий пример — от начала до конца

Ниже представлен автономный скрипт, который можно сохранить в файл `process_html.py`. В нём реализована обработка ошибок, логирование и небольшая вспомогательная функция, выводящая степень уменьшения размера.

```python
import os
from aspose.html import HTMLDocument, ResourceHandlingOptions, SaveOptions

def process_html(
    src_path: str,
    dst_path: str,
    depth: int = 3,
    fmt: str = "HTML"
) -> None:
    """
    Loads an HTML file, applies resource handling, and saves it in the requested format.
    Returns nothing; prints size statistics for quick verification.
    """
    if not os.path.isfile(src_path):
        raise FileNotFoundError(f"Source file not found: {src_path}")

    # Load document
    doc = HTMLDocument(src_path)

    # Set up resource handling
    res_opts = ResourceHandlingOptions()
    res_opts.max_handling_depth = depth

    # Configure save options (including format)
    save_opts = SaveOptions()
    save_opts.resource_handling_options = res_opts
    save_opts.format = fmt.upper()   # Aspose expects upper‑case format strings

    # Perform save / conversion
    doc.save(dst_path, save_opts)

    # Report size change
    original = os.path.getsize(src_path)
    final = os.path.getsize(dst_path)
    reduction = (original - final) / original * 100
    print(f"Saved {fmt.lower()} to '{dst_path}'. Size reduced by {reduction:.2f}%.")

# -------------------------------------------------------------------------
# Example usage
if __name__ == "__main__":
    input_file = "YOUR_DIRECTORY/big_page.html"
    output_file = "YOUR_DIRECTORY/big_page_processed.html"

    process_html(
        src_path=input_file,
        dst_path=output_file,
        depth=3,          # apply resource handling up to three levels
        fmt="HTML"       # change to "PDF" or "PNG" to convert format
    )
```

**Ожидаемый вывод (консоль):**

```
Saved html to 'YOUR_DIRECTORY/big_page_processed.html'. Size reduced by 42.57%.
```

Откройте обработанный файл; вы увидите более лёгкую страницу, которая всё ещё выглядит как оригинал. Если вы измените `fmt` на `"PDF"`, консоль отобразит размер PDF‑файла, и его можно открыть в любом PDF‑просмотрщике.

---

## Часто задаваемые вопросы и особые случаи

- **Что делать, если страница ссылается на ресурсы по HTTPS, требующие аутентификации?**  
  Aspose.HTML следует перенаправлениям, но не отправляет учётные данные автоматически. Вы можете предварительно скачать такие ресурсы или использовать собственный обработчик `WebRequest` (выходит за рамки данного руководства).

- **Можно ли сохранить встроенный CSS, удалив внешние файлы?**  
  Да — установите `resource_options.max_handling_depth = 0`. Это пропустит внешние файлы, но оставит любые блоки `<style>` нетронутыми.

- **А как насчёт очень больших изображений, которые всё ещё «тянут» размер вывода?**  
  После сохранения можно выполнить дополнительный проход с Pillow для уменьшения размеров изображений, либо воспользоваться встроенными опциями сжатия изображений Aspose.HTML (используйте `save_options.image_quality`).

- **Применяется ли ограничение глубины отдельно к каждому типу ресурса?**  
  Ограничение глобальное для всех типов ресурсов (изображения, скрипты, стили). Если нужна более тонкая настройка, придётся фильтровать ресурсы вручную после загрузки документа.

---

## Заключение

Теперь вы знаете, **как использовать SaveOptions** в Aspose.HTML


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Convert HTML to PDF Java – Using Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [How to Convert HTML to MHTML with Aspose.HTML for Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-mhtml/)
- [How to Use Aspose to Render HTML to PNG – Step‑by‑Step Guide](/html/english/net/rendering-html-documents/how-to-use-aspose-to-render-html-to-png-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}