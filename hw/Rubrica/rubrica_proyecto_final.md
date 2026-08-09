# Rúbrica de Evaluación 

## 1. Requisitos de entrega

- **Video** (10–15 min, subido a un enlace accesible): debe explicar el proyecto de punta a punta — motivación, datos, metodología, resultados y limitaciones — como si se presentara ante un comité de riesgo o un equipo de inversión, no como una demo técnica desordenada.
- **Repositorio/notebook(s)**: código reproducible que sustente lo mostrado en el video (mismo criterio de reproducibilidad usado en las clases del curso).
- **Si el proyecto es una aplicación de paper**: se debe citar la fuente explícitamente y explicar qué se replicó tal cual y qué se adaptó (datos, features, horizonte, mercado) y por qué.

---

## 2. Criterios de evaluación

La nota final es el promedio ponderado de 7 criterios, cada uno evaluado en una escala de **1 a 5**.

| # | Criterio | Ponderación |
|---|---|---|
| 1 | Formulación del problema y motivación | 15% |
| 2 | Datos e ingeniería de variables | 15% |
| 3 | Validación metodológica (no leakage, walk-forward) | 20% |
| 4 | Modelamiento y comparación de alternativas | 15% |
| 5 | Interpretabilidad y model risk | 10% |
| 6 | Evaluación orientada a decisión (costos, riesgo, backtest) | 15% |
| 7 | Comunicación en el video y reproducibilidad del código | 10% |

---

### Criterio 1 — Formulación del problema y motivación (15%)

| Nivel | Descripción |
|---|---|
| **5 — Excelente** | El problema está formulado con precisión como tarea de ML (target, horizonte, unidad de observación), con motivación de negocio o científica clara y explícita. Si es un paper, se explica por qué ese paper y qué pregunta responde. |
| **4 — Bueno** | Formulación clara pero con algún supuesto no justificado (ej. horizonte elegido sin argumento). |
| **3 — Suficiente** | El problema se entiende pero la definición de target/horizonte es ambigua o cambia a mitad del video. |
| **2 — Insuficiente** | Motivación genérica ("predecir el precio") sin conexión a una decisión o pregunta concreta. |
| **1 — Deficiente** | No queda claro qué problema se está resolviendo. |

### Criterio 2 — Datos e ingeniería de variables (15%)

| Nivel | Descripción |
|---|---|
| **5** | Fuente de datos apropiada y bien documentada (real, no sintética salvo justificación explícita). Features diseñados con criterio financiero (lags, rolling, momentum, indicadores), calculados sin usar información futura. |
| **4** | Buen feature engineering pero con una o dos variables cuya construcción no queda del todo clara. |
| **3** | Features básicos (solo lags simples) sin exploración de alternativas. |
| **2** | Uso de variables cuya construcción sugiere leakage potencial, sin que el equipo lo detecte. |
| **1** | Datos no documentados o variables construidas con información contemporánea/futura al target. |

### Criterio 3 — Validación metodológica: no leakage y walk-forward (20%)

Este es el criterio de mayor peso — es el eje del curso (Sesión 3).

| Nivel | Descripción |
|---|---|
| **5** | Split walk-forward o expanding/rolling window correctamente implementado; todo ajuste (scaler, imputación, selección de features, tuning de hiperparámetros) se hace solo con información pasada respecto de cada fold. Se reporta métrica out-of-time (OOT), no solo un holdout aleatorio. |
| **4** | Validación temporal correcta pero con algún detalle menor de leakage (ej. scaler ajustado con toda la serie antes de particionar). |
| **3** | Usa un split train/test temporal simple (un solo corte) sin walk-forward, pero sin leakage evidente. |
| **2** | Usa `train_test_split` aleatorio o k-fold estándar sobre datos temporales. |
| **1** | Leakage evidente (target usado como feature, normalización con datos futuros, etc.) que invalida los resultados. |

