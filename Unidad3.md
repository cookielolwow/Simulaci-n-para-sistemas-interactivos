# Unidad 3: Fuerzas  ヾ(⌐■_■)ノ♪ 🪩
## Actividad 03: encargo de diseño 

### Intención del instrumentoヾ(⌐■_■)ノ♪ 🪩

Desde que empezamos a hablar de la actividad, la verdad es que solo tuve una forma de visualizarla y entender qué era lo que quería hacer.

<img width="703" height="436" alt="image" src="https://github.com/user-attachments/assets/1d126eb1-f8fe-4a37-b8e1-6a0630b3a64a" />

Literalmente solo pude entenderlo como de esa forma. 


Escuchando LesAlpx me imaginé como una DJ, pero en vez de estar mezclando sonidos estaría “tocando” una masa de figuras o partículas. Por eso empecé a pensar el proyecto como una especie de mesa de DJ, pero visual, donde las teclas del computador fueran los controles que me permiten intervenir en el sistema.

Me lo imagino con faders, barritas y botones, pero todos esos controles estarían realmente en el teclado. La idea no es que en pantalla aparezca una mesa llena de botones, sino que yo pueda aprenderme qué hace cada tecla y utilizarla durante la canción como si estuviera tocando un instrumento.

Algo que tuve claro mientras desarrollaba la idea es que no quiero que cada tecla sea un “modo” diferente que reemplaza lo que estaba pasando antes. Quiero que las teclas se comporten como instrumentos que puedo tocar encima de un estado que sigue evolucionando.

Por ejemplo, puedo aumentar un vórtice manteniendo una tecla y, mientras ese movimiento sigue ocurriendo, presionar otras teclas para generar golpes asi simulando q somos djs.


**Faders**

Los faders serían controles que se mantienen presionados y modifican progresivamente una fuerza:

- A / Z → Atracción +/-
- D / C → Vórtice +/-
- F / V → Drag +/-
- G / B → Wind +/-
- H / N → Recover +/-

La intención es que mantener una tecla sea parecido a mover lentamente un fader. Por ejemplo, mantener D hace que el vórtice aumente poco a poco, mientras que al soltarla el valor se queda donde lo dejé. De esta forma puedo hacer cambios graduales, como un fade in o un fade out, sin reiniciar la simulación.

**Eventos**

Además de los faders quiero tener teclas que funcionen como golpes o intervenciones puntuales:

- J → BEAT / PUM
- K → CLAP
- L → VOICE
- SPACE → DROP

Estos eventos no deberían cambiar permanentemente el estado de la simulación. Al presionar una tecla se genera un impulso de fuerza que aparece, afecta la masa durante un momento y después desaparece.

Por ejemplo, J puede funcionar como un “PUM”: una expansión rápida de la masa. Mientras tanto, un vórtice que ya estaba activo puede continuar.

Esto permite hacer combinaciones como:


VORTEX  ──────────────────────
           J     J   J
           PUM   PUM PUM

RECOVER  ────────────────
                  K
                 CLAP

SPACE
        DROP

        

La idea es que estos eventos puedan superponerse a las fuerzas que ya están ocurriendo, como si estuviera construyendo una composición con diferentes capas.

Relación entre LAB y PERFORMANCE

El proyecto tiene dos momentos diferentes.

                  LAB
                   │
          estudiar / verificar
                   │
                   ▼
              FUERZAS
                   │
                   ▼
             PERFORMANCE
                   │
          ┌────────┴────────┐
          │                 │
        FADERS            EVENTOS
    A/Z D/C F/V        J K L ; SPACE
          │                 │
          └────────┬────────┘
                   ▼
               PARTÍCULAS


              

El modo LAB me permite entender qué hace cada fuerza, probarla por separado y comprobar que el comportamiento que estoy imaginando realmente ocurre.

El modo PERFORMANCE, en cambio, no muestra la interfaz. La pantalla queda únicamente con la masa de partículas y la cámara. Los controles existen, pero están en el teclado y yo soy quien los interpreta.

Por eso quiero que la presentación no se sienta como una animación que simplemente responde a la canción. La composición visual nace de las decisiones auditivas que toma el intérprete mientras escucha la pieza.

