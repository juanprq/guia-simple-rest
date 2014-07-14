Guía Simple REST
================

introducción
------------

Rest es un protocolo para la representación del estado, se basa en una arquitectura cliente servidor sobre *HTTP* en donde se transfiere el estado en la comunicación por lo que se dice que el servidor no guarda el estado del cliente.

Empleado usualmente como un estilo arquitectónico para el diseño de aplicaciones que trabajan por medio de redes, con un
enfoque simple realizando llamados *HTTP* entre maquinas en vez de emplear protocolos complejos como CORBA, RCP o SOAP.

Las aplicaciones llamadas *RESTful* ponen y adquieren datos del sistema realizando operaciones (CRUD) sobre recursos.

Para que un sistema sea *REST* debe cumplir 6 restricciones, en caso de fallar una se dice que no es un sistema *RESTful*:

* Interface uniforme: La provee el protocolo *HTTP*, una forma clara de comunicarse con los servicios.
* Sin estado: El Servidor nunca debe mantener estado sobre el cliente, cada que el cliente manda un mensaje para ser
procesado, este debe contener la información necesaria para que siempre el servidor pueda procesarla sin tener que conocer
algo de antemano.
* Cacheable: cada uno de los recursos que se adquieren pueden ser cacheados, ya sea de manera implícita, explícita o 
negiociada.
* Cliente - servidor: Requisito básico en la arquitectura del sistema.
* Sistema por capas: El cliente al mandar mensajes no debe saber quien responde, en el caso del protocolo *HTTP*
es común que se responda un recurso cacheado.
* Código por demanda (Opcional): Cuando el servidor extiende el código del cliente para añadir funcionalidades, etc.

REST como servicios livianos
----------------------------

Como una alternativa a protocolo mas complejos, el enfoque *REST* puede ser empelado para la creación de servicios web
los cuales tienen ciertas características:

* Independiente de la plataforma (los servcios funcionan bajo linux, windows, etc...).
* Independiente del lenguaje (pueden ser implementados en muchos lenguaje de programación y a su vez interactuar entre ellos).
* Basados en estandar (*HTTP*).
* Pueden ser usados fácilmente en presencia de firewalls.

Como cualquier protocolo de servicios *REST* no ofrece ninguna caracterísica de seguridad, pero puede ser fácilmente
implementadas bajo el soporte de *HTTP*, la única característica del protocolo *HTTP* que no es una buena práctica en 
*REST* es el uso de cookies, ya que estas sirven para mantener el estado, pero la especificación de *REST* dice que el 
estado debe ser transferido en cada request (autocontenido).

Ejemplo simple de un servicio REST
----------------------------------

Un servicio *REST* puede ser fácilmente implementado sobre cualquier libería que funcione como servidor *HTTP*, es
importante conocer cada uno de los método del protocolo ya que estos nos determinan la acción que se está realizando, estas
acciones se realizan sobre recursos, por ello se emplea una *URI* que se encarga de especificarlo.

Los métodos *HTTP* son verbos que le indican al servidor una acción a realizar sobre el recurso especificado, para ello
el protocolo describe el uso de estos métodos de la siguiente manera:

* GET: acción para obtener un recurso (colecciones de entidades o una sola), ej: /clientes, /cliente/{id}
* PUT: acción para actualizar un recurso.
* POST: acción para crear un recurso.
* DELETE: acción para eliminar un recurso.

Hay que tener en cuenta que normalmente los navegadores no soportan todos los métodos, por lo que normalmente se emplea 
el método post y por medio de campos enmascarados en el cuerpo de la petición se le indica al servidor que método se está
usando, muchos frameworks traen esta funcionalidad implementada y generalmente es transparente para el usuario.

Tips para la implementación de un API *REST*
--------------------------------------------

### Emplear los verbos *HTTP* para que sean significativos

Al implementar los servicios tener en cuenta el bueno uso de cada uno de los verbos *HTTP* dandole un significado lógico
sobre la operación que se está realizando, por ejemplo, si estamos empleando el verbo *GET* es importante tener en cuenta
que el servicio no debe modificar ningun recurso en el servidor y por su significado deberá acceder al recurso especificado.

