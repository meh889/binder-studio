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
| `adelanto` | `items` (pasos, uno por →), `vuelan` (posiciones de las cartas que vuelan, ej. `"1-409"`; vacío: todas) | Apertura tipo "en este video": las cartas de la especie vuelan hacia la cámara, desenfocadas de cerca. Pasos: `texto …` (frase sobre las cartas volando), `carta #11 \| JAPÓN, *1996*` (esa carta viene al frente y la nube sigue atrás; con `\| crece` entra más chica y crece a los 0,6 s, para una jumbo; `\| crece 0.8` cambia el tiempo; con `\| sale de media/revista.jpg` la foto cae a la derecha y la carta sale por su costado, entre las páginas; agregando `desde x,y,ancho,alto` (en % de la foto, donde está la carta, como la ventanita de un pack) la cámara entra hasta ahí y la carta sale de su lugar), `suspenso #32 \| US$66.000` (la carta muy desenfocada con un contador; esa carta nunca vuela con las demás ni aparece en "A un toque", para no adelantarla) y `silencio ¿CUÁL *ES*?` (corta la música y congela todo). Si el `guion` tiene una línea por paso, el teleprompter muestra la de cada paso. En las frases, ` / ` fuerza un renglón. |
| `muro` | `texto` (la pregunta; el número entre `*asteriscos*` hace de contador), `respuesta` (segundo toque), `cartas` (vacío: todas) | La pregunta se escribe a máquina sobre oscuro; cuando llega al número, la cámara se aleja desde la primera carta y aparece el muro con todas las cartas de la lista mientras el número cuenta hasta el total. Con el segundo →, la respuesta. El guion puede tener un párrafo por toque. |
| `caos` | `texto` (el desorden; la última línea se desarma letra por letra), `cinta` (el orden; ` / ` la parte en dos tiras), `cartas` (las 9 de la hoja, ej. `"1-9"`) | Del caos al orden, en dos toques: primero las cartas de la especie caen desparramadas por todo el playmat con el texto encima; con el segundo →, las de la hoja vuelan a sus bolsillos en orden, las demás se van y se pega la cinta de rotuladora. Si el `guion` tiene dos párrafos (separados por una línea en blanco), el teleprompter muestra uno por toque. |
| `rafaga` | `items` (lista), `ritmo` (seg por elemento, ej. `"0.28"`), `fin` (`"auto"` o `"espera"`) | Montaje rápido con zoom de golpe, sacudida y flashes. |
| `titulo` | — | Portada con el título de la especie y la cantidad de cartas. |
| `cartel` | `estilo` (`golpe`, `barrido`, `maquina`, `contador`), `texto`, `valor` (contador), `fondo` | Tipografía cinética a pantalla completa, sobre papel, el playmat o cartulina de color. |
| `binder` | `cartas` (posiciones, `"1-9"`) | El binder sobre el playmat: cada → sube la carta a la cámara y después la mete en su bolsillo y la tilda en el checklist. Si el tramo empieza en la carta 1, arranca con el binder cerrado y el primer → lo abre. Usa el guion de cada carta (`script` en binder.json). |
| `carta` | `carta` (número `"SH11/99"` o posición `"#13"`), `texto` | La carta en la mano, en grande, con su ficha impresa en una hoja al lado. Los zooms marcados en la carta se recorren con →. |
| `media` | `media` (`"media/archivo.ext"`), `pide`, `texto`, `sonido` | Imagen, GIF o clip a pantalla completa con texto encima. Con `"sonido": "si"` el clip suena una vez desde el principio (la música de fondo se corre mientras tanto y queda en el último cuadro); si no, va mudo y en loop. |
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