La canción funciona como una restricción y como una guía para mis decisiones, pero no entra automáticamente al sistema mediante FFT, beats o análisis de audio.

**Invariante visual** 

La simulación debe conservar una masa tridimensional reconocible durante la interpretación.

No quiero que el sistema termine pareciendo un plano, una caja de partículas o un punto completamente colapsado. La masa puede cambiar y deformarse, pero debe mantener una sensación de volumen.

**Variables**

Durante la interpretación pueden cambiar:

- compactación
- dispersión
- circulación
- velocidad
- deformación
- intensidad de los movimientos
- recuperación de la masa

Estas variables permiten que una misma masa pueda pasar por diferentes estados sin convertirse en diferentes “escenas” independientes.


# **01.Instrumento funcional y publicado: URL pública, modo LAB y modo PERFORMANCE.**


https://cookielolwow.github.io/InteractivOOOOOSFUerzas/


# **02. Mapa del sistema**ヾ(⌐■_■)ノ♪ 🪩

- **RESUMEN**

| Parte       | Qué hace                            | Archivo                          |
| ----------- | ----------------------------------- | -------------------------------- |
| Estado      | posición y velocidad de partículas  | `simulation/createSimulation.js` |
| Parámetros  | intensidad, velocidad, tamaño, etc. | `simulation/parameters.js`       |
| Fuerzas     | wind, radial, vortex, drag          | `simulation/createSimulation.js` |
| Integración | actualiza velocidad y posición      | `simulation/createSimulation.js` |
| Render      | convierte el estado GPU en imagen   | `simulation/createSimulation.js` |
| LAB         | sliders, pruebas y presets          | `ui/labPanel.js`                 |
| Entrada     | teclado, puntero y modos            | `main.js`                        |
| PERFORMANCE | mapping que se diseñó        | `main.js`                        |


El instrumento parte de una simulación de partículas ejecutada mediante GPU Compute. Cada partícula posee un estado dinámico que es modificado por diferentes fuerzas antes de ser renderizado.

### Flujo general

```text
PARÁMETROS
    ↓
ESTADO DE PARTÍCULAS
    ↓
FUERZAS
    ↓
INTEGRACIÓN
    ↓
NUEVO ESTADO
    ↓
RENDER
```

### Estado

Cada partícula posee:

* **posición actual**
* **velocidad**
* **posición inicial**

La posición y velocidad se almacenan en buffers de GPU mediante `instancedArray`.

La posición inicial se guarda en `initialPositionBuffer` para permitir la fuerza `RECOVER`.

### Fuerzas

Actualmente el sistema contempla:

```text
Wind
Radial
Vortex
Drag
Recover
Beat
Clap
Voice
Drop
```

Las fuerzas se acumulan en una variable común:

```js
const force = vec3(0.0).toVar();
```

Posteriormente esa fuerza modifica la velocidad de cada partícula.

### Integración

La simulación utiliza una integración de Euler semiimplícita:

```text
Fuerza
  ↓
aceleración
  ↓
velocidad
  ↓
posición
```

En el código:

```js
v.addAssign(force.mul(dt));
p.addAssign(v.mul(dt));
```

La velocidad tiene además un límite máximo controlado por `maxSpeed`.

### Render

El estado de posición de la GPU se conecta directamente al sistema de instancias mediante:

```js
material.positionNode =
  positionBuffer.toAttribute();
```

Las partículas se representan mediante `SpriteNodeMaterial`.

El color se relaciona con la velocidad de las partículas, por lo que los cambios visuales son consecuencia del comportamiento dinámico.

### Controles

El sistema está dividido en dos modos.

#### LAB

Permite estudiar y modificar directamente los parámetros de las fuerzas.

Archivo:

```text
src/ui/labPanel.js
```

#### PERFORMANCE

La interfaz desaparece y el teclado funciona como instrumento invisible.

Archivo principal:

```text
src/main.js
```

### Mapping actual

```text
A / Z → Radial
D / C → Vortex
F / V → Drag
G / B → Wind
H / N → Recover

J      → Beat / Pum
K      → Clap
L      → Voice
SPACE  → Drop
```

