# Who Wants to Be a Knowledge Millionaire?

Juego de preguntas de ciencias y matemáticas, estilo "¿Quién quiere ser millonario?".
Todo el juego está en un solo archivo: `index.html`.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | El juego completo (preguntas, logo y estilos incluidos). **Es el único obligatorio.** |
| `questions.json` | Copia del banco de preguntas, para editarlo y cargarlo. |
| `logo-knowledge-millionaire.svg` | El logo como archivo aparte (el juego ya lo trae dentro). |

## Publicar con GitHub Pages

1. Sube estos archivos a la raíz de un repositorio nuevo.
2. Ve a **Settings → Pages**.
3. En **Source** elige **Deploy from a branch**, rama `main`, carpeta `/ (root)`, y guarda.
4. En uno o dos minutos estará en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPOSITORIO/`.

## Cambiar las preguntas

**Solo para una sesión (sin tocar el código):** en la pantalla de inicio abre
"Load my questions", elige un `.json` o pega el contenido, y pulsa "Use these questions".
Al recargar la página vuelve el banco incluido.

**De forma permanente:** en `index.html`, reemplaza el contenido del bloque
`<script type="application/json" id="banco-preguntas"> ... </script>`
por tu JSON.

### Formato de cada pregunta

```json
{
  "level": 1,
  "grade": "4 - 5",
  "subject": "Maths",
  "question": "What is 7 × 8?",
  "options": ["54", "56", "58", "64"],
  "correct": 1,
  "explanation": "Opcional: se muestra después de responder."
}
```

- `level` (1 a 15, opcional): posición en la escalera de premios. Puede haber varias preguntas por nivel; el juego elige una al azar.
- `grade` (opcional): `"Pre school - 1"`, `"2 - 3"`, `"4 - 5"`, `"6 - 7"`, `"8 - 9"` o `"11"`. También acepta una lista, por ejemplo `["2 - 3", "4 - 5"]`. Sin `grade`, la pregunta sale en todos los grados.
- `subject` (opcional): etiqueta que se muestra sobre la pregunta, por ejemplo `"Maths"` o `"Science"`.
- `question` y `options` (exactamente 4): obligatorios.
- `correct`: índice de la respuesta correcta (0 a 3) o la letra `"A"` a `"D"`.
- `explanation` (opcional).

Las respuestas se barajan en cada partida, así que el orden de `options` no importa.

## Ajustes rápidos

Al inicio del `<script>` de `index.html` está el objeto `CONFIG`:
premios, moneda (`£`), niveles asegurados (5 y 10), tiempo por pregunta (`0` = sin límite)
y nombres de los amigos de la ayuda "Phone a Friend".
Las opciones del selector de grado están en la constante `GRADES`.

## Notas

- Todavía no hay preguntas para **Pre school - 1**; con ese grado el botón de inicio queda bloqueado.
- El grado y el curso solo se muestran en pantalla; el juego no guarda ni envía datos.
