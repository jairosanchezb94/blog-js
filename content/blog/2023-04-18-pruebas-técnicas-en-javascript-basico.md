---
layout: blog
title: Pruebas técnicas en JavaScript *Basico*
date: 2023-04-18T18:07:40.310Z
---
<!--StartFragment-->

Aquí te presento algunos ejemplos de pruebas técnicas para un junior en JavaScript, con ejemplos de código:

1. Prueba de lógica: Crear una función que tome un número entero y devuelva true si es par, de lo contrario, false.

<!--EndFragment-->

```javascript
function esPar(numero) {
  return numero % 2 === 0;
}

console.log(esPar(2)); // true
console.log(esPar(3)); // false
console.log(esPar(10)); // true

```

<!--StartFragment-->

2. Prueba de manipulación de DOM: Crear una página web con un botón que al hacer clic en él, se cambie el texto de un párrafo.

HTML:

<!--EndFragment-->

```html
<button id="cambiar-texto">Cambiar Texto</button>
<p id="texto-a-cambiar">Texto a cambiar</p>

```

<!--StartFragment-->

JavaScript:

<!--EndFragment-->

```javascript
const botonCambiarTexto = document.getElementById('cambiar-texto');
const textoACambiar = document.getElementById('texto-a-cambiar');

botonCambiarTexto.addEventListener('click', function() {
  textoACambiar.textContent = 'Nuevo texto';
});

```

<!--StartFragment-->

3. Prueba de manejo de eventos: Crear una página web que tenga un botón y un cuadro de texto. Al hacer clic en el botón, se debe agregar el texto del cuadro de texto a una lista debajo.

HTML:

<!--EndFragment-->

```html
<input id="texto-a-agregar" type="text">
<button id="agregar-texto">Agregar Texto</button>
<ul id="lista-textos"></ul>

```

<!--StartFragment-->

JavaScript:

<!--EndFragment-->

```javascript
const botonAgregarTexto = document.getElementById('agregar-texto');
const inputTextoAAgregar = document.getElementById('texto-a-agregar');
const listaTextos = document.getElementById('lista-textos');

botonAgregarTexto.addEventListener('click', function() {
  const nuevoElementoLista = document.createElement('li');
  nuevoElementoLista.textContent = inputTextoAAgregar.value;
  listaTextos.appendChild(nuevoElementoLista);
  inputTextoAAgregar.value = '';
});

```

<!--StartFragment-->

4. Prueba de manejo de arrays: Crear una función que tome un array de números y devuelva el número más grande.

<!--EndFragment-->

```javascript
function numeroMasGrande(array) {
  let numeroMayor = array[0];
  for (let i = 1; i < array.length; i++) {
    if (array[i] > numeroMayor) {
      numeroMayor = array[i];
    }
  }
  return numeroMayor;
}

console.log(numeroMasGrande([1, 5, 10, 2, 7])); // 10

```

<!--StartFragment-->

5. Prueba de uso de AJAX: Crear una página web que haga una petición AJAX a una API de citas aleatorias y muestre la cita en la página.

HTML:

<!--EndFragment-->

```html
<p id="cita"></p>
<button id="nueva-cita">Nueva Cita</button>

```

<!--StartFragment-->

JavaScript:

<!--EndFragment-->

```javascript
const botonNuevaCita = document.getElementById('nueva-cita');
const citaMostrada = document.getElementById('cita');

botonNuevaCita.addEventListener('click', function() {
  const xhr = new XMLHttpRequest();
  xhr.open('GET', 'https://api.quotable.io/random');
  xhr.onload = function() {
    if (xhr.status === 200) {
      const respuesta = JSON.parse(xhr.responseText);
      citaMostrada.textContent = respuesta.content + ' - ' + respuesta.author;
    } else {
      console.log('Error al obtener cita');
    }
  };
  xhr.send();
});

```

<!--StartFragment-->

6. Prueba de uso de promesas: Crear una función que tome una cadena y devuelva una promesa que resuelve la cadena en mayúsculas después de 2 segundos.

<!--EndFragment-->

```javascript
function convertirMayusculas(texto) {
  return new Promise(function(resolve) {
    setTimeout(function() {
      resolve(texto.toUpperCase());
    }, 2000);
  });
}

convertirMayusculas('hola mundo')
  .then(function(resultado) {
    console.log(resultado); // HOLA MUNDO
  });

```

<!--StartFragment-->

Estos son solo algunos ejemplos de pruebas técnicas que un junior en JavaScript podría enfrentar. Dependiendo de la empresa, pueden variar en dificultad y complejidad.

<!--EndFragment-->