Las teclas de los faders se mantienen presionadas y modifican progresivamente los parámetros. Los eventos son pulsaciones independientes que generan fuerzas temporales.

### Archivos principales

| Archivo                              | Responsabilidad                                        |
| ------------------------------------ | ------------------------------------------------------ |
| `src/main.js`                        | modos LAB/PERFORMANCE, teclado, cámara, eventos y loop |
| `src/simulation/parameters.js`       | parámetros y uniforms                                  |
| `src/simulation/createSimulation.js` | estado GPU, fuerzas, integración y render              |
| `src/ui/labPanel.js`                 | interfaz del modo LAB                                  |

---

# 03. Ficha de fuerzasヾ(⌐■_■)ノ♪ 🪩

## Fuerza radial

### Función

Controla la compactación o expansión de la masa respecto al atractor.

### Dirección

```text
atractor - posición
```

La dirección apunta desde la partícula hacia el atractor.

### Ecuación conceptual

```text
F_radial = dirección_radial × intensidad × falloff
```

En el sistema:

```js
const radialForce =
  radialDirection
    .mul(params.radialStrength)
    .mul(radialFalloff)
    .mul(params.radialEnabled);
```

### Parámetros

* `radialStrength`
* `radialEnabled`
* `softening`
* `attractor`

### Signo

```text
radialStrength > 0 → atracción
radialStrength < 0 → repulsión
```

### Predicción

Una fuerza radial positiva debería llevar las partículas hacia el atractor, mientras una fuerza negativa debería alejarlas.

### Decisión de diseño

La fuerza radial representa el gesto de **compactar / expandir** la masa.

---

## Vortex

### Función

Generar circulación y deformación de la masa.

### Dirección

La fuerza utiliza una dirección tangencial respecto al movimiento alrededor del sistema.

La intención es que Vortex produzca **remolinos tridimensionales**, sin utilizarlo como una fuerza adicional de atracción hacia el centro.

### Ecuación conceptual

```text
F_vortex = dirección_tangencial × intensidad
```

### Parámetros

* `vortexStrength`
* `vortexEnabled`

### Predicción

Al aumentar Vortex debería aumentar la circulación y la deformación de la masa.

### Decisión de diseño

Se descartó una versión que añadía una componente de cohesión radial al Vortex porque hacía que `D` llevara las partículas hacia el centro.

La intención actual es separar las funciones:

```text
Radial → compactar / expandir
Vortex → retorcer / hacer remolinos
```

---

## Drag

### Función

Reducir la velocidad de las partículas.

### Ecuación

[
F_{drag}=-cv
]

En el sistema:

```js
force.addAssign(
  v
    .mul(params.dragCoefficient)
    .mul(params.dragEnabled)
    .mul(-1.0)
);
```

### Parámetros

* `dragCoefficient`
* `dragEnabled`

### Predicción

Al aumentar Drag, la velocidad de las partículas debería disminuir progresivamente.

### Decisión de diseño

Drag funciona como un gesto de **hacer más pesada o más ligera la masa**.

---

## Wind

### Función

Introducir una fuerza constante en una dirección determinada.

### Ecuación conceptual

[
F_{wind}=W
]

Actualmente se utiliza principalmente el componente X.

```js
force.addAssign(
  params.wind.mul(params.windEnabled)
);
```

### Parámetros

* `wind`
* `windEnabled`

### Predicción

Las partículas deberían adquirir una aceleración constante en la dirección del viento.

### Decisión de diseño

Wind funciona como un control para **desplazar toda la masa dentro del espacio**.

---

## Recover

### Función

Permitir que la masa vuelva progresivamente hacia su distribución inicial.

### Ecuación conceptual

[
F_{recover}=k(p_{inicial}-p)-cv
]

Utiliza `initialPositionBuffer` como referencia.

### Parámetros

* `recoverStrength`
* `recoverEnabled`
* `initialPositionBuffer`

### Predicción

Al aumentar Recover, las partículas deberían comenzar a regresar hacia las posiciones que tenían al inicio de la simulación.

### Decisión de diseño

Recover reemplaza la necesidad de utilizar siempre un reset brusco durante PERFORMANCE. Se plantea como un gesto de **recomposición**.

---

## Beat / Pum

### Función

