## Ver 01 — 2026-09-21

### Cambios
- Creada la primera versión funcional de Fruit Basket en HTML, CSS y JavaScript vanilla.
- Incorporados menú, configuración mínima de sonido, HUD arcade, campo vertical y pantalla final.
- Implementadas cuatro canastas rotatorias, una fruta por vez, capturas, feedback visual/sonoro, pausa, tiempo, reintento y regreso al menú.
- Centralizados los principales parámetros visuales y funcionales para facilitar ajustes posteriores.

### Motivo
- Validar la mecánica central de mover las cuatro canastas con las flechas izquierda y derecha.

### Archivos afectados
- index.html
- LOG.md

### Estado
- Implementación terminada. Sintaxis, assets, controles, capturas, pausa, final de partida y layout 1366×768 / 1920×1080 verificados automáticamente; sensación de control, volumen y lectura visual requieren prueba manual del usuario.

## Ver 02 — v0.1.1 — 2026-09-21

### Cambios
- Incorporado escalado responsive proporcional para aprovechar mejor 1080p sin perjudicar el layout de 768p.
- Corregido el wrap visual para que la canasta que cruza un extremo se reposicione sin atravesar el campo.
- Ampliado el menú de pausa con los botones Continuar y Volver al menú, conservando Esc para pausar y reanudar.

### Motivo
- Refinar presentación, claridad y comodidad del prototipo sin modificar su mecánica central.

### Archivos afectados
- index.html
- LOG.md
- old_versions/Ver01/ (copia histórica de v0.1)

### Estado
- Sintaxis y carga correctas. Verificados en navegador los layouts 1366×768 y 1920×1080 sin scroll, flechas y pulsaciones rápidas, wrap en ambas direcciones, pausa/continuación con Esc y botón, salida al menú sin avance del loop y reinicio posterior de una partida. Pendiente de evaluación manual: sensación subjetiva del escalado y del movimiento.

## Ver 03 — v0.1.2 — 2026-09-21

### Cambios
- Reemplazada la reposición instantánea del wrap por una salida y entrada simultáneas en bordes opuestos mediante una copia exclusivamente visual y temporal.
- Agregada en Configuración la opción `Animación de canastas`, activada de forma predeterminada y sin persistencia.
- Conservada la actualización lógica inmediata y agregada limpieza segura de animaciones y copias ante pulsaciones rápidas, cambio de tamaño, fin de partida o regreso al menú.
- Actualizado de forma localizada `DEVELOPMENT_SPEC.md` con el comportamiento visual y la nueva opción.

### Motivo
- Mejorar la lectura de la rotación circular sin afectar la precisión ni bloquear entradas.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver02/ (copia histórica de v0.1.1)

### Estado
- Sintaxis JavaScript, assets, IDs y versión verificados automáticamente. Probados en navegador: rotación y wrap en ambos sentidos, secuencia rápida `← ← → ← →`, actualización correcta del orden, una sola copia visual durante el cruce y ninguna copia huérfana al finalizar, capturas posteriores, modos Animación ON/OFF, nueva partida tras cambiar la opción, pausa/continuación y regreso al menú sin errores de consola. Pendiente de evaluación visual manual: sensación subjetiva de continuidad y velocidad del nuevo wrap.

## Ver 04 — v0.2 — 2026-09-21

### Cambios
- Agregados presets centralizados Fácil, Normal y Difícil, más un modo Custom con límites conservadores para velocidad, máximo de frutas e intervalo de spawn.
- Reemplazada la fruta única por una colección de frutas activas independientes y un spawn escalonado integrado al game loop.
- Incorporados objetivo configurable, penalización opcional que resta progreso sin bajar de 0 y dificultad actual en el HUD.
- Conservadas pausa, controles, sonidos, feedback, animación de canastas, reintento y regreso al menú; todas las frutas comparten una velocidad global fija durante cada partida.
- Actualizado de forma localizada `DEVELOPMENT_SPEC.md` y preservada v0.1.2 en `old_versions/Ver03/`.

### Motivo
- Incorporar el primer sistema real de dificultad y múltiples frutas activas sin alterar la mecánica central validada.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver03/ (copia histórica de v0.1.2)

### Estado
- Sintaxis JavaScript, IDs, assets, versión y diff verificados. Probados en navegador Chromium: Fácil con 1 fruta, Normal con 2, Difícil con 3 y Custom con 4; spawn escalonado, frutas repetidas y en la misma columna, pausa/reanudación sin ráfaga, penalización ON/OFF, límite inferior 0, fin, reintento, menú, animación ON/OFF y limpieza de frutas/copias. Layout sin scroll probado en 1366×768 y 1920×1080, sin errores de consola. Pendiente de prueba manual: balance subjetivo de presets, sensación de control, lectura visual y audición de los sonidos.

