---
layout: blog
title: Preguntas Técnicas Frontend Developer
date: 2023-04-19T09:24:13.182Z
---
<!--StartFragment-->

En este blog v﻿oy a dejar unas cuantas claves técnicas para esas posibles preguntas técnicas aunque no se puede abarcar todo, es importante tener alguna en mente.

<!--EndFragment-->

# **A﻿ngular**

## C﻿iclo de vida en Angular.

<!--StartFragment-->

Ciclo de vida de Agular: son componentes que se encuentran en el ciclo de vida de angular se divide en 8 etapas las cuales son:

1. **\*ngOnChanges**: este evento se ejecuta cada ver que cambia el valor del input control, siempre recibe el data map.

E﻿jemplo:

```typescript
import { Component, Input, OnChanges, SimpleChanges } from '@angular/core';

@Component({
  selector: 'app-my-component',
  templateUrl: './my-component.component.html',
  styleUrls: ['./my-component.component.css']
})
export class MyComponentComponent implements OnChanges {

  @Input() public data: any;

  ngOnChanges(changes: SimpleChanges): void {
    if (changes.data) {
      // Lógica para actualizar otras propiedades en respuesta a los cambios en "data"
    }
  }
}
```

2. **\*ngOnInit**: se ejecuta cuando se ha desplegado los data-bound-propertis o cuando se ha inicializado del ngOnChanges. Lo uso para inicializar datos en el componente.

E﻿jemplo:

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-my-component',
  templateUrl: './my-component.component.html',
  styleUrls: ['./my-component.component.css']
})
export class MyComponentComponent implements OnInit {

  public data: any;

  ngOnInit(): void {
    this.getDataFromServer();
  }

  getDataFromServer() {
    // Lógica para hacer una petición HTTP y asignar los datos a la propiedad "data"
  }
}
```

3. **ngDoCheck**: aquí puedes poner la logica o cambios para cualquier componente.
4. **ngAfterContentInit**: se ejecuta justo despues de ngDoCheck y esta vinculado a los componentes hijos.
5. **ngAfterContentChecked**: este evento llama al ngAfterContentInit y se invoca posteriormente de ngDoCheck.
6. **\*ngAfterViewInit**: este evento se ejecuta en la vista del componente y llama despues al ngAfterContentChecked.

E﻿jemplo: 

```typescript
import { Component, AfterViewInit, ViewChild } from '@angular/core';

@Component({
  selector: 'app-my-component',
  templateUrl: './my-component.component.html',
  styleUrls: ['./my-component.component.css']
})
export class MyComponentComponent implements AfterViewInit {

  @ViewChild('myElement') public myElement: ElementRef;