### Emplear nombres de recursos acertados

Gran parte del esfuerzo de diseñar una buena API está en buscar o acomodar de la mejor manera posible los recursos para
que los nombres sean significativos y se haga buen uso de una jerarquía y en la menor medida ser repetitivos; estos
deberán ser nombrados en lo posible para que cualquier persona lea (lenguaje natural) y entienda cual es el recurso sobre el que se realiza
la operación, ejemplos:

* Emplear identificadores en vez de parámetros de consulta por cadenas: /usuarios/3123 en vez de /api?tipo=usuario&id=3123.
* Diseñar una buena jerarquía de recursos: /usuarios/3123/roles.
* Diseñar pensando en como los clientes van a usar la información mas no en como es la información.
* No emplear verbos en la URIs, solo usar sustantivos.
* Emplear sustantivos plurales en la composición de URIs, ya que esto ayuda a mantener la consistencia entre servicios: 
/customers/33245/orders/8769/lineitems/1 en vez de /customer/33245/order/8769/lineitem/1.
* Evitar el uso de palabras que especifiquen que el recurso es una colección, para ello emplear sustantivos plurales:
usuarios en vez de usuario_list.
* Emplear siempre minúsculas en las URIs y separar las palabras con '-' o '_' (emplear el mismo caracter para todo el diseño).
* Mantener las URLs lo mas pequeñas y descriptivas posibles con la menor cantidad de segmentos mientras tenga sentido.

### Emplear los códigos de respuesta *HTTP* para indicar el estatus

Estos códigos sirven para dar una respuesta a la petición indicando al cliente que ha pasado con esta, para ello es importante conocer el significado de lo códigos mas comunes.

* 200 ok: estatus general, empleado normalmente para decir que todo salió bien.
* 201 created: indica que la creación del recurso fué exitosa via POST o PUT, se envia el header Location para indicar donde quedó el recurso, el cuerpo del mensaje puede o no tener contenido.
* 204 no content: Indica éxito pero que no hay nada en el cuerpo del mensaje, normalmente se usa en operaciones de actualización o eliminación.
* 400 bad request: error general que indica que el request no fué procesado debido a un estado inválido, validaciónes del dominio, faltan datos, etc.
* 401 unauthorized: código de error que se emplea cuando el token de autenticación del usuario es inválido o no está.
* 403 forbidden: código de error que se emplea cuando un usuario no autorizado trata de realizar una acción sobre un recurso el cual no es alcanzable por alguna razón.
* 404 not found: código de error que se emplea cuando el recurso que se está intentando obtener no existe.
* 405 method no allowed: Se emplea cuando la URL si pertenece a un recurso pero el método que se está empleando no es válido.
* 409 conflict: es la respuesta a un conflicto al procesar la petición, ya que se está creando un recurso duplicado o eliminar entidades en cascada cuando no es posible.
* 500 internal server error: nunca retornar este código a propósito, error común del servidor cuando algo inesperado ha pasado.

### Ofrecer *JSON* y *XML*

Por ser un formato mucho mas simple generalmente se favorece el soporte hacia *JSON*, en caso que se requiera explicitamente un soporte hacia *XML* la implementación de este no es estrictamente necesaria, ya que en el momento de empezar a construir respuestas en este formato se empieza a hablar de esquemas y validaciones; siempre y cuando sea posible, ofrecer la implementación en los 2 formatos, construir un *JSON* y hacer que el *XML* se parezca a este, y espcificando en el servicio .xml o .json retornar el formato especificado; tener en cuenta que hoy en día es muy raro ver APIs que usen formato *XML* ya que es mas costoso su consumo.

### Creación de servicios pequeños y puntuales

Cuando se inicia el diseño e implementación de una API es mejor empezar realizando servicios que cumplan operaciones sobre recursos pequeños como el modelo de dominio en si, esto es debido a que es mas fácil crear luego sobre estos servicios otros que sean mas complejos y realicen operaciones mas intricados y no empezar por servicios grandes que no se puedan descomponer en otros mas pequeños después.

