
---

## 📂 Fuente del Dataset

**📄 Nombre:** Online Retail Dataset  
**📍 Fuente:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Online+Retail)  
**📅 Periodo:** Diciembre de 2010 a diciembre de 2011  
**📊 Descripción:**  
Contiene información de facturas emitidas por una tienda online del Reino Unido, incluyendo:
- Código de factura (*InvoiceNo*)
- Código y descripción del producto (*StockCode*, *Description*)
- Cantidad vendida (*Quantity*)
- Precio unitario (*UnitPrice*)
- Identificador del cliente (*CustomerID*)
- País del comprador (*Country*)

---

## ⚙️ Herramientas y Librerías Utilizadas

| Herramienta / Librería | Uso Principal |
|-------------------------|----------------|
| **Python 3.10+** | Lenguaje base |
| **Google Colab** | Entorno de desarrollo SaaS |
| **Pandas / NumPy** | Manipulación y análisis de datos |
| **Matplotlib / Seaborn** | Visualización de datos |
| **Scikit-learn** | Modelado de machine learning |
| **OpenPyXL** | Lectura de archivos Excel |
| **Joblib** | Serialización de modelos |

---

## 🔍 1️⃣ Carga y Exploración de Datos

- Lectura del archivo `Online Retail.xlsx` desde Google Colab.  
- Inspección inicial de estructura, tipos de datos y valores faltantes.  
- Generación de estadísticas descriptivas.  
- Detección de:
  - Valores negativos en `Quantity` (devoluciones).
  - Valores faltantes en `CustomerID`.
  - Precios unitarios atípicos.

📊 **Primeras observaciones:**
- Más del **80%** de las transacciones corresponden al **Reino Unido**.
- La mediana del precio unitario es de **£3.00**, lo que muestra un mercado de productos de bajo costo.
- Algunos registros presentan `Quantity` mayores a 50,000, considerados *outliers*.

---

## 📈 2️⃣ Análisis Exploratorio de Datos (EDA)

### 🔹 Distribución de variables numéricas
Se analizaron las distribuciones de `Quantity`, `UnitPrice` y `TotalPrice`:
- Se observan valores sesgados con outliers extremos.
- Se aplicaron recortes al percentil 99 y escalas logarítmicas para visualizaciones claras.

### 🔹 Análisis de variables categóricas
- Los países con más transacciones: **UK, Alemania, Francia, Países Bajos, Irlanda.**
- El producto más vendido pertenece a la categoría de **regalos y decoración.**

### 🔹 Matriz de correlación
- Se identificó una correlación moderada entre `Quantity` y `TotalPrice`.
- Variables como `UnitPrice` muestran poca relación lineal directa con el resto.

### 🔹 Identificación de outliers
- Se utilizaron **boxplots ajustados y logarítmicos** para detectar valores anómalos en precios y cantidades.
- Los outliers más altos fueron filtrados para evitar distorsión visual.

### 📊 Visualizaciones destacadas:
1. Histogramas de `UnitPrice` y `TotalPrice` (ajustados y logarítmicos).  
2. Boxplots comparativos con outliers.  
3. Heatmap de correlación.  
4. Ventas totales por país (barplot).  
5. Productos más vendidos (gráfico de barras).

---

## ⚙️ 3️⃣ Preprocesamiento

- Eliminación de registros con valores nulos en `CustomerID`.
- Conversión de tipos de datos a formatos numéricos adecuados.
- Creación de la variable `TotalPrice = Quantity * UnitPrice`.
- Codificación de la variable categórica `Country` mediante `LabelEncoder`.
- Escalado de características numéricas con `StandardScaler`.
- División del conjunto de datos en entrenamiento (80%) y prueba (20%).

---

## 🤖 4️⃣ Modelado con Machine Learning

### Algoritmos utilizados:
1. **Regresión Logística (modelo base lineal)**  
2. **Random Forest Classifier (modelo no lineal y robusto a outliers)**

### Entrenamiento y evaluación:
- Se entrenaron ambos modelos con los datos preprocesados.  
- Se evaluaron usando:
  - **Accuracy**
  - **Matriz de Confusión**
  - **Validación cruzada (k=5)**

### 🔹 Resultados:

| Modelo | Accuracy | Observaciones |
|--------|-----------|----------------|
| **Regresión Logística** | ~0.72 | Buen desempeño general, pero sensible a outliers |
| **Random Forest** | ~0.86 | Mejor manejo de datos desbalanceados y variables no lineales |

### 🔹 Visualización:
- **Matrices de confusión mejoradas** (Top 10 países y normalizadas).  
- **Gráfico comparativo de rendimiento (barplot)** mostrando el desempeño de ambos modelos.

---

## 🧾 5️⃣ Resultados Principales

- El modelo **Random Forest** alcanzó la mayor precisión (≈86%).  
- La **Regresión Logística** tuvo buen rendimiento general, pero menor capacidad de generalización.  
- Los países con más confusiones fueron aquellos con menos datos (ej. Portugal, Noruega).  
- La variable `TotalPrice` es la que más influye en la predicción del país de origen.

---

## 🧩 6️⃣ Conclusiones y Recomendaciones

### 🎯 **Hallazgos Principales**
- El **Reino Unido concentra más del 80%** de las transacciones totales.  
- Los productos más vendidos son **artículos pequeños de decoración y regalo**.  
- Se identificaron **outliers y valores negativos** asociados a devoluciones.  
- La variable `Quantity` tiene alta dispersión y afecta las correlaciones.  

### 📊 **Patrones Identificados**
- Los clientes internacionales tienden a comprar menos unidades, pero con precios unitarios más altos.  
- Existen comportamientos estacionales o picos de compra no explicados (posibles campañas).  
- Los datos confirman un patrón de **microtransacciones frecuentes**.

### ⚠️ **Limitaciones**
- Dataset limitado a un año (2010–2011).  
- Falta de información de contexto (promociones, canales, fechas).  
- Campos incompletos en *CustomerID* y *Description*.  

### 💡 **Recomendaciones**
1. Implementar procesos automáticos de limpieza y validación de datos.  
2. Usar técnicas de segmentación avanzada (como RFM o clustering).  
3. Analizar tendencias a lo largo del tiempo incorporando variables de fecha.  
4. Utilizar el modelo Random Forest como base para sistemas de predicción de mercado.  

---

## ☁️ 7️⃣ Reflexión sobre Google Colab y SaaS

> Google Colab permitió desarrollar este proyecto sin necesidad de instalaciones locales, ofreciendo acceso gratuito a recursos de cómputo, integración directa con Google Drive y un entorno ideal para el aprendizaje colaborativo.  
> Este enfoque SaaS demuestra cómo las plataformas en la nube facilitan el análisis de datos, la experimentación con modelos de Machine Learning y la gestión eficiente de notebooks compartidos.

---

## 🎥 8️⃣ Video de Sustentación

**Duración:** 10 minutos  
**Contenido:**
1. Introducción y planteamiento del problema.  
2. EDA y hallazgos principales.  
3. Metodología de modelado y métricas.  
4. Resultados, conclusiones y reflexión final.  

📁 Disponible en la carpeta `/video/`.

---

## 👩‍💻 Autora

**Yuliana Díaz**  

📅 Octubre 2025  




---

> “Transformar los datos en conocimiento es el primer paso para tomar decisiones inteligentes.”


