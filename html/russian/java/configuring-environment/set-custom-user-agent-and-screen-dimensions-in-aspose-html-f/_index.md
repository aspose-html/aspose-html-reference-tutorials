---
category: general
date: 2026-09-29
description: Установите пользовательский агент в Aspose.HTML для Java и узнайте, как
  задать виртуальный размер экрана для точного рендеринга HTML.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom user agent
- set virtual screen size
- specify user agent
- set screen dimensions
- set screen width
language: ru
lastmod: 2026-09-29
og_description: Установите пользовательский агент в Aspose.HTML для Java и узнайте,
  как задать виртуальный размер экрана для точного рендеринга HTML.
og_image_alt: Diagram showing how to set custom user agent and screen dimensions in
  a Java sandbox
og_title: Задайте пользовательский агент и размеры экрана в Aspose.HTML для Java
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Set custom user agent in Aspose.HTML for Java and learn how to set
    virtual screen size for accurate HTML rendering.
  headline: Set custom user agent and screen dimensions in Aspose.HTML for Java
  type: TechArticle
tags:
- Aspose.HTML
- Java
- sandbox
- user agent
- screen size
title: Задайте пользовательский агент и размеры экрана в Aspose.HTML для Java
url: /ru/java/configuring-environment/set-custom-user-agent-and-screen-dimensions-in-aspose-html-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Установите пользовательский агент и размеры экрана в Aspose.HTML для Java

Если вам нужно **установить пользовательский агент** при рендеринге HTML с помощью Aspose.HTML для Java, это руководство покажет, как это сделать. Настраивая песочницу, вы также получаете возможность **установить виртуальный размер экрана**, обеспечивая соответствие макета реальному окну браузера.

В конце этого урока вы получите полностью готовую, исполняемую программу, которая **устанавливает пользовательский агент**, **задаёт ширину экрана** и **задаёт высоту экрана**. Никакие внешние инструменты не требуются — только Aspose.HTML для Java и среда выполнения Java 8+.

## Что вы узнаете

* Как создать `SandboxConfiguration` для изоляции рендеринга.  
* Как **установить пользовательский агент** и почему это важно для адаптивных страниц.  
* Как **установить виртуальный размер экрана** (ширину и высоту) для точного отображения.  
* Как загрузить HTML‑файл в песочницу и сохранить полученный результат.  
* Распространённые подводные камни и рекомендации по лучшим практикам при рендеринге в песочнице.

> **Требования** – Вам нужна действующая лицензия Aspose.HTML для Java, Java 8 или новее, а также IDE (IntelliJ IDEA, Eclipse или VS Code). В примере используется локальный файл `input.html`, но подойдет любой доступный URL.

![Диаграмма потока песочницы](sandbox-flow.png "пример установки пользовательского агента в Java")

## Шаг 1: Создайте конфигурацию песочницы (основа)

Песочница изолирует среду рендеринга от хост‑JVM, что необходимо, когда вы хотите **установить пользовательский агент** или изменить размер области просмотра.

```java
import com.aspose.html.sandbox.SandboxConfiguration;

// Create a fresh sandbox configuration object
SandboxConfiguration sandboxConfig = new SandboxConfiguration();
```

*Зачем этот шаг?*  
`SandboxConfiguration` хранит все параметры рендеринга, включая **размеры экрана** и строки **user‑agent**. Настроив её до загрузки документа, вы гарантируете, что HTML‑движок учтёт эти параметры уже при первом запросе.

## Шаг 2: Установите размеры экрана, имитируя реальное устройство

Адаптивные сайты часто читают `window.innerWidth` и `window.innerHeight`. Чтобы заставить движок думать, что он работает на экране 1024 × 768, вы **устанавливаете виртуальный размер экрана**:

```java
// Define the virtual screen size for the sandboxed document
sandboxConfig.setScreenWidth(1024);   // set screen width
sandboxConfig.setScreenHeight(768);   // set screen height
```

*Почему это важно* – Если не **установить размеры экрана**, рендерер может по умолчанию использовать крошечную область просмотра, из‑за чего CSS‑медиа‑запросы выберут мобильный макет. Явно **установив ширину экрана** и **установив высоту экрана**, вы контролируете, какие CSS‑правила сработают.

## Шаг 3: Укажите строку пользовательского агента

Некоторые веб‑страницы предоставляют разный контент в зависимости от заголовка user‑agent. Чтобы **указать пользовательский агент**, достаточно задать его в конфигурации песочницы:

```java
// Set a custom user‑agent string that will be sent during resource loading
sandboxConfig.setUserAgent("AsposeHTML/1.0");
```

*Зачем использовать пользовательский агент?*  
Пользовательская строка может обойти обнаружение ботов, активировать функции, доступные только на десктопе, или протестировать поведение сайта для конкретной версии браузера. Движок Aspose передаёт это значение в каждом HTTP‑запросе, выполняемом при загрузке внешних ресурсов (CSS, изображения, скрипты).

## Шаг 4: Загрузите HTML‑документ в песочницу

Теперь, когда песочница полностью настроена, загрузите HTML‑файл. Конструктор, принимающий путь к файлу и `SandboxConfiguration`, автоматически применит все заданные параметры.

```java
import com.aspose.html.HTMLDocument;

// Load the HTML file using the previously configured sandbox
HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);
```

Если нужно загрузить документ по удалённому URL, замените путь к файлу строкой URL — Aspose.HTML всё равно будет учитывать **установленный пользовательский агент** и **размеры экрана**.

