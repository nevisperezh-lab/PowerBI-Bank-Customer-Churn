# Bank Customer Churn - Power BI Dashboard

## Descripción del Proyecto
Este proyecto de Inteligencia de Negocios analiza la tasa de abandono (Churn Rate) de los clientes de una institución bancaria. El objetivo es identificar los factores demográficos y financieros que influyen en la decisión de un cliente de cerrar su cuenta, proporcionando insights clave para el departamento de retención y marketing.

**Dataset utilizado:** Banking Customer Churn Prediction de Kaggle.

## Problema de Negocio
El banco busca reducir la fuga de clientes. Para ello, necesita responder a las siguientes preguntas:

- ¿Cuál es la tasa de abandono actual del banco?
Se muestra una tasa de abandono global del 20,37% sobre una base de 10 mil clientes

- ¿Existen diferencias significativas de abandono entre géneros o países?
Las clientas presentan una tasa de abandono significativamente superior (25,07%) en comparación con los clientes masculinos (16,46%).
Alemania registra el mayor riesgo geográfico con una tasa de abandono del 32,44% y la mayor proporción de clientes perdidos en relación con su base.
Francia y España muestran niveles de retención más saludables, con tasas de abandono del 16,15% y 16,67% respectivamente.

- ¿Los clientes con mayor saldo en su cuenta tienen mayor o menor probabilidad de irse?
Según el gráfico de "Suma de Balance", los 2 mil clientes que abandonaron acumulaban un saldo total cercano a los 18 mil millones, mientras que los 8 mil clientes activos suman aproximadamente 55 mil millones. Esto indica que el saldo promedio por cliente es más alto entre los que se dan de baja en comparación con los que permanecen activos.

- ¿Qué rango de edad representa el mayor riesgo de fuga?
El segmento de los 50 años representa el pico máximo de riesgo de fuga, con una tasa de abandono que supera el 50 % a nivel global. Esta situación es aún más crítica en Alemania, donde el abandono en este mismo rango de edad se acerca al 70 %.

## Herramientas Utilizadas
- **Power BI:** Limpieza de datos (Power Query), modelado, cálculos (DAX) y visualización.
- **Kaggle:** Fuente de datos.

## Proceso ETL (Extracción, Transformación y Carga)
1. **Extracción:** Carga del archivo CSV original en Power BI Desktop.
2. **Transformación (Power Query):** 
   - Eliminación de columnas no relevantes para el modelo analítico (ej. `RowNumber`, `Surname`).
   - Verificación y corrección de tipos de datos (saldos a formato decimal, edades a enteros).
   - Creación de la columna condicional `Estado del Cliente` (1 = Abandonó, 0 = Activo).
3. **Carga:** Aplicación de los datos transformados al modelo de Power BI.

## Medidas DAX Principales
Se creó una tabla de medidas explícitas para calcular los KPIs del negocio:

```dax
Total Clientes = DISTINCTCOUNT(Churn_Modelling[CustomerId])

Clientes Perdidos = CALCULATE([Total Clientes], Churn_Modelling[Exited] = 1)

Tasa de Abandono = DIVIDE([Clientes Perdidos], [Total Clientes], 0)
