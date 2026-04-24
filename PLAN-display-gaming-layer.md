# Plan: Display customization + Gaming layer (Stardew Valley)

## Context

El Corne tiene nice!nano v2 con nice!view displays. Se quiere:
1. Personalizar las pantallas con widgets comunitarios (bongo cat, bateria, WPM)
2. Agregar una capa de gaming especifica para Stardew Valley

Esto se hara en una **nueva rama** separada del PR actual de Bluetooth.

## Paso 1: Crear rama nueva desde master

Crear `feat/display-gaming-layer` desde `master` (no desde `feat/keyboard-improvements`, para mantener los cambios independientes).

```bash
git checkout master
git checkout -b feat/display-gaming-layer
```

## Paso 2: Agregar capa Gaming (Stardew Valley)

**Archivo:** `config/corne.keymap`

Agregar layer `gaming` (index 4) con layout **QWERTY** optimizado para Stardew Valley:

```
// GAMING (Stardew Valley) - Toggle con LWR+RSE+G
// -----------------------------------------------------------------------------------------
// | TAB  |  Q  |  W  |  E  |  R  |  T  |        |  1  |  2  |  3  |  4  |  5  | ESC  |
// | SHFT |  A  |  S  |  D  |  F  |  G  |        |  6  |  7  |  8  |  9  |  0  | DEL  |
// | CTRL |  Z  |  X  |  C  |  V  |  B  |        |  M  |  Y  | UP  |     |     |      |
//                    | ALT |     | SPC |        | ENT | tog | RSE |
```

### Controles de Stardew Valley

**Izquierda (movimiento + acciones):**
- **WASD** - Movimiento
- **Shift** - Correr
- **E** - Abrir menu/inventario
- **C** - Usar herramienta
- **X** - Interactuar/Comer
- **F** - Diario
- **Tab** - Cambiar toolbar
- **Q/R/T** - Teclas auxiliares

**Derecha (inventario + navegacion):**
- **1-0** - Slots de inventario (seleccion directa)
- **M** - Mapa
- **Y** - Emotes
- **UP** - Flecha arriba (opcional)
- **ESC** - Menu/Salir
- **DEL** - Borrar

**Toggle:** `&tog 4` en thumb derecho (posicion central) para salir de la capa gaming

### Cambios en capa Adjust

Agregar `&tog 4` en la capa **Adjust** para activar el modo gaming. Posicion sugerida: donde esta la G en la capa base (fila 1, columna 6 izquierda), actualmente `&bt BT_SEL 4`.

**Alternativa:** Usar una posicion de la segunda o tercera fila que esta en `&trans`, para no perder BT5.

Ejemplo usando posicion fila 2, columna 6 izquierda (actualmente `&trans`):

```
// Adjust layer - fila 2 modificada:
&trans  &trans  &trans  &trans  &trans  &tog 4    &trans  &trans  &trans  &trans  &trans  &trans
```

### Codigo completo de la capa gaming

```c
                gaming {
// -----------------------------------------------------------------------------------------
// | TAB  |  Q  |  W  |  E  |  R  |  T  |        |  1  |  2  |  3  |  4  |  5  | ESC  |
// | SHFT |  A  |  S  |  D  |  F  |  G  |        |  6  |  7  |  8  |  9  |  0  | DEL  |
// | CTRL |  Z  |  X  |  C  |  V  |  B  |        |  M  |  Y  | UP  |     |     |      |
//                    | ALT |     | SPC |        | ENT | tog | RSE |
                        bindings = <
&kp TAB    &kp Q  &kp W  &kp E     &kp R   &kp T        &kp N1     &kp N2   &kp N3  &kp N4  &kp N5  &kp ESC
&kp LSHFT  &kp A  &kp S  &kp D     &kp F   &kp G        &kp N6     &kp N7   &kp N8  &kp N9  &kp N0  &kp DEL
&kp LCTRL  &kp Z  &kp X  &kp C     &kp V   &kp B        &kp M      &kp Y    &kp UP  &trans  &trans  &trans
                          &kp LALT  &trans  &kp SPACE    &kp ENTER  &tog 4   &mo 2
            >;
        };
```

## Paso 3: Integrar zmk-nice-oled

### Riesgo de compatibilidad

