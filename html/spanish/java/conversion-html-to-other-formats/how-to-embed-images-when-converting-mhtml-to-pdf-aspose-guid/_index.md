---
category: general
date: 2026-03-29
description: Cómo incrustar imágenes al convertir MHTML a PDF con Aspose HTML. Reduce
  el tamaño del archivo PDF y domina las técnicas de Aspose HTML a PDF en minutos.
draft: false
keywords:
- how to embed images
- convert mhtml to pdf
- reduce pdf file size
- aspose html to pdf
- reduce pdf size
language: es
og_description: Cómo incrustar imágenes al convertir MHTML a PDF con Aspose HTML.
  Aprende a reducir el tamaño del archivo PDF y saca el máximo provecho de Aspose
  HTML a PDF.
og_title: Cómo incrustar imágenes al convertir MHTML a PDF – Guía de Aspose
tags:
- Aspose
- Java
- PDF
- MHTML
title: Cómo incrustar imágenes al convertir MHTML a PDF – Guía de Aspose
url: /es/java/conversion-html-to-other-formats/how-to-embed-images-when-converting-mhtml-to-pdf-aspose-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo incrustar imágenes al convertir MHTML a PDF – Guía de Aspose

¿Alguna vez te has preguntado **cómo incrustar imágenes** durante una conversión de MHTML‑a‑PDF y mantener el archivo resultante ligero? No eres el único. Muchos desarrolladores se topan con un problema cuando sus PDFs se inflan porque cada recurso — fuentes, scripts, incluso pequeños íconos — se incluye dentro. ¿La buena noticia? Con Aspose.HTML for Java puedes indicarle al convertidor que incruste **solo las imágenes**, dejando todo lo demás como referencias externas. Ese único ajuste a menudo reduce drásticamente el tamaño del PDF.

En este tutorial recorreremos la conversión de un informe MHTML a PDF, nos enfocaremos en **cómo incrustar imágenes** y añadiremos algunos consejos extra para **reducir el tamaño del archivo PDF**. Al final tendrás una clase Java lista para ejecutar, comprenderás por qué incrustar solo imágenes es importante y sabrás a dónde acudir si más adelante necesitas incrustar fuentes u otros recursos. Sin atajos vagos de “ver la documentación”, solo una solución completa lista para copiar y pegar.

## Lo que aprenderás

- Las llamadas exactas a la API necesarias para **convertir MHTML a PDF** con Aspose.HTML.  
- Cómo configurar `PdfConversionOptions` para que el convertidor **incruste solo imágenes**.  
- Por qué incrustar solo imágenes ayuda a **reducir el tamaño del PDF** y cuándo podrías querer una configuración diferente.  
- Un ejemplo Java completo y ejecutable que puedes añadir a cualquier proyecto Maven/Gradle.  
- Problemas comunes (recursos faltantes, rutas de archivo incorrectas) y soluciones rápidas.

### Prerrequisitos

- Java 8 o superior instalado.  
- Maven o Gradle para gestionar dependencias (mostraremos el fragmento Maven).  
- Biblioteca Aspose.HTML for Java (puedes obtener una prueba gratuita en el sitio de Aspose).  
- Un archivo MHTML que quieras convertir a PDF (el ejemplo usa `report.mhtml`).

> **Consejo profesional:** Mantén tu MHTML y el PDF de salida en la misma carpeta durante las pruebas; las rutas relativas mantienen todo ordenado.

---

## Paso 1 – Añadir Aspose.HTML a tu proyecto

Si usas Maven, pega lo siguiente en tu `pom.xml`. La versión mostrada es la más reciente a partir de marzo 2026; revisa el repositorio de Aspose para versiones más nuevas.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-html</artifactId>
    <version>23.12</version>
</dependency>
```

Para Gradle, el equivalente es:

```groovy
implementation 'com.aspose:aspose-html:23.12'
```

Una vez que la dependencia se resuelva, estarás listo para importar las clases que necesitaremos.

## Paso 2 – Crear opciones de conversión y establecer el modo de incrustación

El corazón de **cómo incrustar imágenes** está en `PdfConversionOptions`. Por defecto Aspose incrusta *todos* los recursos (fuentes, CSS, imágenes). Cambiaremos eso a `EMBED_IMAGES_ONLY`.

```java
// Step 2: Prepare conversion options – embed only images
PdfConversionOptions options = new PdfConversionOptions();
options.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);
```

¿Por qué importa esto? Imagina un informe corporativo que hace referencia a una fuente corporativa almacenada en un recurso de red. Incrustar esa fuente inflaría el PDF en cientos de kilobytes aunque el visor pueda obtenerla de forma remota. Al incrustar solo las imágenes, el PDF conserva la fidelidad visual que necesitas mientras sigue siendo ligero.

## Paso 3 – Realizar la conversión

Ahora llamamos a `Converter.convert`, pasando la ruta del MHTML de origen, la ruta del PDF de destino y las opciones que acabamos de configurar.

```java
// Step 3: Convert MHTML to PDF using the options above
String sourcePath = "YOUR_DIRECTORY/report.mhtml";
String targetPath = "YOUR_DIRECTORY/report.pdf";

Converter.convert(sourcePath, targetPath, options);
```

Si todo está conectado correctamente, verás aparecer un `report.pdf` junto a tu archivo MHTML. Ábrelo; cada imagen del informe original debería estar presente, mientras que fuentes y CSS permanecen como referencias externas.

## Paso 4 – Verificar la reducción del tamaño del PDF

Una rápida comprobación de sentido común ayuda a confirmar que realmente **redujiste el tamaño del PDF**. Compara el tamaño del archivo antes y después de cambiar el modo de incrustación:

```java
File before = new File("YOUR_DIRECTORY/report_full.pdf"); // generated with default settings
File after  = new File(targetPath); // our image‑only PDF

