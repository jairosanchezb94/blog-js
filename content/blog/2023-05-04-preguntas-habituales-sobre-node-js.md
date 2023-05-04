---
layout: blog
title: Preguntas habituales sobre Node.js
date: 2023-05-04T09:39:07.212Z
---
<!--StartFragment-->

## ¿Qué son los "stubs"?

<!--EndFragment-->

<!--StartFragment-->

Los "stubs" son funciones o objetos que se utilizan para reemplazar temporalmente un módulo o función en una aplicación durante las pruebas unitarias o de integración en Node.js.

A continuación, se muestra un ejemplo sencillo de cómo utilizar un "stub" en una prueba unitaria utilizando la biblioteca Mocha y Sinon.js:

Supongamos que tenemos una función llamada "getUser" que hace una solicitud a una API REST para obtener los datos de un usuario. En lugar de hacer una solicitud real a la API en nuestras pruebas, podemos crear un "stub" de la función que devuelva datos simulados.

<!--EndFragment-->

```javascript
// Importamos las bibliotecas necesarias
const sinon = require('sinon');
const assert = require('assert');
const getUser = require('./getUser');

// Creamos una prueba utilizando Mocha
describe('getUser', () => {
  it('should return user data', async () => {
    // Creamos un stub de la función getUser
    const getUserStub = sinon.stub(getUser, 'getUser').returns({ name: 'John Doe', age: 30 });

    // Llamamos a la función getUser
    const userData = await getUser.getUser();

    // Verificamos que la función getUser se haya llamado
    assert(getUserStub.calledOnce);

    // Verificamos que los datos devueltos sean correctos
    assert.deepStrictEqual(userData, { name: 'John Doe', age: 30 });

    // Restauramos la función getUser original
    getUserStub.restore();
  });
});
```

<!--StartFragment-->

En este ejemplo, creamos un "stub" de la función getUser utilizando Sinon.js. Este "stub" reemplaza temporalmente la función getUser original y devuelve un objeto con datos simulados en lugar de hacer una solicitud real a la API. En la prueba, llamamos a la función getUser y verificamos que el "stub" se haya llamado y que los datos devueltos sean los correctos. Finalmente, restauramos la función getUser original para que no afecte a otras pruebas o al código de la aplicación.

<!--EndFragment-->

<!--StartFragment-->

## ¿Qué son los "callback hell"?

<!--EndFragment-->

<!--StartFragment-->

Los "callback hell" son un patrón común en el código de Node.js que se produce cuando se anidan múltiples llamadas de devolución de llamada (callbacks) dentro de otras. Esto puede hacer que el código sea difícil de leer, mantener y depurar.

A continuación se muestra un ejemplo sencillo de cómo se puede producir un "callback hell" en Node.js:

<!--EndFragment-->

```javascript
function getUser(userId, callback) {
  db.getUser(userId, (err, user) => {
    if (err) {
      callback(err);
    } else {
      db.getPosts(user.id, (err, posts) => {
        if (err) {
          callback(err);
        } else {
          db.getComments(posts[0].id, (err, comments) => {
            if (err) {
              callback(err);
            } else {
              callback(null, { user, posts, comments });
            }
          });
        }
      });
    }
  });
}
```

<!--StartFragment-->

En este ejemplo, la función "getUser" recibe un ID de usuario y una función de devolución de llamada. Dentro de esta función, se realizan tres llamadas a la base de datos utilizando devoluciones de llamada anidadas, lo que resulta en un "callback hell". Cada llamada de devolución de llamada verifica si hay un error y, de ser así, llama a la función de devolución de llamada con el error. Si no hay un error, se realiza la siguiente llamada de devolución de llamada.

Para evitar el "callback hell", se puede utilizar la técnica de "promisificación", que convierte las devoluciones de llamada en promesas que se pueden encadenar en lugar de anidar. El siguiente es un ejemplo de cómo se vería la misma función "getUser" con promesas:

<!--EndFragment-->

```javascript
function getUser(userId) {
  return db.getUser(userId)
    .then((user) => db.getPosts(user.id))
    .then((posts) => db.getComments(posts[0].id))
    .then((comments) => ({ user, posts, comments }));
}
```

<!--StartFragment-->

En este ejemplo, la función "getUser" devuelve una promesa en lugar de aceptar una función de devolución de llamada. Cada llamada a la base de datos devuelve una promesa que se encadena con la siguiente llamada utilizando el método "then". Esto hace que el código sea más legible, fácil de mantener y menos propenso a errores.

<!--EndFragment-->

1. ¿Qué es un "evento"? Un evento en Node.js es una acción que ocurre en el entorno de Node, como un clic de ratón o un cambio de estado en un servidor. Los eventos se pueden escuchar y se pueden asociar con una función de devolución de llamada para que se ejecute cuando ocurre el evento.
2. ¿Qué es la programación "Impulsada por eventos"? La programación impulsada por eventos (Event-driven programming) es un estilo de programación en el que el flujo de control del programa está determinado por los eventos que ocurren en el entorno. En Node.js, se utiliza el modelo de programación impulsada por eventos para manejar las operaciones de entrada/salida (I/O) no bloqueantes.
3. ¿Cuál es la diferencia entre Módulo/Dependencia/Paquete? En Node.js, un módulo es un archivo JavaScript que contiene código que se puede reutilizar en una aplicación. Una dependencia es un módulo que una aplicación utiliza y que se ha instalado a través de un administrador de paquetes como npm. Un paquete es un conjunto de módulos que se pueden instalar y utilizar juntos, como una biblioteca.
4. ¿Qué es el Global Object u Objeto Global de Node? El objeto global de Node.js es un objeto especial que contiene variables y funciones globales que están disponibles en todo el entorno de Node.js. Algunas de las variables y funciones globales incluyen "process", "console", "setTimeout" y "setInterval".
5. ¿Por qué importamos/exportamos módulos con require/module.exports y no con import de ES6? En Node.js, se utiliza el método de "require" y "module.exports" para importar y exportar módulos porque Node.js utiliza CommonJS, un sistema de módulos diferente al de ES6. Sin embargo, con la introducción de la versión 14 de Node.js, también se puede utilizar el sistema de módulos ES6 utilizando "import" y "export".

