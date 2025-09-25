# Predicción de Default de Tarjeta de Crédito

Este proyecto presenta un análisis completo y el desarrollo de un modelo de machine learning para predecir la probabilidad de que un cliente incumpla con el pago de su tarjeta de crédito. El análisis se realiza en un Jupyter Notebook y se resume en un informe detallado en PDF.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pablotgp/prediccion-default-credito/blob/main/notebooks/Calibración.ipynb)
_Haz clic en el botón  para abrir y ejecutar el notebook directamente en Google Colab._

---

## Contenido del Repositorio

*   **/notebooks**: Contiene el Jupyter Notebook `Calibración.ipynb` con todo el proceso: limpieza de datos, análisis exploratorio (EDA), entrenamiento de modelos y explicabilidad con SHAP.
*   **/reports**: Incluye el informe final `Informe_Calibracion_Modelos.pdf` que resume los hallazgos y conclusiones del análisis.
*   **/data**: Contiene el dataset original `default of credit card clients.xls` utilizado para el análisis.

## Metodología

1.  **Análisis Exploratorio de Datos (EDA)**: Investigación de las distribuciones de variables clave y sus relaciones para entender el perfil de los clientes.
2.  **Preprocesamiento de Datos**: Limpieza y agrupación de categorías en variables como `EDUCATION` y `MARRIAGE`.
3.  **Entrenamiento de Modelos**: Se compararon tres algoritmos: Regresión Logística, Random Forest y **Gradient Boosting**.
4.  **Evaluación y Selección**: Se eligió el modelo **Gradient Boosting** como el de mejor rendimiento, utilizando un criterio de selección que balancea el **AUC** y el **F1-Score** para la clase minoritaria (clientes en default).
5.  **Interpretabilidad del Modelo**: Se utilizó la librería **SHAP** para entender qué características son las más influyentes en las predicciones del modelo, tanto a nivel global como para predicciones individuales.

## Resultados Clave

*   El modelo **Gradient Boosting** demostró ser el más equilibrado, con un **AUC de 0.7822** y un **F1-score de 0.4625** para la clase "Default".
*   Las características más importantes para predecir el impago son el **estado de pago del mes más reciente (PAY_0)**, el **límite de crédito (LIMIT_BAL)** y el historial de pagos anteriores.
*   Se identificó una limitación clave en el bajo **recall (35%)**, lo que motivó recomendaciones para futuras mejoras, como el uso de técnicas de balanceo de clases (SMOTE).

## Cómo Usar este Repositorio en Google Colab

1.  **Abrir el Notebook**: Haz clic en el badge "Open in Colab" al inicio de este README.
2.  **Subir el Dataset**: El notebook está diseñado para funcionar con una ruta relativa. Como Colab no puede acceder directamente a la carpeta `data/` del repositorio, deberás subir el archivo de datos manualmente a tu sesión de Colab.
    *   En el panel izquierdo de Colab, ve a la pestaña de **Archivos (icono de carpeta)**.
    *   Haz clic en el icono de **"Subir al almacenamiento de la sesión"**.
    *   Selecciona el archivo `default of credit card clients.xls` de la carpeta `data/` que descargaste de este repositorio.
3.  **Ajustar la Ruta en el Notebook (si es necesario)**: Una vez subido, la ruta en el notebook para leer el archivo debe ser la simple:
    ```python
    # Asegúrate de que la celda de carga de datos use esta ruta:
    pd.read_excel('default of credit card clients.xls', header=1)
    ```
4.  **Ejecutar las Celdas**: ¡Ya puedes ejecutar todo el notebook!

## Autor

*   **Pablo Antonio García Pastor**
    *   [LinkedIn](https://www.linkedin.com/in/pablogp-ai)
    *   [Correo Electrónico](pablotgp2002@gmail.com)
