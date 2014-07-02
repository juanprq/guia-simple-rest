REST
====

introducción
------------

Rest es un protocolo para la representación del estado, se basa en una arquitectura cliente servidor sin estado basada
en un protocolo de comunicación cacheable, normalmente *HTTP*.

Empleado usualmente como un estilo arquitectónico para el diseño de aplicaciones que trabajan por medio de redes, con un
enfoque simple realizando llamados *HTTP* entre maquinas en vez de emplear protocolos complejos como CORBA, RCP o SOAP.

Las aplicaciones llamadas *RESTful* son aquellas emplean el protocolo *HTTP* para poner datos en el sistema o adquirirlos
operaciones tipicamente llamadas CRUD basandose en el concepto que se trata de representar, ya que de por si *REST* no es
un estandar.

Para que un systema sea *REST* dbe cumplir 6 restricciones, en caso de fallar una se dice que no es un sistema RESTful.
* Interface uniforme: La provee el protocolo *HTTP*, una forma clara de comunicarse con los servicios.
* Sin estado: El Servidor nunca debe mantener estado sobre el cliente, cada que el cliente manda un mensaje para ser
procesado, este debe contener la información necesaria para que siempre el servidor pueda procesarla sin tener que conocer
algo de antemano.
* Cacheable: cada uno de los recursos que se adquieren pueden ser cacheados, ya sea de manera implícita, explícita o 
negiociada entre el cliente y el servidor.
* Cliente - servidor: La arquitectura del sistema siempre debe ser cliente servidor.
* Sistema por capas: El cliente al mandar mensajes no siempre debe saber quien responde, en el caso del protocolo *HTTP*
es común que se responda un recurso cacheado, con lo cual se identifica el sistema por capas.
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
estado debe ser entre request (autocontenido).

Ejemplo simple de un servicio REST
----------------------------------

Un servicio *REST* puede ser fácilmente implementado sobre cualquier libería que funcione como servidor *HTTP*, es
importante conocer cada uno de los método del protocolo ya que estos nos determinan la acción que se está realizando, estas
acciones se realizan sobre recursos, por ello se emplea una *URL* que se encarca de especificar el recurso.

Los métodos *HTTP* son verbos que le indican al servidor una acción a realizar sobre el recurso especificado, para ello
el protocolo especifica el uso de los métodos de la siguiente manera:
* GET: acción para obtener un recurso, se emplea generalmente para obtener colecciones de entidades o para un recurso en
específico, ej: /clientes, /cliente/{id}
* PUT: acción para actualizar un recurso.
* post: acción para crear un recurso.
* delete: acción para eliminar un recurso.

Hay que tener en cuenta que normalmente los navegadores no soportan todos los métodos, por lo que normalmente se emplea 
el método post y por medio de campos enmascarados en el cuerpo de la petición se le indica al servidor que método se está
usando, muchos frameworks traen esta funcionalidad implementada y generalmente es transparente para el usuario.