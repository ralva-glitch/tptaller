# StreamAI: Recomendador de Contenido de Streaming

Página web que presenta un dashboard de análisis y un sistema de recomendación de películas y series sobre un
dataset combinado de Netflix, Disney+, Prime Video, HBO Max y Apple TV+.

## Contenido

```
.
├── index.html          # Pagina Web
├── app.js               # Lógica: KPIs, gráficos, filtros y motor de similitud (TF-IDF)
├── dataset_embed.js     # Dataset (800 títulos) embebido como variable JS
└── scripts/
    └── generate_dataset.py   # Script opcional para regenerar el dataset (Python)
```

## Funcion de la pagina web 

- **Home**: presentación del proyecto y catálogo por plataforma con conteo real de títulos.
- **Dashboard**: KPIs (total de títulos, puntaje promedio, género más frecuente, mejor plataforma) y tres gráficos con Chart.js (distribución por plataforma, por género y evolución por año).
- **Sistema de recomendación**:
  - Filtros estructurados por género, plataforma, tipo (película/serie) y puntaje mínimo.
  - Buscador de títulos similares basado en un motor de similitud de contenido (TF-IDF + similitud de coseno) implementado en JavaScript puro sobre la descripción y el género de cada título.

## Dataset

El archivo `dataset_embed.js` contiene una muestra de 800 títulos, con un esquema
equivalente al dataset público *"Netflix Movies and TV Shows"* de Kaggle,
extendido con la columna `plataforma` para cubrir los 5 servicios de
streaming. Columnas: `show_id`, `titulo`, `tipo`, `plataforma`, `director`,
`elenco`, `pais`, `fecha_agregado`, `anio_lanzamiento`, `clasificacion`,
`duracion`, `genero`, `descripcion`, `puntaje`.
