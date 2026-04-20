---
date: 2026-02-23
description: Aprende cómo convertir archivos zip a PDF usando Aspose.HTML para Java.
  Esta guía paso a paso muestra cómo configurar el servicio de red, agregar un manejador
  personalizado y registrar la duración de la solicitud.
linktitle: Creating Message Handler Pipelines in Aspose.HTML
second_title: Java HTML Processing with Aspose.HTML
title: Cómo convertir ZIP a PDF con Aspose.HTML para Java
url: /es/java/message-handling-networking/message-handler-pipeline/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo convertir ZIP a PDF con Aspose.HTML para Java

## Introducción
En este tutorial completo descubrirás **cómo convertir archivos zip** en documentos PDF usando Aspose.HTML para Java. Recorreremos la creación de una canalización de manejadores de mensajes, la configuración del servicio de red, la incorporación de un manejador personalizado y el registro de la duración de la solicitud, todo manteniendo el código claro y ejecutable. Ya sea que estés automatizando la generación de informes o necesites una forma fiable de empaquetar contenido HTML como PDF, esta guía te cubre.

## Respuestas rápidas
- **¿Qué hace la canalización?** Procesa un archivo ZIP, extrae HTML y lo renderiza a PDF.  
- **¿Qué manejador registra la duración?** `StartRequestDurationLoggingMessageHandler` y `StopRequestDurationLoggingMessageHandler`.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para pruebas; se requiere una licencia comercial para producción.  
- **¿Puedo cambiar la ruta de salida?** Sí, modifica la variable `savePath` en el Paso 1.  
- **¿Qué versión de Java se requiere?** JDK 8 o superior.

## ¿Qué es una canalización de manejadores de mensajes?
Una canalización de manejadores de mensajes es una cadena configurable de componentes de procesamiento que interceptan las solicitudes de red realizadas por Aspose.HTML. Al insertar manejadores personalizados puedes controlar cómo se obtienen, transforman y registran los recursos, ideal para escenarios como convertir un archivo ZIP a PDF.

## ¿Por qué usar una canalización para convertir ZIP a PDF?
- **Control granular** – Añade, reordena o elimina manejadores según tu flujo de trabajo.  
- **Información de rendimiento** – Registra la duración de la solicitud para identificar cuellos de botella.  
- **Extensibilidad** – Conecta tu propia lógica (p. ej., autenticación, caché).  
- **Fiabilidad** – La biblioteca maneja casos extremos como HTML mal formado automáticamente.

