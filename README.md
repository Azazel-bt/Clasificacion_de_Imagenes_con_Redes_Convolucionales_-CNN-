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

## 🏗️ Arquitectura de la Red (Tabla 1)

El modelo replica la estructura convolucional diseñada para clasificar las imágenes del dataset CIFAR-10, la cual evalúa de forma idónea la capacidad de aprendizaje de las neuronas rectificadas bajo diferentes condiciones de contorno.
