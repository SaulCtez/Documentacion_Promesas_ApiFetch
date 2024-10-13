# Promise.race 

## Concepto
**`Promise.race()`** es un método que permite ejecutar múltiples promesas en paralelo y devuelve una nueva promesa que se resuelve o rechaza tan pronto como una de las promesas originales se resuelve o rechaza. Es como una carrera donde la primera promesa en cruzar la línea de meta determina el resultado final.

## Definición
El método **`Promise.race(iterable)`** retorna una promesa que se cumplirá o no tan pronto como una de las promesas del argumento iterable se cumpla o se rechace, con el valor o razón de rechazo de ésta.

## Sintaxis
```javascript
Promise.race([promesa1, promesa2, promesa3])
  .then((resultado) => {
    // Se resuelve con el valor de la promesa que se haya completado primero
    console.log('Primera promesa en resolverse:', resultado);
  })
  .catch((error) => {
    // Si alguna promesa es rechazada antes de que otra se resuelva
    console.error('Primera promesa en fallar:', error);
  });
```

## Explicacón

**Promise.race()**: Toma un arreglo de promesas.

Se **resuelve** o **rechaza** tan pronto como una de las promesas se complete (ya sea con éxito o con error).

**.then()** se ejecuta con el resultado de la primera promesa en completarse.

**.catch()** se ejecuta si la primera promesa en completarse es rechazada.

![Promise.race](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRb70GTREGozXxSiPiy_gCqvCkcb0Vr9F8qRw&s)
