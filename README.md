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

| Dimensión de Entrada | Capa / Operación (NIN) | ¿Qué le hace esta transformación a la imagen? (Efecto Paso a Paso) |
|----------------------|------------------------|---------------------------------------------------------------------|
| **32×32×3** | **Conv 5×5, 192** | **Extracción de características iniciales:** Aplica **192 filtros de 5×5** para detectar bordes y texturas básicas. Mantiene el tamaño **32×32**, pero expande la representación a **192 canales** de profundidad. |
| **32×32×192** | **Conv 1×1, 160** | **Combinación de canales (MLP):** Mezcla la información de los **192 canales** anteriores reduciéndolos a **160**. Al ser una convolución **1×1**, no altera la resolución espacial (**32×32**), actuando como una pequeña red neuronal por cada píxel. |
| **32×32×160** | **Conv 1×1, 96** | **Compresión de canales:** Reduce los canales de **160 a 96**, conservando la resolución **32×32**, mientras obtiene representaciones más abstractas. |
| **32×32×96** | **Max Pooling 3×3, stride 2** | **Reducción de resolución (Submuestreo):** Disminuye la resolución a **16×16**. Conserva únicamente el valor máximo de cada ventana de **3×3**, resaltando las características más importantes y eliminando ruido. |
| **16×16×96** | **Dropout, 0.5** | **Regularización:** Desactiva aleatoriamente el **50 %** de las neuronas durante el entrenamiento. No modifica las dimensiones, pero reduce el sobreajuste al obligar a la red a aprender representaciones más generales. |
| **16×16×96** | **Conv 5×5, 192** | **Extracción de características complejas:** En una resolución menor, los filtros de **5×5** detectan patrones más elaborados como partes de objetos o siluetas. La profundidad aumenta a **192 canales**. |
| **16×16×192** | **Conv 1×1, 192** | **Interconexión profunda:** Combina la información de los **192 canales** para generar relaciones no lineales más complejas sin modificar el tamaño espacial. |
| **16×16×192** | **Conv 1×1, 192** | **Refinamiento:** Nueva combinación de características de alto nivel que mejora la representación antes de la siguiente reducción espacial. |
| **16×16×192** | **Avg Pooling 3×3, stride 2** | **Segunda reducción de resolución:** Reduce la representación a **8×8** utilizando el promedio de cada ventana **3×3**, preservando la información global de manera más suave que el Max Pooling. |
| **8×8×192** | **Dropout, 0.5** | **Segunda regularización:** Aplica nuevamente Dropout al **50 %**, fortaleciendo la capacidad de generalización sobre las características de alto nivel. |
| **8×8×192** | **Conv 3×3, 192** | **Análisis de patrones finales:** Examina patrones globales utilizando **192 filtros de 3×3** sobre una representación espacial reducida. |
| **8×8×192** | **Conv 1×1, 192** | **Preparación de canales:** Realiza la última combinación de características abstractas antes de la clasificación. |
| **8×8×192** | **Conv 1×1, 10** | **Reducción a clases objetivo:** Comprime los **192 canales** en **10 canales**, uno por cada clase de **CIFAR-10**. Cada mapa de **8×8** representa la evidencia correspondiente a una categoría. |
| **8×8×10** | **Avg Pooling 8×8, stride 1** | **Global Average Pooling:** Promedia cada mapa completo de **8×8**, reduciendo la representación espacial a un único valor por clase. El resultado es un **vector de 10 elementos**. |
| **10** | **Softmax** | **Conversión a probabilidades:** Transforma el vector de salida en una distribución de probabilidades cuya suma es **100 %**. La clase con mayor probabilidad corresponde a la predicción final de la red. |

El modelo replica la estructura convolucional diseñada para clasificar las imágenes del dataset CIFAR-10, la cual evalúa de forma idónea la capacidad de aprendizaje de las neuronas rectificadas bajo diferentes condiciones de contorno.

<img width="1182" height="227" alt="image" src="https://github.com/user-attachments/assets/a374912a-a1a2-4d3a-bf5c-812fd0f8bbfe" />

