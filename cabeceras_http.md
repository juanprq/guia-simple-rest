Listado de las distintas cabeceras del protocolo HTTP
=====================================================

La cabeceras en el protocolo *HTTP* son parámetros adicionales al cuerpo del mensaje que especifican comportamientos operacionales sobre la transacción; para cada cabecera existe una llave única que es previamente conocida (header name) y un valor para esta.

Cabeceras para peticiones
-------------------------

Cabeceras que son empleadas únicamente cuando el cliente realiza una petición al servidor.

| Nombre o llave de la cabecera | Descripción                                                                                                 |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Accept                        | Content-types que son aceptables para la respuesta a esta petición. (ej. text/plain)                        |
| Accept-Charset                | Juego de caracteres que son aceptables para la respuesta a esta petición. (ej. utf-8)                       |
| Accept-Encoding               | Listado de encodings aceptables para la respuesta a está petición. (ej. gzip, deflate)                      |
| Accept-Language               | Listado de lenguajes humanos para dar respuesta a está petición. (ej. en-US)                                |
| Accept-Datetime               | Versión aceptable de formato de fecha.                                                                      |
| Authorization                 | Credenciales de autenticación *HTTP*.                                                                       |
| Cache-Control                 | Empleada para especificar directivas que deben ser cumplidas por todos los mecanismos de caching.           |
| Connection                    | Que tipo de conexión el cliente prefiere. (ej. keep-alive)                                                  |
| Cookie                        | Valor de una *cookie* que ha sido previamente establecida por el servidor.                                  |
| Content-Length                | El tamaño del cuerpo de la petición en octetos (bytes).                                                     |
| Content-MD5                   | La codificación binaria *MD5* del cuerpo de la petición.                                                    |
| Content-Type                  | El *MIME-type* del cuerpo del mensaje de está petición (usada para peticiones *POST* y *PUT*).              |
| Date                          | La fecha y hora en que este mensaje fue enviado.                                                            |
| Expect                        | Indica algún comportamiento en particular del servidor que requiere el cliente. (ej. 100-continue)          |
| From                          | El correo electrónico del usuario que está realizando la petición.                                          |
| Host                          | El nombre de dominio del servidor y el puerto donde este está escuchando a peticiones entrantes.            |
| If-Match                      | Solo realizar la acción si la entidad que provee el cliente concuerda con la entidad del servidor.          |
| If-Modified-Since             | Le indica al servidor que puede responder un 304 si el contenido no ha cambiado.                            |
| If-None-Match                 | Le indica al servidor que puede responder un 304 si el contenido no ha cambiado.                            |
| If-Range                      | Si la entidad no ha cambiado, enviar partes que el cliente no tiene, de lo contrario volver a enviar la entidad. |
| If-Unmodified-Since           | Solo enviar la respuesta si la entidad no ha sido modificada desde la fecha indicada.                       |
| Max-Forwards                  | Limita el número de veces que el mensaje puede ser retransmitido a través de proxys o gateways.             |
| Origin                        | Inicia una petición *cross-origin*.                                                                         |
| Proxy-Authorization           | Credenciales de autenticación para conectarse al proxy.                                                     |
| Range                         | Petición solo por la parte de una entidad.                                                                  |
| Referer                       | Es la dirección de la página anterior de donde el vinculo fue referido.                                     |
| TE                            | La codificación de transferencia que el cliente esta dispuesto a aceptar.                                   |
| User-Agent                    | Nombre y versión del software que está realizando la petición.                                              |
| Upgrade                       | Pregunta al servidor para cambiar a otro protocolo.                                                         |
| Via                           | Informa al servidor de proxys por los cuales la petición fue enviada.                                       |
| Warning                       | Una advertencia general indicando posibles problemas con el cuerpo de petición.                             |

Cabeceras para respuestas
-------------------------

Cabeceras que son empleadas únicamente en la respuesta que da el servidor al cliente.

| Nombre o llave de la cabecera | Descripción                                                                                                 |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Access-Control-Allow-Origin   | Especifica que sitios web pueden participar de una petición *cross-origin resource sharing*.                |
| Accept-Ranges                 | Que tipo de contenido parcial el servidor puede aceptar. (ej. bytes)                                        |
| Age                           | La edad del objeto que ha estado en proxy-cache en segundos.                                                |
| Allow                         | Acciones válidas para un recurso en específico.                                                             |
| Cache-Control                 | Le indica al cliente los mecanismos de cacheo que se pueden realizar sobre el objeto.                       |
| Connection                    | Opciones que son deseadas para la conexión.                                                                 |
| Content-Encoding              | El tipo de codificación usado en los datos. (ej. GZIP)                                                      |
| Content-Language              | El lenguaje en el que está el contenido de la respuesta. (EN-us)                                            |
| Content-Length                | El tamaño del contenido en octetos (bytes).                                                                 |
| Content-location              | Locación alternativa para los datos que fueron retornados.                                                  |
| Content-MD5                   | Codificación binaria del contenido de la respuesta.                                                         |
| Content-Disposition           | Da una oportunidad de lanzar un dialogo para descargar un archivo para un *MIME-type* de formato binario.   |
| Content-Range                 | Rango indicando donde pertenece la respuesta en relación a un documento completo.                           |
| Content-Type                  | El *MIME-Type* del contenido de esta respuesta.                                                             |
| Date                          | Fecha y hora del mensaje en la cual está respuesta fue hecha.                                               |
| ETag                          | Un identificador para una versión en específico de un recurso.                                              |
| Expires                       | Da una fecha y hora en donde se considera que la respuesta estará vieja.                                    |
| Last-Modified                 | Indica la fecha y hora donde fue modificado por última vez el recurso.                                      |
| Link                          | Empleado para expresar la relación que existe con otro recurso.                                             |
| Location                      | Usado para realizar redirecciones o cuando un nuevo recurso es creado.                                      |
| Proxy-Authenticate            | Petición para autenticarse para el acceso al proxy.                                                         |
| Refresh                       | Empleado en una redirección o cuando un recurso ha sido o no creado.                                        |
| Retry-After                   | Si un recurso es temporalmente inalcanzable, está instrucción le indica al cliente que vuelva a intentar en un tiempo o una fecha y hora dada. |
| Server                        | El nombre (Software) del servidor.                                                                          |
| Set-Cookie                    | Pone una cookie en el cliente.                                                                              |
| Status                        | El código de estatus de la respuesta.                                                                       |
| Strict-Transport-Security     | Política que informa al cliente cuanto cachear *HTTPS* y si aplica para subdominios.                        |
| Transfer-Encoding             | La forma de codificación para transferir de manera segura la entidad al usuario.                            |
| Upgrade                       | Pregunta al cliente para cambiar a otro protocolo.                                                          |
| Vary                          | Le dice a los proxys de descargas en como comparar headers de peticiones para decidir si responde el recurso cacheado o no. |
| Via                           | Informa al cliente los proxys donde la respuesta pasó.                                                      |
| Warning                       | Una advertencia general informando sobre posibles problemas con la entidad.                                 |
| WWW.authenticate              | Indica el esquema de autenticación que debe ser empleado para acceder a este recurso.                       |
| X-Frame-Options               | Política de protección para negar el renderizado de frames si no provienen del mismo origen.                |