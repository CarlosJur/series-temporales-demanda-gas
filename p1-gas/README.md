# P1 · ¿Cuánto gas necesitará España este invierno?

Práctica transversal 1 de *Análisis Avanzado de Series Temporales* (GRDAN 2627 · ESIC University).
Predicción mensual de la demanda de gas natural en España para el invierno **octubre de 2026 - marzo de 2027**, con métodos de referencia (suite Nixtla) y recomendaciones para el Ministerio para la Transición Ecológica.

📓 **Notebook:** [`p1_gas_demanda_invierno.ipynb`](p1_gas_demanda_invierno.ipynb), entregado ya ejecutado.

---

## Ficha de la fuente

| | |
|---|---|
| **Quién la publica y quién la produce** | La publica la **CNMC** en su catálogo de datos abiertos (conjunto [`ds_24333_1`](https://catalogodatos.cnmc.es/dataset/ds_24333_1), «Evolución diaria de la demanda de gas en España»). La produce **Enagás GTS**, el Gestor Técnico del Sistema gasista, a partir de sus mediciones de operación. |
| **Frecuencia, cobertura y unidad** | **Diaria**, para todo el sistema gasista español, desde el **1-ene-2009** hasta el **31-mar-2026** (6.299 días sin huecos). La unidad es **MWh/día**. |
| **Qué componentes separa** | Tres: demanda **convencional por gasoducto**, demanda **convencional en cisternas de GNL** y **sector eléctrico** (gas para ciclos combinados). |
| **Con qué retraso se actualiza** | **Trimestral.** La versión de septiembre de 2026 llega hasta marzo de 2026, unos **6 meses de retraso**. Por eso la predicción se contrasta con los avances mensuales de Enagás. |
| **Licencia** | **CC BY-SA 4.0**: uso libre citando a la CNMC y compartiendo las obras derivadas con la misma licencia. |
| **Por qué es mejor que las alternativas** | Es la única serie oficial **diaria**, larga (desde 2009), descargable por API y con la **separación entre convencional y eléctrico**. **Eurostat** es mensual, va con más retraso y no separa la generación eléctrica de forma homogénea. **CORES** da consumos mensuales sin detalle diario. Los **informes de Enagás** son PDF mensuales provisionales y redondeados, útiles como avance pero no como serie histórica. |

---

## Qué contiene el notebook

| Bloque | Contenido |
|---|---|
| **A · Datos** | Descarga desde el código (API CKAN de la CNMC), controles de calidad (huecos, duplicados, unidades y atípicos), construcción del total y de los componentes en formato largo, y peso de cada componente. |
| **B · Serie diaria** | Gráfico temporal con medias móviles, gráficos estacionales anual y semanal, diagramas de retardos, ACF y análisis de 2022. |
| **C · Descomposición** | Agregación mensual (media diaria, que corrige el calendario), decisión sobre Box-Cox, descomposición clásica frente a STL, MSTL diaria (7 y 365 días) y reparto de la varianza. |
| **D · Listón** | Prueba con los últimos 12 meses y cuatro métodos (media, naïve, seasonal naïve y drift) sobre tres series con `StatsForecast`. Métricas: MAE, RMSE, MAPE y sesgo. |
| **E · Residuos** | Gráfico temporal, ACF, histograma y Ljung-Box del mejor método de cada serie. |
| **F · Predicción** | Invierno 2026/27 en TWh/mes, comparación con los inviernos anteriores, contraste con Enagás (abril-agosto de 2026, más septiembre), escenario corregido, tres recomendaciones y limitaciones. |

### Resultados principales

- **Predicción del invierno 2026/27: ≈ 188 TWh** (rango central de 184 a 193 TWh), con picos en diciembre (35 TWh) y enero (36 TWh).
- **Métodos ganadores:** seasonal naïve para el total (MAPE 6,9 %) y para la convencional (4,5 %). En el sector eléctrico gana la media (17,9 %), pero no se mantiene fuera de muestra.
- **Contraste con Enagás (abril-agosto de 2026):** el total se desvía un −1,8 %; la convencional se sobreestima un +4,4 % y el sector eléctrico se infraestima un −17,7 %.

---

## Cómo reproducirlo

Desde la raíz del repositorio, con el entorno ya creado (ver el [README principal](../README.md)):

```bash
cd p1-gas
python -m nbconvert --to notebook --execute --inplace p1_gas_demanda_invierno.ipynb
```

- La primera ejecución descarga el CSV de la CNMC en `p1-gas/data/`, una carpeta que **Git ignora**. Para forzar una descarga nueva hay que poner `REFRESH = True` en la celda de descarga.
- Los avances de Enagás («Progreso mensual de la demanda», marzo-septiembre de 2026) están transcritos en el notebook a partir de los PDF oficiales, con la URL de cada uno.
- Tiempo de ejecución: menos de 1 minuto.

## Fuentes

- CNMC, *Evolución diaria de la demanda de gas en España* (Enagás GTS): <https://catalogodatos.cnmc.es/dataset/ds_24333_1>
- Enagás GTS, *Progreso mensual de la demanda* (2026): `https://www.enagas.es/content/dam/enagas/es/ficheros/gestion-tecnica-sistema/energy-data/publicaciones/demanda-de-gas/demanda-mensual/Progreso_<mes>26.pdf`
- Hyndman, R. J. y Athanasopoulos, G., *Forecasting: Principles and Practice* (3.ª ed.), OTexts.
- Nixtla, documentación de `statsforecast` y `utilsforecast`: <https://nixtlaverse.nixtla.io/>
