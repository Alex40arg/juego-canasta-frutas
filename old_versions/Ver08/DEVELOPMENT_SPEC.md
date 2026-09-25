# DEVELOPMENT_SPEC.md

## Proyecto

**Nombre:** Fruit Basket  
**Tipo:** Minijuego arcade / cognitivo  
**Plataforma:** Navegador web de escritorio  
**Tecnologías previstas:** HTML5, CSS y JavaScript vanilla  
**Archivo principal inicial:** `index.html`

---

# 1. Objetivo del proyecto

Fruit Basket es un minijuego arcade orientado principalmente a adultos mayores, principiantes en informática y usuarios que deseen practicar coordinación, atención visual, velocidad de reacción y uso de las teclas cursoras izquierda y derecha.

El jugador no controla directamente los objetos que caen.

La mecánica principal consiste en:

- cuatro frutas diferentes que caen desde la parte superior del campo de juego;
- cuatro canastas situadas en la parte inferior;
- cada canasta corresponde a un tipo de fruta;
- el jugador debe rotar horizontalmente las cuatro canastas utilizando las teclas de cursor izquierda y derecha;
- el objetivo es lograr que cada fruta caiga en la canasta correspondiente.

El juego debe comenzar siendo simple y accesible, pero permitir posteriormente niveles de dificultad altos y un ritmo arcade exigente.

La prioridad del proyecto es:

- controles precisos;
- respuesta inmediata;
- reglas fáciles de comprender;
- buena legibilidad;
- estética amigable;
- posibilidad de aumentar progresivamente la dificultad;
- funcionamiento correcto en diferentes resoluciones de PC;
- facilidad para ajustar manualmente tamaños, velocidades y aspectos visuales durante el desarrollo.

---

# 2. Concepto general de juego

El campo de juego debe contener cuatro columnas verticales invisibles.

Cada fruta aparece en una de esas cuatro columnas y cae verticalmente hacia la parte inferior.

La fruta no debe cambiar de columna durante su caída.

En la parte inferior existen siempre cuatro canastas, una por columna.

Ejemplo conceptual:

```text
Columna 1   Columna 2   Columna 3   Columna 4

   fruta ↓

-----------------------------------------------

Canasta 1   Canasta 2   Canasta 3   Canasta 4
```

Al presionar:

```text
←
```

las canastas rotan una posición hacia la izquierda.

Ejemplo:

```text
1 - 2 - 3 - 4
```

pasa a:

```text
2 - 3 - 4 - 1
```

Si vuelve a presionarse izquierda:

```text
3 - 4 - 1 - 2
```

Al presionar derecha:

```text
2 - 3 - 4 - 1
```

El sistema funciona como una rotación circular.

Nunca puede quedar una columna sin canasta.

Por lo tanto, toda fruta termina siendo recogida por alguna canasta:

- correcta;
- o incorrecta.

Las frutas nunca caen al suelo.

---

# 3. Frutas y canastas iniciales

La primera versión debe utilizar cuatro frutas:

- manzana;
- pera;
- banana;
- naranja.

Debe existir una canasta correspondiente para cada fruta.

Los assets actuales del proyecto deben utilizarse desde la primera versión siempre que sean adecuados.

No reemplazar innecesariamente estos assets por dibujos generados mediante CSS, Canvas o código.

Los assets permiten evaluar desde el comienzo:

- tamaños reales;
- proporciones;
- legibilidad;
- contraste;
- estética general;
- distribución del campo de juego.

---

# 4. Relación entre fruta y columna

El tipo de fruta y la columna de caída deben seleccionarse de manera independiente.

Cualquier fruta puede caer por cualquiera de las cuatro columnas.

Ejemplos válidos:

```text
banana → columna 1
banana → columna 4
pera → columna 2
manzana → columna 3
naranja → columna 1
```

Nunca asociar permanentemente una fruta con una columna fija.

La posición de aparición debe tener suficiente aleatoriedad para obligar al jugador a mover las canastas.

Puede permitirse que una misma columna se repita consecutivamente.

Sin embargo, el sistema debe evitar, cuando sea razonable, rachas excesivamente largas en una misma columna o con una misma fruta si estas generan una experiencia poco natural.

No implementar inicialmente reglas excesivamente rígidas de aleatoriedad.

---

# 5. Orden inicial de las canastas

Las cuatro canastas pueden comenzar siempre en un orden fijo.

