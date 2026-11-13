# Proyecto Final del Curso:
# **Optimización Cuántica aplicada en tu Proyecto de Posgrado**

### **Fecha Final de Entrega:** Viernes 11 de diciembre del 2026.

---

# 1. Objetivos

- Describir matemáticamente un problema de optimización específico mediante una formulación **QUBO (Quadratic Unconstrained Binary Optimization)**.
- Diseñar e implementar un **Circuito Cuántico Variacional** requerido para resolver dicho problema **QUBO** mediante un abordaje **Variational Quantum Eigensolver** (**VQE**), o mediante el abordaje **Quantum Approximate Optimization Algorithm** (**QAOA**).
- Implementar mediante **PennyLane** la solución al problema QUBO siguiendo uno de los abordajes indicados (**VQE** o **QAOA**).
- Evaluar e interpretar los resultados obtenidos, cuidando la calidad de las soluciones y su relación con el problema original.

---

# 2. Descripción general del Proyecto

- Considerando su proyecto de investigación de posgrado, piense y defina un **problema de optimización** específico que pueda recibir las ventajas de su solución mediante las técnicas de computación cuántica variacional estudiadas en el curso.

- Con ello, el problema seleccionado deberá tener una formulación matemática que permita su transformación a un modelo **QUBO**, con un operador **Hamiltoniano** adecuado para implementar su solución mediante un **circuito VQE**, o un **circuito QAOA**.

---

# 3. Procedimiento

## 3.1 Definición del Problema de Optimización

Para la definición de su problema de optimización describa:

1. **Contexto:** Indique de manera específica, el problema de optimización escogido asociado a su **proyecto de posgrado**.
2. **Motivación:** ¿Por qué es importante resolver este problema dentro de su proyecto de investigación?
3. **Objetivo:** ¿Qué se desea minimizar o maximizar en dicho problema de optimización?
4. **Variables de decisión:** ¿Cuáles son las variables de decisión que se deben considerar en la solución algorítmica?
5. **Restricciones:** ¿Su problema de optimización presenta alguna condición o condiciones que deban ser cumplidas en la solución final del problema?
6. **Resultado esperado:** ¿Qué representa o qué significa presenta una solución óptima para el problema planteado?

## 3.2 Formulación matemática

Presente una **formulación matemática** de su problema de optimización, identificando:

- Variables de decisión.
- Función objetivo.
- Restricciones.
- Parámetros del modelo.

Tenga presente que, de manera general, su problema de optimización deberá expresarse como:

$$
\begin{aligned}
\min_{\mathbf{x}} \quad & f(\mathbf{x})\\
\text{sujeto a} \quad & g_i(\mathbf{x}) \leq 0 \quad \text{y/o}\\
& h_j(\mathbf{x}) = 0
\end{aligned}
$$

Donde:

- $\mathbf{x}$ representa las variables de decisión.
- $f(\mathbf{x})$ es la función objetivo.
- $g_i(\mathbf{x})$ representa las restricciones de desigualdad (si las hay).
- $h_j(\mathbf{x})$ representa las restricciones de igualdad (si las hay).

Con ello, la formulación corresponderá a un **problema de minimización o maximización**.

## 3.3 Conjunto de datos

Defina un conjunto de datos relacionado con el problema de optimización escogido para el Proyecto Final. Para ello considere una de las siguientes opciones:

- **Datos reales:** obtenidos de su propio proyecto de investigación, o de repositorios científicos, bases de datos abiertas, plataformas públicas o fuentes institucionales.
- **Datos sintéticos:** generados mediante simulación o procedimientos computacionales que representen las características del problema estudiado.

### 3.3.1 Características del conjunto de datos:

Con relación al conjunto de datos definido, indique:

- Descripción de las variables y parámetros.
- Número de registros, elementos o instancias.
- Tipo de datos y sus respectivos dominios.
- Procedimiento de preprocesamiento, cuando sea necesario.

## 3.4. Formulación QUBO del problema

Una vez definido el problema de optimización y su conjunto de datos, construya la **formulación QUBO** respectiva.

En general, la formulación de un **problema QUBO** está dada por:

$$
\min_{\mathbf{x}\in\{0,1\}^{n}}
E(\mathbf{x}) =
\mathbf{x}^{T}Q\mathbf{x}
$$

Donde:

- $\mathbf{x}$ es un vector de variables binarias.
- $n$ es el número de variables de decisión.
- $Q$ es una matriz de coeficientes que representa los costos e interacciones entre las variables.
- $E(\mathbf{x})$ es la función objetivo cuadrática que se desea minimizar.

### 3.4.1 Codificación de las variables de decisión

Explique cómo se representan las variables de decisión originales mediante variables binarias.

Por ejemplo:

