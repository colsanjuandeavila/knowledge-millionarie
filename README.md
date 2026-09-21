# Who Wants to Be a Knowledge Millionaire?

Juego de preguntas de ciencias y matemáticas para todo un curso, estilo "¿Quién quiere ser millonario?".
Todo el juego está en un solo archivo: `index.html`.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | El juego completo (preguntas, logo y estilos incluidos). **Es el único obligatorio.** |
| `questions.json` | Copia del banco de preguntas (respaldo y referencia del formato). |
| `revision-dificultad.xlsx` | Orden de dificultad de cada pregunta por grado, para revisarlo y pedir cambios. |
| `logo-knowledge-millionaire.svg` | El logo como archivo aparte (el juego ya lo trae dentro). |

## Publicar con GitHub Pages

1. Sube estos archivos a la raíz de un repositorio nuevo.
2. Ve a **Settings → Pages**.
3. En **Source** elige **Deploy from a branch**, rama `main`, carpeta `/ (root)`, y guarda.
4. En uno o dos minutos estará en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPOSITORIO/`.

## Cómo se juega (modo curso)

1. **Pantalla inicial:** elige el **Grade**, escribe el **Course** (por ejemplo `301`) e **inscribe a los estudiantes**:
   escribe un nombre y pulsa **+** (o Enter). Cada nombre aparece como una etiqueta que se puede quitar con la ×.
   Para inscribir a todo el curso de una vez, copia la columna de nombres desde Excel o Word y pégala en el cuadro (un nombre por línea).
   No se repiten nombres (agrega un apellido o inicial) y el máximo es 60 estudiantes.
2. **Cada pregunta:** aparece la pregunta con sus opciones A, B, C y D, y a la derecha la lista de estudiantes,
   cada uno con un selector horizontal **A B C D**. Cada estudiante elige su respuesta (se puede cambiar antes de verificar).
3. **Check answers (verificar):** se revela la respuesta correcta y **solo los estudiantes que acertaron ganan el dinero** de esa pregunta.
   Si alguien no respondió, el juego pregunta antes de verificar.
4. **Ranking:** entre pregunta y pregunta se muestra el ranking actualizado, de mayor a menor dinero
   (con el dinero ganado en esa pregunta). Los empates comparten posición.
5. **Al final:** ranking final con el ganador. **Play again** vuelve al inicio conservando a los estudiantes.

El botón **Ranking** de la parte superior permite ver la clasificación en cualquier momento.

### Cuánto vale cada pregunta

Cada pregunta vale más que la anterior y **la suma de todas es exactamente £1,000,000**:
un estudiante que responde bien todas las preguntas del grado termina con £1,000,000. (Ejemplo con 60 preguntas: la primera vale £500 y la última £32,800.)
El valor de la pregunta actual aparece arriba ("Worth £…").

## Qué preguntas salen

- **Lo decide únicamente el selector de Grade**, no el texto del curso. Para evitar errores, si el curso es un código como `301`
  (grado 3, grupo 1) o `1101` (grado 11, grupo 1), el juego elige solo el grado que corresponde y no deja empezar si el grado
  seleccionado no coincide. Si el curso es otro texto (por ejemplo `Prueba`), no se verifica.
- Se usan **todas** las preguntas del grado, de más fáciles a más difíciles, intercalando Matemáticas y Ciencias
  (nunca más de 2 seguidas de la misma materia).
- Cada pregunta muestra arriba la materia y el grado (por ejemplo `Science · Grade 2 - 3`).

## Cambiar las preguntas

Las preguntas están dentro de `index.html`, en el bloque
`<script type="application/json" id="banco-preguntas"> ... </script>`.
Para agregar o corregir preguntas, edita ese bloque (o pide el archivo actualizado) y vuelve a subir `index.html` al repositorio.
Mantén `questions.json` al día con los mismos cambios, como respaldo.

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

- `level` (1 a 15, opcional): dificultad **dentro del grado**, de 1 (fácil) a 15 (difícil). Solo define el orden: las preguntas de nivel bajo salen primero, y dentro del mismo nivel el orden es aleatorio. En el banco actual se calculó ordenando las preguntas de cada grado por dificultad (ver `revision-dificultad.xlsx`).
- `grade` (opcional): `"Pre school - 1"`, `"2 - 3"`, `"4 - 5"`, `"6 - 7"`, `"8 - 9"` o `"11"`. También acepta una lista, por ejemplo `["2 - 3", "4 - 5"]`. Sin `grade`, la pregunta sale en todos los grados.
- `subject` (opcional): etiqueta que se muestra sobre la pregunta, por ejemplo `"Maths"` o `"Science"`.
- `question` y `options` (exactamente 4): obligatorios.
- `correct`: índice de la respuesta correcta (0 a 3) o la letra `"A"` a `"D"`.
- `explanation` (opcional).

Las respuestas se barajan en cada partida, así que el orden de `options` no importa.

## Ajustes rápidos

Al inicio del `<script>` de `index.html` está el objeto `CONFIG`:
`premioTotal` (dinero total de una partida perfecta, `1000000`), `redondeo` (los valores de las preguntas son múltiplos de `100`),
moneda (`£`), `maxAlumnos` (`60`), tiempo por pregunta (`0` = sin límite) y `verificarCurso`.
Las opciones del selector de grado están en la constante `GRADES`.

## Notas

- Todavía no hay preguntas para **Pre school - 1**; con ese grado el botón de inicio queda bloqueado.
- Los nombres de los estudiantes, el grado y el curso solo viven en la pantalla mientras el juego está abierto: el juego no guarda ni envía datos.
  Si se recarga la página hay que inscribir a los estudiantes de nuevo.
- El texto de derechos de autor está en la etiqueta `<footer class="copyright">` de `index.html` y aparece en todas las pantallas.
- Todas las pantallas se ajustan al tamaño de la ventana (computador, tableta y celular). Con cursos grandes, la lista de estudiantes se desplaza dentro de su panel.