Ejemplo:

```text
Manzana - Pera - Banana - Naranja
```

El orden inicial concreto puede ajustarse durante las pruebas.

No es necesario randomizar las canastas al comenzar una partida.

Una vez iniciada la partida, el orden cambiará constantemente debido a las acciones del jugador.

---

# 6. Controles

## 6.1 Teclado principal

Controles obligatorios:

```text
←  mover / rotar canastas hacia la izquierda
→  mover / rotar canastas hacia la derecha
Esc  pausa / continuar
```

Las teclas cursoras son el método principal de control.

El proyecto está orientado especialmente a usuarios que pueden no estar familiarizados con esquemas de videojuegos como:

```text
WASD
```

Por ese motivo, WASD no debe reemplazar a las flechas como control principal.

Puede considerarse posteriormente como alternativa opcional.

---

# 7. Precisión y respuesta de controles

La respuesta del teclado es crítica.

El movimiento de las canastas debe sentirse:

- inmediato;
- preciso;
- rápido;
- confiable.

No perder pulsaciones de teclado.

No bloquear nuevas entradas mientras una animación anterior todavía está terminando.

Si el jugador pulsa rápidamente:

```text
← ← → ←
```

todas las entradas deben procesarse correctamente y en el orden adecuado.

La lógica de posición de las canastas debe actualizarse inmediatamente.

La animación visual nunca debe bloquear la lógica del juego.

---

# 8. Animación de movimiento de canastas

Las canastas deben tener una transición visual breve al cambiar de posición.

La animación existe únicamente para:

- mejorar identidad visual;
- facilitar la lectura del movimiento;
- evitar una sensación de teletransporte brusco.

Debe ser extremadamente rápida.

Valor inicial orientativo:

```text
60–100 ms
```

Este valor no es definitivo.

Debe quedar centralizado y ser fácil de modificar.

Si la animación afecta la precisión del control, debe priorizarse siempre la respuesta del jugador.

La animación puede activarse o desactivarse desde Configuración mediante la opción:

```text
Animación de canastas
```

Su estado predeterminado debe ser activado. Al desactivarla, cada cambio de posición debe mostrarse de inmediato, sin transiciones ni copias visuales, manteniendo intacta la misma lógica de juego.

---

# 9. Movimiento circular

Cuando una canasta sale por un extremo debe reaparecer por el opuesto.

Ejemplo hacia la izquierda:

```text
1 2 3 4
↓
2 3 4 1
```

Ejemplo hacia la derecha:

```text
1 2 3 4
↓
4 1 2 3
```

La rotación debe mantenerse consistente independientemente de la velocidad con la que el jugador pulse las teclas.

El wrap debe verse como una cinta circular continua: la canasta que sale progresivamente por un borde debe aparecer simultáneamente por el borde opuesto, aprovechando el recorte del campo de juego. No debe verse un teletransporte, una desaparición brusca ni una canasta atravesando todo el campo.

Cualquier representación adicional utilizada para este efecto debe ser exclusivamente visual: no forma parte de las capturas, no modifica el orden lógico de las canastas y debe eliminarse al terminar o interrumpirse la animación. La posición lógica debe actualizarse inmediatamente y una animación activa nunca debe bloquear nuevas pulsaciones.

---

# 10. Caída de frutas

Cada fruta:

1. aparece en la zona superior;
2. se asigna a una de las cuatro columnas;
3. cae verticalmente;
4. mantiene esa columna hasta llegar a las canastas;
5. se evalúa al producirse la captura;
6. desaparece;
7. se registra el resultado.

Desde v0.2 puede existir una colección de frutas activas. Cada fruta conserva de forma independiente su tipo, columna, posición vertical, elemento visual y estado.

La primera fruta aparece al comenzar la partida. Las siguientes aparecen de forma escalonada según `spawnInterval`, siempre que la cantidad activa sea menor que `maxActiveFruits`.

No deben generarse grupos completos en el mismo instante ni varias frutas en un mismo frame por acumulación de tiempo.

---

# 11. Velocidad global

Todas las frutas activas deben utilizar la misma velocidad global de caída.

No utilizar frutas con velocidades individuales diferentes.

Desde v0.2.1, cada dificultad define una velocidad inicial y una velocidad máxima. Desde v0.2.2, la velocidad global aumenta con una curva suave no lineal para que el cambio resulte perceptible desde los primeros aciertos, incluso en partidas cortas:

```text
progreso bruto = correctas / objetivo
progreso = raíz cuadrada de limitar(progreso bruto, 0, 1)
velocidad actual = velocidad inicial + (velocidad máxima - velocidad inicial) × progreso
```

El progreso y la velocidad deben mantenerse dentro de sus límites. Al inicio se usa la velocidad inicial; al acercarse al objetivo, la velocidad se acerca suavemente a la máxima sin superarla.

Todas las frutas activas comparten la misma velocidad global calculada en cada frame. Si una penalización reduce las correctas, la velocidad también puede disminuir hasta el valor correspondiente al nuevo progreso.

---

# 12. Frutas simultáneas

"Frutas simultáneas" significa la cantidad máxima de frutas que pueden permanecer activas al mismo tiempo dentro del campo, no que aparezcan exactamente juntas.

El flujo es escalonado:

- aparece la primera fruta al comenzar;
- cada `spawnInterval` puede aparecer otra si existe un slot disponible;
- cuando una fruta se captura, su slot vuelve a quedar disponible;
- el spawn continúa respetando la misma cadencia.

Puede permitirse que dos frutas aparezcan en la misma columna.

No es necesario impedirlo.

Debe evitarse una superposición visual problemática mediante valores razonables de velocidad e intervalo.

---

# 13. Dificultad

El diseño previsto incluye:

- Fácil;
- Normal;
- Difícil;
- Custom.

Las tres variables principales de dificultad son:

```text
rango de velocidad global
cantidad de frutas simultáneas
intervalo entre spawns
```

Los presets funcionales son Fácil, Normal, Difícil y Custom. Cada uno define `startFallSpeed` y `maxFallSpeed`. Fácil utiliza 135–190 y permite una fruta activa con intervalo de 1500 ms; Normal utiliza 180–270 y permite hasta dos con intervalo de 1150 ms; Difícil utiliza 225–350 y permite hasta tres con intervalo de 850 ms.

Los valores están centralizados en `DIFFICULTY_PRESETS` y deben mantenerse fáciles de ajustar.

Deben considerarse valores de balance sujetos a pruebas.

---

# 14. Modo Custom

El modo Custom permite modificar manualmente:

- velocidad inicial;
- velocidad máxima;
- cantidad máxima de frutas simultáneas;
- intervalo de spawn;
- cantidad objetivo de frutas;
- penalización por error.

Los controles utilizan límites conservadores centralizados para impedir valores que rompan el flujo o produzcan superposiciones extremas. La velocidad máxima se normaliza para que nunca quede por debajo de la inicial. No existe persistencia de estas opciones.

---

# 15. Objetivo de partida

La condición principal de victoria será alcanzar una cantidad determinada de frutas recogidas correctamente.

Ejemplo:

```text
Objetivo: 20 frutas correctas
```

La cantidad objetivo es configurable antes de comenzar la partida y se mantiene al reintentar. Existen accesos rápidos para 10, 20, 30 y 50 que actualizan el mismo campo numérico utilizado por el juego; la entrada manual de otros valores continúa disponible.

No utilizar inicialmente una partida limitada exclusivamente por tiempo.

El tiempo debe medirse para estadísticas y feedback final.

---

# 16. Errores

Una captura incorrecta ocurre cuando una fruta entra en una canasta correspondiente a otro tipo de fruta.

Debe registrarse como error.

El juego permite configurar si un error:

- solamente aumenta el contador de errores;
- o además resta progreso / puntuación.

La opción equivale a:

```text
Los errores restan progreso:
Sí / No
```

Cuando está activada, cada error resta una correcta sin permitir que el progreso baje de 0.

---

# 17. Feedback visual de captura

El feedback debe ser localizado y claro.

## Captura correcta

La canasta involucrada puede mostrar brevemente:

- halo verde;
- borde verde;
- resplandor verde;
- efecto equivalente.

## Captura incorrecta

La canasta involucrada puede mostrar brevemente:

- halo rojo;
- borde rojo;
- resplandor rojo;
- efecto equivalente.

Evitar inicialmente flashes de pantalla completa.

El efecto debe:

- ser visible;
- ser breve;
- no molestar;
- no ocultar el gameplay;
- no interrumpir los controles.

La duración e intensidad deben quedar fácilmente ajustables.

---

# 18. Feedback sonoro

Debe existir:

- sonido de acierto;
- sonido de error.

