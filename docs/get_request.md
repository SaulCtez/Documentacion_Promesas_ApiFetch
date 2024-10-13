# GET requests con Fetch API

## ¿Qué es una petición GET?
Una petición GET es un tipo de solicitud HTTP que se utiliza para solicitar datos de un servidor. Es el método más común y seguro para recuperar información, ya que no modifica los datos en el servidor.

Una **GET request** (solicitud GET) es uno de los métodos más comunes utilizados en el protocolo HTTP para solicitar datos de un servidor. En una solicitud GET, el cliente (como un navegador web) pide al servidor que le envíe información, y el servidor responde con los datos solicitados.

![Demostración grafica de Get Request](https://www.jcchouinard.com/wp-content/uploads/2023/04/http-requests.png)

### Características clave de una GET request:
1. **Sin cuerpo de solicitud**: Las solicitudes GET no tienen un cuerpo, ya que están diseñadas únicamente para recuperar datos, no para enviarlos. La información que el cliente envía al servidor se coloca en la URL (por ejemplo, en parámetros de consulta o "query parameters").
2. **Uso en la URL**: Los datos de la solicitud (como los parámetros) se añaden a la URL después del signo `?`. Ejemplo: `https://ejemplo.com/busqueda?query=javascript`.
3. **Idempotente**: Repetir una solicitud GET no debería tener efectos secundarios. Cada vez que se hace una solicitud GET, debe obtenerse el mismo resultado (si los datos del servidor no han cambiado).
4. **Seguro**: Una solicitud GET no cambia el estado del servidor. Solo solicita información, pero no modifica los datos en el servidor.

## Realizando una petición GET con Fetch

```javascript
fetch('https://api.example.com/datos')
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```
### Explicación del código: 

**fetch('https://api.example.com/datos')**:
   - `fetch()` es la función principal de Fetch API.
   - Se le pasa la URL del recurso que queremos obtener.
   - Devuelve una promesa que se resuelve con un objeto `Response`.

**.then(response => response.json())**:
   - Si la petición es exitosa, se ejecuta esta función.
   - `response.json()` convierte el cuerpo de la respuesta en un objeto JavaScript (asumiendo que el servidor devuelve datos en formato JSON).
   - Devuelve otra promesa que se resuelve con el objeto JavaScript convertido.

**.then(data =>  ... )**:
   - Si la conversión a JSON es exitosa, se ejecuta esta función.
   - `data` contiene los datos obtenidos del servidor.
   - Aquí puedes procesar los datos como quieras, por ejemplo, mostrarlos en la página, almacenarlos, etc.

**.catch(error =>  ... )**:
   - Si ocurre algún error en el proceso, se ejecuta esta función.
   - `error` contiene información sobre el error.

![Demostración grafica de Get Request](https://www.aisangam.com/blog/wp-content/uploads/2019/10/HTTPRequestMessageFormat.png)