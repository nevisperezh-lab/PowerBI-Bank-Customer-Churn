#Bank Customer Churn - Power BI Dashboard

##Descripción del Proyecto
Este proyecto de Inteligencia de Negocios analiza la tasa de abandono (Churn Rate) de los clientes de una institución bancaria. El objetivo es identificar los factores demográficos y financieros que influyen en la decisión de un cliente de cerrar su cuenta, proporcionando insights clave para el departamento de retención y marketing.

**Dataset utilizado:** [Banking Customer Churn Prediction] de Kaggle.

##Problema de Negocio
El banco busca reducir la fuga de clientes. Para ello, necesita responder a las siguientes preguntas:
- ¿Cuál es la tasa de abandono actual del banco?
- ¿Existen diferencias significativas de abandono entre géneros o países?
- ¿Los clientes con mayor saldo en su cuenta tienen mayor o menor probabilidad de irse?
- ¿Qué rango de edad representa el mayor riesgo de fuga?

##Herramientas Utilizadas
- **Power BI:** Limpieza de datos (Power Query), modelado, cálculos (DAX) y visualización.
- **Kaggle:** Fuente de datos.

## Proceso ETL (Extracción, Transformación y Carga)
1. **Extracción:** Carga del archivo CSV original en Power BI Desktop.
2. **Transformación (Power Query):** 
   - Eliminación de columnas no relevantes para el modelo analítico (ej. `RowNumber`, `Surname`).
   - Verificación y corrección de tipos de datos (saldos a formato decimal, edades a enteros).
   - Creación de la columna condicional `Estado del Cliente` (1 = Abandonó, 0 = Activo).
3. **Carga:** Aplicación de los datos transformados al modelo de Power BI.

## 🧮 Medidas DAX Principales
Se creó una tabla de medidas explícitas para calcular los KPIs del negocio:

```dax
Total Clientes = DISTINCTCOUNT(Bank_Churn[CustomerId])

Clientes Perdidos = CALCULATE([Total Clientes], Bank_Churn[Exited] = 1)

Tasa de Abandono = DIVIDE([Clientes Perdidos], [Total Clientes], 0)