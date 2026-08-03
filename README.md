# Legajo · Seguimiento de carrera

Sitio estático de una sola página (`index.html`) que muestra el avance de tu carrera a partir de tu planilla de materias: aprobadas, cursando, pendientes, promedio, disponibilidad para cursar y el cronograma vigente.

No depende de ningún backend ni de abrir el archivo manualmente: los datos están embebidos en el propio HTML, así que alcanza con publicarlo como sitio estático.

## Publicarlo con GitHub Pages (gratis)

1. Creá un repositorio nuevo en GitHub (público, para que Pages sea gratis) — por ejemplo `carrera-tracker`.
2. Desde esta carpeta, corré:

   ```bash
   git remote add origin https://github.com/TU_USUARIO/carrera-tracker.git
   git branch -M main
   git push -u origin main
   ```

3. En GitHub: **Settings → Pages → Source → Deploy from a branch**, elegí la branch `main` y la carpeta `/ (root)`.
4. En un par de minutos el sitio queda publicado en:

   `https://TU_USUARIO.github.io/carrera-tracker/`

## Las cinco vistas

- **Graph view** — el plan como grafo de correlativas. Hover sobre una materia bloqueada resalta la cadena que te falta. Lo que busques en el explorador de la izquierda se resalta también acá. Los ajustes del panel derecho (fuerzas, tamaños, "resaltar disponibles", "atenuar aprobadas") y los años visibles se guardan entre sesiones.
- **Avance** — porcentaje, promedio, cuántas te faltan y una estimación de cuántos cuatrimestres quedan. Las barras por año están apiladas: aprobada / cursando / disponible / bloqueada. Abajo, la distribución de notas de final.
- **Cronograma** — auto-armado de horario a partir de la oferta, y opciones manuales con grilla semanal, horas totales y detección de superposiciones.
- **Legajo** — la tabla completa con filtros, búsqueda, orden y exportación a CSV.
- **Planificador** — qué conviene cursar según cuántas materias destraba cada una, con la proyección hasta el título y hasta el intermedio.

## Actualizar tus materias

Los datos viven en el array `SEED` dentro de `index.html` (buscá `const SEED = [...]`). Podés:

- Editarlo a mano (cada materia es `{codigo, nombre, condicion, disponibilidad, nota, anio, intermedio}`), o
- Pedirme que regenere el archivo a partir de una versión nueva de tu Excel.

`condicion` acepta: `"Aprobada"`, `"Cursada"` (cursada, final pendiente) o `"No aprobada"`.
`disponibilidad` e `intermedio` **no hace falta cargarlos**: se recalculan solos a partir de `PREREQS` y del plan oficial.

### Correlativas

`PREREQS` mapea código → array de códigos que hay que tener aprobados. Ojo con la diferencia:

- `3632: []` significa *no tiene correlativas*.
- Que un código **no figure** significa *correlativas sin cargar*. La materia va a aparecer como disponible igual (no hay mejor dato), pero marcada con un asterisco rojo en el Legajo y con un aviso en el detalle. Hoy pasa con `3677`, `3678` y `3679`.

## La oferta de comisiones

`OFERTA_2C_2026` tiene el formato `[codigo, [[comision, dias, horaInicio, horaFin], ...]]`, donde `dias` es `"Lu"`, `"Ma,Vi"`, etc., o `null` para las materias a distancia. Se puede reemplazar sin tocar el código: **Importar JSON** en la pestaña Cronograma. El botón **Exportar** baja la oferta actual y sirve de plantilla.

El botón **PDF** necesita un endpoint propio (se configura con ⚙) que reciba `POST {pdf:"<base64>"}` y devuelva ese mismo array. La API key vive en ese servidor, nunca en este HTML.

## Backups

El botón de descarga del tab bar baja un JSON con materias, opciones de cronograma y oferta. Se restaura con el botón de al lado. Los backups viejos se leen igual: el cronograma guardaba nombres de materia y ahora guarda `codigo#comision`, y la conversión es automática al importar.

## Nota sobre privacidad

GitHub Pages gratis solo funciona con repositorios **públicos** — el sitio queda accesible para cualquiera que tenga el link (no aparece en ningún listado ni buscador salvo que lo compartas). Si preferís que el repo sea privado, necesitás GitHub Pro/Team/Enterprise, o alternativamente correr el sitio localmente (abriendo `index.html` en el navegador) sin subirlo a ningún lado.
