# Tablero de plantas pesqueras industriales
 
Tablero web del consolidado de licencias de plantas de procesamiento de recursos hidrobiológicos del Perú (1991–2026). Es un único archivo HTML autónomo que se conecta a Google Sheets y se dibuja solo en el navegador.
 
## Qué muestra
 
- **Panorama actual** — KPIs (licencias, empresas únicas, % vigentes, suspendidas y capacidad por actividad), licencias por departamento, distribución por actividad y estado por departamento.
- **Mapa** — mapa del Perú sombreado por número de plantas, con un cuadro por departamento desglosado por tipo de actividad (A.C.P., Harina Normal, Harina Residual, Congelado, Curado y Enlatado).
- **Evolución histórica** — capacidad instalada 1991–2026: harina por tipo (ACP, convencional, residual) y, por separado, enlatado, congelado y curado.
- **Dinámica del padrón** — altas y bajas de licencias por año y padrón acumulado.
- **Detalle** — tabla buscable y ordenable de todas las licencias.
Incluye filtros por departamento, actividad, subactividad (cuando aplica) y estado, además de selector de tema claro/oscuro.
 
## Fuente de datos
 
Lee tres hojas publicadas en la web desde Google Sheets en formato CSV:
 
- **Matriz** — registro maestro de licencias.
- **TENDENCIAS** — series históricas de capacidad.
- **HISTORIAL ELIMINADAS** — licencias canceladas.
Las URLs publicadas están configuradas dentro del archivo (constante `SHEET_URLS`). Al abrir la página descarga esas hojas automáticamente; el botón **↻ Actualizar** vuelve a leerlas sin recargar. Si la descarga falla, permite subir el Excel manualmente como respaldo.
 
> Los cambios que se hagan en la hoja de Google se reflejan en el tablero unos minutos después (tiempo que tarda Google en refrescar la versión publicada).
 
## Reglas de negocio aplicadas
 
- **Callao se integra a Lima**: sus plantas se suman a Lima en todas las vistas; el distrito real se conserva en la tabla de detalle.
- **La actividad "Otras" no se considera** en ningún indicador, gráfico ni cuadro.
- La **capacidad** se trata siempre por actividad, nunca como un total único, porque cada actividad usa una unidad distinta (harina t/h, congelado t/día, enlatado cajas/turno, curado t/mes).
## Cómo publicarlo (GitHub Pages)
 
1. Crea un repositorio **público** y sube el archivo como `index.html`.
2. **Settings → Pages → Deploy from a branch → main → / (root) → Save**.
3. En 1–2 minutos queda disponible en `https://tu-usuario.github.io/nombre-del-repo/`.
Para actualizar el tablero, vuelve a subir el `index.html` sobre el anterior.
 
## Tecnología
 
HTML, CSS y JavaScript sin framework. Usa [SheetJS](https://sheetjs.com/) para leer los CSV/Excel y [Chart.js](https://www.chartjs.org/) para los gráficos, ambos vía CDN. La geometría de los departamentos del Perú está incrustada en el propio archivo, por lo que el mapa funciona sin conexión.
 
## Privacidad
 
Al publicar las hojas y alojar la página en un sitio público, **los datos quedan visibles para cualquiera con el enlace**. Si la información debe mantenerse restringida, conviene una alternativa con control de acceso (por ejemplo, un Google Apps Script desplegado como aplicación web que lea la hoja del lado del servidor).
