# Unidad 6 ☎️𝄞♔꧂

## Agentes autónomos ☎️𝄞♔꧂

## Actividad 03: encargo de diseño

Para este encargo de diseño vamos a trabajar con la canción [*Girl Like Me*](https://youtu.be/qRAJowgHqxA?si=UsrJC73w6zfGMk16)[ de PinkPantheress](https://youtu.be/qRAJowgHqxA?si=UsrJC73w6zfGMk16).

<img width="736" height="736" alt="image" src="https://github.com/user-attachments/assets/1389ab92-567f-43da-bed4-7446c8050112" />

**LINK ENTREGA:** https://cookielolwow.github.io/InteractivOOOOOSFUerzas/

---

# Bitácora y autoevaluación — Unidad 6: Agentes autónomos☎️𝄞♔꧂

## Proyecto☎️𝄞♔꧂

## Intención artística☎️𝄞♔꧂

Elegí *Girl Like Me* porque me gustaba mucho la estetica que ella maneja en su marca personal.


<img width="735" height="478" alt="image" src="https://github.com/user-attachments/assets/4aa77ebb-f9f7-41d4-81d2-1002292acb8f" />


Mientras pensaba en esto, me acorde que el video musical de esta canción estaba inspirado en rythym heaven y yo queria que el instrumento  tuviera esa vibe.

Tomé esa idea como inspiración, pero no quería copiarla literalmente. En el instrumento, los golpes de la canción se convierten en rebotes escalonados, los recortes cambian de pose por pasos y los stickers aparecen como una respuesta rápida a las acciones. Al mismo tiempo, los agentes siguen teniendo sus propias reglas y pueden generar movimientos que no están definidos de antemano.
Quise representar ese contraste con un enjambre que puede juntarse, alinearse, separarse, seguir corrientes o formar caminos. El escenario toma referencias visuales de Londres, especialmente con el tartán, las fotografías y los recortes. Estos elementos ayudan a construir la identidad visual, pero no controlan directamente el movimiento de los agentes.

Tampoco quería que cada partícula representara una nota específica. Los cuatro tipos de recortes funcionan más como diferentes capas visuales y musicales dentro del grupo. Lo que se ve en cada momento depende de las reglas de los agentes, las estelas que van dejando y las decisiones que tomo mientras interpreto.

## Cómo funciona el instrumento☎️𝄞♔꧂

### Percepción y acción de cada agente

Cada agente tiene su propia posición, velocidad, aceleración, límite de velocidad y fuerza, además de radios de percepción y separación, sensores para las estelas y un estado de rebote rítmico.

Para saber qué está pasando a su alrededor, cada agente consulta únicamente a los agentes cercanos mediante una cuadrícula espacial. No conoce el estado completo del enjambre ni tiene una trayectoria definida.

Dentro de su radio de percepción utiliza tres comportamientos principales de flocking:

* **Separación:** se aleja de los vecinos que están demasiado cerca.
* **Alineación:** intenta ajustar su dirección según la velocidad de los vecinos.
* **Cohesión:** intenta acercarse hacia la posición promedio del grupo que tiene cerca.

Además de esto, cada agente consulta el campo de flujo en la posición donde se encuentra. El campo solamente le indica una dirección y el agente convierte esa información en una fuerza de steering.

Cuando Physarum está activo, el agente también revisa tres sensores que están ubicados delante de él: izquierda, centro y derecha. Dependiendo de cuál tenga una señal más fuerte, cambia su dirección.

Las estelas se van creando cerca de los agentes, se difunden y después desaparecen poco a poco. Esto hace que funcionen como una especie de memoria temporal del movimiento colectivo.

La combinación principal de fuerzas es:

```text
F_total = w_sep · F_sep + w_ali · F_ali + w_coh · F_coh + w_flow · F_flow
```

Los pesos de estas fuerzas se pueden modificar desde los controles. Physarum también afecta la dirección dependiendo de lo que detectan sus sensores.

Además, las acciones que hago con el teclado y el mouse pueden aplicar impulsos temporales al sistema. Después de recibir estas fuerzas, cada agente actualiza su velocidad y posición respetando sus límites.

### Conducción humana

El score está dividido en seis momentos. Cada uno tiene una intención visual y algunas acciones que puedo utilizar durante la canción.

Estas secciones no funcionan como una coreografía automática. Puedo escoger una sección, cambiar de acción, mantener un estado o simplemente esperar a ver qué hace el sistema.

Si la canción está reproduciéndose, su reloj sirve para acompañar las transiciones del fondo. Sin embargo, el audio no se analiza automáticamente para decidir cómo se mueven los agentes.

Las acciones globales tampoco duran para siempre. Tienen una duración y van perdiendo fuerza, por lo que después las reglas locales vuelven a tener mayor importancia.

De esta manera, yo no estoy controlando directamente a cada agente. Estoy modificando las condiciones del sistema y dejando que el comportamiento colectivo aparezca a partir de esas reglas.

## Controles de interpretación☎️𝄞♔꧂

| Control                  | Acción en el instrumento                                                                                                |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| **Q** o **espacio**      | Marca un golpe y activa el rebote escalonado de los agentes junto con el acento de papel del escenario.                 |
| **A**                    | Dispersa el enjambre y aumenta temporalmente la separación.                                                             |
| **S**                    | Reúne el enjambre y aumenta temporalmente la cohesión.                                                                  |
| **D**                    | Cambia entre los modos de flujo y permite generar un giro alrededor del centro.                                         |
| **C**                    | Cambia el peso de cohesión para acercar o soltar el grupo.                                                              |
| **V**                    | Cambia el peso de separación para abrir o cerrar el enjambre.                                                           |
| **F** o **T**            | Activa o desactiva las estelas de Physarum.                                                                             |
| **1–6**                  | Selecciona una sección del score y aplica su preset de parámetros.                                                      |
| **I**                    | Hace aparecer brevemente una fotografía de PinkPantheress como un recorte con efecto stop motion. Es una acción manual. |
| **B**                    | Activa un salto de papel dentro del collage.                                                                            |
| **L**                    | Reproduce o pausa *Girl Like Me*.                                                                                       |
| **P**                    | Activa o desactiva la base sintética 2-step de 138 BPM.                                                                 |
| **Clic sobre el lienzo** | Cambia entre dispersión, agrupación, órbita y deriva libre desde el punto seleccionado.                                 |
| **M** o **F2**           | Oculta o muestra la interfaz para utilizar el instrumento en proyección.                                                |
| **R**                    | Reinicia la distribución de los agentes y limpia las estelas.                                                           |

El panel **PARÁMETROS** permite cambiar el radio de percepción, el radio de separación, la fuerza máxima, la velocidad máxima, la evaporación de las estelas y la cantidad de agentes. También permite visualizar los vectores del flow field.

Los botones del dock funcionan como accesos rápidos para marcar golpes, reunir, dispersar, girar y activar Physarum.

## Partitura visual☎️𝄞♔꧂

El score funciona como una guía para la interpretación. No indica exactamente qué tengo que hacer en cada segundo, sino que propone diferentes posibilidades dependiendo de lo que esté pasando con la música y con el enjambre.

| Sección                    | Pasaje e intención                                   | Posible decisión interpretativa                                                        |
| -------------------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **1. Intro — 0:00–0:18**   | Voz cercana; sensación de reposo e intimidad.        | Reunir el grupo y dejar que aparezcan poco a poco las primeras estelas.                |
| **2. Verso 1 — 0:18–0:45** | Entra el 2-step y empieza a aparecer más movimiento. | Marcar algunos golpes con Q o espacio y probar otro modo de flujo con D.               |
| **3. Coro 1 — 0:45–1:12**  | El estribillo se siente más expansivo.               | Dispersar con A y decidir si mantener Physarum activo.                                 |
| **4. Puente — 1:12–1:40**  | Hay cortes sincopados y cambia la energía.           | Girar el campo con D y observar cómo responde el sistema antes de volver a intervenir. |
| **5. Coro 2 — 1:40–2:05**  | Momento de mayor intensidad.                         | Alternar entre reunión, dispersión y golpes según lo que se esté escuchando.           |
| **6. Outro — 2:05–2:25**   | La voz y la energía comienzan a desaparecer.         | Reducir las intervenciones y dejar que las estelas se vayan disolviendo.               |

## Registro de decisiones y aprendizaje☎️𝄞♔꧂

### Pasar de un movimiento decorativo a un instrumento

Una de las cosas que tuve en cuenta fue que los controles realmente produjeran cambios que se pudieran notar. Por eso los organicé alrededor de acciones como abrir, reunir, girar, seguir estelas y marcar el pulso.

La idea era que interactuar con el sistema no se sintiera como cambiar parámetros porque sí, sino que cada cambio tuviera una consecuencia visual durante la interpretación.

### Separar el campo de las reglas de los agentes

El flow field define una dirección diferente dependiendo de la zona del espacio. Cada agente consulta esa dirección desde su propia posición y después la convierte en una fuerza de steering.

Esta separación me ayudó a entender mejor qué estaba pasando. Si cambio el modo del flow field, cambia el mapa de direcciones. Si cambio el peso del flow field, cambia cuánto afecta esa dirección al movimiento del agente.

### Integrar Physarum como memoria compartida

Las estelas funcionan como una memoria temporal del movimiento.

Los agentes dejan una señal mientras se mueven y después utilizan sensores para detectar dónde hay mayor concentración de esa señal. Como la estela se difunde y se evapora, esa memoria no permanece para siempre.

El control de Physarum permite decidir en qué momentos quiero que esa memoria sea más visible y tenga mayor influencia sobre el comportamiento.

### Construir una identidad de collage

Para la parte visual mantuve el tartán como soporte y reforcé la referencia a Londres usando fotografías recortadas de lugares como Westminster y Big Ben, además de elementos como una cabina telefónica y un taxi.

La ciudad está construida en diferentes capas que se mueven a distintas escalas y velocidades. También utilicé inclinaciones por pasos, bordes de papel y pequeños acentos para que todo se sintiera más como un collage armado a mano.

La fotografía de PinkPantheress aparece mediante una intervención manual. Su posición y duración pueden cambiar y el movimiento por cuadros le da una sensación de stop motion, sin convertirlo en una animación automática.

### Reducir el ruido visual y mejorar la lectura

Durante el proceso también reduje algunos elementos que estaban haciendo que la escena se sintiera demasiado cargada.

Reemplacé los destellos genéricos por pequeños fragmentos de papel y trabajé una paleta más controlada. También ajusté la escala y el contorno de los agentes para que se entendieran como recortes y no como partículas luminosas.

Los golpes ahora utilizan pequeños fragmentos opacos en lugar de una placa grande que terminaba tapando demasiado el escenario.

Los stickers de respuesta muestran solamente la acción que acaba de ocurrir, como **BEAT!**, **SCATTER!** o **SPIN!**. La idea era que funcionaran como feedback rápido sin convertirse en otro elemento que compitiera con el resto de la composición.

### Optimizar la animación

Para que el sistema pudiera manejar una mayor cantidad de agentes, utilicé una cuadrícula espacial para evitar comparar cada agente con todos los demás.

El búfer de Physarum funciona a una resolución menor y el flow field se actualiza en fotogramas alternos. También reutilicé las fotografías ya preparadas con sus bordes y sombras para no tener que repetir ese trabajo durante cada frame.

## Verificación del prototipo☎️𝄞♔꧂

| Comprobación                  | Resultado observable                                                                                                           |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Compilación de producción** | `npm run build` genera la aplicación de Vite sin errores.                                                                      |
| **Percepción limitada**       | El radio configurado desde el panel cambia la distancia a la que cada agente considera a sus vecinos.                          |
| **Flocking**                  | Separación, alineación y cohesión se calculan individualmente a partir de los vecinos cercanos.                                |
| **Campo de flujo**            | D permite cambiar entre corriente, vórtice y ondas; los agentes consultan la dirección correspondiente a su posición.          |
| **Physarum**                  | F o T activa y desactiva el sistema de estelas y su consulta mediante sensores.                                                |
| **Intervención en vivo**      | A, S, D, C, V y el clic permiten cambiar fuerzas o modos. Los efectos disminuyen con el tiempo y el movimiento local continúa. |
| **Score musical**             | Las seis secciones pueden seleccionarse y cada una aplica diferentes presets.                                                  |
| **Escenario**                 | El tartán, las fotografías de Londres, los golpes de papel y el cameo manual se renderizan dentro del canvas.                  |
| **Modo de proyección**        | M o F2 permite ocultar el HUD sin detener la animación.                                                                        |

La implementación está organizada para poder identificar y explicar cada regla por separado. Para comprobar el funcionamiento del instrumento se tuvieron en cuenta tanto el comportamiento esperado como la observación directa de los controles y la compilación de producción.

## Autoevaluación — 100 / 100☎️𝄞♔꧂

| Criterio                       |       Puntaje | Evidencia que sustenta la valoración                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------ | ------------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Cumplimiento del encargo**   |   **25 / 25** | El instrumento funciona en navegador, integra la pieza musical, actualiza el canvas en tiempo real y cuenta con modo de proyección. También utiliza steering, flocking, flow field y Physarum. Evidencia: [src/main.js](src/main.js), [src/agents/AgentSystem.js](src/agents/AgentSystem.js) y [src/background.js](src/background.js).                                                            |
| **Comprensión y verificación** |   **25 / 25** | Puedo explicar cómo funciona el agente, qué percibe, cómo se combinan las fuerzas, cómo consulta el campo y cómo utiliza las estelas. El panel permite modificar diferentes parámetros y comprobar sus efectos. Evidencia: [src/agents/Boid.js](src/agents/Boid.js), [src/agents/FlowField.js](src/agents/FlowField.js) y [src/agents/PhysarumTrailBuffer.js](src/agents/PhysarumTrailBuffer.js). |
| **Diseño e intención**         |   **25 / 25** | Las reglas de movimiento buscan representar elementos como la síncopa, la expansión, la tensión y la disolución. El score y el collage británico ayudan a conectar la parte musical con la visual. Evidencia: [src/visualScore.js](src/visualScore.js), [src/background.js](src/background.js) y [src/styles.css](src/styles.css).                                                                |
| **Interpretación humana**      |   **25 / 25** | Durante la ejecución puedo elegir secciones, marcar golpes, cambiar el flujo, activar Physarum y modificar la reunión o dispersión del grupo. También puedo decidir cuándo aparece el recorte fotográfico. La interpretación depende de mis decisiones y no de un análisis automático del audio. Evidencia: [src/main.js](src/main.js) y [src/ui/camcorderUI.js](src/ui/camcorderUI.js).          |
| **Total**                      | **100 / 100** | Los cuatro criterios corresponden a decisiones que están implementadas dentro del prototipo y pueden verificarse en sus diferentes componentes.                                                                                                                                                                                                                                                   |
