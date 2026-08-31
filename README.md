# Tablero de plantas pesqueras industriales
 
Tablero web del consolidado de licencias de plantas de procesamiento de recursos hidrobiológicos del Perú (1991–2026). Es un único archivo HTML autónomo que se conecta a Google Sheets y se dibuja solo en el navegador.
 
## Qué muestra
 
- **Panorama actual** — KPIs (licencias, empresas únicas, % vigentes, suspendidas y capacidad por actividad), licencias por departamento, distribución por actividad y estado por departamento.
- **Mapa** — mapa del Perú sombreado por número de plantas, con un cuadro por departamento desglosado por tipo de actividad (A.C.P., Harina Normal, Harina Residual, Congelado, Curado y Enlatado).
- **Evolución histórica** — capacidad instalada 1991–2026: harina por tipo (ACP, convencional, residual) y, por separado, enlatado, congelado y curado.
- **Dinámica del padrón** — altas y bajas de licencias por año y padrón acumulado.
- **Detalle** — tabla buscable y ordenable de todas las licencias.
- **Reportes** — dos consultas exportables a PDF o Excel, con filtros propios independientes de la barra superior:
  - *Consulta de planta por tipo de procesamiento y actividad*: listado de plantas filtrable por actividad, subactividad, estado y ubicación. Sale dividido en secciones por actividad y subactividad, con la unidad en la cabecera de la columna **Capacidad**, un total por sección y un resumen general por unidad.
  - *Distribución de establecimientos industriales pesqueros según región*: cuadro de número de plantas y capacidad instalada por región y actividad, con el anexo de otras actividades y, en Excel, una hoja de detalle.

Incluye filtros por departamento, actividad, subactividad (cuando aplica) y estado, además de selector de tema claro/oscuro.
 
## Fuente de datos
 
Lee tres hojas publicadas en la web desde Google Sheets en formato CSV:
 
- **Matriz** — registro maestro de licencias.
- **TENDENCIAS** — series históricas de capacidad.
- **HISTORIAL ELIMINADAS** — licencias canceladas.
Las URLs publicadas están configuradas dentro del archivo (constante `SHEET_URLS`). Al abrir la página descarga esas hojas automáticamente; el botón **↻ Actualizar** vuelve a leerlas sin recargar. Si la descarga falla, permite subir el Excel manualmente como respaldo.
El botón **⤓ Excel** descarga la hoja **Matriz** tal como se está usando: sin normalizar, con todas sus columnas y su encabezado original, y siempre completa (no la afectan los filtros de la barra superior). El archivo resultante se puede volver a cargar en el propio tablero.
 
> Los cambios que se hagan en la hoja de Google se reflejan en el tablero unos minutos después (tiempo que tarda Google en refrescar la versión publicada).
 
## Reglas de negocio aplicadas
 
- **Callao se integra a Lima**: sus plantas se suman a Lima en todas las vistas; el distrito real se conserva en la tabla de detalle.
- **La actividad "Otras" sí se considera** en los KPIs, gráficos y tabla del tablero. En el cuadro por región se aparta a un anexo propio, porque no encaja en las categorías del cuadro oficial.
- La **capacidad** se trata siempre por actividad, nunca como un total único, porque cada actividad usa una unidad distinta (harina t/h, congelado t/día, enlatado cajas/turno, curado t/mes).

## Cómo publicarlo (GitHub Pages)
 
El despliegue está automatizado con GitHub Actions (`.github/workflows/pages.yml`): cada push a `main` publica el sitio.

1. Crea un repositorio **público** y sube el archivo como `index.html`.
2. **Settings → Pages → Source → GitHub Actions**.
3. En 1–2 minutos queda disponible en `https://tu-usuario.github.io/nombre-del-repo/`.
Para actualizar el tablero basta con hacer commit y push del `index.html` a `main`; el workflow se encarga del resto.
 
## Tecnología
 
HTML, CSS y JavaScript sin framework. Usa [SheetJS](https://sheetjs.com/) para leer los CSV/Excel y generar los reportes en Excel, [Chart.js](https://www.chartjs.org/) para los gráficos y [jsPDF](https://github.com/parallax/jsPDF) con [jspdf-autotable](https://github.com/simonbengtsson/jsPDF-AutoTable) para los reportes en PDF, todos vía CDN. La geometría de los departamentos del Perú está incrustada en el propio archivo, por lo que el mapa funciona sin conexión.
 
## Privacidad
 
Al publicar las hojas y alojar la página en un sitio público, **los datos quedan visibles para cualquiera con el enlace**. Si la información debe mantenerse restringida, conviene una alternativa con control de acceso (por ejemplo, un Google Apps Script desplegado como aplicación web que lea la hoja del lado del servidor).
