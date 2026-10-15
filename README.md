# Binder Studio

Herramienta para grabar videos de *master lists* de Pokémon TCG: un binder animado donde cada carta aparece en grande, se puede hacer zoom en un detalle (un stamp, una firma) y después se achica hasta su bolsillo y se tilda. Graba el video directo desde el navegador, sin grabador de pantalla.

**Usala acá:** https://meh889.github.io/binder-studio/

Funciona en **Chrome o Edge en una computadora** (son los navegadores que permiten leer y guardar en carpetas).

## Cómo se usa

1. Creá una carpeta por especie, por ejemplo `Ponyta/`, y poné ahí las imágenes de las cartas.
2. Abrí la herramienta y tocá **Abrir carpeta**. El navegador te pide permiso una vez.
3. Completá los datos de cada carta (o pegalos desde una planilla con **Pegar desde planilla**).
4. Tocá **● Grabar**, avanzá con **→** y al terminar guardá el video en la carpeta o descargalo.

Si sumás imágenes a la carpeta mientras la herramienta está abierta, tocá **Volver a leer** (o simplemente volvé a la pestaña: la relee sola).

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
├── _editadas/            imágenes recortadas o enderezadas con el editor
└── videos/               los videos que guardes desde la herramienta
```

El logo, el fondo y los colores del canal (pestaña **Overlay y marca**) se guardan en el navegador y se usan en todas las especies.

## Atajos mientras grabás

| Tecla | Acción |
|---|---|
| → / Espacio / clic | Siguiente paso (carta en grande → zooms → a su bolsillo) |
| ← | Volver una carta |
| Z | Zoom rápido |
| Esc | Terminar |

## Ejemplo

`ejemplos/Ponyta/binder.json` tiene la lista de Ponyta (29 cartas, de Team Rocket a Destined Rivals) con sets, números, ilustradores y datos. Copialo a tu carpeta `Ponyta/` junto con las imágenes, o usá **Importar datos**.

Los datos de las cartas salen de [TCGdex](https://tcgdex.dev). Las imágenes de las cartas son propiedad de sus dueños; esta herramienta no incluye ninguna.
