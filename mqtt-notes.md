MQTT es un protocolo de mesajeria dedicada para el Internet de las Cosas (IoT). Es esta diseñado como  un transporte de mensajerrica por **publish/subscribe ligero** que es ideal para conectar dispositivos remotos con:

1. Poco *code footprint* (Poco tamaño de mensaje). 
2. Con un minimo ancho de banda.

> MQTT significa *Message Queuing Telemetry Transport*, algo asi como Transporte Telemetrico de cola de mensajes.

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

