---
category: general
date: 2026-07-21
description: Создайте параметры обработки ресурсов в Python и узнайте, как установить
  максимальную глубину обработки при парсинге HTML. Следуйте этому пошаговому руководству
  для надёжного управления ресурсами.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create resource handling options
- how to set max handling depth
language: ru
lastmod: 2026-07-21
og_description: Создайте параметры обработки ресурсов в Python и мгновенно узнайте,
  как установить максимальную глубину обработки для безопасной загрузки HTML‑документов.
  Овладейте техникой за несколько минут.
og_image_alt: Screenshot of Python code that creates resource handling options with
  max handling depth set
og_title: Создание вариантов обработки ресурсов в Python — Полное пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  headline: Create Resource handling options in Python – Full Guide
  type: TechArticle
- description: Create resource handling options in Python and learn how to set max
    handling depth for HTML parsing. Follow this step‑by‑step tutorial for reliable
    resource management.
  name: Create Resource handling options in Python – Full Guide
  steps:
  - name: Circular References
    text: 'Some legacy sites embed an iframe that points back to the original page,
      creating a loop. With `max_handling_depth` set, the loop is automatically broken
      after the third iteration. However, you might still see a warning in the logs.
      To silence noisy logs, adjust the logger level:'
  - name: Missing Resources
    text: 'If a nested resource fails to load (404 or network timeout), the parser
      throws an exception by default. Wrap the loading call in a `try/except` block
      to keep your application alive:'
  - name: Adjusting Depth Dynamically
    text: 'Sometimes you need different depths for different parts of your pipeline.
      Because `resource_options` is a mutable object, you can change `max_handling_depth`
      on the fly:'
  type: HowTo
tags:
- Python
- HTML parsing
- resource management
title: Создание вариантов обработки ресурсов в Python – Полное руководство
url: /ru/python/general/create-resource-handling-options-in-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание параметров обработки ресурсов в Python – Полное руководство

Когда‑нибудь задавались вопросом, как **создать параметры обработки ресурсов** для огромной HTML‑страницы, не перегружая память? Вы не одиноки. Когда вы передаёте гигантский документ парсеру, вложенные ресурсы, такие как frames, iframes или подключённые CSS, могут быстро выйти из‑под контроля.  

Хорошие новости? Вы можете указать парсеру остановиться после определённого количества уровней вложенности. В этом руководстве мы покажем, как **установить максимальную глубину обработки** и сохранить отзывчивость вашего приложения. Готовы? Погрузимся.

## Что вы узнаете

- Почему ограничение глубины вложенности важно для производительности и безопасности.  
- Точный код, необходимый для **создания параметров обработки ресурсов** с использованием класса `ResourceHandlingOptions`.  
- Как настроить `max_handling_depth`, чтобы парсер останавливался после трёх уровней.  
- Советы по обработке граничных случаев, таких как документы с круговыми ссылками или отсутствующими ресурсами.  

Предыдущий опыт работы с библиотекой не требуется — достаточно установленного Python 3 и базового понимания ввода‑вывода файлов.

## Требования

- Python 3.8+ (библиотека работает на всех современных версиях).  
- Пакет `htmlparser`, предоставляющий `HTMLDocument` и `ResourceHandlingOptions`.  
- Пример HTML‑файла (`big_page.html`), размещённый в папке, к которой вы можете обратиться.  

Если вы ещё не установили пакет, выполните:

```bash
pip install htmlparser
```

Теперь, когда подготовка завершена, перейдём к сути.

## Создание параметров обработки ресурсов – Шаг 1

Первое, что нужно сделать: создать экземпляр `ResourceHandlingOptions`. Представьте его как набор инструментов, где вы можете задать ограничения и политики, которым должен следовать парсер.

```python
# Step 1: Create resource handling options and limit nesting depth
resource_options = ResourceHandlingOptions()
resource_options.max_handling_depth = 3   # Stop after three levels of nested resources
```

**Почему это важно:**  
Когда парсер встречает `<iframe>` внутри другого `<iframe>`, он обычно следует цепочке бесконечно. Ограничив глубину до `3`, вы предотвращаете бесконтрольную рекурсию, которая могла бы исчерпать ОЗУ или вызвать переполнение стека.  

> **Полезный совет:** Если вы парсите недоверенный контент (например, загруженный пользователем HTML), рассмотрите возможность снижения глубины до `1` или `2`, чтобы уменьшить риск потенциальных атак.

## Загрузка HTML‑документа – Шаг 2

Когда объект параметров готов, передайте его в `HTMLDocument`. Конструктор учтёт установленный `max_handling_depth`.

```python
# Step 2: Load the HTML document using the configured options
html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
```

**Что происходит «под капотом»?**  
`HTMLDocument` читает файл, строит дерево DOM, а затем проходит по каждому внешнему ресурсу (таблицам стилей, скриптам, изображениям). Каждый раз, когда встречается вложенный ресурс, проверяется `resource_options.max_handling_depth`. Если предел достигнут, парсер записывает предупреждение в журнал и пропускает дальнейшую вложенность.  

Это означает, что вы получаете полностью пригодное DOM‑дерево для первых трёх уровней, а остальные безопасно игнорируются.

## Проверка конфигурации – Шаг 3

Всегда полезно убедиться, что ваши настройки вступили в силу. Объект `resource_options` раскрывает своё текущее состояние, поэтому вы можете вывести его на печать или проверить в тесте.