### Criterio 4 — Modelamiento y comparación de alternativas (15%)

| Nivel | Descripción |
|---|---|
| **5** | Se entrena y compara honestamente al menos un modelo clásico (lineal/árbol/boosting) contra el modelo elegido como protagonista (incluyendo deep learning si aplica), con tuning de hiperparámetros documentado y justificación de la métrica de selección. |
| **4** | Comparación presente pero con tuning superficial o sin justificar la métrica. |
| **3** | Un solo modelo entrenado, sin comparación contra baseline. |
| **2** | Modelo aplicado "de caja negra" sin entender ni justificar su configuración. |
| **1** | No hay modelamiento real, o el modelo no corresponde al problema planteado. |

### Criterio 5 — Interpretabilidad y model risk (10%)

| Nivel | Descripción |
|---|---|
| **5** | Se analiza qué variables explican las predicciones (SHAP/feature importance/atención u otro método apropiado a la arquitectura) y se discute estabilidad temporal o riesgo de degradación (drift) del modelo. |
| **4** | Interpretabilidad presente pero sin conexión a decisiones o riesgos concretos. |
| **3** | Se menciona interpretabilidad de forma superficial (una gráfica sin análisis). |
| **2** | No se aborda interpretabilidad ni se justifica su ausencia. |
| **1** | El equipo no puede explicar por qué el modelo predice lo que predice cuando se le pregunta. |

### Criterio 6 — Evaluación orientada a decisión: costos, riesgo, backtest (15%)

| Nivel | Descripción |
|---|---|
| **5** | Las predicciones se conectan a una decisión financiera concreta (señal, portafolio, política de aprobación/rechazo) con backtesting que incorpora costos de transacción u otras fricciones realistas, y métricas de riesgo relevantes (drawdown, turnover, Sharpe, o el análogo apropiado al problema — ej. para crédito: costo de falsos positivos/negativos). |
| **4** | Evaluación de decisión presente pero sin incorporar costos/fricciones. |
| **3** | Solo métricas estadísticas de error (MSE, accuracy, AUC) sin traducción a impacto de negocio. |
| **2** | Métricas reportadas sin ningún análisis de qué significan para la decisión. |
| **1** | No hay evaluación más allá del entrenamiento. |

### Criterio 7 — Comunicación en el video y reproducibilidad (10%)

| Nivel | Descripción |
|---|---|
| **5** | Video claro, dentro del tiempo, estructurado (problema → datos → método → resultados → limitaciones); código reproducible de principio a fin sin intervención manual. |
| **4** | Video ordenado pero excede el tiempo o código requiere pasos manuales menores para reproducir. |
| **3** | Video cubre lo esencial pero desordenado o con partes técnicas no explicadas en lenguaje entendible. |
| **2** | Video incompleto (falta alguna etapa del pipeline) o código no ejecuta sin intervención significativa. |
| **1** | Video no permite entender el proyecto de punta a punta, o el código no es reproducible. |

---

## 3. Escala de nota final

$$\text{Nota} = \sum_i w_i \cdot \text{criterio}_i, \qquad \text{criterio}_i \in [1,5]$$

| Nota promedio ponderada | Equivalente |
|---|---|
| 4.5 – 5.0 | Excelente |
| 3.5 – 4.4 | Bueno |
| 2.5 – 3.4 | Suficiente |
| 1.5 – 2.4 | Insuficiente |
| 1.0 – 1.4 | Deficiente |

---

## 4. Descuentos / causales de no aprobación automática

- **Leakage no detectado por el equipo** (criterio 3 = 1): el proyecto no puede promediar por sobre "Suficiente" independiente del resto de los criterios, dado que invalida los resultados reportados.
- **Plagio de código o de video sin atribución** (en caso de aplicación de paper, no citar la fuente): causal de revisión individual con el equipo docente.
- **Video ausente o ilegible**: nota máxima 1.0 (Deficiente) independiente del código entregado.
