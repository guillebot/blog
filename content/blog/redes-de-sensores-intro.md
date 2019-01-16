---
title: "Introducción redes de Sensores"
date: 2019-01-10T12:52:36+06:00
image: images/blog/blog-post-1.jpg
author: Guillermo
---

## Intro (de la intro)

Si te interesa como a mi la tecnología y te gusta el [diy](https://en.wikipedia.org/wiki/Do_it_yourself), tarde o temprano vas a ver que todos están conectando cosas, midiendo parámetros de su entorno, y eventualmente analizando esos datos o hasta controlando cosas a partir de los mismos.

Bienvenido al mundo de las [Redes de Sensores](https://es.wikipedia.org/wiki/Red_de_sensores). Salvo contadas excepciones, en nuestro caso estas redes van a ser inalámbricas, por lo menos el último tramo hasta los sensores o actuadores.

Te ponés a googlear un poco y el abanico es infinito. ¿Por dónde arranco?

Acá abajo te voy a contar el proceso que me fue llevando hasta el combo que por el momento me funciona y me parece sostenible en varios aspectos. Yo busco soluciones:

1. Que tengan continuidad en el tiempo, con comunidades activas y participativas. Cualquiera sea la solución elegida, tiene su curva de aprendizaje que normalmente es compleja. Dado que el tiempo es escaso no me interesa gastarlo en plataformas que tengan muchas chances de discontinuarse de un momento a otro.

2. Abiertas, gratis y opensource e incluso me permitan desarrollar proyectos comerciales.

3. Escalables en volumen, desde uno hasta miles de sensores. Después de todo cuando uno tiene el interés por medir, lo quiere medir todo.

4. Baratas. No me sirven soluciones de USD25 por nodo. El nodo completo debe ser sub USD10, lo que me deja como máximo USD 1 o USD 2 para las comunicaciones.


En resumen, lo que estoy usando es [esto](https://guillebot.github.io/blog/resumen-plataforma/). En este artículo vamos a ir desde abajo hacia arriba en cada item.

### Nodos

Lo primero es tener algo in situ para poder conectarle sensores y medir cosas. Acá lo que buscamos es un pequeño microcontrolador, fácil de conectar, fácil de programar, barato y con muchas entradas y salidas. Es deseable también que tenga bajo consumo de energía, para permitirnos nodos alimentados a batería.

Hay muchas opciones en el mercado, las que mas se escuchan son: [Arduino](https://www.arduino.cc/), [Teensy](https://www.pjrc.com/teensy/), [STM32](https://en.wikipedia.org/wiki/STM32), [PIC](https://en.wikipedia.org/wiki/PIC_microcontrollers), y ultimamente las que traen incluido el módulo de WiFi, como [ESP8266](https://www.espressif.com/en/products/hardware/esp8266ex/overview) y el mucho mas moderno y potente [ESP32](https://www.espressif.com/en/products/hardware/esp32/overview).

Buscando sobre todo precio, disponibilidad y comunidad, yo me inclino por la plataforma Arduino. Mas adelante voy a mostrar algunos experimentos con ESP8266 y ESP32, pero dado que WiFi no es mi primera opción en términos de networking no les estoy dando tanta importancia.

En mi caso al pensar en redes de sensores busco funcionalidad mínima en el borde y concentrar la inteligencia y procesamiento en un controlador (mas de esto abajo). Hay otros casos de uso donde se necesita procesar con mas potencia en origen y ahí son muy potentes las soluciones de 32 bits del STM32.

### ¿Qué es el famoso Arduino?

Por el lado del hardware son pequeñas placas con un microcontrolador Atmel, que ya vienen completas y listas para usar, como Arduino [Nano](https://www.arduino.cc/en/Guide/ArduinoNano) o Arduino [Uno](https://store.arduino.cc/usa/arduino-uno-rev3). Lo mas importante es todo el entorno que tienen, Arduino IDE y una gran cantidad de ejemplos. Los programas de arduino se llaman *sketches*.

A mi de la plataforma Arduino me gusta la comunidad, y que es muy fácil pasar de una placa "comprada" a un circuito propio, migrando sólo el microcontrolador Atmel 328p y 4 componentes discretos. [Ejemplo](https://www.arduino.cc/en/Tutorial/ArduinoToBreadboard).

Esto a veces conviene y a veces no, según el caso, pero es muy práctico desde el punto de vista de la manufactura masiva y económica, de la reducción de tamaños y costos y de la baja en consumo de energía.

Normalmente el camino pasa por desarrollar en protoboard, usando por ejemplo un Arduino Nano, y luego si funciona y queremos escalar el diseño para bajar costos y producir en volumen, se va despojando de todo lo innecesario hasta llevarlo a su mínima expresión. Si es sólo para pocas unidades o para prototipos, se deja el arduino completo. Tengo varios casos de Arduinos Nano en posiciones definitivas midiendo temperatura, altura de tanque de agua, humedad, etc.

## Sensores

Afortunadamente hay multitud de sensores para medir prácticamente todo lo que se nos ocurra. Podemos comenzar con los mas clásicos como Temperatura, Humedad Relativa o Presión Atmosférica para pasar luego a detecciones de gases, partículas, movimiento, etc.

## Conectividad

Quizás el punto mas importante de las redes de sensores es como conectar todos los dispositivos.

### Hardware

Si bien a esta altura el candidato natural parece ser WiFi, en la práctica yo me encontré con algunos inconvenientes que me llevaron a evaluar otras opciones:

1. Consumo de energía. WiFi consume en el orden de los cientos de mA. Esto para dispositivos conectados a 220V no es un inconveniente pero deja fuera la posibilidad de tener dispositivos alimentados exclusivamente a baterias.

2. Alcance. Mi experiencia incluso en lugares chicos es que nunca se llega a tener una cobertura total y confiable. Los modos mas avanzados de WiFi, como 802.11ac no están disponibles en los módulos económicos para microcontroladores, y los modos mas convencionales como 802.11b/g/n tienen inconvenientes.

3. Repetidoras/Mesh. Cada dispositivo WiFi opera como una entidad independiente. Es bastante complejo armar redes tipo mesh donde cada nodo sea también un repetidor. Esa característica es muy deseable y nos permite armar redes con una robustez muy importante.

4. Precio. Aún con la masividad de estos módulos, se encuentran en el mercado alternativas en banda ISM mas económicas.

En resumen, tengo a WiFi como una alternativa para algunos dispositivos que sé que van a estar en buena área de cobertura, y con acceso a energía de 220V.

¿Que otras alternativas hay?

Las principales que veo son:

1. [RFM69](https://www.semtech.com/products/wireless-rf/fsk-transceivers/sx1231h), en 433MHz o 900MHz
2. [nRF24](https://www.nordicsemi.com/Products/Low-power-short-range-wireless/nRF24-series), en 2.4GHz
3. [nRF5x](https://www.mouser.com/new/nordicsemiconductor/nrf52-series-soc/), en 2.4GHz

De todas estas yo estoy trabajando por el momento con los módulos nRF24L01 de Nordic. Tiene características de ancho de banda, consumo de energía, alcance, posibilidad de armar repetidores y varias otras que la hacen muy interesante, sobre todo con una buena plataforma de software.

No he necesitado indagar en RFM69, que por ser una frecuencia mas baja tiene algunas ventajas desde el punto de vista alcance, pero sí tengo pendiente explorar la línea nRF5x que es la versión mas moderna de nRF24.

Los módulos de nRF24 trabajan en 2.4GHz al igual que WiFi, lo que nos permite utilizar antenas pequeñas, consumen menos de 1mA en standby, alrededor de 10mA cuando transmiten, son fisicamente muy chicos, y están ampliamente difundidos en la comunidad.

### Software

Sin importar el hardware que se use, el acceso a software de calidad que lo pueda utilizar es clave.

En el caso de los módulos RFM69 y nRF, hay una gran comunidad alrededor de la plataforma [MySensors](https://www.mysensors.org/). El trabajo en esta plataforma es bastante extenso pero lo principal se puede resumir en:

1.  Open Source. Gran comunidad de desarrolladores de software y hardware.
2.  Utiliza al detalle las mejores características de los módulos nRF para armar redes que si bien no son full mesh, son árboles con repetidores automáticos, autodiscovery, reintento en caso de errores, etc.
3.  Tipifican y resuelven de forma elegante la cantidad de tipos de sensores y los valores que estos sensores entregan.
4.  Resuelve de forma directa o via MQTT la conectividad con los principales controladores de domótica existentes como HA, OpenHAB, Domoticz, etc.

## Controlador

En mi caso elegí centralizar todo en [OpenHAB](https://openhab.org), utilizando [MQTT](http://mqtt.org) como protocolo intermedio.
![openhab.org](https://guillebot.github.io/images/blog/openhab-logo.png "Logo OpenHAB")

Esto me permite aprovechar todas las ventajas de OpenHAB pero al mismo tiempo me deja toda la información de sensores y actuadores disponibles para cualquier otra aplicación mas específica que quiera hacer. Por ejemplo si quisiera armar una app para smartphone que muestre la temperatura de algunos de los nodos, puedo hacerlo sin necesidad de pasar (o incluso de tener instalado) un controlador de domótica completo.

Lo mismo si quisiera armar alguna pantalla muy simple para mostrar información o setear escenas.

Es decir esta combinación permite arrancar con nodo y gateway muy sencillos para luego convertirse si así se desea en una solución completa de domótica.

OpenHAB es increiblemente amplio y se va a desarrollar en un artículo posterior.


# TL;DR

**Nodo**


1.  Usar Arduino Nano programado via Arduino IDE
2.  Conectarle sensor de temperatura [Ejemplo](https://www.mysensors.org/build/temp)
3.  Conectarle un módulo nRF24l01. Sirve cualquier módulo.
4.  Utilizar la plataforma y library MySensors con sketch [Temperature](https://www.mysensors.org/build/temp)



**Gateway**

1.  Usar Arduino Uno
2.  Conectar Ethernet Shield
3.  Conectar un módulo nRF24l01. Recomiendo módulo con amplificador y antena externa.
4.  Utilizar la plataforma y library MySensors con sketch [mqtt-gateway](https://www.mysensors.org/build/mqtt_gateway)



A partir de ahí la info de los sensores va a estar disponible en topics de mqtt.

