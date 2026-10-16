# Binder Studio — guía para Claude

Binder Studio (`index.html`, una sola página, sin build) arma videos de *master lists* de Pokémon TCG: un binder que se ve filmado de verdad sobre un playmat (cada carta sube a la cámara en la mano, entra en su bolsillo y se tilda en una hoja de checklist impresa al lado) más escenas de edición (ráfagas, carteles cinéticos, cartas en grande), grabadas directo desde el navegador con la voz del creador.

El usuario trabaja con **una carpeta por especie** en su compu:

```
Ponyta/
├── binder.json      cartas (la herramienta lo escribe)
├── video.json       plan del video: escenas (lo escribe Claude a partir del guion; la herramienta lo relee sola)
├── 60.jpg, SH11.png imágenes de cartas (nombre = número de carta)
├── media/           imágenes, GIF y clips para ráfagas y escenas
├── musica/          música de fondo
├── _editadas/       recortes hechos con el editor
└── videos/          videos grabados
```

## Antes del plan: trabajar el guion juntos

El usuario quiere ir y venir con el guion hasta dejarlo lo mejor posible. Puede mandar un guion entero, un borrador o solo ideas sueltas. En cada vuelta:

- Devolvé el guion completo mejorado, en castellano rioplatense y en el tono de él (hablado, no escrito: frases cortas, que se puedan decir de un tirón).
- Marcá en pocas líneas qué cambiaste y por qué, y hacé 1 o 2 preguntas concretas (una anécdota propia, cuál es su carta favorita, si tiene alguna).
- Cuidá: el gancho de los primeros 10 segundos (una pregunta, una promesa o un dato sorprendente), dar motivos para quedarse hasta el final (adelantar la carta más rara o un ranking), una frase por carta que diga algo que no se ve en la imagen, y un cierre con pregunta para comentarios.
- Chequeá los datos (sets, años, ilustradores, rarezas) contra TCGdex y avisá si algo no cierra. No inventes precios ni datos: si hace falta un número que no podés confirmar, dejalo marcado para que él lo complete.
- Estimá la duración (unas 150 palabras por minuto más el tiempo de binder).

Recién cuando el usuario aprueba el guion, pasás al plan. Desde ahí la regla es usar su texto tal cual, repartido entre escenas.

## Cuando el usuario pasa un guion aprobado

Tu trabajo es **proponer la edición**: convertir el guion en `video.json`. Leé `binder.json` de su carpeta para saber qué cartas hay y en qué posición. Si la carpeta está vinculada a la sesión, escribí `video.json` directo ahí (la herramienta lo detecta al volver a la pestaña); si no, mandalo como archivo para que lo guarde en la carpeta.

Después, en el chat: un resumen corto de la estructura (escenas y capítulos) y **la lista de archivos que tiene que conseguir** para `media/` (lo que pusiste en cada `pide`).

## Formato de `video.json`

```json
{
  "app": "binder-studio-video",
  "version": 1,
  "titulo": "Todas las cartas de Ponyta",
  "musica": "musica/tema.mp3",
  "escenas": [ { "tipo": "...", "capitulo": "...", "guion": "...", ... } ]
}
```

Campos comunes a todas las escenas:
- `tipo`: uno de los de abajo.
- `guion`: lo que el creador dice en esa escena. Aparece en el teleprompter mientras graba. Copiá el texto del guion original, repartido entre escenas; no lo reescribas salvo para cortarlo.
- `capitulo` (opcional): nombre del capítulo de YouTube que empieza en esta escena. Poné entre 4 y 8 capítulos en todo el video, el primero en la primera escena.

Tipos:

| tipo | campos | qué hace |
|---|---|---|
| `rafaga` | `items` (lista), `ritmo` (seg por elemento, ej. `"0.28"`), `fin` (`"auto"` o `"espera"`) | Montaje rápido con zoom de golpe, sacudida y flashes. |
| `titulo` | — | Portada con el título de la especie y la cantidad de cartas. |
| `cartel` | `estilo` (`golpe`, `barrido`, `maquina`, `contador`), `texto`, `valor` (contador), `fondo` | Tipografía cinética a pantalla completa, sobre papel, el playmat o cartulina de color. |
| `binder` | `cartas` (posiciones, `"1-9"`) | El binder sobre el playmat: cada → sube la carta a la cámara y después la mete en su bolsillo y la tilda en el checklist. Si el tramo empieza en la carta 1, arranca con el binder cerrado y el primer → lo abre. Usa el guion de cada carta (`script` en binder.json). |
| `carta` | `carta` (número `"SH11/99"` o posición `"#13"`), `texto` | La carta en la mano, en grande, con su ficha impresa en una hoja al lado. Los zooms marcados en la carta se recorren con →. |
| `media` | `media` (`"media/archivo.ext"`), `pide`, `texto` | Imagen, GIF o clip a pantalla completa con texto encima. |
| `lista` | `titulo`, `items` (lista) | Una hoja de cuaderno: cada → escribe a mano el punto siguiente. |
| `cierre` | `texto` | Cierre con logo, texto y botón de suscripción. |

