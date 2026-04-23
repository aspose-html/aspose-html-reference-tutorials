---
category: general
date: 2026-04-23
description: Как использовать querySelectorAll в Java для фильтрации элементов по
  классу, чтения значений атрибутов и перебора NodeList для извлечения данных о продуктах.
draft: false
keywords:
- how to use queryselectorall
- how to read attribute
- iterate nodelist java
- filter elements by class
- select elements css selector
language: ru
og_description: Как использовать querySelectorAll в Java для фильтрации элементов
  по классу, чтения значений атрибутов и перебора NodeList для извлечения данных о
  продуктах.
og_title: Как использовать querySelectorAll в Java – фильтрация по классу
tags:
- Java
- HTML parsing
- DOM manipulation
title: Как использовать querySelectorAll в Java – фильтрация по классу
url: /ru/java/creating-managing-html-documents/how-to-use-queryselectorall-in-java-filter-by-class/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать querySelectorAll в Java – Фильтрация по классу

Как использовать querySelectorAll в Java — это ключевой навык, когда нужно извлечь определённые элементы из HTML‑документа. В этом руководстве мы будем фильтровать элементы по классу, считывать значения атрибутов и проходить по NodeList, чтобы получить цены товаров со страницы каталога.  

Когда‑то вы, вероятно, смотрели на огромный HTML‑файл и задавались вопросом, как вытащить только карточки «со скидкой», не пиша кастомный парсер? Именно эту задачу мы решим здесь — без дополнительных библиотек, кроме Aspose.HTML, и с помощью нескольких простых шагов.

В результате вы получите полностью готовую, исполняемую программу, которая:

* **Выбирает элементы** с помощью CSS‑селектора (`select elements css selector`),
* **Фильтрует по классу** (`filter elements by class`),
* **Считывает пользовательский атрибут** (`how to read attribute`),
* **Итерирует полученный NodeList** (`iterate nodelist java`).

Предварительный опыт работы с Aspose.HTML не требуется — достаточно базовой настройки Java и HTML‑файла для тестов.