`zmk-nice-oled` fue probado con ZMK **v0.3.0**. Nuestro repo usa `revision: main` que ya incluye Zephyr 4.1.

**Estrategia:**
- **Primero:** Probar con `main` — si compila, funciona
- **Fallback:** Si falla, pinear ZMK a `revision: v0.3.0`
- **Ultimo recurso:** Usar solo el built-in status screen sin modulo externo

### 3a. Modificar `config/west.yml`

Agregar el remote y proyecto de `zmk-nice-oled`:

```yaml
manifest:
  remotes:
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    - name: mctechnology17
      url-base: https://github.com/mctechnology17
  projects:
    - name: zmk
      remote: zmkfirmware
      revision: main
      import: app/west.yml
    - name: zmk-nice-oled
      remote: mctechnology17
      revision: main
  self:
    path: config
```

### 3b. Modificar `build.yaml`

Cambiar los shields para usar `nice_oled` (central/izquierda) y `nice_epaper` (peripheral/derecha):

```yaml
---
include:
  - board: nice_nano//zmk
    shield: corne_left nice_view_adapter nice_oled
  - board: nice_nano//zmk
    shield: corne_right nice_view_adapter nice_epaper
  - board: nice_nano//zmk
    shield: settings_reset
```

**Nota:** `nice_oled` muestra los widgets principales (bongo cat, WPM, bateria). `nice_epaper` muestra animaciones en el peripheral (cat, gem, spaceman, pokemon).

### 3c. Modificar `config/corne.conf`

Agregar configuracion de display:

```ini
# Display
CONFIG_ZMK_DISPLAY=y
CONFIG_ZMK_DISPLAY_STATUS_SCREEN_CUSTOM=y
```

### 3d. Widgets disponibles para habilitar

Estos se configuran con flags `CONFIG_NICE_OLED_WIDGET_*` en `corne.conf`:

| Widget | Config flag | Descripcion |
|--------|------------|-------------|
| Bongo cat | `CONFIG_NICE_OLED_WIDGET_BONGO_CAT=y` | Gato que escribe al tipear |
| Luna | `CONFIG_NICE_OLED_WIDGET_LUNA=y` | Perrito que camina/corre |
| Bateria | `CONFIG_NICE_OLED_WIDGET_BATTERY=y` | Indicador de bateria |
| WPM | `CONFIG_NICE_OLED_WIDGET_WPM=y` | Palabras por minuto |
| Layer status | `CONFIG_NICE_OLED_WIDGET_LAYER_STATUS=y` | Nombre de capa activa |

**Configuracion sugerida para probar:**

```ini
# Display widgets (zmk-nice-oled)
CONFIG_NICE_OLED_WIDGET_BONGO_CAT=y
CONFIG_NICE_OLED_WIDGET_BATTERY=y
CONFIG_NICE_OLED_WIDGET_WPM=y
CONFIG_NICE_OLED_WIDGET_LAYER_STATUS=y
```

## Paso 4: Actualizar README

Agregar al README:

1. **Seccion "Gaming (Stardew Valley)"** con el diagrama de la capa y los controles
2. **Como activar/desactivar:** LWR + RSE + toggle key para entrar, `tog` en thumb derecho para salir
3. **Seccion "Display"** con los widgets habilitados

## Paso 5: Commit, push y crear PR

```bash
git add config/corne.keymap config/west.yml build.yaml config/corne.conf README.md
git commit -m "Add gaming layer (Stardew Valley) and display customization with zmk-nice-oled"
git push -u origin feat/display-gaming-layer
gh pr create --title "Add gaming layer and display widgets" --base master
```

## Verificacion

1. **Push** → verificar que GitHub Actions compila sin errores
2. **Si el build falla** por incompatibilidad de zmk-nice-oled:
   - Opcion A: Pinear ZMK a `revision: v0.3.0` en `west.yml`
   - Opcion B: Usar otro modulo de display
   - Opcion C: Quitar zmk-nice-oled y usar solo `CONFIG_ZMK_DISPLAY=y` (status screen built-in)
3. **Flashear** ambas mitades con los `.uf2` generados
4. **Verificar displays** — que muestren bongo cat, bateria, WPM
5. **Probar capa gaming** — activar con LWR+RSE+toggle, probar en Stardew Valley
6. **Verificar salida** — que `&tog 4` en thumb derecho desactiva la capa gaming correctamente
