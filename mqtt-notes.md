MQTT es un protocolo de mesajeria dedicada para el Internet de las Cosas (IoT). Es esta diseñado como  un transporte de mensajerrica por **publish/subscribe ligero** que es ideal para conectar dispositivos remotos con:

1. Poco *code footprint* (Poco tamaño de mensaje). 
2. Con un minimo ancho de banda.

> MQTT significa *MQ Telemetry Transport*.

**MQTT** es usado en muchas aplicaciones de la industria, manufactura, telecomunicaciones entre otras.

## Ventajas de MQTT

- Ligero y Eficiente
- Comunicaciones Bidireccionales: Dispositivo a la nube y de la nube al dispositivo.
- Escalable a cientos de cosas
- Mensajeria Segura
- Soporte para Redes que no tienen confiabilidad
- Permite seguridad (Encriptación).

## Arquitectura Publish/Subcribe de MQTT

El modelo **Pub/Sub** de MQTT, un nodo puede subscribirse a un canal para recibir cierta información y puedo publicar en este canal.

El protocolo MQTT corre encima del protocolo TCP/IP. Otro procolo que utiliza el pub/sub es el websockets y es una comunicación full-duplex, y esta coneción se realice por medio de handshake.

![](2022-10-06-21-16-38.png)

Este protocolo es un conjunto de reglas que definen como los dispositivos pueden publicar y subscribirse a los datos sobre el internet. Este procolo es un **conductor de eventos** y conecta dispositivos que usan patrones de Pub/Sub.

La emisor (Publisher) y el recepetor (Subscriber) se comunican via **topics** (topicos) y son desacoplados de cada otro.

La conexión entre ellos es resuelta por un **MQTT broker**, este filtrara todos los mensajes y los distribuira correctamente a los subscriptores.

**Basic Concepts**
1. publish/subscribe
2. client/broker

**Basic Functionality**
1. Connect
2. Publish
3. Subscribe

**Feactures**
1. Quality of Service
2. Retained Messages
3. Persistent Session
4. Last Will and Testament
5. Keep Alive
6. MQTT over WebSockets

## Introducción
> MQTT es un protocolo de transporte de mensajes basado en Pub/Sub, viales para comunicaciones M2M (Machine to Machine) y IoT (Internet de las Cosas) donde se necesite:

- Poco codigo *footprint*
- Ancho de Banda Limitado

