---
date: 2025-12-10
description: Узнайте, как использовать Aspose для обработки битых ссылок в Java, конвертировать
  HTML в PNG и загружать HTML‑документ в Java с помощью Aspose.HTML для Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Как использовать обработчики сообщений Aspose.HTML в Java
url: /ru/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать обработчики сообщений Aspose.HTML в Java

## Введение
В этом руководстве пошагово демонстрируется **how to use aspose** для обработки отсутствующих ресурсов в HTML. Мы создадим простой HTML‑документ, который ссылается на отсутствующее изображение, прикрепим пользовательский обработчик сообщений и покажем, как **load html document java**, корректно обрабатывая битые ссылки. В конце вы также увидите, как **convert html to png** с помощью Aspose.HTML, получив полное представление о конвертации HTML в изображение в Java.

## Быстрые ответы
- **What is the primary purpose of a message handler?** Перехватывать сетевые операции и реагировать на коды статуса, такие как отсутствующие ресурсы.  
- **Can Aspose.HTML convert HTML to PNG?** Да, используя `Converter.convertHTML` вы можете выполнять конвертацию html в изображение.  
- **Do I need a license for this example?** Временная лицензия снимает ограничения оценки; постоянная лицензия требуется для продакшна.  
- **Which Java version is supported?** Любой JDK 8+ (в руководстве используется JDK 11).  
- **Is it possible to handle multiple broken links?** Абсолютно — вы можете цепочкой добавить несколько обработчиков для управления разными сценариями.

