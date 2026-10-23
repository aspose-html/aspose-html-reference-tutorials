---
category: general
date: 2026-10-21
description: Узнайте, как быстро преобразовать HTML в PNG. В этом руководстве также
  рассматривается экспорт веб‑страницы в PNG и конвертация HTML‑файла в PNG с помощью
  Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert html to png
- export webpage to png
- how to convert html to image
- convert html file to png
language: ru
lastmod: 2026-10-21
og_description: Преобразуйте HTML в PNG с помощью Python. Следуйте этому понятному
  руководству, чтобы экспортировать веб‑страницу в PNG, обрабатывать особые случаи
  и автоматизировать генерацию изображений.
og_image_alt: Screenshot of HTML page converted to PNG using Python
og_title: Конвертировать HTML в PNG на Python — полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  headline: How to convert HTML to PNG in Python – step‑by‑step guide
  type: TechArticle
- description: Learn how to convert HTML to PNG quickly. This tutorial also covers
    export webpage to PNG and convert HTML file to PNG with Python.
  name: How to convert HTML to PNG in Python – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the script prints:'
  - name: Why adjust viewport size?
    text: Web pages designed for desktop screens often look cramped if rendered at
      a small width. By increasing the `width` and `height` options, you capture the
      full layout, which is especially useful for **export webpage to PNG** tasks.
  - name: 6.1 Large pages or infinite scroll
    text: 'For pages that load content lazily (e.g., infinite scroll), increase the
      JavaScript delay and optionally set a larger viewport:'
  - name: 6.2 Authentication‑protected pages
    text: 'If a page requires a session cookie, you can embed the cookie header:'
  - name: 6.3 Missing images or fonts
    text: '`wkhtmltoimage` respects the `--disable-local-file-access` flag for security.
      If your HTML references local assets, enable them explicitly:'
  type: HowTo
tags:
- python
- html conversion
- image processing
- web automation
title: Как конвертировать HTML в PNG на Python – пошаговое руководство
url: /ru/python/general/how-to-convert-html-to-png-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Конвертация HTML в PNG на Python — полное руководство по программированию

Если вам нужно **конвертировать HTML в PNG**, это руководство покажет надёжный способ сделать это с помощью чистого Python. Независимо от того, экспортируете ли вы статический отчёт, создаёте миниатюры для галереи или автоматизируете скриншоты для тестирования, вы получите полностью готовое решение, которое можно запустить за несколько минут.

Вы также увидите, как **export webpage to PNG**, поймёте разницу между конвертацией HTML‑файла и живого URL, и узнаете лучшие практики работы с большими страницами или динамическим контентом. Внешние сервисы не требуются — только несколько пакетов Python и короткий скрипт.

## Требования

- Установлен Python 3.9+ (код работает на Windows, macOS и Linux)
- Доступ к терминалу или командной строке
- Базовые знания менеджера пакетов Python (`pip`)

Вам понадобится пакет `imgkit` (тонкая обёртка над `wkhtmltoimage`) и сам бинарный файл `wkhtmltoimage`. Оба бесплатны и с открытым исходным кодом.

## Шаг 1: Установите необходимые инструменты

Первый шаг — установить `wkhtmltoimage` и Python‑обёртку, которая взаимодействует с ним.

```bash
# Install wkhtmltoimage (Linux example)
sudo apt-get update && sudo apt-get install -y wkhtmltopdf

# On macOS using Homebrew
brew install wkhtmltopdf

# On Windows download the installer from:
# https://wkhtmltopdf.org/downloads.html
# and add the installation folder to your PATH.

# Install the Python wrapper
pip install imgkit
```

> **Почему этот шаг важен** – `wkhtmltoimage` рендерит HTML с использованием движка WebKit, создавая пиксельно‑точные PNG. `imgkit` просто передаёт ваши параметры в бинарный файл, поэтому вы получаете такое же качество, как в браузере.

