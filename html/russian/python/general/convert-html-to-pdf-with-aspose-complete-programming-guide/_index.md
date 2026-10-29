---
category: general
date: 2026-05-25
description: Преобразуйте HTML в PDF с помощью Aspose HTML for Python, одновременно
  извлекая изображения из HTML. Узнайте, как извлекать изображения, как сохранять
  изображения и как сохранять HTML как PDF в одном руководстве.
draft: false
keywords:
- convert html to pdf
- extract images from html
- how to extract images
- how to save images
- save html as pdf
language: ru
og_description: Конвертировать HTML в PDF с помощью Aspose HTML для Python. Это руководство
  показывает, как извлекать изображения из HTML, как сохранять изображения и как сохранять
  HTML в PDF.
og_title: Преобразовать HTML в PDF с помощью Aspose – Полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert HTML to PDF using Aspose HTML for Python while extracting images
    from HTML. Learn how to extract images, how to save images, and save HTML as PDF
    in one tutorial.
  headline: Convert HTML to PDF with Aspose – Complete Programming Guide
  type: TechArticle
- description: Convert HTML to PDF using Aspose HTML for Python while extracting images
    from HTML. Learn how to extract images, how to save images, and save HTML as PDF
    in one tutorial.
  name: Convert HTML to PDF with Aspose – Complete Programming Guide
  steps:
  - name: 1. What if the HTML references remote images that require authentication?
    text: The default handler will try to fetch them anonymously and fail. You can
      extend `handle_resource` to add custom HTTP headers (e.g., `Authorization`)
      before reading the stream.
  - name: 2. My images are huge—will this blow up memory?
    text: Because we stream directly to disk (`resource.stream.read()`), memory usage
      stays low. However, you might still want to resize images after extraction using
      Pillow if file size is a concern.
  - name: 3. How do I keep the original folder structure for images?
    text: 'Replace the `image_path` construction with something like:'
  - name: 4. Can I also extract CSS or fonts?
    text: Absolutely. The `resource_handler` receives every resource type. Just check
      `resource.content_type` for `text/css` or `font/` prefixes and write them to
      appropriate folders.
  type: HowTo
tags:
- Aspose
- Python
- HTML
- PDF
- Image Extraction
title: Преобразование HTML в PDF с помощью Aspose – Полное руководство по программированию
url: /ru/python/general/convert-html-to-pdf-with-aspose-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в PDF с Aspose – Полное руководство по программированию

Когда‑нибудь задумывались, как **convert HTML to PDF** без потери изображений, встроенных в страницу? Вы не одиноки. Будь то создание инструмента отчётности, генератора счетов или просто надёжный способ архивировать веб‑контент, возможность превратить HTML в чёткий PDF, извлекая каждое изображение, — реальная задача, с которой сталкиваются многие разработчики.

В этом руководстве мы пройдём через полностью готовый к запуску пример, который не только **convert html to pdf**, но и показывает, **как извлекать изображения** из исходного HTML, **как сохранять изображения** на диск и лучшую практику для **save html as pdf** с использованием Aspose.HTML для Python. Никаких расплывчатых ссылок — только нужный код, объяснение каждого шага и советы, которые вы сразу сможете применить.

---

## Что вы узнаете

- Как настроить Aspose.HTML для Python в виртуальном окружении.  
- Как загрузить HTML‑файл и подготовить его к конвертации.  
- Как написать пользовательский обработчик ресурсов, который **извлекает изображения из HTML** и сохраняет их эффективно.  
- Как сконфигурировать `SaveOptions`, чтобы конвертация учитывала ваш обработчик.  
- Как выполнить конвертацию и проверить как PDF, так и извлечённые файлы изображений.  

К концу вы получите переиспользуемый скрипт, который можно добавить в любой проект, требующий **save HTML as PDF** с сохранением локальной копии каждого изображения.

---

## Требования

| Требование | Зачем это нужно |
|------------|-----------------|
| Python 3.8+ | Aspose.HTML для Python требует современного интерпретатора. |
| `aspose.html` package | Основная библиотека, выполняющая всю тяжёлую работу. |
| Входной HTML файл (`input.html`) | Источник, который вы будете конвертировать и из которого извлекать данные. |
| Права записи в папку (`YOUR_DIRECTORY`) | Необходимо как для вывода PDF, так и для сохранения извлечённых изображений. |

Если у вас уже всё готово — переходите к первому шагу. Если нет, быстрый гайд по установке ниже поможет вам начать работу менее чем за пять минут.

