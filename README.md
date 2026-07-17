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

Dimensión de EntradaCapa / Operación (NIN)¿Qué le hace esta transformación a la imagen? (Efecto Paso a Paso)$32 \times 32 \times 3$Conv 5x5, 192Extracción de características iniciales: Aplica 192 filtros de $5 \times 5$ para detectar bordes y texturas básicas. Mantiene el tamaño $32 \times 32$ pero expande la imagen a 192 canales de profundidad.$32 \times 32 \times 192$Conv 1x1, 160Combinación de canales (MLP): Mezcla la información de los 192 canales anteriores reduciéndolos a 160. Al ser $1 \times 1$, no altera el tamaño visual ($32 \times 32$), actúa como una mini-red densa por píxel.$32 \times 32 \times 160$Conv 1x1, 96Compresión de canales: Vuelve a mezclar y comprimir la información, bajando de 160 a 96 canales. La imagen sigue midiendo $32 \times 32$ píxeles, pero con características más abstractas.$32 \times 32 \times 96$Max Pooling 3x3, str. 2Reducción de resolución (Submuestreo): Reduce el tamaño de la imagen a la mitad ($16 \times 16$). Se queda solo con el valor máximo de cada ventana de $3 \times 3$, conservando las características más marcadas y reduciendo el ruido.$16 \times 16 \times 96$Dropout, 0.5Regularización: Apaga aleatoriamente el 50% de las neuronas durante el entrenamiento. No altera el tamaño ni los canales, pero fuerza a la red a no depender de píxeles específicos (evita el sobreajuste).$16 \times 16 \times 96$Conv 5x5, 192Extracción de características complejas: Al tener una imagen más pequeña, un filtro de $5 \times 5$ ahora detecta estructuras y formas más complejas (siluetas, partes de objetos). Sube los canales a 192.$16 \times 16 \times 192$Conv 1x1, 192Interconexión profunda: Mezcla las nuevas formas detectadas a lo largo de los 192 canales para crear combinaciones no lineales más potentes sin alterar el tamaño $16 \times 16$.$16 \times 16 \times 192$Conv 1x1, 192Refinamiento: Otra capa de abstracción píxel a píxel que pule las características reconocidas antes de volver a achicar la imagen.$16 \times 16 \times 192$Avg Pooling 3x3, str. 2Segunda reducción de resolución: Suaviza y reduce la imagen a la mitad ($8 \times 8$). En lugar de tomar el máximo, promedia los valores de la ventana de $3 \times 3$ para mantener una transición suave de las formas.$8 \times 8 \times 192$Dropout, 0.5Segunda regularización: Vuelve a aplicar un filtro de ruido del 50% para que las características de alto nivel ($8 \times 8$) sean robustas y generalizables.$8 \times 8 \times 192$Conv 3x3, 192Análisis de patrones finales: Examina las estructuras globales de la imagen en un espacio pequeño de $3 \times 3$ píxeles con 192 filtros.$8 \times 8 \times 192$Conv 1x1, 192Preparación de canales: Última mezcla de alta abstracción de las características macro de la imagen.$8 \times 8 \times 192$Conv 1x1, 10Reducción a clases de destino: Contrae drásticamente los 192 canales a solo 10 canales (uno por cada categoría de CIFAR-10). Ahora cada mapa de $8 \times 8$ representa la "fuerza" de una clase (ej. carro, perro, gato).$8 \times 8 \times 10$Avg Pooling 8x8, str. 1Colapso espacial (Global Pooling): Aplica un promedio sobre todo el mapa de $8 \times 8$, reduciendo cada matriz a un único número. Al final de esta capa, la imagen deja de ser una matriz y se convierte en un vector de 10 números.10SoftmaxConversión a probabilidades: Toma esos 10 números finales y los transforma en porcentajes que suman 100%. El valor más alto representa la predicción final de la red (ej: 85% de probabilidad de que sea un "avión").

El modelo replica la estructura convolucional diseñada para clasificar las imágenes del dataset CIFAR-10, la cual evalúa de forma idónea la capacidad de aprendizaje de las neuronas rectificadas bajo diferentes condiciones de contorno.
