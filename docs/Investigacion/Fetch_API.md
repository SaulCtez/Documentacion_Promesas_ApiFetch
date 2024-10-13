---
sidebar_position: 3
---


# Fetch API

La **Fetch API** es una función de JavaScript que se puede utilizar para enviar una solicitud a cualquier URL de API web y obtener una respuesta. Esta API permite hacer peticiones HTTP para obtener recursos de forma asíncrona desde un servidor. Esto facilita el manejo de operaciones asíncronas, permitiendo encadenar múltiples acciones, como procesar respuestas JSON y actualizar la interfaz de usuario.

## Sintaxis

Para enviar una petición similar a la de un formulario HTML, solo necesitas pasar la URL a la que deseas enviar los datos como argumento a la función `fetch()`:

```javascript
fetch('https://api.ejemplo.com/endpoint', {
  method: 'POST', // Opcional: método de la solicitud
  headers: {
    'Content-Type': 'application/json' // Opcional: tipo de contenido
  },
  body: JSON.stringify({
    key: 'value' // Opcional: datos a enviar
  })
})
```


### Parámetros de la función fetch()
La función fetch() acepta dos parámetros:

URL: La URL a la que enviar la petición (este es un parámetro obligatorio).
Opciones: Las opciones a configurar en la petición. Puedes configurar el método de solicitud aquí (este es un parámetro opcional).
Promesas y manejo de respuestas
Bajo el capó, la función fetch() devuelve una promesa, por lo que necesitas agregar los métodos .then() y .catch() para manejar la respuesta.

Cuando la petición devuelve una respuesta, se llamará al método .then(). Si la solicitud devuelve un error, se ejecutará el método .catch():
```javascript
fetch('https://api.ejemplo.com/endpoint')
  .then((response) => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json(); // Procesar la respuesta JSON
  })
  .then((data) => {
    console.log(data); // Manejar los datos recibidos
  })
  .catch((error) => {
    console.error('Hubo un problema con la solicitud Fetch:', error);
  });
```
### Parámetros de la función fetch()

La función fetch() acepta dos parámetros:

URL: La URL a la que enviar la petición (este es un parámetro obligatorio).
Opciones: Las opciones a configurar en la petición. Puedes configurar el método de solicitud aquí (este es un parámetro opcional).

### Promesas y manejo de respuestas
Bajo el capó, la función fetch() devuelve una promesa, por lo que necesitas agregar los métodos .then() y .catch() para manejar la respuesta.

Cuando la petición devuelve una respuesta, se llamará al método .then(). Si la solicitud devuelve un error, se ejecutará el método .catch():

```javascript
fetch('https://api.ejemplo.com/endpoint')
  .then((response) => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json(); // Procesar la respuesta JSON
  })
  .then((data) => {
    console.log(data); // Manejar los datos recibidos
  })
  .catch((error) => {
    console.error('Hubo un problema con la solicitud Fetch:', error);
  });
```
### Consideraciones sobre el método .catch()
El método .catch() se puede omitir en la Fetch API. Se usa solo cuando Fetch no puede realizar una solicitud a la API, como por ejemplo, si no hay conexión de red o no se encuentra la URL.
# Ejercicios 

### 1: Llamada a una API con fetch() 

Utiliza el método fetch() para obtener datos de una API de tu elección. Imprime los datos resultantes en la consola. 

Utiliza el método `fetch()` para obtener datos de una API de tu elección. Imprime los datos resultantes en la consola.

```js
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
  });
  ```
  ### 2: Manejo de Errores 

Realiza una solicitud GET y maneja el error si ocurre. 
```js
fetch('https://jsonplaceholder.typicode.com/invalid-url')
  .then(response => {
    if (!response.ok) {
      throw new Error('Error en la solicitud');
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error.message));

```
### 3: Encadenar múltiples fetch 

Haz varias solicitudes fetch y muestra los resultados de ambas. 
```js
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(response => response.json())
  .then(post => {
    console.log(post);
    return fetch(`https://jsonplaceholder.typicode.com/users/${post.userId}`);
  })
  .then(response => response.json())
  .then(user => console.log(user))
  .catch(error => console.error('Error:', error));

```
### 4: Manipulación de datos de una API 

Después de realizar una llamada a una API con fetch(), utiliza el método .then() para filtrar los datos y mostrar solo los elementos que cumplan ciertos criterios (por ejemplo, mostrar solo los nombres que comiencen con "A"). 
```js
fetch('https://jsonplaceholder.typicode.com/posts')
  .then((response) => response.json())
  .then((data) => {
    const filteredPosts = data.filter((post) => post.title.startsWith('A'));
    console.log(filteredPosts);
  });

```
### 5: Solicitud GET con Parámetros 

Envía parámetros en una solicitud GET para filtrar los resultados. 
```js
const userId = 1;

fetch(`https://jsonplaceholder.typicode.com/posts?userId=${userId}`)
  .then(response => response.json())
  .then(data => console.log(`Posts del usuario ${userId}:`, data))
  .catch(error => console.error('Error:', error));

```
### 6: Promise.all con fetch 

Realiza varias solicitudes en paralelo y espera a que todas se completen. 
```js
const urls = [
  'https://jsonplaceholder.typicode.com/posts/1',
  'https://jsonplaceholder.typicode.com/posts/2',
  'https://jsonplaceholder.typicode.com/posts/3',
];

Promise.all(urls.map(url => fetch(url).then(response => response.json())))
  .then(results => console.log(results))
  .catch(error => console.error('Error:', error));

```
### 7: Encadenamiento de Promises con manipulación de datos 

Realiza una llamada a una API con fetch() y, después de recibir los datos, encadena Promises para realizar varias operaciones de manipulación de datos, como filtrar, mapear o reducir los resultados. 
```js
fetch('https://jsonplaceholder.typicode.com/posts')
  .then((response) => response.json())
  .then((data) => {
    return data.map((post) => post.title.toUpperCase());
  })
  .then((titles) => {
    console.log('Títulos en mayúsculas:', titles);
  })
  .catch((error) => {
    console.error('Error:', error);
  });

```
### 8: Subir un Archivo con fetch 

Envía un archivo a una API utilizando el método POST y el objeto FormData. 

const archivo = document.querySelector('#archivo').files[0]; 
```js
const archivo = document.querySelector('#archivo').files[0];

const formData = new FormData();
formData.append('archivo', archivo);

fetch('https://ejemplo.com/subir', {
  method: 'POST',
  body: formData
})
  .then(response => response.json())
  .then(data => console.log('Archivo subido:', data))
  .catch(error => console.error('Error:', error));

```
