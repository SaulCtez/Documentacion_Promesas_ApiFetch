# Ejercicios sobre `Promise.race`

## 1. Carrera de Dos Promesas

Crea dos promesas: una que se resuelva después de 2 segundos con el valor "Promesa 1" y otra que se resuelva después de 1 segundo con el valor "Promesa 2". Usa `Promise.race` para obtener el valor de la promesa que se resuelva primero.

### Solución

```javascript
const promesa1 = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Promesa 1");
    }, 2000);
});

const promesa2 = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Promesa 2");
    }, 1000);
});

// Usar Promise.race para obtener el valor de la promesa que se resuelva primero
Promise.race([promesa1, promesa2])
    .then((resultado) => {
        console.log(resultado); // Imprimir el resultado de la promesa que se resuelva primero
    });
```
### Explicación

- **Creación de las Promesas**: Se crean dos promesas que se resuelven en diferentes intervalos de tiempo usando `setTimeout`.  

- **Uso de `Promise.race`**: `Promise.race` toma un arreglo de promesas y se resuelve con el resultado de la primera promesa que se complete.  

- **Impresión del Resultado**: Se imprime el resultado en la consola.  


### Resultado

## 2. Manejo de Error con `Promise.race`

Crea dos promesas: una que se resuelva exitosamente después de 2 segundos y otra que se rechace con un error después de 3 segundos. Utiliza `Promise.race` para manejar ambas promesas e imprime el resultado o el error.

### Solución

```javascript
const promesaExitosa = new Promise((resolve) => {
    setTimeout(() => {
        resolve("¡Promesa resuelta exitosamente!");
    }, 2000); // Resuelve después de 2 segundos
});

const promesaConError = new Promise((_, reject) => {
    setTimeout(() => {
        reject(new Error("Algo salió mal.")); // Rechaza después de 3 segundos
    }, 3000);
});

// Usar Promise.race para manejar ambas promesas
Promise.race([promesaExitosa, promesaConError])
    .then((resultado) => {
        console.log(resultado); // Imprimir resultado si se resuelve
    })
    .catch((error) => {
        console.error("Error:", error.message); // Manejar error si se rechaza
    });
```

**Explicación**  
- **Creación de la Promesa con Error**: Se crea una promesa que se rechaza con un objeto de error después de 3 segundos.  
- **Uso de `Promise.race`**: Se utiliza `Promise.race` para manejar ambas promesas, donde la que se resuelva primero determina el resultado.  
- **Manejo del Error**: Se usa `catch()` para manejar el error y mostrar un mensaje personalizado en la consola.  

### Resultado






## Ejercicio 3: Verificación de Número Aleatorio

Crea una promesa que se resuelva con un número aleatorio entre 1 y 10. Crea otra promesa que se resuelva después de 2 segundos con el valor "Timeout". Utiliza `Promise.race` para determinar cuál de las dos promesas se resuelve primero e imprime el resultado.

### Solución

```javascript
const numeroAleatorioPromise = new Promise((resolve) => {
    const numeroAleatorio = Math.floor(Math.random() * 10) + 1; // Genera un número entre 1 y 10
    resolve(numeroAleatorio); // Resuelve la promesa con el número aleatorio
});

const timeoutPromise = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Timeout"); // Resuelve con "Timeout" después de 2 segundos
    }, 2000);
});

// Usar Promise.race para determinar cuál promesa se resuelve primero
Promise.race([numeroAleatorioPromise, timeoutPromise])
    .then((resultado) => {
        console.log("Resultado:", resultado); // Imprimir resultado
    })
    .catch((error) => {
        console.error("Error:", error); // Manejo de errores (opcional)
    });
```

**Explicación**  
- **Creación de la Promesa Aleatoria**: Se crea una promesa que se resuelve con un número aleatorio entre 1 y 10.  
- **Promesa de Timeout**: Se crea otra promesa que se resuelve después de 2 segundos con el valor "Timeout".  
- **Uso de `Promise.race`**: Se usa `Promise.race` para determinar cuál de las dos promesas se resuelve primero.  
- **Impresión del Resultado**: Se imprime el resultado en la consola.  

### Resultado


## Ejercicio 4: Verificación de Estado de Red

Crea tres promesas que simulen verificar la conexión a internet con diferentes tiempos de respuesta (1, 2 y 3 segundos). Utiliza `Promise.race` para determinar cuál promesa se resuelve primero e imprime el resultado.

### Solución

```javascript
const verificarConexion1 = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Conexión rápida (1 segundo)"); // Resuelve después de 1 segundo
    }, 1000);
});

const verificarConexion2 = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Conexión media (2 segundos)"); // Resuelve después de 2 segundos
    }, 2000);
});

const verificarConexion3 = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Conexión lenta (3 segundos)"); // Resuelve después de 3 segundos
    }, 3000);
});

// Usar Promise.race para determinar cuál promesa se resuelve primero
Promise.race([verificarConexion1, verificarConexion2, verificarConexion3])
    .then((resultado) => {
        console.log("Resultado de la conexión:", resultado); // Imprimir resultado
    })
    .catch((error) => {
        console.error("Error:", error); // Manejo de errores (opcional)
    });
```

**Explicación**  
- **Creación de Promesas de Conexión**: Se crean tres promesas que simulan la verificación de la conexión con diferentes tiempos de respuesta.  
- **Uso de `Promise.race`**: Se utiliza `Promise.race` para obtener el resultado de la conexión que responde primero.  
- **Impresión del Resultado**: Se imprime el resultado en la consola.  

### Resultado


## Ejercicio 5: Cancelación de Tarea Asíncrona

