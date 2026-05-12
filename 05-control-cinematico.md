---
layout: default
title: Control cinemático
nav_order: 6
---

# Control cinemático con UR5e

> Proyecto de Leo González Yamada

> Código `CC_UR5e.m` del [repositorio del proyecto](https://github.com/LeoGonYama39/JustTheDocs_Robotica).

En esta sección, se demostrará el control cinemático del UR5e. Se controlará únicamente las posiciones cartesianas *x*, *y* y *z* del EF, sin controlar la orientación.

También, se usará el método de **ecuaciones paramétricas**, combinado nuevamente con el **método eurístico**, para dibujar un círculo con el EF.

## Contenido

- [Ecuaciones paramétricas](#ecuaciones-paramétricas)
- [Control cinemático](#control-cinemático)

---

## Ecuaciones paramétricas

Parecido al polinomio quíntico, en este método moveremos al EF en función dle tiempo, pero con la diferencia de que vamos a describir cuerpos geométricos a partir de ecuaciones.

Como ejemplo, la ecuación de un círculo, la cuál es:

```text
x = Cx + rcos(ft)
y = Cy + rsen(ft)
```

Donde:
- **x:** posición en eje x.
- **y:** posición en eje y.
- **Cx:** centro del círculo en eje x.
- **Cy:** centro del círculo en eje y.
- **r:** radio del círculo.
- **f:** frecuencia.
- **t:** tiempo.

Esta ecuación es la que usaremos para esta demostración, pero el método es capaz de describir cualquier figura geométrica, siemrpe y cuando se cuente con su ecuación paramétrica.

---

## Control cinemático

Es una técnica de control que permite satisfacer una pose deseada calculando las velocidades angulares necesarias para alcanzar la pose.

La fórmula es la siguiente:

