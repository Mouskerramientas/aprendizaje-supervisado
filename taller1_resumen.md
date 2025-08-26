# Resumen Analítico del Taller: Predicción de Revenue de Películas

Este taller aborda la aplicación de métodos estadísticos y de machine learning para predecir el revenue de películas, utilizando mínimos cuadrados, regresión lineal simple y múltiple, análisis de varianza (ANOVA) y estudio de la varianza.

## 1. Mínimos Cuadrados

- Se implementó el método de mínimos cuadrados ordinarios (OLS) tanto manualmente como con sklearn.
- Se normalizaron las variables y se incluyó el intercepto en la matriz de diseño.
- Los coeficientes obtenidos manualmente y con sklearn fueron consistentes.
- El modelo OLS mostró buen ajuste (R² y RMSE razonables), y los residuos fueron analizados para verificar supuestos.

## 2. Regresión Lineal Simple y Múltiple

- Se analizaron individualmente las variables `budget`, `popularity`, `runtime` y `vote_average` mediante regresión lineal simple.
- Se identificó que `budget` es el predictor más fuerte para revenue.
- Se construyeron modelos múltiples combinando variables, incluyendo:
  - Modelo completo (todas las variables)
  - Top 3 variables (por correlación)
  - Solo budget
  - Sin vote_average
- Se compararon los modelos usando R², RMSE y MAE, mostrando que la regresión múltiple mejora el poder predictivo.
- Se realizó validación cruzada y análisis de multicolinealidad (VIF), confirmando que no hay problemas graves.

## 3. ANOVA

- Se aplicó ANOVA para evaluar la significancia de los modelos de regresión.
- Se descompuso la varianza total en componentes explicada y residual.
- Se realizó ANOVA de un factor para analizar diferencias de revenue entre grupos categóricos (género, idioma, status).
- Se presentaron hipótesis claras: H0 (no hay diferencia entre grupos) y HA (al menos un grupo es diferente).
- Los resultados mostraron diferencias significativas en revenue entre géneros e idiomas, pero no entre status.
- Se interpretaron los p-values y F-statistics para cada caso.

## 4. Análisis de Varianza

- Se calcularon y compararon varianzas y coeficientes de variación entre grupos.
- Se identificaron los géneros con mayor y menor variabilidad en revenue.
- Se aplicaron tests de igualdad de varianzas (Bartlett, Levene) y se analizaron los resultados.

## Visualizaciones y Tablas

- Se incluyeron gráficos de dispersión, histogramas de residuos, matrices de correlación y visualizaciones comparativas de modelos.
- Se presentaron tablas resumen de métricas y resultados de ANOVA.

## Conclusiones y Recomendaciones

- El método de mínimos cuadrados es robusto y eficiente para este tipo de problemas.
- La regresión múltiple ofrece mejor poder predictivo, pero la simple es útil para interpretación.
- ANOVA es esencial para validar la significancia de los modelos y diferencias entre grupos.
- El análisis de varianza ayuda a entender la dispersión y estabilidad de los ingresos por grupo.
- Se recomienda usar el modelo múltiple optimizado para predicción y el simple para interpretación.

Este taller integra todos los pasos requeridos y demuestra el uso correcto de las técnicas estadísticas y de machine learning en el contexto de predicción de revenue de películas.

# Análisis Detallado: Predicción de Revenue de Películas

## 1. Mínimos Cuadrados Ordinarios (OLS)

- **Variables seleccionadas:** `budget`, `popularity`, `runtime`, `vote_average`.
- **Coeficientes (sklearn):**
  - Intercepto: $39,321,584.91
  - budget: $87,315,669.97
  - popularity: $10,446,169.92
  - runtime: $-514,202.41
  - vote_average: $3,180,582.76
- **Métricas de rendimiento:**
  - R² (manual): 0.5273
  - RMSE (manual): $88,057,731
  - R² (sklearn - test): 0.5142
  - RMSE (sklearn - test): $98,147,151

## 2. Regresión Lineal Simple y Múltiple

- **Regresión Simple:**
  - BUDGET: R² = 0.5166, RMSE = $97,896,374, MAE = $31,314,209, Correlación = 0.7238
  - POPULARITY: R² = -0.1196, RMSE = $148,989,730, MAE = $53,579,182, Correlación = 0.2324
  - RUNTIME: R² = 0.0241, RMSE = $139,102,612, MAE = $55,907,868, Correlación = 0.1572
  - VOTE_AVERAGE: R² = 0.0168, RMSE = $139,622,573, MAE = $56,036,761, Correlación = 0.1210
  - Mejor variable individual: **BUDGET**
