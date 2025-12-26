---
date: 2025-12-10
description: Aprende a usar Aspose para manejar enlaces rotos en Java, convertir HTML
  a PNG y cargar documentos HTML en Java con Aspose.HTML para Java.
linktitle: Use Message Handlers in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Cómo usar los controladores de mensajes de Aspose.HTML en Java
url: /es/java/configuring-environment/use-message-handlers/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo usar los manejadores de mensajes de Aspose.HTML en Java

## Introducción
En este tutorial se muestra paso a paso **cómo usar aspose** para manejar recursos faltantes en HTML. Crearemos un documento HTML sencillo que hace referencia a una imagen inexistente, adjuntaremos un manejador de mensajes personalizado y le mostraremos cómo **cargar documento html java** manejando de forma elegante los enlaces rotos. Al final, también verá cómo **convertir html a png** usando Aspose.HTML, obteniendo una visión completa de la conversión de HTML a imagen en Java.

## Respuestas rápidas
- **¿Cuál es el propósito principal de un manejador de mensajes?** Interceptar operaciones de red y reaccionar a códigos de estado como recursos faltantes.  
- **¿Puede Aspose.HTML convertir HTML a PNG?** Sí, usando `Converter.convertHTML` puede realizar la conversión de html a imagen.  
- **¿Necesito una licencia para este ejemplo?** Una licencia temporal elimina los límites de evaluación; se requiere una licencia permanente para producción.  
- **¿Qué versión de Java es compatible?** Cualquier JDK 8+ (el tutorial usa JDK 11).  
- **¿Es posible manejar varios enlaces rotos?** Absolutamente – puede encadenar varios manejadores para gestionar diferentes escenarios.

