---
layout: blog
title: GraphQL y Node.js
date: 2023-05-10T10:07:25.703Z
---
<!--StartFragment-->

¡Bienvenido! En este tutorial, te guiaré a través de los pasos para crear tu primera base de datos utilizando GraphQL y Node.js. Antes de comenzar, es importante que tengas algunos conocimientos previos en programación y en GraphQL.

### Paso 1: Configuración del entorno

Primero, necesitas configurar tu entorno de desarrollo. Asegúrate de tener Node.js y npm instalados en tu computadora. Luego, crea un directorio para tu proyecto y abre una terminal en ese directorio.

Ejecuta el siguiente comando para crear un archivo package.json y definir las dependencias necesarias:

<!--EndFragment-->

```javascript
npm init -y
```

<!--StartFragment-->

Luego, instala las siguientes dependencias:

<!--EndFragment-->

```javascript
npm install express graphql express-graphql mongoose
```

<!--StartFragment-->

Estas dependencias son necesarias para crear una aplicación web con Express, implementar GraphQL con express-graphql y trabajar con una base de datos MongoDB utilizando Mongoose.

### Paso 2: Creación del esquema

Antes de comenzar a trabajar con la base de datos, necesitas definir el esquema de tu base de datos utilizando GraphQL. En la raíz de tu proyecto, crea un archivo llamado schema.graphql. En este archivo, define el esquema de tu base de datos.

Por ejemplo, puedes definir un esquema simple para una base de datos de usuarios de la siguiente manera:

<!--EndFragment-->

```javascript
type User {
  id: ID!
  name: String!
  email: String!
}

type Query {
  users: [User]!
  user(id: ID!): User
}

type Mutation {
  createUser(name: String!, email: String!): User!
  updateUser(id: ID!, name: String!, email: String!): User!
  deleteUser(id: ID!): User!
}
```

<!--StartFragment-->

Este esquema define un tipo de usuario con un ID, nombre y correo electrónico. También define tres consultas (Query) y tres mutaciones (Mutation) para trabajar con la base de datos.

### Paso 3: Creación del modelo

Luego, necesitas crear el modelo de tu base de datos utilizando Mongoose. En la raíz de tu proyecto, crea un archivo llamado user.js. En este archivo, define el modelo de usuario utilizando Mongoose.

Por ejemplo, puedes definir el modelo de usuario de la siguiente manera:

<!--EndFragment-->

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true,
    unique: true
  }
});

const User = mongoose.model('User', userSchema);

module.exports = User;
```

<!--StartFragment-->

Este modelo define un esquema de usuario con un nombre y un correo electrónico. También utiliza la función `mongoose.model()` para crear un modelo de usuario que puede ser utilizado para interactuar con la base de datos.

### Paso 4: Creación del servidor

Ahora, necesitas crear el servidor web utilizando Express. En la raíz de tu proyecto, crea un archivo llamado server.js. En este archivo, configura Express y GraphQL utilizando el esquema y modelo que has creado anteriormente.

Por ejemplo, puedes configurar el servidor de la siguiente manera:

<!--EndFragment-->

```javascript
const express = require('express');
const { graphqlHTTP } = require('express-graphql');
const mongoose = require('mongoose');
const schema = require('./schema');
const User = require('./user');

mongoose.connect('mongodb://localhost/graphql', { useNewUrlParser: true, useUnifiedTopology: true });

const app = express();

app.use('/graphql', graphqlHTTP({
  schema,
  rootValue: {
  // Query resolvers
users: async () => {
  const users = await User.find();
    return users;
},
    
user: async ({ id }) => {
  const user = await User.findById(id);
     return user;
},
  // Mutation resolvers
createUser: async ({ name, email }) => {
  const user = new User({ name, email });
    await user.save();
      return user;
},
    
updateUser: async ({ id, name, email }) => {
  const user = await User.findByIdAndUpdate(id, { name, email }, { new: true });
    return user;
},
    
deleteUser: async ({ id }) => {
  const user = await User.findByIdAndDelete(id);
     return user;
  }
},
  
  graphiql: true
}));

app.listen(3000, () => {
  console.log('Servidor iniciado en el puerto 3000');
});
```

Este código configura Express y GraphQL utilizando el esquema que has definido y los resolvers para interactuar con la base de datos utilizando el modelo de usuario que has creado.

### Paso 5: Prueba de la aplicación

Para probar la aplicación, ejecuta el siguiente comando en tu terminal:

```javascript
node server.js
```

Esto iniciará el servidor web en el puerto 3000. Abre tu navegador y dirígete a http://localhost:3000/graphql para abrir la interfaz de GraphiQL.

Aquí puedes ejecutar consultas y mutaciones para interactuar con la base de datos. Por ejemplo, para crear un nuevo usuario, puedes ejecutar la siguiente consulta en la pestaña de "Query":

```javascript
mutation {
  createUser(name: "Juan", email: "juan@example.com") {
    id
    name
    email
  }
}
```

Esto creará un nuevo usuario en la base de datos con el nombre "Juan" y el correo electrónico "juan@example.com". Luego, puedes ejecutar una consulta para obtener todos los usuarios de la base de datos:

```javascript
query {
  users {
    id
    name
    email
  }
}
```

Esto devolverá una lista de todos los usuarios en la base de datos, incluyendo el usuario que acabas de crear.

¡Felicidades! Ahora has creado tu primera base de datos utilizando GraphQL y Node.js. Este es solo el comienzo de lo que puedes hacer con GraphQL y Node.js, así que sigue explorando y creando aplicaciones increíbles.

<!--StartFragment-->

### Paso 6: Otras operaciones CRUD

Además de crear y consultar usuarios, también puedes actualizar y eliminar usuarios en la base de datos. Puedes hacer esto ejecutando mutaciones utilizando la interfaz de GraphiQL.

Para actualizar un usuario existente, puedes ejecutar la siguiente mutación:

<!--EndFragment-->

```javascript
mutation {
  updateUser(id: "user_id_here", name: "New Name", email: "new_email@example.com") {
    id
    name
    email
  }
}
```

<!--StartFragment-->

Esto actualizará el usuario con el ID proporcionado a un nuevo nombre y correo electrónico. También puedes actualizar solo el nombre o el correo electrónico si lo deseas.

Para eliminar un usuario de la base de datos, puedes ejecutar la siguiente mutación:

<!--EndFragment-->

```javascript
mutation {
  deleteUser(id: "user_id_here") {
    id
    name
    email
  }
}
```

<!--StartFragment-->

Esto eliminará el usuario con el ID proporcionado de la base de datos.

### Conclusión

En este tutorial, has aprendido cómo crear tu primera base de datos utilizando GraphQL y Node.js. Has creado un esquema de GraphQL para representar los datos de usuario, definiste resolvers para interactuar con la base de datos y creaste una API GraphQL utilizando Express.

Este es solo el comienzo de lo que puedes hacer con GraphQL y Node.js. Puedes utilizar GraphQL para crear APIs más flexibles y eficientes para cualquier tipo de aplicación. Además, puedes utilizar Node.js para construir aplicaciones de backend escalables y de alto rendimiento.

¡Sigue explorando y creando cosas asombrosas con GraphQL y Node.js!

P﻿uedes ver un ejemplo de como implentarlo en React en repositorio:

<https://github.com/jairosanchezb94/react-graphql>

<!--EndFragment-->