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

## Actualizar tus materias

Los datos viven en el array `DATA` dentro de `index.html` (buscá `const DATA = [...]`). Podés:

- Editarlo a mano (cada materia es `{codigo, nombre, condicion, disponibilidad, nota}`), o
- Pedirme que regenere el archivo a partir de una versión nueva de tu Excel.

`condicion` acepta: `"Aprobada"`, `"Cursada"` (cursada, final pendiente) o `"No aprobada"`.
`disponibilidad` acepta: `"Disponible"` o `"No Disponible"`.

## Nota sobre privacidad

GitHub Pages gratis solo funciona con repositorios **públicos** — el sitio queda accesible para cualquiera que tenga el link (no aparece en ningún listado ni buscador salvo que lo compartas). Si preferís que el repo sea privado, necesitás GitHub Pro/Team/Enterprise, o alternativamente correr el sitio localmente (abriendo `index.html` en el navegador) sin subirlo a ningún lado.
