---

# 📈 Predicción de Incumplimiento de Pago de Tarjetas de Crédito

Este proyecto desarrolla un modelo de Machine Learning de extremo a extremo para predecir la probabilidad de que un cliente de tarjeta de crédito incumpla su próximo pago. El principal desafío fue abordar el severo **desbalance de clases** en los datos, lo cual se resolvió exitosamente utilizando la técnica **SMOTE**.

El modelo final, un `Gradient Boosting Classifier` optimizado, logra un **F1-score de 0.51** y es capaz de **identificar correctamente al 56%** de los clientes que incumplirán su pago.

## 🎯 El Problema de Negocio

La capacidad de anticipar el incumplimiento de pago es crucial para las instituciones financieras. Un modelo predictivo fiable permite:
*   **Mitigar riesgos:** Tomar acciones preventivas con clientes de alto riesgo.
*   **Optimizar la asignación de capital:** Ajustar límites de crédito y políticas de préstamo.
*   **Reducir pérdidas financieras:** Minimizar las pérdidas por deudas incobrables.

La principal dificultad técnica es que el número de clientes que incumplen es mucho menor que el de los que pagan a tiempo. Esto provoca que los modelos tiendan a ignorar la clase minoritaria, resultando en una baja capacidad de detección, que es precisamente el objetivo de negocio.

## 📊 El Conjunto de Datos

El proyecto utiliza el conjunto de datos [**"Default of Credit Card Clients"**](https://archive.ics.uci.edu/ml/datasets/default+of+credit+card+clients) del Repositorio de Machine Learning de la UCI.

*   **Tamaño:** 30,000 observaciones.
*   **Características:** 23 variables que incluyen información demográfica del cliente (género, edad, educación), su límite de crédito, historial de pagos pasados, estados de cuenta y montos de pago.
*   **Variable Objetivo:** `default payment next month` (1 = sí, 0 = no).

## 🛠️ Metodología y Flujo de Trabajo

El proyecto se desarrolló siguiendo un flujo de trabajo sistemático para garantizar la robustez y fiabilidad del modelo final.

1.  **Análisis Exploratorio de Datos (EDA):** Se realizó un análisis inicial para entender la distribución de las variables, identificar correlaciones y visualizar la composición del conjunto de datos.

2.  **Preprocesamiento de Datos:** Las características categóricas fueron tratadas adecuadamente y se aplicó un escalado (`StandardScaler`) para normalizar las variables numéricas.

3.  **Selección del Modelo Base:** Se compararon tres modelos de clasificación (Random Forest, Logistic Regression y Gradient Boosting) utilizando validación cruzada estratificada. El `Gradient Boosting` fue seleccionado como el de mejor rendimiento inicial.

4.  **Manejo del Desbalance de Clases (SMOTE):** Este fue el paso más crítico. Se integró la técnica **SMOTE** dentro de un `Pipeline` para crear muestras sintéticas de la clase minoritaria *únicamente* durante el entrenamiento de la validación cruzada, evitando así la fuga de datos. Este paso **aumentó el Recall de la clase minoritaria de 0.35 a 0.56**, transformando el modelo de inútil a valioso.

5.  **Optimización de Hiperparámetros (GridSearchCV):** Se realizó una búsqueda exhaustiva en rejilla para encontrar la combinación de hiperparámetros que maximizara el F1-score del modelo `Gradient Boosting`.

6.  **Evaluación Final:** El modelo optimizado final fue evaluado en un conjunto de prueba completamente reservado para medir su rendimiento en datos no vistos.

## ✨ Resultados: La Evolución del Rendimiento

La siguiente tabla ilustra el impacto de cada etapa del proceso en el rendimiento del `Gradient Boosting Classifier` para predecir la clase `Default`.

| Modelo | F1-Score (Default) | Recall (Default) | Precision (Default) |
| :--- | :---: | :---: | :---: |
| **1. Modelo Base (Sin SMOTE)** | 0.46 | 0.35 | 0.67 |
| **2. Modelo Final (con SMOTE + Optimizado)**| **0.51** | **0.56** | **0.46** |

El uso de SMOTE fue clave para mejorar drásticamente la capacidad del modelo para detectar a los clientes en riesgo, aunque esto implicara un trade-off con la precisión.

## 💡 Visualizaciones Sugeridas

Para enriquecer este análisis, se podrían añadir las siguientes gráficas al notebook:

*   **Distribución de Clases:** Un gráfico de barras para visualizar el desbalance inicial entre las clases `Default` y `No Default`.
    ```markdown
    ![Distribución de Clases](ruta/a/tu/imagen_distribucion.png)
    ```
*   **Importancia de Características:** Un gráfico de barras que muestre qué variables (`LIMIT_BAL`, `PAY_0`, etc.) tienen más peso en las predicciones del modelo final.
    ```markdown
    ![Importancia de Características](ruta/a/tu/imagen_importancia.png)
    ```*   **Matriz de Confusión Final:** Una visualización de la matriz de confusión del modelo optimizado en el conjunto de prueba para ver claramente los Verdaderos Positivos, Falsos Positivos, etc.
    ```markdown
    ![Matriz de Confusión](ruta/a/tu/imagen_matriz.png)
    ```

## 🚀 Próximos Pasos y Mejoras Futuras

*   **Ingeniería de Características (Feature Engineering):** Crear nuevas variables a partir de las existentes (ej. ratios entre el límite de crédito y los saldos) para intentar capturar patrones más complejos.
*   **Probar Algoritmos Avanzados:** Implementar `XGBoost` o `LightGBM`, que son versiones más potentes y rápidas de Gradient Boosting y a menudo ofrecen un mayor rendimiento.
*   **Ajustar el Umbral de Decisión:** Analizar la curva de Precisión-Recall para seleccionar un umbral de probabilidad óptimo que se alinee mejor con los objetivos de negocio (ej. capturar al 70% de los impagadores, aceptando una menor precisión).

## ⚙️ Cómo Ejecutar este Proyecto

1.  **Clonar el repositorio:**
    ```bash
    git clone https://github.com/pablotgp/prediccion-default-credito.git
    cd prediccion-default-credito
    ```
2.  **Instalar las dependencias:**
    Se recomienda crear un entorno virtual.
    ```bash
    pip install -r requirements.txt
    ```
3.  **Ejecutar el Notebook:**
    Abrir y ejecutar el archivo `.ipynb` en la carpeta `notebooks` usando Jupyter Notebook o Visual Studio Code.

## Autor

*   **Pablo Antonio García Pastor**
    *   [LinkedIn](https://www.linkedin.com/in/pablogp-ai)
    *   [Correo Electrónico](mailto:pablotgp2002@gmail.com)