Generar un golpe radial breve.

### Dirección

Hacia afuera respecto al atractor.

```text
dirección radial × -1
```

### Parámetros

* `beatStrength`
* `beatDecay`
* `beatEnabled`

### Predicción

Al presionar `J`, la masa debería recibir una expansión rápida y posteriormente recuperar su dinámica habitual.

### Decisión de diseño

BEAT funciona como un evento musical, no como una modificación permanente del estado.

---

## Clap

### Función

Generar un golpe radial hacia el centro.

### Dirección

```text
dirección radial
```

### Parámetros

* `clapStrength`
* `clapDecay`
* `clapEnabled`

### Predicción

Al presionar `K`, la masa debería experimentar una contracción breve.

### Decisión de diseño

Se planteó como contraste del Beat:

```text
J → expandir
K → contraer
```

---

## Voice

### Función

Generar una perturbación más prolongada y menos percusiva.

### Dirección

Principalmente tangencial, con una componente tridimensional.

### Parámetros

* `voiceStrength`
* `voiceDecay`
* `voiceEnabled`

### Predicción

Al presionar `L`, la masa debería adquirir una perturbación que permanezca visible durante más tiempo.

### Decisión de diseño

Se planteó como una capa sostenida que contraste con los eventos cortos.

---

## Drop

### Función

Producir una transformación de mayor intensidad.

### Dirección

Expansión radial.

### Parámetros

* `dropStrength`
* `dropDecay`
* `dropEnabled`

### Predicción

Al presionar `SPACE`, la masa debería experimentar una expansión significativamente mayor que el Beat.

### Decisión de diseño

DROP representa un acontecimiento de máxima intensidad dentro de la performance.

---

# 04. Registro de pruebasヾ(⌐■_■)ノ♪ 🪩

Las cinco pruebas base corresponden a los presets proporcionados por el proyecto original. La intención es primero comprobar el comportamiento individual y después comparar esos resultados con las predicciones.

## Prueba 1 — Inercia

### Configuración

```text
Initial Speed = 0.8
Fuerzas externas = desactivadas
```

### Predicción

Las partículas deberían comenzar con una velocidad inicial y continuar desplazándose debido a su inercia.

### Observación

<img width="1144" height="974" alt="image" src="https://github.com/user-attachments/assets/a11bd876-870e-4120-b66e-57da4a0c2310" />


### Resultado

Las particulitas se quedan por ahi andando asi como relajadas, no se mueven mucho.

## Prueba 2 — Fuerza constante +X

### Configuración

```text
Wind ON
Wind X = 1.5
```

### Predicción

Las partículas deberían recibir una fuerza constante hacia el eje X positivo.

### Observación

<img width="1186" height="994" alt="image" src="https://github.com/user-attachments/assets/580c0041-efeb-4ba1-a6b4-e8848846c9df" />


### Resultado

Las particulitas si se fueron a la derecha pero al llegar al limite se devolvieron y hicieron una figurita similar a una medusita. 

## Prueba 3 — Atracción

### Configuración

```text
Radial ON
Radial Strength = +3
```

### Predicción

Las partículas deberían experimentar una fuerza hacia el atractor.

### Observación

<img width="833" height="763" alt="image" src="https://github.com/user-attachments/assets/a06c6e0b-0e43-408d-b054-062bf5ed9cfb" />


### Resultado

La predicción direccional se cumplió, las particulitas si se dirigieron hacia el atarcator, pero el comportamiento visual llevó a plantear la necesidad de una fuerza o regla adicional que preserve la masa.

### Decisión

Mantener Radial como la fuerza encargada de la compactación, pero evitar que la masa termine reducida a un único punto.

## Prueba 4 — Repulsión

### Configuración

```text
Radial ON
Radial Strength = -3
```

### Predicción

Las partículas deberían acelerarse alejándose del atractor.

### Observación
<img width="1378" height="967" alt="image" src="https://github.com/user-attachments/assets/e690fb5a-40bd-4741-aa7d-c0b4ef79cfaa" />


### Resultado

Si se alejaron del atractor y creaban figuras muy interesantes.

## Prueba 5 — Vórtice

### Configuración

