REST
====

introducción
------------

Rest es un protocolo para la representación del estado, se basa en una arquitectura cliente servidor sin estado basada
en un protocolo de comunicación cacheable, normalmente *HTTP*.

Empleado usualmente como un estilo arquitectónico para el diseño de aplicaciones que trabajan por medio de redes, con un
enfoque simple realizando llamados *HTTP* entre maquinas en vez de emplear protocolos complejos como CORBA, RCP o SOAP.

Las aplicaciones llamadas *RESTful* ponen y adquieren datos del sistema realizando operaciones (CRUD) sobre recursos.

Para que un systema sea *REST* debe cumplir 6 restricciones, en caso de fallar una se dice que no es un sistema RESTful:

* Interface uniforme: La provee el protocolo *HTTP*, una forma clara de comunicarse con los servicios.
* Sin estado: El Servidor nunca debe mantener estado sobre el cliente, cada que el cliente manda un mensaje para ser
procesado, este debe contener la información necesaria para que siempre el servidor pueda procesarla sin tener que conocer
algo de antemano.
* Cacheable: cada uno de los recursos que se adquieren pueden ser cacheados, ya sea de manera implícita, explícita o 
negiociada entre el cliente y el servidor.
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
acciones se realizan sobre recursos, por ello se emplea una *URLURI* que se encarga de especificarlo.

Los métodos *HTTP* son verbos que le indican al servidor una acción a realizar sobre el recurso especificado, para ello
el protocolo especifica el uso de los métodos de la siguiente manera:

* GET: acción para obtener un recurso (colecciones de entidades o una sola), ej: /clientes, /cliente/{id}
* PUT: acción para actualizar un recurso.
* POST: acción para crear un recurso.
* DELETE: acción para eliminar un recurso.

Hay que tener en cuenta que normalmente los navegadores no soportan todos los métodos, por lo que normalmente se emplea 
el método post y por medio de campos enmascarados en el cuerpo de la petición se le indica al servidor que método se está
usando, muchos frameworks traen esta funcionalidad implementada y generalmente es transparente para el usuario.

Tips para la implementación de un API *REST*
--------------------------------------------

### Emplear los verbos *HTTP* para que tengan un significado

Al implementar los servicios tener en cuenta el bueno uso de cada uno de los verbos *HTTP* dandole un significado lógico
sobre la operación que se está realizando, por ejemplo, si estamos empleando el verbo *GET* es importante tener en cuenta
que el servicio no debe modificar ningun recurso en el servidor y por su significado deberá acceder al recurso especificado.

### Emplear nombres de recursos acertados

Gran parte del esfuerzo de diseñar una buena API está en buscar o acomodar de la mejor manera posible los recursos para
que los nombres sean significativos, se haga buen uso de una jerarquía y en la menos medida que sean repetitivos; estos
deberán ser nombrados en lo posible para que cualquier persona lea y entienda cual es el recurso sobre el que se realiza
la operación, ejemplos:

* Emplear identificadores en vez de parámetros de consulta por cadenas: /usuarios/3123 en vez de /api?tipo=usuario&id=3123.
* Diseñar una buena jerarquía de recursos: /usuarios/3123/roles.
* Diseñar pensando en como los clientes van a usar la información mas no en como es su información.
* No emplear verbos en la URIs, solo usar sustentivos.
* Emplear sustantivos plurales en la composición de URIs, ya que esto ayuda a mantener la consistencia entre servicios: 
/customers/33245/orders/8769/lineitems/1 en vez de /customer/33245/order/8769/lineitem/1.
* Evitar el uso de palabras que especifiquen que el recurso es una colección, para ello emplear sustantivos plurales:
usuarios en vez de usuario_list.
* Emplear siempre minúsculas en las URIs y separar las palabras con "-" o "_" (emplear el mismo caracter para todo el diseño).
* Mantener las URLs lo mas pequeñas y descriptivas posibles con la menor cantidad de segmentos mientras tenga sentido.

### Emplear los códigos de respuesta *HTTP* para indicar el estatus