## Шаг 5: Сохраните обработанный вывод

После завершения загрузки документа вы можете сохранить его в любом поддерживаемом формате. Здесь мы записываем HTML‑файл из песочницы, отражающий любые изменения DOM, вызванные пользовательскими настройками.

```java
// Save the processed document to the desired output location
document.save("YOUR_DIRECTORY/sandboxed_output.html");
```

Сохранённый файл будет содержать тот же разметочный код, но любые скрипты, которые запрашивали `navigator.userAgent` или проверяли `window.innerWidth`, теперь получат значения, которые вы задали.

## Полный, исполняемый пример

Объединив все шаги, получаем самодостаточную программу, которую можно скопировать, вставить и запустить.

```java
import com.aspose.html.HTMLDocument;
import com.aspose.html.sandbox.SandboxConfiguration;

public class SandboxDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a sandbox configuration to isolate the rendering environment
        SandboxConfiguration sandboxConfig = new SandboxConfiguration();

        // Step 2: Define the virtual screen size for the sandboxed document
        sandboxConfig.setScreenWidth(1024);   // set screen width
        sandboxConfig.setScreenHeight(768);   // set screen height

        // Step 3: Set a custom user‑agent string to be used during loading
        sandboxConfig.setUserAgent("AsposeHTML/1.0"); // set custom user agent

        // Step 4: Load the HTML document within the sandbox using the configuration
        HTMLDocument document = new HTMLDocument("YOUR_DIRECTORY/input.html", sandboxConfig);

        // Step 5: Save the processed document to the desired output location
        document.save("YOUR_DIRECTORY/sandboxed_output.html");
    }
}
```

### Ожидаемый вывод

Запуск программы создаёт `sandboxed_output.html`. Если открыть его в браузере и в консоли выполнить `navigator.userAgent`, вы увидите **AsposeHTML/1.0**. Аналогично, `window.innerWidth` вернёт **1024**, подтверждая, что **установка размеров экрана** сработала корректно.

## Часто задаваемые вопросы и обработка крайних случаев

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если страница загружает дополнительные ресурсы с другого домена?** | Песочница передаёт **пользовательский агент** со всеми запросами, но политики кросс‑домена по‑прежнему действуют. При необходимости ослабить ограничения используйте `sandboxConfig.setAllowCrossDomain(true)`. |
| **Можно ли изменить размер экрана после загрузки документа?** | Нет. Размеры экрана читаются во время начального прохода компоновки. Чтобы отрендерить с другими параметрами, создайте новую `SandboxConfiguration` и перезагрузите документ. |
| **Нужно ли вызывать `document.close()`?** | `HTMLDocument` реализует `AutoCloseable`. Использование блока `try‑with‑resources` обеспечивает корректную очистку, но явный вызов `close()` необязателен в простых скриптах. |
| **Чем это отличается от установки user‑agent в HTTP‑клиенте?** | Установка user‑agent в песочнице влияет **на все** запросы ресурсов, выполняемые HTML‑движком, а не только на первоначальное получение HTML. Это более точно имитирует поведение реального браузера. |
| **Безопасна ли песочница для недоверенного HTML?** | Да. Песочница изолирует доступ к файловой системе и ограничивает сетевые вызовы согласно конфигурации, снижая риск воздействия вредоносных скриптов на хост‑JVM. |

## Профессиональные советы

* **Повторное использование конфигураций** – Если вы рендерите множество страниц с одинаковой областью просмотра, создайте один `SandboxConfiguration` и переиспользуйте его, чтобы избежать лишних расходов на создание объектов.  
* **Отладка через логирование** – Включите логирование Aspose.HTML (`sandboxConfig.setLogLevel(LogLevel.DEBUG)`), чтобы увидеть, какие ресурсы были получены с пользовательским агентом.  
* **Комбинация с CSS‑медиа‑запросами** – Регулируя **ширину экрана**, вы можете проверять, как ваш адаптивный дизайн ведёт себя на планшетах, телефонах или больших десктопах без запуска реального браузера.

## Заключение

Теперь вы знаете, как **установить пользовательский агент** и **установить размеры экрана** при рендеринге HTML с помощью Aspose.HTML для Java. Настраивая песочницу, вы изолируете среду, контролируете область просмотра и гарантируете, что внешние ресурсы получают точно те заголовки, которые вы задали. Эта техника незаменима для тестирования адаптивных макетов, обхода блокировок ботов или воспроизведения функций, доступных только на десктопе, в автоматизированных конвейерах.

Далее вы можете изучить **как установить пользовательские cookies** или **как захватывать отрендеренные скриншоты** с помощью API рендеринга Aspose.HTML — обе концепции построены на том же шаблоне конфигурации песочницы, который вы только что освоили.

Удачной разработки!

## Что вам следует изучить дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Рендеринг с высоким DPI в Java – захват скриншотов веб‑страниц с пользовательским агентом](/html/english/java/conversion-html-to-various-image-formats/high-dpi-rendering-in-java-capture-webpage-screenshots-with/)
- [Как загрузить HTML, установить DPI устройства и прочитать цвет фона](/html/english/java/advanced-usage/how-to-load-html-set-device-dpi-read-background-color/)
- [Создание HTML‑файла в Java и настройка сетевого сервиса (Aspose.HTML)](/html/english/java/configuring-environment/setup-network-service/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}