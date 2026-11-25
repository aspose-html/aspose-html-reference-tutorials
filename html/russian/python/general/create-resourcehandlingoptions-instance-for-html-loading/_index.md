---
category: general
date: 2026-05-31
description: Создайте экземпляр ResourceHandlingOptions для управления загрузкой ресурсов
  HTML. Узнайте, как ограничить глубину ресурсов и загрузить HTMLDocument с пользовательскими
  параметрами.
draft: false
keywords:
- create resourcehandlingoptions instance
- limit resource depth
- HTMLDocument options
- resource loading configuration
- python html parsing
language: ru
og_description: Создайте экземпляр ResourceHandlingOptions для управления загрузкой
  HTML‑ресурсов. Это руководство показывает, как установить максимальную глубину обработки
  и загрузить HTMLDocument с пользовательскими параметрами.
og_title: Создать экземпляр ResourceHandlingOptions для загрузки HTML
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create ResourceHandlingOptions instance to control HTML resource loading.
    Learn how to limit resource depth and load an HTMLDocument with custom options.
  headline: Create ResourceHandlingOptions Instance for HTML Loading
  type: TechArticle
tags:
- Python
- HTML parsing
- Resource handling
title: Создать экземпляр ResourceHandlingOptions для загрузки HTML
url: /ru/python/general/create-resourcehandlingoptions-instance-for-html-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание экземпляра ResourceHandlingOptions для загрузки HTML

Вы когда‑нибудь задумывались, как **создать экземпляр ResourceHandlingOptions**, чтобы огромная HTML‑страница не вывела ваш парсер из строя? Вы не одиноки — большие документы с вложенными скриптами, фреймами или включениями могут быстро превратить простое сканирование в кошмар.  

В этом руководстве мы пройдём точные шаги по созданию объекта `ResourceHandlingOptions`, ограничим уровень вложенности и передадим его в `HTMLDocument`. К концу вы получите чистый, повторяемый шаблон для **конфигурации загрузки ресурсов**, который работает с любой по размеру HTML‑страницей.

## Что вы узнаете

- Почему экземпляр `ResourceHandlingOptions` важен при разборе огромных страниц.  
- Как **ограничить глубину ресурсов**, чтобы избежать бесконечной рекурсии.  
- Точный синтаксис загрузки `HTMLDocument` с вашими пользовательскими параметрами.  
- Полный, готовый к запуску пример, который вы можете сразу добавить в свой проект.  

**Требования:** Python 3.8+, библиотека `htmlparser`, предоставляющая `HTMLDocument` и `ResourceHandlingOptions`. Других зависимостей не требуется.

---

## Шаг 1: Создать экземпляр ResourceHandlingOptions

Первое, что вам нужно, — это новый объект `ResourceHandlingOptions`. Считайте его панелью управления для каждого внешнего ресурса, с которым может столкнуться парсер — скрипты, изображения, iframe и т.д.

```python
# Step 1: Initialize the options object
options = ResourceHandlingOptions()
```

> **Почему это важно:** Без явного экземпляра парсер использует свои значения по умолчанию, что часто означает «загружать всё». Для огромных страниц такие настройки могут потреблять гигабайты памяти и заставлять ваш скрипт зависать.

---

## Шаг 2: Ограничить глубину ресурсов

Далее мы указываем параметрам, насколько глубоко мы готовы идти. Установка `max_handling_depth` в 5, например, останавливает парсер после пяти уровней вложенных ресурсов. Подберите число под ваш сценарий.

```python
# Step 2: Cap the nesting depth (e.g., stop after 5 levels)
options.max_handling_depth = 5
```

> **Совет:** Если вам интересен только контент верхнего уровня, глубина 1 или 2 обычно достаточна и значительно ускоряет процесс.

---

## Шаг 3: Загрузить HTML‑документ с параметрами

Теперь мы передаём настроенные `options` в `HTMLDocument`. Конструктор принимает путь к файлу (или URL) и объект параметров, предоставляя вам детальный контроль над тем, что будет загружено.

