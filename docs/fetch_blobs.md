# Fetch de Blobs


### ¿Qué es un Blob?

Un Blob (Binary Large Object) es un tipo de objeto en JavaScript que representa datos binarios, como archivos (imágenes, audio, video, etc.) o cualquier tipo de datos binarios.

### Fetch y Blob

Cuando hablamos de "fetch de Blob", nos referimos a utilizar la API Fetch para obtener un Blob como respuesta a una petición HTTP. Esto es especialmente útil cuando queremos descargar archivos, imágenes o cualquier otro tipo de recurso binario directamente desde un servidor.

### Concepto

El concepto detrás de **fetch de Blob** es bastante sencillo: en lugar de convertir la respuesta de una petición HTTP directamente a texto o JSON, la convertimos a un Blob. Esto nos permite manipular los datos binarios directamente, como por ejemplo:

- **Crear URLs de objetos**: Podemos crear una URL a partir de un Blob y usarla en etiquetas `<img>`, `<audio>`, `<video>`, etc. para mostrar el contenido.
- **Guardar archivos**: Podemos permitir a los usuarios descargar el Blob como un archivo local.
- **Procesar imágenes**: Podemos utilizar el Blob como entrada para librerías de procesamiento de imágenes.

### Sintaxis

La sintaxis para obtener un Blob utilizando Fetch es muy similar a la de obtener texto o JSON, pero en lugar de usar los métodos `text()` o `json()`, utilizamos el método `blob()`:

```javascript
fetch('https://example.com/imagen.jpg')
  .then(response => response.blob())
  .then(blob => {
    // Hacemos algo con el Blob, por ejemplo:
    const url = URL.createObjectURL(blob);
    const img = document.createElement('img');
    img.src = url;
    document.body.appendChild(img);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```
### Explicación:
**1.	`fetch('https://example.com/imagen.jpg')`**: Hace una petición a la URL especificada.

**2.	`response.blob()`**: Convierte la respuesta a un Blob.

**3.	`URL.createObjectURL(blob)`**: Crea una URL temporal para el Blob.

**4.	`img.src = url`**: Asigna la URL al atributo src de una etiqueta `<img>`.