$$
x_i =
\begin{cases}
1 & \text{si se selecciona el elemento }i\\
0 & \text{en caso contrario}
\end{cases}
$$

La codificación deberá ser consistente con la naturaleza del problema seleccionado.

### 3.4.2 Incorporación de restricciones

Incorpore a la función objetivo, las restricciones de su problema original  mediante **términos de penalización**.

Por ejemplo, para una **restricción de igualdad**:

$$
\sum_i a_i x_i=b
$$

Se puede incorporar el siguiente término:

$$
P\left(\sum_i a_i x_i-b\right)^2
$$

Donde $P$ representa el **coeficiente de penalización**.

Dadas sus restricciones requeridas, justifique la selección de los coeficientes de penalización, y verifique que las restricciones del problema original estén correctamente representadas.

### 3.4.3 Construcción de la matriz QUBO

- Presente la matriz QUBO derivada para su problema de optimización, explique el significado de sus coeficientes, y cómo estos representan la **función objetivo** y las **restricciones del problema**.

- Igualmente, verifique que la energía QUBO calculada para una solución binaria corresponda al valor de la función objetivo penalizada del problema original.

---

## 3.5 Implementación mediante algoritmos cuánticos variacionales

Una vez obtenida la formulación QUBO, el siguiente paso consiste en construir el **Hamiltoniano** correspondiente requerido para implementar el algoritmo cuántico variacional en **PennyLane**.

### 3.5.1. Conversión de QUBO a Hamiltoniano de Ising

Transforme las variables binarias en **operadores de Pauli** mediante la relación:

$$
x_i=\frac{1-Z_i}{2}
$$

* Donde $Z_i$ es el operador de **Pauli-Z** aplicado al qubit correspondiente.

A partir de esta transformación, construya su **Hamiltoniano** de costo:

$$
H_C =\sum_{i} h_i Z_i +\sum_{i < j} J_{ij} Z_i Z_j + C
$$

* Donde:

    - $h_i$ son los coeficientes asociados a los términos individuales.
    - $J_{ij}$ son los coeficientes de interacción entre pares de qubits.
    - $C$ es una constante independiente de las variables de decisión.

Verifique que la energía de este Hamiltoniano corresponde a la energía del modelo QUBO, teniendo presente la transformación utilizada.

## 3.6 Implementación en PennyLane

Para su implementación final en **Pennylane**, considere el desarrollo de los siguientes componentes:

1. Definición del dispositivo cuántico.
2. Construcción del Hamiltoniano de costo.
3. Implementación del circuito cuántico variacional (**Feature Maps** y **Ansatz**).
4. Definición de los parámetros entrenables.
5. Definición de la función de costo.
6. Implementación del procedimiento de optimización.
7. Extracción y evaluación de las soluciones obtenidas.

---

# 4. Análisis experimental

En el análisis final de la implementación de su solución al problema de optimización escogido, tenga en cuenta las siguientes preguntas:

- ¿El algoritmo implementado logró encontrar una solución factible?
- ¿La solución obtenida satisface las restricciones originales?
- ¿Cómo influye el número de qubits en el comportamiento del algoritmo?
- ¿Cómo influye el número de capas del circuito variacional?
- ¿Qué comportamiento presenta la función de costo durante el entrenamiento?
- ¿Cuáles son las principales limitaciones encontradas durante la implementación?

---

# 5. Entrega del proyecto

Para la entrega del presente Proyecto Final, considere:

## 5.1 Exposición Final

* Realice una **exposición** de su solución completa llevada a cabo, teniendo presente todos los pasos indicados en esta guía.
* Explique detalladamente el código fuente implementado.
* Igualmente, explique detalladamente los resultados de optimización obtenidos, y su interpretación conceptual relacionada al problema original plenteado.
* Si utilizó IA para implementar el presente Proyecto Final, realice una **Declaración Formal** de uso de IA, indicando qué modelo de IA utilizó, para qué la utilizó, y un resumen de los prompts utilizados.
* Finalmente, presente conclusiones y referencias bibliográficas utilizadas.

## 5.2 Código Fuente

* Por favor comparta a mi correo electrónico (adolfo.patino@udea.edu.co), el enlace de su repositorio de GitHub, o del notebook en Google Colab, con la **implementación completa desarrollada**.

* En dicho código fuente incluya:

    - Carga o generación del conjunto de datos.
    - Construcción del modelo de optimización.
    - Formulación QUBO.
    - Construcción del Hamiltoniano.
    - Implementación del algoritmo VQE o QAOA en PennyLane.
    - Procedimiento de optimización.
    - Evaluación de las soluciones.
    - Generación de las gráficas y resultados experimentales.

El código deberá estar **organizado y documentado** de manera que pueda ser ejecutado y reproducido por otras personas.