  ngAfterViewInit(): void {
    // Lógica para inicializar plugins o configurar eventos en el elemento referenciado por "myElement"
  }
}
```

7. **ngAfterViewChecked**: aquí se puede ver cuando el componente espera algun valor que proviene de sus componentes secundarios.
8. **ngOnDestroy**: este evento se ejecuta para destruir los componentes, tienes que darte de baja de los componentes event handlers para evitar memory leaks o fugas de memoria.

<!--EndFragment-->

## Las interfaces son un mecanismo para definir tipo de clases, para definir los atributos y métodos de una «cosa», sin importar qué sea esa cosa.

<!--StartFragment-->

Para detectar cambios Angular tiene dos estrategias:

1. **default**: empieza a recorrer el árbol de componentes desde el principio para comprobar si tiene que actualizar algo.
2. **OnPush**: Los componentes que utilizan esta estrategia se saltan los ciclos de detección de cambios a menos que se trate de un cambio de estado interno del propio componente o de sus inputs.

<!--EndFragment-->

## Diferencias entre subject subject behaviour, input, output, viewchild, contentchild en Angular.

<!--StartFragment-->

En Angular, existen varios conceptos que se relacionan con la manipulación de elementos y componentes en la aplicación. A continuación, se explican las diferencias entre ellos:

1. **Subject**: Es un tipo de objeto que se utiliza para manejar eventos y notificaciones asíncronas en la aplicación. Los subjects permiten que un componente envíe y reciba datos en tiempo real.
2. **Behavior Subject**: Es similar a un subject, pero tiene la característica adicional de emitir el valor actual o la última emisión para cualquier nuevo suscriptor.
3. **Input**: Es una propiedad de un componente que recibe valores de otro componente o del módulo padre. Los inputs se utilizan para comunicar datos de un componente a otro.
4. **Output**: Es una propiedad de un componente que emite valores a otro componente o al módulo padre. Los outputs se utilizan para comunicar eventos de un componente a otro.
5. **ViewChild**: Es una directiva que permite acceder a un componente hijo desde el componente padre. La directiva ViewChild se utiliza para manipular el componente hijo y acceder a sus propiedades y métodos.
6. **ContentChild**: Es similar a ViewChild, pero se utiliza para acceder a un elemento o componente que se encuentra dentro del contenido proyectado en un componente.

En resumen, los subjects se utilizan para manejar eventos asíncronos, los inputs y outputs se utilizan para comunicar datos y eventos entre componentes, y las directivas ViewChild y ContentChild se utilizan para acceder a componentes y elementos hijos en la jerarquía de componentes de la aplicación.

<!--EndFragment-->

## ¿Cuando modulizar y como usar los preload strategies?

<!--StartFragment-->

Modularizar es una práctica común en la programación en la que se divide el código en diferentes módulos o archivos para facilitar su mantenimiento y reutilización. Se puede modularizar un proyecto por diferentes razones, como por ejemplo para separar la lógica de la interfaz de usuario, para dividir el código en diferentes funcionalidades o para mejorar la legibilidad del código.

En Angular, se puede modularizar una aplicación mediante la creación de módulos de Angular. Un módulo de Angular es un contenedor para diferentes componentes, servicios, directivas y otros artefactos de Angular. Al modularizar una aplicación, se puede mejorar su organización y estructura, lo que facilita su mantenimiento y reutilización.

En cuanto a los preload strategies, se refieren a la estrategia de precarga de módulos de Angular. Angular ofrece diferentes estrategias de precarga de módulos para mejorar la velocidad de la aplicación y la experiencia del usuario. Las estrategias de precarga incluyen:

* **NoPreloading**: No se precargan módulos de forma automática. Solo se cargan los módulos que se necesitan en el momento.
* **PreloadAllModules**: Se precargan todos los módulos de forma automática después de que se haya cargado el módulo principal.
* **PreloadSomeModules**: Se precargan solo algunos módulos de forma automática, según una lista de módulos definida por el desarrollador.
* **Custom preload strategies**: Se pueden crear estrategias de precarga personalizadas para adaptarse a las necesidades específicas de la aplicación.

Para utilizar las estrategias de precarga en Angular, se pueden definir en el archivo `app-routing.module.ts` del proyecto. Allí se pueden especificar las rutas de la aplicación y las estrategias de precarga para cada ruta.

En resumen, modularizar un proyecto puede mejorar su organización y estructura, lo que facilita su mantenimiento y reutilización. Y las estrategias de precarga de módulos de Angular son útiles para mejorar la velocidad de la aplicación y la experiencia del usuario.

<!--EndFragment-->

## **Redux**

<!--StartFragment-->

Redux es un gestor del estado centralizado, para gestionar la comunicación entre distintos componentes.\
\
**NgRx** es el estándar de facto para implementar Redux en Angular. Está basada en **RxJS** y es una librería modular con todo lo necesario para crear grandes aplicaciones.

\
Sus componentes son:

1. **store**: Es el módulo principal con el administrador del estado centralizado y reactivo.

E﻿jemplo: 

```typescript
import { createStore } from 'redux';

const initialState = {
  counter: 0
};

function reducer(state = initialState, action) {
  switch (action.type) {
    case 'INCREMENT':
      return {
        ...state,
        counter: state.counter + 1
      };
    case 'DECREMENT':
      return {
        ...state,
        counter: state.counter - 1
      };
    default:
      return state;
  }
}

const store = createStore(reducer);

export default store;
```

2. **store-devtools**: Instrumentación para depurar desde el navegador. Vale su peso en oro.

E﻿jemplo:

```typescript
import { createStore } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';

