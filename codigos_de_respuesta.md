Códigos de respuesta HTTP
=========================

1** Códigos de información
---------------------------

Son códigos de estatus que indican una respuesta provisional.

| Código              | Descripción                                                                                           |
|---------------------|-------------------------------------------------------------------------------------------------------|
| 100 (continue)      | El servidor ha recivido las cabeceras y el cliente debe mandar ahora el cuerpo del mensaje.           |
| 101 (switching protocols) | El servicio ha recivido una petición para cambiar de protocolo y el servidor está listo.        |
| 102 (processing)    | Cuando se tienen peticiones grandes que son divididas, el servidor responde este código para indicar que aún no tiene respuesta y está esperando por la secuencia de peticiones para finalizar. |

2** Códigos de Éxito
---------

Son códigos para indicar que la petición se ha resuelto con éxito.

| Código              | Descripción                                                                                           |
|---------------------|-------------------------------------------------------------------------------------------------------|
| 200 (ok)            | Respueta mas común en el protocolo http la cual indica que la operación realiazada ha finalizado con éxito. |
| 201 (created)       | Indica que la operación realizada ha creado con éxito un nuevo recurso.                                |
| 202 (accepted)      | La petición ha sido aceptada pero el procesamiento no se ha completado y puede tomar cierto tiempo.   |
| 203 (no-authoritative-information) | El servidor procesó la información pero puede estar respondiendo información de otra fuente. |
| 204 (no content)    | El proceso de la petición fue exitosa pero el cuerpo del mensaje viene vacio.                         |
| 205 (reset content) | Indica lo mismo que el código 204 pero esta vez le indica al cliente que limpie el documento que está mostrando. |
| 206 (partial content) | El servidor solo retornó cierta cantidad de información debido a la cabecera rango enviada por el cliente, usualmente empleada para descargar archivos por partes. |
| 207 (multi status)  | El cuerpo del siguiente mensaje está en formato *XML* con varios códigos de respuesta, dependiendo de cuantos sub-request se hayan hecho. |

3** Códigos de redirección
--------------------------

El cliente deberá tomar acciones una vez recibido un codigo de este tipo, probablemente sin interacción del usuario.

| Código              | Descripción                                                                                           |
|---------------------|-------------------------------------------------------------------------------------------------------|
| 300 (multiple choices) | Inidica mulples opciones del recurso de las cuales el cliente deberá elegir.                       |
| 301 (moved permanently) | Está y demás peticiones deberán ser dirigidas a la url especificada.                              |
| 303 (see other)     | La respuesta a la petición puede ser encontrada en la url indicada mediante un GET.                   |
| 304 (not modified)  | Indica que la versión del sercurso no ha sido modificada desde la información que llevan los headers, lo que significa que el recurso no debe ser retransimitido y el cliente puede usar la versión que ya tiene descargada de la última vez.               |
| 305 (use proxy)     | El recurso pedido solo es accesible mediante el uso de un proxy y la dirección de este fue enviada en el body. |

4** Códigos de error del cliente
--------------------------------

Estos código se responden en casos en los que el cliente se encuentra haciendo peticiones que tienen errores y el servidor no puede procesarlas.

| Código              | Descripción                                                                                           |
|---------------------|-------------------------------------------------------------------------------------------------------|
| 400 (bad request)   | La petición no puede ser completada debido a que no está correctamente formada.                       |
| 401 (unauthorized)  | Autenticación es necesaria para acceder al recurso.                                                   |
| 403 (forbidden)     | La petición fue válida pero el servidor se rehusa a responder.                                        |
| 404 (not found)     | El recurso pedido no fue encontrado en el servidor.                                                   |
| 405 (method not allowed) | La petición hecha al recurso no soporta la operación que se está realizando.                     |
| 406 (not acceptable) | El recurso pedido solo puede generarse en contenido que está descrito como contenido no aceptable en los headers. |
| 407 (proxy authentication required) | El cliente debe autenticarse primero ante el proxy.                                   |
| 408 (request timeout) | El servidor agotó el tiempo de espera para la petición.                                             |
| 409 (conflict)      | La petición no pude ser procesada debido a un conflicto, por ejemplo al realizar actualizaciones concurrentes. |
| 410 (gone)          | El recurso solicitado ya no esta disponible y nunca mas lo estará.                                    |
| 411 (length required) | La petición no especificó su tamaño y este es requerido para dar respuesta.                         |
| 412 (precondition failed) | El servidor encontró que la petición no cumple con las precondiciones establecidas.             |
| 413 (request entity too large) | La petición es mas larga de lo que el servidor está dispuesto a  procesar.                 |
| 414 (request uri too long) | La URI de la petición es muy larga para que el servidor pueda responder.                       |
| 415 (unsupported media type) | La entidad de petición tiene un media type que el servidor o el recurso no soporta.          |
| 416 (request range not satisfable) | El cliente ha pedido una porción de un archivo pero el servidor no puede responder esa porción. |
| 417 (expectation failed) | El servidor no puede cumplir los requisitos de la cabecera Expect.                               |
| 419 (authentication timeout) | Indica que la autenticación previamente hecha ha expirado.                                   |
| 422 (unprocessable entity) | La petición se encuentra bien formada pero no puede ser procesada debido a errores semánticos. |
| 423 (locked)        | El recurso que se está accediendo está bloqueado.                                                     |
| 424 (failed dependency) | La petición ha fallado debido a la falla de una petición anterior.                                |
| 426 (upgrade required) | El cliente debe pasar a un protocolo diferente.                                                    |
| 429 (too many request) | El cliente ha mandado muchas peiciones en un periodo de tiempo dado.                               |
| 431 (request header fields too large) | El servidor no está dispuesto a procesar la petición debido a que uno o mas header son demasiado largos. |
| 451 (unavailable for legal reasons) | Usado cuando el acceso a un recurso es negado por razones legales.                    |

5** Códigos de error del servidor
---------------------------------

Estos códigos son empleados cuando ha ocurrido un error interno en el servidor y la petición no puede ser procesada.

| Código              | Descripción                                                                                           |
|---------------------|-------------------------------------------------------------------------------------------------------|
| 500 (internal server error) | Mensaje de error genérico, cuando pasa algo inesperado en el servidor.                        |
| 501 (not implemented) | O el servidor no reconoce el método de la petición o es incapás de terminar la petición, usualmente es debido a que en el futuro se va a implementar. |
| 502 (bad gateway)   | El servidor está actuando como gateway o proxy y recivió una respuesá inválida del servidor.          |
| 503 (service unavailable) | El servidor no está disponible actualmente, generalmente es un estado temporal.                 |
| 504 (gateway timeout) | El servidor está actuando como gateway o proxy y no recivió respuesta del servidor en el tiempo establecido. |
| 505 (HTTP version not supported) | El servidor no soporta la versión de protocolo *HTTP* especificada en la petición.       |
| 507 (insufficient storage) | El servidor no puede encontrar el espacio necesario para poder procesar la petición.           |
| 508 (loop detected) | El servidor ha detectado un ciclo infinito mientras procesa la petición.                              |
| 511 (network authentication required) | El cliente necesita autenticarse para ganar acceso a la red.                        |