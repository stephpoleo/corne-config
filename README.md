# Corne Keyboard Config (Dvorak)

![image](https://github.com/stephpoleo/corne-config/assets/25173418/eaa343cd-3191-4a1f-a5fb-aa671bf53617)
![image](https://github.com/stephpoleo/corne-config/assets/25173418/d7e0a93b-f150-4452-8161-6decb604fab7)
![image](https://github.com/stephpoleo/corne-config/assets/25173418/03671c31-aba4-482f-a0b6-4bf72c459047)

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

**Bluetooth:** Fila superior para seleccionar perfiles BT (1-5). `BTCLR` limpia el perfil activo.

**Gaming toggle:** Presiona LWR + RSE + la tecla en fila 2, columna 6 izquierda para entrar al modo gaming.

### Gaming (Stardew Valley)
```
// -----------------------------------------------------------------------------------------
// | TAB  |  Q  |  W  |  E  |  R  |  T  |        |  1  |  2  |  3  |  4  |  5  | ESC  |
// | SHFT |  A  |  S  |  D  |  F  |  G  |        |  6  |  7  |  8  |  9  |  0  | DEL  |
// | CTRL |  Z  |  X  |  C  |  V  |  B  |        |  M  |  Y  | UP  |     |     |      |
//                    | ALT |     | SPC |        | ENT | tog | RSE |
```

**Controles izquierda (movimiento + acciones):**
- **WASD** — Movimiento
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

**Salir del modo gaming:** Presiona `tog` en el thumb derecho (posición central).

## Display

Usa [zmk-nice-oled](https://github.com/mctechnology17/zmk-nice-oled) para personalizar los nice!view displays.

**Widgets habilitados:**
- Bongo Cat — gato que escribe al tipear
- Batería — indicador de nivel
- WPM — palabras por minuto
- Layer Status — nombre de la capa activa

**Shields:**
- Izquierda (central): `nice_oled` — widgets principales
- Derecha (peripheral): `nice_epaper` — animaciones

## Flash

1. Descarga los archivos `.uf2` de GitHub Actions
2. Conecta cada mitad por USB mientras presionas el botón de reset (entra en modo bootloader)
3. Copia el `.uf2` correspondiente (`corne_left` o `corne_right`) al dispositivo
4. Repite para la otra mitad
