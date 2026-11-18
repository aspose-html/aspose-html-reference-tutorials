---
category: general
date: 2026-04-23
description: Aplica estilos de fuente de forma programática y aprende a eliminar el
  subrayado del texto, cambiar el estilo del texto y establecer texto en negrita de
  forma programática en un tutorial conciso.
draft: false
keywords:
- apply font style
- remove underline from text
- change text style
- text formatting tutorial
- set bold text programmatically
language: es
og_description: Aplica estilos de fuente programáticamente y descubre cómo eliminar
  el subrayado del texto, cambiar el estilo del texto y establecer texto en negrita
  de forma programática en un tutorial corto y práctico.
og_title: Aplicar estilo de fuente programáticamente – Guía rápida de C#
tags:
- csharp
- ui
- text-formatting
- programming
title: Aplicar estilo de fuente programáticamente – Guía rápida de C#
url: /es/net/html-document-manipulation/apply-font-style-programmatically-quick-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar estilo de fuente programáticamente – Guía rápida de C# 

¿Alguna vez necesitaste **aplicar estilo de fuente** a un elemento de UI pero no sabías por dónde empezar? No eres el único—la mayoría de los desarrolladores se topan con ese obstáculo cuando se inician en el formato dinámico de texto. ¿La buena noticia? En solo unos minutos sabrás exactamente cómo cambiar la apariencia de una etiqueta, eliminar el subrayado del texto y establecer texto en negrita programáticamente sin buscar en interminables documentos.

En este **tutorial de formato de texto** recorreremos un ejemplo completo y ejecutable, explicaremos el “por qué” detrás de cada línea y añadiremos consejos prácticos que puedes copiar‑pegar en cualquier proyecto WinForms o WPF. Sin rodeos, solo lo necesario para hacer el trabajo.

---

## Lo que aprenderás

- Cómo **aplicar estilo de fuente** usando una pequeña clase auxiliar.  
- Los pasos precisos para **eliminar el subrayado del texto** manteniendo los demás estilos intactos.  
- Formas de **cambiar el estilo de texto** (negrita, cursiva, subrayado) sobre la marcha.  
- Un fragmento completo, listo para copiar, que **establece texto en negrita programáticamente**.  
- Trampas comunes y manejo de casos límite para que no te sorprendan más adelante.  

**Requisitos previos:** .NET 6+ (o cualquier .NET Framework reciente), conocimientos básicos de C# y un IDE de tu elección (Visual Studio, Rider o VS Code). Eso es todo—no se requieren paquetes NuGet adicionales.

---

## Paso 1 – Aplicar estilo de fuente a tu control

El núcleo de cualquier operación de **aplicar estilo de fuente** es un enum `FontStyle` combinado con un objeto `Font`. Para mantener el código ordenado envolveremos la lógica del enum dentro de una pequeña clase `WebFontStyle`. Esta clase refleja las propiedades que viste en el fragmento original (`Bold`, `Italic`, `Underline`) y construye un valor `FontStyle` que puedes pasar a `Font`.

```csharp
using System;
using System.Drawing;

/// <summary>
/// Simple helper that mimics the original WebFontStyle API.
/// It lets you toggle Bold, Italic, and Underline flags and
/// converts the result into a System.Drawing.FontStyle value.
/// </summary>
public class WebFontStyle
{
    public bool Bold { get; set; } = false;
    public bool Italic { get; set; } = false;
    public bool Underline { get; set; } = false;

    /// <summary>
    /// Returns a FontStyle that combines the selected flags.
    /// </summary>
    public FontStyle ToFontStyle()
    {
        FontStyle style = FontStyle.Regular;
        if (Bold)      style |= FontStyle.Bold;
        if (Italic)    style |= FontStyle.Italic;
        if (Underline) style |= FontStyle.Underline;
        return style;
    }

    /// <summary>
    /// Creates a new Font based on an existing one but with the
    /// updated style. Handy for UI controls that already have a font.
    /// </summary>
    public Font ToFont(Font baseFont)
    {
        return new Font(baseFont, ToFontStyle());
    }
}
```

**Por qué es importante:**  
Al aislar la lógica de construcción de banderas, evitas esparcir operaciones bit a bit `|` por todo tu código de UI. Es más fácil de leer, más fácil de probar y—lo más importante—deja la intención de **aplicar estilo de fuente** perfectamente clara.

---

## Paso 2 – Eliminar subrayado del texto (y mantener los demás estilos intactos)

Supongamos que heredaste una etiqueta que ya está subrayada, pero el diseño requiere texto en negrita simple. No quieres perder la negrita al eliminar el subrayado. Aquí es donde la clase `WebFontStyle` brilla.

```csharp
// Assume we already have a Label named lblSample.
var fontStyle = new WebFontStyle
{
    Bold = true,          // Keep bold on.
    Italic = false,      // No italic needed.
    Underline = false    // This line **removes underline**.
};

// Apply the new Font to the label.
lblSample.Font = fontStyle.ToFont(lblSample.Font);
```

**Punto clave:** Establecer `Underline = false` indica explícitamente al ayudante que *excluya* la bandera de subrayado. Si omites esa línea por completo, el subrayado anterior persistirá, lo cual es una fuente común de errores cuando los desarrolladores solo alternan la propiedad `Bold`.

