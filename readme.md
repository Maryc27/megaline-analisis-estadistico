# 📊 Megaline: Análisis Estadístico y Optimización de Ingresos por Tarifas de Telecomunicaciones

> **Evaluación exploratoria y pruebas de hipótesis para la asignación estratégica del presupuesto publicitario entre los planes Surf y Ultimate.**

## 📌 Resumen del Proyecto y Objetivo de Negocio
El departamento comercial de **Megaline** necesita optimizar la asignación del presupuesto publicitario entre sus dos tarifas de prepago: **Surf** y **Ultimate**. 

El objetivo principal es realizar un análisis exploratorio y aplicar **pruebas de hipótesis estadísticas** para determinar cuál de los planes genera mayores ingresos promedio por usuario, así como evaluar el impacto regional (Área Metropolitana NY-NJ vs. otras regiones).

---

## 💡 Key Business Insights (Conclusiones Clave de Negocio)
**Plan con Mayor Ingreso Promedio:** El plan **Ultimate** genera un ingreso promedio por usuario significativamente mayor (~$70.00/mes) debido a su cuota fija, en comparación con el plan **Surf** (~$60.00/mes).
- **Patrón de Excedentes en Surf:** Pese a su tarifa base de $20/mes, los usuarios del plan Surf superan de forma recurrente el límite de 15 GB incluidos. Los cobros marginales por GB extra ($10/GB) representan la mayor parte del ingreso adicional generado por este plan.
- **Comportamiento en Ultimate:** Los usuarios del plan Ultimate raramente exceden sus límites (30 GB, 3000 min, 1000 SMS), pagando casi exclusivamente la cuota mensual fija.
- **Prueba de Hipótesis 1 (Planes):** Se **rechazó $H_0$** ($p < 0.05$). Existe una diferencia estadísticamente significativa en los ingresos promedio entre los clientes del plan Surf y los del plan Ultimate.
- **Prueba de Hipótesis 2 (Regiones):** **No se rechazó $H_0$** ($p > 0.05$). No existe evidencia estadística de una diferencia en el ingreso promedio entre los usuarios del área metropolitana de NY-NJ ($63.37) y los de otras regiones ($64.64). La ubicación geográfica no afecta el rendimiento financiero de los usuarios.

---
## 🎯 Recomendaciones Estratégicas para el Negocio

Con base en el análisis exploratorio y las pruebas de hipótesis realizadas, se sugiere al departamento comercial y de marketing de Megaline implementar las siguientes acciones:

### 1. Reasignación del Presupuesto Publicitario (Marketing ROI)
* **Priorizar la captación en el plan Ultimate:** Dado que la prueba de hipótesis confirmó que el plan **Ultimate** genera un ingreso promedio significativamente mayor y más estable (~$70.00/mes frente a los ~$60.00/mes de Surf), se recomienda destinar la mayor parte del presupuesto de adquisición de usuarios (ej. 60%-65%) a promocionar el plan Ultimate.
* **Mensaje de campaña centrado en "Tranquilidad y Cero Sorpresas":** Los usuarios de Ultimate raramente exceden sus límites. La publicidad debe posicionar a Ultimate como la opción *premium* donde el cliente no tiene que preocuparse por cargos sorpresa en su factura al final del mes.

### 2. Estrategia de Monetización y Retención para el Plan Surf
* **Estrategia de Upselling Gradual:** Un alto porcentaje de usuarios del plan Surf excede el límite de 15 GB y termina pagando facturas de $50, $60 o más debido a los cargos adicionales por GB ($10/GB). Megaline debe identificar a los usuarios de Surf que llevan 2 o 3 meses consecutivos pagando más de $60/mes y enviarles ofertas personalizadas para migrar a Ultimate ("*Por solo $10 más, obtén el doble de GB y elimina los cobros extra*").
* **Mitigación de Churn (Fuga de Clientes):** Los cobros imprevistos por excedentes de datos suelen causar insatisfacción. Implementar alertas de consumo cuando el usuario de Surf llegue al 80% y 100% de su cuota de datos ayudará a reducir cancelaciones y fricción comercial.

### 3. Estrategia Geográfica Unificada
* **Campañas Nacionales sin Segmentación Regional:** La segunda prueba de hipótesis demostró que no existe una diferencia estadísticamente significativa entre los ingresos del área metropolitana de NY-NJ ($63.37) y el resto del país ($64.64).
* **Optimización de Costos Publicitarios:** No se justifica pagar costos por clic (CPC) o impresiones más caras en el área metropolitana de NY-NJ bajo la expectativa de que generarán mayor valor. La pauta publicitaria debe optimizarse por perfil de cliente e intención de consumo, no por ubicación geográfica.

---

### 📈 Resumen del Impacto Esperado (KPIs)
| Acción Propuesta | KPI a Impactar | Resultado Esperado |
| :--- | :--- | :--- |
| **Enfoque publicitario en Ultimate** | *ARPU* (Ingreso Promedio por Usuario) | Incremento en el ingreso base recurrente de la empresa. |
| **Upselling Surf $\rightarrow$ Ultimate** | *LTV* & *Retention Rate* | Reducción del churn por facturación imprevista y mayor lealtad. |
| **Pauta geográfica unificada** | *CAC* (Costo de Adquisición de Cliente) | Reducción en el costo de pauta publicitaria al evitar pujas de CPC caras en NY-NJ. |

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