## Требования
1. Java Development Kit (JDK): Убедитесь, что JDK установлен в вашей системе. Вы можете скачать его с [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML for Java: Вам необходимо установить Aspose.HTML for Java. Вы можете скачать его со [Aspose releases page](https://releases.aspose.com/html/java/).
3. IDE: Используйте вашу любимую интегрированную среду разработки Java (IDE), например IntelliJ IDEA, Eclipse или NetBeans.
4. Basic Knowledge of Java: Знание программирования на Java необходимо для эффективного следования этому руководству.
5. Temporary License: Если вы используете пробную версию Aspose.HTML, рассмотрите возможность получения [temporary license](https://purchase.aspose.com/temporary-license/) чтобы избежать ограничений во время разработки.

## Импорт пакетов
Прежде чем начать, убедитесь, что необходимые пакеты импортированы в ваш Java‑проект. Ниже приведены основные импорты, которые вам понадобятся:
```java
import java.io.IOException;
```
Эти импорты предоставят вам доступ к классам и методам, необходимым для обработки сетевых операций, создания HTML‑документов и выполнения конвертации HTML‑в‑PNG.

## Шаг 1: Подготовьте HTML‑код
Первое, что нам нужно, — простой фрагмент HTML, который ссылается на файл изображения. Мы намеренно укажем изображение, которого не существует, чтобы вызвать механизм обработки ошибок.
```java
String code = "<img src='missing.jpg'>";
```
Этот код создает тег `<img>`, указывающий на `missing.jpg`. Поскольку изображение отсутствует, сетевой сервис вернёт код статуса, отличный от 200, который наш пользовательский обработчик перехватит.

## Шаг 2: Запишите HTML‑код в файл
Далее нам нужно сохранить фрагмент HTML, чтобы Aspose.HTML мог загрузить его как документ.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
С помощью `FileWriter` мы сохраняем HTML в **document.html**. Этот файл становится источником для шага **load html document java** позже.

## Шаг 3: Создайте пользовательский обработчик сообщений
Теперь создадим пользовательский обработчик сообщений, который реагирует, когда изображение не найдено. Обработчик проверяет HTTP‑код статуса и выводит дружелюбное сообщение.
```java
com.aspose.html.net.MessageHandler handler = new com.aspose.html.net.MessageHandler() {
    @Override
    public void invoke(com.aspose.html.net.INetworkOperationContext context) {
        if (context.getResponse().getStatusCode() != 200) {
            System.out.println(String.format("File '%s' Not Found", context.getRequest().getRequestUri().toString()));
        }
        invoke(context);
    }
};
```
Метод `invoke` проверяет `context.getResponse().getStatusCode()`. Если он не **200**, мы выводим чёткое предупреждение, что файл отсутствует. Финальный вызов `invoke(context);` передаёт управление следующему обработчику в цепочке.

## Шаг 4: Настройте сетевой сервис
Чтобы Aspose.HTML знал о нашем обработчике, мы регистрируем его в сетевом сервисе через класс `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Здесь мы создаём экземпляр `Configuration`, получаем `INetworkService` и добавляем наш пользовательский обработчик в его коллекцию. Это гарантирует, что обработчик будет выполнен при любом сетевом запросе, например при загрузке изображений.

## Шаг 5: Загрузите HTML‑документ
С готовой конфигурацией мы теперь можем загрузить HTML‑файл, созданный ранее. Этот шаг демонстрирует **load html document java**, пока отсутствующее изображение вызывает наш обработчик.
```java
com.aspose.html.HTMLDocument document = new com.aspose.html.HTMLDocument("document.html", configuration);
try {
    // Additional operations will go here
} finally {
    if (document != null) {
        document.dispose();
    }
}
```
Конструктор `HTMLDocument` принимает путь к файлу и пользовательскую `configuration`. Когда документ парсит тег `<img>`, сетевой сервис пытается получить `missing.jpg`, получает 404, и наш обработчик выводит предупреждение.

## Шаг 6: Конвертируйте HTML в PNG
Чтобы продемонстрировать более широкие возможности Aspose.HTML, мы конвертируем загруженный документ в PNG‑изображение. Это классический сценарий **convert html to png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` принимает `HTMLDocument`, необязательный `ImageSaveOptions` (где можно задать DPI, качество и т.д.) и имя выходного файла. В результате получается растровое изображение отрендеренного HTML.

## Шаг 7: Очистка ресурсов
Правильное управление ресурсами необходимо в любом Java‑приложении. Мы освобождаем как `Configuration`, так и `HTMLDocument`, чтобы избежать утечек памяти.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Обёртывание очистки в блок `finally` гарантирует её выполнение, даже если ранее возникло исключение.

## Зачем использовать обработчики сообщений?
Обработчики сообщений дают вам тонкий контроль над сетевыми операциями, такими как **handle broken links java**. Вместо того чтобы библиотека молча падала, вы можете вести журнал, повторять запросы, заменять ресурсы или предоставлять запасной контент — делая обработку HTML надёжной и готовой к продакшну.

## Распространённые проблемы и решения
- **Handler recursion** — Убедитесь, что вызываете `invoke(context);` только один раз, чтобы избежать бесконечных циклов.  
- **Missing license** — Без действующей лицензии конвертация может создавать изображение с водяным знаком.  
- **File path errors** — Используйте абсолютные пути или правильно задайте рабочий каталог при загрузке `document.html`.

## Часто задаваемые вопросы

**Q: Могу ли я цепочкой добавить несколько обработчиков сообщений?**  
A: Да, вы можете добавить несколько обработчиков в коллекцию `network.getMessageHandlers()`; они будут выполнены в порядке добавления.

**Q: Обрабатывает ли обработчик ресурсы CSS или скрипты?**  
A: Абсолютно — любой сетевой запрос, сделанный HTML‑движком (изображения, CSS, JS, шрифты), проходит через обработчик.

**Q: Как изменить HTTP‑запрос перед отправкой?**  
A: Реализуйте обработчик, который модифицирует `context.getRequest()` перед вызовом `invoke(context)`.

**Q: Можно ли подавить предупреждение для определённых URL?**  
A: Внутри обработчика проверьте `context.getRequest().getRequestUri()` и условно пропустите запись в журнал.

**Q: Какая версия Aspose.HTML требуется для этих API?**  
A: Код работает с Aspose.HTML for Java 22.10 и более поздними версиями.

## Заключение
И вот он — всестороннее руководство по **how to use aspose** обработчикам сообщений в Java. Мы рассмотрели создание HTML‑файла, подключение пользовательского обработчика к **handle broken links java**, загрузку документа и выполнение **convert html to png**. С помощью этого шаблона вы сможете уверенно управлять отсутствующими ресурсами, применять пользовательские политики и расширять сетевые возможности Aspose.HTML в любом Java‑приложении.

---

**Последнее обновление:** 2025-12-10  
**Тестировано с:** Aspose.HTML for Java 24.11  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}