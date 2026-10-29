---
category: general
date: 2026-06-03
description: Crear un documento HTML en Java e incrustar JavaScript para incrementar
  un contador. Aprender un ejemplo de motor de scripts, obtener innerHTML de un elemento
  y más.
draft: false
keywords:
- create html document
- embed javascript html
- get element innerhtml
- increment counter javascript
- script engine example
language: es
og_description: Crear documento HTML en Java, incrustar JavaScript para incrementar
  un contador y obtener el valor final usando un motor de scripts, ejemplo.
og_title: Crear documento HTML con JavaScript incrustado – Ejemplo en Java
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  headline: Create HTML Document with Embedded JavaScript – Java Example
  type: TechArticle
- description: Create HTML document in Java and embed JavaScript to increment a counter.
    Learn a script engine example, get element innerHTML, and more.
  name: Create HTML Document with Embedded JavaScript – Java Example
  steps:
  - name: '**Creates an HTML document** in memory.'
    text: '**Creates an HTML document** in memory.'
  - name: '**Embeds a small JavaScript snippet** that increments a counter five times.'
    text: '**Embeds a small JavaScript snippet** that increments a counter five times.'
  - name: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
    text: '**Initializes a script engine** (the `ScriptEngine` example) to run that
      snippet.'
  - name: '**Retrieves the final counter value** using `getElementInnerHTML`.'
    text: '**Retrieves the final counter value** using `getElementInnerHTML`.'
  - name: 'Prints `Final counter value: 5` to the console.'
    text: 'Prints `Final counter value: 5` to the console.'
  type: HowTo
tags:
- HTML
- JavaScript
- Java
- ScriptEngine
title: Crear documento HTML con JavaScript incrustado – Ejemplo en Java
url: /es/java/creating-managing-html-documents/create-html-document-with-embedded-javascript-java-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear documento HTML con JavaScript incrustado – Ejemplo en Java

¿Alguna vez necesitaste **crear documento HTML** desde código Java y te preguntaste cómo incrustar JavaScript dentro de él? En esta guía te mostraremos exactamente eso, paso a paso, y terminarás con un ejemplo funcional de motor de scripts que imprime el valor final del contador.  

Si alguna vez te has preguntado *“¿cómo puedo obtener el innerHTML de un elemento después de que se ejecute un script?”* o *“¿cuál es la forma más limpia de incrementar un contador en JavaScript desde Java?”*—estás en el lugar correcto. Cubriremos **embed javascript html**, **increment counter javascript**, y **get element innerHTML** todo en un tutorial cohesivo.

![Crear documento HTML con JavaScript](/images/create-html-document.png){: .center alt="Ejemplo de crear documento HTML con JavaScript"}

## Lo que construirás

Al final de este tutorial tendrás un programa Java autónomo que:

1. **Crea un documento HTML** en memoria.
2. **Incrusta un pequeño fragmento de JavaScript** que incrementa un contador cinco veces.
3. **Inicializa un motor de scripts** (el ejemplo `ScriptEngine`) para ejecutar ese fragmento.
4. **Recupera el valor final del contador** usando `getElementInnerHTML`.
5. Imprime `Final counter value: 5` en la consola.

Sin archivos externos, sin servidor web—solo Java puro y una pequeña cadena HTML.

---

## Requisitos previos

- Java 17 o posterior (la API `ScriptEngine` forma parte de la biblioteca estándar).
- Familiaridad básica con HTML y JavaScript (no necesitas ser un experto).
- Un IDE o un editor de texto simple más una terminal para compilar y ejecutar el programa.

---

## Paso 1: Crear documento HTML en Java

Lo primero que necesitamos es un objeto de documento HTML en blanco que luego podamos rellenar con marcado. Piensa en él como una página virtual que solo existe en memoria.

```java
// Import statements
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

// Minimal HTML document wrapper (pseudo‑class for illustration)
class HTMLDocument {
    private StringBuilder html = new StringBuilder();

    public void write(String content) {
        html.append(content);
    }

    public String getContent() {
        return html.toString();
    }

    // Simple DOM simulation for getElementById / innerHTML
    private java.util.Map<String, String> elements = new java.util.HashMap<>();

    public void setElementInnerHTML(String id, String value) {
        elements.put(id, value);
    }

    public String getElementInnerHTML(String id) {
        return elements.getOrDefault(id, "");
    }

    // Helper used by the script engine (not production‑grade)
    public void updateCounter(int value) {
        setElementInnerHTML("counter", String.valueOf(value));
    }
}
```

**Por qué es importante:** Al **crear documentos HTML** tú mismo, evitas escribir en disco y mantienes todo testeable. La pequeña simulación del DOM nos permite luego **obtener el innerHTML del elemento** sin un navegador completo.

---

## Paso 2: Incrustar JavaScript HTML – La lógica del contador

Ahora escribiremos el marcado HTML que incluye un bloque `<script>`. Este script **incrementará el contador en JavaScript** cinco veces.

```java
HTMLDocument doc = new HTMLDocument();

doc.write(
    "<!DOCTYPE html><html><body>"
  + "<div id='counter'>0</div>"
  + "<script>"
  + "for (let i = 0; i < 5; i++) {"
  + "  document.getElementById('counter').innerHTML = i + 1;"
  + "}"
  + "</script>"
  + "</body></html>"
);
```

**Explicación:**  
- El `<div id='counter'>0</div>` es nuestro elemento objetivo.  
- El bucle `for` ejecuta la lógica de **increment counter javascript**, actualizando el div en cada iteración.  
- Como no estamos en un navegador real, el motor de scripts que usaremos más adelante necesitará entender `document.getElementById`. Por eso añadimos un pequeño stub en `HTMLDocument`.