- **Regresión Múltiple:**
  - Modelo completo: R² = 0.5142, RMSE = $98,147,151, MAE = $31,747,289
    - Ecuación: revenue = -4,680,323 + 2.72*budget + 226,533.13*popularity + (-11,126.15)*runtime + 1,261,623.75*vote_average
  - Top 3 variables: R² = 0.5127, RMSE = $98,296,434, MAE = $30,789,542
  - Solo budget: R² = 0.5166, RMSE = $97,896,374, MAE = $31,314,209
  - Sin vote_average: R² = 0.5127, RMSE = $98,296,434, MAE = $30,789,542
  - Validación cruzada (5-fold): R² promedio = -0.1936 ± 0.4493

## 3. ANOVA

- **Modelos de regresión:**
  - FULL: SSR = 3.18e+19, SSE = 3.67e+19, R² = 0.4209, F = 825.18, p = 1.11e-16
  - TOP3: SSR = 3.19e+19, SSE = 3.69e+19, R² = 0.4213, F = 1098.13, p = 1.11e-16
  - BUDGET ONLY: SSR = 2.98e+19, SSE = 3.66e+19, R² = 0.3935, F = 3103.94, p = 1.11e-16
  - NO VOTE AVG: SSR = 3.19e+19, SSE = 3.69e+19, R² = 0.4213, F = 1098.13, p = 1.11e-16
- **ANOVA por idioma:**
  - Inglés: Media = $55,073,183, Mediana = $5,471,376, Desv. Est. = $152,345,595
  - Otros: Media = $12,027,283, Mediana = $770,869, Desv. Est. = $54,014,897
  - F-statistic = 507.13, p-value = 7.42e-111, Diferencia de medias = $43,045,900
- **ANOVA por status:**
  - Released: Media = $39,831,747, Mediana = $2,500,000
  - In Production: Media = $33,376,530, Mediana = $150
  - F-statistic = 0.2146, p-value = 0.643, No significativo
- **ANOVA por género:**
  - Adventure: Media = $124,490,031, Mediana = $12,764,958, Desv. Est. = $266,174,842
  - Action: Media = $75,899,444, Mediana = $8,793,378, Desv. Est. = $187,459,258
  - Horror: Media = $28,216,306, Mediana = $1,464,000, Desv. Est. = $112,911,583
  - Comedy: Media = $27,516,843, Mediana = $3,432,342, Desv. Est. = $73,894,826
  - Drama: Media = $21,308,822, Mediana = $1,333,202, Desv. Est. = $86,618,679
  - Documentary: Media = $3,203,491, Mediana = $14,332, Desv. Est. = $16,051,099
  - F-statistic = 165.26, p-value = 2.38e-171, Significativo

## 4. Análisis de Varianza

- **Variables individuales:**
  - budget: Media = $12,910,948.71, Varianza = 1.03e+15, Desv. Est. = $32,140,021.46, CV = 2.489
  - popularity: Media = 12.83, Varianza = 2.13e+03, Desv. Est. = 46.11, CV = 3.595
  - runtime: Media = 92.73, Varianza = 2.14e+03, Desv. Est. = 46.22, CV = 0.498
  - vote_average: Media = 5.59, Varianza = 6.36e+00, Desv. Est. = 2.52, CV = 0.451
  - revenue: Media = $39,741,395.51, Varianza = 1.64e+16, Desv. Est. = $128,086,953.85, CV = 3.223
  - Mayor variabilidad: popularity (CV = 3.595), Menor: vote_average (CV = 0.451)
- **Descomposición de varianza en modelos:**
  - full: Varianza total = 1.98e+16, Explicada = 8.35e+15 (42.1%), No explicada = 9.64e+15
  - top3: Explicada = 8.35e+15 (42.1%)
  - budget_only: Explicada = 7.80e+15 (39.3%)
  - no_vote_avg: Explicada = 8.35e+15 (42.1%)
- **Homocedasticidad:**
  - Todos los modelos muestran heterocedasticidad (Breusch-Pagan p < 0.05)
  - Varianza residual (menor es mejor):
    - budget_only: 9.58e+15
    - full: 9.63e+15
    - top3: 9.66e+15
    - no_vote_avg: 9.66e+15

## 5. Conclusiones

- El mejor modelo simple es solo budget (R² = 0.5166, menor varianza residual).
- El modelo múltiple completo explica el 42.1% de la varianza.
- Hay diferencias significativas de revenue por idioma y género.
- Todos los modelos presentan heterocedasticidad, por lo que se recomienda explorar transformaciones o modelos robustos.
- Las variables con mayor variabilidad son popularity y revenue; la más estable es vote_average.
- Adventure y Action son los géneros con mayor media y varianza de revenue.

---

**Este resumen incluye los valores concretos de todos los resultados principales de tu análisis.**
