# Optimización Logística en E-Commerce: Análisis de Olist

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow)](https://powerbi.microsoft.com/)
[![Status](https://img.shields.io/badge/Status-Completado-green)]()

> **Nota:** Este proyecto es parte del portafolio profesional para la postulación al cargo de *Data Analyst* en **Datalized**. Se basa en una adaptación ejecutiva de mi Memoria de Título de Ingeniería Civil Industrial (UTFSM).

## 1. Contexto y Problema de Negocio

En el ecosistema del comercio electrónico brasileño, la logística es el principal factor de fricción debido a la complejidad geográfica del país. El dataset público de **Olist** ofrece una visión transaccional, pero carece de variables logísticas profundas.

**La Pregunta Analítica:**
> *¿Qué factores operativos y geográficos están generando las mayores brechas (Gaps) entre la promesa de venta y la entrega real, impactando la satisfacción del cliente?*

Este proyecto no se limita a visualizar los datos entregados, sino que enriquece el modelo con **datos externos de infraestructura vial y calendarios festivos** para contrastar la teoría (distancia lineal) con la realidad operativa.

## 2. Arquitectura de la Solución

El flujo de trabajo sigue un pipeline de datos estructurado para garantizar la reproducibilidad y la calidad del dato ("Golden Record").

```
Raw Data Olist + Datos Propios
            ↓
    ETL & Cleaning (Python/Pandas)
            ↓
    Feature Engineering
            ↓
    Dataset Maestro
          ↙   ↘
    Power BI    Modelos ML
    Dashboard   
```

### Tecnologías Utilizadas

- **Procesamiento:** Python (Pandas, NumPy)
- **Análisis Exploratorio:** Jupyter Notebooks, Seaborn, Matplotlib
- **Visualización:** Microsoft Power BI
- **Control de Versiones:** Git / GitHub

## 3. Metodología de Procesamiento (ETL)

El procesamiento se encuentra detallado en el notebook `notebooks/01_ETL_y_Feature_Engineering.ipynb`. Los hitos principales son:

### A. Ingesta y Enriquecimiento

Se integraron las 8 tablas relacionales de Olist con dos fuentes de datos propietarias:

- **Matriz de Distancias Viales:** Datos reales de rutas por carretera entre estados (construida manualmente desde [distanciaentreascidades.com.br](https://www.distanciaentreascidades.com.br)), superando la limitación de la distancia Haversine (lineal).
- **Calendario de Festivos:** Para calcular el impacto de días no hábiles en el Lead Time.

### B. Reglas de Negocio y Limpieza

- **Integridad de la Variable Dependiente:** Se eliminaron registros sin fecha de entrega para evitar sesgos en el cálculo de tiempos.
- **Imputación Inteligente:**
  - *Reviews:* Se imputó "without comments" para no perder feedback cuantitativo.
  - *Dimensiones:* Se normalizaron productos sin dimensiones con valores mínimos técnicos para evitar errores de cálculo volumétrico.

### C. Definición de Variables del Modelo

Se estructuró el dataset final diferenciando claramente las variables para el modelo predictivo:

- **Variable Dependiente ($Y$):**
  - `order_delivery_time`: Tiempo real de entrega en días.

- **Variables Independientes ($X$):**
  - `distance_km`: Variable crítica de distancia real por carretera.
  - `product_volume_cm3`: Cálculo cúbico para análisis de estiba.
  - `is_holiday`: Variable binaria ($1$/$0$) para aislar el efecto estacional.

## 4. Visualización (Power BI)

El dashboard interactivo permite navegar desde el panorama general hasta el detalle operativo, respondiendo a la pregunta de negocio planteada.

👉 [Ver Dashboard Interactivo en Power BI](url powerbi en mi sitio web)

*(Nota: El dashboard es público y no requiere credenciales de acceso)*

## 5. Estructura del Repositorio

```
├── data/
│   ├── raw/             # Datasets originales (Olist) + Excel auxiliares
│   └── processed/       # Salida del ETL (CSV listos para Power BI)
├── notebooks/
│   └── 01_ETL_y_Feature_Engineering.ipynb  # Código fuente documentado
├── references/
│   ├── schema.png       # Modelo relacional
│   └── memoria_titulo.pdf                  # Documento académico de respaldo
├── README.md            # Documentación del proyecto
└── requirements.txt     # Dependencias de Python
```

## 6. Cómo Ejecutar este Proyecto

### Clonar el repositorio

```bash
git clone https://github.com/TU_USUARIO/TU_REPO.git
cd TU_REPO
```

### Instalar dependencias

```bash
pip install -r requirements.txt
```

### Ejecutar el Notebook

Abrir `notebooks/01_ETL_y_Feature_Engineering.ipynb` y ejecutar las celdas secuencialmente. El proceso generará los archivos en `data/processed/`.

## 7. Autor

**Francisco Mora**  
Ingeniero Civil Industrial & Informático | UTFSM

- [LinkedIn](https://www.google.com/search?q=TU_LINK_DE_LINKEDIN)
- [Portafolio Web](https://www.google.com/search?q=TU_SITIO_WEB_DEV)



