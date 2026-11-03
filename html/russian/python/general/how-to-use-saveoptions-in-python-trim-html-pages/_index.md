---
category: general
date: 2026-05-28
description: Узнайте, как использовать SaveOptions для обрезки HTML‑страниц в Python.
  Это пошаговое руководство также объясняет, как загрузить HTML‑документ и эффективно
  удалить вложенные ресурсы.
draft: false
keywords:
- how to use saveoptions
- how to load html document
- how to trim html page
language: ru
og_description: Как использовать SaveOptions для обрезки HTML‑страниц в Python. Следуйте
  этому руководству, чтобы загрузить HTML‑документ, установить ограничения ресурсов
  и сохранить чистый, лёгкий файл.
og_title: Как использовать SaveOptions в Python — Обрезка HTML‑страниц
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Learn how to use SaveOptions to trim HTML pages in Python. This step‑by‑step
    guide also explains how to load an HTML document and efficiently remove nested
    resources.
  headline: How to Use SaveOptions in Python – Trim HTML Pages
  type: TechArticle
tags:
- python
- html-processing
- saveoptions
- resource-handling
title: Как использовать SaveOptions в Python — Обрезка HTML‑страниц
url: /ru/python/general/how-to-use-saveoptions-in-python-trim-html-pages/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать SaveOptions в Python – Обрезка HTML‑страниц

Задумывались ли вы когда‑нибудь **как использовать SaveOptions**, чтобы уменьшить огромный HTML‑файл, не ломая ничего? Вы не одиноки. Когда вы загружаете страницу, содержащую десятки вложенных ресурсов — например CSS, JS или даже другие HTML‑фрагменты — ваш результат может выйти из‑под контроля.  

В этом руководстве мы пройдём полный, готовый к запуску пример, который не только показывает **как использовать SaveOptions**, но и охватывает **как загрузить HTML‑документ** и лучший способ **обрезать HTML‑страницу**, ограничивая глубину вложения. К концу вы получите чистый, обрезанный файл, готовый к развертыванию или дальнейшей обработке.

## Что вы получите

- Загрузите любой локальный HTML‑файл одной строкой кода.  
- Настроите параметры обработки ресурсов, чтобы остановиться на определённой глубине включения.  
- Сохраните обрезанный результат, используя мощный класс `SaveOptions`.  

Никаких внешних инструментов, никакой магии — только чистый Python и небольшая библиотека, которая делает всю тяжёлую работу.

---

## Требования

Прежде чем мы начнём, убедитесь, что у вас есть:

1. **Python 3.9+** установлен (используемый синтаксис работает на любой современной версии).  
2. Гипотетический пакет `htmlprocessor`, предоставляющий `HTMLDocument`, `SaveOptions` и `ResourceHandlingOptions`. Установите его с помощью:

```bash
pip install htmlprocessor
```

> **Полезный совет:** Если вы используете виртуальное окружение, сначала активируйте его — это поможет держать зависимости в порядке.

---

## Шаг 1: Как загрузить HTML‑документ

Загрузка файла так же проста, как передать путь конструктору. Библиотека читает разметку, строит дерево, похожее на DOM, и готовит его к дальнейшему изменению.

```python
from htmlprocessor import HTMLDocument

# Replace with the actual path to your file
doc = HTMLDocument("YOUR_DIRECTORY/complex_page.html")
print("Document loaded –", doc.title or "Untitled")
```

> **Почему это важно:** Объект `HTMLDocument` абстрагирует работу с сырыми строками, предоставляя методы для запросов, модификаций и, в конечном итоге, сохранения страницы. Он также нормализует окончания строк и кодировки символов, что избавляет от скрытых багов позже.

Мы выводим заголовок только для проверки успешной загрузки. Если файл отсутствует или повреждён, конструктор бросит понятное исключение — без тихих сбоев.

---

## Шаг 2: Настройка обработки ресурсов — ядро обрезки

Следующий элемент головоломки — **как обрезать HTML‑страницу**, ограничивая то, насколько глубоко процессор следует включениям. Здесь в игру вступает `ResourceHandlingOptions`.

```python
from htmlprocessor import ResourceHandlingOptions

# Create a fresh options instance
res_opt = ResourceHandlingOptions()
# max_handling_depth = 2 means: main page + one level of includes
res_opt.max_handling_depth = 2
```

### Что делает `max_handling_depth`?

- **Глубина 1** → Только корневой HTML‑файл, все внешние ресурсы игнорируются.  
- **Глубина 2** → Корень плюс любые напрямую указанные файлы (например, `iframe` или сервер‑сайд включение).  
- **Более высокие значения** → Глубокие вложения, но также больший размер вывода и более длительное время обработки.

Ограничивая глубину значением **2**, мы сохраняем основную страницу и один уровень включений, отбрасывая всё более глубокое. Обычно этого достаточно, чтобы избавиться от лишних подвалов, аналитических скриптов или вложенных шаблонов, которые не нужны в обрезанной копии.

---

## Шаг 3: Привязка параметров к конфигурации сохранения

Теперь мы связываем наши правила ресурсов с экземпляром `SaveOptions`. Этот объект указывает библиотеке *точно*, как записать файл обратно на диск.

```python
from htmlprocessor import SaveOptions

save_opt = SaveOptions()
save_opt.resource_handling_options = res_opt
```

> **Зачем использовать `SaveOptions`?**  
> Он даёт детальный контроль над выводом — помимо глубины ресурсов. Позже вы сможете добавить сжатие, красивый вывод или даже пользовательские колбэки, не меняя основную логику сохранения.

---

## Шаг 4: Как использовать SaveOptions для обрезки HTML‑страницы