```text
Radial = 1
Vortex = 3
Drag = 0.08
```

### Predicción

Las partículas deberían adquirir una componente tangencial y comenzar a circular alrededor del campo.

### Observación

Las primeras versiones del vórtice produjeron comportamientos no deseados: concentración hacia el centro y tendencia a formar estructuras planas.

Se identificó que una componente de cohesión radial añadida al vórtice estaba provocando parte de ese comportamiento.

### Modificación

Se eliminó la componente de cohesión adicional para separar:

```text
Radial → compactación
Vortex → circulación
```

### Resultado

La fuerza continúa en proceso de ajuste. El objetivo visual definitivo es producir **remolinos dentro de una masa tridimensional**, sin que la masa se convierta en un plano.
### Observación
<img width="1051" height="994" alt="image" src="https://github.com/user-attachments/assets/ac27cbb8-4254-47f7-b9af-3a5845abad87" />


## Prueba específica — Combinación central del instrumento

### Vortex + Beat

### Intención

Comprobar cómo responde la masa cuando una fuerza continua se combina con un evento temporal.

### Configuración conceptual

```text
Vortex
+
J / Beat
```

### Predicción

Vortex debería mantener una transformación/circulación continua mientras cada pulsación de `J` introduce una expansión breve.

```text
Vortex ─────────────────────
       J      J      J
       ↑      ↑      ↑
   perturbaciones temporales
```

### Criterio de éxito

La simulación no debe reiniciarse y las perturbaciones de `J` deben modificar momentáneamente el comportamiento sin reemplazar el estado producido por Vortex.

### Observación

<img width="1475" height="964" alt="image" src="https://github.com/user-attachments/assets/79b50748-6c83-4f23-860b-6e219be3665a" />


### Justificación

Esta combinación representa directamente el concepto del instrumento:

**fader continuo + evento musical = interpretación dinámica de la masa.**


# **05. Score visual de LesAlpx* ヾ(⌐■_■)ノ♪ 🪩

<img width="360" height="360" alt="image" src="https://github.com/user-attachments/assets/ce8ea3bd-2fb0-4684-ba66-8c2c770965e2" />

- **0- 0:43**
  
    Me lo imagino primero como una entrada suave con el modo vortex y dejarlo fluir por este momento como para la introducción de la canción.
    Además, para darle diferencia a la visual voy a presionar el espacio p

- **0:43-1:15**
  
  Esta parte se vuelve mas erratica y más crazyy con la introducción del nuevo beat.  Aca quiero hacer como un preambulo del drop raro que viene, lo voy a hacer hacieendo como una argolla q va a ir transformandose hasta explotar, la hare presionando varias veces la l,j y k.

- **1:15 - 1:54**
  
  Esta parte como que va siendo de silencio, me imagino al sistema como calmandose y comprimiendose. Esto lo voy a hacer moviendo los faders del recover y atract pero que todo sea muy progresivo.

- **1:54 - 2:44**

    Esta parte si me la imagino mas como un poco de lo mismo. Dejar al sistema fluir con el vortex y las fuerzas. Para que no se quede quieto la idea es ir presionando los beats y mover el fader de atracción contonuamente para que repela y atraiga.

- **2:44 - 3:50**
  
   Aca como que se va la percusión asi de hit hat y se quedan los bajos principalmente. Es como un poco mas grave pero resaltan unas voces, aca planeo hacer el sistema saltar con las voces presionando space y moviendo los faders de atract otra vez para seguir los faders del fondo.

- **3:50 - 4:25**
 
  Esta parte vuelve un poquito a lo mismo pero vuelven el resto de los instrumentos, aca lo voy a hacer mas erratico pero siguiendo con la idea de las voces.

- **4:25 - 4:43**

  Aca la canción ya se esta apagando, entonces me lo imagino como todo ralentizandose pero con ritmito todavia. Aca con el recover y el drag voy a hacer como un reinicio lento del sistema llevandolo como al inicio con vortex.


# **06. Bitácora de IA**ヾ(⌐■_■)ノ♪ 🪩

## Iteración 1 — Diseño del modo PERFORMANCE

### Prompt / intención

