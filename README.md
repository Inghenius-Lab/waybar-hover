# waybar-hover

Waybar compilada con un parche local que le agrega lo que upstream no
trae: **eventos de hover para los módulos**.

- `waybar-hover.patch` — diff sobre `src/AModule.cpp` de
  [Alexays/Waybar](https://github.com/Alexays/Waybar) en el commit
  `4e207a0cb51a9eb89b4245d90245721f5e39bf06` (v0.15.0-1085). Cuando el
  cursor entra o sale de la pastilla de un módulo, Waybar ejecuta los
  comandos configurados en las claves nuevas **`on-hover`** y
  **`on-hover-out`**, despachados igual que los comandos de clic.
- `.github/workflows/build.yml` — compila en GitHub Actions
  (ubuntu-24.04) y publica el binario como asset del release `build`.
  fmt, spdlog y jsoncpp se enlazan estáticos desde los wraps del
  propio árbol de Waybar, porque sus sonames difieren entre Ubuntu y
  Arch y el binario debe correr en una laptop con Arch Linux.

Para qué: en la barra de esa laptop, las pastillas de brillo, volumen
y micrófono muestran su barra de nivel **dentro de la pastilla**
mientras el cursor está encima (los scripts de los widgets reaccionan
a los marcadores que crean los comandos de hover), y un clic sobre la
barra salta al nivel pulsado mientras el clic sobre el icono conserva
su acción de siempre.

Descarga (repo público):

```sh
curl -LO https://github.com/Inghenius-Lab/waybar-hover/releases/download/build/waybar
```
## Módulo ring/* (2026-11-08)

Módulo nuevo `ring/<nombre>`: anillo de porcentaje dibujado con
Cairo alrededor de un icono centrado. El `exec` devuelve el JSON
de siempre de los módulos custom más "percentage" (0-100).
Config: `size` (px, 28), `thickness` (px, 3), `smooth` (true),
`gradient`: paradas de color por NOMBRE del tema GTK (los
@define-color que genera matugen en colors.css se resuelven en
cada dibujo: el anillo sigue al tema) o literales CSS; por
defecto waybar-tertiary -> waybar-source -> waybar-primary-container.
Sin números: el porcentaje exacto vive en el tooltip.
