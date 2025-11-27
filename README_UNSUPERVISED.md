# Análisis No Supervisado: DBSCAN para Segmentación de Riesgo

---

## **1. Descripción de la Técnica y Justificación de la Elección**

| Criterio | Descripción |
| :---- | :---- |
| **Técnica Utilizada** | **Análisis de *Clusters* y Detección de Anomalías** mediante el algoritmo **DBSCAN**. |
| **Justificación de Elección** | DBSCAN fue seleccionado porque su capacidad de **aislar *outliers*** de forma nativa (etiqueta -1) es fundamental para detectar anomalías en los perfiles de riesgo. Además, permite **descubrir la estructura de densidad natural** de los datos, lo cual es más adecuado que K-Means para *datasets* financieros complejos. |
| **Objetivo** | El objetivo fue identificar segmentos de clientes homogéneos y patrones atípicos para **complementar el modelo supervisado principal**. |

---

## **2. Instrucciones de Ejecución Claras del Código**

El código completo del análisis no supervisado se encuentra en el archivo `ML_EA3_Castro_Molins.ipynb`.

### **Requisitos de Entorno**
Asegúrese de tener un entorno Python (3.8+) con las siguientes librerías instaladas:
- `pandas`
- `numpy`
- `scikit-learn` (para `StandardScaler` y `DBSCAN`)
- `matplotlib`
- `seaborn`

### **Pasos para la Ejecución**

1.  **Ubicación de Datos:** Coloque los archivos fuente de datos (`application_.parquet`, `bureau.parquet`, y `bureau_balance.parquet`) en la misma carpeta que el *notebook* `ML_EA3_Castro_Molins.ipynb`.
2.  **Apertura:** Abra el archivo `ML_EA3_Castro_Molins.ipynb` en una interfaz compatible (Jupyter Notebook, JupyterLab o Google Colab).
3.  **Ejecución Secuencial:** Ejecute **todas las celdas** del *notebook* de forma secuencial. El proceso realiza la carga, *feature engineering* (agregación de burós), escalado, aplicación del algoritmo DBSCAN y la evaluación final.
4.  **Validación:** Tras la ejecución, el *notebook* debe generar las tablas de Tasa de *Default* por *cluster* utilizadas en la Sección 4.

---

## **3. Lógica del Proceso (CRISP-DM) y Uso del Dataset**

El análisis se ejecutó siguiendo las fases del proceso **CRISP-DM** y se adhirió estrictamente al requisito de la rúbrica de **evitar el *Data Leakage***, utilizando **únicamente el conjunto de entrenamiento**.

### **A. Comprensión y Preparación de los Datos**

* **Uso Exclusivo del Entrenamiento:** Se utilizó **únicamente el conjunto de entrenamiento** (validado por la presencia de la columna TARGET), evitando el *Data Leakage*.
* **Ingeniería de Características:** Se consolidaron datos de `application`, `bureau`, y `bureau_balance` para crear un conjunto de variables consolidadas.
* **Preparación:** Las variables numéricas clave se estandarizaron (utilizando `StandardScaler`) para que DBSCAN, un algoritmo basado en distancias, funcionara correctamente.

---

## **4. Análisis e Interpretación de Resultados**

La ejecución de DBSCAN resultó en la identificación de varios *clusters* y un grupo significativo de *outliers* (-1). El desempeño del método se evaluó midiendo la **Tasa de *Default*** (`TARGET_count_ratio`) en cada segmento:

| Cluster Label | Tasa de Default | Cantidad de Clientes | Interpretación Estratégica de Riesgo |
| :---- | :---- | :---- | :---- |
| **0** | **9.09%** | 207,088 | **Máximo Riesgo/Población General.** Foco principal de morosidad. |
| **-1** | **6.48%** | 53,247 | **Outliers (Anomalías).** Clientes atípicos con riesgo intermedio. |
| **1** | 5.41% | 46,939 | **Bajo Riesgo.** |
| **3** | 4.35% | 69 | **Micro-Cluster (Riesgo Muy Bajo).** |
| **2** | **2.98%** | 168 | **Micro-Cluster de Mínimo Riesgo (Élite).** |

**Interpretación Clave:** La Tasa de *Default* varía drásticamente desde el 9.09% (Cluster 0) hasta el 2.98% (Cluster 2). El modelo no supervisado ha logrado segmentar el riesgo de una manera más granular y efectiva que la simple distribución original de `TARGET`.

---

## **5. Discusión sobre la Incorporación al Proyecto Final**

**El método DBSCAN debe incorporarse al proyecto final.**

### **Argumentación Técnica y de Aplicabilidad**

1.  **Poder Predictivo Extremo:** La etiqueta **CLUSTER\_LABEL\_DBSCAN** es la *feature* más fuerte generada en el proyecto. Esta variable categórica es capaz de identificar los segmentos de **riesgo extremo** (2.98%) y **riesgo máximo** (9.09%), mejorando la capacidad del modelo supervisado para tomar decisiones críticas.
2.  **Identificación de la Élite (Valor de Negocio):** El descubrimiento de los **Micro-Clusters 2 y 3** (los segmentos más seguros) proporciona un **valor de negocio directo**. Estos clientes deben recibir una **política de aprobación inmediata** o beneficios preferenciales, lo que es un hallazgo clave del análisis no supervisado.