Se le explicó a la IA la idea de transformar la simulación base de fuerzas en un instrumento visual inspirado en una mesa de DJ. La intención era que el teclado funcionara como una consola invisible durante PERFORMANCE, sin mostrar controles en pantalla y sin reiniciar la simulación al interactuar.

Se implementó un sistema de teclas mantenidas mediante un conjunto `heldKeys`. Los parámetros se actualizan continuamente mientras la tecla permanece presionada y conservan el valor alcanzado cuando se suelta.

Mapping inicial:

* `A / Z` → fuerza radial.
* `D / C` → vórtice.
* `F / V` → drag.
* `G / B` → viento.
* `H / N` → recuperación.

### Modificación realizada

Se mantuvo la cámara y `OrbitControls` durante PERFORMANCE, pero se ocultaron los elementos visuales propios del LAB.

También se separaron los presets del LAB de los controles de PERFORMANCE para evitar que la interpretación reiniciara el sistema.

### Decisión propia

Se decidió que PERFORMANCE debía permanecer visualmente vacío. La interfaz de control no sería visible para el público; el instrumento estaría compuesto por el teclado, la simulación y las decisiones de la intérprete.

---

## Iteración 2 — Recuperación progresiva

### Problema

El sistema inicialmente solo permitía volver al estado inicial mediante `reset()`, produciendo un cambio brusco que no encajaba con la idea de una composición continua.

### Propuesta de IA

Crear una fuerza de recuperación utilizando la posición inicial de cada partícula como referencia:

[
F_{recover}=k(p_{inicial}-p)
]

La IA propuso guardar una `initialPositionBuffer` en GPU y utilizarla para generar una fuerza de retorno.

### Cambio aceptado

Se agregó:

```js
const initialPositionBuffer =
  instancedArray(count, 'vec3');
```

Cada partícula conserva su posición inicial y puede recibir posteriormente una fuerza que la acerque nuevamente a esa distribución.

### Decisión de diseño

La recuperación no se planteó como un teletransporte ni como un nuevo `reset`, sino como una fuerza integrada dentro de:

**fuerzas → integración → velocidad → posición**

Esto permite utilizarla durante la interpretación como un gesto continuo.

---

## Iteración 3 — Primer evento percusivo: BEAT

### Intención

Crear una tecla que funcionara como un golpe musical tipo **“PAM / POW”**, sin reemplazar las fuerzas que ya están activas.

### Propuesta de IA

Se propuso crear un envelope temporal:

```js
beatEnvelope
beatStrength
beatDecay
```

La pulsación de `J` establece el envelope en `1`, y este disminuye progresivamente con el tiempo.

### Cambio aceptado

La fuerza del BEAT se incorporó al acumulador de fuerzas:

```js
const beatForce = radialDirection
  .negate()
  .mul(params.beatStrength)
  .mul(params.beatEnabled);

force.addAssign(beatForce);
```

La tecla `J` funciona como un evento independiente de los faders.

### Decisión propia

Se decidió que el BEAT debía sentirse como una perturbación breve y perceptible sobre la masa, no como un cambio permanente del estado.

---

## Iteración 4 — Problema con el VORTEX

### Problema observado

El vórtice inicialmente hacía que las partículas se dirigieran demasiado hacia el centro o terminaran formando estructuras similares a un plano.

Durante las pruebas se identificó que parte del comportamiento provenía de utilizar `radialDirection` y añadir una componente de cohesión:

```js
const vortexCohesion = radialDirection
  .mul(...)
```

Esto hacía que el control de VORTEX también funcionara como una fuerza hacia el atractor.

### Cambio aceptado

Se eliminó la componente de cohesión para separar las funciones de las fuerzas.

Posteriormente se exploró una versión de vórtice tridimensional basada en la posición de cada partícula, con el objetivo de generar torsión dentro de la masa en lugar de hacer que toda la distribución orbite un único punto.

### Decisión propia

Se estableció como criterio visual que el VORTEX debe:

* producir remolinos;
* conservar la profundidad de la masa;
* deformar el volumen;
* evitar que la simulación se convierta en una lámina.

---

## Iteración 5 — Concepto de masa

### Observación

El sistema podía concentrarse demasiado en el centro cuando aumentaba la atracción.

### Decisión de diseño

