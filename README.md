

# **README - Análisis de Transacciones y Cuentas Bancarias con PySpark**

Este proyecto realiza un análisis de datos bancarios utilizando PySpark, con la implementación de la arquitectura **Medallion** (Bronze, Silver y Gold) para procesar datos de transacciones, cuentas de clientes, demografía y categorías de comerciantes. 

### **Índice:**
1. [Descripción del Proyecto](#descripción-del-proyecto)
2. [Requisitos](#requisitos)
3. [Estructura de Archivos](#estructura-de-archivos)
4. [Instrucciones de Ejecución](#instrucciones-de-ejecución)
5. [Decisiones de Diseño](#decisiones-de-diseño)
6. [Licencia](#licencia)

---

## **Descripción del Proyecto**

Este proyecto carga, limpia y procesa datos bancarios en tres capas:
- **Capa Bronze:** Se cargan los datos originales en formato CSV.
- **Capa Silver:** Se realiza la limpieza y transformación de datos, eliminando duplicados, valores nulos y realizando conversiones de tipo.
- **Capa Gold:** Se realiza una agregación para obtener información útil sobre el gasto total por cliente, la cantidad de transacciones y su relación con el límite de crédito.

La solución utiliza **PySpark** para procesar grandes volúmenes de datos y **Matplotlib** para la visualización del gasto total por cliente.

---

## **Requisitos**

1. **Google Colab** o entorno compatible con Python 3.x.
2. **PySpark**: Instalación de la librería para trabajar con grandes volúmenes de datos.
3. **Matplotlib**: Para la visualización de resultados.
4. **CSV de entrada** con las siguientes columnas:
   - `credit_transactions.csv`: Transacciones de clientes con los detalles de cada transacción.
   - `customer_accounts.csv`: Cuentas de clientes, incluyendo el límite de crédito.
   - `customer_demographics.csv`: Datos demográficos de los clientes.
   - `merchant_categories.csv`: Categorías de los comerciantes.

---

## **Estructura de Archivos**

```
/path-to-project/
│
├── credit_transactions.csv       # Datos de transacciones bancarias
├── customer_accounts.csv         # Datos de cuentas bancarias
├── customer_demographics.csv     # Datos demográficos de clientes
├── merchant_categories.csv       # Datos de categorías de comerciantes
│
├── transactions_bronze.parquet   # Datos en Capa Bronze (formato Parquet)
├── accounts_bronze.parquet       # Datos en Capa Bronze (formato Parquet)
├── transactions_silver.parquet   # Datos en Capa Silver (formato Parquet)
├── accounts_silver.parquet       # Datos en Capa Silver (formato Parquet)
├── customer_spending_dold.parquet# Datos agregados en Capa Gold (formato Parquet)
│
├── analysis.ipynb                # Notebook con el código de procesamiento y análisis
└── README.md                     # Este archivo
```

---

## **Instrucciones de Ejecución**

### Paso 1: Preparación del entorno
1. Asegúrate de tener un entorno con **PySpark** y **Matplotlib** instalados. Si estás usando **Google Colab**, puedes instalarlo ejecutando:
   ```python
   !pip install pyspark matplotlib
   ```

### Paso 2: Subir los archivos CSV
- Utiliza Google Colab para subir los archivos CSV (`credit_transactions.csv`, `customer_accounts.csv`, `customer_demographics.csv`, `merchant_categories.csv`).
  ```python
  from google.colab import files
  uploaded = files.upload()
  ```

### Paso 3: Ejecutar el código
- Ejecuta el código en el notebook `analysis.ipynb`, que cubre:
  - Carga y procesamiento de datos en la Capa Bronze.
  - Transformaciones para la Capa Silver.
  - Agregaciones y análisis en la Capa Gold.

### Paso 4: Visualización de los Resultados
- El gráfico generado con **Matplotlib** mostrará el total de gastos por cliente.

### Paso 5: Guardar los Resultados
- Los resultados procesados se guardarán en archivos Parquet en las diferentes capas (`transactions_silver.parquet`, `accounts_silver.parquet`, `transactions_gold.parquet`).

---

## **Decisiones de Diseño**

1. **Arquitectura Medallion:**
   - **Capa Bronze:** Los datos se cargan sin modificaciones en formato Parquet para asegurar que los datos originales se mantengan intactos.
   - **Capa Silver:** Se realizan transformaciones como eliminación de nulos y duplicados, y conversiones de tipos de datos. Esto asegura la calidad de los datos antes de cualquier análisis.
   - **Capa Gold:** Se realizan agregaciones y análisis como el gasto total por cliente y la relación entre gasto y límite de crédito. Esto proporciona métricas clave para decisiones de negocio.

2. **Uso de PySpark:**
   - PySpark se utiliza para aprovechar su capacidad de procesamiento distribuido y manejo de grandes volúmenes de datos, lo cual es esencial para el análisis bancario.

3. **Uso de Parquet:**
   - Se utiliza Parquet como formato de almacenamiento porque es eficiente en términos de almacenamiento y procesamiento, además de ser compatible con PySpark.

4. **Visualización:**
   - Se utiliza **Matplotlib** para generar un gráfico que ilustra el gasto total por cliente. Esto ayuda a entender visualmente los patrones de consumo.

---

## **Licencia**

Este proyecto está bajo la Licencia MIT. Para más detalles, revisa el archivo LICENSE.