---

## Paso 3 – Cambiar estilo de texto: negrita, cursiva y más

Podrías preguntarte, “¿Y si también necesito alternar la cursiva?” El mismo objeto funciona para cualquier combinación. A continuación tienes una matriz rápida que puedes consultar mientras codificas.

| Estilo deseado | `Bold` | `Italic` | `Underline` |
|---------------|--------|----------|-------------|
| **Solo negrita** | true   | false    | false       |
| *Solo cursiva* | false  | true     | false       |
| **Negrita + Cursiva** | true   | true     | false       |
| **Negrita + Subrayado** | true   | false    | true        |

Simplemente establece las propiedades que necesites y llama a `ToFont`. El ayudante hace el trabajo pesado por ti, para que puedas centrarte en la lógica de la UI.

---

## Ejemplo completo – Establecer texto en negrita programáticamente

A continuación tienes un ejemplo **completo y ejecutable de WinForms** que demuestra todo lo que hemos cubierto. Pégalo en un nuevo proyecto WinForms estilo consola y pulsa **F5**.

```csharp
using System;
using System.Drawing;
using System.Windows.Forms;

namespace FontStyleDemo
{
    static class Program
    {
        [STAThread]
        static void Main()
        {
            ApplicationConfiguration.Initialize(); // .NET 6+ boilerplate
            Application.Run(new DemoForm());
        }
    }

    public class DemoForm : Form
    {
        private readonly Label _sampleLabel;

        public DemoForm()
        {
            Text = "Apply Font Style Demo";
            Size = new Size(400, 200);
            StartPosition = FormStartPosition.CenterScreen;

            _sampleLabel = new Label
            {
                Text = "Hello, world!",
                AutoSize = true,
                Location = new Point(20, 30)
            };
            Controls.Add(_sampleLabel);

            // STEP: instantiate WebFontStyle and configure it
            var fontStyle = new WebFontStyle
            {
                Bold = true,          // set bold text programmatically
                Italic = false,      // no italic
                Underline = false    // remove underline from text
            };

            // Apply the new style to the label
            _sampleLabel.Font = fontStyle.ToFont(_sampleLabel.Font);
        }
    }

    // ---- WebFontStyle class from Step 1 (included for completeness) ----
    public class WebFontStyle
    {
        public bool Bold { get; set; } = false;
        public bool Italic { get; set; } = false;
        public bool Underline { get; set; } = false;

        public FontStyle ToFontStyle()
        {
            FontStyle style = FontStyle.Regular;
            if (Bold)      style |= FontStyle.Bold;
            if (Italic)    style |= FontStyle.Italic;
            if (Underline) style |= FontStyle.Underline;
            return style;
        }

        public Font ToFont(Font baseFont)
        {
            return new Font(baseFont, ToFontStyle());
        }
    }
}
```

### Resultado esperado

Al ejecutar el programa, aparece una ventana con el texto **“Hello, world!”** renderizado en **negrita**, **no cursiva**, y **sin subrayado**. Esa confirmación visual te indica que la lógica de **aplicar estilo de fuente** funcionó perfectamente.

---

## Consejos profesionales y casos límite

- **Actualizaciones dinámicas:** Si necesitas cambiar el estilo después de que el formulario se muestre (p. ej., en respuesta a una casilla de verificación), simplemente recrea la instancia `WebFontStyle` o modifica sus propiedades y vuelve a asignar `lbl.Font`. La UI se actualiza al instante.  
- **Consideraciones de alta DPI:** Cuando reemplazas un objeto `Font`, Windows lo escala automáticamente según la DPI actual. No se necesita código adicional a menos que manejes el escalado manualmente.  
- **Equivalente en WPF:** En WPF enlazarías `FontWeight`, `FontStyle` y `TextDecorations` en lugar de intercambiar un objeto `Font`. La misma separación lógica se aplica—mantén la lógica de estilo fuera de la capa de vista.  
- **Evitar fugas de memoria:** Reasignar `Label.Font` crea un nuevo objeto `Font`. Desecha el anterior si cambias estilos con frecuencia: `var oldFont = lbl.Font; lbl.Font = newFont; oldFont.Dispose();`

---

## Conclusión

Ahora sabes cómo **aplicar estilo de fuente** a cualquier control .NET, **eliminar el subrayado del texto** y **cambiar el estilo de texto** sobre la marcha—todo mientras mantienes tu código limpio y reutilizable. El pequeño ayudante `WebFontStyle` convierte un puñado de banderas booleanas en un componente sólido y testeable, y el ejemplo completo demuestra que puedes **establecer texto en negrita programáticamente** en solo unas pocas líneas.

¿Qué sigue? Prueba combinar este enfoque con configuraciones dirigidas por el usuario, o experimenta con otras banderas `FontStyle` como `Strikeout`. Incluso podrías exponer un pequeño panel de UI que permita a usuarios no técnicos elegir negrita, cursiva o subrayado en tiempo de ejecución—sin necesidad de recompilar.

Si encontraste útil este **tutorial de formato de texto**, no dudes en dejar un comentario o compartir tus propias variantes. ¡Feliz codificación, y que tu UI siempre se vea exactamente como la imaginaste! 

---

![Screenshot showing how to apply font style to a label in C#](https://example.com/images/apply-font-style.png

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}