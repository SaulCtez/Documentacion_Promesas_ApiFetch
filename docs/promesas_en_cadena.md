# Promesas en Cadena

Imagina una línea de producción donde cada paso depende del resultado del anterior. En programación asíncrona, este flujo secuencial de operaciones se logra con el encadenamiento de promesas.

## ¿Qué es una promesa?

Una promesa es un objeto que representa la eventual compleción (o fracaso) de una operación asíncrona. Puede estar en tres estados:

- **Pendiente**: La operación aún no ha terminado.
- **Cumplida**: La operación se completó con éxito.
- **Rechazada**: La operación falló.

## ¿Y el encadenamiento?

El encadenamiento de promesas consiste en conectar una serie de promesas, donde el resultado de una promesa se pasa como entrada a la siguiente. Esto crea una secuencia de operaciones que se ejecutan de forma asíncrona, pero de manera ordenada.

## ¿Por qué es útil?

- **Mejora la legibilidad**: Evita anidar callbacks, haciendo el código más limpio y fácil de entender.
- **Simplifica el manejo de errores**: Permite manejar errores de forma centralizada en un solo lugar.
- **Facilita el flujo de datos**: Permite pasar datos entre diferentes operaciones asíncronas.

Podemos decir que una promesa es un objeto que representa la terminación o el fracaso de una operación asíncrona. Dado que la mayoría de las personas consumen promises ya creadas, las promesas en cadena son una forma de ejecutar varias operaciones asíncronas una tras otra. Esto se logra creando una secuencia de promesas, donde cada operación posterior se inicia cuando la anterior tiene éxito.

![Explicación de promesas en JavaScript](https://cdn.hashnode.com/res/hashnode/image/upload/v1628159334680/NIcSeGwUU.png?border=1,CCCCCC&auto=compress&auto=compress,format&format=webp)

## Sintaxis de una promesa en cadena

```javascript
primeraPromesa()
  .then((resultado1) => {
    // Manejar el resultado de la primera promesa
    return segundaPromesa(resultado1); // Retornar otra promesa
  })
  .then((resultado2) => {
    // Manejar el resultado de la segunda promesa
    return terceraPromesa(resultado2); // Retornar una tercera promesa
  })
  .then((resultado3) => {
    // Manejar el resultado de la tercera promesa
    console.log('Resultado final:', resultado3);
  })
  .catch((error) => {
    // Manejar cualquier error que ocurra en la cadena
    console.error('Error en la cadena de promesas:', error);
  });

```
### Explicación:
**1. primeraPromesa()**: Es una función que retorna una promesa.

**2. then((resultado1)) =>**: Cuando se resuelve la primera promesa, se ejecuta el código dentro de este bloque con el resultado.

**3. Segunda promesa(resultado1)**: Cuando se resuelve la primera promesa, se ejecuta el código dentro de este bloque con el resultado.

**4. SegundaPromesa(resultado1)**: Aquí se encadena una segunda promesa basada en el resultado de la primera.

**5. then(resultado2) =>**: Maneja el resultado de la segunda promesa.

**6. Catch(error)**: Captura cualquier error que ocurra en cualquier parte de la cadena.