System.out.println("Full embed size: " + before.length() / 1024 + " KB");
System.out.println("Images‑only size: " + after.length() / 1024 + " KB");
```

En la mayoría de los casos observarás una caída del 30‑70 % dependiendo de cuántas fuentes o archivos CSS estaban originalmente incrustados. Es una victoria considerable para quien envía PDFs por la web o los almacena en un bucket en la nube.

## Paso 5 – Ejemplo completo y ejecutable

A continuación tienes la clase Java completa que puedes copiar en tu IDE. Sustituye `YOUR_DIRECTORY` por la ruta real de la carpeta donde se encuentra `report.mhtml`.

```java
import com.aspose.html.converters.Converter;
import com.aspose.html.converters.PdfConversionOptions;
import com.aspose.html.converters.ResourceEmbeddingMode;

import java.io.File;

public class MhtmlToPdf {
    public static void main(String[] args) throws Exception {

        // ---------- Step 1: Define source and destination ----------
        String sourcePath = "YOUR_DIRECTORY/report.mhtml";
        String targetPath = "YOUR_DIRECTORY/report.pdf";

        // ---------- Step 2: Set conversion options (embed only images) ----------
        PdfConversionOptions conversionOptions = new PdfConversionOptions();
        conversionOptions.setResourceEmbeddingMode(ResourceEmbeddingMode.EMBED_IMAGES_ONLY);

        // ---------- Step 3: Run the conversion ----------
        Converter.convert(sourcePath, targetPath, conversionOptions);
        System.out.println("Conversion complete! PDF saved to: " + targetPath);

        // ---------- Step 4: (Optional) Show size reduction ----------
        File outputPdf = new File(targetPath);
        System.out.println("Resulting PDF size: " + outputPdf.length() / 1024 + " KB");
    }
}
```

**Salida esperada** (en la consola):

```
Conversion complete! PDF saved to: YOUR_DIRECTORY/report.pdf
Resulting PDF size: 842 KB
```

Abre `report.pdf` en cualquier visor; deberías ver todas las imágenes originales renderizadas correctamente. Si notas que faltan imágenes, verifica que las URLs de las imágenes en el MHTML sean absolutas o que los archivos sean accesibles desde la máquina de conversión.

## Preguntas comunes y manejo de casos límite

### ¿Qué pasa si *sí* necesito incrustar fuentes?

Cambia `ResourceEmbeddingMode` a `EMBED_ALL` o `EMBED_FONTS_ONLY`. El enum ofrece cuatro opciones:

| Modo                     | Qué se incrusta |
|--------------------------|-----------------|
| `EMBED_ALL`              | Imágenes, fuentes, CSS |
| `EMBED_IMAGES_ONLY`      | Solo imágenes (nuestro valor predeterminado) |
| `EMBED_FONTS_ONLY`       | Solo fuentes |
| `EMBED_NONE`             | Nada (solo referencias externas) |

### Mi MHTML contiene CSS externo que afecta el diseño—¿el PDF quedará roto?

Como no estamos incrustando CSS, el convertidor seguirá descargándolo durante la conversión. Si el CSS está alojado en una intranet a la que el servidor de conversión no puede acceder, el diseño podría volver a los valores predeterminados. En esos casos, incrusta el CSS (`EMBED_ALL`) o copia la hoja de estilos localmente y ajusta el MHTML para que apunte al archivo local.

### ¿Puedo procesar por lotes una carpeta de archivos MHTML?

Absolutamente. Envuelve la lógica de conversión en un bucle que itere sobre `File.listFiles()` y cambia el nombre de archivo de destino en consecuencia. Solo recuerda reutilizar una única instancia de `PdfConversionOptions` para mejorar el rendimiento.

### ¿Qué pasa con el consumo de memoria para documentos muy grandes?

Aspose.HTML transmite el contenido, por lo que el uso de memoria se mantiene moderado. Sin embargo, imágenes muy grandes pueden seguir provocando picos. Si encuentras un `OutOfMemoryError`, considera reducir la resolución de las imágenes antes de incrustarlas—Aspose ofrece `ImageConversionOptions` para eso, pero ese es tema de otro tutorial.

---

## Conclusión

Ahora sabes **cómo incrustar imágenes** al convertir MHTML a PDF con Aspose.HTML, y has visto por qué esta pequeña configuración puede **reducir drásticamente el tamaño del PDF**. El ejemplo Java completo y listo para copiar‑pegar muestra todo el flujo—from adding the Maven dependency to printing the final file size.

A partir de aquí podrías:

- Experimentar con `EMBED_FONTS_ONLY` si tus PDFs necesitan ser completamente autosuficientes.  
- Automatizar conversiones por lotes para una carpeta completa de informes.  
- Combinar esta técnica con las APIs de optimización de PDF de Aspose para obtener archivos aún más pequeños.

Ya sea que estés construyendo un servicio de generación de informes, una canalización de email‑a‑PDF, o simplemente organizando páginas web archivadas, controlar qué se incrusta es una palanca clave para el rendimiento y el costo. Pruébalo, ajusta las opciones y deja que tus PDFs permanezcan lo más esbeltos posible.

*¡Feliz codificación!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}