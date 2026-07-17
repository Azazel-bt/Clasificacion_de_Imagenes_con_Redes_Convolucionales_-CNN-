# Proyecto CPS - Evaluación Empírica de Activaciones Rectificadas en Redes Convolucionales

Este proyecto implementa una evaluación empírica y replicación del estudio sobre funciones de activación rectificadas en Redes Neuronales Convolucionales (CNN), utilizando como base la arquitectura de red descrita en la **Tabla 1** del artículo científico de referencia, entrenada con el conjunto de datos **CIFAR-10** de Keras.

**Autor:** Carlos Stiven Roa Martinez  
**Artículo de Referencia:** [arXiv:1505.00853](https://arxiv.org/abs/1505.00853) *(Delving Deep into Rectifiers: Surpassing Human-Level Performance on ImageNet Classification)*

---

## 🎯 Objetivos del Proyecto

El propósito principal es validar de manera empírica las afirmaciones del artículo mediante la experimentación con diferentes funciones de activación e inicializaciones de pesos:

1. **Prueba de ReLU con Inicialización Deficiente:** Evaluar el impacto en el rendimiento y convergencia de la red al usar una inicialización de pesos inadecuada junto con la activación ReLU.
2. **Análisis de Inicialización por Defecto:** Investigar y documentar cuál es la estrategia de inicialización de pesos predeterminada en Keras.
3. **Optimización con Leaky ReLU:** Utilizando la misma arquitectura de red, evaluar el comportamiento de la variante **Leaky ReLU** configurada con su mejor inicialización teórica bajo dos escenarios de hiperparámetros:
   - $a = 0.2$
   - $a = 0.001$
4. **Conclusión Científica:** Determinar si los resultados obtenidos soportan o contradicen las afirmaciones presentadas en el artículo original.

---

## 🏗️ Arquitectura de la Red
Aquí tienes la tabla en formato Markdown basada exactamente en los datos de la imagen (la arquitectura de red tipo *Network in Network* o NIN) para que puedas integrarla directamente en tu archivo `README.md`:

| Input Size | NIN |
| --- | --- |
| $32 \times 32$ | 5x5, 192 |
| $32 \times 32$ | 1x1, 160 |
| $32 \times 32$ | 1x1, 96 |
| $32 \times 32$ | 3x3 max pooling, /2 |
| $16 \times 16$ | dropout, 0.5 |
| $16 \times 16$ | 5x5, 192 |
| $16 \times 16$ | 1x1, 192 |
| $16 \times 16$ | 1x1, 192 |
| $16 \times 16$ | 3x3, avg pooling, /2 |
| $8 \times 8$ | dropout, 0.5 |
| $8 \times 8$ | 3x3, 192 |
| $8 \times 8$ | 1x1, 192 |
| $8 \times 8$ | 1x1, 10 |
| $8 \times 8$ | 8x8, avg pooling, /1 |
| 10 or 100 | softmax |


El modelo replica la estructura convolucional diseñada para clasificar las imágenes del dataset CIFAR-10, la cual evalúa de forma idónea la capacidad de aprendizaje de las neuronas rectificadas bajo diferentes condiciones de contorno.
