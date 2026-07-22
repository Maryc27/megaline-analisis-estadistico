# 📊 Análisis MarTech & Telecom: Evaluación de Monetización y Comportamiento de Usuarios (Megaline)

## 📌 Resumen del Proyecto y Objetivo de Negocio
El departamento comercial de **Megaline** necesita optimizar la asignación del presupuesto publicitario entre sus dos tarifas de prepago: **Surf** y **Ultimate**. 

El objetivo principal es realizar un análisis exploratorio y aplicar **pruebas de hipótesis estadísticas** para determinar cuál de los planes genera mayores ingresos promedio por usuario, así como evaluar el impacto regional (Área Metropolitana NY-NJ vs. otras regiones).

---

## 💡 Key Business Insights (Conclusiones Clave de Negocio)
- **Tarifa más rentable:** El plan **Surf** genera mayores ingresos excedentes debido a que el 68% de sus usuarios supera con frecuencia el límite de MB incluidos.
- **Patrón de consumo:** Los usuarios del plan Ultimate raramente sobrepasan sus límites de minutos y SMS, pagando principalmente la tarifa base ($70/mes).
- **Hipótesis Estadística:** Se rechazó / No se rechazó la hipótesis nula ($p < 0.05$). Existe una diferencia estadísticamente significativa entre los ingresos promedio de ambos planes.

---

## 🛠️ Stack Tecnológico y Metodología
- **Lenguaje:** Python 3.10+
- **Librerías principales:** `pandas` (manipulación y agregación), `numpy` (operaciones vectoriales), `scipy.stats` (pruebas de hipótesis), `seaborn` & `matplotlib` (visualización).
- **Enfoque estadístico:** Prueba $t$ de Student para dos muestras independientes con varianzas desiguales (`equal_var=False` / Welch's t-test).

---

## 📂 Estructura de los Datos
El análisis integra 5 fuentes de datos interrelacionadas (`user_id`):
1. `megaline_users.csv`: Datos demográficos y plan contratado.
2. `megaline_plans.csv`: Condiciones tarifarias y costos excedentes.
3. `megaline_calls.csv`: Registro individual de llamadas y duración.
4. `megaline_messages.csv`: Registro individual de SMS.
5. `megaline_internet.csv`: Registro de sesiones de navegación (MB).

---

## ⚙️ Reglas de Negocio Implementadas
Para garantizar la precisión de los datos, se aplicaron las políticas de facturación de Megaline:
- **Redondeo de llamadas:** Cada llamada individual se redondea hacia arriba al minuto entero más cercano (`np.ceil`).
- **Redondeo de datos:** El tráfico mensual total se redondea al Gigabyte (GB) superior (1 GB = 1024 MB).
- **Cálculo de ingresos excedentes:** Se aplican las tarifas marginales por mensaje, minuto y GB consumido por encima del límite del plan.

---