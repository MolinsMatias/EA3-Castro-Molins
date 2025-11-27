# 🏆 Proyecto de Scoring Crediticio Avanzado con Machine Learning

## 1. Introducción y Propósito del Proyecto

Este proyecto implementa un modelo de **Scoring Crediticio** robusto, diseñado para predecir la probabilidad de **default** (incumplimiento de pago) en solicitantes de crédito. El objetivo es optimizar la toma de decisiones financieras mediante la clasificación precisa de los clientes en segmentos de riesgo.

El proyecto abarca las metodologías estándar de la ciencia de datos (CRISP-DM), desde la ingeniería de características complejas utilizando múltiples fuentes de datos hasta la implementación de modelos predictivos y análisis no supervisados para la segmentación.

## 2. Fuentes de Datos

El análisis y modelado se realizan a partir de la consolidación de tres archivos principales:

* **`application_.parquet`**: Datos de la solicitud principal del cliente.
* **`bureau.parquet`**: Historial crediticio y de buró de crédito del cliente.
* **`bureau_balance.parquet`**: Información detallada del historial de pagos y balances de las líneas de crédito del cliente.

## 3. Estructura y Entregables del Proyecto

El repositorio se organiza para soportar los diferentes componentes del proyecto (Supervisado y No Supervisado):

| Componente | Objetivo | Archivos Clave |
| :--- | :--- | :--- |
| **Análisis No Supervisado** | Segmentación y detección de anomalías (DBSCAN) para generar *features* de riesgo avanzadas. | `ML_EA3_Castro_Molins.ipynb` |
| **Documentación DBSCAN** | Descripción, justificación, resultados y discusión de la técnica no supervisada. | `README_UNSUPERVISED.md` |
| **Modelo Supervisado Final** | Predicción final de la variable `TARGET` (modelo de *scoring*). | *[Notebook Supervisado Pendiente]* |

## 4. Instrucciones de Ejecución General

### **⚙️ Requisitos de Entorno**

Para ejecutar los *notebooks* del proyecto, asegúrese de tener instalado Python (3.8+) y las librerías principales de *data science*, incluyendo: `pandas`, `numpy`, `scikit-learn`, `matplotlib`, y `seaborn`.

### **🚀 Ejecución del Componente No Supervisado (DBSCAN)**

Para replicar el análisis de *clustering* de riesgo:

1.  **Datos:** Coloque todos los archivos `.parquet` en la carpeta raíz.
2.  **Notebook:** Ejecute secuencialmente el archivo `ML_EA3_Castro_Molins.ipynb`.
3.  **Detalles:** Para obtener las instrucciones detalladas de este entregable específico, consulte el archivo **`README_UNSUPERVISED.md`**.