---
category: general
date: 2026-10-25
description: Узнайте, как ограничить глубину ресурсов и применить обработку ресурсов
  при сохранении больших HTML‑файлов с помощью Python. Следуйте этому пошаговому руководству
  для надёжных результатов.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- limit resource depth
- apply resource handling
- HTML document processing
- save options Python
- resource handling options
language: ru
lastmod: 2026-10-25
og_description: Ограничьте глубину ресурсов и примените их обработку при сохранении
  HTML с помощью Python. Этот учебник демонстрирует полное, готовое к запуску решение.
og_image_alt: Screenshot illustrating limit resource depth in a Python script
og_title: Ограничьте глубину ресурсов при их обработке — руководство по Python
schemas:
- author: GroupDocs
  dateModified: '2026-10-25'
  description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  headline: How to limit resource depth with resource handling options
  type: TechArticle
- description: Learn how to limit resource depth and apply resource handling when
    saving large HTML files using Python. Follow this step‑by‑step guide for reliable
    results.
  name: How to limit resource depth with resource handling options
  steps:
  - name: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
    text: '**Dynamic content loaded via JavaScript** – The parser only sees static
      HTML. If your page relies on scripts that inject further resources, those will
      never be counted toward the depth limit. Consider pre‑rendering the page with
      a headless browser before applying the limit.'
  - name: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
    text: '**Circular references** – Some pages include iframes that point back to
      the same page. The depth counter prevents infinite loops, but you may still
      see partially rendered sections. Adjust `max_handling_depth` or manually exclude
      problematic frames.'
  - name: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
    text: '**Mixed protocols (http/https)** – If resources use different schemes,
      the library may treat them as separate domains. The depth limit still applies
      across protocols, but network permissions might differ. Ensure your environment
      permits both.'
  type: HowTo
tags:
- Python
- HTML
- File handling
title: Как ограничить глубину ресурса с помощью опций обработки ресурсов
url: /ru/python/general/how-to-limit-resource-depth-with-resource-handling-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как ограничить глубину ресурсов с помощью параметров обработки ресурсов

Если вам нужно **ограничить глубину ресурсов** при обработке огромного HTML‑файла, это руководство покажет, как это сделать. К концу урока вы также узнаете, как **применять обработку ресурсов**, чтобы операция сохранения учитывала ограничение глубины и избегала неконтролируемой обработки.

Большие HTML‑страницы часто включают множество внешних ресурсов — изображения, скрипты, таблицы стилей и вложенные iframe. Без ограничения глубины парсер может следовать по каждой ссылке, резко увеличивая использование памяти и время обработки. Описанная здесь техника сохраняет операцию быстрой и предсказуемой.

## Предварительные требования

* Python 3.9+ установлен.
* `groupdocs-viewer` (или аналогичная библиотека для обработки HTML), доступна через `pip install groupdocs-viewer`.
* Пример HTML‑файла (`big_page.html`) в известном каталоге.
* Права записи в каталог вывода.

Эти элементы гарантируют, что код будет работать без дополнительной настройки.

## Шаг 1: Загрузить исходный HTML‑документ

Первый шаг — создать экземпляр `HTMLDocument`, указывающий на оригинальный файл. Этот объект представляет всю структуру HTML и позже предоставляет доступ к параметрам сохранения.

```python
# Step 1: Load the source HTML document
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

*Почему это важно*: Загрузка файла один раз предоставляет библиотеке единую точку входа для всех последующих операций. Также проверяется существование файла, и при неправильном пути сразу генерируется ошибка.

## Шаг 2: Создать параметры обработки ресурсов и ограничить глубину обработки

`ResourceHandlingOptions` позволяет управлять тем, насколько глубоко библиотека будет проходить по связанным ресурсам. Установка `max_handling_depth` в небольшое число (например, 5) сообщает движку прекращать следовать по ссылкам после пяти уровней вложенности.

```python
# Step 2: Create resource handling options and limit the processing depth
resource_opts = ResourceHandlingOptions()
resource_opts.max_handling_depth = 5  # Restricts handling to 5 levels deep
```

*Почему это важно*: **Ограничивая глубину ресурсов**, вы предотвращаете загрузку парсером каждого изображения, скрипта или iframe, которые могут быть указаны косвенно. Это снижает сетевой трафик и нагрузку на память, особенно для страниц, встраивающих сторонний контент.

## Шаг 3: Привязать параметры ресурсов к параметрам сохранения

`SaveOptions` собирает все настройки, влияющие на выходной файл. При присвоении `resource_handling_options` мы **применяем обработку ресурсов** к предстоящей операции сохранения.

```python
# Step 3: Attach the resource options to the save options
save_opts = SaveOptions()
save_opts.resource_handling_options = resource_opts
```

*Почему это важно*: Объект `save_opts` служит контейнером для множества флагов (сжатие, формат и т.д.). Добавление `resource_handling_options` гарантирует, что ограничение глубины будет соблюдаться во время записи.

## Шаг 4: Сохранить документ с применённым ограничением обработки ресурсов

Наконец, вызовите `doc.save()` с настроенными `save_opts`. Выходной файл будет содержать только те ресурсы, которые находятся в пределах определённой глубины.

```python
# Step 4: Save the document with the limited resource handling applied
doc.save("YOUR_DIRECTORY/big_page_limited.html", save_opts)
```

**Ожидаемый результат**:  
Новый файл `big_page_limited.html` появляется в `YOUR_DIRECTORY`. Откройте его в браузере; вы увидите оригинальное оформление, но любые ресурсы, находящиеся более чем на пяти уровнях вложенности, будут опущены. Страница загружается быстрее и потребляет гораздо меньше памяти.

## Проверка сохранённого HTML

После сохранения рекомендуется убедиться, что ограничение глубины было соблюдено.

```python
# Verify that the saved file exists and its size is reasonable
import os