---

## Шаг 1: Установите Aspose.HTML для Python

Откройте терминал (или PowerShell) и выполните:

```bash
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate
pip install aspose-html
```

> **Pro tip:** Держите виртуальное окружение изолированным; это предотвратит конфликты версий, когда вы позже добавите другие библиотеки для работы с PDF.

---

## Шаг 2: Загрузите HTML‑документ (Первая часть Convert HTML to PDF)

Загрузка документа проста, но это фундамент любой конвейерной конвертации.

```python
from aspose.html import HTMLDocument

# Replace YOUR_DIRECTORY with the actual path on your machine
document = HTMLDocument("YOUR_DIRECTORY/input.html")
```

*Почему это важно:* `HTMLDocument` парсит разметку, обрабатывает CSS и строит DOM, который Aspose затем может отрисовать в страницу PDF. Если HTML содержит внешние таблицы стилей или скрипты, Aspose попытается автоматически загрузить их — при условии, что пути доступны.

---

## Шаг 3: Как извлекать изображения – Создайте пользовательский обработчик ресурсов

Aspose позволяет подключиться к процессу загрузки ресурсов. Предоставив `resource_handler`, мы можем **how to extract images** «на лету», не загружая весь файл в память.

```python
def handle_resource(resource):
    """
    Custom handler that writes image resources to disk.
    Other resources (CSS, fonts) are ignored for brevity.
    """
    # Check the MIME type to ensure we only process images
    if resource.content_type.startswith("image/"):
        # Build a safe file name; Aspose gives us the original name
        image_path = f"YOUR_DIRECTORY/images/{resource.file_name}"
        # Write the binary stream directly to the file system
        with open(image_path, "wb") as file:
            file.write(resource.stream.read())
```

**Что происходит?**  
- `resource.content_type` сообщает MIME‑тип (`image/png`, `image/jpeg` и т.д.).  
- `resource.file_name` — имя, которое Aspose извлекает из URL; мы используем его, чтобы сохранить оригинальное название.  
- Читая `resource.stream`, мы избегаем загрузки всего документа в ОЗУ — выигрыш для больших наборов изображений.

*Особый случай:* Если у URL изображения нет имени файла (например, data‑URI), `resource.file_name` может быть пустым. В продакшене стоит добавить запасной вариант, например `uuid4().hex + ".png"`.

---

## Шаг 4: Настройте параметры сохранения – Подключите обработчик к конвертации PDF

Теперь привязываем наш обработчик к конвейеру конвертации:

```python
from aspose.html import ResourceHandlingOptions, SaveOptions

# Create the options container
resource_options = ResourceHandlingOptions()
resource_options.resource_handler = handle_resource

# Attach the resource handling options to the save options
save_options = SaveOptions()
save_options.resource_handling_options = resource_options
```

**Зачем это нужно:** `SaveOptions` управляет всем, что касается вывода — размером страницы, версией PDF и, что особенно важно для нас, тем, как обрабатываются внешние ресурсы. Подключив `resource_options`, каждый раз, когда конвертер встречает изображение, вызывается наша функция `handle_resource`.

---

## Шаг 5: Конвертируйте HTML в PDF и проверьте результат

Наконец, запускаем конвертацию. Это момент, когда операция **convert html to pdf** действительно происходит.

```python
from aspose.html import Converter

# The third argument is the save options we configured above
Converter.convert(document, "YOUR_DIRECTORY/output.pdf", save_options)
```

После завершения скрипта вы должны увидеть два результата:

1. `output.pdf` в `YOUR_DIRECTORY` — точная визуальная копия `input.html`.  
2. Папка `images/`, заполненная всеми изображениями, на которые ссылается оригинальный HTML.

**Быстрая проверка:** Откройте PDF в любом просмотрщике; изображения должны находиться точно там, где они были на странице. Затем выведите содержимое каталога `images/`, чтобы убедиться в извлечении.

```bash
ls YOUR_DIRECTORY/images
# Expected: logo.png banner.jpg icon.svg ...
```

Если какие‑то изображения отсутствуют, проверьте обработку MIME‑типа в `handle_resource` и убедитесь, что исходный HTML использует абсолютные URL или пути, которые скрипт может разрешить.

---

## Полный скрипт – Готов к копированию и вставке