## Requisitos previos
Antes de sumergirnos en la guía paso a paso, asegúrese de contar con todo lo necesario:
1. Java Development Kit (JDK): Verifique que tenga el JDK instalado en su sistema. Puede descargarlo desde el [sitio web de Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2. Aspose.HTML for Java: Necesitará tener Aspose.HTML for Java instalado. Puede descargarlo desde la [página de lanzamientos de Aspose](https://releases.aspose.com/html/java/).
3. IDE: Use su entorno de desarrollo integrado (IDE) favorito para Java, como IntelliJ IDEA, Eclipse o NetBeans.
4. Conocimientos básicos de Java: Familiaridad con la programación en Java es esencial para seguir este tutorial de manera eficaz.
5. Licencia temporal: Si está usando la versión de prueba de Aspose.HTML, considere obtener una [licencia temporal](https://purchase.aspose.com/temporary-license/) para evitar limitaciones durante el desarrollo.

## Importar paquetes
Antes de comenzar, asegúrese de haber importado los paquetes necesarios en su proyecto Java. A continuación se muestran las importaciones esenciales que necesitará:
```java
import java.io.IOException;
```
Estas importaciones le darán acceso a las clases y métodos requeridos para manejar operaciones de red, crear documentos HTML y realizar la conversión de HTML a PNG.

## Paso 1: Preparar el código HTML
Lo primero que necesitamos es un fragmento HTML sencillo que haga referencia a un archivo de imagen. Deliberadamente referiremos una imagen que no existe para activar el mecanismo de manejo de errores.
```java
String code = "<img src='missing.jpg'>";
```
Este código crea una etiqueta `<img>` que apunta a `missing.jpg`. Como la imagen falta, el servicio de red devolverá un código de estado distinto de 200, que nuestro manejador personalizado capturará.

## Paso 2: Escribir el código HTML en un archivo
A continuación, debemos persistir el fragmento HTML para que Aspose.HTML pueda cargarlo como documento.
```java
try (java.io.FileWriter fileWriter = new java.io.FileWriter("document.html")) {
    fileWriter.write(code);
}
```
Usando un `FileWriter` guardamos el HTML en **document.html**. Este archivo se convierte en la fuente para el paso **cargar documento html java** más adelante.

## Paso 3: Crear un manejador de mensajes personalizado
Ahora construyamos un manejador de mensajes personalizado que reaccione cuando la imagen no se encuentre. El manejador verifica el código de estado HTTP y muestra un mensaje amigable.
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
El método `invoke` examina `context.getResponse().getStatusCode()`. Si no es **200**, emitimos una advertencia clara de que el archivo falta. La llamada final `invoke(context);` pasa el control al siguiente manejador en la cadena.

## Paso 4: Configurar el servicio de red
Para que Aspose.HTML reconozca nuestro manejador, lo registramos en el servicio de red mediante la clase `Configuration`.
```java
com.aspose.html.Configuration configuration = new com.aspose.html.Configuration();
try {
    com.aspose.html.services.INetworkService network = configuration.getService(com.aspose.html.services.INetworkService.class);
    network.getMessageHandlers().addItem(handler);
```
Aquí creamos una instancia de `Configuration`, obtenemos el `INetworkService` y añadimos nuestro manejador personalizado a su colección. Esto garantiza que el manejador se ejecute durante cualquier solicitud de red, como la carga de imágenes.

## Paso 5: Cargar el documento HTML
Con la configuración lista, ahora podemos cargar el archivo HTML que creamos anteriormente. Este paso demuestra **cargar documento html java** mientras la imagen faltante activa nuestro manejador.
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
El constructor `HTMLDocument` recibe tanto la ruta del archivo como la `configuration` personalizada. Cuando el documento analiza la etiqueta `<img>`, el servicio de red intenta obtener `missing.jpg`, recibe un 404 y nuestro manejador muestra la advertencia.

## Paso 6: Convertir HTML a PNG
Para ilustrar las capacidades más amplias de Aspose.HTML, convertiremos el documento cargado a una imagen PNG. Este es un escenario clásico de **convertir html a png**.
```java
com.aspose.html.converters.Converter.convertHTML(
    document,
    new com.aspose.html.saving.ImageSaveOptions(),
    "output.png"
);
```
`Converter.convertHTML` toma el `HTMLDocument`, opciones opcionales `ImageSaveOptions` (donde podría establecer DPI, calidad, etc.) y el nombre del archivo de salida. El resultado es una imagen rasterizada del HTML renderizado.

## Paso 7: Liberar recursos
Una gestión adecuada de recursos es esencial en cualquier aplicación Java. Liberamos tanto la `Configuration` como el `HTMLDocument` para evitar fugas de memoria.
```java
} finally {
    if (configuration != null) {
        configuration.dispose();
    }
}
```
Encerrar la limpieza en un bloque `finally` garantiza su ejecución incluso si ocurre una excepción antes.

## ¿Por qué usar manejadores de mensajes?
Los manejadores de mensajes le brindan control granular sobre operaciones de red como **manejar enlaces rotos java**. En lugar de permitir que la biblioteca falle silenciosamente, puede registrar, reintentar, reemplazar recursos o proporcionar contenido alternativo, haciendo su procesamiento de HTML robusto y listo para producción.

## Problemas comunes y soluciones
- **Recursión del manejador** – Asegúrese de llamar a `invoke(context);` solo una vez para evitar bucles infinitos.  
- **Licencia ausente** – Sin una licencia válida, la conversión puede generar una imagen con marca de agua.  
- **Errores en la ruta del archivo** – Use rutas absolutas o configure correctamente el directorio de trabajo al cargar `document.html`.

## Preguntas frecuentes

**P: ¿Puedo encadenar varios manejadores de mensajes?**  
R: Sí, puede añadir varios manejadores a la colección `network.getMessageHandlers()`; se ejecutarán en el orden en que se agreguen.

**P: ¿El manejador funciona también para recursos CSS o scripts?**  
R: Absolutamente—cualquier solicitud de red realizada por el motor HTML (imágenes, CSS, JS, fuentes) pasa por el manejador.

**P: ¿Cómo modifico la solicitud HTTP antes de enviarla?**  
R: Implemente un manejador que modifique `context.getRequest()` antes de llamar a `invoke(context)`.

**P: ¿Existe una forma de suprimir la advertencia para URLs específicas?**  
R: Dentro del manejador, inspeccione `context.getRequest().getRequestUri()` y omita el registro de forma condicional.

**P: ¿Qué versión de Aspose.HTML se requiere para estas API?**  
R: El código funciona con Aspose.HTML for Java 22.10 y versiones posteriores.

## Conclusión
Y eso es todo: una guía completa sobre **cómo usar aspose** manejadores de mensajes en Java. Cubrimos la creación de un archivo HTML, la conexión de un manejador personalizado para **manejar enlaces rotos java**, la carga del documento y la ejecución de **convertir html a png**. Con este patrón podrá gestionar recursos faltantes con confianza, aplicar políticas personalizadas y ampliar las capacidades de red de Aspose.HTML en cualquier aplicación Java.

---

**Última actualización:** 2025-12-10  
**Probado con:** Aspose.HTML for Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}