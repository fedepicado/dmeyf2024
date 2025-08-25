# Segmentación de Clientes Bancarios y Predicción de Churn con LightGBM

Este repositorio contiene un pipeline completo de *machine learning* desarrollado para un problema real de predicción de **churn de clientes bancarios**, originalmente creado para el desafío competitivo **Data Mining en Economía y Finanzas (DMEyF) 2024**.

La solución evolucionó a lo largo de múltiples etapas competitivas, escalando desde pequeños conjuntos de datos hasta procesar **dos años completos de información en Google Cloud Platform (GCP)**.

El proyecto presenta un flujo de trabajo avanzado que integra **segmentación no supervisada de clientes** con un enfoque supervisado robusto basado en ensamblado de modelos para predecir churn, utilizando **LightGBM** como algoritmo principal.

---

## 🧠 Metodología y Aspectos Técnicos Destacados

### 1. Segmentación Avanzada de Clientes

El proceso de *clustering* no se basó en variables crudas, sino en una **matriz de proximidad derivada de Random Forest**, diseñada para capturar relaciones no lineales y complejas entre clientes.

- **Cálculo de la Matriz de Proximidad:**  
  Una función personalizada (`distanceMatrix`) calculó similitudes par a par según los nodos terminales en los que caían los clientes a lo largo de todos los árboles del modelo Random Forest. Esta matriz funcionó como una métrica de distancia aprendida.

- **Reducción de Dimensionalidad:**  
  La matriz de alta dimensión fue reducida a incrustaciones 2D mediante **UMAP**, elegido por su capacidad para preservar tanto la estructura local como global de los datos, superando a alternativas como *t-SNE*.

- **Clustering:**  
  Las incrustaciones resultantes se agruparon con **DBSCAN**, lo que permitió identificar regiones densas de clientes sin asumir formas esféricas, revelando segmentos de comportamiento diferenciados.

<img width="841" height="547" alt="Cluster DBSCAN" src="https://github.com/user-attachments/assets/54b914bf-fbf8-4866-a211-def8b6623fca" />


#### Descripción de los 5 grupos de clientes

El proceso de *clustering* reveló cinco perfiles de clientes con comportamientos y valores muy distintos para el banco. Esta caracterización permite diseñar estrategias de retención específicas y eficientes:

- **Cluster 1: Clientes Inactivos**  
  Se caracterizan por una **inactividad financiera total** (sin transferencias, uso de tarjetas y saldo cercano a cero). No generan rentabilidad y probablemente utilizaban la cuenta como producto secundario.  
  **Recomendación:** evaluar la conveniencia de invertir recursos en su retención, priorizando perfiles de mayor valor.

- **Cluster 0: Clientes que Perciben Haberes**  
  Todos los clientes de este segmento recibieron su sueldo el mes previo a la baja, lo que sugiere que son **empleados en relación de dependencia** que posiblemente cambiaron de empleador y banco.  
  **Recomendación:** implementar estrategias de portabilidad bancaria u ofertas competitivas durante la transición para retenerlos.

- **Cluster 4: Clientes de Alto Valor**  
  Este es el **perfil más crítico de retener**. No reciben haberes, pero mantienen **saldos elevados** (en pesos, dólares o ambas monedas), indicando una alta capacidad financiera (potencialmente pequeños empresarios o inversores). Su partida representa una pérdida significativa de rentabilidad.  
  **Recomendación:** desarrollar estrategias proactivas y personalizadas, como asesoría financiera premium, productos exclusivos y comunicación directa para comprender sus necesidades.

- **Clusters 2 & 3: Clientes Activos con Potencial**  
  Ambos grupos muestran **alta actividad transaccional y uso intensivo de tarjetas de crédito** (con un límite mayor en el Cluster 3). No acreditan haberes, por lo que podrían ser **monotributistas o trabajadores independientes**. Generan rentabilidad en ascenso y merecen atención.  
  **Recomendación:** profundizar el análisis para identificar *drivers* de churn específicos y diseñar ofertas que incrementen su *engagement* y lealtad.

---

### 2. Predicción de Churn

El flujo supervisado fue diseñado para **maximizar rendimiento y generalización**:

- **Selección de Algoritmo:**  
  **LightGBM** fue elegido por su velocidad, eficiencia en grandes volúmenes de datos y capacidad nativa para manejar valores faltantes sin necesidad de imputación previa (evitando sesgos de métodos como *MICE* o *KNN*).

- **Ingeniería de Features:**  
  Factor clave en el rendimiento. Se generaron nuevas variables a partir del análisis temporal del comportamiento de los clientes, lo que mejoró significativamente la precisión del modelo.

- **Optimización de Hiperparámetros:**  
  Realizada con **Optuna**, utilizando búsqueda bayesiana más eficiente que *GridSearch* para encontrar configuraciones superiores y robustas.

- **Robustez del Modelo y Validación Temporal:**  
  - **Seed Ensembling (Voting):** se entrenaron múltiples modelos con distintas semillas y se promediaron sus predicciones (*soft voting*) para mitigar la aleatoriedad del entrenamiento, logrando resultados más estables y generalizables.  
  - **Backtesting Temporal:** el modelo fue validado rigurosamente con particiones fuera de tiempo para simular el despliegue real y garantizar consistencia ante el *drift* temporal, un paso crítico que suele pasarse por alto.

---

## 🛠️ Stack Tecnológico

- **Lenguaje:** Python  
- **Frameworks ML:** LightGBM, Scikit-learn, XGBoost  
- **Aprendizaje No Supervisado:** UMAP, DBSCAN, Scikit-learn  
- **Optimización de Hiperparámetros:** Optuna  
- **Manejo y Cómputo de Datos:** Pandas, NumPy, Google Cloud Platform (GCP)  
- **Visualización:** Matplotlib, Seaborn

## Competencias Kaggle

[DM EYF 2024 - Primera](https://www.kaggle.com/competitions/dm-ey-f-2024-primera/leaderboard)  

[DM EYF 2024 - Segunda](https://www.kaggle.com/competitions/dm-ey-f-2024-segunda)  

[DM EYF 2024 - Tercera](https://www.kaggle.com/competitions/dm-ey-f-2024-tercera)  