```python
# ------------------------------------------------------------
# Convert HTML to PDF with Aspose – Extract Images Example
# ------------------------------------------------------------
from aspose.html import HTMLDocument, Converter, ResourceHandlingOptions, SaveOptions

# -----------------------------------------------------------------
# Step 1: Load the source HTML document (the entry point for conversion)
# -----------------------------------------------------------------
document = HTMLDocument("YOUR_DIRECTORY/input.html")

# -----------------------------------------------------------------
# Step 2: Define a custom resource handler (how to extract images)
# -----------------------------------------------------------------
def handle_resource(resource):
    """
    Saves each image resource to the 'images' subfolder.
    Non‑image resources are ignored.
    """
    if resource.content_type.startswith("image/"):
        image_path = f"YOUR_DIRECTORY/images/{resource.file_name}"
        with open(image_path, "wb") as file:
            file.write(resource.stream.read())

# -----------------------------------------------------------------
# Step 3: Attach the custom handler to resource‑handling options
# -----------------------------------------------------------------
resource_options = ResourceHandlingOptions()
resource_options.resource_handler = handle_resource

# -----------------------------------------------------------------
# Step 4: Associate the resource options with the save options
# -----------------------------------------------------------------
save_options = SaveOptions()
save_options.resource_handling_options = resource_options

# -----------------------------------------------------------------
# Step 5: Convert the HTML document to PDF (convert html to pdf)
# -----------------------------------------------------------------
Converter.convert(document, "YOUR_DIRECTORY/output.pdf", save_options)

print("Conversion complete! PDF and images are saved.")
```

---

## Часто задаваемые вопросы и особые случаи

### 1. Что делать, если HTML ссылается на удалённые изображения, требующие аутентификации?
Обработчик по умолчанию попытается загрузить их анонимно и провалится. Вы можете расширить `handle_resource`, добавив пользовательские HTTP‑заголовки (например, `Authorization`) перед чтением потока.

### 2. Мои изображения огромные — не приведёт ли это к переполнению памяти?
Поскольку мы сразу записываем поток на диск (`resource.stream.read()`), использование памяти остаётся низким. Тем не менее, при необходимости можно уменьшить размер изображений после извлечения с помощью Pillow.

### 3. Как сохранить оригинальную структуру папок для изображений?
Замените построение `image_path` на что‑то вроде:

```python
import os
rel_path = os.path.relpath(resource.uri, start=document.base_uri)
image_path = os.path.join("YOUR_DIRECTORY/images", rel_path)
os.makedirs(os.path.dirname(image_path), exist_ok=True)
```

Это воспроизведёт иерархию источника.

### 4. Можно ли также извлекать CSS или шрифты?
Конечно. `resource_handler` получает каждый тип ресурса. Достаточно проверить `resource.content_type` на префиксы `text/css` или `font/` и записать их в соответствующие каталоги.

---

## Ожидаемый вывод

Запуск скрипта должен дать:

- **`output.pdf`** — PDF‑файл (одностраничный или многостраничный), визуально идентичный `input.html`.  
- **Каталог `images/`** — содержащий каждый файл изображения, названный точно так же, как в HTML (например, `logo.png`, `header.jpg`).  

Откройте PDF; вы увидите тот же макет, типографику и изображения. Затем выполните:

```bash
du -sh YOUR_DIRECTORY/images
```

чтобы убедиться, что общий размер совпадает с суммой размеров извлечённых файлов.

---

## Заключение

Теперь у вас есть надёжное решение «end‑to‑end», которое **convert html to pdf**, одновременно **extract images from HTML**, **how to extract images** и **how to save images** с помощью Aspose.HTML для Python. Скрипт модульный — заменяйте обработчик ресурсов на обработку шрифтов, CSS или даже JavaScript, если требуется более глубокий контроль.

Что дальше? Попробуйте добавить номера страниц, водяные знаки или защиту паролем к PDF, изменив `SaveOptions`. Или поэкспериментируйте с асинхронной загрузкой ресурсов для ещё более быстрой обработки крупных сайтов.

Счастливого кодинга, и пусть ваши PDF всегда отображаются безупречно! 

---

![Пример преобразования HTML в PDF](/images/convert-html-to-pdf.png "Convert HTML to PDF using Aspose")


## Связанные руководства

- [Как конвертировать HTML в PDF на Java – используя Aspose.HTML для Java](/html/english/java/conversion-html-to-other-formats/convert-html-to-pdf/)
- [Как конвертировать HTML в JPEG с помощью Aspose.HTML для Java](/html/english/java/conversion-html-to-various-image-formats/convert-html-to-jpeg/)
- [Конвертация HTML в PDF с Aspose.HTML – Полное руководство по манипуляциям](/html/english/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}