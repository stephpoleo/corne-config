# Corne Keyboard Config (Dvorak)

![image](https://github.com/stephpoleo/corne-config/assets/25173418/eaa343cd-3191-4a1f-a5fb-aa671bf53617)
![image](https://github.com/stephpoleo/corne-config/assets/25173418/d7e0a93b-f150-4452-8161-6decb604fab7)
![image](https://github.com/stephpoleo/corne-config/assets/25173418/03671c31-aba4-482f-a0b6-4bf72c459047)

## Hardware

- **Board:** nice!nano v2
- **Display:** nice!view (e-paper)
- **Firmware:** [ZMK](https://zmk.dev) pinned to `v0.3.0`

## Layers

### Base (Dvorak)
```
// -----------------------------------------------------------------------------------------
// | TAB       | ' " | ,   | .   |  P  |  Y  |         | F   |  G   |  C  |  R  |  L  | BKSP |
// | CAPS      |  A  |  O  |  E  |  U  |  I  |         |  D  |  H   |  T  |  N  |  S  |  DEL |
// | LCTRL     | : ; |  Q  |  J  |  K  |  X  |         |  B  |  M   |  W  |  V  |  Z  | ESC  |
//                     | COMMAND | LWR | SPC |         | ENT | RSE  | ALT |
```

### Lower (Numbers + F-keys)
```
// -----------------------------------------------------------------------------------------
// | TAB  |   1  |   2  |   3  |  4  |  5  |            |  6  |  7   |  8  |  9  |  0  | BSPC  |
// | SHF  |  F1  |  F2  |  F3  | F4  | F5  |            | LFT | DWN  | UP  | RGT |     |       |
// | CTRL |  F6  |  F7  |  F8  | F9  |     |            |     |  F10 | F11 | F12 |     |       |
//                   | COMMAND |     | SPC |            | ENT |      | ALT |
```

### Raise (Symbols)
```
// -----------------------------------------------------------------------------------------
// |  TAB |  !  |  @  |  #  |  $  |  %  |        |  ^  |  &  |  *  |  (  |  )  | BKSP |
// | SHF  |  ?  |  -  |  [  |  (  |  :  |        |  ;  |  )  |  ]  |  +  |  =  |  `   |
// | CTRL |  ~  |  _  |  <  |  {  |  "  |        |  '  |  }  |  >  |  |  |  /  |  \   |
//                | COMMAND |     | SPC |        | ENT |     | ALT |
```

### Adjust (LWR + RSE — Tri-layer)
```
// -----------------------------------------------------------------------------------------
// | BTCLR | BT1  | BT2  | BT3  | BT4  | BT5  |        |     |     |     |     |     |      |
// |       |      |      |      |      | GAME |        |     |     |     |     |     |      |
// |       |      |      |      |      |      |        |     |     |     |     |     |      |
//                       |      |      |      |        |     |     |     |
```

Se activa manteniendo **LWR + RSE** al mismo tiempo (tri-layer condicional).

- **Fila 1:** Perfiles Bluetooth 1-5. `BTCLR` limpia el perfil activo.
- **GAME:** Toggle para entrar/salir del modo gaming (fila 2, columna 6 izquierda).

### Gaming (Stardew Valley)
```
// -----------------------------------------------------------------------------------------
// | TAB  |  Q  |  W  |  E  |  R  |  T  |        |  1  |  2  |  3  |  4  |  5  | ESC  |
// | SHFT |  A  |  S  |  D  |  F  |  G  |        |  6  |  7  |  8  |  9  |  0  | DEL  |
// | CTRL |  Z  |  X  |  C  |  V  |  B  |        |  M  |  Y  | UP  |     |     |      |
//                    | ALT |     | SPC |        | ENT | tog | RSE |
```

Layout QWERTY optimizado para Stardew Valley.

**Controles izquierda (movimiento + acciones):**
- **WASD** �� Movimiento
- **Shift** — Correr
- **E** — Abrir menú/inventario
- **C** — Usar herramienta
- **X** — Interactuar/Comer
- **F** — Diario
- **Tab** — Cambiar toolbar

**Controles derecha (inventario + navegación):**
- **1-0** — Slots de inventario (selección directa)
- **M** — Mapa
- **Y** — Emotes
- **ESC** — Menú/Salir

**Activar:** LWR + RSE + GAME (desde capa Adjust)
**Salir:** Presiona `tog` en el thumb derecho (posición central)

## Display

Usa [zmk-nice-oled](https://github.com/mctechnology17/zmk-nice-oled) para personalizar los nice!view displays.

> **Nota:** ZMK está pineado a `v0.3.0` para compatibilidad con este módulo. El workflow de GitHub Actions también usa `v0.3.0`.

**Shields:** Ambas mitades usan `nice_view_adapter nice_epaper`.

**Widgets disponibles:** Bongo Cat, batería, WPM, layer status, y animaciones en el peripheral.

## Bluetooth

Soporta hasta 5 dispositivos emparejados. Selecciona perfiles desde la capa **Adjust** (LWR + RSE):

| Tecla | Acción |
|-------|--------|
| BTCLR | Limpia el perfil BT activo |
| BT1-BT5 | Selecciona perfil de conexión |

**Emparejar nuevo dispositivo:**
1. Selecciona un perfil vacío (BT1-BT5)
2. El teclado entra en modo pairing automáticamente
3. Busca "Corne" desde tu dispositivo

## Flash

1. Descarga el artifact `firmware` desde [GitHub Actions](../../actions)
2. Conecta cada mitad por USB mientras presionas el botón de reset (doble click) para entrar en modo bootloader
3. Copia el `.uf2` correspondiente (`corne_left` o `corne_right`) al dispositivo que aparece
4. Repite para la otra mitad

> **Tip:** Si el teclado no responde después del flash, flashea también el `settings_reset.uf2` en ambas mitades y luego vuelve a flashear el firmware normal.
