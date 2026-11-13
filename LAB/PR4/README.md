# **Práctica de Laboratorio No. 4**  
## Sistema de Regresión Cuántica Variacional para Estimación de Congestión Vehicular

---

# 1. Objetivos

Al finalizar este laboratorio, el estudiante será capaz de:

- Implementar un sistema de regresión cuántica variacional usando **PennyLane**.
- Definir un *feature map* cuántico para codificar variables de tráfico vehicular.
- Definir un *ansatz* variacional para construir un circuito cuántico de regresión de congestión vehicular.
- Implementar un Hamiltoniano como función de salida de regresión.
- Entrenar un modelo híbrido cuántico-clásico usando optimización por gradientes.
- Analizar el comportamiento de convergencia del sistema.
- Comparar valores reales y predichos de congestión vehicular.

---

# 2. Estimación de Congestión Vehicular mediante un VQA

Tomando como base el ejemplo analizado en el siguiente *blog* de Pennylane:

https://pennylane.ai/blog/2022/06/how-to-choose-your-optimizer

y la siguiente implementación en Pennylane de un *Regresor No-Lineal* para la función $\sin(x)$:

https://github.com/gpatigno/QC_POSGRADO_2026/tree/main/MODULO4/SinFunct_Regression.ipynb

Implemente un **sistema de estimación de congestión vehicular** basado en el siguiente modelo de regresión cuántica:

$$
\hat{y}(x,\theta)=\langle \psi(x,\theta)\mid H \mid \psi(x,\theta)\rangle
$$

donde:

| Símbolo | Significado |
|---|---|
| $x$ | variables del tráfico |
| $\theta$ | parámetros entrenables |
| $H$ | Hamiltoniano de salida |
| $\hat{y}$ | congestión estimada |


## 2.1. Definición del Hamiltoniano

Utilice el siguiente Hamiltoniano como el **observable** que relaciona la congestión vehicular con las variables del tráfico.

$$
H = 0.4Z_0 - 0.2Z_1 + 0.3Z_2 + 0.5Z_3 + 0.1X_0X_3
$$


## 2.2. Variables de Tráfico Vehicular

Las variables de tráfico vehícular a ser analizadas son las siguientes:

| Variable | Descripción |
|---|---|
| $x_0$ | densidad vehicular |
| $x_1$ | velocidad promedio |
| $x_2$ | intensidad de lluvia |
| $x_3$ | flujo vehicular en intersección cercana |

Y la función de congestión que se quiere aproximar es:

$$
y \in [0,1]
$$

donde:

- $y=0$ representa tráfico libre.
- $y=1$ representa congestión severa.

## 2.3. Conjunto de Datos de Entrada y Salida

A continuación se comparte el dataset de entrenamiento y el dataset de prueba, tal que todas las variables están normalizadas en $[0,1]$:

* [Training Dataset](https://github.com/gpatigno/QC_POSGRADO_2026/tree/main/LAB/PR4/traffic_train.csv)

* [Testing Dataset](https://github.com/gpatigno/QC_POSGRADO_2026/tree/main/LAB/PR4/traffic_test.csv)

<br>

---

# 3. Entrega de la actividad

Cuando termine la presente implemente, por favor envie a mi correo electrónico el enlace de su **Github o Notebook en Google Colab** con el código completo desarrollado.