Se estableció una condición visual para el instrumento:

> La simulación debe comportarse como una masa tridimensional que pueda compactarse, expandirse, girar, deformarse y recuperarse sin perder completamente su volumen.

Esta decisión pasó a ser un criterio para evaluar futuras modificaciones.

---

## Iteración 6 — Separación entre faders y eventos

### Estado actual

El instrumento comienza a utilizar dos tipos de interacción:

**Faders**

```text
A / Z → Radial
D / C → Vortex
F / V → Drag
G / B → Wind
H / N → Recover
```

**Eventos**

```text
J → Beat / Punch
```

### Próximas modificaciones

Se plantea ampliar la capa de eventos con diferentes comportamientos físicos:

```text
K → Clap
L → Voice
SPACE → Drop
```

Cada evento deberá utilizar una fuerza temporal diferente y poder combinarse con los faders sin reiniciar la simulación.
## Iteración 7 — Incorporación de eventos musicales

### Intención

Ampliar el instrumento con una segunda capa de interacción que no funcione como fader, sino como eventos momentáneos. La intención es que ciertas teclas permitan “tocar” la masa como si fueran golpes, claps o voces dentro de una composición musical.

Mientras los faders modifican progresivamente el estado del sistema, los eventos deben producir perturbaciones temporales que se mezclen con las fuerzas que ya están activas.

### Propuesta de IA

Se propuso utilizar distintos `envelopes` temporales para controlar la duración e intensidad de cada evento. Al presionar una tecla, el envelope comienza en `1` y disminuye progresivamente hasta desaparecer.

La estructura planteada fue:

```text
J      → BEAT / PUM
K      → CLAP
L      → VOICE
SPACE  → DROP
```

### Cambio aceptado

Se incorporaron variables independientes para cada evento:

```js
beatEnvelope
clapEnvelope
voiceEnvelope
dropEnvelope
```

Cada evento posee además parámetros propios de intensidad y decaimiento.

La fuerza de cada evento se añade al acumulador `force` de la simulación y posteriormente pasa por la misma integración que las demás fuerzas:

```text
evento
↓
fuerza temporal
↓
aceleración
↓
velocidad
↓
posición
```

De esta manera, los eventos no modifican directamente las posiciones de las partículas ni reinician la simulación.

### Comportamientos definidos

**J — BEAT / PUM**

Produce una fuerza radial breve hacia afuera. Se plantea como un golpe percusivo que expande momentáneamente la masa.

**K — CLAP**

Produce una fuerza radial hacia el centro durante un periodo corto, funcionando como una contracción rápida.

**L — VOICE**

Produce una perturbación tangencial más prolongada para generar una transformación sostenida de la masa.

**SPACE — DROP**

Produce una expansión radial de mayor intensidad, pensada como un acontecimiento de mayor impacto dentro de la interpretación.

### Problemas encontrados

Durante la implementación se detectó que los eventos podían interferir con el sistema de faders cuando se incluían dentro del mismo conjunto de teclas mantenidas.

Esto provocaba que eventos como `J` no fueran tratados como pulsaciones independientes.

### Corrección

Se separaron explícitamente los dos tipos de entrada:

```text
FADERS
→ teclas mantenidas
→ modifican parámetros progresivamente

EVENTOS
→ pulsaciones individuales
→ generan impulsos temporales
```

`J`, `K`, `L` y `SPACE` dejaron de pertenecer al conjunto de `performanceKeys` y pasaron a gestionarse como eventos independientes.

### Decisión propia

Se decidió que los eventos no deben sustituir ni reiniciar el estado del sistema. Deben funcionar como intervenciones sobre una masa que ya está en movimiento.

Esto permite combinaciones como:

```text
VORTEX ───────────────────
        J     J   J
        PUM   PUM PUM

RECOVER ────────────────
              K

SPACE
      DROP
```

La intención es que la interpretación pueda acumular capas de comportamiento de manera similar a una composición musical.

### Estado de la iteración

La arquitectura de eventos ya está definida y separada de los faders. El comportamiento visual de cada evento continúa en etapa de prueba y ajuste, especialmente en cuanto a intensidad, duración y percepción del impacto.

### Próximo paso