output_path = "YOUR_DIRECTORY/big_page_limited.html"
if os.path.isfile(output_path):
    size_kb = os.path.getsize(output_path) / 1024
    print(f"Saved file size: {size_kb:.2f} KB")
else:
    raise FileNotFoundError("The limited HTML file was not created.")
```

Если размер значительно меньше оригинального (который может достигать сотен килобайт), настройка **ограничения глубины ресурсов** сработала как задумано.

## Распространённые подводные камни и как их избежать

| Симптом | Причина | Решение |
|---------|-------|-----|
| Размер файла не изменился | `max_handling_depth` оставлен по умолчанию (неограниченный) | Явно установить `resource_opts.max_handling_depth` в значение < ∞ |
| Отсутствуют изображения на странице | Ресурсы находились глубже ограничения | Увеличьте глубину или переместите критические ресурсы на более высокий уровень |
| `PermissionError` при сохранении | Каталог вывода доступен только для чтения | Выберите каталог с правом записи или измените разрешения ОС |
| Неожиданное исключение `ResourceHandlingException` | Несовместимость версии библиотеки | Обновите до последней версии `groupdocs-viewer` (`pip install --upgrade groupdocs-viewer`) |

**Совет**: Начните с глубины 3 для очень больших страниц и постепенно увеличивайте её, пока визуальное качество не удовлетворит ваши требования.

## Пограничные случаи, с которыми вы можете столкнуться

1. **Динамический контент, загружаемый через JavaScript** – Парсер видит только статический HTML. Если ваша страница зависит от скриптов, которые внедряют дополнительные ресурсы, они никогда не будут учитываться при подсчёте глубины. Рассмотрите возможность предварительного рендеринга страницы с помощью безголового браузера перед применением ограничения.  
2. **Круговые ссылки** – Некоторые страницы включают iframe, которые ссылаются обратно на ту же страницу. Счётчик глубины предотвращает бесконечные циклы, но вы всё равно можете увидеть частично отрисованные секции. Отрегулируйте `max_handling_depth` или вручную исключите проблемные фреймы.  
3. **Смешанные протоколы (http/https)** – Если ресурсы используют разные схемы, библиотека может рассматривать их как отдельные домены. Ограничение глубины всё равно применяется к обоим протоколам, но сетевые разрешения могут различаться. Убедитесь, что ваша среда допускает оба протокола.

## Следующие шаги: расширенная обработка ресурсов

Теперь, когда вы можете **ограничивать глубину ресурсов** и **применять обработку ресурсов**, вы можете захотеть изучить:

* **Custom filters** – Используйте `resource_opts.resource_filter` для пропуска определённых типов файлов (например, больших видео).  
* **Compression settings** – Сочетайте `SaveOptions` с `compression_level` для дальнейшего уменьшения размера вывода.  
* **Batch processing** – Пройдитесь по каталогу HTML‑файлов, применяя одинаковое ограничение глубины к каждому.

Эти расширения позволяют построить полноценный конвейер оптимизации HTML для масштабных документооборотных процессов.

## Заключение

Вы узнали, как **ограничивать глубину ресурсов** и **применять обработку ресурсов** при сохранении большого HTML‑документа с помощью Python. Настраивая `ResourceHandlingOptions` и привязывая их к `SaveOptions`, вы получаете точный контроль над количеством обрабатываемых вложенных ресурсов, что приводит к более быстрым сохранениям и меньшим выходным файлам. Экспериментируйте с различными значениями глубины и дополнительными `SaveOptions`, чтобы адаптировать поведение под потребности вашего проекта.

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс содержит полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Как установить max_handling_depth в Aspose.HTML Python – Полное руководство](/html/english/python/general/how-to-set-max-handling-depth-in-aspose-html-python-complete/)
- [Создать параметры обработки ресурсов и загрузить HTML‑документ в Python](/html/english/python/general/create-resource-handling-options-and-load-an-html-document-i/)
- [Как сохранить HTML с контролируемой глубиной – Пошаговое руководство на Python](/html/english/python/general/how-to-save-html-with-controlled-depth-step-by-step-python-g/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}