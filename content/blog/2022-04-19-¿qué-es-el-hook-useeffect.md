---
layout: blog
title: ¿QUÉ ES EL HOOK USEEFFECT?
date: 2022-04-19T10:21:34.581Z
---
<!--StartFragment-->

El **Hook useEffect** es un Hook de efecto que nos permite ejecutar tareas secundaria dentro de nuestros componentes funcionales, por ejemplo, podemos emular los métodos de ciclo de vida, sin la necesidad de utilizar componentes de clase.

<!--EndFragment-->

<!--StartFragment-->

Para usar este hook, primero debemos importarlo desde la librería de React.

<!--EndFragment-->

```javascript
import React, { useEffect, useState } from 'react'
```

<!--StartFragment-->

Para ver su uso vamos a ver como podemos controlarlo mediante un ejemplo en este caso un mini formulario en el cual usaremos de prueba para entender como manejar el **useEffect** junto al **useState**. 

Ejemplo de como controlar el funcionamiento de **useEffect**:

<!--EndFragment-->

```javascript
export const SimpleForm = () => {

  const [formState, setformState] = useState({
    name: '',
    email: '',
    password: ''
  })

  const { name, email, password } = formState

  useEffect(() => {
    //console.log('useEffect')
  }, [])

  useEffect(() => {
    //console.log('formState cambió -->', formState)
  }, [formState])

  useEffect(() => {
    //console.log('formState cambió -->', email)
  }, [email])

  const handleInputChange = ({target}) => {
    setformState({
      ...formState,
      [target.name]: target.value
    })
  } 
```

<!--StartFragment-->

Como podemos ver, ya que React lo sugiere crear eventos independientes para que lo podamos ver que realiza cada escucha que realiza el **useEffect**. De esta manera podemos ver que es lo que nos trae por consola del navegador, y la reacción de este mismo evento.

<!--EndFragment-->

<!--StartFragment-->

Vamos a montar el html para poder ver por consola y en la web el resultado de lo que hemos realizado en este ejemplo supersencillo del uso del **useEffect**.

<!--EndFragment-->

```javascript
return (
    <>
        <h1>Simple Form</h1>
        <hr />

        <div className="form-group">
          <input 
            type="text"
            name="name"
            className="form-control"
            placeholder="Tu nombre"
            autoComplete="off"
            value={name}
            onChange={handleInputChange} 
          />
        </div>
        <div className="form-group">
          <input 
            type="text"
            name="email"
            className="form-control"
            placeholder="Tu email"
            autoComplete="off"
            value={email}
            onChange={handleInputChange} 
          />
        </div>
        <div className="form-group">
          <input 
            type="text"
            name="contraseña"
            className="form-control"
            placeholder="Tu contraseña"
            autoComplete="off"
            value={password}
            onChange={handleInputChange} 
          />
        </div>
    </>
  )
}
```

<!--StartFragment-->

Esto sería el resultado de todos los elementos por consola y la web.

<!--EndFragment-->

![](/content/blog/screenshot-2022-04-19-123342.png)

<!--StartFragment-->

Como podemos ver por cada elemento independiente del **useEffect** podemos ver como escucha y muestra lo que realiza cada elemento del formulario, en este caso el **formState** y el email. Esto se puede hacer para facilitar la escucha de los eventos que queramos referenciar.

<!--EndFragment-->

<!--StartFragment-->

**Conclusiones sobre useEffect**


Con el **hook useEffect** podremos ejecutar código cada vez que nuestro componente se renderice. Y no sólo eso. Ya hemos visto que es el sitio ideal para suscribirnos a eventos, ya sea del navegador o de otras fuentes, pero también que podemos manejar las desuscripción para evitar crear memory leaks.

También hemos podido entender que **useEffect** viene a sustituir en gran parte los ciclos de vida de los componentes que vimos en los componentes que extendían de la clase Component. Esto nos debería ayudar a generar menos código y hacer nuestros componentes más sencillos.

<!--EndFragment-->