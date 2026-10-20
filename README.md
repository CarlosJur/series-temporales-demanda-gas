# Series temporales · Demanda de gas natural en España

Proyecto de la asignatura *Análisis Avanzado de Series Temporales* (GRDAN 2627 · ESIC University).
Es una práctica transversal: un mismo caso, **la demanda de gas natural en España**, se trabaja en varias fases con técnicas cada vez más avanzadas.

| Fase | Técnica | Estado |
|---|---|---|
| **P1** · [`p1-gas/`](p1-gas/) | Exploración, descomposición y métodos de referencia (Nixtla `statsforecast`) | ✅ Entregada |
| X6 | Suavizado exponencial (ETS) | ⏳ Pendiente |
| X7-X8 | ARIMA / SARIMA | ⏳ Pendiente |
| X9 | Temperatura como variable externa | ⏳ Pendiente |

## Estructura del repositorio

```
proyecto_gas/
├── README.md                         ← este archivo
├── requirements.txt                  ← dependencias con versión fija
├── .gitignore                        ← ignora .venv/, data/ y *.csv
├── .venv/                            ← entorno virtual (no se versiona)
└── p1-gas/
    ├── README.md                     ← ficha de la fuente y resumen de la P1
    ├── p1_gas_demanda_invierno.ipynb ← notebook ejecutado
    └── data/                         ← CSV descargado desde el código (no se versiona)
```

## Puesta en marcha

Hace falta **Python 3.13**.

```powershell
# 1. Clonar
git clone https://github.com/CarlosJur/series-temporales-demanda-gas.git
cd series-temporales-demanda-gas

# 2. Crear y activar el entorno virtual
python -m venv .venv
.venv\Scripts\activate            # Windows
# source .venv/bin/activate       # macOS / Linux

# 3. Instalar dependencias
pip install -r requirements.txt

# 4. Registrar el kernel de Jupyter del proyecto
python -m ipykernel install --sys-prefix --name proyecto-gas --display-name "Python (proyecto-gas)"

# 5. Abrir el notebook
jupyter lab p1-gas/p1_gas_demanda_invierno.ipynb
```

## Buenas prácticas del repositorio

- **Los datos no se versionan.** Cada notebook descarga sus datos de la fuente oficial al ejecutarse.
- **Entorno reproducible.** Las versiones de `requirements.txt` están fijadas y el notebook usa el kernel `proyecto-gas`.
- **Notebooks ejecutados de principio a fin** antes de cada entrega (`nbconvert --execute`).

## Autor

Carlos Jurado · ESIC University