```python
# Step 3: Verify that the max handling depth is set correctly
assert resource_options.max_handling_depth == 3, "Depth limit not applied!"

print(f"Resource handling options configured: max depth = {resource_options.max_handling_depth}")
```

Если проверка проходит, вы можете быть уверены, что парсер будет соблюдать ограничение в течение всей работы.

## Обработка граничных случаев

### Круговые ссылки

Некоторые устаревшие сайты встраивают iframe, который указывает обратно на оригинальную страницу, создавая цикл. При установленном `max_handling_depth` цикл автоматически разрывается после третьей итерации. Тем не менее, в журнале может появиться предупреждение. Чтобы подавить шумные сообщения, отрегулируйте уровень логгера:

```python
import logging
logging.getLogger("htmlparser").setLevel(logging.ERROR)
```

### Отсутствующие ресурсы

Если вложенный ресурс не удаётся загрузить (404 или тайм‑аут сети), парсер по умолчанию бросает исключение. Оберните вызов загрузки в блок `try/except`, чтобы приложение оставалось живым:

```python
try:
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", resource_options)
except Exception as e:
    print(f"Failed to load a nested resource: {e}")
    # Fallback: load the document without additional resources
    html_doc = HTMLDocument("YOUR_DIRECTORY/big_page.html")
```

### Динамическое изменение глубины

Иногда требуются разные глубины для разных частей конвейера. Поскольку `resource_options` — изменяемый объект, вы можете менять `max_handling_depth` «на лету»:

```python
resource_options.max_handling_depth = 5   # Temporarily allow deeper nesting
html_doc_deep = HTMLDocument("deep_page.html", resource_options)

resource_options.max_handling_depth = 2   # Tighten for a lightweight preview
html_doc_preview = HTMLDocument("preview.html", resource_options)
```

Просто помните, что перед повторным использованием того же экземпляра параметров в другом потоке нужно сбросить значение.

## Полный рабочий пример

Ниже представлен полный скрипт, который вы можете скопировать, скорректировать пути к файлам и сразу запустить.

```python
import logging
from htmlparser import HTMLDocument, ResourceHandlingOptions

# Optional: Reduce noisy output
logging.getLogger("htmlparser").setLevel(logging.ERROR)

def load_document(path: str, max_depth: int = 3):
    """
    Load an HTML document with a controlled resource handling depth.
    Returns the HTMLDocument instance.
    """
    opts = ResourceHandlingOptions()
    opts.max_handling_depth = max_depth    # How to set max handling depth
    try:
        doc = HTMLDocument(path, opts)
        print(f"Loaded '{path}' with max depth {max_depth}.")
        return doc
    except Exception as exc:
        print(f"Error loading '{path}': {exc}")
        # Fallback to a simple load without resource handling
        return HTMLDocument(path)

if __name__ == "__main__":
    # Example 1: Standard depth
    doc1 = load_document("YOUR_DIRECTORY/big_page.html", max_depth=3)

    # Example 2: Deeper inspection for debugging
    doc2 = load_document("YOUR_DIRECTORY/complex_page.html", max_depth=5)

    # Example 3: Very shallow preview (e.g., thumbnail generation)
    doc3 = load_document("YOUR_DIRECTORY/preview_page.html", max_depth=1)
```

**Ожидаемый вывод (при наличии файлов и их корректном формате):**

```
Loaded 'YOUR_DIRECTORY/big_page.html' with max depth 3.
Loaded 'YOUR_DIRECTORY/complex_page.html' with max depth 5.
Loaded 'YOUR_DIRECTORY/preview_page.html' with max depth 1.
```

Если файл не удаётся прочитать, вы увидите сообщение об ошибке вместо сбоя.

![Create resource handling options in Python](/images/resource-options.png){alt="Create resource handling options in Python"}

## Итоги – Почему этот подход крут

- **Безопасность превыше всего:** Ограничение глубины вложенности предотвращает бесконтрольную рекурсию и рост потребления памяти.  
- **Гибкость:** Вы можете менять `max_handling_depth` во время выполнения, подстраивая под разные сценарии.  
- **Простота:** Пара строк кода позволяют **создать параметры обработки ресурсов** и сразу их применить.  

Короче говоря, теперь у вас есть надёжный шаблон для контроля того, насколько глубоко ваш парсер следует внешним ресурсам.

## Что дальше?

- Подробнее изучите класс `ResourceHandlingOptions` — в нём есть флаги для кэширования, обработки тайм‑аутов и фильтрации MIME‑типов.  
- Сочетайте ограничение глубины с пользовательской строкой `UserAgent`, чтобы избежать блокировки со стороны агрессивных серверов.  
- Если вы работаете с асинхронным вводом‑выводом, обратите внимание на вариант `aiohtmlparser`, который учитывает те же параметры, но работает с `asyncio`.  

Не стесняйтесь экспериментировать: попробуйте установить глубину в `0` и наблюдайте, как парсер игнорирует все внешние ссылки. Это удобный приём, когда нужен только чистый HTML‑разметка.

Есть вопросы или сложная страница, которая всё ещё вызывает проблемы? Оставьте комментарий ниже, и я с радостью помогу вам точно настроить параметры. Приятного парсинга!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Создать HTML из строки в C# – Руководство по пользовательскому обработчику ресурсов](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Как сохранить HTML в C# – Полное руководство с использованием пользовательского обработчика ресурсов](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Создание песочницы для HTML в Java – Пошаговое руководство](/html/english/java/creating-managing-html-documents/create-sandbox-for-html-in-java-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}