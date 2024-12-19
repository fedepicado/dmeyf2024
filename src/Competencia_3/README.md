# Instructivo para Reproducir el Proceso de la Competencia 3

Este instructivo detalla el orden y el propósito de los notebooks y scripts utilizados para obtener el resultado final de la competencia.

## Resumen del Flujo de Trabajo

1. **Creación de la clase ternaria**
2. **Data Quality (DQ)**
3. **Feature Engineering**
4. **Optimización de Hiperparámetros**
5. **Entrenamiento Final y Generación de Predicciones**

---

## Pasos Detallados

### Paso 1: Creación de la Clase Ternaria

- **Notebook:** `Clase_ternaria_compe_03.ipynb`  

### Paso 2: Data Quality (DQ)

- **Notebook:** `DataQuality.ipynb`  
- **Objetivo:**  
  - Eliminación de columnas con drifting.  
  - Corrección de variables con valores nulos (NaN).  
  - Imputación de valores faltantes para determinadas columnas en meses específicos.

  Al finalizar, se obtiene un dataset consistente y listo para la generación de nuevas características.

### Paso 3: Feature Engineering

- **Notebooks:**  
  - `Feature_Engineering_en_SQL_1.ipynb`  
- **Objetivo:**  
  Creación de nuevas variables a partir de las monetarias, incluyendo:
  - Diferencias entre meses consecutivos (dif1 y dif2).
  - Promedios móviles de 5 meses, lo que permite captar tendencias.

### Paso 4: Optimización de Hiperparámetros

- **Carpeta:** `Opt_m_final`  
- **Notebook:** `opt_m_final.ipynb`  
- **Objetivo:**  
  Ajustar los hiperparámetros del modelo para maximizar su desempeño predictivo.  
  Tras múltiples iteraciones, se seleccionan los parámetros óptimos para el modelo final.

### Paso 5: Entrenamiento Final

- **Carpeta:** `Entrenamiento final`  
- **Notebooks:**  
  - `j_21_semillero.ipynb`   
  - `j_21_predecir_y_ordenar.ipynb`  
  - `Subida_Kaggle.ipynb`
    
- **Objetivo:**  
  Utilizando los mejores hiperparámetros encontrados, se entrena 10 modelos cambiando solo la semilla, se realizan las 10 predicciones y se toma el promedio por cada cliente.  
  Luego, se aplica un punto de corte de 10500.