## Ver 05 — v0.2.1 — 2026-09-23

### Cambios
- Incorporada una velocidad global progresiva calculada continuamente según las correctas respecto del objetivo.
- Reemplazada la velocidad fija de cada preset por rangos centralizados `startFallSpeed` / `maxFallSpeed`, sin cambiar sus cantidades activas ni intervalos de spawn.
- Ampliado Custom con velocidad inicial y máxima, límites conservadores y normalización del máximo cuando queda por debajo del inicial.
- Conservado un único valor global por frame para mover todas las frutas; una penalización puede reducir proporcionalmente esa velocidad.
- Actualizado de forma localizada `DEVELOPMENT_SPEC.md` y preservada v0.2 en `old_versions/Ver04/` sin duplicar assets.

### Motivo
- Agregar progresión gradual de dificultad durante la partida sin modificar la presentación ni las mecánicas ya validadas.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver04/ (copia histórica textual de v0.2)

### Estado
- Sintaxis, IDs, versión y diff verificados. Un harness comprobó inicio, mitad, máximo, límites y descenso de velocidad para Fácil, Normal, Difícil y Custom, incluida la normalización de valores invertidos. En navegador Chromium se verificaron los controles Custom, dos frutas con desplazamiento global idéntico, pausa/reanudación, limpieza al volver al menú y ausencia de errores de consola. Pendiente de prueba manual: balance y sensación subjetiva de la aceleración.

## Ver 06 — v0.2.2 — 2026-09-23

### Cambios
- Sustituida la progresión lineal por una curva de raíz cuadrada, limitada entre 0 y 1, para anticipar la aceleración sin superar la velocidad máxima.
- Ajustados los rangos de velocidad a 135–190 en Fácil, 180–270 en Normal y 225–350 en Difícil, conservando cantidades activas e intervalos de spawn.
- Agregados accesos rápidos de objetivo 10, 20, 30 y 50 que actualizan el mismo input numérico y mantienen disponible la entrada manual.
- Incorporada al HUD una barra de progreso acotada que refleja correctas sobre objetivo y disminuye con las penalizaciones.
- Ampliado de forma localizada a 400 el límite superior de velocidad Custom y actualizado `DEVELOPMENT_SPEC.md`.
- Preservada v0.2.1 en `old_versions/Ver05/` mediante una copia textual sin assets.

### Motivo
- Hacer más perceptible la progresión en partidas cortas y mejorar la lectura y selección del objetivo antes del rediseño visual.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver05/ (copia histórica textual de v0.2.1)

### Estado
- Sintaxis, versión, presets, límites, curva y diff verificados. Un harness comprobó inicio, avance temprano, progresión continua, máximo, descenso por penalización y barra en 0 %, valores intermedios, 100 % y tope para objetivos 10, 20, 30, 50 y manuales. En navegador Chromium se verificaron los cuatro accesos rápidos, entrada manual, Fácil, Normal, Difícil y Custom, múltiples frutas, pausa, fin, reintento, menú, animación ON/OFF y layouts 1366×768 / 1920×1080 sin scroll ni errores de consola. Pendiente de prueba manual: balance y sensación subjetiva de la nueva aceleración.

## Ver 07 — v0.3 — 2026-09-23

### Cambios
- Reemplazado el fondo técnico del playfield por una composición veraniega de capas independientes para cielo, tierra y pasto.
- Centralizados alturas, colores, opacidad de columnas y posiciones de nubes para facilitar ajustes manuales.
- Integradas las cuatro columnas mediante guías y sombreado mucho más sutiles, sin cambiar su lógica.
- Conservados los assets y la posición funcional de frutas y canastas; mejorado su contraste sobre el nuevo escenario.
- Actualizado de forma localizada `DEVELOPMENT_SPEC.md` y preservada v0.2.2 en `old_versions/Ver06/` sin duplicar assets.

### Motivo
- Dar al gameplay una estética más alegre, veraniega y amigable sin recargar la zona jugable ni modificar mecánicas.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver06/ (copia histórica textual de v0.2.2)

### Estado
- Sintaxis, versión, capas requeridas, diff y conservación exacta del JavaScript verificados automáticamente. En navegador Chromium integrado se comprobaron 1366×768 y 1920×1080 sin scroll, cielo/tierra/pasto diferenciados, columnas sutiles, frutas y canastas legibles, cuatro canastas sin copias huérfanas, entradas rápidas, pausa con tiempo y frutas congelados y ausencia de errores de consola. Pendiente de prueba manual en Chrome/Edge: apreciación final de contraste, colores y ambientación.

