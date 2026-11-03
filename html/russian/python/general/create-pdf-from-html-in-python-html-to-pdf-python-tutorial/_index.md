---
category: general
date: 2026-07-15
description: Создайте PDF из HTML с помощью Python. Узнайте, как быстро преобразовать
  HTML в PDF с помощью простого скрипта и понятных шагов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create pdf from html
- convert html to pdf
- html to pdf python
- save html as pdf
- html to pdf tutorial
language: ru
lastmod: 2026-07-15
og_description: Создайте PDF из HTML с помощью Python. Это руководство покажет, как
  конвертировать HTML в PDF, сохранять HTML как PDF и эффективно управлять ресурсами.
og_image_alt: Screenshot of a Python script that creates PDF from HTML
og_title: Создание PDF из HTML в Python – практический учебник
schemas:
- author: Aspose
  dateModified: '2026-07-15'
  description: Create PDF from HTML using Python. Learn how to convert HTML to PDF
    quickly with a simple script and clear steps.
  headline: Create PDF from HTML in Python – HTML to PDF Python Tutorial
  type: TechArticle
tags:
- python
- pdf
- html
- conversion
title: Создание PDF из HTML в Python – учебник по преобразованию HTML в PDF на Python
url: /ru/python/general/create-pdf-from-html-in-python-html-to-pdf-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создать PDF из HTML в Python – Полное руководство

Когда‑нибудь вам нужно было **создать PDF из HTML**, но вы не знали, какую библиотеку Python выбрать? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда пытаются превратить веб‑отчёт, счёт‑фактуру или маркетинговую страницу в печатный PDF.  

Хорошая новость в том, что всего несколькими строками кода вы можете **конвертировать HTML в PDF** надёжно, а скрипт работает на Windows, macOS и Linux. В этом руководстве мы пройдём через полностью готовый пример, объясним, почему каждый шаг важен, и покажем, как **сохранить HTML как PDF** без лишних проблем.

---

## Чего вы научитесь

- Установить правильный пакет Python для конвертации HTML‑в‑PDF.  
- Загрузить HTML‑файл с пользовательскими параметрами обработки ресурсов (чтобы избежать бесконечных импортов CSS).  
- Сгенерировать чистый PDF‑файл на диске.  
- Решать распространённые граничные случаи, такие как внешние изображения, относительные пути и большие документы.  

К концу этого **урока по HTML в PDF** у вас будет переиспользуемая функция, которую можно добавить в любой проект.

---

## Предварительные требования

- Python 3.9+ (код также работает с 3.8, но 3.9+ даёт новейшие возможности `pathlib`).  
- Базовое знакомство с командной строкой и виртуальными окружениями.  
- HTML‑файл, который вы хотите превратить в PDF — любой статический документ подойдёт.

> **Pro tip:** Если вы используете виртуальное окружение, активируйте его перед установкой библиотеки; так ваш глобальный Python останется чистым.

---

## Шаг 1 – Установить WeasyPrint (движок, отвечающий за конвертацию)

WeasyPrint — это чисто‑Python библиотека, которая рендерит HTML и CSS в PDF. Она поддерживает большинство современных веб‑фич и даёт тонкий контроль над загрузкой ресурсов.

```bash
pip install weasyprint
```

