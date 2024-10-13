---
sidebar_position: 1
---

# Promises

El objeto `Promise` representa la eventual finalización (o falla) de una operación asincrónica y su valor resultante.

Una Promesa actúa como un proxy para un valor que no necesariamente se conoce cuando se crea. Permite asociar controladores con el eventual valor de éxito o el motivo de falla de una acción asincrónica. Esto permite que los métodos asíncronos devuelvan valores como los métodos síncronos: en lugar de devolver inmediatamente el valor final, el método asíncrono devuelve la promesa de proporcionar el valor en el futuro.

Una promesa pendiente puede cumplirse con un valor o rechazarse con un motivo (error). Cuando ocurre cualquiera de estas opciones, se llama a los controladores asociados con el método `then` de la promesa. Si la promesa ya se ha cumplido o rechazado cuando se adjunta un controlador, este será llamado inmediatamente, lo que evita condiciones de carrera.

Como los métodos `Promise.prototype.then()` y `Promise.prototype.catch()` devuelven promesas, se pueden encadenar.

## Sintaxis y Uso Básico

### Creación de una Promesa

Para crear una promesa, se usa el constructor `Promise`, que recibe una función ejecutora con dos parámetros: `resolve` y `reject`.

```javascript
const miPromesa = new Promise((resolve, reject) => {
  // operación asíncrona
  let exito = true;

  if (exito) {
    resolve('Operación exitosa');
  } else {
    reject('Operación fallida');
  }
});
```

# Consumo de Promesas

Una vez creada la promesa, se pueden manejar los resultados utilizando los métodos `.then()`, `.catch()`, y `.finally()`:

- **`then()`**: Maneja el resultado cuando la promesa se cumple.
- **`catch()`**: Maneja los errores cuando la promesa es rechazada.
- **`finally()`**: Se ejecuta después de que la promesa se haya cumplido o rechazado, sin importar el resultado.
`
```javascript
miPromesa
  .then(resultado => {
    console.log(resultado); // 'Operación exitosa'
  })
  .catch(error => {
    console.error(error); // 'Operación fallida'
  })
  .finally(() => {
    console.log('Operación completada'); // siempre se ejecuta
  });
  ```
  # Encadenamiento de Promesas

Las promesas permiten encadenar múltiples operaciones asincrónicas. Cada llamada a `.then()` devuelve una nueva promesa, lo que facilita el manejo secuencial de tareas asincrónicas:

```javascript
miPromesa
  .then(resultado => {
    console.log(resultado); // 'Operación exitosa'
    return 'Siguiente tarea';
  })
  .then(siguienteResultado => {
    console.log(siguienteResultado); // 'Siguiente tarea'
  })
  .catch(error => {
    console.error('Error:', error);
  });
  ```
 # Ejercicios

 ### 1:Crea una Promise que se resuelva después de 3 segundos y luego imprima "Promise resuelta" cuando se cumpla. 
 ```js
const miPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise resuelta');
  }, 3000);
});

miPromise.then((resultado) => {
  console.log(resultado);
});
```
### 2. Define una función asincrónica que espere 1 segundo y luego devuelva una cadena que diga "Operación completada". Utiliza async/await. 

```js
async function operacionAsincronica() {
  await new Promise((resolve) => setTimeout(resolve, 1000));
  return 'Operación completada';
}

async function ejecutarOperacion() {
  const resultado = await operacionAsincronica();
  console.log(resultado);
}

ejecutarOperacion();
```
### 3. Manejo de errores con Promises
 Crea una Promise que se rechace después de 2 segundos y captura el error para imprimir "Error: Promise rechazada". 
```js
const miPromiseRechazada = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('Promise rechazada');
  }, 2000);
});

miPromiseRechazada.catch((error) => {
  console.log('Error:', error);
});

```
### 4. Promesa con Rechazo
Crea una promesa que se resuelva o rechace dependiendo de un valor booleano. 

```js 
const promesaCondicional = (condicion) => {
  return new Promise((resolve, reject) => {
    if (condicion) {
      resolve("La condición fue verdadera");
    } else {
      reject("La condición fue falsa");
    }
  });
};

promesaCondicional(true)
  .then((mensaje) => console.log(mensaje))
  .catch((error) => console.log(error));

```

### 5. Promesa con setTimeout
 Crea una promesa que se resuelva después de un tiempo aleatorio entre 1 y 3 segundos.
```js
const promesaAleatoria = () => {
  return new Promise((resolve) => {
    const tiempo = Math.floor(Math.random() * 3000) + 1000;
    setTimeout(() => {
      resolve(`Promesa resuelta después de ${tiempo} ms`);
    }, tiempo);
  });
};

promesaAleatoria().then((mensaje) => console.log(mensaje));

```
### 6. Convertir Función Asíncrona con Promesas
 Convierte una función que utiliza setTimeout en una que devuelve una promesa. 
```js
const esperar = (ms) => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(`Esperado por ${ms} ms`);
    }, ms);
  });
};

esperar(2000).then((mensaje) => console.log(mensaje));

```
### 7. Crea una Promesa que simule la realización de una tarea simple, como preparar un café.
Usa setTimeout para simular un retraso de 2 segundos antes de que la Promesa se cumpla. Muestra cómo usar .then() para manejar la Promesa cumplida. 

```js
function prepararUnCafe() {
  return new Promise((resolve) => {
    console.log("Preparando tu café...");
    setTimeout(() => {
      resolve("El café está listo.");
    }, 2000);
  });
}

prepararUnCafe().then((resultado) => {
  console.log(resultado);
});

```
### 8.Encadenamiento de Promises
 Crea tres Promises consecutivas, donde cada una se resuelva después de 1 segundo y devuelva un número diferente. Luego, encadena las tres Promises para sumar los resultados y mostrar el resultado final. 
```js
function crearPromiseConRetraso(valor, retraso) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(valor);
    }, retraso);
  });
}

let numero1;
let numero2;
let numero3;

crearPromiseConRetraso(1, 1000)
  .then((resultado1) => {
    console.log(resultado1);
    numero1 = resultado1;
    return crearPromiseConRetraso(2, 1000);
  })
  .then((resultado2) => {
    console.log(resultado2);
    numero2 = resultado2;
    return crearPromiseConRetraso(3, 1000);
  })
  .then((resultado3) => {
    console.log(resultado3);
    numero3 = resultado3;
    const suma = numero1 + numero2 + numero3;
    console.log('Suma:', suma);
  });

```

