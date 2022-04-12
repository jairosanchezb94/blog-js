---
layout: blog
title: Cómo Insertar JavaScript en HTML
date: 2022-04-12T16:48:27.034Z
thumbnail: /assets/images/html-javascript.jpg
---
## Ventajas de JavaScript

JavaScript primero fue conocido como LiveScript. Pero como[ Java](https://www.hostinger.es/tutoriales/como-instalar-java-en-ubuntu/) era un lenguaje muy popular, [Netscape](https://es.wikipedia.org/wiki/Netscape_Navigator) decidió cambiarle el nombre a JavaScript. Su primera aparición se remonta a 1995 dentro de Netscape 2.0. Estas son algunas de las principales ventajas de usar JavaScript:

### Interacción mínima con el servidor

Es un hecho bien conocido que si quieres optimizar el rendimiento de un sitio web, la mejor manera es reducir la comunicación con el servidor. JavaScript ayuda en este sentido al validar la información que ingresa el usuario en el lado del cliente. Solo envía solicitudes al servidor después de ejecutar las comprobaciones de validación iniciales. Como resultado, el uso de recursos y la cantidad de solicitudes al servidor se reduce significativamente.

### Interfaces más completas y fáciles de usar

Al usar JavaScript, puedes crear interfaces interactivas del lado del cliente. Por ejemplo, agregar controles deslizantes, presentaciones de diapositivas, efectos al poner el cursor sobre objetos, funciones de arrastrar y soltar, etc.

### Retroalimentación inmediata para el usuario

Al usar JavaScript, puedes asegurarte de que los usuarios obtengan una respuesta inmediata. Por ejemplo, imaginemos que un usuario ha rellenado un formulario y ha dejado un campo vacío. Sin la validación de JavaScript, tendrán que esperar a que la página se vuelva a cargar solo para darse cuenta de que dejaron un campo vacío. Sin embargo, con JavaScript, serán alertados al instante.

### Fácil depuración

JavaScript es un lenguaje interpretado, lo que significa que el código escrito se descifra línea por línea. En caso de que aparezcan errores, obtendrás el número de línea exacto donde se encuentra el problema.

## Insertar JavaScript en HTML

Hay dos formas de incluir JavaScript en HTML y hacer que funcionen juntos. Ahora que hemos hablado sobre JavaScript y hemos visto cuáles pueden ser algunas de sus ventajas, echemos un vistazo a algunas de las formas en que podemos conectar JavaScript con HTML.

### Agregar JavaScript directamente a un archivo HTML

La primera forma de insertar JavaScript en HTML es directa. Puedes hacerlo utilizando la etiqueta **<script> </script>** que debe envolver todo el código JS que escribas. Se puede agregar el código JS:

* entre las etiquetas **<head>**
* entre las etiquetas **<body>**

Dependiendo de dónde agregues el código JavaScript en tu archivo HTML, la carga será diferente. Por lo general se recomienda agregarlo en la sección **<head>** para que permanezca separado del contenido de tu archivo HTML. Pero colocarlo dentro de **<body>** puede ayudar a mejorar la velocidad de carga, ya que el contenido del sitio web se cargará más rápido, y solo después de eso se procesará el JavaScript. Para este ejemplo, echemos un vistazo al siguiente archivo HTML que debe mostrar la hora actual:

```html
<!DOCTYPE html>
<html lang="en-US">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<script>JAVASCRIPT IS USUALLY PLACED HERE</script>
<title>Time right now is: </title>
</head>
<body>
<script>JAVASCRIPT CAN ALSO GO HERE</script>
</body>
</html>
```

En este momento, el código anterior no contiene JavaScript y, por lo tanto, no puede mostrar la hora. Podemos agregar el siguiente código para asegurarnos de que muestre la hora correcta:

```javascript
var time = new Date();
console.log(time.getHours() + ":" + time.getMinutes() + ":" + time.getSeconds());
```