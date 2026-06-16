# StreamAI · Recomendador de Contenido de Streaming

Página web estática (HTML + CSS + JavaScript puro) que presenta un dashboard
de análisis y un sistema de recomendación de películas y series sobre un
dataset combinado de Netflix, Disney+, Prime Video, HBO Max y Apple TV+.

No requiere backend, servidor ni instalación de dependencias: el dataset
viene embebido en `dataset_embed.js` y todo el procesamiento (KPIs, gráficos,
filtros y motor de similitud) corre en el navegador.

## Contenido del repositorio

```
.
├── index.html          # Estructura y estilos de la página
├── app.js               # Lógica: KPIs, gráficos, filtros y motor de similitud (TF-IDF)
├── dataset_embed.js     # Dataset (800 títulos) embebido como variable JS
└── scripts/
    └── generate_dataset.py   # Script opcional para regenerar el dataset (Python)
```

## Cómo ejecutar la página

### Opción 1 — Abrir directamente (más simple)
Hacé doble clic sobre `index.html`, o abrilo con clic derecho → "Abrir con" →
tu navegador. Funciona sin servidor porque no usa `fetch` para cargar el
dataset (está embebido directamente en `dataset_embed.js`).

### Opción 2 — Servidor local (recomendado para desarrollo)
Algunos navegadores aplican restricciones a archivos abiertos con `file://`.
Si notás que los gráficos no cargan, levantá un servidor local desde la
carpeta del proyecto:

```bash
# Con Python ya instalado
python3 -m http.server 8000

# o con Node.js
npx serve .
```

Luego abrí `http://localhost:8000` en el navegador.

### Opción 3 — GitHub Pages
1. Subí este repositorio a GitHub.
2. Activá GitHub Pages: Settings → Pages → Source: rama `main`, carpeta `/ (root)`.
3. La página queda disponible en `https://<usuario>.github.io/<repositorio>/`.

## Funcionalidades

- **Home**: presentación del proyecto y catálogo por plataforma con conteo real de títulos.
- **Dashboard**: KPIs (total de títulos, puntaje promedio, género más frecuente, mejor plataforma) y tres gráficos con Chart.js (distribución por plataforma, por género y evolución por año).
- **Sistema de recomendación**:
  - Filtros estructurados por género, plataforma, tipo (película/serie) y puntaje mínimo.
  - Buscador de títulos similares basado en un motor de similitud de contenido (TF-IDF + similitud de coseno) implementado en JavaScript puro sobre la descripción y el género de cada título.

## Dataset

El archivo `dataset_embed.js` contiene una muestra de 800 títulos (subconjunto
representativo de un dataset combinado de 5.000 registros), con un esquema
equivalente al dataset público *"Netflix Movies and TV Shows"* de Kaggle,
extendido con la columna `plataforma` para cubrir los 5 servicios de
streaming. Columnas: `show_id`, `titulo`, `tipo`, `plataforma`, `director`,
`elenco`, `pais`, `fecha_agregado`, `anio_lanzamiento`, `clasificacion`,
`duracion`, `genero`, `descripcion`, `puntaje`.

Si querés regenerar o ampliar el dataset, podés correr el script opcional
incluido en `scripts/generate_dataset.py` (requiere Python 3 con `pandas` y
`numpy` instalados):

```bash
pip install pandas numpy
python3 scripts/generate_dataset.py
```

Esto genera un CSV nuevo; para volver a embeberlo en la web hay que
convertirlo a JSON y pegarlo como valor de la constante `DATASET` dentro de
`dataset_embed.js`.

## Tecnologías

- HTML5 / CSS3 (variables CSS, grid, flexbox, diseño responsive)
- JavaScript (ES6+), sin frameworks
- [Chart.js](https://www.chartjs.org/) (CDN) para los gráficos
- Google Fonts (Bebas Neue + Inter)
