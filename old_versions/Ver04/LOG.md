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