Los sonidos deben ser:

- breves;
- suaves;
- fácilmente diferenciables;
- no estridentes.

Para las primeras versiones pueden generarse mediante Web Audio API si resulta conveniente.

Posteriormente pueden reemplazarse por archivos reales.

---

# 19. Música

El proyecto contempla música de fondo.

La música debe tener una estética:

- simpática;
- alegre;
- ligera;
- arcade;
- apropiada para un escenario veraniego y colorido.

La música puede generarse posteriormente mediante herramientas externas.

No es necesario que Codex genere música.

La música NO es requisito obligatorio de v0.1.

---

# 20. Gamepad

Se contempla soporte futuro mediante Gamepad API.

Objetivo:

permitir jugar con controles como:

- Xbox Controller;
- gamepads compatibles con navegador.

Controles previstos:

```text
D-Pad izquierda
D-Pad derecha
```

No implementar necesariamente en v0.1.

La prioridad inicial es:

```text
teclado + gameplay
```

---

# 21. Pausa

La tecla:

```text
Esc
```

debe pausar y continuar la partida.

Durante la pausa:

- las frutas deben detenerse;
- no deben registrarse capturas;
- el tiempo de partida debe detenerse;
- debe mostrarse claramente que el juego está pausado.

La pausa no debe modificar el estado de las canastas ni reiniciar la fruta actual.

---

# 22. Menú principal

Debe existir una pantalla inicial.

Opciones previstas:

```text
JUGAR
CONFIGURACIÓN
```

Puede mostrarse además una indicación breve:

```text
Usá ← y → para mover las canastas
```

No implementar todavía instrucciones extensas.

Las instrucciones completas deben redactarse cerca del final del proyecto, cuando las reglas estén estabilizadas.

---

# 23. Configuración

La pantalla de configuración debe diseñarse para crecer progresivamente.

Parámetros funcionales desde v0.2:

- preset de dificultad;
- cantidad objetivo;
- penalización de errores;
- sonido;
- configuración Custom.

La opción funcional `Animación de canastas` permite activar o desactivar el movimiento visual circular. Su estado predeterminado es activado y puede cambiarse antes de iniciar una partida.

La configuración Custom incluye velocidad inicial, velocidad máxima, máximo de frutas activas e intervalo de spawn. La música continúa fuera del alcance actual.

Evitar crear opciones que todavía no tengan función real.

---

# 24. HUD

El HUD debe ubicarse preferentemente en el lateral izquierdo del área arcade.

Debe evitar el aspecto típico de una tarjeta genérica de página web.

Buscar una apariencia más cercana a:

- videojuego arcade;
- panel de máquina recreativa;
- interfaz integrada al juego.

Información prevista:

```text
FRUIT BASKET
Dificultad
Correctas
Errores
Objetivo
Tiempo
```

El HUD muestra además una barra horizontal discreta junto a Correctas y Objetivo. Representa `correctas / objetivo`, comienza vacía, se limita al 100 % y también disminuye si una penalización resta progreso.

No sobrecargar el HUD con información innecesaria.

Durante la primera versión puede simplificarse.

---

# 25. Campo de juego

El juego debe tener orientación vertical.

Relación de aspecto inicial recomendada:

```text
3:4
```

Puede ajustarse durante las pruebas.

No considerar esta proporción como un valor absoluto.

La estética buscada es similar a un arcade vertical clásico.

En pantallas panorámicas quedará espacio lateral disponible.

Ese espacio podrá utilizarse posteriormente para:

- bezel;
- marquee;
- decoración arcade;
- elementos gráficos.

En las primeras versiones puede permanecer simple.

---

# 26. Resoluciones objetivo

Debe probarse especialmente en:

```text
1920 × 1080
1366 × 768
```

El juego debe permanecer completamente visible y usable en ambas.

Evitar:

- botones fuera de pantalla;
- HUD cortado;
- canastas fuera del playfield;
- frutas excesivamente pequeñas;
- texto ilegible;
- scroll vertical durante gameplay normal.

Debe tolerar razonablemente escalas y zoom habituales de usuarios de PC.

---

# 27. Escenario visual

La estética final deseada es:

- alegre;
- veraniega;
- luminosa;
- amigable;
- pixel art / arcade.

Referencia conceptual:

- cielo celeste;
- ambiente de día;
- árboles frutales laterales;
- vegetación;
- colores agradables.

