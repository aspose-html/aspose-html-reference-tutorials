---
category: general
date: 2026-06-16
description: Узнайте, как установить DPI устройства в Aspose и задать ширину и высоту
  области просмотра при рендеринге HTML с помощью песочницы Aspose.HTML в Java. Включён
  пошаговый код.
draft: false
keywords:
- set device dpi aspose
- set viewport width height
language: ru
og_description: Узнайте, как установить DPI устройства в Aspose и задать ширину и
  высоту области просмотра, используя песочницу Aspose.HTML для Java. Полный код и
  объяснение.
og_title: Установка DPI устройства в Aspose на Java – Полное руководство по Sandbox
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  headline: set device dpi aspose in Java – Complete Sandbox Guide
  type: TechArticle
- description: Learn how to set device dpi aspose and set viewport width height when
    rendering HTML with Aspose.HTML sandbox in Java. Step‑by‑step code included.
  name: set device dpi aspose in Java – Complete Sandbox Guide
  steps:
  - name: Configure sandbox options (including DPI and viewport size).
    text: Configure sandbox options (including DPI and viewport size).
  - name: Instantiate a `DocumentSandbox` with those options.
    text: Instantiate a `DocumentSandbox` with those options.
  - name: Load an external HTML page inside the sandbox.
    text: Load an external HTML page inside the sandbox.
  - name: Perform a simple DOM operation—printing the page title.
    text: Perform a simple DOM operation—printing the page title.
  type: HowTo
tags:
- Aspose.HTML
- Java
- HTML rendering
- Sandbox
title: Установить DPI устройства Aspose в Java – Полное руководство по Sandbox
url: /ru/java/advanced-usage/set-device-dpi-aspose-in-java-complete-sandbox-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set device dpi aspose – Руководство по Java Sandbox

Когда‑нибудь задавались вопросом, как **set device dpi aspose** при рендеринге веб‑страницы на Java? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда необходимо, чтобы отрисованная страница выглядела точно так же, как на реальном экране — особенно когда DPI важен для расчётов макета.  

В этом руководстве мы пройдём практический пример, который не только **set device dpi aspose**, но и покажет, как **set viewport width height**, чтобы страница вела себя так же, как в окне браузера размером 1280 × 800 пикселей. К концу вы получите готовый фрагмент кода, чёткое объяснение каждого шага и советы по избежанию типичных ошибок.

## Что покрывает этот учебник

Мы начнём с описания предпосылок, а затем перейдём к четырём лаконичным шагам:

1. Настроить параметры sandbox (включая DPI и размер viewport).  
2. Создать `DocumentSandbox` с этими параметрами.  
3. Загрузить внешнюю HTML‑страницу в sandbox.  
4. Выполнить простую DOM‑операцию — вывести заголовок страницы.

Вы увидите, почему каждый элемент важен, как подстроить настройки под разные устройства и как выглядит ожидаемый вывод. Внешняя документация не требуется; всё, что нужно, находится здесь.

## Предпосылки

- Java 8 или новее (библиотека Aspose.HTML for Java поддерживает JDK 8+).  
- JAR‑файлы Aspose.HTML for Java, добавленные в classpath вашего проекта.  
- IDE или система сборки (Maven/Gradle) для компиляции и запуска кода.  
- Доступ в Интернет, если планируется загрузка живого URL, например `https://example.com`.

Если все пункты отмечены, приступаем.

## Шаг 1: Set device DPI aspose – определение параметров Sandbox

Первое, что нужно сделать, — сообщить sandbox, какой «экран» вы имитируете. Здесь и вступает в игру **set device dpi aspose**. DPI (dots per inch) влияет на интерпретацию CSS‑единиц `px`, что может менять размеры шрифтов, масштаб изображений и медиазапросы.

```java
// Step 1: Create sandbox options and configure DPI and viewport.
SandboxOptions sandboxOptions = new SandboxOptions();
sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
sandboxOptions.setViewportWidth(1280);         // set viewport width height
sandboxOptions.setViewportHeight(800);         // set viewport width height
```

> **Почему это важно:**  
> *Вызов `setDeviceDpi` сообщает Aspose.HTML рассматривать один CSS‑пиксель как 1/96 дюйма, что соответствует большинству настольных мониторов. Если пропустить этот шаг, макет может выглядеть слишком мелким или слишком крупным на экранах с высоким DPI.*

## Шаг 2: Создание Sandbox с настроенными параметрами

Теперь, когда параметры готовы, нужен экземпляр sandbox, который их учитывает. Представьте sandbox как маленький изолированный движок браузера, который не трогает вашу файловую систему.

```java
// Step 2: Initialise the DocumentSandbox using the options above.
DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);
```

> **Pro tip:**  
> Повторное использование одного и того же `DocumentSandbox` для нескольких страниц экономит память, но не забудьте сбросить параметры, если позже понадобится другое DPI или размер viewport.

## Шаг 3: Загрузка HTML‑документа в Sandbox

С готовым sandbox загрузка страницы проста. Конструктор `HTMLDocument` принимает URL и sandbox, который вы только что создали.

```java
// Step 3: Load a remote HTML page using the sandbox.
HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);
```

> **Edge case:**  
> Если целевой сайт блокирует автоматические запросы, вы можете получить ошибку 403. В этом случае либо скачайте HTML локально и загрузите его из файлового пути, либо задайте пользовательскую строку user‑agent через `sandboxOptions`.

## Шаг 4: Обычные DOM‑операции – вывод заголовка страницы

