# Corne Keyboard (ZMK)

Configuracion ZMK para teclado split Corne con nice!nano v2 y nice!view displays.

## Hardware

- **MCU:** nice!nano v2
- **Displays:** nice!view (ambas mitades)
- **Layout:** Corne (3x6 + 3 thumb keys)

## Capas

### Base (Dvorak)

```
| TAB       | ' " | ,   | .   |  P  |  Y  |         |  F  |  G  |  C  |  R  |  L  | BKSP |
| LSHFT     |  A  |  O  |  E  |  U  |  I  |         |  D  |  H  |  T  |  N  |  S  |  DEL |
| LCTRL     | : ; |  Q  |  J  |  K  |  X  |         |  B  |  M  |  W  |  V  |  Z  | ESC  |
                    | CMD | LWR | SPC |         | ENT | RSE | ALT |
```

### Lower (Numeros + Fn + Navegacion)

```
| TAB  |  1  |  2  |  3  |  4  |  5  |            |  6  |  7  |  8  |  9  |  0  | BSPC |
| SHF  | F1  | F2  | F3  | F4  | F5  |            | LFT | DWN |  UP | RGT |     |      |
| CTRL | F6  | F7  | F8  | F9  |     |            |     | F10 | F11 | F12 |     |      |
                   | CMD |     | SPC |            | ENT |     | ALT |
```

### Raise (Simbolos)

```
| TAB |  !  |  @  |  #  |  $  |  %  |        |  ^  |  &  |  *  |  (  |  )  | BKSP |
| SHF |  ?  |  -  |  [  |  (  |  :  |        |  ;  |  )  |  ]  |  +  |  =  |  `   |
| CTRL|  ~  |  _  |  <  |  {  |  "  |        |  '  |  }  |  >  |  |  |  /  |  \   |
               | CMD |     | SPC |        | ENT |     | ALT |
```

### Adjust (Bluetooth) - Se activa presionando LWR + RSE al mismo tiempo

```
|     | BT1 | BT2 | BT3 | BT4 | BT5 |        |     |     |     |     |     | BTCLR |
|     |     |     |     |     |     |        |     |     |     |     |     |       |
|     |     |     |     |     |     |        |     |     |     |     |     |       |
               |     |     |     |        |     |     |     |
```

- **BT1-BT5:** Seleccionar perfil Bluetooth (ej. BT1 = computadora, BT2 = Meta Quest 2)
- **BTCLR:** Limpiar el perfil Bluetooth actual (usar si hay problemas de conexion)

## Bluetooth - Conectar dispositivos

### Emparejar con la computadora (perfil 1)

1. Presiona **LWR + RSE** simultaneamente para activar la capa Adjust
2. Presiona la tecla en la posicion de **BT1** (donde esta el `1` en la capa base)
3. En tu computadora, ve a configuracion Bluetooth y busca "Corne"
4. Empareja el dispositivo

### Emparejar con Meta Quest 2 (perfil 2)

1. Presiona **LWR + RSE** para activar la capa Adjust
2. Presiona **BT2** (donde esta el `2`) para cambiar al perfil 2
3. En las Meta Quest 2, ve a **Settings > Devices > Bluetooth**
4. Activa Bluetooth y busca "Corne"
5. Empareja el dispositivo

### Cambiar entre dispositivos

- **LWR + RSE + BT1** = Computadora
- **LWR + RSE + BT2** = Meta Quest 2

### Solucionar problemas de conexion

Si el teclado no conecta:
1. Selecciona el perfil con problemas (LWR + RSE + BTx)
2. Presiona **BTCLR** (LWR + RSE + tecla superior derecha) para limpiar ese perfil
3. Vuelve a emparejar desde cero
4. Si persiste, flashea el firmware `settings_reset` en ambas mitades y luego reflashea el firmware normal

## Flash del firmware

### Opcion 1: GitHub Actions (recomendado)

1. Haz push de tus cambios a GitHub
2. Ve a la pestana **Actions** en tu repositorio
3. El workflow `build.yml` compilara el firmware automaticamente
4. Descarga el artifact `firmware` que contiene los archivos `.uf2`
5. Dentro encontraras:
   - `corne_left-nice_nano_v2-zmk.uf2`
   - `corne_right-nice_nano_v2-zmk.uf2`
   - `settings_reset-nice_nano_v2-zmk.uf2`

### Opcion 2: Flashear los archivos .uf2

1. Conecta la mitad **izquierda** del teclado por USB
2. Haz doble click en el boton **reset** del nice!nano (entra en modo bootloader)
3. Aparecera una unidad USB llamada **NICENANO**
4. Copia el archivo `corne_left-nice_nano_v2-zmk.uf2` a esa unidad
5. El teclado se reiniciara automaticamente
6. Repite los pasos 1-5 con la mitad **derecha** usando `corne_right-nice_nano_v2-zmk.uf2`

### Reset de fabrica

Si tienes problemas persistentes de Bluetooth:

1. Flashea `settings_reset-nice_nano_v2-zmk.uf2` en **ambas** mitades
2. Luego flashea los firmware normales (`corne_left` y `corne_right`) de nuevo

![image](https://github.com/stephpoleo/corne-config/assets/25173418/eaa343cd-3191-4a1f-a5fb-aa671bf53617)
![image](https://github.com/stephpoleo/corne-config/assets/25173418/d7e0a93b-f150-4452-8161-6decb604fab7)
![image](https://github.com/stephpoleo/corne-config/assets/25173418/03671c31-aba4-482f-a0b6-4bf72c459047)