## Requisitos previos
- **Java Development Kit (JDK) 8+** – Asegúrate de que `java -version` muestre 8 o superior.  
- **Biblioteca Aspose.HTML para Java** – Descárgala desde la página de [descargas de Aspose](https://releases.aspose.com/html/java/).  
- **Un IDE** – IntelliJ IDEA, Eclipse o NetBeans facilitarán la codificación.  
- **Conocimientos básicos de Java y HTML** – Útiles pero no obligatorios.

## Importar paquetes
Para comenzar, importa las clases que necesitaremos. Estas importaciones nos dan acceso a la configuración, la red y las funciones de renderizado PDF.

```java
import com.aspose.html.Configuration;
import com.aspose.html.HTMLDocument;
import com.aspose.html.net.MessageHandlerCollection;
import com.aspose.html.rendering.pdf.PdfDevice;
import com.aspose.html.services.INetworkService;
```

## Guía paso a paso

### Paso 1: Preparar las rutas a los archivos
```java
// Prepare path to a source zip file
String documentPath = "input/test.zip";
// Prepare path for converted file saving
String savePath = "output/zip-to-pdf-duration.pdf";
```
Establece `documentPath` al ZIP que contiene tus archivos HTML y `savePath` a donde deseas que se guarde el PDF final.

### Paso 2: Crear una instancia de Configuration
```java
// Create an instance of the Configuration class
Configuration configuration = new Configuration();
```
El objeto `Configuration` es la base para personalizar la canalización de procesamiento.

### Paso 3: Inicializar el servicio de red
```java
INetworkService service = configuration.getService(INetworkService.class);
MessageHandlerCollection handlers = service.getMessageHandlers();
```
Aquí **configuramos el servicio de red** y obtenemos la `MessageHandlerCollection`, que es la caja de herramientas para añadir manejadores personalizados.

### Paso 4: Añadir el manejador de mensajes para archivos ZIP
```java
// Custom Schema: ZIP. Add ZipFileSchemaMessageHandler to the end of the pipeline
handlers.addItem(new ZIPFileSchemaMessageHandler(documentPath));
```
Al **añadir un manejador personalizado** (`ZIPFileSchemaMessageHandler`) indicamos a Aspose.HTML cómo tratar el archivo ZIP como un sistema de archivos virtual.

### Paso 5: Insertar el manejador de registro de duración de solicitud al inicio
```java
// Duration Logging. Add the StartRequestDurationLoggingMessageHandler at the first place in the pipeline
handlers.insertItem(0, new StartRequestDurationLoggingMessageHandler());
```
Este manejador **registra la duración de la solicitud** al principio de la canalización, proporcionando una marca de tiempo para cuando comienza el procesamiento.

### Paso 6: Añadir el manejador de registro de duración de solicitud al final
```java
// Add the StopRequestDurationLoggingMessageHandler to the end of the pipeline
handlers.addItem(new StopRequestDurationLoggingMessageHandler());
```
Colocarlo al final permite capturar el tiempo total que lleva convertir el ZIP a PDF.

### Paso 7: Inicializar el documento HTML
```java
// Initialize an HTML document with specified configuration
HTMLDocument document = new HTMLDocument("zip-file:///test.html", configuration);
```
Apuntamos el `HTMLDocument` al archivo HTML de entrada dentro del ZIP (`zip-file:///test.html`). La configuración que construimos antes se aplica automáticamente.

### Paso 8: Crear el dispositivo PDF
```java
// Create the PDF Device
PdfDevice device = new PdfDevice(savePath);
```
El **dispositivo PDF** (`PdfDevice`) es lo que **crea el PDF a partir del contenido del ZIP**. Recibe las páginas renderizadas y las escribe en `savePath`.

### Paso 9: Renderizar el ZIP a PDF
```java
// Render ZIP to PDF
document.renderTo(device);
```
Llamar a `renderTo` desencadena toda la canalización: el ZIP se descomprime, el HTML se renderiza, se registra la duración y se escribe el PDF final.

## Problemas comunes y soluciones
| Problema | Causa | Solución |
|----------|-------|----------|
| `FileNotFoundException` | Ruta `documentPath` o `savePath` incorrecta | Verifica que las rutas sean absolutas o relativas al directorio de trabajo. |
| No hay contenido en el PDF | Nombre de HTML de entrada incorrecto en el constructor de `HTMLDocument` | Asegúrate de que el nombre del archivo coincida exactamente con el HTML dentro del ZIP (`test.html`). |
| La duración no se registra | Manejadores insertados en orden incorrecto | Inserta `StartRequestDurationLoggingMessageHandler` en el índice 0 y `StopRequestDurationLoggingMessageHandler` después de todos los demás manejadores. |
| Funcionalidades HTML no compatibles | Uso de CSS/JS no soportado por Aspose.HTML | Simplifica el marcado o pre‑procesa el HTML antes de renderizar. |

## Preguntas frecuentes

**P: ¿Qué es Aspose.HTML para Java?**  
R: Aspose.HTML para Java es una biblioteca que permite manipular documentos HTML y convertirlos a formatos como PDF, imagen y EPUB.

**P: ¿Cómo descargo Aspose.HTML para Java?**  
R: Puedes descargarla desde la página de [descargas de Aspose](https://releases.aspose.com/html/java/).

**P: ¿Puedo usar Aspose.HTML de forma gratuita?**  
R: Sí, hay una prueba gratuita disponible. Regístrate [aquí](https://releases.aspose.com/).

**P: ¿Dónde encuentro soporte para Aspose.HTML?**  
R: Visita el [Foro de Soporte de Aspose](https://forum.aspose.com/c/html/29) para obtener ayuda de la comunidad y de los ingenieros de Aspose.

**P: ¿Qué son los manejadores de mensajes en Aspose.HTML?**  
R: Los manejadores de mensajes son componentes que interceptan y procesan solicitudes de red dentro de la canalización, útiles para registro, autenticación o recuperación de contenido personalizado.

**P: ¿Cómo puedo añadir mi propio manejador personalizado?**  
R: Implementa `IMessageHandler` y añádelo a la `MessageHandlerCollection` con `handlers.addItem(new MyCustomHandler())`.

**P: ¿Es posible convertir varios archivos ZIP en lote?**  
R: Sí, recorre una lista de rutas ZIP reutilizando la misma configuración y canalización para cada iteración.

## Conclusión
Ahora sabes **cómo convertir archivos zip** en archivos PDF usando Aspose.HTML para Java, con un servicio de red configurable, un manejador ZIP personalizado y un registro preciso de la duración de la solicitud. Esta canalización te brinda control total sobre el proceso de conversión, lo que la hace ideal para informes automatizados, archivado de documentos o cualquier escenario donde el contenido HTML necesite empaquetarse como PDF.

---

**Última actualización:** 2026-02-23  
**Probado con:** Aspose.HTML para Java 24.11  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}