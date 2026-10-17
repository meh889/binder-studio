# Binder Studio

Herramienta para grabar videos de *master lists* de Pokémon TCG. Arma el video entero: ráfaga de intro, carteles con tipografía cinética, cartas en grande con zoom, y un binder que se ve filmado de verdad sobre el playmat: cada carta sube a la cámara, entra en su bolsillo y se tilda en el checklist impreso de la página (si te falta, el bolsillo queda vacío). Graba directo desde el navegador, con tu voz, música y efectos de sonido, sin grabador de pantalla.

**Usala acá:** https://meh889.github.io/binder-studio/

Funciona en **Chrome o Edge en una computadora** (son los navegadores que permiten leer y guardar en carpetas).

## Cómo se usa

1. Creá una carpeta por especie, por ejemplo `Ponyta/`, y poné ahí las imágenes de las cartas.
2. Abrí la herramienta y tocá **Abrir carpeta**. El navegador te pide permiso una vez. Para abrir otra especie o una reciente, usá el menú de la carpeta, arriba a la izquierda.
3. En **Cartas** está el estante: cada carta lleva etiquetas de lo que le falta (*sin imagen*, *sin guion*, *me falta*) o de lo que tiene (*2 zooms*). Tocá una y el escenario la muestra; a la derecha completás sus datos, la recortás o marcás sus zooms. Filtrá por etiqueta o buscá con `/`. Para sumar cartas: **+ Agregar** (imágenes, pegar desde planilla o carta vacía).
4. Tocá **● Grabar**, avanzá con **→** y al terminar guardá el video en la carpeta o descargalo. La calidad, los cuadros por segundo y el audio están en el botón de ajustes, al lado de Grabar.

Si sumás imágenes a la carpeta mientras la herramienta está abierta, elegí **Volver a leer la carpeta** en el menú de la carpeta (o simplemente volvé a la pestaña: la relee sola).

## El video completo (Plan del video)

1. Escribí el guion y pasáselo a Claude en el chat. Claude propone la edición y deja un `video.json` en tu carpeta con las escenas: ráfaga, carteles, tramos de binder, cartas especiales y cierre. La herramienta lo carga sola al volver a la pestaña.
2. En **Plan del video** ves las escenas en orden, cuánto dura cada una más o menos y qué imágenes, GIF o clips te faltan (van en `media/`). Tocá una escena para retocarla a la derecha mientras el escenario la reproduce.
3. Debajo del escenario elegís **Video completo** y tocás **● Grabar**. Leés el guion en el teleprompter y avanzás con →. Se graba tu voz, la música de `musica/` (que baja sola cuando hablás) y los efectos de sonido.
4. Al terminar, te da el MP4 con audio y la lista de capítulos para pegar en la descripción de YouTube.

Tipos de escena: ráfaga, portada, cartel cinético (golpe, barrido, máquina de escribir, contador), binder, carta en grande, imagen o clip, lista y cierre. En los carteles, `*palabra*` sale grande y en color, `_palabra_` chica en cursiva y `~palabra~` aparece y se tacha.

## Mismo arte en varios idiomas

Si una carta tiene el mismo arte en varios idiomas, tocá **Unir con la de arriba** en la ficha de cada versión (o completá el campo **Grupo** con el mismo nombre) y poné el **Idioma** de cada una. En el video, cada → muestra juntas las versiones seguidas de ese arte que comparten condición (por ejemplo, la Unlimited en todos los idiomas; la 1st Edition, la Shadowless, las Reverse y cada sello van aparte), cada una con su idioma, y nunca más de las que entran en lo que queda de la hoja. Con el próximo → se guardan y el contador las suma. Para que se junten, ordená cada arte por condición y dentro de cada condición por idioma.

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

La app viene con la marca de Mafia TCG puesta: el logo (como sticker en la tapa, en la esquina y en el cierre), el binder lila y los colores del logo. Todo se cambia en la vista **Marca** (el tema **Mafia TCG** la vuelve a poner con un clic) y se guarda en el navegador para todas las especies. Los archivos de la marca en alta (avatar, banner, logo y stickers) están en [`marca/`](marca/).

## Atajos mientras grabás

| Tecla | Acción |
|---|---|
| → / Espacio / clic | Siguiente paso: próxima escena, próxima carta, zoom o punto de la lista |
| ← | Volver un paso |
| Z | Zoom rápido |
| Esc | Terminar la grabación |

Fuera de la grabación también funcionan → y ← sobre el escenario, **Inicio** para volver al principio, **/** para buscar cartas, **↑ ↓** para moverte por la lista y **Ctrl+Z** para deshacer.

## Ejemplo

`ejemplos/Ponyta/` tiene la lista de Ponyta (29 cartas, de Team Rocket a Destined Rivals) en `binder.json` y un plan de video de ejemplo en `video.json`. Copiá los dos a tu carpeta `Ponyta/` junto con las imágenes.

Los datos de las cartas salen de [TCGdex](https://tcgdex.dev). Las imágenes de las cartas son propiedad de sus dueños; esta herramienta no incluye ninguna.
