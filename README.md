# Corne Keyboard (ZMK)

Configuracion ZMK para teclado split Corne con nice!nano v2 y nice!view displays.

## Hardware

- **MCU:** nice!nano v2
- **Displays:** nice!view (ambas mitades)
- **Layout:** Corne (3x6 + 3 thumb keys)
- **Firmware:** [ZMK](https://zmk.dev) pinned to `v0.3.0`

![image](https://github.com/stephpoleo/corne-config/assets/25173418/eaa343cd-3191-4a1f-a5fb-aa671bf53617)
![image](https://github.com/stephpoleo/corne-config/assets/25173418/d7e0a93b-f150-4452-8161-6decb604fab7)
![image](https://github.com/stephpoleo/corne-config/assets/25173418/03671c31-aba4-482f-a0b6-4bf72c459047)

## Capas

| # | Capa | Activacion |
|---|------|-----------|
| 0 | Base (Dvorak) | Default |
| 1 | Lower (Nums + Fn) | Hold LWR |
| 2 | Raise (Simbolos) | Hold RSE |
| 3 | Adjust (BT + toggles) | LWR + RSE |
| 4 | Gaming (Stardew) | Toggle desde Adjust |
| 5 | Espanol (acentos) | Hold RALT o toggle desde Adjust |

### Base (Dvorak)

```
| TAB       | ' " | ,   | .   |  P  |  Y  |         |  F  |  G  |  C  |  R  |  L  | BKSP |
| LSHFT     |  A  |  O  |  E  |  U  |  I  |         |  D  |  H  |  T  |  N  |  S  |  DEL |
| LCTRL     | : ; |  Q  |  J  |  K  |  X  |         |  B  |  M  |  W  |  V  |  Z  | ESC  |
                    | CMD | LWR | SPC |         | ENT | RSE | ESP/ALT |
```

- **ESP/ALT (thumb derecho):** Tap = ALT, Hold = capa Espanol

### Lower (Numeros + Fn + Navegacion)

```
| TAB  |  1  |  2  |  3  |  4  |  5  |            |  6  |  7  |  8  |  9  |  0  | BSPC |
| SHF  | F1  | F2  | F3  | F4  | F5  |            | LFT | DWN |  UP | RGT |     |      |
| CTRL | F6  | F7  | F8  | F9  |     |            |     | F10 | F11 | F12 |     |      |
                   | CMD |     | SPC |            | ENT |     | ALT |
```

### Raise (Simbolos — optimizado para Python/SQL)

```
| TAB  |  !  |  @  |  #  |  $  |  %  |        |  ^  |  &  |  *  |  ?  |  +  | BKSP |
| SHF  |  :  |  (  |  )  |  [  |  ]  |        |  ;  |  _  |  =  |  -  |  /  |  `   |
| CTRL |     |  {  |  }  |  <  |  >  |        |  ~  |  "  |  '  |  |  |  \  |      |
                   | CMD |     | SPC |        | ENT |     | ALT |
```

**Filosofia:** Mano izquierda = pares de brackets, mano derecha = simbolos sueltos.

**Home row izquierda — Pares (mas usados):**
- `:` (ring) — Python defs, dicts, slices
- `(` `)` (middle, index) — roll natural para `()`, lo mas comun en Python/SQL
- `[` `]` (index-stretch, pinky-stretch) — lists, indexing

**Home row derecha — Simbolos sueltos:**
- `_` (index) — snake_case, SQL columns
- `=` (middle) — asignacion, comparacion
- `-` (ring) — sustraccion, kwargs
- `/` (pinky) — division, paths

**Bottom izquierda — Pares secundarios:**
- `{` `}` — dicts, f-strings, sets
- `<` `>` — comparacion, type hints

### Adjust (LWR + RSE — Tri-layer)

```
| BTCLR | BT1  | BT2  | BT3  | BT4  | BT5  |        |     |     |     |     |     |      |
|       |      |      |      | ESP  | GAME |        |     |     |     |     |     |      |
|       |      |      |      |      |      |        |     |     |     |     |     |      |
                      |      |      |      |        |     |     |     |
```

Se activa manteniendo **LWR + RSE** al mismo tiempo (tri-layer condicional).

- **BT1-BT5:** Seleccionar perfil Bluetooth
- **BTCLR:** Limpiar el perfil Bluetooth actual
- **GAME:** Toggle para entrar al modo gaming (fila 2, columna 6 izquierda)
- **ESP:** Toggle para capa Espanol (fila 2, columna 5 izquierda)

### Gaming (Stardew Valley)

```
| TAB  |  Q  |  W  |  E  |  R  |  T  |        |  1  |  2  |  3  |  4  |  5  | ESC  |
| SHFT |  A  |  S  |  D  |  F  |  G  |        |  6  |  7  |  8  |  9  |  0  | DEL  |
| CTRL |  Z  |  X  |  C  |  V  |  B  |        |  C  |  X  |  M  |  Y  | UP  |      |
                   | ALT |     | SPC |        | ENT | tog | RSE |
```

Layout QWERTY optimizado para Stardew Valley.

**Controles izquierda (movimiento):**
- **WASD** — Movimiento
- **Shift** — Correr
- **E** — Abrir menu/inventario
- **F** — Diario
- **Tab** — Cambiar toolbar
- **C / X** — Tambien disponibles aqui (duplicados) para uso ocasional

**Controles derecha (acciones + inventario):**
- **C** — Usar herramienta (indice, fila inferior — espejo de la izquierda)
- **X** — Interactuar/Seleccionar (medio, fila inferior)
- **1-0** — Slots de inventario (seleccion directa)
- **M** — Mapa
- **Y** — Emotes
- **ESC** — Menu/Salir

**Filosofia:** Mano izquierda mueve, mano derecha selecciona/actua. Las acciones `C` y `X` estan en la fila inferior derecha en posiciones espejo a las originales QWERTY, asi que la memoria muscular se traslada naturalmente.

**Activar:** LWR + RSE + GAME (desde capa Adjust)
**Salir:** Presiona `tog` en el thumb derecho (posicion central)

### Espanol (acentos)

```
|      |     |     |     |     |     |         |     |     |     |     |     |      |
|      |  á  |  ó  |  é  |  ú  |  í  |         |     |     |     |  ñ  |     |      |
|      |  ¡  |  ¿  |     |  ü  |     |         |     |     |     |     |     |      |
                   |     |     |     |         |     |     | ### |
```

Caracteres espanoles via macros de Alt codes (Windows). Funciona en cualquier layout de Windows sin instalar software adicional.

**Activar:**
- **Hold RALT** (thumb derecho) — momentaneo, para uso rapido
- **LWR + RSE + ESP** (desde Adjust) — toggle, para escritura prolongada en espanol

**Posiciones:** Las vocales acentuadas estan en las mismas posiciones que en Dvorak (A, O, E, U, I en home row izquierda), asi que la memoria muscular es natural.

- `ñ` en posicion de N (home row derecha)
- `ü` en posicion de K (debajo de U)
- `¡` en posicion de `: ;` (debajo de A)
- `¿` en posicion de Q (debajo de O)

## Display

Usa [zmk-nice-oled](https://github.com/mctechnology17/zmk-nice-oled) para personalizar los nice!view displays.

> **Nota:** ZMK esta pineado a `v0.3.0` para compatibilidad con este modulo. El workflow de GitHub Actions tambien usa `v0.3.0`.

**Shields:** Ambas mitades usan `nice_view_adapter nice_epaper`.

**Widgets disponibles:** Bongo Cat, bateria, WPM, layer status, y animaciones en el peripheral.

## Bluetooth - Conectar dispositivos

Soporta hasta 5 dispositivos emparejados. Selecciona perfiles desde la capa **Adjust** (LWR + RSE):

| Tecla | Accion |
|-------|--------|
| BTCLR | Limpia el perfil BT activo |
| BT1-BT5 | Selecciona perfil de conexion |

### Emparejar nuevo dispositivo

1. Presiona **LWR + RSE** simultaneamente para activar la capa Adjust
2. Selecciona un perfil vacio (BT1-BT5)
3. El teclado entra en modo pairing automaticamente
4. Busca "Corne" desde tu dispositivo

### Cambiar entre dispositivos

- **LWR + RSE + BT1** = Dispositivo 1
- **LWR + RSE + BT2** = Dispositivo 2
- etc.

### Solucionar problemas de conexion

Si el teclado no conecta:
1. Selecciona el perfil con problemas (LWR + RSE + BTx)
2. Presiona **BTCLR** para limpiar ese perfil
3. Vuelve a emparejar desde cero
4. Si persiste, flashea el firmware `settings_reset` en ambas mitades y luego reflashea el firmware normal

## Flash del firmware

### GitHub Actions (recomendado)

1. Haz push de tus cambios a GitHub
2. Ve a la pestana [Actions](../../actions)
3. Descarga el artifact `firmware` que contiene los archivos `.uf2`

### Flashear los archivos .uf2

1. Conecta la mitad por USB
2. Haz doble click en el boton **reset** del nice!nano (entra en modo bootloader)
3. Aparecera una unidad USB llamada **NICENANO**
4. Copia el `.uf2` correspondiente (`corne_left` o `corne_right`) a esa unidad
5. Repite para la otra mitad

### Reset de fabrica

Si tienes problemas persistentes de Bluetooth:

1. Flashea `settings_reset` en **ambas** mitades
2. Luego flashea los firmware normales (`corne_left` y `corne_right`) de nuevo