Desde v0.3.1, el fondo interno del gameplay se construye mediante capas independientes y ajustables, tomando como referencia de composición la captura de Catch'n Avoid: cielo veraniego con degradé generado por código, el asset `sun.png` arriba a la derecha, pocas nubes creadas con `cloud_1.png`, `cloud_2.png` y `cloud_3.png`, y el asset `surface_light.png` repetido en la base como apoyo visual de las canastas. Las posiciones, tamaños y velocidades de estos elementos se mantienen centralizados para facilitar retoques manuales sin afectar la lógica.

Las cuatro columnas continúan existiendo únicamente en la mecánica: no deben mostrarse líneas, grilla ni divisiones artificiales entre carriles. No se agregan árboles, flores, arbustos, cercas ni decoración cargada dentro del playfield. Ese tipo de ambientación se reserva para una futura iteración del bezel y los laterales externos.

La estética puede inspirarse en el estilo del Stage 1 del juego Catch'n Avoid, sin copiar necesariamente su implementación.

En v0.1 el fondo debe ser deliberadamente simple.

Primero validar gameplay.

No dedicar trabajo excesivo a decoración antes de aprobar la mecánica principal.

---

# 28. Assets

Los assets actuales del proyecto deben conservarse.

No eliminar archivos desconocidos o adicionales dentro de `assets/`.

Los assets que no se utilicen inicialmente deben permanecer intactos.

La estructura prevista puede incluir:

```text
assets/
music/
sound_effects/
```

Estas carpetas pueden ampliarse cuando sea necesario.

No mover ni renombrar assets existentes sin necesidad.

---

# 29. Estructura prevista del proyecto

Estructura general:

```text
juego canasta frutas/
│
├── assets/
│
├── music/
│
├── sound_effects/
│
├── old_versions/
│
├── AGENTS.md
├── DEVELOPMENT_SPEC.md
├── README.md
├── index.html
└── log.md
```

No es obligatorio que todas las carpetas existan desde el primer momento.

Si una etapa requiere una carpeta o archivo previsto y todavía no existe, puede crearse.

No crear estructuras adicionales innecesarias.

---

# 30. README.md

`README.md` NO debe modificarse durante el desarrollo normal.

Aunque actualmente esté vacío o tenga solamente un título, debe permanecer intacto.

El README se redactará al finalizar el proyecto.

Su función final será documentar públicamente el juego para GitHub.

Codex no debe actualizar README en cada iteración.

Solo modificarlo cuando el usuario lo solicite explícitamente al cierre del proyecto.

---

# 31. log.md

`log.md` debe mantenerse actualizado en cada iteración que produzca cambios reales.

Debe registrar:

- versión;
- fecha;
- cambios;
- decisiones técnicas relevantes;
- archivos modificados;
- estado de prueba.

Debe servir también como contexto técnico para futuras iteraciones.

No convertirlo en una copia completa del DEVELOPMENT_SPEC.

Mantenerlo breve pero suficientemente informativo.

---

# 32. DEVELOPMENT_SPEC.md como documento vivo

Este archivo representa el plan vigente del proyecto.

El diseño puede cambiar durante el desarrollo.

Si el usuario decide modificar de manera importante:

- gameplay;
- dificultad;
- arquitectura;
- controles;
- diseño;
- alcance;
- comportamiento;
- estructura del proyecto;

el prompt correspondiente podrá solicitar explícitamente que Codex actualice también `DEVELOPMENT_SPEC.md`.

No modificar este archivo automáticamente por cambios menores.

Actualizarlo cuando exista un cambio real de dirección o requisito.

El contenido actualizado debe representar siempre el rumbo vigente del proyecto.

---

# 33. Versionado

Seguir las reglas definidas en `AGENTS.md`.

El archivo principal debe comenzar con:

```html
<!-- Version: v0.1 -->
```

Las siguientes iteraciones deben incrementar la versión según corresponda.

Antes de modificar una versión funcional existente, guardar su estado dentro de:

```text
old_versions/
```

Ejemplo:

```text
old_versions/
    Ver01/
    Ver02/
    Ver03/
```

No es necesario crear una copia histórica antes de generar la primera versión porque todavía no existe una versión funcional anterior.

A partir de la segunda iteración, aplicar normalmente el sistema de copias.

---

# 34. Ajustes manuales y parámetros centralizados

El proyecto debe estar diseñado para permitir ajustes visuales manuales rápidos.