const initialState = {
  counter: 0
};

function reducer(state = initialState, action) {
  switch (action.type) {
    case 'INCREMENT':
      return {
        ...state,
        counter: state.counter + 1
      };
    case 'DECREMENT':
      return {
        ...state,
        counter: state.counter - 1
      };
    default:
      return state;
  }
}

const store = createStore(reducer, composeWithDevTools());

export default store;
```

3. **router-Store**: Almacena el estado del router de Angular en el store, tratando cada evento como una acción Redux.

E﻿jemplo:

```typescript
import { StoreModule } from '@ngrx/store';
import { StoreRouterConnectingModule, routerReducer } from '@ngrx/router-store';

@NgModule({
  imports: [
    StoreModule.forRoot({}),
    StoreRouterConnectingModule.forRoot({
      routerState: RouterState.Minimal
    }),
    // ...
  ],
  // ...
})
export class AppModule {}
```

4. **effects**: Los reductores son funciones puras sin efectos colaterales. Este módulo es la solución para comandos asíncronos.

E﻿jemplo:

```typescript
import { Injectable } from '@angular/core';
import { Actions, createEffect, ofType } from '@ngrx/effects';
import { catchError, map, switchMap } from 'rxjs/operators';
import { of } from 'rxjs';

import { ApiService } from './api.service';
import { loadTodos, loadTodosSuccess, loadTodosFailure } from './todo.actions';

@Injectable()
export class TodoEffects {
  loadTodos$ = createEffect(() =>
    this.actions$.pipe(
      ofType(loadTodos),
      switchMap(() =>
        this.apiService.getTodos().pipe(
          map((todos) => loadTodosSuccess({ todos })),
          catchError((error) => of(loadTodosFailure({ error })))
        )
      )
    )
  );

