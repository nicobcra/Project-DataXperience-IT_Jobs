# Proyecto Final DataXperience — Análisis de Ofertas de Empleo en TI

Análisis completo de ciencia de datos sobre el **Global IT Job Listings Dataset**
(Kaggle), desarrollado como proyecto final del curso **DataXperience**. Recorre el
ciclo completo: preparación de datos, análisis estadístico y modelado + comunicación.

**Programa:** Ingeniería de Sistemas

**Integrantes:** Alejandra Leguizamon · Francy Atehortua · Nicolás Becerra

**Fecha:** agosto–septiembre de 2026

---

## Dataset

- **Fuente:** [Global IT Job Listings Dataset](https://www.kaggle.com/datasets/himelsarder/global-it-job-listings-dataset) — Kaggle, autor *himelsarder*. Uso educativo.
- **Original:** 2.500 filas × 4 columnas (`Job Title`, `Company Name`, `Location`, `Experience (Years)`).
- **Depurado:** 2.283 filas × 6 columnas tras la limpieza del Módulo 1.

---

## Estructura del proyecto (3 etapas)

### Etapa 1 — Módulo 1: Fundamentos y Preparación de Datos
Exploración y limpieza sin alterar el original: eliminación de 216 duplicados exactos
+ 1 duplicado oculto que apareció al normalizar `Location`, imputación de 104
ubicaciones nulas como `"Unknown"`, limpieza de 43 textos con el token literal `null`,
transformación de `Experience (Years)` (texto tipo `"3 - 8 Years"`) en las variables
numéricas `Min Experience` y `Max Experience`, y corrección de 4 errores ortográficos.
**Salida:** `data/IT_jobs_clean.csv` (2.283 × 6).

### Etapa 2 — Módulo 2: Análisis Estadístico
Estadística descriptiva sobre el dataset limpio. Variables derivadas: `Experiencia
Media`, `Rango Experiencia`, `Num Ubicaciones`. Cubre tendencia central, posición
(cuartiles/deciles/percentiles), dispersión y coeficiente de variación, forma
(asimetría/curtosis), comparación de subgrupos (local vs. exterior), correlación,
detección de outliers (regla IQR), escalado (Min-Max y Z-score) e hipótesis.
**Hallazgo central:** la experiencia requerida sigue una distribución asimétrica
positiva, no normal. **Salida:** `data/IT_jobs_modulo2.csv` (2.283 × 10).

### Etapa 3 — Módulo 3: Modelado, Visualización y Storytelling
Cinco visualizaciones (barras, histograma, diagrama de caja, diagrama de violín,
dispersión), un modelo predictivo de **regresión lineal** (simple y múltiple) evaluado
con `train/test`, métricas (R², MAE, MSE/RMSE) y **validación cruzada k-fold**, un
modelo de **regresión logística** para clasificación evaluado con matriz de confusión
y métricas (accuracy, precisión, recall, F1, AUC), una narrativa de datos
(planteamiento–desarrollo–cierre) y una propuesta de aplicación profesional. Variable
nueva: `Nivel Titulo` (senior/medio/junior a partir del texto del título).
**Salida:** `data/IT_jobs_modulo3.csv` (2.283 × 15).

---

## Resultados principales

| Resultado | Valor |
|---|---|
| Nivel del título | medio 63,6 % · senior 29,9 % · junior 6,4 % |
| Experiencia media por nivel | junior 1,4 · medio 4,5 · senior 7,4 años |
| Ofertas al exterior | 350 (15,3 %) — experiencia media 6,1 vs. 5,0 años |
| Correlación experiencia mínima–máxima | 0,931 |
| **Regresión lineal simple** (`Max ~ Min`) | `Max ≈ 2,82 + 1,19·Min` · R² 0,868 · MAE 1,16 años · RMSE 1,45 |
| **Regresión lineal múltiple** (`Max ~ Min + exterior + nº ubicaciones + nivel`) | R² 0,893 · MAE 0,98 años · RMSE 1,30 |
| Validación cruzada (5 folds) | simple R² 0,865 ± 0,007 · múltiple R² 0,888 ± 0,007 (sin sobreajuste) |
| **Regresión logística** (oferta al exterior) | accuracy 0,59 · precisión 0,23 · recall 0,73 · F1 0,35 · **AUC 0,66** (capacidad de discriminación limitada) |

---

## Estructura del repositorio

```
.
├── README.md
├── requirements.txt
├── notebooks/
│   └── DataXperience_IT_Jobs_Analysis.ipynb   # notebook completo (Módulos 1, 2 y 3)
├── data/
│   ├── IT_jobs.csv            # dataset original (Kaggle)
│   ├── IT_jobs_clean.csv      # salida del Módulo 1
│   ├── IT_jobs_modulo2.csv    # salida del Módulo 2
│   └── IT_jobs_modulo3.csv    # salida del Módulo 3
├── docs/
└── presentacion/                        # video / diapositivas de la entrega
```

---

## Cómo reproducir el análisis

### Opción A — Google Colab (recomendada)
1. Sube `notebooks/DataXperience_IT_Jobs_Analysis.ipynb` a [Google Colab](https://colab.research.google.com/).
2. Sube `data/IT_jobs.csv` al panel de archivos.
3. Ejecuta *Entorno de ejecución → Ejecutar todas*. El notebook genera por sí mismo
   `IT_jobs_clean.csv`, `IT_jobs_modulo2.csv` e `IT_jobs_modulo3.csv`.

### Opción B — Local
```bash
python -m venv .venv
# Windows:  .venv\Scripts\activate
# Linux/Mac: source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook notebooks/DataXperience_IT_Jobs_Analysis.ipynb
```

---

## Entregable

Video de 5 minutos que explica las tres etapas del proyecto, con interpretación
personal y aplicación profesional.

---

## Créditos y licencia

Trabajo académico del curso DataXperience. El dataset pertenece a su autor original en
Kaggle y se utiliza con fines educativos, citando la fuente. El código de este
repositorio puede reutilizarse libremente con fines educativos.
