# Trabajo en SuperVanilla

Consulta [el índice de documentación](docs/README.md) y
[la guía de compilación](docs/build/README.md) antes de editar.

- Conserva los IDs de Confogl, el orden de carga y descarga, los nombres de
  plugins y las rutas de Stripper, fuentes y recursos de SourceMod.
- Compila con el Makefile raíz. El mapa de producto en
  `scripts/package/package-map.json` declara los entrypoints. Genera y valida el ZIP con
  `make release` y `make validate-artifact`. Las salidas quedan en
  `.deps/`, `.build/` y `dist/`.
- Conserva autoría y licencias. Distingue compilación, validación offline y
  prueba en SRCDS. Los cambios remotos y el despliegue requieren autorización.

## Actualizar la base de ZoneMod

1. Toma la versión, el SHA y los pares de perfiles de la
   [referencia técnica](docs/mode/zonemod-baseline.md). Compara la revisión
   registrada con la candidata. Sigue los `exec` de cada tamaño y revisa
   los cambios en Plugin Manager, los CFG compartidos y los proveedores.
2. Aplica los cambios acordados a los cuatro perfiles y al CFG compartido.
   Conserva las reglas de SuperVanilla para jefes, armas, puntuación y
   comunes. Antes de incorporar `mapinfo.txt`, `mapcvars.txt` o filtros de
   Stripper, revisa su efecto en los spawns de Witch y de armas T2/T3.
   Comprueba las rutas y mayúsculas de los filtros. Ajusta el mapa de
   producto si cambian los recursos instalables o sus proveedores.
3. Ejecuta `make validate-modes`, `make release` y `make validate-artifact`.
   Si falta una compilación válida o cambian fuentes o includes, sigue la
   guía de compilación y ejecuta `make build-smx` antes de empaquetar.
   Registra por separado la prueba en SRCDS de carga, inicio de ronda,
   cambio de modo y restauración de Cvars. Actualiza la revisión y el
   alcance sincronizado en la referencia técnica. Anota los cambios de
   comportamiento en el changelog.
