---
title: "Domótica para mercados emergentes"
date: 2018-12-05T14:51:12+06:00
author: Guillermo
image: images/blog/blog-post-3.jpg
---

# Introducción
En este artículo junto con todos los siguientes, vamos a intentar dar nuestra visión sobre la domótica y las premisas que creemos son fundamentales para atacar el tema desde nuestra posición de país emergente. La idea es definir una serie de fundamentos o lineamientos que luego vamos a seguir desarrollando tanto en un proyecto abierto como su variante comercial.

El problema del IoT es nuevo y amplio, tiene elementos de networking, hardware y software. Al agregar además la condición “hogareña” se agregan indefectiblemente factores como usabilidad y seguridad (as in safety). Este proyecto va a intentar transitar la intersección de todo lo anterior, tomando algunas decisiones   de adopción de tecnología, diseño y desarrollo hasta la elaboración de un caso funcional.

Why spanish? Well I think that there are plenty of english content for IoT and Home Automation already. I think that we tech tinkerers have to build bridges between worlds and right now my world needs home automation in spanish. As I haven’t been able to find a similar blog elsewhere, feel free to take some ideas and/or translate this. I’m happy to answer any doubts that you may have in the future. 

Este blog va a estar en español pero va a contener innumerable cantidad de referencias a fuentes en inglés. No vamos a hacer un esfuerzo por traducir innecesariamente pero si necesitan ayuda con algo puntual nos avisan. Por tratarse de casos prácticos vamos a conversar de los precios de algunos productos, los precios se van a indicar en dólar a efectos de mantenernos vigentes en el tiempo. 

# Domótica en el mundo
La domótica como categoría está apenas comenzando. Muchos dispositivos hogareños comienzan a tener algún tipo de interacción con el entorno a través de conexiones de red.

Cada fabricante intenta centralizar la domótica alrededor de su producto y es así que se van generando distintos clusters. Cada uno de ellos con sus dispositivos, su controlador, su servicio online (nube) y su aplicación móvil.

Algunos grandes jugadores aprovechan esta fragmentación e intentan posicionarse como el gran hub que centralice todo.

Todas las soluciones “globales” dependen de alguna combinación de dispositivo físico y nube. Se comienzan a plantear algunos cuestionamientos en cuanto a seguridad y privacidad.

Adicionalmente se va a un modelo de certificación donde muchos dispositivos perfectamente funcionales quedan fuera de los ecosistemas por no tener el interés o los recursos necesarios para sumarse. Desde el punto de vista de los usuarios, cuanto más cerrado el sistema más costosa su adopción.

# En Argentina
Todo lo anterior es válido, pero debemos sumar las inmensas barreras económicas y de accesibilidad. Económica porque la relación ingresos/precios de todos los productos automatizables es lejos peor que en los países centrales; todo nos resulta muy caro. Y de accesibilidad porque las barreras arancelarias o paraarancelarias hacen muy difícil la obtención de productos, la generación de empresas que brinden soporte, la generación de comunidad en general; y todo nos resulta más difícil. 

Se suman además algunas consideraciones extra desde el punto de vista técnico:
Deficiencias en conectividad a Internet. Cualquier solución del tipo cloud se ve seriamente afectada.
Deficiencias en servicio eléctrico. La tasa de interrupciones en el servicio es notablemente más alta. Es así que cualquier solución de automatización debe lidiar de forma más concreta con las situaciones de falta de energía.

*Prioridades*: En términos de nuestras viviendas, calidad de vida y hábitos en general, en Argentina estamos lejos de los países centrales. A raíz de esto nuestros casos de uso, prioridades y tipo de dispositivos a controlar van a ser distintos. Por ejemplo nuestro recambio tecnológico es más lento y es posible que debamos interactuar con dispositivos antiguos que van a requerir un poco más de inventiva. También es posible que la nueva realidad de las tarifas energéticas lleve a prestar especial atención a temas de control de consumo o apagado automático de dispositivos, cuando en el primer mundo la prioridad pasa más por el confort.

# ¿Entonces qué hacemos?
Desde nuestro punto de vista, la solución ideal para economías emergentes debería reunir la mayor cantidad de las siguientes características:

## Software o plataforma

### Totalmente agnóstico ante marcas o fabricantes. 
La solución ideal no debe centralizarse de ninguna manera en una marca o fabricante, sin importar que contenga extensiones que permitan expandir su ecosistema. Son numerosos los casos en los que una empresa cambia su estrategia y deja inutilizados o limitados en su funcionalidad a sus productos.

### Funcionalidad offline completa.
No puede dependerse de ninguna forma de una correcta conexión a Internet para el funcionamiento completo. Obviamente pueden incorporarse funciones extra no centrales que dependan de servicios externos, pero en ningún caso un dispositivo debería dejar de funcionar ni cambiar su funcionamiento básico en caso de no haber conectividad a Internet.

