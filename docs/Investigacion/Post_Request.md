---
sidebar_position: 4
---
# POST Requests con Fetch API

Las peticiones **POST** se utilizan para enviar datos al servidor, comúnmente para crear nuevos recursos o enviar información de formularios. A diferencia de las peticiones **GET**, que solo recuperan datos, las solicitudes **POST** permiten enviar datos en el cuerpo de la solicitud.

## Configuración de un POST Request

Para hacer una petición **POST** con Fetch API, es necesario pasar un objeto de opciones de configuración como segundo argumento en el `fetch`. Este objeto opcional puede incluir muchos parámetros diferentes, pero los más esenciales son:

1. **method**: Indica que estamos utilizando el método POST.
2. **headers**: Para especificar que los datos se enviarán en formato JSON, debemos establecer el encabezado `Content-Type` con el valor `application/json`.
3. **body**: Aquí se incluirán los datos que deseamos enviar, normalmente en formato JSON. Para ello, debemos convertir el objeto JavaScript en una cadena JSON utilizando `JSON.stringify()`.

### Ejemplo de un POST Request

A continuación se muestra cómo hacer una solicitud POST que envía los datos necesarios para crear una nueva publicación de blog:

```js
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    title: 'Nueva publicación',
    body: 'Este es el contenido de la nueva publicación.',
    userId: 1
  })
})
  .then(response => response.json())
  .then(data => console.log('Publicación creada:', data))
  .catch(error => console.error('Error:', error));
```
Si tu solicitud POST es exitosa, recibirás un cuerpo de respuesta que contendrá el objeto de la nueva publicación junto con una nueva ID. La respuesta puede variar dependiendo de cómo esté configurada la API.

Es importante tener en cuenta que los puntos finales de las APIs pueden cambiar con el tiempo y las APIs pueden ser reestructuradas. Por esta razón, es una buena práctica organizar todas las llamadas fetch juntas en un lugar centralizado para facilitar el acceso y la modificación futura.
# Ejercicios con Solicitudes POST y Fetch

### 1: Solicitud POST Básica

Envía un objeto JSON a una API con el método POST y muestra la respuesta.

```js
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    title: 'Post de prueba',
    body: 'Este es el contenido del post.',
    userId: 1
  })
})
  .then(response => response.json())
  .then(data => console.log('Post creado:', data))
  .catch(error => console.error('Error:', error));
```
### 2: Solicitud POST con Manejo de Errores 

Realiza una solicitud POST y maneja los errores de forma adecuada si la respuesta no es exitosa. 
```js
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    title: 'Post erróneo',
    body: 'Este post puede fallar.',
    userId: 2
  })
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Error en la solicitud');
    }
    return response.json();
  })
  .then(data => console.log('Post creado:', data))
  .catch(error => console.error('Error capturado:', error));

```
### 3: Enviar Datos de un Formulario con POST 

Toma los datos de un formulario HTML y envíalos en una solicitud POST. 
```js
<form id="miFormulario">
  <input type="text" id="titulo" name="titulo" placeholder="Título">
  <textarea id="contenido" name="contenido" placeholder="Contenido"></textarea>
  <button type="submit">Enviar</button>
</form>

<script>
  document.getElementById('miFormulario').addEventListener('submit', function(event) {
    event.preventDefault();

    const titulo = document.getElementById('titulo').value;
    const contenido = document.getElementById('contenido').value;

    fetch('https://jsonplaceholder.typicode.com/posts', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        title: titulo,
        body: contenido,
        userId: 1
      })
    })
      .then(response => response.json())
      .then(data => console.log('Post enviado:', data))
      .catch(error => console.error('Error:', error));
  });
</script>

```
### 4:Solicitud POST con async/await 

Reescribe una solicitud POST utilizando async/await para simplificar el manejo de promesas. 
```js
async function crearPost() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        title: 'Post con async/await',
        body: 'Este es un post utilizando async/await.',
        userId: 3
      })
    });

    const data = await response.json();
    console.log('Post creado:', data);
  } catch (error) {
    console.error('Error:', error);
  }
}

crearPost();

```
### 5: Enviar Datos como FormData 

Envía datos como FormData en lugar de JSON, útil cuando trabajas con formularios que incluyen archivos. 
```js
const formData = new FormData();
formData.append('title', 'Post con FormData');
formData.append('body', 'Este post se envía con FormData');
formData.append('userId', 4);

fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  body: formData
})
  .then(response => response.json())
  .then(data => console.log('Post creado con FormData:', data))
  .catch(error => console.error('Error:', error));

```
### 6: Enviar Archivos en una Solicitud POST 

Envía un archivo en una solicitud POST utilizando FormData. 
```js
<input type="file" id="archivo" name="archivo">

<script>
  const inputArchivo = document.getElementById('archivo');

  inputArchivo.addEventListener('change', function() {
    const archivo = inputArchivo.files[0];

    const formData = new FormData();
    formData.append('archivo', archivo);

    fetch('https://ejemplo.com/subir', {
      method: 'POST',
      body: formData
    })
      .then(response => response.json())
      .then(data => console.log('Archivo subido:', data))
      .catch(error => console.error('Error:', error));
  });
</script>

```
### 7: Solicitud POST con Datos Anidados 

Envía un objeto JSON con datos anidados (objetos dentro de objetos) a una API. 
```js
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    title: 'Post con datos anidados',
    body: 'Este es un post con un objeto anidado.',
    userId: 5,
    metadata: {
      author: 'Juan Pérez',
      date: '2024-10-10'
    }
  })
})
  .then(response => response.json())
  .then(data => console.log('Post con datos anidados:', data))
  .catch(error => console.error('Error:', error));
```
### 8:Actualizar Datos Usando POST y PUT 

Envía datos utilizando POST para crear un recurso y PUT para actualizarlo. 
```js
const nuevoPost = {
  title: 'Nuevo post',
  body: 'Este es un nuevo post.',
  userId: 6
};

const postId = 1;  // Suponiendo que estamos actualizando el post con ID 1

// Crear un nuevo post
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(nuevoPost)
})
  .then(response => response.json())
  .then(data => {
    console.log('Nuevo post creado:', data);

    // Actualizar el post
    return fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`, {
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        title: 'Post actualizado',
        body: 'Este post ha sido actualizado.',
        userId: 6
      })
    });
  })
  .then(response => response.json())
  .then(data => console.log('Post actualizado:', data))
  .catch(error => console.error('Error:', error));

```