No dispersar valores importantes por todo el código.

Centralizar cuando sea razonable:

- tamaño del campo de juego;
- relación de aspecto;
- ancho del HUD;
- tamaño de las frutas;
- tamaño de las canastas;
- separación entre columnas;
- posición vertical de canastas;
- offsets;
- velocidad de caída;
- duración de animación;
- duración del feedback;
- intensidad de efectos;
- tamaños tipográficos importantes.

Ejemplo conceptual:

```css
:root {
    --game-width: ...;
    --game-height: ...;
    --fruit-size: ...;
    --basket-width: ...;
    --basket-height: ...;
    --hud-width: ...;
}
```

Y para lógica:

```javascript
const GAME_CONFIG = {
    startFallSpeed: ...,
    maxFallSpeed: ...,
    basketMoveDuration: ...,
    targetCorrectFruits: ...
};
```

Los nombres concretos pueden variar.

La prioridad es que los valores sean:

- fáciles de encontrar;
- fáciles de comprender;
- fáciles de modificar;
- reutilizados consistentemente.

Evitar números mágicos repetidos.

---

# 35. Layout adaptable

Evitar basar todo el juego en coordenadas absolutas rígidas.

Las posiciones de las cuatro columnas deben calcularse preferentemente a partir del ancho útil del playfield.

Los cambios de:

- tamaño del campo;
- tamaño de fruta;
- tamaño de canasta;

no deberían exigir rehacer manualmente todas las coordenadas.

Puede utilizarse posicionamiento absoluto cuando sea apropiado para el arcade, pero basado en parámetros centralizados.

---

# 36. Tamaños iniciales

Codex puede elegir valores razonables iniciales para:

- tamaño del playfield;
- tamaño de frutas;
- tamaño de canastas;
- HUD;
- tipografías;
- separaciones.

No es necesario definir todos esos valores antes de generar el prototipo.

Estos valores se consideran provisionales.

Deben poder ajustarse fácilmente durante las pruebas visuales.

---

# 37. Resumen final de partida

Al alcanzar el objetivo debe aparecer una pantalla o panel final.

Información mínima prevista:

```text
Partida completada
Tiempo total
Frutas correctas
Errores
```

Puede mostrar además:

```text
Reintentar
Volver al menú
```

No es necesario implementar estadísticas complejas.

---

# 38. Puntuación

Durante las primeras versiones puede utilizarse:

```text
Correctas
```

como indicador principal en lugar de un sistema abstracto de puntos.

El sistema de puntuación puede ampliarse posteriormente si aporta valor.

No agregar combos, multiplicadores o bonificaciones sin una decisión específica.

---

# 39. Sonido configurable

Posteriormente debe existir una opción para:

```text
Sonido: ON / OFF
```

La música podrá tener su propio control si se incorpora.

No obligar a reproducir audio si el usuario lo desactiva.

---

# 40. Compatibilidad

Objetivo principal:

- Google Chrome;
- Microsoft Edge;
- navegadores Chromium modernos.

No utilizar frameworks.

No agregar dependencias externas salvo necesidad real.

Preferir:

```text
HTML
CSS
JavaScript vanilla
```

---

# 41. Rendimiento

El juego debe ser liviano.

Evitar:

- cálculos innecesarios;
- loops intensivos;
- efectos gráficos excesivos;
- filtros costosos;
- animaciones que aumenten considerablemente carga de CPU/GPU.

Debe poder ejecutarse razonablemente en PCs modestas utilizadas por alumnos.

---

# 42. Principio de accesibilidad

Aunque Fruit Basket puede llegar a ser difícil, debe comenzar siendo comprensible para usuarios mayores o sin experiencia en videojuegos.

Priorizar:

- texto legible;
- buen contraste;
- objetivos claros;
- feedback evidente;
- botones grandes;
- navegación simple;
- ausencia de información innecesaria.

La dificultad debe provenir del gameplay, no de una interfaz confusa.

---

# 43. Alcance de v0.1

La versión v0.1 tiene un único objetivo principal:

```text
VALIDAR LA MECÁNICA CENTRAL DEL JUEGO
```

La pregunta que debe responder es:

> ¿Resulta claro, preciso y entretenido mover las cuatro canastas con izquierda/derecha para hacer coincidir cada fruta con su canasta?

La v0.1 NO pretende ser el juego terminado.

---

