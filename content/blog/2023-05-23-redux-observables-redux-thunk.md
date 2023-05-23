---
layout: blog
title: Redux Observables & Redux Thunk
date: 2023-05-23T17:59:07.021Z
---
<!--StartFragment-->

Redux Observables es una biblioteca middleware utilizada en aplicaciones React Native (y también en aplicaciones React) para manejar acciones asíncronas y efectos secundarios complejos en combinación con Redux. Aquí tienes algunas cosas importantes y relevantes sobre Redux Observables en el contexto de React Native:

1. Middleware de Redux: Redux Observables es un middleware que se utiliza junto con Redux para extender su funcionalidad básica. Al igual que Redux Thunk, Redux Observables proporciona una forma de manejar acciones asíncronas, pero utiliza la biblioteca RxJS para gestionar los efectos secundarios y las operaciones asíncronas de manera más potente y escalable.
2. Programación reactiva con RxJS: Redux Observables se basa en la programación reactiva, que es un paradigma que utiliza Observables para representar flujos de eventos y manejar operaciones asíncronas y efectos secundarios de manera declarativa. RxJS es la biblioteca utilizada para implementar la programación reactiva en JavaScript, y Redux Observables aprovecha su poder y flexibilidad.
3. Epic: En Redux Observables, las acciones asíncronas se manejan mediante "epics". Un epic es una función que toma un flujo de acciones (llamado "action stream") y devuelve otro flujo de acciones (llamado "action stream"). Los epics se definen utilizando RxJS y permiten realizar transformaciones complejas y combinar múltiples flujos de eventos.
4. Ejemplo de implementación: Aquí tienes un ejemplo básico de cómo utilizar Redux Observables en una aplicación React Native:

<!--EndFragment-->

```javascript
import { createStore, applyMiddleware } from 'redux';
import { createEpicMiddleware, combineEpics } from 'redux-observable';
import { ajax } from 'rxjs/ajax';
import { map, mergeMap } from 'rxjs/operators';
import rootReducer from './reducers';

// Definición de epics
const fetchDataEpic = (action$, state$) =>
  action$.pipe(
    ofType('FETCH_DATA_REQUEST'),
    mergeMap(action =>
      ajax.getJSON('https://api.example.com/data').pipe(
        map(response => fetchDataSuccess(response)),
        catchError(error => of(fetchDataFailure(error.message)))
      )
    )
  );

const rootEpic = combineEpics(fetchDataEpic);

// Configuración del almacén de Redux
const epicMiddleware = createEpicMiddleware();
const store = createStore(rootReducer, applyMiddleware(epicMiddleware));

epicMiddleware.run(rootEpic);
```

<!--StartFragment-->

En este ejemplo, `createEpicMiddleware` crea el middleware de Redux Observables, mientras que `combineEpics` combina todos los epics en un epic raíz. Luego, se configura el almacén de Redux con el middleware y se ejecuta el epic raíz utilizando `epicMiddleware.run()`.

5. Beneficios de Redux Observables: Redux Observables permite manejar acciones asíncronas y efectos secundarios complejos de manera más eficiente y escalable. Al utilizar RxJS, puedes aprovechar el poder de la programación reactiva para componer y transformar flujos de eventos de manera declarativa. Esto facilita la gestión de lógicas complejas y asincrónicas en tu aplicación React Native, manteniendo un flujo de datos predecible y fácil de razonar.

Recuerda que este es solo un ejemplo básico para mostrar cómo usar Redux Observables en una aplicación React Native. Puedes adaptar y personalizar este código según tus necesidades específicas y explorar más características y operadores de RxJS para aprovechar al máximo Redux Observables en tu proyecto.

<!--EndFragment-->

<!--StartFragment-->

Redux Thunk es una biblioteca middleware popular utilizada en aplicaciones React Native (y también en aplicaciones React) para manejar acciones asíncronas en combinación con Redux. Aquí tienes algunas cosas importantes y relevantes sobre Redux Thunk en el contexto de React Native:

1. Middleware de Redux: Redux Thunk es un middleware que se utiliza junto con Redux para extender su funcionalidad básica. Redux es una biblioteca de administración del estado que se utiliza comúnmente en aplicaciones React Native para mantener un estado global predecible. El middleware actúa como una capa intermedia entre las acciones despachadas y los reducers de Redux.
2. Acciones asíncronas: Redux Thunk permite manejar acciones asíncronas en Redux. En una aplicación React Native, a menudo necesitas realizar llamadas a API, interactuar con bases de datos o realizar otras operaciones asíncronas. Con Redux Thunk, puedes despachar acciones asíncronas y controlar la lógica dentro de ellas.
3. Funciones Thunk: En Redux Thunk, las acciones no son solo objetos planos, sino funciones Thunk. Un Thunk es una función que envuelve una expresión para retrasar su evaluación. En el contexto de Redux Thunk, una función Thunk puede despachar acciones y acceder al estado actualizado a través de `getState()`. También puede realizar operaciones asíncronas antes de despachar una acción.
4. Ejemplo de implementación: Aquí tienes un ejemplo básico de cómo utilizar Redux Thunk en una aplicación React Native:

<!--EndFragment-->

```javascript
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const store = createStore(rootReducer, applyMiddleware(thunk));
```

<!--StartFragment-->

En este ejemplo, `createStore` crea el almacén de Redux y `applyMiddleware` agrega el middleware Redux Thunk al almacén.

5. Beneficios de Redux Thunk: Redux Thunk simplifica el manejo de acciones asíncronas en Redux al proporcionar un patrón de diseño claro. Te permite realizar operaciones asíncronas dentro de acciones, mantener tu lógica de negocios y llamadas a API separadas de los componentes de React Native y mantener un flujo de datos más predecible en toda tu aplicación.

Recuerda que esta es solo una introducción a Redux Thunk en el contexto de React Native. Puedes consultar la documentación oficial de Redux Thunk para obtener más detalles y ejemplos sobre su uso en aplicaciones React Native.

<!--EndFragment-->