Probar y ajustar individualmente `J`, `K`, `L` y `SPACE` para que cada evento tenga una identidad visual claramente diferenciable antes de utilizarlos durante la interpretación de *LesAlpx*.

## Iteración 8 — Tratamiento visual del color
**Intención**

Evitar que la masa se percibiera como una colección de partículas con un único color.

**Propuesta Mia**

Relacionar el color con la velocidad de las partículas para que el cambio cromático surgiera de la dinámica.

**Cambio aceptado**

El color comenzó a interpolarse en función de la velocidad:

movimiento lento
→ colores fríos

movimiento rápido
→ colores cálidos/intensos

También se exploró ampliar la paleta para pasar por varios tonos en vez de utilizar solamente dos.

**Decisión propia**

El color no debía ser controlado directamente por cada tecla. Se decidió que debía seguir siendo una consecuencia del movimiento para conservar la relación:

fuerza → movimiento → transformación visual.

## Iteración 9 — Exploración del fondo
**Intención**

Quitar la sensación de “demo técnica” producida por el cubo de partículas.

**Propuesta de IA**

Se exploró agregar estrellas, niebla y un glow de fondo.

**Resultado**

La propuesta de fondo espacial no resultó convincente porque añadía elementos decorativos que no estaban relacionados directamente con la dinámica del sistema.

**Decisión de rechazo**

Se descartaron las estrellas y el fondo decorativo.

Se decidió que el espacio debía mantenerse oscuro y que la propia masa debía ser el elemento principal de la composición.

## Iteración 10 — Problema de concentración de la masa
**Problema observado**

Cuando RECOVER estaba en cero, la masa podía terminar demasiado acumulada. Esto evidenció que la recuperación estaba cumpliendo también, indirectamente, una función de mantener la distribución.

**Análisis**

Se identificó que había que separar dos responsabilidades:

- RECOVER
→ volver a la forma inicial

- VOLUME / COHESION
→ impedir que la masa colapse

**Nueva propuesta**

Introducir una fuerza de preservación de volumen que solamente actúe cuando las partículas están demasiado cerca del núcleo.

**Estado**

Esta modificación todavía se encuentra en exploración y debe probarse antes de incorporarla definitivamente al instrumento.

**Decisión propia**

Se estableció que RECOVER = 0 no debe significar que la masa pierda su identidad volumétrica. La masa debe seguir siendo estable por sus propias reglas y RECOVER debe funcionar solamente como un gesto adicional de recomposición. 


## Iteración 11 — Rediseño visual de la interfaz

### Intención

Dar al modo LAB una identidad visual más cercana a un instrumento audiovisual y menos parecida a un panel técnico. La interfaz debía acompañar la metáfora de la mesa de DJ sin interferir con la visualización de la masa de partículas.

### Problema observado

La interfaz anterior funcionaba, pero visualmente se percibía como un panel de parámetros convencional. Esto no representaba la intención del proyecto de crear un instrumento experimental para una interpretación audiovisual.

### Decisión propia

Se rediseñó `styles.css` para modificar:

* fondo y panel;
* tipografía;
* jerarquía de títulos;
* apariencia de sliders;
* botones;
* checkboxes;
* HUD;
* estados hover y active.

El panel pasó a utilizar una estética de vidrio oscuro con transparencias y pequeños acentos luminosos.

Se decidió mantener esta estética únicamente en el modo LAB. Durante PERFORMANCE, todos estos elementos deben desaparecer para conservar la idea de una interfaz invisible y permitir que la audiencia observe solamente la masa de partículas.

La interfaz, por tanto, funciona como herramienta de exploración y no como parte principal de la presentación final.

### Estado

La estructura funcional del instrumento no fue modificada en esta iteración. El cambio se concentró exclusivamente en la presentación visual de la interfaz.

La arquitectura física continúa siendo:

**estado → fuerzas → integración → render**

y el teclado continúa siendo el principal medio de interpretación durante PERFORMANCE.

<img width="1864" height="865" alt="image" src="https://github.com/user-attachments/assets/a75a64bd-e5ba-445d-8846-d14f7ea6153c" />

# **7. Autoevaluación**ヾ(⌐■_■)ノ♪ 🪩