```python
# Step 3: Parse the HTML file using the configured options
doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
```

> **Что вы увидите:** Парсер прочитает `big_page.html`, но любой ресурс, который привёл бы к превышению глубины 5, будет тихо проигнорирован. Это предотвращает бесконтрольную рекурсию и делает использование памяти предсказуемым.

---

## Шаг 4: Проверить результат (необязательно, но полезно)

Хорошая привычка — проверять, что документ загружен как ожидалось. Ниже простой sanity‑check, выводящий количество успешно обработанных ресурсов.

```python
# Step 4: Quick verification
print(f"Handled resources: {len(doc.resources)}")
print(f"Document title: {doc.title}")
```

**Ожидаемый вывод** (ваши числа будут отличаться в зависимости от входного файла):

```
Handled resources: 12
Document title: Example Large Page
```

Если количество значительно ниже ожидаемого, возможно, потребуется увеличить `max_handling_depth` или скорректировать другие свойства `ResourceHandlingOptions`.

---

## Общие варианты и граничные случаи

| Situation | Adjustment |
|-----------|------------|
| **Вам нужно игнорировать только изображения** | Set `options.ignore_images = True`. |
| **Скрипты вызывают тайм‑ауты** | Use `options.max_script_execution_time = 2` (seconds). |
| **Разбор удалённого URL вместо файла** | Pass the URL string to `HTMLDocument` just like a file path. |
| **Вы хотите собственный логгер** | Assign `options.logger = my_logger` before loading. |

These tweaks are all part of the **HTMLDocument options** toolkit and let you fine‑tune **resource loading configuration** without rewriting your parser.

---

## Полный рабочий пример

Объединив всё вместе, представляем автономный скрипт, который вы можете запустить прямо сейчас. Сохраните его как `parse_big_page.py` и выполните командой `python parse_big_page.py`.

```python
# parse_big_page.py
from htmlparser import HTMLDocument, ResourceHandlingOptions

def main():
    # 1️⃣ Create the options instance
    options = ResourceHandlingOptions()
    
    # 2️⃣ Limit how deep we go into nested resources
    options.max_handling_depth = 5
    
    # Optional: ignore images to speed things up
    # options.ignore_images = True
    
    # 3️⃣ Load the document with our custom options
    doc = HTMLDocument("YOUR_DIRECTORY/big_page.html", options)
    
    # 4️⃣ Verify the load
    print(f"Handled resources: {len(doc.resources)}")
    print(f"Document title: {doc.title}")

if __name__ == "__main__":
    main()
```

Запустите его, и вы увидите вывод количества ресурсов и заголовка, подтверждающий, что вы успешно **создали экземпляр ResourceHandlingOptions** и применили его.

---

## Заключение

Мы только что показали, как **создать экземпляр ResourceHandlingOptions**, ограничить уровень вложенности и передать его в `HTMLDocument`. Этот шаблон обеспечивает надёжную **конфигурацию загрузки ресурсов** для любого большого HTML‑файла, делая ваш парсинг в Python быстрым и экономным по памяти.

Готовы к следующему шагу? Попробуйте изменить ограничение глубины, переключить `ignore_images` или интегрировать собственный логгер — каждая настройка даст вам больше понимания о **HTMLDocument options** и их взаимодействии с вашим конвейером данных.

Если этот гид оказался полезным, смело делитесь им, ставьте звёздочку репозиторию или оставляйте комментарий со своими советами. Счастливого парсинга!

## Что стоит изучить дальше?

- [Создать HTML из строки в C# — руководство по пользовательскому обработчику ресурсов](/html/english/net/html-document-manipulation/create-html-from-string-in-c-custom-resource-handler-guide/)
- [Как сохранить HTML в C# — полное руководство с использованием пользовательского обработчика ресурсов](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Создать Stream Provider в .NET с Aspose.HTML](/html/english/net/advanced-features/create-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}