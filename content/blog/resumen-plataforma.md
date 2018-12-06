---
title: "Resumen Plataforma"
date: 2018-12-05T12:52:36+06:00
image: images/blog/blog-post-1.jpg
author: Guillermo
---

Nosotros usamos el framework [Eclipse Smarthome](https://www.eclipse.org/smarthome/) corriendo en [Raspberry Pi](https://www.raspberrypi.org/) como producto, o en máquina virtual para desarrollo o soluciones muy grandes. 

Utilizamos todos los [bindings](https://www.eclipse.org/smarthome/documentation/features/bindings/astro/readme.html) disponibles, y [MQTT](http://mqtt.org/) como conector de todo lo demás, siempre que es posible.

A nivel networking [ethernet](https://en.wikipedia.org/wiki/Ethernet) o [wifi](https://en.wikipedia.org/wiki/Wi-Fi) para los dispositivos standard del mercado. Para nuestros sensores y actuadores utilizamos la [banda ISM](https://en.wikipedia.org/wiki/ISM_band) de 2.4GHz con el chipset [Nordic](https://www.nordicsemi.com/) [nRF24](https://www.nordicsemi.com/Products/Low-power-short-range-wireless/nRF24-series), aunque estamos ya experimentando con el mucho mas moderno [nRF5x](https://www.nordicsemi.com/Products/Low-power-short-range-wireless/nRF52832).

En el [resto de los artículos](/blog) van a poder encontrar el porqué de cada una de esas decisiones.
