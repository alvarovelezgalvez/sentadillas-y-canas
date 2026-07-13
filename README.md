# 🏋️ Sentadillas y Canas

Una app web minimalista para hacer **15 minutos de ejercicio al día** sin gimnasio, sin material (solo cuerpo + esterilla) y sin excusas. Pensada para sustituir las clases de core/fuerza/intensidad durante el verano, con rutinas que rotan solas cada día.

**🔗 App en vivo:** https://alvarovelezgalvez.github.io/sentadillas-y-canas/

---

## ¿Qué hace?

- **Propone la rutina del día automáticamente**, rotando entre tres tipos de sesión: **Core**, **Fuerza** e **Intenso** (cardio/HIIT). Nunca repite el mismo tipo dos días seguidos si sigues el orden sugerido.
- Dentro de cada tipo hay **3 variantes** de 6 ejercicios (A/B/C) que también van rotando, para no hacer siempre los mismos movimientos.
- **Vista previa**: antes de empezar puedes ver los 6 ejercicios de la sesión, con un icono esquemático, una explicación corta de cómo hacerlos bien y un enlace directo a una búsqueda en YouTube por si alguno no queda claro.
- **Modo seguimiento**: pantalla a pantalla con temporizador circular, aviso sonoro (pitido) y vibración en cada cambio de ejercicio/descanso, botones de pausa, saltar y retroceder.
- **Estructura de cada sesión (~14-15 min)**: 1 min de calentamiento → 2 rondas de 6 ejercicios (40 s de trabajo / 20 s de descanso) con un descanso más largo entre rondas.
- **Historial y racha**: guarda cada sesión completada, calcula días seguidos de racha, total de sesiones y minutos acumulados.
- **Se puede "instalar"** en la pantalla de inicio del móvil (iOS/Android) para usarla a pantalla completa, como una app nativa.

## Cómo funciona la rotación

No hay backend ni calendario fijo: el tipo de sesión de "hoy" se calcula a partir de **cuántas sesiones llevas hechas en total** (`sesiones completadas % 3`), así que si un día te la saltas, no se descuadra nada — simplemente continúa donde lo dejaste la próxima vez que abras la app. También puedes anular la sugerencia y elegir tú el tipo desde la pantalla de inicio.

La variante (A/B/C) de cada tipo se calcula igual, contando cuántas veces has hecho ese tipo concreto.

## Almacenamiento y privacidad

Todo se guarda **en el propio navegador** del dispositivo, usando `localStorage`. Esto implica:

- No hay servidor ni cuenta: nadie más ve tus datos, ni siquiera quien mantiene el repositorio.
- El historial **es local a ese navegador y dispositivo concreto**. Si la usas desde el móvil y desde el ordenador, cada uno lleva su propio historial por separado.
- Si borras datos de navegación de este sitio (o usas modo incógnito), el historial se pierde.
- No hay conexión a internet necesaria para usarla una vez cargada, salvo para los enlaces de "Ver vídeo" (búsqueda en YouTube) y las fuentes tipográficas la primera vez.

## Tecnología

Un único archivo `index.html` autocontenido: HTML + CSS + JavaScript vainilla, sin frameworks, sin build, sin dependencias que instalar. Los iconos de los ejercicios son SVG generados por código (figuras esquemáticas simples), no imágenes externas. El sonido de aviso se genera con la Web Audio API, sin archivos de audio.

Fuentes vía Google Fonts (Bebas Neue, Work Sans, JetBrains Mono) — es la única llamada externa aparte de los enlaces de vídeo.

## Cómo desplegarlo (GitHub Pages)

1. Haz fork o clona este repo.
2. En **Settings → Pages**, elige como *Source* la rama `main` y carpeta `/ (root)`.
3. En un par de minutos estará disponible en `https://TU-USUARIO.github.io/sentadillas-y-canas/`.

## Cómo usarla a pantalla completa en el móvil

1. Abre la URL en Safari (iPhone) o Chrome (Android).
2. Toca **Compartir → "Añadir a pantalla de inicio"** (iPhone) o el menú **⋮ → "Instalar app"** (Android).
3. Ábrela desde ese icono nuevo: se abrirá sin barra de navegador, como una app instalada.

## Personalizarla

Todo el contenido de las rutinas vive en el objeto `WORKOUTS` dentro del `<script>` del `index.html`: cada ejercicio es `{name, tip, icon}`. Para ajustarla a tu gusto puedes tocar, entre otras cosas:

- **Ejercicios y descripciones**: edita o añade entradas en `WORKOUTS.core / .fuerza / .intenso`.
- **Duración de trabajo/descanso**: constantes `WORK_SEC`, `REST_SEC`, `WARMUP_SEC`, `ROUNDREST_SEC` cerca del final del bloque de datos.
- **Icono de un ejercicio**: cada ejercicio referencia un `icon` (por ejemplo `"squat"`, `"plank"`); el diccionario `ICONS` define las figuras disponibles. Se puede añadir una nueva pose siguiendo el mismo patrón (`fig(cabeza, segmentos, extra)`).
- **Colores y tipografía**: variables CSS al principio del `<style>` (`--core`, `--fuerza`, `--intenso`, fuentes de Google Fonts).

No hace falta ningún paso de compilación: se edita el `index.html` y se hace commit.

## Limitaciones conocidas

- El temporizador puede perder precisión si el móvil bloquea la pantalla o pasa a segundo plano durante la sesión (limitación típica de los navegadores móviles con los timers en background).
- El historial no se sincroniza entre dispositivos ni navegadores.
- Los enlaces de "Ver vídeo" abren una búsqueda en YouTube, no un vídeo curado fijo (para evitar enlaces rotos con el tiempo).

## Uso previsto

Proyecto personal, sin ánimo de ser una app pública ni de sustituir consejo médico o de un entrenador. Si tienes alguna lesión o condición que lo desaconseje, consulta antes con un profesional.
