---
date: 2026-02-10
description: Узнайте, как использовать Aspose для обработки битых ссылок в Java, конвертировать
  HTML в PNG и загружать HTML‑документ в Java с помощью Aspose.HTML для Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Конвертировать HTML в PNG с помощью обработчиков сообщений Aspose.HTML в Java
url: /ru/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Преобразование HTML в PNG с помощью Aspose.HTML Message Handlers в Java

## Введение
В этом руководстве вы узнаете **как преобразовать HTML в PNG**, аккуратно обрабатывая отсутствующие ресурсы с помощью Aspose.HTML for Java. Мы пройдем процесс создания небольшого HTML‑файла, который ссылается на несуществующее изображение, подключения **custom message handler** для **перехвата сетевых запросов**, настройки **network service**, загрузки документа и, наконец, выполнения **html to image conversion**. К концу вы получите надёжный шаблон как для **handle broken links java**, так и для получения PNG высокого качества — идеально подходит для отчетов, миниатюр или предварительных просмотров в письмах.

## Быстрые ответы
- **Что делает message handler?** Он перехватывает сетевые операции (например, запросы изображений) и позволяет реагировать на коды статуса, такие как 404.  
- **Может ли Aspose.HTML преобразовать HTML в PNG?** Да — `Converter.convertHTML` выполняет преобразование одним вызовом.  
- **Нужна ли лицензия для этого примера?** Временная лицензия снимает ограничения оценки; постоянная лицензия требуется для использования в продакшене.  
- **Какая версия Java подходит?** Любая JDK 8+ (пример работает на JDK 11).  
- **Можно ли настроить network service?** Конечно — используйте `configuration.getService(INetworkService.class)`, чтобы добавить ваш обработчик.

## Требования
Перед тем как приступить, убедитесь, что у вас готово следующее:

1. **Java Development Kit (JDK)** – загрузите с [Oracle website](https://www.oracle.com/java/technologies/javase-downloads.html).  
2. **Aspose.HTML for Java** – получите библиотеку со [Aspose releases page](https://releases.aspose.com/html/java/).  
3. **IDE** – IntelliJ IDEA, Eclipse или NetBeans подойдут.  
4. **Basic Java knowledge** – вы должны быть уверены в работе с классами, try‑with‑resources и обработкой исключений.  
5. **Temporary License** – если вы используете пробную версию, получите [temporary license](https://purchase.aspose.com/temporary-license/) , чтобы избежать водяных знаков.

## Импорт пакетов
Сначала подключим класс Java I/O, который понадобится для работы с файлами. Остальные классы Aspose будут использоваться с полностью квалифицированными именами позже, чтобы список импортов оставался компактным.

```java
import java.io.IOException;
```

## Шаг 1: Подготовьте HTML‑код
Мы создаём минимальный фрагмент HTML, который намеренно ссылается на отсутствующее изображение. Это вызовет наш обработчик, когда движок попытается загрузить ресурс.

```java
String code = "<img src='missing.jpg'>";
```

## Шаг 2: Запишите HTML‑код в файл
Далее сохраняем фрагмент в *document.html*. Использование блока try‑with‑resources гарантирует правильное закрытие `FileWriter`.

```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```

## Шаг 3: Создайте пользовательский Message Handler
Теперь мы создаём **custom message handler**, который проверяет HTTP‑статус каждого сетевого запроса. Если ответ не `200`, мы записываем дружелюбное предупреждение. Обратите внимание на вызов `invoke(context);` в конце — он передаёт запрос следующему обработчику в цепочке, предотвращая рекурсию.

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

## Шаг 4: Настройте Network Service
Чтобы Aspose.HTML «узнал» о нашем обработчике, получаем **network service** из экземпляра `Configuration` и добавляем обработчик в его коллекцию. Это шаг, где мы **configure network service** для пользовательского поведения.

```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```

## Шаг 5: Загрузите HTML‑документ
После настройки конфигурации загружаем *document.html*. Движок теперь использует наш network service, поэтому запрос к отсутствующему изображению перехватывается добавленным обработчиком.

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

## Шаг 6: Преобразуйте HTML в PNG
Это ядро процесса **html to image conversion**. Метод `Converter.convertHTML` принимает загруженный `HTMLDocument`, необязательный `ImageSaveOptions` (где можно настроить DPI или качество) и имя выходного файла.

```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```

## Шаг 7: Очистите ресурсы
Хорошая практика Java предписывает освобождать все нативные ресурсы. Блок `finally` гарантирует, что `Configuration` будет освобождена, даже если возникнет исключение.

```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```

## Почему использовать Message Handlers?
Message handlers предоставляют **тонкий контроль** над каждым сетевым запросом — будь то изображение, CSS, JavaScript или файл шрифта. Вместо того чтобы библиотека молча падала, вы можете фиксировать отсутствующие ресурсы, предоставлять запасной контент или даже повторять запрос. Это делает ваш конвейер обработки HTML **надёжным**, **готовым к продакшену** и упрощает отладку.

## Распространённые проблемы и решения
- **Handler recursion** — вызывайте `invoke(context);` только один раз, чтобы избежать бесконечных циклов.  
- **Missing license** — без действующей лицензии полученный PNG будет содержать водяной знак.  
- **Incorrect file paths** — используйте абсолютные пути или правильно задайте рабочий каталог при загрузке `document.html`.  
- **Unsupported resource types** — убедитесь, что ресурс, который вы хотите перехватить (изображение, CSS и т.д.), действительно запрашивается движком HTML.

## Часто задаваемые вопросы

**Q: Можно ли цепочкой добавить несколько message handlers?**  
A: Да, вы можете добавить несколько обработчиков в коллекцию `network.getMessageHandlers()`; они будут выполнены в порядке добавления.

**Q: Обрабатывает ли handler ресурсы CSS или скрипты?**  
A: Абсолютно — любой сетевой запрос, сделанный движком HTML (изображения, CSS, JS, шрифты), проходит через обработчик.

**Q: Как изменить HTTP‑запрос перед отправкой?**  
A: Реализуйте обработчик, который модифицирует `context.getRequest()` перед вызовом `invoke(context)`.

**Q: Есть ли способ подавить предупреждение для определённых URL?**  
A: Внутри обработчика проверьте `context.getRequest().getRequestUri()` и условно пропустите запись в лог.

**Q: Какая версия Aspose.HTML требуется для этих API?**  
A: Код работает с Aspose.HTML for Java 22.10 и более новыми версиями.

## Заключение
Теперь у вас есть полный пример **как преобразовать HTML в PNG**, используя **custom message handler** для **перехвата сетевых запросов** и **handle broken links java**. Настроив network service, загрузив документ и вызвав конвертер, вы сможете надёжно генерировать PNG‑миниатюры или скриншоты полной страницы в любом Java‑приложении.

---

**Последнее обновление:** 2026-02-10  
**Тестировано с:** Aspose.HTML for Java 24.11  
**Автор:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}