# 44. Funciones requeridas en v0.1

Implementar:

- `index.html`;
- comentario de versión;
- menú inicial simple;
- botón Jugar;
- configuración básica si resulta necesaria;
- HUD básico;
- escenario vertical provisional;
- cuatro columnas invisibles;
- cuatro frutas utilizando assets reales;
- cuatro canastas utilizando assets reales;
- orden inicial fijo;
- movimiento circular de canastas;
- flecha izquierda;
- flecha derecha;
- respuesta inmediata;
- animación corta y no bloqueante;
- una fruta simultánea;
- velocidad fija;
- selección aleatoria de fruta;
- selección aleatoria de columna;
- captura correcta;
- captura incorrecta;
- contador de correctas;
- contador de errores;
- objetivo de partida;
- feedback visual verde;
- feedback visual rojo;
- sonido sencillo de acierto;
- sonido sencillo de error;
- medición de tiempo;
- pausa con Esc;
- final de partida;
- pantalla final básica;
- reiniciar partida;
- volver al menú.

---

# 45. Funciones NO requeridas en v0.1

No implementar todavía salvo necesidad técnica:

- múltiples frutas simultáneas;
- progresión interna de velocidad;
- presets completos Fácil / Normal / Difícil;
- modo Custom completo;
- joystick;
- Gamepad API;
- música;
- bezel;
- marquee;
- decoración avanzada;
- árboles complejos;
- partículas;
- frutas especiales;
- power-ups;
- combos;
- puntuación avanzada;
- instrucciones completas;
- estadísticas persistentes;
- récords;
- localStorage;
- sistemas online.

---

# 46. Criterios de éxito de v0.1

La v0.1 será considerada satisfactoria si permite evaluar correctamente los siguientes puntos.

## Control

- las flechas responden inmediatamente;
- no se pierden pulsaciones rápidas;
- pueden realizarse varios movimientos consecutivos;
- la animación no bloquea controles;
- el orden lógico de canastas permanece correcto.

## Lectura visual

- se identifica fácilmente la fruta;
- se identifica claramente la columna;
- se distingue cada canasta;
- las cuatro posiciones se comprenden de forma natural.

## Movimiento

- la rotación circular resulta intuitiva;
- la animación acompaña al movimiento;
- no genera retraso perceptible;
- no produce saltos visuales molestos.

## Capturas

- las capturas correctas se detectan correctamente;
- las incorrectas también;
- no existen frutas que atraviesen las canastas;
- no se generan dobles capturas accidentales.

## Feedback

- verde = acierto;
- rojo = error;
- sonido correcto y error son diferenciables;
- el feedback no bloquea la partida.

## Gameplay

- aparece una fruta;
- se captura;
- aparece la siguiente rápidamente;
- tipo y columna varían;
- el objetivo puede completarse;
- el juego termina correctamente.

## Pausa

- Esc pausa;
- Esc continúa;
- fruta y tiempo se congelan correctamente.

## Resolución

Verificar al menos:

```text
1920×1080
1366×768
```

Sin elementos importantes fuera de pantalla.

---

# 47. Pruebas manuales de v0.1

El usuario debe probar especialmente:

### A. Sensación del control

Preguntas:

- ¿las canastas responden suficientemente rápido?
- ¿la animación molesta?
- ¿se siente retraso?
- ¿se pueden hacer correcciones rápidas?

### B. Tamaños

Evaluar:

- fruta demasiado grande / pequeña;
- canastas demasiado grandes / pequeñas;
- playfield demasiado ancho / angosto;
- HUD demasiado grande;
- separación entre columnas.

Modificar mediante parámetros centralizados.

### C. Velocidad

Comprobar si la velocidad base resulta:

- demasiado lenta;
- adecuada;
- demasiado rápida.

La velocidad inicial es provisional.

### D. Feedback

Comprobar:

- intensidad del verde;
- intensidad del rojo;
- duración;
- sonidos;
- claridad.

### E. Layout

Comprobar:

- relación 3:4;
- ubicación del HUD;
- aspecto general;
- aprovechamiento de la pantalla;
- funcionamiento en notebook 1366×768.

---

# 48. PASO 1 — v0.1: mecánica base

Objetivo:

crear un prototipo funcional completo pero simple.

Debe permitir jugar una partida básica de principio a fin.

Prioridades:

1. controles;
2. movimiento de canastas;
3. caída de fruta;
4. detección de captura;
5. feedback;
6. estabilidad;
7. layout.