Elementos de `items` en una ráfaga (strings):
- `"media/fuego.gif | GIF de llamas"`: archivo de la carpeta `media/`, y después de `|` qué tiene que conseguir el usuario.
- `"carta SH11/99"` o `"carta #13"`: una carta del binder, grande, sobre su propio fondo desenfocado.
- `"texto 29 CARTAS"`: una palabra o frase corta sobre color sólido.
- `"color"` o `"color acento"`: flash de color.

Texto de los carteles (`texto`):
- Cada línea es un renglón (`\n`).
- `*palabra*` = grande y en color de acento. `_palabra_` = chica, en cursiva (contraste de tamaños, estilo Casey Neistat). `~palabra~` = aparece y se tacha.
- Pocas palabras por cartel (2 a 7). Es un golpe visual, no un subtítulo.

`fondo` de un cartel: `blanco` (papel, texto negro: el clásico), `negro` o `marca` (el playmat), `acento` (cartulina del color del canal), `carta SH11/99` (la carta desenfocada) o un archivo `media/…`.

## Estilo de edición del canal

Referencias: Casey Neistat "Do What You Can't" (energía, tipografía cinética, cortes al ritmo) y Check The Box (formato de master list: binder, reglas, cartas que faltan). El video tiene que parecer filmado: un binder real sobre el playmat, nada de look generado.

- **Gancho en los primeros 10 segundos**: abrí con una `rafaga` de 6 a 10 elementos (ritmo 0.25–0.35) que mezcle cartas llamativas del binder, 1 o 2 textos con datos duros (cantidad de cartas, años) y 1 o 2 GIF/clips temáticos. Después, un `cartel` golpe con la pregunta o promesa del video, y recién ahí la `titulo`.
- **Reglas** de la lista en una `lista` corta (3 puntos) si el guion las menciona.
- **Separá el binder por eras** (Wizards, EX, Diamante y Perla/Platino, HGSS/BW, XY, Sun & Moon, Sword & Shield, Scarlet & Violet). Antes de cada tramo, un `cartel` (alterná `barrido` y `golpe`) con el nombre de la era. Cada tramo es un capítulo.
- **Cartas especiales** (shiny, promos, la más cara, errores, stamps) van como escena `carta` aparte, antes del tramo de binder que la contiene, con un `texto` corto ("LA *MÁS BUSCADA*").
- **Datos numéricos** fuertes del guion (precios, cantidades, años) → `cartel` estilo `contador`.
- Usá `media` para chistes o referencias del guion (un GIF de reacción, una escena del anime). Siempre con `pide` claro y concreto.
- Ritmo: no pongas más de ~45 segundos seguidos de binder sin un cartel o una carta especial en el medio.
- Cerrá con `cierre` y una pregunta para los comentarios.
- Los nombres de archivo que pidas: en minúsculas, sin espacios ni tildes (`media/caballo-galopando.gif`).

## Cartas en `binder.json`

Cada carta tiene, entre otros: `set`, `year`, `num`, `label`, `rarity`, `variants`, `illustrator`, `note` (dato en pantalla: va escrito a mano en un post-it, así que conviene que no pase de unos 110 caracteres), `script` (lo que dice en el teleprompter), `falta` (true si no la tiene: el bolsillo queda vacío y el checklist la anota como "falta"), `idioma` (`EN`, `JP`, `KO`, `ZH-T`, `ZH-S`, `FR`, `DE`, `IT`, `ES`, `PT`, `TH`, `ID`…) y `grupo`.

**Mismo arte en varios idiomas:** las cartas seguidas con el mismo `grupo` (por ejemplo `"base-44"`) aparecen todas juntas en grande, cada una con su idioma, y se guardan juntas en el binder con un solo →; el contador suma todas. Al armar una lista multi-idioma, ordená cada grupo seguido (EN, JP, KO, ZH, FR, DE, IT, ES, PT…) y poné el `script` solo en la primera carta del grupo.

## Notas técnicas

- Todo el código vive en `index.html` (un IIFE). Render en un `<canvas>` de 1920×1080; la grabación usa `captureStream` + `MediaRecorder`, con el micrófono, la música y efectos sintetizados mezclados por Web Audio.
- `binder.json` = cartas y marca; `video.json` = escenas. La herramienta guarda ambos.
- Los datos de cartas salen de TCGdex (repo `tcgdex/cards-database`, se puede clonar desde la sesión).
