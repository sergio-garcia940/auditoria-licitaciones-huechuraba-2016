# auditoria-licitaciones-huechuraba-2016
Análisis de estacionalidad, categorización temática y auditoría de compras públicas (Municipalidad de Huechuraba).
# Auditoría y Estacionalidad de Compras Públicas: Análisis de 291 Licitaciones Adjudicadas (Municipalidad de Huechuraba 2016)

## 1. Resumen Ejecutivo
Este proyecto analiza el comportamiento operativo, la estacionalidad del gasto y la distribución por rubros de **291 licitaciones públicas adjudicadas** durante el año 2016 por la Municipalidad de Huechuraba. A través de técnicas de auditoría de datos, ingeniería de características y matrices cruzadas, se identificaron los patrones temporales de contratación y las categorías clave que impulsaron los picos operativos del municipio.

* **Fuente oficial de datos:** Portal Nacional de Datos Abiertos (`datos.gob.cl` / Mercado Público de Chile).
* **Volumen:** 291 registros únicos analizados (100% adjudicados).
* **Entorno técnico:** LibreOffice Calc / Hojas de cálculo (Data Cleaning, Control de Unicidad y Modelado Tabular).

---

## 2. Metodología y Calidad de Datos

* **Auditoría de Unicidad:** Implementación de fórmulas de control de frecuencia (`=CONTAR.SI(...)`) sobre los identificadores únicos (`numero`), verificando un **0% de duplicidad** en el padrón contractual.
* **Corrección de Integridad Estructural:** Detección y corrección de desplazamiento de columnas generado por delimitadores de texto en descripciones extensas.
* **Tratamiento de Nulos:** Documentación y aislamiento de campos no obligatorios en origen (`fecha determino`), concentrando el análisis de ciclo en la variable verificada `fecha de cierra`.
* **Ingeniería de Características:**
  * **Temporal:** Extracción del mes operativo (`Mes_Cierre = MES(...)`).
  * **Minería de Texto y Categorización:** Clasificación algorítmica de texto no estructurado mediante funciones anidadas (`SI + HALLAR`) para agrupar las 291 licitaciones en rubros clave: *Educación/Social, Salud, Obras, Servicios/Mantención y Vehículos*.

---

## 3. Principales Hallazgos (Data Insights)

* **Estacionalidad y Concentración Operativa:**
  * **Pico anual:** El mes de **agosto lideró la actividad con 39 licitaciones adjudicadas** (13,4% del total anual).
  * **Segundo mes de alta actividad:** Mayo concentró 37 licitaciones (12,7%).
  * **Desaceleración a fin de año:** Noviembre registró una caída abrupta a solo **4 licitaciones**, evidenciando un cierre preventivo del ciclo licitatorio previo al cierre contable formal.
* **Causa Raíz del Pico de Agosto (Matriz Cruzada Rubro vs. Mes):**
  * Al cruzar la estacionalidad con las categorías, se descubrió que el alza de agosto estuvo impulsada directamente por el **área de Educación y Eventos Sociales**, la cual saltó de un promedio basal de 1 a 2 licitaciones mensuales a un **récord anual de 11 licitaciones en un solo mes** (concentrando más del 28% de los procesos de ese período).
* **Segmentación del Gasto Municipal:**
  * Las áreas operativas centrales de contratación correspondieron a compras especializadas en **Educación/Social** y **Salud**, mientras que las compras de flota y transporte mantuvieron una cadencia baja y acotada durante el ejercicio.

---

## 4. Recomendaciones Operativas y de Gestión

* **Descongestión del Calendario de Contratación:** Distribuir las bases técnicas de licitaciones educacionales a lo largo del segundo trimestre para mitigar el cuello de botella evaluativo observado en agosto.
* **Estandarización de Registros:** Implementar validación obligatoria de catálogo en los sistemas de origen para evitar descripciones libres y reducir la dispersión de categorías en el registro público.

---

## 5. Fórmulas Clave Aplicadas

* **Control de Duplicados:**
  ```text
  =CONTAR.SI(A:A; A2)
  Extracción de Mes:
  =MES(E2)
  Matriz de Categorización por Búsqueda de Texto:
  =SI(O(ESNUMERO(HALLAR("salud";B2));ESNUMERO(HALLAR("medic";B2)));"Salud";SI(O(ESNUMERO(HALLAR("escuel";B2));ESNUMERO(HALLAR("coleg";B2));ESNUMERO(HALLAR("taller";B2)));"Educación y Social";"Otros"))