Наконец, вызываем метод `save` с нашими настроенными параметрами. Библиотека пройдётся по DOM, учтёт ограничение глубины и запишет обрезанный файл.

```python
# Save the trimmed document
output_path = "YOUR_DIRECTORY/trimmed_page.html"
doc.save(output_path, save_opt)

print(f"Trimmed page saved to {output_path}")
```

### Ожидаемый результат

- Файл `trimmed_page.html` содержит оригинальную разметку **плюс** любые включения до одного уровня вложения.  
- Все более глубокие включения опускаются, что приводит к меньшему и быстрее загружаемому файлу.  
- Не появляется сломанных тегов — библиотека автоматически закрывает любые элементы, оставшиеся «висячими» после удаления.

Вы можете открыть полученный файл в браузере, чтобы убедиться, что основной контент всё ещё отображается, а лишние скрипты или вложенные фреймы исчезли.

---

## Полный рабочий пример

Объединяя всё вместе, представляем полный скрипт, который можно скопировать и запустить:

```python
# -*- coding: utf-8 -*-
"""
Trim an HTML page using SaveOptions.
Demonstrates:
- How to load an HTML document
- How to configure ResourceHandlingOptions
- How to use SaveOptions to save a trimmed version
"""

from htmlprocessor import HTMLDocument, SaveOptions, ResourceHandlingOptions

def trim_html(input_path: str, output_path: str, max_depth: int = 2) -> None:
    # Load the source document
    doc = HTMLDocument(input_path)
    print("Loaded:", doc.title or "Untitled")

    # Set up resource handling (how to trim HTML page)
    res_opt = ResourceHandlingOptions()
    res_opt.max_handling_depth = max_depth

    # Attach options to save configuration (how to use SaveOptions)
    save_opt = SaveOptions()
    save_opt.resource_handling_options = res_opt

    # Perform the save
    doc.save(output_path, save_opt)
    print(f"Trimmed HTML saved to {output_path}")

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/complex_page.html"
    OUTPUT = "YOUR_DIRECTORY/trimmed_page.html"
    trim_html(INPUT, OUTPUT, max_depth=2)
```

Запустите скрипт, укажите `INPUT` на любой сложный HTML‑файл, и вы получите более лёгкую версию в `OUTPUT`.  

> **Примечание о граничных случаях:** Если оригинальная страница содержит условные комментарии (`<!--[if IE]>…<![endif]-->`), которые ссылаются на более глубокие ресурсы, они будут удалены так же, как и любые другие вложенные включения. Это предотвращает рост размера из‑за старых IE‑хака.

---

## Визуальное резюме

Ниже представлена быстрая диаграмма, иллюстрирующая поток — от загрузки документа, через обработку ресурсов, к сохранению обрезанного результата.

![пример использования saveoptions](https://example.com/placeholder.png "Диаграмма, показывающая, как использовать SaveOptions для обрезки HTML‑страниц")

*Alt text:* **пример использования saveoptions** – показывает трёхшаговый процесс загрузки, настройки и сохранения HTML‑документа.

---

## Часто задаваемые вопросы и подводные камни

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если нужна более глубокая вложенность?** | Увеличьте `max_handling_depth` до 3 или 4, но помните, что размер вывода возрастёт. |
| **Можно ли исключить определённые теги (например, `<script>`), независимо от глубины?** | Да — `SaveOptions` также поддерживает свойство `tag_exclusion_list`. Добавьте `"script"` в этот список, чтобы всегда удалять скрипты. |
| **Является ли библиотека потокобезопасной?** | Текущая версия не является потокобезопасной. Создавайте отдельный `HTMLDocument` для каждого потока. |
| **Будут ли переписаны относительные URL?** | По умолчанию — нет. Используйте `save_opt.rewrite_relative_urls = True`, если необходимо скорректировать их под новое расположение. |

---

## Следующие шаги

Теперь, когда вы освоили **как использовать SaveOptions**, попробуйте следующие расширения:

- **Сжать вывод:** Установите `save_opt.enable_gzip = True` для уменьшения файлов при передаче по сети.  
- **Красивый вывод для отладки:** Переключите `save_opt.indent_output = True`, чтобы получить красиво отформатированный HTML.  
- **Пакетная обработка:** Пройдитесь по каталогу HTML‑файлов и примените ту же логику обрезки — отлично подходит для генераторов статических сайтов.

Каждое из этих улучшений опирается на ту же основу, которую вы только что изучили, помогая держать код чистым и поддерживаемым.

---

## Заключение

Мы прошли весь жизненный цикл обрезки HTML‑страницы в Python: **как загрузить HTML‑документ**, настроить **как обрезать HTML‑страницу** с помощью `ResourceHandlingOptions` и, наконец, **как использовать SaveOptions** для записи очищенного файла. Пример полностью автономный, работает «из коробки» и демонстрирует, почему контроль глубины ресурсов — важная оптимизация для веб‑скрейпинга, генерации статических сайтов или любой ситуации, где нужен лёгкий HTML‑снимок.

Попробуйте, экспериментируйте с разными значениями `max_handling_depth`, и позвольте обрезанным страницам выполнять тяжёлую работу за вас. Если возникнут вопросы, оставляйте комментарий ниже — happy coding!

## Связанные руководства

- [Как сохранить HTML в C# — Полное руководство с пользовательским обработчиком ресурсов](/html/english/net/working-with-html-documents/how-to-save-html-in-c-complete-guide-using-a-custom-resource/)
- [Как отрендерить HTML в PNG — Полное руководство для C#](/html/english/net/rendering-html-documents/how-to-render-html-as-png-complete-c-guide/)
- [Как упаковать HTML в ZIP в C# — Сохранить HTML в ZIP](/html/english/net/html-extensions-and-conversions/how-to-zip-html-in-c-save-html-to-zip/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}