- **Gancho en los primeros 10 segundos**: abrí con un `adelanto` (lo que eligió el creador para Bulbasaur): la promesa en una frase ("En este video vamos a ver todas las cartas de … que existen"), la cantidad y los idiomas, 5 o 6 cartas que van subiendo (la más vieja, otro idioma, una rareza de un lugar, una exclusiva, un premio) y al final un `suspenso` con la carta más cara o más rara y un `silencio` ("¿Cuál es? Quedate hasta el final"). Después, unos `cartel` con el porqué del canal, la intro, la `titulo` y las reglas. La `rafaga` sigue sirviendo para montajes rápidos en el medio.
- **El creador no tiene las cartas**: el canal muestra todas las que existen de cada especie. Nunca escribas en un guion que las tiene, las juntó, le faltan o le costó conseguirlas; sí que armó la lista y que la información estaba desparramada.
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

**Mismo arte en varios idiomas:** las cartas seguidas con el mismo `grupo` (por ejemplo `"base-44"`) y la misma condición aparecen juntas en grande, cada una con su idioma, y se guardan juntas con un solo →; el contador suma todas. La condición sale de `variants`: Normal, Unlimited (con cualquier línea de ©) y los códigos son la impresión común; 1st Edition, Shadowless, Reverse, Holo y cada sello o promo van cada uno aparte. Un → nunca muestra más cartas de las que entran en lo que queda de la hoja (9 bolsillos): si no entran, siguen en el próximo →.

Al armar una lista multi-idioma, ordená cada arte **por condición y dentro de cada condición por idioma** (EN, JP, KO, ZH, FR, DE, IT, ES, PT…): primero todas las 1st Edition, después Shadowless (o la tirada sin símbolo de rareza), la común (Unlimited/Normal) de todos los idiomas, Holo, Reverse, y al final cada sello o promo. Poné el `script` en la primera carta de cada condición, que es la que abre cada →.

## Notas técnicas

- Todo el código vive en `index.html` (un IIFE). Render en un `<canvas>` de 1920×1080; la grabación usa `captureStream` + `MediaRecorder`, con el micrófono, la música y efectos sintetizados mezclados por Web Audio.
- `binder.json` = cartas y marca; `video.json` = escenas. La herramienta guarda ambos.
- Los datos de cartas salen de TCGdex (repo `tcgdex/cards-database`, se puede clonar desde la sesión).
- Qué se graba no depende de la pestaña: el escenario sigue a la pestaña (Cartas = binder, Plan = video, `syncStage`), y Grabar/Ensayar usan `recTarget` ("video" o "binder", en los ajustes de Grabar) y, con "Desde acá" prendido, la posición del escenario (`stagePos` → `resolveFrom`).
- Grabación por partes: `P` pausa y retoma (`MediaRecorder.pause`, el reloj y los capítulos descuentan la pausa); grabando, `Esc` primero pausa. "Desde acá" arranca el estudio en una escena y, en un tramo de binder, en una carta (`openStudio(record, {scene, card}, target)`); en el ensayo, `R` pasa a grabar desde ese punto (`recordFromHere`). Al terminar, `nextFrom` calcula dónde sigue la parte siguiente ("Grabar la siguiente"). Al guardar en la carpeta, cada video lleva un `.json` al lado con `seconds`, `chapters` y `from`, y "Unir partes" reproduce las partes en orden dentro de un solo `MediaRecorder` y corre los capítulos.
- El guion se edita debajo del escenario (`#scriptText`): es el `script` de la carta en escena (la primera de un grupo de mismo arte) o el `guion` de la escena, lo mismo que mostraría el teleprompter en ese punto.
- La intro del canal es un clip con su propia música y textos (`intro-mafia-tcg.webm`, ~16 s): en cada video va como escena `media` con `"sonido": "si"`, después del gancho y antes de la portada, con el archivo copiado en `media/` de la especie. El guion de esa escena es la bienvenida que dice el creador cuando se pega el logo ("Bienvenidos a la Mafia. Hoy le toca a …").
- La marca del canal (Mafia TCG) está en `marca/` y la app la usa por defecto. Reglas del creador: la tipografía del logo es tributo a Pokémon y no se cambia; si aparecen cartas en piezas de marca, van dadas vuelta y con dorso fan art; nada de fondos negros ni grises en la marca.
