---
layout: default
title: Planificación de trayectorias
nav_order: 5
---

# Planificación de trayectorias con UR5e

> Proyecto de Leo González Yamada

> Código `PlanTrayec_proceso.m` del [repositorio del proyecto](https://github.com/LeoGonYama39/JustTheDocs_Robotica).

En esta sección, se explicará y demsotrará la **planificación de trayectorias** de un **UR5e** efectuada en la aplicación industrial Pick and Place explicada en el inicio. Específicamente, usaremos el **método heurístico** y el **polinomio quíntico**

Como se mencionó el el apartado anterior, al resolver el problema por pura cinemática inversa, estamos atados a las acciones de las funciones nativas de UR, y si queremos controlar la velocidad de un movimiento, es necesario usar otros métodos como el **polinomio quíntico**, el cuál requiere del **método eurístico**.

## Contenido

- [Método eurístico](#método-eurístico)
- [Polinomio quíntico](#polinomio-quíntico)

---

## Método eurístico

Este método consiste en definir la pose deseada en función del tiempo con condiciones. En otras palabras, tenemos el control total de qué pose queremos que haga el robot en qué momento del tiempo, sin estar atados solamente a esperar a que el UR5e acabe de poner la pose indicada en las funciones `MoveJ` o `MoveL`.

Para este caso, usaremos las mismas poses definidas en la sección anterior (a exepción de una pose), las cuáles procesaremos con cinemática inversa para obtener las posiciones articulares y mover el robot con esas posiciones. Por lo tanto, seguiremos usando el método de inversa geométrica explorado en la sección anterior.

En el código de esta sección, pdoremos observar la siguiente secuencia (en segundos):

- **Si tiempo (t) menor a 1:** Moverse a la posición previa al agarre de la botella.
- **t de 1 a 10:** la botella se transportará por la banda.
- **t de 10 a 11:** el robot se moverá a la posición para agarrar la botella y la agarrará.
- **t de 11 a 12:** el robot volverá a la posición previa al agarre de la botella, pero con la botella agarrada por el gripper.
- **t de 12 a 13:** el robot se moverá a la posición previa a la colocacción de la botella.
- **t de 13 a 16:** el robot se moverá a la posición donde se dejará la botella con **polinomio quíntico**.
- **t de 16 a 17:** el gripper soltará el objeto y el robot volverá a la posición previa a la colocacción de la botella.

Por lo tanto, gracias al método eurístico, tenemos una rutina más controlada, donde podemos decidir qué hará el robot en cada momento de la rutina.

---

## Polinomio quíntico

Este método nos permite mover el robot con una trayectoria *suave*, de manera *segura* y *controlada*, y esto en función del tiempo, por lo que se puede convinar con el método eurístico.

Este polinomio, como lo dice su nombre, es de quinto grado, por lo que tendremos la siguiente forma:

<p>
$$x(t) = a_5t^5 + a_4t^4 + a_3t^3 + a_2t^2 + a_1t + a_0$$
</p>