## Шаг 2: Проверьте установку

Запустите быструю проверку, чтобы убедиться, что бинарный файл доступен из Python.

```python
import imgkit

# This will raise an exception if wkhtmltoimage is not found
print("wkhtmltoimage version:", imgkit.config().wkhtmltoimage)
```

Если скрипт выводит путь к `wkhtmltoimage`, вы готовы конвертировать HTML в PNG. Если появляется `OSError`, проверьте, что бинарный файл находится в `PATH` вашей системы.

## Шаг 3: Напишите переиспользуемую функцию конвертации

Инкапсуляция логики в функции упрощает **convert HTML file to PNG** или **export webpage to PNG** из любой части вашего проекта.

```python
import os
import imgkit

def convert_html_to_png(source, output_path, *, options=None):
    """
    Convert an HTML file or URL to a PNG image.

    Parameters
    ----------
    source : str
        Path to a local HTML file (e.g., "report.html") or a URL
        (e.g., "https://example.com").
    output_path : str
        Destination file path for the PNG (e.g., "report.png").
    options : dict, optional
        imgkit options such as viewport size, zoom factor, or
        JavaScript delay. If omitted, sensible defaults are used.

    Returns
    -------
    bool
        True if the conversion succeeded, False otherwise.
    """
    # Use a default set of options if none are provided
    default_options = {
        "format": "png",
        "quality": "100",
        "encoding": "UTF-8",
        "quiet": "",
        # Render at 1280×720 – adjust for your layout
        "width": 1280,
        "height": 720,
        # Wait for JavaScript to finish (ms)
        "javascript-delay": 500,
    }
    # Merge user‑supplied options over defaults
    final_options = {**default_options, **(options or {})}

    try:
        # imgkit can handle both files and URLs transparently
        imgkit.from_file(source, output_path, options=final_options) \
            if os.path.isfile(source) else \
            imgkit.from_url(source, output_path, options=final_options)
        print(f"✅ Successfully saved PNG to: {output_path}")
        return True
    except Exception as e:
        print(f"❌ Conversion failed: {e}")
        return False
```

> **Почему мы оборачиваем и `from_file`, и `from_url`** – Теперь одна функция поддерживает **how to convert HTML to image** для локальных файлов и живых веб‑страниц, делая ваш код DRY (Don’t Repeat Yourself).

## Шаг 4: Конвертировать локальный HTML‑файл в PNG

Поместите HTML‑файл с именем `sample.html` в папку `assets`. Затем вызовите вспомогательную функцию, которую мы только что определили:

```python
if __name__ == "__main__":
    # Example: convert a static HTML file
    html_path = os.path.join("assets", "sample.html")
    png_path = os.path.join("output", "sample.png")

    # Ensure the output directory exists
    os.makedirs(os.path.dirname(png_path), exist_ok=True)

    # Perform the conversion
    success = convert_html_to_png(html_path, png_path)

    if success:
        # Show a tiny preview in the console (optional)
        from PIL import Image
        img = Image.open(png_path)
        img.thumbnail((200, 200))
        img.show()
```

### Ожидаемый вывод

Запуск скрипта выводит:

```
✅ Successfully saved PNG to: output/sample.png
```

Новый файл `output/sample.png` теперь содержит пиксельно‑точный снимок `sample.html`. Открытие его в любом просмотрщике изображений покажет отрендеренную страницу точно так, как она выглядела бы в браузере.

## Шаг 5: Экспортировать живую веб‑страницу в PNG

Если вам нужно **export webpage to PNG** для URL, который часто меняется (например, дашборд), просто передайте строку URL вместо пути к файлу.

```python
# Example: convert a live page
url = "https://developer.mozilla.org/en-US/docs/Web/HTML"
output_file = "output/mdn_homepage.png"

convert_html_to_png(url, output_file, options={"width": 1920, "height": 1080})
```

### Почему стоит менять размер области просмотра?