### Consideración de la conectividad

Para el diseño de servicios que sean mas descriptivos se recomienda el uso de vínculos; es aconsejable que cuando un servicio retorne una respuesta incluya en los headers vinculos, siempre y cuando estos tengan un significado para el servicio, por ejemplo, si un recurso acaba de ser creado, en el header Location poner la URI o el vinculo del recurso, si es una colección, indicar en los headers cual es la primera página, última, siguiente y anterior, para ello se puede usar la cabecera Link como se recomienda en la especificación o alguna representación *JSON* (hay varias especificaciones para ello).

Manejo de recursos
------------------

El manejo típico de recursos para operaciones *CRUD* se puede realizar de la siguiente manera (suponiendo que estamos realizando las operaciones sobre el recurso *usuario*):

* Para obtener la colección de recursos: GET http://example.com/users
* Para insertar un nuevo registro: POST http://example.com/users
* Para obtener un recurso: GET http://example.com/users/{id}
* Para actualizar un recurso: PUT http://example.com/users/{id}
* Para eliminar un recurso: DELETE http://example.com/users/{id}

Para un diseño un poco mas complejo donde se tienen recursos que pertenecen o tienen relaciones con otros recursos, se emplea la jerarquia para darle un significado, en este caso suponer que un usuario puede realizar ordenes (por lo tanto la entidad usuario tiene un listado de ordenes asociadas):

* Para obtener las ordenes de un usuario en específico: GET http://example.com/users/{userId}/orders
* Para crear una orden a un usuario en espcífico: POST http://example.com.users/{userId}/orders
* Para obtener una orden específica de un usuario: GET http://example.com/users/{userId}/orders/{orderId}
* Para actualizar una orden en específico: PUT http://example.com/users/{userId}/orders/{orderId}
* Para eliminar la orden específica de un usuario: DELETE http://example.com/users/{userId}/orders/{orderId}

Ejemplos de como se deben emplear los métodos sobre un recurso y lo que responde el servicio ante las diferentes situaciones:

| Método | Colección (/usuarios) | Recurso específico (/usuarios/{id}) |
|--------|-----------------------|-------------------------------------|
| GET    | 200 (Ok), Lista de usuarios, usar paginación, ordenamiento y filtrado para navegar por listas grandes. | 200 (Ok), Usuario específico. 404 (Not Dound) si el id no existe o es inválido. |
| PUT    | 404 (Not Found), a menos que se quiera implementar un servicio que actualize o reemplace toda la colección. | 200 (Ok) o 204 (Not Content). 404 (Not Found), si el identificador no es válido o no existe. |
| POST   | 201 (Created). Usar el header Location con el vinculo donde quedó creado el nuevo recurso (/usuarios/{id}). | 404 (Not Found). |
| DELETE | 404 (Not Found), a menos que se quiera implementar un servicio que elimine toda la colección. | 200 (Ok). 404 (Not Found), en caso de ser un identificador inválido o no existir. |

Idempotencia
------------

Se dice que la idempotencia es la propiedad que tiene algo para realizar la misma operación varias veces obteniendo siempre el mismo resultado, para ello *REST* tiene un enfoque y es que toda acción que no sea idempotente debe ser realiazada con el método *POST*, por ejemplo siempre que realizemos una acción *GET* siempre se obtiene la misma representación del recurso, si se realiza una actualización de un recurso con el método *PUT* siempre se obtiene el mismo código de estatus, con *DELETE* es mas complejo pero se supone que debe pasar igual, para la ejecución de la acción se debe tener el mismo resultado, pero cuando se realiza un método *POST* el recurso se crea pero si se vuelve a realiza la acción la respuesta es diferente ya que el recurso es diferente o la creación de un duplicado no es posible.

Recursos
--------

Este documento guía fue basado en los siguientes recursos:

* [REST API Tutorial.](http://www.restapitutorial.com/)
* [Learn REST: A Tutorial.](http://rest.elkstein.org/)