### Abierto, open source, con comunidad activa. 
En relación a los movimientos de software abierto, libre, open source, es importante destacar que nunca antes en la historia de la humanidad hubo una transferencia tan grande de conocimiento (y por ende de riqueza) desde los países centrales hacia los emergentes. Software y hardware abierto son algo a lo que nos acostumbramos. Profesionales de primer nivel internacional regalando su conocimiento y trabajo. Está todo a disposición. Depende de nosotros aprovecharlo. Este proyecto toma como premisa fundamental nunca reinventar la rueda. Siempre buscar primero si existe una buena solución disponible.

Esta facilidad que brinda el software libre tiene a veces una contracara no tan favorable. La disponibilidad y baja barrera de entrada fomentan la proliferación de proyectos similares, todos bien intencionados pero que en su mayoría no logran reunir la masa crítica que los haga sustentables en el tiempo. El no renovarse y mantenerse en el tiempo hace que un proyecto por más bueno que sea en sus inicios se convierta en obsoleto e inservible sólo con el paso de algunos pocos años. Es por eso que la solución a explorar deberá contar con una comunidad que permita suponer su continuidad al menos en un plazo intermedio de 3 a 5 años. Si bien nada asegura eso en el mundo FOSS, algunos indicadores a atender son la edad del proyecto, actividad en sus foros de discusión, actividad en sus plataformas de desarrollo y tracking de issues, etc. 

Como verán también más adelante se toman algunas decisiones de diseño tendientes a independizar cada capa de la otra, utilizar protocolos estándar siempre que sea posible, etc. todo tendiente a minimizar el impacto que puede tener la obsolescencia o finalización de alguno de los proyectos que lo componen.

Conscientes de esto mismo, intentaremos también mantener nuestra solución abierta, pública y dando la bienvenida a todos aquellos que quieran participar.

### Capaz de interactuar con la mayor cantidad de sistemas posibles
Por lo variado de los dispositivos disponibles, y también por lo variado de los niveles socioeconómicos de nuestros países, es importante que la solución a desarrollar sea capaz de interactuar con la mayor variedad de dispositivos y plataformas. Más adelante se intenta hacer una lista con sus prioridades.

### Simplicidad
Si bien uno de los targets, quizás el primero, es el del hobbista avanzado o usuario techie, para una adopción masiva de la domótica es fundamental que la solución intente emular  la experiencia que los usuarios tienen con el resto de sus dispositivos tecnológicos. Es así que como requisitos mínimos deberán plantearse cosas como que se trate de una caja que pueda enchufarse, encenderse, conectarse a la red y presente una interface web para su configuración, que deberá ser asimismo lo más simple posible.
Esto no anula en absoluto que la solución cuente con capacidades avanzadas para usuarios avanzados. Se privilegia de hecho en la selección toda solución que simplifique este acceso de bajo nivel.

## Hardware
Para entender la problemática del hardware en domótica hay que separar en 3:

### Hardware central. Controlador.
El requisito de funcionamiento 100% offline con control local obliga a pensar en un controlador local. Exigencias de bajo consumo y ruido nos llevan a alguna opción de computadora pequeña y económica que pueda interactuar con todo el hardware de networking que definamos utilizar y que sea apta para correr el software que definamos.
“Link”

### Dispositivos de Terceros
La solución elegida cuenta con capacidad de conexión con una inmensa cantidad de dispositivos existentes. Cuando sea posible utilizaremos conectores estándar y cuando esto no existan vamos a explorar la forma de conectarnos desarrollando el hardware o software apropiado.

Ver lista de dispositivos ya probados y por probar en: xxxx

### Dispositivos propios
A efectos de lograr bajar la barrera de entrada económica, es clave desarrollar y/o adaptar dispositivos sensores y actuadores de bajo costo y alta robustez.
Si bien wifi se posiciona como un standard global de conexión inalámbrica, y lo vamos a usar mucho a lo largo de este proyecto, tiene algunas desventajas en cuanto a alcance o consumo de energía.
Vamos a explorar algunas alternativas de redes inalámbricas de bajo costo por dispositivo (<1 dólar), bajo consumo, posibilidad de armar redes del tipo mesh, etc.
La lista completa de dispositivos que construimos y planeamos construir está en: xxxx

### Plataformas de terceros
Sería necio de nuestra parte aislarnos de las excelentes plataformas que comienzan a estar ampliamente difundidas. Es por eso que vamos a intentar conectarnos e interactuar con Google Home, Alexa, Homekit y toda aquella plataforma que resulte relevante.

# TL;DR;
En el siguiente post se mantiene actualizada la última versión de nuestra selección.

[Estoy apurado quiero ver](../resumen-plataforma)


Mapa del proyecto


