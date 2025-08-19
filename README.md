# Análisis de Evasión de Clientes — Telecom X

---

## 🚀 Propósito del análisis

Este repositorio reúne mi trabajo para **entender y reducir la evasión de clientes (churn)** en Telecom X. Implementé un pipeline **ETL + EDA** en Python para:
- Preparar un **DataFrame limpio** a partir del JSON original.
- Medir la **tasa de churn** global y por segmentos.
- Identificar **factores asociados** a la deserción para priorizar acciones de retención.

---

## 🧾 Datos y fuente

- **Archivo**: `TelecomX_Data.json`  
- **Estructura**: JSON con diccionarios anidados de cliente, telefonía, internet y cuenta.  
- **Clave**: `customerID` (sin duplicados en la corrida base).

Durante la extracción aplané las estructuras anidadas para llevarlas a columnas manejables en pandas y asegurar consistencia tipando variables numéricas y categóricas.

---

## 🧭 Metodología (ETL + EDA)

1. **Extracción (E - Extract)**  
   Lectura del JSON y **aplanado** con `pandas` para consolidar información de servicios y cargos.

2. **Transformación (T - Transform)**  
   - **Tipificación** de columnas (IDs como `string`, numéricas con conversión robusta).  
   - **Normalización** básica de categóricas (minúsculas y `strip`).  
   - **Imputaciones mínimas** y **variables derivadas** (por ejemplo, `Churn_bin` y métricas auxiliares de cargo).

3. **Carga + Análisis (L + EDA)**  
   - **Descriptivos** globales y por churn.  
   - **Comparativas por segmentos** (tipo de contrato, método de pago, activación de servicios, etc.).  
   - **Exploración de numéricas** relevantes (`tenure`, cargos mensuales y totales).

---

## 🗂️ Estructura del proyecto

- **`Telecom_Latam0_sin_notas.ipynb`** → Cuaderno principal con el pipeline ETL + EDA.  
- **`TelecomX_Data.json`** → Dataset fuente.  
- **`assets/`** *(opcional)* → Gráficos y tablas exportadas.  
- **`data/processed/`** *(opcional)* → Datasets transformados (Parquet/CSV).

---

## 📊 Resultados e insights clave (corrida base)

**Tendencias observadas en la exploración inicial:**

- **Tenure bajo → mayor churn.** Los clientes con poca antigüedad presentan más probabilidad de deserción.  
- **Contratos de ciclo corto** (mes a mes) concentran **tasas de churn superiores** respecto de contratos de mayor permanencia.  
- **Cargos mensuales elevados** se asocian con **mayor churn**, especialmente cuando no hay servicios de valor que compensen el costo percibido.  
- **Método de pago**: se observan **diferencias de churn** entre medios de pago, lo que sugiere fricciones o perfiles distintos por canal.  
- **Servicios de seguridad/soporte**: su **activación coincide** con **menor churn** en varios segmentos, apuntando a un efecto de valor agregado.

Estas señales orientan las primeras **hipótesis de intervención** y priorización de segmentos.

---

## 🧠 Conclusiones y líneas de acción

1. **Retención temprana**: foco en clientes con **tenure bajo** mediante onboarding y ofertas de valor en las primeras semanas.  
2. **Estrategia de contrato**: **migrar** clientes de alto riesgo a **planes de mayor permanencia** con beneficios claros.  
3. **Valor percibido**: **empaquetar servicios** (seguridad, soporte) para **disminuir churn** en segmentos sensibles al precio.  
4. **Pagos**: revisar experiencia en **métodos de pago** con peor retención (recordatorios, incentivos, UX).  
5. **Priorización**: vigilar perfiles con **cargos mensuales altos** y **baja antigüedad**, dada su mayor propensión a churn.

---