Веб‑страницы, разработанные для настольных экранов, часто выглядят сжатыми при рендеринге в небольшой ширине. Увеличивая параметры `width` и `height`, вы захватываете полную раскладку, что особенно полезно для задач **export webpage to PNG**.

## Шаг 6: Обработка распространённых граничных случаев

### 6.1 Большие страницы или бесконечная прокрутка

Для страниц, которые загружают контент лениво (например, бесконечная прокрутка), увеличьте задержку JavaScript и при необходимости задайте большую область просмотра:

```python
options = {
    "javascript-delay": 2000,   # wait 2 seconds for JS to finish
    "width": 1440,
    "height": 3000,             # tall enough for the whole page
    "disable-smart-width": "", # forces the width we set
}
convert_html_to_png(url, "long_page.png", options=options)
```

### 6.2 Страницы, защищённые аутентификацией

Если страница требует cookie сессии, вы можете встроить заголовок cookie:

```python
options = {
    "custom-header": [
        "Cookie: sessionid=YOUR_SESSION_ID"
    ]
}
convert_html_to_png("https://internal.example.com/report", "report.png", options=options)
```

### 6.3 Отсутствующие изображения или шрифты

`wkhtmltoimage` учитывает флаг `--disable-local-file-access` для безопасности. Если ваш HTML ссылается на локальные ресурсы, включите их явно:

```python
options = {"enable-local-file-access": ""}
convert_html_to_png("assets/complex.html", "complex.png", options=options)
```

## Шаг 7: Программно проверять результат (опционально)

Иногда необходимо убедиться, что PNG был сгенерирован корректно (например, в CI‑конвейерах). Следующий фрагмент проверяет размер файла и его размеры:

```python
from pathlib import Path
from PIL import Image

def verify_png(path):
    p = Path(path)
    if not p.is_file():
        raise FileNotFoundError(f"{path} does not exist")
    if p.stat().st_size < 10_000:  # arbitrary minimal size
        raise ValueError("Generated PNG seems too small")
    with Image.open(p) as img:
        print(f"Image size: {img.width}×{img.height}, mode: {img.mode}")

verify_png(png_path)
```

Если PNG проходит эти проверки, вы можете безопасно использовать его в последующих процессах, таких как генерация PDF, вложения в письма или конвейеры машинного обучения.

## Заключение

Теперь у вас есть полный, готовый к продакшену метод **convert HTML to PNG** с использованием Python. В руководстве рассмотрено:

- Установка `wkhtmltoimage` и `imgkit`
- Проверка окружения
- Переиспользуемая функция `convert_html_to_png`, которая обрабатывает как локальные файлы, так и URL
- Практические примеры для **export webpage to PNG**, **how to convert HTML to image** и **convert HTML file to PNG**
- Обработка граничных случаев для больших страниц, аутентификации и локальных ресурсов
- Опциональные шаги проверки для CI/CD конвейеров

Не стесняйтесь экспериментировать с дополнительными параметрами `imgkit` — такими как `zoom`, `crop-h` или `crop-w` — чтобы точно настроить вывод под ваш конкретный случай. В дальнейшем вы можете изучить:

- Конвертация PNG в PDF‑отчёт (библиотека `img2pdf`)
- Автоматизация пакетной конвертации всей папки HTML‑файлов
- Использование Selenium для страниц, требующих полного рендеринга браузером (например, тяжёлые JavaScript‑фреймворки)

Приятного кодинга и наслаждайтесь пиксельно‑точными скриншотами!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Convert HTML to PNG – Complete Python Guide](/html/english/python/general/convert-html-to-png-complete-python-guide/)
- [Convert HTML to PNG in Python – Complete Streaming Save Guide](/html/english/python/general/convert-html-to-png-in-python-complete-streaming-save-guide/)
- [Convert SVG to PNG in Python using Aspose.HTML](/html/english/python/general/convert-svg-to-png-in-python-using-aspose-html/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}