## Ver 08 — v0.3.1 — 2026-09-24

### Cambios
- Descartado el intento visual de v0.3 y restaurada como base funcional la presentación de v0.2.2 antes de rehacer únicamente el fondo.
- Construido un nuevo cielo en degradé inspirado en `example.png`, con `sun.png` arriba a la derecha y las tres nubes PNG existentes en movimiento suave hacia la derecha a velocidades distintas.
- Incorporado `surface_light.png` como franja inferior repetida para apoyar visualmente las canastas, sin mantener la franja de tierra anterior.
- Eliminadas por completo las líneas y divisiones visibles de las cuatro columnas; su lógica interna permanece intacta.
- Centralizados posición y tamaño del sol, altura del pasto y posición, tamaño, duración y desfase de cada nube.
- Actualizado de forma localizada `DEVELOPMENT_SPEC.md` y preservada la v0.3 descartada en `old_versions/Ver07/` sin duplicar assets.

### Motivo
- Rehacer el fondo del gameplay con los assets reales aportados y una composición más fiel a la referencia de Catch'n Avoid.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver07/ (copia histórica textual de v0.3)

### Estado
- Implementación terminada; pendientes comprobaciones automáticas, responsive y visuales.

## Ver 09 — v0.3.2 — 2026-09-24

### Cambios
- Agregado un halo permanente y suave a cada canasta con color propio; el de manzana es rosado/coral.
- Centralizados color, opacidad y desenfoque del halo normal y del feedback.
- El feedback sustituye inmediatamente el halo por verde o rojo puro y devuelve el color habitual sin estados intermedios sin halo.
- Conservado el halo en la copia visual del wrap y evitado que un feedback anterior corte uno repetido rápidamente.
- Preservada v0.3.1 en `old_versions/Ver08/` con los tres archivos de texto vigentes, sin duplicar assets.

### Motivo
- Integrar visualmente las canastas y mantener un feedback claro y continuo sobre la silueta transparente real.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver08/

### Estado
- Sintaxis JavaScript y filtros calculados verificados en Chrome sin interfaz. Comprobados cuatro colores normales, verde y rojo puro, regreso inmediato, feedback repetido, wrap durante feedback, feedback durante wrap, animación desactivada, ausencia de errores JavaScript y layouts 1366×768 / 1920×1080 sin desborde. Pendiente de evaluación visual final de sutileza, contraste y continuidad perceptiva en Chrome/Edge externo.

## Ver 10 — v0.3.3 — 2026-09-24

### Cambios
- Separados desplazamiento, giro y estela en cada fruta, con dirección de giro aleatoria y ángulo ligado a la distancia caída.
- Agregada una estela vertical suave y del color de cada fruta, detrás del sprite, sin partículas ni nodos por frame.
- Centralizados grados por píxel, longitud, ancho, opacidad, blur y colores de las estelas; las nubes se congelan durante la pausa.
- Preservada v0.3.2 en `old_versions/Ver09/` con archivos de texto verificados por SHA-256, sin duplicar assets.

### Motivo
- Dar vida visual a las frutas sin modificar su caída lógica, capturas ni otras mecánicas.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver09/

### Estado
- Sintaxis JavaScript y `git diff --check` verificados. Un harness con DOM simulado comprobó spawn, giros en ambos sentidos, pausa/reanudación, límites de 1/2/3/4 frutas para Fácil/Normal/Difícil/Custom, umbral de captura, aciertos, errores, fin, reintento, menú y ausencia de estelas huérfanas. Pendiente: evaluación visual y funcional en Chrome/Edge externo; la política de URL del navegador integrado bloqueó la carga local.

## Ver 11 — v0.3.4 — 2026-09-25

### Cambios
- Integrado `assets/marquee.png` como capa decorativa centrada detrás de `game-shell`, sin interceptar entradas ni modificar el PNG.
- Limitado de forma centralizada el escalado global al ancho útil del centro transparente, manteniendo HUD de 230 px, gap de 24 px y gameplay de 540 px.
- Registrada la integración visual vigente en `DEVELOPMENT_SPEC.md` y preservada v0.3.3 en `old_versions/Ver10/` sin duplicar assets.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver10/ (copia histórica textual de v0.3.3)

### Estado
- En Chrome automatizado se verificaron 1920×1080 y 1366×768: bezel centrado y proporcional, HUD y gameplay contenidos en la transparencia, sin recortes ni scroll. Se probaron menú, configuración, inicio, rotación, estelas, pausa/reanudación, captura, final, reintento, regreso al menú y resize, sin errores JavaScript. Pendiente: evaluación visual manual en Chrome/Edge de escritorio.