A continuación, se muestro un ejemplo sencillo de cómo se utilizan estos conceptos en Node.js

<!--EndFragment-->

```javascript
// Ejemplo de evento
const events = require('events');
const eventEmitter = new events.EventEmitter();

// Escuchar un evento
eventEmitter.on('saludo', () => {
  console.log('Hola mundo!');
});

// Emitir un evento
eventEmitter.emit('saludo');

// Ejemplo de módulo
// módulo.js
module.exports = {
  saludo: () => {
    console.log('Hola mundo!');
  }
}

// app.js
const modulo = require('./modulo');
modulo.saludo();

// Ejemplo de objeto global
console.log(__dirname);
console.log(__filename);

// Ejemplo de dependencia/paquete
// Instalar el paquete "express" mediante npm
const express = require('express');
const app = express();
```

<!--StartFragment-->

En este ejemplo, he utilizado el "events.EventEmitter" para crear un objeto de eventos que escucha y emite eventos. También se muestra cómo se utiliza el método "module.exports" para exportar una función de un módulo y cómo se utiliza el método "require" para importarla en otra parte de la aplicación. Además, se muestra cómo se pueden utilizar las variables globales "\_\_dirname" y "\_\_filename" para obtener información sobre la ruta actual del archivo y el nombre del archivo actual. Finalmente, se muestra cómo se utiliza una dependencia/paquete instalado a través de npm, en este caso, "express".

<!--EndFragment-->

<!--StartFragment-->

6. ¿Qué es el middleware en Node.js? El middleware en Node.js es una función que procesa una solicitud HTTP antes de que se la pase a la función de devolución de llamada final. El middleware se utiliza comúnmente para agregar funcionalidades adicionales a una aplicación, como la autenticación y la validación de datos. En Express, un framework popular de Node.js, el middleware se utiliza para manejar las solicitudes HTTP.
7. ¿Qué son las promesas en Node.js? Las promesas en Node.js son objetos que representan un valor que puede estar disponible en algún momento en el futuro, o que puede fallar. Las promesas se utilizan comúnmente para manejar operaciones asincrónicas en Node.js, y se pueden encadenar juntas para crear flujos de control más legibles. En lugar de utilizar el callback hell, las promesas pueden simplificar y hacer más legible el código asíncrono.
8. ¿Qué es el patrón de diseño de middleware "chain of responsibility" en Node.js? El patrón de diseño "chain of responsibility" es un patrón de diseño de middleware que se utiliza en Node.js. El patrón consiste en una serie de objetos que se encadenan juntos y que manejan una solicitud de manera incremental. Cada objeto en la cadena tiene la oportunidad de manejar la solicitud antes de pasarla al siguiente objeto en la cadena. Este patrón se utiliza comúnmente en frameworks web como Express.

A continuación, se muestro un ejemplo sencillo de cómo se utilizan estos conceptos en Node.js

<!--EndFragment-->

```javascript
// Ejemplo de middleware
const express = require('express');
const app = express();

// Middleware para manejar las solicitudes HTTP
app.use((req, res, next) => {
  console.log('Solicitud recibida.');
  next();
});

// Ruta para manejar una solicitud GET
app.get('/', (req, res) => {
  res.send('¡Hola mundo!');
});

// Ejemplo de promesas
const fs = require('fs');

// Promesa para leer un archivo
const readFilePromise = (filePath) => {
  return new Promise((resolve, reject) => {
    fs.readFile(filePath, 'utf-8', (err, data) => {
      if (err) {
        reject(err);
      } else {
        resolve(data);
      }
    });
  });
};

// Uso de la promesa
readFilePromise('./archivo.txt')
  .then((data) => {
    console.log(data);
  })
  .catch((err) => {
    console.log(err);
  });

// Ejemplo de patrón de diseño "chain of responsibility"
const app = express();

// Middleware 1
app.use((req, res, next) => {
  console.log('Middleware 1');
  next();
});

// Middleware 2
app.use((req, res, next) => {
  console.log('Middleware 2');
  next();
});

// Middleware 3
app.use((req, res, next) => {
  console.log('Middleware 3');
  res.send('Fin de la cadena de responsabilidad');
});
```

<!--StartFragment-->

En este ejemplo, se muestra cómo he utilizado el middleware en Express para manejar solicitudes HTTP. Además, se muestra cómo se utilizan las promesas para manejar operaciones asincrónicas, en este caso, leer un archivo. Por último, se muestra cómo se utiliza el patrón de diseño de middleware "chain of responsibility" en Express, para manejar las solicitudes HTTP en una serie de pasos.

<!--EndFragment-->