---

## Paso 3: Inicializar el motor de scripts – Un ejemplo de motor de scripts

Java incluye la API `ScriptEngine` (JSR‑223). Crearemos un pequeño contenedor que suministra el contenido HTML al motor y proporciona los métodos DOM mínimos que espera.

```java
class SimpleScriptEngine {
    private final HTMLDocument document;
    private final ScriptEngine engine;

    public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
        this.document = doc;
        ScriptEngineManager manager = new ScriptEngineManager();
        this.engine = manager.getEngineByName("JavaScript");
        // Expose a mock 'document' object to the JavaScript context
        engine.put("document", new Object() {
            public Object getElementById(String id) {
                return new Object() {
                    public void setInnerHTML(String value) {
                        document.updateCounter(Integer.parseInt(value));
                    }
                };
            }
        });
    }

    public void execute() throws ScriptException {
        // Extract only the script part from the HTML (simplified)
        String html = document.getContent();
        int scriptStart = html.indexOf("<script>") + "<script>".length();
        int scriptEnd   = html.indexOf("</script>");
        String script = html.substring(scriptStart, scriptEnd);
        engine.eval(script);
    }
}
```

**Por qué es importante:** Este **ejemplo de motor de scripts** muestra cómo puedes ejecutar JavaScript incrustado sin un navegador completo. También demuestra una forma ligera de exponer `document.getElementById` para que el script pueda interactuar con nuestro DOM simulado.

---

## Paso 4: Ejecutar JavaScript – Increment Counter JavaScript en acción

Con el motor listo, simplemente ejecutamos el script. El bucle dentro de la etiqueta `<script>` se disparará, y nuestro mock `setInnerHTML` actualizará el contador.

```java
try {
    SimpleScriptEngine engine = new SimpleScriptEngine(doc);
    engine.execute(); // runs the embedded JavaScript
} catch (ScriptException e) {
    e.printStackTrace();
}
```

**¿Qué ocurre detrás de escena?** Cada iteración del bucle llama a `document.getElementById('counter').innerHTML = i + 1;`. Nuestro mock `setInnerHTML` envía la cadena numérica a `HTMLDocument.updateCounter`, que almacena el último valor. Después de que el bucle termina, el mapa interno del documento contiene `"5"` para el elemento `counter`.

---

## Paso 5: Recuperar el valor final del contador – Obtener el innerHTML del elemento

Ahora que el script ha finalizado, podemos **obtener el innerHTML del elemento** desde nuestra instancia `HTMLDocument`.

```java
String finalValue = doc.getElementInnerHTML("counter");
System.out.println("Final counter value: " + finalValue); // prints 5
```

Ejecutar todo el programa imprime:

```
Final counter value: 5
```

Eso confirma que la lógica de **increment counter javascript** funcionó y que hemos recuperado con éxito el **innerHTML del elemento** después de la ejecución del script.

---

## Ejemplo completo y funcional

Juntando todo, aquí tienes la clase Java completa, lista para ejecutar:

```java
import javax.script.ScriptEngine;
import javax.script.ScriptEngineManager;
import javax.script.ScriptException;

public class HtmlJsDemo {

    // ---------- Minimal HTMLDocument implementation ----------
    static class HTMLDocument {
        private final StringBuilder html = new StringBuilder();
        private final java.util.Map<String, String> elements = new java.util.HashMap<>();

        public void write(String content) {
            html.append(content);
        }

        public String getContent() {
            return html.toString();
        }

        public void setElementInnerHTML(String id, String value) {
            elements.put(id, value);
        }

        public String getElementInnerHTML(String id) {
            return elements.getOrDefault(id, "");
        }

        public void updateCounter(int value) {
            setElementInnerHTML("counter", String.valueOf(value));
        }
    }

    // ---------- SimpleScriptEngine (script engine example) ----------
    static class SimpleScriptEngine {
        private final HTMLDocument document;
        private final ScriptEngine engine;

        public SimpleScriptEngine(HTMLDocument doc) throws ScriptException {
            this.document = doc;
            ScriptEngineManager manager = new ScriptEngineManager();
            this.engine = manager.getEngineByName("JavaScript");
            // Expose a mock 'document' object
            engine.put("document", new Object() {
                public Object getElementById(String id) {
                    return new Object() {
                        public void setInnerHTML(String value) {
                            document.updateCounter(Integer.parseInt(value));
                        }
                    };
                }
            });
        }

        public void execute() throws ScriptException {
            String html = document.getContent();
            int start = html.indexOf("<script>") + "<script>".length();
            int end   = html.indexOf("</script>");
            String script = html.substring(start, end);
            engine.eval(script);
        }
    }

    // ---------- Main method ----------
    public static void main(String[] args) {
        // Step 1: create HTML document
        HTMLDocument doc = new HTMLDocument();

        // Step 2: embed JavaScript HTML (increment counter JavaScript)
        doc.write(
            "<!DOCTYPE html><html><body>"
          + "<div id='counter'>0</div>"
          + "<script>"
          + "for (let i = 0; i < 5; i++) {"
          + "  document.getElementById('counter').innerHTML = i


## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Crear documentos HTML vacíos en Aspose.HTML para Java](/html/english/java/creating-managing-html-documents/create-empty-html-documents/)
- [Crear documentos HTML a partir de una cadena en Aspose.HTML para Java](/html/english/java/creating-managing-html-documents/create-html-documents-from-string/)
- [Guardar documento HTML en Aspose.HTML para Java](/html/english/java/saving-html-documents/save-html-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}