![пример использования querySelectorAll в Java](https://example.com/images/queryselectorall-java.png "пример использования querySelectorAll в Java")

---

## Что вам понадобится

| Требование | Почему это важно |
|------------|------------------|
| **Java 17+** | Современные возможности языка и улучшенная работа с модулями. |
| **Aspose.HTML for Java** (latest version) | Предоставляет класс `Document` и движок CSS‑селекторов. |
| **catalog.html** (sample HTML) | Исходный файл, по которому будем выполнять запросы. |
| **IDE или обычный `javac`** | Для компиляции и запуска демонстрации. |

Если вы ещё не добавили Aspose.HTML в проект, поместите JAR‑файл в папку `libs` и добавьте его в classpath:

```bash
javac -cp "libs/*" CssSelectorDemo.java
java -cp ".:libs/*" CssSelectorDemo
```

---

## Шаг 1 – Загрузка HTML‑документа

Прежде чем что‑то запросить, нужен объект `Document`, представляющий HTML‑файл. Это как открыть таблицу перед тем, как читать ячейки.

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");
```

> **Почему это важно:** Класс `Document` парсит разметку в дерево DOM, позволяя работать с движком CSS‑селекторов. Пропуск этого шага оставит вас лишь со строкой и без возможности использовать `querySelectorAll`.

---

## Шаг 2 – Выбор элементов с помощью CSS‑селектора

Теперь переходим к сути: **как использовать querySelectorAll**. Метод принимает любой корректный CSS‑селектор, поэтому вы можете быть настолько точными или общими, насколько захотите. В нашем случае нам нужны карточки товаров, которые:

* имеют класс `product-card`,
* также помечены классом `sale`,
* и содержат атрибут `data-price`.

```java
        // Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );
```

> **Объяснение:**  
> * `.product-card.sale` → фильтрует элементы, содержащие **обе** указанные классы.  
> * `[data-price]` → гарантирует наличие атрибута, эффективно **фильтруя элементы по классу** **и** атрибуту в одном вызове.  
> * Результатом является `NodeList` — упорядоченная коллекция, по которой можно итерировать.  

Если вам понадобится **select elements css selector** для другого шаблона, просто измените строку — переписывать код не потребуется.

---

## Шаг 3 – Итерация NodeList в Java

`NodeList` ведёт себя почти как массив, но не реализует `Iterable`. Поэтому мы используем классический `for`‑цикл — идеальный для сценариев **iterate nodelist java**.

```java
        // Iterate over the selected elements
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
```

> **Почему `for`‑цикл?**  
> Он даёт прямой доступ к индексу, что удобно для логирования или условных ветвлений. Если предпочитаете `while`‑цикл, логика останется той же — просто замените конструкцию цикла.

---

## Шаг 4 – Чтение атрибута `data-price`

Теперь мы наконец отвечаем на вопрос **how to read attribute** из элемента. В DOM‑API метод `getAttribute` возвращает сырую строку точно так, как она указана в разметке.

```java
            // Read the price value from the data-price attribute
            String priceValue = productElement.getAttribute("data-price");
```

> **Подсказка:** Если атрибут может отсутствовать, `getAttribute` вернёт `null`. Защищаться от этого можно простой проверкой:

```java
            if (priceValue == null) {
                priceValue = "N/A"; // fallback for missing data-price
            }
```

---

## Шаг 5 – Вывод результатов

И, наконец, выводим каждую цену в консоль. Это имитирует реальный сценарий, когда вы, вероятно, отправляете значения в базу данных или в payload API.

```java
            // Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

### Ожидаемый вывод в консоль

```
Sale item price: 19.99
Sale item price: 34.50
Sale item price: 12.00
```

Если селектор не найдёт подходящих узлов, цикл просто не выполнится — исключения не будет. Это хорошая защита от **edge cases**, когда каталог может быть пустым.

---

## Полный рабочий пример

Собрав всё вместе, получаем полный файл, который можно скопировать в `CssSelectorDemo.java`:

```java
import com.aspose.html.Dom.*;
import com.aspose.html.*;

public class CssSelectorDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the HTML document that contains product listings
        Document catalogDoc = new Document("YOUR_DIRECTORY/catalog.html");

        // Step 2: Select all product cards that are on sale and have a data-price attribute
        NodeList saleProductCards = catalogDoc.querySelectorAll(
                ".product-card.sale[data-price]"
        );

        // Step 3 & 4: Iterate over the selected elements and read the price attribute
        for (int i = 0; i < saleProductCards.getLength(); i++) {
            Element productElement = (Element) saleProductCards.item(i);
            String priceValue = productElement.getAttribute("data-price");
            if (priceValue == null) {
                priceValue = "N/A"; // fallback if attribute is missing
            }

            // Step 5: Output the price of each sale item
            System.out.println("Sale item price: " + priceValue);
        }
    }
}
```

Сохраните файл, скомпилируйте и запустите — наблюдайте, как цены выводятся в консоль. 🎉

---

## Часто задаваемые вопросы и профессиональные советы

| Вопрос | Ответ |
|--------|-------|
| *Что если мне также нужно выбрать по имени тега?* | Просто добавьте тег перед селектором: `document.querySelectorAll("div.product-card.sale[data-price]")`. |
| *Могу ли я цепочкой применять несколько фильтров атрибутов?* | Конечно. Пример: `[data-price][data-stock]` оставит только элементы, имеющие **оба** атрибута. |
| *Является ли `querySelectorAll` чувствительным к регистру?* | Да — в HTML5 CSS‑селекторы рассматривают имена классов и атрибутов как регистрозависимые. |
| *Как обрабатывать огромный HTML‑файл?* | Aspose.HTML потоково читает документ, но вы также можете ограничить селектор поддеревом (`someElement.querySelectorAll(...)`). |
| *What |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}