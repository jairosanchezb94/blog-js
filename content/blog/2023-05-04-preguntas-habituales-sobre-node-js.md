---
layout: blog
title: Preguntas habituales sobre Node.js
date: 2023-05-04T09:39:07.212Z
---
<!--StartFragment-->

¿Qué son los "stubs"?

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