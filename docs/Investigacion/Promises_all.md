---
sidebar_position: 2
---



# Promise.all

El método `Promise.all(iterable)` devuelve una promesa que termina correctamente cuando todas las promesas en el argumento iterable han sido concluidas con éxito, o bien rechaza la petición con el motivo pasado por la primera promesa que es rechazada.

## Descripción

`Promise.all` se cumple cuando todas las promesas del iterable dado se han cumplido, o es rechazada si alguna promesa no se cumple. Si alguna de las promesas pasadas en el argumento iterable falla, la promesa `all` es rechazada inmediatamente con el valor de la promesa que fue rechazada, descartando todas las demás promesas, hayan sido o no cumplidas. Si se pasa un array vacío a `all`, la promesa se cumple inmediatamente.

## Sintaxis

```javascript
Promise.all(iterable); 
```



## Valor devuelto
Una Promise que se cumplirá cuando todas las promesas del argumento iterable hayan sido cumplidas, o bien se rechazará cuando alguna de ellas se rechace.

## Ejemplos
### Uso de Promise.all
Promise.all espera a que todo se cumpla (o bien al primer rechazo).

```javascript
const promesa1 = Promise.resolve(3);
const promesa2 = 42;
const promesa3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, '¡Hola!');
});

Promise.all([promesa1, promesa2, promesa3]).then((valores) => {
  console.log(valores); // [3, 42, '¡Hola!']
});
```
 ### Comportamiento de fallo rápido
Promise.all se rechaza si uno de los elementos ha sido rechazado. Promise.all falla rápido: si tienes cuatro promesas que se resuelven después de un timeout y una de ellas falla inmediatamente, entonces Promise.all se rechaza inmediatamente.
```javascript
const promesaRápida = Promise.reject('Error en la promesa rápida');
const promesaLenta = new Promise((resolve) => {
  setTimeout(resolve, 100, 'Resultado de la promesa lenta');
});

Promise.all([promesaRápida, promesaLenta])
  .then((valores) => {
    console.log(valores);
  })
  .catch((error) => {
    console.error(error); // 'Error en la promesa rápida'
  });

```
# Ejercicios 

### 1: Promise.all() 

Crea tres Promises que se resuelvan después de diferentes intervalos de tiempo y luego utilice Promise.all() para mostrar un mensaje cuando todas se hayan resuelto.
```js
const promise1 = new Promise((resolve) => setTimeout(() => resolve(1), 1000));
const promise2 = new Promise((resolve) => setTimeout(() => resolve(2), 2000));
const promise3 = new Promise((resolve) => setTimeout(() => resolve(3), 1500));

Promise.all([promise1, promise2, promise3]).then((resultados) => {
  console.log('Todas las Promises se han resuelto:', resultados);
});
```
### 2: Promise.all con Rechazo 

Crea un grupo de promesas donde una se rechaza. Observa cómo Promise.all maneja el rechazo. 
```js
const promesa1 = new Promise((resolve) => setTimeout(() => resolve("Promesa 1 completa"), 1000));
const promesa2 = new Promise((_, reject) => setTimeout(() => reject("Promesa 2 fallida"), 1500));
const promesa3 = new Promise((resolve) => setTimeout(() => resolve("Promesa 3 completa"), 2000));

Promise.all([promesa1, promesa2, promesa3])
  .then((resultados) => console.log(resultados))
  .catch((error) => console.log(`Error capturado: ${error}`));

```
### 3: Promise.all con Funciones que Devuelven Promesas 

Crea funciones que devuelvan promesas y utiliza Promise.all para esperar los resultados de todas. 
```js
const tareaAsincrona = (mensaje, tiempo) => {
  return new Promise((resolve) => {
    setTimeout(() => resolve(mensaje), tiempo);
  });
};

Promise.all([tareaAsincrona("Tarea 1", 1000), tareaAsincrona("Tarea 2", 2000)])
  .then((resultados) => console.log(resultados));  

```
### 4: Promise.allSettled() 

Realiza tres Promises, algunas de las cuales se resuelvan y otras se rechacen. Utiliza Promise.allSettled() para obtener información sobre el estado de todas las Promises. 
```js
const promise1 = new Promise((resolve) => setTimeout(() => resolve(1), 1000));
const promise2 = new Promise((resolve, reject) => setTimeout(() => reject('Error en Promise 2'), 2000));
const promise3 = new Promise((resolve) => setTimeout(() => resolve(3), 1500));

Promise.allSettled([promise1, promise2, promise3]).then((resultados) => {
  console.log('Estado de todas las Promises:', resultados);
});

```
### 5: Promise.all con un Array Dinámico 

Genera un número dinámico de promesas en un bucle y usa Promise.all para esperar a que todas se resuelvan. 
```js
const generarPromesas = (cantidad) => {
  const promesas = [];
  for (let i = 1; i <= cantidad; i++) {
    promesas.push(new Promise((resolve) => setTimeout(() => resolve(`Promesa ${i}`), i * 1000)));
  }
  return Promise.all(promesas);
};

generarPromesas(3).then((resultados) => console.log(resultados)); 
```
### 6: Promise.all con Procesamiento de Resultados 

Crea un grupo de promesas y procesa los resultados una vez que todas se resuelvan. 
```js
const calcularSuma = (a, b) => {
  return new Promise((resolve) => {
    setTimeout(() => resolve(a + b), 1000);
  });
};

Promise.all([calcularSuma(1, 2), calcularSuma(3, 4), calcularSuma(5, 6)])
  .then((resultados) => {
    const sumaTotal = resultados.reduce((acc, valor) => acc + valor, 0);
    console.log(`Suma total: ${sumaTotal}`);  
  });

```
###  7: Promise.all con Promesas Anidadas 

Crea una promesa que dependa de otras dos promesas utilizando Promise.all. 
```js
const obtenerValor = (valor) => new Promise((resolve) => setTimeout(() => resolve(valor), 1000));

const combinarValores = () => {
  return Promise.all([obtenerValor(5), obtenerValor(10)]).then(([valor1, valor2]) => valor1 + valor2);
};

Promise.all([combinarValores(), obtenerValor(20)])
  .then((resultados) => console.log(`Resultados combinados: ${resultados}`));  

```
### 8: Promise.all con Manejo de Errores y Resultados Parciales 

Implementa un manejo avanzado de errores donde algunas promesas pueden fallar, pero se quiere obtener los resultados de las que se resuelvan correctamente. 
```js
const tareaExitosa = (mensaje) => new Promise((resolve) => setTimeout(() => resolve(mensaje), 1000));
const tareaFallida = (mensaje) => new Promise((_, reject) => setTimeout(() => reject(mensaje), 1000));

Promise.allSettled([tareaExitosa("Tarea 1 completa"), tareaFallida("Tarea 2 fallida"), tareaExitosa("Tarea 3 completa")])
  .then((resultados) => {
    resultados.forEach((resultado) => {
      if (resultado.status === "fulfilled") {
        console.log(`Éxito: ${resultado.value}`);
      } else {
        console.log(`Error: ${resultado.reason}`);
      }
    });
  });

```