[Documentación Oficial](https://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.html)

- Otra caracteristica que tiene MQTT es que es un **protocolo binario**, debido a que tiene una minima sobrecarga de paquetes, por lo que es ideal para la transferencia de datos sobre el cable en comparación al protocolo HTTP. 

- MQTT es facil de implementar del lado del cliente, y su construcción sobre dispositivos con recursos limitados.

### Un poco de historia
Inventado en el 99' por IBMY y Arcom, se desarrollo para comunicaciones con baja costo de bateria y ancho de banda limitado, este se usaba para conectar oleoductos via satelite. Con el tiempo el propietario del protocolo lo puso abierto para el uso de aplicaciones IoT. *MQ* se refiere a la serie MQ de productoss de IBM. 
En el 2010 IBM libera la version MQTT 3.

### Patron Pub/Sub de MQTT
El patron de MQTT Publish/Subscribe provee una alternativa para la arquitectura tradicional cliente-servidor. En el modelo cliente-servidor, un cliente se comunica directamente con un endpoint. Mientras que **el modelo pub/sub desacopla al cliente que envia un mensaje (el publicador) de el cliente o los clientes que reciben los mensajes (los subscriptores)**. Asi el publicador y el subscriptor nunca tienen contacto, inclusive ellos se pueden encontrar en diferentes existencias. **La coneccion entre ellos es resuelta por un tercer componente llamado broker**. 
El trabajo del **broker** es la  **filtración de todos los mensajes  entrantes** y **distribuirlos** entre ellos.

![](2022-10-08-09-18-13.png)

Se recuerda que **el aspecto mas importante es el desacople del publicador del mensaje y el subscriptor**. 

El desacople de las dimensiones tiene que ser:

- **Desacople en espacio**: Publicador y subcriptor no necesitan concerce entre ellos (por ejemplo, no intercambian IP o puerto).
- **Desacople de tiempo**: El Publicador y el subscriptor no necesita correr en el mismo tiempo.
- **Desacople por sincronización**: Las operaciones sobre ambos componentes no necesitan ser interrumpidos durante la publicanción y la recepción.

#### Resumen
En resumen, la **Arquitectura o modelo MQTT pub/sub** elimina la comunicación directa entre el publicador de el mensaje y el receptor/subcriptor. **La actividad de filtración de el broker** que  esto sea posible, a traves del control de mensajes que se envian a los cliente/subscriptor. Y el desacople tiene tres dimensiones: en espacio, tiempo y sincronización.

### Escalabilidad
De acuerdo con [hivemq.com](https://www.hivemq.com/blog/mqtt-essentials-part2-publish-subscribe/), MQTT tiene una mejor escalabilidad que el clasico protocolo cliente-servidor, debido a que las operaciones sobre el broker puede ser realizada paralelamente y los mensajes puede ser procesador en un camino  *event-driven*.

El *atrapado/catching* de mensajes y la inteligencia de enrutamiento de los mensajes son generalmente uno de los factores de incremento en la escalabilidad. Sin embargo, escalarlo a millones de conecciones es un verdadero reto. Ya que en un alto nivel de conecciones puede ser logradas a traves de la clusterizacion de nodos del broker para distribuir la carga de trabajo a mas servidores individuale, y de esta manera usar balanceadores de carga. 

## Filtrado de Mensajes
Las siguientes opciones de filtrado tiene un broker:

### Opcion 1: *SUBJECT BASED FILTERING*
Este es un filtrado basado en el *subject*/tema/topico que es parte de cada mensaje. Y el cliente se subscribira al broker unicamente a los topicos de interes.
De cualquier punto que se encuentre encendido, el broker asegura que el ciente obtenga todos los mensajes publicados al llamado **subscribed topics**.

En general, los topics son cadenas de textos con una estructura jerarquica que permita filtrado sobre un numero limitado de expresiones.

### Opcion 2: *CONTENT-BASED FILTERING*

En este filtrado, el broker filtrara los mensajes basados sobre un contenido especifico (filter-language). Lo recibido por los cientes esta subscrito a una **consulta filtrada** (filter queries) de mensajes para los cuales se este interesado. 
Este contenido debe conecerse con antelación y no puede cifrarse, ni cambiarse facilmente.
### Opcion 3: *TYPE-BASED FILTERING*
Cuando se usa lenguajes con paradigma OOP, el filtrado puede ser basado sobre los tipos/clases de un mensaje, esta es una practica comun. 

Por ejemplo, un subscriptor puede listar todos los mensajes los cuales son de `type Exception` o algun `sub-type`.

Claro, que el pub/sub no es la respuesta para todos los casos de uso, existen casos exclusivos en los cuales se deben considerar para utilizar este modelo. 

El desacoplemiento del *publisher* y el *suscriber* es la clave de pub/sub, pero presenta un pequeño reto. Este reto puede ser explicado debido a que ambos deben conocer los topicos que es van a usar. Otra cuestión seria que el publicador puede que publique temas, y puede que no exista ningun subscriptor leyendo. 

### Caracteriticas Clave del MQTT

Como se menciono antes tenemos:
1. El desacople por espacio del *publisher* y el *subscriber*. Para publicar o recibir un mensaje, los *publishers* y *suscribers* unicamente necesitan saber **el hostname/IP y el puerto del broker**.
2. El desacople por tiempo, a pesar que MQTT puede lograr entregar mensajes en tiempos cercanos al tiempo real, si deseamos, **el broker puede almacenar mensajes para los clientes que no se encuentran online**.

Y son dos condiciones para almacenar mensajes: El cliente tiene que conectarse con una **sesión persistente** y **suscribirse a un topico** con una calidad de servicio (QoS) mucho mayor a cero.

3. El MQTT trabaja asincronamente, debido a que la mayoria de librerias de clientes funcionan asincronamente y estan basados en `callbacks` o algun modelo similar, las tareas no se bloquean mientras esperan por un mensaje o publicación de algun mensaje.

En ciertos casos de uso, la sincronia es posible y deseable, para esperar por un cierto mesaje, algunas librerías tiene APIs sincronas, pero el flujo usualmente es asincrono.

Como se dijo antes, es que MQTT es relativamente mas facil utilizar de **lado del cliente**. Los sistemas pub/sub tienen la lógica sobre el **lado del broker**.

**MQTT usa el filtrado basado en subject de los mensajes**, cada mensaje contiene un *subject* que el broker puede usar para determinar lo que el cliente desea de su subcripción.