## Ver 12 — v0.4 — 2026-09-25

### Cambios
- Integrado `music/menu.mp3` en loop para Menú y Configuración, manteniendo la reproducción al cambiar entre ambas pantallas.
- Cada partida y reintento sortea una de las cinco pistas `music/music-1.mp3` a `music/music-5.mp3`; la pista permanece en loop durante juego, pausa y pantalla final.
- Reemplazados los tonos Web Audio por `sound_effects/good.mp3` y `sound_effects/error.mp3`, con dos voces reutilizables por efecto para capturas cercanas.
- Incorporados interruptores y sliders independientes de Música (70 %) y Efectos de sonido (80 %), aplicados en tiempo real.
- Actualizada de forma localizada `DEVELOPMENT_SPEC.md` y preservada v0.3.4 en `old_versions/Ver11/` sólo con archivos de texto.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver11/

### Estado
- Sintaxis JavaScript y `git diff --check` correctos. En Chrome automatizado se verificaron menú, configuración, controles de volumen y ON/OFF, música exclusiva de gameplay, pausa, pantalla final, reintento, regreso al menú, efectos de acierto/error y dos aciertos cercanos. En Edge automatizado se comprobaron las transiciones principales. Configuración sin desborde ni scroll de página en 1920×1080 y 1366×768. Sin errores JavaScript ni rechazos de `play()` sin manejar. Pendiente: evaluación auditiva y visual manual en Chrome/Edge de escritorio.

## Ver 13 — v0.4.1 — 2026-09-25

### Cambios
- La música del menú comienza con la primera interacción en la pantalla inicial, incluido un clic fuera de los botones o una tecla; se respeta el bloqueo de autoplay previo a esa interacción.
- Preservada v0.4 en `old_versions/Ver12/` sólo con archivos de texto.

### Archivos afectados
- index.html
- LOG.md
- old_versions/Ver12/

### Estado
- Sintaxis JavaScript y `git diff --check` verificados. En Chrome y Edge automatizados, sin desactivar autoplay, se comprobó silencio antes de interactuar, inicio con clic libre o teclado, continuidad al entrar en Configuración, cambio a una sola pista de gameplay y ausencia de errores JavaScript o rechazos de `play()` sin manejar. Pendiente: escucha manual en navegadores de escritorio.

## Ver 14 — v0.4.2 — 2026-09-25

### Cambios
- Al completarse la partida, la música de gameplay baja gradualmente hasta silencio durante 3 segundos y luego se pausa.
- Al volver al menú, `menu.mp3` se reinicia desde el principio; Reintentar y Volver al menú cancelan cualquier fade pendiente.
- Preservada v0.4.1 en `old_versions/Ver13/` sólo con archivos de texto.

### Archivos afectados
- index.html
- LOG.md
- old_versions/Ver13/

### Estado
- Sintaxis JavaScript y `git diff --check` verificados. En Chrome y Edge automatizados se comprobó el descenso de volumen durante unos 3 segundos, la pausa al llegar a cero, el reinicio de la música del menú desde 0 y la cancelación limpia del fade al reintentar o volver antes de tiempo. Sin errores JavaScript. Pendiente: escucha manual del efecto en navegadores de escritorio.

## Ver 15 — v0.4.3 — 2026-09-26

### Cambios
- Integrado `assets/banner.png` en el menú principal, centrado y proporcional, con margen superior responsive.
- Eliminado el panel visual del menú y ocultado el título HTML duplicado, conservándolo para accesibilidad.
- Ampliados sólo los botones del menú; la explicación existente quedó debajo de ambos.
- Agregada una respiración sutil al botón Jugar sin interferir con hover o click y con respeto a movimiento reducido.
- Ajustados ancho del banner, botones y separaciones según el viewport; Configuración conserva su panel.
- Preservada v0.4.2 en `old_versions/Ver14/` con archivos de texto verificados por SHA-256, sin copiar recursos estáticos.

### Archivos afectados
- index.html
- DEVELOPMENT_SPEC.md
- LOG.md
- old_versions/Ver14/

### Estado
- Sintaxis JavaScript, estructura y conservación del código JavaScript, Configuración y `banner.png` verificadas; cálculos de espacio para 1920×1080 y 1366×768 sin desborde estimado; `git diff --check` correcto. El navegador integrado bloqueó la apertura del archivo local por su política de URL: pendientes la comprobación visual real, hover/click, navegación, música y ausencia de errores en navegador de escritorio.