На данном этапе страница полностью отрисована внутри sandbox, поэтому любой запрос к DOM работает точно так же, как в полном браузере. Оставим всё просто и получим заголовок.

```java
// Step 4: Access the DOM – print the page title.
System.out.println("Title: " + htmlDoc.getTitle());
```

**Ожидаемый вывод**

```
Title: Example Domain
```

Если вы видите что‑то другое, проверьте доступность URL и убедитесь, что случайно не изменили значения DPI или viewport.

## Почему установка Viewport Width Height критична

Вы можете спросить: «Зачем нам **set viewport width height**?» Ответ кроется в адаптивном дизайне. Медиа‑запросы вроде `@media (max-width: 600px)` реагируют на размеры viewport, а не на физический размер экрана. Указав `1280` × `800`, вы гарантируете, что страница отобразит «десктопный» макет, даже если код запускается на безголовом сервере без дисплея.

```java
sandboxOptions.setViewportWidth(1280);   // set viewport width height
sandboxOptions.setViewportHeight(800);   // set viewport width height
```

Изменяя эти числа, вы можете симулировать планшеты, телефоны или даже ультраширокие мониторы, не выходя из IDE.

## Полный рабочий пример

Ниже представлен полностью готовый к запуску Java‑класс, который объединяет всё. Скопируйте его в файл `SandboxExample.java`, добавьте JAR‑файлы Aspose.HTML в classpath и выполните `javac SandboxExample.java && java SandboxExample`.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.DocumentSandbox;
import com.aspose.html.sandbox.SandboxOptions;

public class SandboxExample {
    public static void main(String[] args) {
        // Step 1: Define sandbox options – set device DPI and viewport.
        SandboxOptions sandboxOptions = new SandboxOptions();
        sandboxOptions.setDeviceDpi(96);               // set device dpi aspose
        sandboxOptions.setViewportWidth(1280);         // set viewport width height
        sandboxOptions.setViewportHeight(800);         // set viewport width height

        // Step 2: Create a DocumentSandbox using the defined options.
        DocumentSandbox documentSandbox = new DocumentSandbox(sandboxOptions);

        // Step 3: Load an HTML document inside the sandbox.
        HTMLDocument htmlDoc = new HTMLDocument("https://example.com", documentSandbox);

        // Step 4: Perform normal DOM operations – print the page title.
        System.out.println("Title: " + htmlDoc.getTitle());
    }
}
```

> **Быстрая проверка:**  
> Запустите программу. Если в консоли появится `Title: Example Domain`, всё настроено правильно. Если нет, проверьте консоль на исключения — большинство проблем связаны с отсутствием JAR‑файлов или сетевыми ограничениями.

## Распространённые ошибки и как их избежать

| Симптом | Вероятная причина | Решение |
|---|---|---|
| `NullPointerException` при `htmlDoc.getTitle()` | Sandbox не загрузил страницу | Проверьте URL, оберните конструктор `HTMLDocument` в try‑catch или включите логирование через `sandboxOptions.setLogLevel(...)`. |
| Макет выглядит увеличенным/уменьшенным | DPI установлен неверно | Убедитесь, что `sandboxOptions.setDeviceDpi(96)` (или ваш целевой DPI). |
| Медиа‑запросы не срабатывают | Отсутствуют размеры viewport | Проверьте, что вызвали оба метода `setViewportWidth` **и** `setViewportHeight`. |
| Ошибка Out‑of‑memory на больших страницах | Повторное использование одного sandbox для многих тяжёлых страниц | Создавайте новый `DocumentSandbox` для каждой страницы или вызывайте `documentSandbox.dispose()` после использования. |

## Расширение примера

Теперь, когда вы знаете, как **set device dpi aspose** и **set viewport width height**, можно экспериментировать дальше:

- **Сделать скриншот** отрисованной страницы с помощью `htmlDoc.renderToBitmap(...)`.  
- **Вставить пользовательский CSS** перед рендерингом для тестирования тёмных тем.  
- **Запустить JavaScript** внутри sandbox через `htmlDoc.getWindow().eval(...)`.  

Все эти действия учитывают настроенные DPI и viewport, предоставляя надёжную площадку для тестирования адаптивных макетов.

## Заключение

Мы только что прошли через лаконичное, сквозное решение, показывающее, как **set device dpi aspose** и **set viewport width height** с помощью sandbox Aspose.HTML в Java. Теперь у вас есть прочная база для рендеринга страниц точно так, как они выглядят на любом устройстве, из безопасного изолированного окружения.

Готовы к следующему шагу? Попробуйте отрисовать страницу, использующую CSS‑grid, или подключите удалённый stylesheet и посмотрите, как DPI влияет на рендеринг шрифтов. Sandbox даёт свободу экспериментировать, не затрагивая вашу хост‑систему.

Если возникнут трудности, оставьте комментарий ниже или обратитесь к документации Aspose.HTML for Java — хотя всё необходимое уже изложено здесь. Приятного кодинга!  

![set device dpi aspose sandbox diagram](https://example.com/images/set-device-dpi-aspose.png "Diagram showing DPI and viewport configuration in Aspose.HTML sandbox")


## Что изучать дальше?


В следующих учебниках рассматриваются тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Create PDF from HTML using Aspose.HTML for Java – Sandbox](/html/english/java/configuring-environment/implement-sandboxing/)
- [Create PDF from HTML – Set User Style Sheet in Aspose.HTML for Java](/html/english/java/configuring-environment/set-user-style-sheet/)
- [How to Set Charset in Aspose.HTML for Java](/html/english/java/configuring-environment/set-character-set/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}