Crea una promesa que simule una tarea que tarda 5 segundos en completarse. Crea otra promesa que se resuelva después de 3 segundos, indicando que el tiempo se ha agotado. Utiliza `Promise.race` para determinar si se completa la tarea o si se cancela debido al tiempo agotado e imprime el resultado.

### Solución

```javascript
const tareaAsincrona = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Tarea completada exitosamente."); // Resuelve después de 5 segundos
    }, 5000);
});

const cancelacion = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Tiempo agotado. Tarea cancelada."); // Resuelve después de 3 segundos
    }, 3000);
});

// Usar Promise.race para determinar si se completa la tarea o se cancela
Promise.race([tareaAsincrona, cancelacion])
    .then((resultado) => {
        console.log(resultado); // Imprimir resultado
    })
    .catch((error) => {
        console.error("Error:", error); // Manejo de errores (opcional)
    });
```


**Explicación**  
- **Creación de la Tarea Asíncrona**: Se crea una promesa que simula una tarea que tarda 5 segundos en completarse.  
- **Promesa de Cancelación**: Se crea otra promesa que se resuelve después de 3 segundos, indicando que el tiempo se ha agotado.  
- **Uso de `Promise.race`**: Se utiliza `Promise.race` para determinar si se completa la tarea o si se cancela debido al tiempo agotado.  
- **Impresión del Resultado**: Se imprime el resultado en la consola.  

### Resultado

## Ejercicio 6: Temporizador con Cancelación

Crea un temporizador usando `Promise.race` que se resuelva con un mensaje "Se acabó el tiempo" después de 5 segundos y se cancele si una promesa se resuelve en menos de 5 segundos.

### Solución

```javascript
const temporizador = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Se acabó el tiempo."); // Resuelve después de 5 segundos
    }, 5000);
});

// Promesa que se resuelve en menos de 5 segundos
const tarea = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Tarea completada antes del tiempo."); // Resuelve antes de 5 segundos
    }, 3000);
});

// Usar Promise.race para manejar el temporizador y la tarea
Promise.race([temporizador, tarea])
    .then((resultado) => {
        console.log(resultado); // Imprimir resultado
    });
```
### Explicación 

- **Creación del Temporizador**: Se crea una promesa que se resuelve con un mensaje "Se acabó el tiempo" después de 5 segundos usando `setTimeout`.
- **Creación de la Tarea**: Se crea otra promesa que se resuelve en 3 segundos, simulando una tarea que se completa antes de que expire el temporizador.
- **Uso de `Promise.race`**: Se utiliza `Promise.race` para correr ambas promesas al mismo tiempo y obtener el resultado de la primera que se resuelva. En este caso, la tarea se completa antes que el temporizador.
- **Impresión del Resultado**: El resultado de la primera promesa que se resuelve es impreso en la consola.

### Resultado
![Resultado](../imgpromisechain/5.png)


## Ejercicio 7: Promesas Rápida y Lenta

Crea una función que devuelva una promesa que se resuelva en 1 segundo con el valor "Rápido" y otra que se resuelva en 3 segundos con el valor "Lento". Usa `Promise.race` para mostrar el resultado.

### Solución

```javascript
const promesaRapida = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Rápido"); // Resuelve después de 1 segundo
    }, 1000);
});

const promesaLenta = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Lento"); // Resuelve después de 3 segundos
    }, 3000);
});

// Usar Promise.race para mostrar el resultado
Promise.race([promesaRapida, promesaLenta])
    .then((resultado) => {
        console.log("Resultado:", resultado); // Imprimir resultado
    });
```
### Explicación 

- **Creación de Promesas**: Se crean dos promesas: una que se resuelve en 1 segundo (con el valor "Rápido") y otra que se resuelve en 3 segundos (con el valor "Lento").
- **Uso de `Promise.race`**: Se utiliza `Promise.race` para iniciar ambas promesas al mismo tiempo y obtener el resultado de la que se resuelve primero. En este caso, la promesa rápida se resuelve antes que la lenta.
- **Impresión del Resultado**: El resultado de la promesa más rápida es impreso en la consola.

### Resultado
![Resultado](../imgpromisechain/6.png)


## Ejercicio 8: Retrasos de Promesas

Crea una promesa que simule un retraso de 4 segundos y una segunda que simule un retraso de 2 segundos. Usa `Promise.race` para obtener el resultado de la promesa que se resuelva primero.

### Solución

```javascript
const promesa4Segundos = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Resultado de la promesa de 4 segundos."); // Resuelve después de 4 segundos
    }, 4000);
});

const promesa2Segundos = new Promise((resolve) => {
    setTimeout(() => {
        resolve("Resultado de la promesa de 2 segundos."); // Resuelve después de 2 segundos
    }, 2000);
});

// Usar Promise.race para obtener el resultado de la promesa que se resuelva primero
Promise.race([promesa4Segundos, promesa2Segundos])
    .then((resultado) => {
        console.log("Resultado:", resultado); // Imprimir resultado
    });
```

### Explicación

- **Creación de Promesas con Retrasos**: Se crean dos promesas que simulan retrasos de diferentes duraciones: una de 4 segundos y otra de 2 segundos, utilizando `setTimeout`.
- **Uso de `Promise.race`**: `Promise.race` se usa para determinar cuál promesa se resuelve primero. En este caso, la promesa de 2 segundos se resuelve antes que la de 4 segundos.
- **Impresión del Resultado**: El resultado de la promesa que se resuelve más rápido se imprime en la consola.

### Resultado
<!-- ![Resultado](../imgpromisechain/10.png) -->