No dedicar tiempo excesivo a decoración.

---

# 49. PASO 2 — Ajuste fino de gameplay

Después de probar v0.1:

ajustar manualmente o mediante Codex:

- tamaño de fruta;
- tamaño de canastas;
- playfield;
- HUD;
- velocidad;
- animación;
- feedback;
- sonidos;
- separación;
- distribución visual.

No agregar todavía sistemas nuevos si la base necesita correcciones.

---

# 50. PASO 3 — Sistema de dificultad (implementado en v0.2)

Implementado:

- Fácil;
- Normal;
- Difícil;
- Custom.

Los valores iniciales son conservadores y quedan sujetos a pruebas de balance.

Variables:

- velocidad;
- cantidad simultánea;
- intervalo de spawn.

---

# 51. PASO 4 — Múltiples frutas (implementado en v0.2)

Se agregó soporte para:

- 2 frutas;
- 3 frutas;
- cantidad superior si las pruebas lo justifican.

Verificar:

- colisiones;
- capturas;
- orden;
- misma columna;
- rendimiento;
- legibilidad.

---

# 52. PASO 5 — Progresión de velocidad (implementada en v0.2.1)

La velocidad global aumenta de forma continua mediante la raíz cuadrada del progreso de correctas respecto del objetivo, limitada entre 0 y 1. Esta curva hace perceptible la aceleración desde el comienzo sin introducir saltos ni superar el máximo.

Parámetros:

```text
startFallSpeed
maxFallSpeed
```

Todas las frutas deben utilizar la misma velocidad global vigente.

La velocidad puede disminuir si una penalización reduce el progreso. No introducir velocidades individuales salvo decisión posterior.

---

# 53. PASO 6 — Configuración base (implementada en v0.2)

Se implementaron controles básicos de:

- dificultad;
- objetivo;
- penalización;
- sonido;
- Custom;
- velocidad inicial, velocidad máxima, cantidad activa e intervalo para Custom.

---

# 54. PASO 7 — Gamepad

Evaluar e implementar Gamepad API.

Probar al menos con un control compatible tipo Xbox si está disponible.

Mantener teclado funcionando simultáneamente.

---

# 55. PASO 8 — Arte y escenario

Una vez aprobado el gameplay:

mejorar:

- fondo;
- árboles;
- vegetación;
- cielo;
- decoración;
- bezel;
- laterales;
- HUD arcade.

Mantener buen rendimiento.

---

# 56. PASO 9 — Música y audio final

Agregar:

- música;
- efectos finales;
- niveles de volumen si resultan necesarios;
- opción de mute.

---

# 57. PASO 10 — Instrucciones

Cuando las reglas estén estabilizadas:

crear instrucciones definitivas.

Deben ser:

- cortas;
- claras;
- visuales;
- aptas para usuarios mayores.

---

# 58. PASO 11 — Pruebas finales

Probar:

- Fácil;
- Normal;
- Difícil;
- Custom;
- teclado;
- gamepad si existe;
- 1920×1080;
- 1366×768;
- Chrome;
- Edge;
- zoom / escala razonable;
- sonido;
- música;
- pausa;
- reintento;
- menú.

---

# 59. PASO 12 — README y cierre

Solo cuando el proyecto se considere finalizado:

- redactar `README.md`;
- describir juego;
- controles;
- requisitos;
- estructura;
- uso;
- créditos si corresponde;
- assets utilizados;
- estado final.

También:

- actualizar `log.md`;
- confirmar versión final;
- guardar copia correspondiente en `old_versions/`;
- revisar archivos;
- eliminar únicamente archivos temporales cuya eliminación haya sido autorizada.

---

# 60. Principio general de desarrollo

Fruit Basket debe construirse en iteraciones pequeñas.

Primero:

```text
MECÁNICA
```

Después:

```text
BALANCE
```

Después:

```text
DIFICULTAD
```

Después:

```text
ARTE Y AUDIO
```

Ante dos soluciones equivalentes:

- preferir la más simple;
- preferir la más fácil de ajustar;
- preferir la que no bloquee futuras modificaciones;
- evitar dependencias;
- evitar reescrituras innecesarias;
- respetar siempre cambios manuales realizados por el usuario.

La prioridad inicial es:

```text
Ver fruta → mover canastas → capturar → recibir feedback → repetir.
```
