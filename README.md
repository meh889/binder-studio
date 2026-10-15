# Binder Studio

Herramienta para grabar videos de *master lists* de Pokémon TCG. Arma el video entero: ráfaga de intro, carteles con tipografía cinética, cartas en grande con zoom, y un binder animado donde cada carta aparece, se achica hasta su bolsillo y se tilda (o se tacha con una X roja si te falta). Graba directo desde el navegador, con tu voz, música y efectos de sonido, sin grabador de pantalla.

**Usala acá:** https://meh889.github.io/binder-studio/

Funciona en **Chrome o Edge en una computadora** (son los navegadores que permiten leer y guardar en carpetas).

## Cómo se usa

1. Creá una carpeta por especie, por ejemplo `Ponyta/`, y poné ahí las imágenes de las cartas.
2. Abrí la herramienta y tocá **Abrir carpeta**. El navegador te pide permiso una vez.
3. Completá los datos de cada carta (o pegalos desde una planilla con **Pegar desde planilla**).
4. Tocá **● Grabar**, avanzá con **→** y al terminar guardá el video en la carpeta o descargalo.

Si sumás imágenes a la carpeta mientras la herramienta está abierta, tocá **Volver a leer** (o simplemente volvé a la pestaña: la relee sola).

## El video completo (pestaña Video)

1. Escribí el guion y pasáselo a Claude en el chat. Claude propone la edición y deja un `video.json` en tu carpeta con las escenas: ráfaga, carteles, tramos de binder, cartas especiales y cierre. La herramienta lo carga sola al volver a la pestaña.
2. En la pestaña **Video** revisás y retocás las escenas, y ves qué imágenes, GIF o clips te faltan para la ráfaga (van en `media/`).
3. Arriba elegís **Video completo** y tocás **● Grabar**. Leés el guion en el teleprompter y avanzás con →. Se graba tu voz, la música de `musica/` (que baja sola cuando hablás) y los efectos de sonido.
4. Al terminar, te da el MP4 con audio y la lista de capítulos para pegar en la descripción de YouTube.

Tipos de escena: ráfaga, portada, cartel cinético (golpe, barrido, máquina de escribir, contador), binder, carta en grande, imagen o clip, lista y cierre. En los carteles, `*palabra*` sale grande y en color, `_palabra_` chica en cursiva y `~palabra~` aparece y se tacha.

## Mismo arte en varios idiomas

Si una carta tiene el mismo arte en varios idiomas, tocá **Unir con la de arriba** en cada versión (o completá el campo **Grupo** con el mismo nombre) y poné el **Idioma** de cada una. En el video aparecen todas juntas en grande, cada una con su idioma, y con un solo → se guardan todas en el binder y el contador las suma.

## Nombres de las imágenes

Si la imagen se llama como el número de la carta, cae sola en su lugar:

| Carta | Archivo |
|---|---|
| 60/102 | `60.jpg` |
| SH11/99 | `SH11.png` |
| SWSH013/307 | `SWSH013.jpg` o `SWSH13.jpg` |
| 14/106 y 14/83 (mismo número en dos sets) | `14-106.jpg` y `14-83.jpg` |

Las imágenes que no coinciden con ningún número se asignan en orden alfabético a las cartas sin imagen, y si sobran se crean cartas nuevas.

## Qué guarda en la carpeta

```
Ponyta/
├── 60.jpg, 64.jpg, …     tus imágenes (no se modifican)
├── binder.json           datos de las cartas, zooms, guion y ajustes
├── video.json            el plan del video (escenas)
├── media/                imágenes, GIF y clips para la ráfaga y las escenas
├── musica/               música de fondo
├── _editadas/            imágenes recortadas o enderezadas con el editor
└── videos/               los videos que guardes desde la herramienta
```

El logo, el fondo y los colores del canal (pestaña **Overlay y marca**) se guardan en el navegador y se usan en todas las especies.

## Atajos mientras grabás

| Tecla | Acción |
|---|---|
| → / Espacio / clic | Siguiente paso: próxima escena, próxima carta, zoom o punto de la lista |
| ← | Volver un paso |
| Z | Zoom rápido |
| Esc | Terminar la grabación |

## Ejemplo

`ejemplos/Ponyta/` tiene la lista de Ponyta (29 cartas, de Team Rocket a Destined Rivals) en `binder.json` y un plan de video de ejemplo en `video.json`. Copiá los dos a tu carpeta `Ponyta/` junto con las imágenes.

Los datos de las cartas salen de [TCGdex](https://tcgdex.dev). Las imágenes de las cartas son propiedad de sus dueños; esta herramienta no incluye ninguna.