  constructor(private actions$: Actions, private apiService: ApiService) {}
}
```

5. **schematics, entity, ngrx-data**: Son otros módulos opcionales con ayudas y plantillas de NgRX.

<!--EndFragment-->

## Metodos de RXjs

<!--StartFragment-->

RxJS es una biblioteca de programación reactiva para JavaScript que se utiliza comúnmente en aplicaciones de Angular. A continuación se describen algunos de los métodos más comunes de RxJS:

1. **\*of()**: Crea un observable que emite una secuencia de valores definidos.

   ```javascript
   import { of } from 'rxjs';

   const observable$ = of(1, 2, 3);

   observable$.subscribe(
     value => console.log(value), // Imprime 1, 2, 3 en consola
     error => console.error(error),
     () => console.log('Completado')
   );
   ```
2. **\*from()**: Convierte un objeto iterable o un observable-like en un observable.

   ```javascript
   import { from } from 'rxjs';

   const array = [1, 2, 3];
   const observable$ = from(array);

   observable$.subscribe(
     value => console.log(value), // Imprime 1, 2, 3 en consola
     error => console.error(error),
     () => console.log('Completado')
   );
   ```
3. **\*map()**: Transforma cada valor emitido por un observable mediante una función.

   ```javascript
   import { from } from 'rxjs';
   import { map } from 'rxjs/operators';

   const array = [1, 2, 3];
   const observable$ = from(array).pipe(
     map(value => value * 2)
   );

   observable$.subscribe(
     value => console.log(value), // Imprime 2, 4, 6 en consola
     error => console.error(error),
     () => console.log('Completado')
   );
   ```
4. **\*filter()**: Filtra los valores emitidos por un observable según un predicado.

   ```javascript
   import { from } from 'rxjs';
   import { filter } from 'rxjs/operators';

   const array = [1, 2, 3];
   const observable$ = from(array).pipe(
     filter(value => value > 1)
   );

   observable$.subscribe(
     value => console.log(value), // Imprime 2, 3 en consola
     error => console.error(error),
     () => console.log('Completado')
   );
   ```
5. **tap()**: Realiza una operación secundaria en cada valor emitido sin alterar el valor original.

   ```javascript
   import { from } from 'rxjs';
   import { tap } from 'rxjs/operators';

   const array = [1, 2, 3];
   const observable$ = from(array).pipe(
     tap(value => console.log(`Valor emitido: ${value}`))
   );

   observable$.subscribe(
     value => console.log(value),
     error => console.error(error),
     () => console.log('Completado')
   );
   ```
6. **\*debounceTime()**: Espera un tiempo determinado después de que se emite un valor antes de pasar el valor al siguiente operador.

   ```javascript
   import { fromEvent } from 'rxjs';
   import { debounceTime } from 'rxjs/operators';

   const input = document.querySelector('input');
   const observable$ = fromEvent(input, 'input').pipe(
     debounceTime(500)
   );

   observable$.subscribe(
     event => console.log(event.target.value),
     error => console.error(error),
     () => console.log('Completado')
   );
   ```
7. **\*switchMap()**: Transforma cada valor emitido por un observable en otro observable y emite los valores del último observable.

   ```javascript
   import { fromEvent, of } from 'rxjs';
   import { switchMap } from 'rxjs/operators';

   const button = document.querySelector('button');
   const observable$ = fromEvent(button, 'click').pipe(
     switchMap(() => of('Hola Mundo'))
   );

   observable$.subscribe(
     value => console.log(value), // Imprime 'Hola Mundo' en consola al hacer clic en el botón
     error => console.error(error),
     () => console.log('Completado')
   );
   ```
8. **\*catchError()**: Maneja errores en un observable y proporciona una alternativa para emitir valores.

   ```javascript
   import { throwError, of } from 'rxjs';
   import { catchError } from 'rxjs/operators';

   const observable$ = throwError('Error!').pipe(
     catchError(() => of('Ocurrió un error'))
   );

   observable$.subscribe(
     value => console.log(value), // Imprime 'Ocurrió un error' en consola
   ```
9. **merge()**: Combina múltiples observables en uno solo que emite valores de todos los observables de manera concurrente.
10. **take()**: Emite un número determinado de valores y luego completa el observable.
11. **retry()**: Intenta emitir los valores de un observable varias veces si se produce un error.
12. **share()**: Comparte un observable y sus emisiones con múltiples suscriptores.

Estos son solo algunos de los métodos de RxJS que se utilizan comúnmente. La biblioteca ofrece una gran cantidad de operadores que se pueden utilizar para crear flujos de datos reactivos y manipularlos de manera flexible y compleja.

<!--EndFragment-->

## ¿Cuando utilizar una pipe?

## ¿Que pasa cuando desde el html llamo a una funcion del componente para calcular algo y como afecta a todo el arbol de cambios y si esa funcion la paso a una pipe?

<!--StartFragment-->

La función `pipe()` en RxJS se utiliza para combinar operadores de manera que se puedan aplicar sucesivamente a un observable para transformar sus emisiones antes de que sean consumidas por los suscriptores.

En cuanto a su pregunta sobre cómo afecta a todo el árbol de cambios cuando se llama a una función del componente desde el HTML, esto dependerá de cómo esté implementada la función y de qué cambios se realicen en el estado de la aplicación como resultado de su ejecución.

En general, es importante tener en cuenta que cuando se llama a una función desde el HTML, se está ejecutando esa función en el contexto del componente y cualquier cambio que se realice en el estado del componente puede afectar a todo el árbol de cambios. Si se llama a la función con frecuencia, esto podría provocar un rendimiento deficiente en la aplicación.

Una forma de evitar este problema es mediante el uso de pipes. En lugar de llamar a una función directamente desde el HTML, se puede encapsular la lógica en una pipe que se puede aplicar a los datos en el componente antes de que se muestren en el HTML. Esto separa la lógica de presentación de la lógica de negocio y reduce el acoplamiento entre las diferentes partes de la aplicación.

Además, el uso de pipes también proporciona un mecanismo para la reutilización de código. Las pipes se pueden crear una vez y luego se pueden utilizar en múltiples componentes y vistas de la aplicación, lo que reduce la cantidad de código que se necesita escribir y mantener.

En resumen, el uso de pipes en lugar de llamar a funciones directamente desde el HTML puede ayudar a separar la lógica de presentación de la lógica de negocio, reducir el acoplamiento y mejorar el rendimiento de la aplicación.

<!--EndFragment-->

## Diferencia entre pipe y directiva

<!--StartFragment-->

Las pipes y las directivas son dos conceptos diferentes en Angular.

Las pipes se utilizan para transformar la salida de los datos en las plantillas. Se utilizan para formatear y transformar los datos en la presentación de una forma más fácil y legible para el usuario. Las pipes son muy útiles cuando se necesita formatear los datos antes de mostrarlos al usuario, como cambiar el formato de una fecha, capitalizar texto o aplicar una transformación personalizada a los datos.

Por otro lado, las directivas son un mecanismo para modificar el comportamiento de los elementos DOM. Las directivas se utilizan para agregar funcionalidades adicionales a los elementos de la vista. Las directivas se pueden usar para crear componentes personalizados, añadir comportamientos personalizados a los elementos de la vista y controlar la interacción del usuario con la aplicación.

Las principales diferencias entre pipes y directivas son:

1. **Propósito**: Las pipes se utilizan para transformar los datos en la presentación, mientras que las directivas se utilizan para modificar el comportamiento de los elementos DOM.
2. **Ubicación**: Las pipes se utilizan en las plantillas para transformar los datos que se muestran al usuario, mientras que las directivas se pueden utilizar tanto en la plantilla como en el código del componente.
3. **Forma de uso**: Las pipes se utilizan como filtros en la interpolación y en la propiedad de enlace de los elementos HTML, mientras que las directivas se utilizan como atributos personalizados de los elementos HTML.

En resumen, las pipes se utilizan para transformar los datos en la presentación, mientras que las directivas se utilizan para modificar el comportamiento de los elementos DOM. Ambas son herramientas poderosas que se pueden utilizar juntas para crear aplicaciones Angular dinámicas y personalizadas.

<!--EndFragment-->

# **J﻿avaScript**

## ¿Que me ofrece un observable que no una promesa?

<!--StartFragment-->

Un observable y una promesa son ambos mecanismos para manejar flujos asíncronos en JavaScript. Sin embargo, hay algunas diferencias clave entre ellos:

1. **Manejo de eventos múltiples**: Un observable puede manejar múltiples eventos mientras que una promesa solo puede manejar un evento.
2. **Cancelación**: Un observable puede ser cancelado en cualquier momento, mientras que una promesa no puede ser cancelada.
3. **Soporte de operadores**: Los observables proporcionan una gran cantidad de operadores de transformación, filtrado y combinación, que se pueden utilizar para transformar los datos emitidos. En cambio, las promesas no proporcionan estos operadores.
4. **Emisión de valores en tiempo real**: Los observables emiten valores en tiempo real mientras que una promesa solo emite un valor cuando se resuelve.
5. **Stream de datos**: Un observable es un flujo de datos continuo, mientras que una promesa solo emite un valor una sola vez.

En resumen, un observable ofrece más funcionalidades y flexibilidad que una promesa. Los observables se pueden usar para manejar flujos de datos continuos y pueden ser cancelados en cualquier momento, lo que es particularmente útil en aplicaciones en tiempo real. Además, los operadores de transformación de los observables permiten que los datos se procesen de manera más compleja y flexible.

<!--EndFragment-->

## Ciclos de vida de JavaScript

<!--StartFragment-->

JavaScript no tiene un ciclo de vida específico, ya que es un lenguaje de programación interpretado y su comportamiento depende del entorno en el que se esté ejecutando.

Sin embargo, los navegadores web tienen un ciclo de vida en el que se cargan y descargan los recursos, incluyendo el código JavaScript que se ejecuta en la página. A continuación, se describen los principales eventos del ciclo de vida del navegador que pueden ser relevantes para el código JavaScript:

1. `DOMContentLoaded`: Este evento se dispara cuando se ha cargado el HTML y se ha construido el árbol DOM, pero aún no se han cargado los recursos externos (como imágenes o scripts).
2. `load`: Este evento se dispara cuando se han cargado todos los recursos de la página, incluyendo las imágenes y los scripts.
3. `unload`: Este evento se dispara cuando se está descargando la página o cuando se navega fuera de ella. Se puede usar para liberar recursos o para realizar tareas de limpieza antes de que la página se cierre.

Además, en el contexto de frameworks y bibliotecas de JavaScript, como Angular, React o Vue, se definen sus propios ciclos de vida para los componentes que se crean y se destruyen a lo largo del tiempo de ejecución de la aplicación. Estos ciclos de vida son una serie de eventos que se ejecutan en el componente en un orden específico, lo que permite controlar el flujo de la aplicación y realizar tareas en diferentes momentos del ciclo de vida del componente.

En resumen, aunque JavaScript no tiene un ciclo de vida específico, los navegadores web tienen eventos relevantes para el código JavaScript y los frameworks de JavaScript definen sus propios ciclos de vida para los componentes. Es importante conocer estos eventos y ciclos de vida para poder escribir código eficiente y manejar correctamente los recursos y el flujo de la aplicación.

<!--EndFragment-->

## ¿Como compartes datos con componentes si no tienes la store en JavaScript?

<!--StartFragment-->

En JavaScript, una forma común de compartir datos entre componentes es a través de la propagación de eventos y la comunicación entre componentes mediante su árbol de elementos padre/hijo.

Por ejemplo, si tienes un componente hijo que necesita enviar datos al componente padre, puedes definir una función de devolución de llamada en el componente padre y pasarla al componente hijo a través de una propiedad de entrada. El componente hijo puede llamar a esta función de devolución de llamada con los datos necesarios, y el componente padre puede actualizar su estado en consecuencia.

Por otro lado, si necesitas compartir datos entre componentes que no están relacionados directamente, puedes utilizar una arquitectura basada en eventos, donde los componentes emiten eventos y los otros componentes los escuchan y reaccionan en consecuencia. Para ello, puedes utilizar un patrón de diseño como el patrón de publicación/suscripción (pub/sub) o el patrón de observador.

En resumen, aunque no tengas una store en JavaScript, hay varias formas de compartir datos entre componentes. La elección de la técnica adecuada dependerá del diseño de tu aplicación y de las necesidades específicas de tus componentes.

<!--EndFragment-->

<!--StartFragment-->

## Controlar los estados, la optimizacion del render, la optimizacion de los servicios un buen modulado de la aplicacion en JavaScript

<!--StartFragment-->

Controlar los estados, optimizar el render, optimizar los servicios y modularizar la aplicación son aspectos fundamentales para crear una aplicación escalable y mantenible en JavaScript.

Controlar los estados implica tener un control riguroso de los datos y su ciclo de vida en la aplicación. Para ello, se pueden utilizar diferentes técnicas, como el uso de patrones de diseño como el patrón Observador o la implementación de una arquitectura basada en eventos. También se pueden utilizar librerías y frameworks de gestión de estados, como Redux o MobX.

La optimización del render implica asegurarse de que los componentes se rendericen de manera eficiente y sólo se actualicen cuando sea necesario. Esto se puede lograr utilizando técnicas como el uso de React.memo o el uso de shouldComponentUpdate en componentes de clase.

La optimización de los servicios implica asegurarse de que la comunicación con el backend sea eficiente y no tenga un impacto negativo en la experiencia del usuario. Para ello, se pueden utilizar técnicas como el caché de solicitudes o el uso de web sockets.

Por último, modularizar la aplicación implica dividir la aplicación en módulos y componentes reutilizables, lo que facilita el mantenimiento y la escalabilidad de la aplicación. Para ello, se pueden utilizar técnicas como la división de código y la inyección de dependencias.

En resumen, controlar los estados, optimizar el render, optimizar los servicios y modularizar la aplicación son aspectos fundamentales para crear una aplicación escalable y mantenible en JavaScript.

<!--EndFragment-->

### Un ejemplo usando javascript:

<!--StartFragment-->

Supongamos que tenemos una aplicación que muestra una lista de tareas. Cada tarea se compone de un título y una descripción. Además, cada tarea tiene un estado que puede ser "completada" o "pendiente".

Para controlar el estado de las tareas, podemos utilizar un objeto JavaScript que almacene la información de cada tarea:

<!--EndFragment-->

```javascript
const tasks = [
  { id: 1, title: "Hacer la compra", description: "Comprar leche, huevos y pan", completed: false },
  { id: 2, title: "Llamar al médico", description: "Pedir cita para la semana que viene", completed: false },
  { id: 3, title: "Pasar la aspiradora", description: "Limpiar la casa", completed: true }
];
```

<!--StartFragment-->

En este caso, estamos utilizando un arreglo para almacenar las tareas, y cada tarea es un objeto con un id, un título, una descripción y un estado. El estado de cada tarea se almacena en la propiedad "completed".

Para renderizar la lista de tareas, podemos utilizar JavaScript para iterar sobre el arreglo de tareas y mostrar la información de cada tarea en la interfaz de usuario:

<!--EndFragment-->

```javascript
const taskList = document.getElementById("task-list");

tasks.forEach(task => {
  const taskElement = document.createElement("div");
  taskElement.classList.add("task");

  const titleElement = document.createElement("h2");
  titleElement.textContent = task.title;

  const descriptionElement = document.createElement("p");
  descriptionElement.textContent = task.description;

  const statusElement = document.createElement("p");
  statusElement.textContent = task.completed ? "Completada" : "Pendiente";

  taskElement.appendChild(titleElement);
  taskElement.appendChild(descriptionElement);
  taskElement.appendChild(statusElement);

  taskList.appendChild(taskElement);
});
```

<!--StartFragment-->

En este ejemplo, estamos utilizando JavaScript para crear elementos HTML dinámicamente y añadirlos al DOM. También estamos utilizando un operador ternario para mostrar el estado de cada tarea como "Completada" o "Pendiente" según su valor booleano.

Este es sólo un ejemplo sencillo, pero muestra cómo JavaScript puede utilizarse para controlar el estado de una aplicación y renderizar la información de manera dinámica en la interfaz de usuario.

<!--EndFragment-->

<!--EndFragment-->

# React

## Ciclos de vida de React

<!--StartFragment-->

En React, cada componente tiene un ciclo de vida que se puede dividir en tres fases principales: montaje, actualización y desmontaje. A continuación, se describen brevemente las diferentes fases y los métodos del ciclo de vida que se llaman en cada fase:

1. Montaje:

   * **constructor()**: Se llama antes de que se monte el componente y se usa para inicializar el estado y enlazar métodos de clase.
   * **static getDerivedStateFromProps()**: Este método se llama justo antes de renderizar el componente y se utiliza para actualizar el estado del componente a partir de los props recibidos.
   * **render()**: Este método es el que genera la salida del componente y se llama en cada actualización.
   * **componentDidMount()**: Se llama después de que el componente se haya montado en el DOM y se puede utilizar para realizar tareas como solicitudes de red o inicializar eventos.
2. Actualización:

   * **static getDerivedStateFromProps()**: Este método se llama cuando se actualizan los props y se utiliza para actualizar el estado del componente a partir de los props recibidos.
   * **shouldComponentUpdate()**: Se llama antes de la actualización y se utiliza para determinar si el componente debe actualizarse o no.
   * **render()**: Este método es el que genera la salida del componente y se llama en cada actualización.
   * **getSnapshotBeforeUpdate()**: Se llama antes de aplicar las actualizaciones al DOM y se utiliza para capturar información del estado del componente (por ejemplo, la posición de desplazamiento) antes de que cambie.
   * **componentDidUpdate()**: Se llama después de que se hayan aplicado las actualizaciones al DOM y se puede utilizar para realizar tareas como solicitudes de red o actualizar eventos.
3. Desmontaje:

   * **componentWillUnmount()**: Se llama justo antes de que se desmonte el componente y se utiliza para limpiar recursos, como eliminar eventos o cancelar solicitudes de red.

Además de estos métodos, React también proporciona algunos métodos adicionales del ciclo de vida que se pueden utilizar para manejar errores o realizar tareas específicas en diferentes momentos.

En resumen, el ciclo de vida de React se divide en tres fases principales (montaje, actualización y desmontaje) y cada fase tiene diferentes métodos del ciclo de vida que se llaman en diferentes momentos. Es importante conocer estos métodos para poder controlar el flujo de la aplicación y realizar tareas específicas en diferentes momentos del ciclo de vida del componente.

<!--EndFragment-->

## Usomemo React

<!--StartFragment-->

`useMemo` es un hook de React que permite memoizar (cachear) el resultado de una función para evitar su cálculo repetido en futuras renderizaciones. Esto puede ser útil para optimizar el rendimiento de la aplicación, ya que reduce la cantidad de cálculos innecesarios.

Para utilizar `useMemo`, se debe definir una función que calcule el resultado deseado, y pasarla como primer argumento del hook. El segundo argumento es un arreglo de dependencias que indica cuáles son las variables que deben ser observadas para que el resultado de la función sea recalculado. Si las variables no cambian, se utiliza el resultado memoizado en lugar de volver a ejecutar la función.

Para optimizar el uso de `useMemo`, se pueden seguir algunas prácticas recomendadas:

1. **Utilizar `useMemo` solo cuando sea necesario:** `useMemo` debe ser utilizado solo cuando el cálculo de la función sea costoso en términos de rendimiento, ya que su uso innecesario puede llevar a una complejidad innecesaria en el código.
2. **Evitar la memoización de funciones simples:** Si la función que se desea memoizar es muy simple, es posible que no valga la pena memoizarla, ya que el costo de memoizarla puede ser mayor que el costo de su cálculo.
3. **Ser cuidadoso con el arreglo de dependencias:** El arreglo de dependencias debe incluir todas las variables que son necesarias para el cálculo de la función, y ninguna que no lo sean. Si se incluyen variables innecesarias, el resultado de la función puede ser recalculado innecesariamente.
4. **Utilizar `useCallback` en lugar de `useMemo` para funciones:** Si se desea memoizar una función, es mejor utilizar el hook `useCallback` en lugar de `useMemo`, ya que `useCallback` memoiza la función en sí misma en lugar de su resultado.
5. **Realizar pruebas de rendimiento:** Es importante realizar pruebas de rendimiento para determinar si la memoización con `useMemo` está teniendo un impacto positivo en el rendimiento de la aplicación. Si no hay una mejora significativa, es posible que sea necesario revisar la implementación y ajustarla para obtener mejores resultados.

   En resumen, `useMemo` puede ser una herramienta muy útil para optimizar el rendimiento de una aplicación de React al memoizar el resultado de una función y evitar su cálculo innecesario en futuras renderizaciones. Para utilizarlo de manera efectiva, es importante tener en cuenta las mejores prácticas y ser cuidadoso al definir las dependencias para asegurarse de que el resultado memoizado sea siempre válido.

   Por otro lado, las estrategias de precarga (preload strategies) son técnicas que se utilizan para cargar los recursos necesarios para una ruta o vista antes de que el usuario la solicite. Estas estrategias pueden ser muy útiles para mejorar la experiencia de usuario al reducir los tiempos de carga y mejorar la sensación de velocidad de la aplicación.

   Algunas de las estrategias de precarga disponibles en Angular son:

   * `PreloadAllModules`: Carga todos los módulos en segundo plano tan pronto como sea posible.
   * `NoPreloading`: No precarga ningún módulo.
   * `PreloadSomeModules`: Carga solo algunos módulos en segundo plano.
   * `SelectivePreloadingStrategy`: Permite definir una estrategia personalizada para la precarga de módulos.

   La elección de la estrategia adecuada dependerá de las necesidades y características de la aplicación. En general, es recomendable utilizar una estrategia que cargue los módulos críticos para la experiencia del usuario de manera anticipada, mientras se evita cargar excesivamente los recursos para no sobrecargar la red y los recursos del usuario.

<!--StartFragment-->

Como se puede ver es mucha la variedad a aprender, pero como siempre digo no todo se puede saber explicar bien técnicamente, pero al menos esto sirva de conocimiento, ante cualquier pregunta tecnica.

<!--EndFragment-->