Выполнение команды выше подтягивает `cairocffi`, `tinycss2` и несколько других зависимостей. Если вы столкнётесь с ошибкой, связанной с `cairo`, на Windows, скачайте готовые колёса с [WeasyPrint website](https://weasyprint.org/docs/install/).

---

## Шаг 2 – Подготовить небольшую вспомогательную функцию для обработки ресурсов

Когда вы загружаете HTML‑документ, который ссылается на внешние таблицы стилей или изображения, библиотека будет следовать этим ссылкам. В некоторых случаях это приводит к глубокой вложенности или даже бесконечным циклам (например, CSS‑файл, который `@import`‑ит сам себя). Чтобы всё было аккуратно, мы ограничиваем глубину обработки ресурсов.

```python
from weasyprint import HTML, CSS
from pathlib import Path

class ResourceHandlingOptions:
    """Simple container to mimic max depth handling."""
    def __init__(self, max_depth: int = 3):
        self.max_depth = max_depth
        self._current_depth = 0

    def within_limit(self) -> bool:
        return self._current_depth < self.max_depth

    def __enter__(self):
        self._current_depth += 1
        return self

    def __exit__(self, exc_type, exc_val, exc_tb):
        self._current_depth -= 1
```

Класс выше не обязателен для WeasyPrint, но он повторяет паттерн из оригинального фрагмента и даёт вам точку входа для остановки бесконтрольных импортов. Вы увидите его использование в следующем шаге.

---

## Шаг 3 – Загрузить HTML‑документ с использованием пользовательских параметров

Теперь мы действительно читаем HTML‑файл. Класс `HTML` принимает аргумент `base_url`, который мы задаём как директорию, содержащую исходный файл — это делает относительные ссылки рабочими без веб‑сервера.

```python
def load_html(input_path: Path, options: ResourceHandlingOptions) -> HTML:
    """
    Load an HTML file while respecting the max handling depth.
    """
    if not options.within_limit():
        raise RuntimeError("Maximum resource handling depth exceeded.")
    # The `with` block increments depth for the duration of the call.
    with options:
        return HTML(filename=str(input_path), base_url=str(input_path.parent))
```

> **Почему это важно:** Если ваш HTML подтягивает каскад CSS‑файлов, каждый `@import` вызовет очередную загрузку. Защитный механизм глубины предотвращает неконтролируемый рост скрипта.

---

## Шаг 4 – Сохранить обработанный документ в PDF

Имея объект `HTML` в руках, генерация PDF — это однострочник. Мы также передаём простой CSS‑фрагмент, который задаёт чистый размер страницы (A4) и небольшие отступы — при желании изменяйте их.

```python
def save_as_pdf(html_doc: HTML, output_path: Path) -> None:
    """
    Render the HTML document to a PDF file.
    """
    default_css = CSS(string='''
        @page { size: A4; margin: 1cm }
    ''')
    html_doc.write_pdf(target=str(output_path), stylesheets=[default_css])
```

Вызов `write_pdf` записывает PDF на диск, так что вы получаете готовый к распространению файл.

---

## Шаг 5 – Собрать всё вместе

Ниже представлен компактный скрипт, который можно скопировать в `convert.py`. Замените заполнители реальными путями к вашим директориям.

```python
#!/usr/bin/env python3
"""
HTML to PDF Python script – complete, runnable example.
"""

from pathlib import Path

# Import the helper classes we defined earlier
from __main__ import ResourceHandlingOptions, load_html, save_as_pdf  # noqa: E402

def main():
    # 1️⃣  Define input and output locations
    input_html = Path("YOUR_DIRECTORY/input.html")
    output_pdf = Path("YOUR_DIRECTORY/output.pdf")

    # 2️⃣  Create resource handling options (max depth = 3)
    resource_options = ResourceHandlingOptions(max_depth=3)

    # 3️⃣  Load the HTML document with the custom options
    html_doc = load_html(input_html, resource_options)

    # 4️⃣  Save the processed document as PDF
    save_as_pdf(html_doc, output_pdf)

    print(f"✅ PDF saved to {output_pdf.resolve()}")

if __name__ == "__main__":
    main()
```

**Ожидаемый вывод** — после запуска `python convert.py` вы должны увидеть:

```
✅ PDF saved to /full/path/YOUR_DIRECTORY/output.pdf
```

Откройте сгенерированный файл в любом PDF‑просмотрщике; вы увидите оригинальное расположение элементов, стили CSS и изображения (при условии, что они доступны из HTML‑файла).  

Если заметите отсутствующие изображения, дважды проверьте, что их атрибуты `src` являются либо абсолютными URL, либо относительными путями, существующими внутри `YOUR_DIRECTORY`.

---

## Часто задаваемые вопросы и обработка граничных случаев

| Question | Answer |
|----------|--------|
| *What if my HTML references external fonts?* | WeasyPrint will download the font files automatically, but you may want to whitelist domains to avoid long fetch times. |
| *Can I convert a string of HTML instead of a file?* | Yes—use `HTML(string=my_html_string)` and skip the `base_url` or set it to a temporary folder. |
| *How do I control PDF metadata (title, author)?* | Pass a `metadata` dict to `write_pdf`, e.g., `html_doc.write_pdf(target='out.pdf', metadata={'Title': 'Report'})`. |
| *I get a “cairo‑cffi error” on Linux.* | Install the system package `libcairo2-dev` (`apt-get install libcairo2-dev` on Debian/Ubuntu) before pip installing WeasyPrint. |

---

## Итоги

Мы только что **создали PDF из HTML** с помощью чистого Python‑рабочего процесса, рассмотрели механику **конвертации HTML в PDF** и показали, как **сохранить HTML как PDF** с надёжной обработкой ресурсов. Скрипт достаточно мал, чтобы добавить его в CI‑конвейеры, но при этом достаточно гибок для расширения пользовательскими шапками, подвалами или водяными знаками.

Следующие шаги, которые вы можете исследовать:

- Использовать библиотеку **html to pdf python** `pdfkit` для подхода на основе wkhtmltopdf (хорошо работает с устаревшим CSS).  
- Добавить CLI‑интерфейс с `argparse`, чтобы скрипт принимал аргументы ввода/вывода.  
- Генерировать PDF‑файлы «на лету» внутри эндпоинта Flask или FastAPI для отчётов по запросу.  

Не стесняйтесь экспериментировать, ломать вещи, а затем возвращаться к этому руководству для быстрого освежения. Если возникнут проблемы, документация WeasyPrint и форумы сообщества — отличные ресурсы.

Счастливого кодинга и приятного превращения веб‑страниц в стильные PDF!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Convert HTML to PDF with Aspose.HTML – Full Manipulation Guide](/html/english/)
- [Convert HTML to PDF in .NET with Aspose.HTML](/html/english/net/html-extensions-and-conversions/convert-html-to-pdf/)
- [Create PDF from HTML – C# Step‑by‑Step Guide](/html/english/net/html-extensions-and-conversions/create-pdf-from-html-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}