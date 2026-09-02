# Unidad 4 👽✮⋆˙ ☠︎︎ ★☠︎ ✮⋆˙

## Actividad 02: Encargo de diseño - RAVEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEE👽✮⋆˙ ☠︎︎ ★☠︎ ✮⋆˙

Me acordé de esta súper actividad que hice en Sistemas Interactivos 1 que era un rave de gatos, y quise llevar esa vibra a otro nivel usando el modelo de Kuramoto.





Investigando, me topé con esta frase que me voló la cabeza:

> *"Las artes, como la literatura y la música, ayudan a sincronizarnos entre personas. Cuando los dos estamos escuchando la misma canción... la actividad de mis neuronas se sincroniza con la de tus neuronas y lo mismo ocurre con la actividad cardíaca."* — Jesús Ramírez Bermúdez (Neuropsiquiatra).

Ahí estuvo mi concepto: **Un rave donde la multitud no baila al ritmo de la música, sino que la música nace de la sincronización de la multitud.**

### ¿Qué hace Kuramoto aquí que no haría un simple temporizador?

Esta es la pregunta central del proyecto. Si yo usara un reloj global (BPM), todos los agentes simplemente saltarían al mismo tiempo porque un código se los dicta. Sería un secuenciador aburrido y predecible.

En mi experiencia, **no hay un beat externo dictando cuándo saltar**. Cada raver (agente) tiene su propia frecuencia natural ($\omega$) y su propia fase ($\theta$). El modelo de Kuramoto actúa aquí a través de la variable de acoplamiento ($K$). Cuando subo el valor de $K$, las fases de los ravers empiezan a atraerse entre sí de forma orgánica. Pasan del caos absoluto a encontrar un ritmo común, y es esa "negociación" matemática en tiempo real la que genera la música. Es autoorganización pura, no un loop pregrabado.

### Las Personalidades Audiovisuales (La Pista de Baile)

Cumpliendo con los requisitos, fui más allá de los 8 agentes y metí **96 ravers** en una grilla uniforme (bajé de 144 porque el compu iba a explotar y ChatGPT me dañó el código varias veces intentando optimizarlo xd).

No se diferencian solo por colorcitos, sino por su **comportamiento y movimiento**:

* **Movimiento:** Tienen oscilaciones suaves tipo "gelatinita", deformaciones de escala (stretch/compress) y rotaciones que llamo estilo "charrito".
* **Impacto visual:** Su única acción corporal fuerte es saltar verticalmente según su fase de Kuramoto. Cuando aterrizan, su `emissiveIntensity` (brillo) explota, iluminando la pista.
* **La Cámara:** Se mueve medio loco al ritmo del BPM para dar esa sensación inmersiva de club, sumado a las ondas del piso, láseres y luces de techo. (Quité unos flashes de pantalla blanca que tenía antes porque mareaban mucho).

### El Audio: El Parámetro de Orden ($R$) como DJ

¡La música NO es pre-grabada! Es síntesis de audio pura usando Web Audio. El parámetro de orden ($R$), que mide qué tan sincronizados están todos (0 = caos, 1 = perfección), es el que "dirige" las capas de la música.

* **Estado de DESORDEN ($R < 0.25$):** La fuerza de acoplamiento ($K$) es baja. Cada persona salta por su lado. Musicalmente, solo suenan el Kick y un Rumble grave. Como suenan al mismo tiempo y los hats están casi en silencio, al oído se percibe súper vacío, como si solo sonaran "dos cositas".
* **Estado PARCIAL ($0.25 < R < 0.65$):** Se empiezan a ver grupos aterrizando juntos. Empiezan a entrar claps suaves y algunos hats.
* **Estado ESTABLE ($R > 0.65$):** $K$ es alto. La gran mayoría de la pista salta y aterriza al mismo tiempo. Al subir el parámetro $R$, se destraban en cascada todas las capas de audio: open hats en los contratiempos, stabs cortantes, una línea de bajo Acid (tipo 303) loquísima en semicorcheas, y un ruido de subida (swoosh/riser). El volumen y la intensidad crecen literalmente porque la gente está sincronizada.

### Experiencia Performativa: ¿Cómo se toca este instrumento?

La interfaz quedó fija y clara para poder "tocar" el rave en vivo, provocando transiciones entre desorden, organización y estabilidad.

**Controles de Kuramoto:**

* `[ ]` **(Coupling - $K$):** Obligatorio para el reto. Acerca o aleja las fases de los ravers. Es el slider que crea la tensión musical.
* `- =` **(Omega spread):** Controla qué tan dispersas son las frecuencias naturales de la gente.

**Mecanismos de Perturbación (Rompiendo la estabilidad):**

* **Barra Espaciadora (Perturbación Global):** Altera el colectivo entero, rompiendo un estado estable para ver cómo el sistema vuelve a encontrar el ritmo (o se queda en el caos).
* **Click en un raver (Perturbación Individual):** Modifico la fase de un solo individuo para ver cómo su comportamiento desfasado afecta a sus vecinos.

**Visualización:**

* `1 y 2`: Cambian la presentación visual de la multitud (multitud orgánica vs. agrupada por personalidad), pero sin alterar el comportamiento de Kuramoto subyacente. La UI siempre me marca el HUD de $R$ y el estado exacto (DESORDEN / PARCIAL / ESTABLE).

Al final, logré un loop perfecto: Kuramoto calcula las fases $\rightarrow$ saca el promedio $R$ $\rightarrow$ $R$ dispara los sintes de audio $\rightarrow$ las luces reaccionan $\rightarrow$ el performer interviene. Literalmente un rave matemático.

# Errores, crisis y experimentación 👽✮⋆˙ ☠︎︎ ★☠︎ ✮⋆˙

En el proceso de armar este rave pasé por varios dolores de cabeza y experimentos que terminaron dándole la personalidad al proyecto. Aquí documenté los más importantes:

Al principio quería que la pista estuviera a reventar con 144 ravers. El problema es que el compu iba a explotar. Intenté pedirle ayuda a ChatGPT para optimizar el código y organizar los grupos caóticos, pero cada vez me dañaba más el trabajo xd. Al final, tomé la decisión de reducir la población a 96 agentes. Además, cambié la distribución caótica por una grilla uniforme (con pequeñas variaciones). Esto fue un acierto enorme porque en una grilla se nota muchísimo mejor cuando la onda de sincronización de Kuramoto empieza a unirlos.


No quería que los agentes fueran bloques rígidos aburridos. Para que se sintiera como un rave real, me puse a experimentar con la trigonometría del salto. Logré un movimiento que llamo "gelatinita": una oscilación suave donde el modelo sufre una deformación de escala. Básicamente, se estira (`stretch`) cuando va para arriba y se comprime (`compress`) cuando cae al piso. También le sumé rotaciones en los ejes que bauticé como movimiento "charrito" para que se vieran más orgánicos. Para rematar el efecto visual, programé que justo en el impacto del aterrizaje, su material explote con un `emissiveIntensity` dinámico.


En versiones anteriores tenía un sistema de flashes en la pantalla (whiteFlash, flashPulse, discoFlash y blackout). Era demasiado, mareaba horrible y no dejaba ver la sincronización. Eliminé todo eso. Para mantener la energía del club sin causar epilepsia, decidí animar la cámara directamente al BPM de la música. Ahora la cámara se mueve bien loco; tiene un efecto de "pum pum" (un pulso vertical y de profundidad) y un balanceo horizontal que te hace sentir como si estuvieras metido saltando en medio de la multitud.


Al principio me frustraba que en el estado de DESORDEN la simulación sonara súper vacía, como si solo sonaran "dos cositas". Revisando mi planificador de audio (`updateMusic`), entendí perfectamente el porqué: con el parámetro de orden $R$ bajo ($< 0.25$), los únicos sonidos habilitados sin condición son el Kick y el Rumble. Como ambos son golpes graves y suenan exactamente en el mismo instante (cada beat), el cerebro los funde en un solo gran "boom".

Pero la magia real y mi mayor logro en experimentación ocurre al llegar al estado ESTABLE ($R > 0.65$). Programé el sistema para que destrabe instrumentos en cascada. De repente entran los Hats en todas las corcheas, los Open Hats en los contratiempos, acordes cortantes (Stabs) en el último beat, y una línea de bajo Acid tipo 303 loquísima. Además, como casi todas las funciones de sonido tienen un multiplicador del tipo `+ R * algo`, entre más sincronizada está la gente, la música no solo tiene más capas, sino que literalmente suena con más fuerza.

<img width="1841" height="880" alt="image" src="https://github.com/user-attachments/assets/70398838-43c9-40cd-96b6-276111bfff48" />
<img width="1871" height="895" alt="image" src="https://github.com/user-attachments/assets/ddf5b1d8-4b06-41d2-a4e9-ada4294cbd27" />
<img width="1841" height="895" alt="image" src="https://github.com/user-attachments/assets/3e8a2078-3390-4139-8a01-e0f13a24bdd5" />
<img width="1914" height="945" alt="image" src="https://github.com/user-attachments/assets/8057ad6f-02a3-4633-b39e-ad98665a5a44" />
<img width="1760" height="818" alt="image" src="https://github.com/user-attachments/assets/afeee9ee-3f02-41e6-82d6-05475f503d8a" />

- Todos están distribuidos como una multitud de discoteca, compacta e irregular.
- No caminan, no giran, no se desplazan, no hacen coreografías.
- Su única acción corporal es saltar verticalmente.
- La fase de Kuramoto determina cuándo saltan.
- Cuando están más sincronizados, se ve un salto colectivo.
- Cuando están desordenados, los saltos están repartidos.
- Se mantienen las ondas del piso, láseres, luces de techo, luces de club y bloom.
- Se elimina ÚNICAMENTE la pantalla negra/flash.
- Se conserva la lógica del audio anterior dentro de main.js.
- K y Ω siguen siendo controlables.
- La UI queda siempre visible y los sliders están más separados.
- Los estados ahora se llaman DESORDEN / PARCIAL / ESTABLE, que corresponde directamente al reto.
- 1 y 2 no cambian el movimiento de los agentes: solo cambian la presentación visual.
- Click individual perturba un agente.
- SPACE perturba el colectivo.


- DESORDEN → cada persona salta por su lado.
- PARCIAL → aparecen grupos de saltos coincidentes.
- ESTABLE → gran parte de la pista salta junta.

<img width="1854" height="839" alt="image" src="https://github.com/user-attachments/assets/faae8f6b-c354-4603-9c77-6cbed1a4d5d9" />


chatgpete cada vez ,me daño mas el trabajo xd 


<img width="1854" height="839" alt="image" src="https://github.com/user-attachments/assets/e8448e73-bc69-4fb9-9447-5c90e9200a21" />


### Los agentes son quienes generan la música en tiempo real.

Funciona así:

- **Modelo Kuramoto:** Los 96 agentes tienen fases que se sincronizan/desincronización según el coupling
- **Order Parameter (R):** Se calcula cuán sincronizados están todos (0 = caos, 1 = perfectamente sincronizados)
- **Music Scheduler**: El valor de R determina cuándo y qué sonidos se tocan

<img width="849" height="700" alt="image" src="https://github.com/user-attachments/assets/97c69501-77da-41f1-bb40-01338fdffc72" />

la camara se mueve bien loco 

<img width="790" height="626" alt="image" src="https://github.com/user-attachments/assets/d4067270-9b9c-47ed-b3d1-3e2129d1a873" />

# Cómo suena cada elemento?

Cada sonido (playKick, playRumble, playHat, etc.) es un instrumento sintetizado con Web Audio, y el "director de orquesta" es la función updateMusic(R), que se llama todos los frames y dispara cosas en tres grillas de tiempo: beat (negra), eighth (corchea) y sixteenth (semicorchea), todas calculadas a partir del BPM (138).

R es el parámetro de orden de Kuramoto — mide qué tan sincronizados están los 96 ravers (0 = todos desfasados / caos, 1 = todos en fase / sincro perfecta). Ese mismo R es el que decide cuántas capas de sonido están activas, no solo el volumen.

## Por qué en DESORDEN suena "como dos cosas"?

Con R bajo (< 0.25), estos son los únicos sonidos que están habilitados sin condición:

Elemento	Condición	¿Suena en DESORDEN?
- Kick	siempre, cada beat	✅ sí
- Rumble	siempre, cada beat	✅ sí
- Clap	siempre, en los beats 2 y 4	✅ sí (pero suave)
- Hat cerrado (en corcheas pares)	siempre	✅ sí (pero volumen bajo: 0.35 + R*0.50)
- Hat cerrado (en corcheas impares)	necesita R > 0.35	❌ no
- Open hat	necesita R > 0.30	❌ no
- Stab	necesita R > 0.52	❌ no
- Acid (corcheas)	necesita R > 0.22	❌ casi nunca (el umbral está pegado al límite de DESORDEN)
- Acid (semicorcheas)	necesita R > 0.60	❌ no
- Build noise (swoosh)	necesita R > 0.72	❌ no

Kick y Rumble suenan exactamente en el mismo instante, cada beat, y ambos son sonidos graves de golpe (el kick es un seno que cae de 165→38 Hz, el rumble es un sawtooth filtrado en 47 Hz) — se funden perceptualmente en un solo "boom". Sumale el hat, que a bajo R suena muy flojito (0.35 de strength base, casi el mínimo). Por eso tu oído capta básicamente "boom" + "tss" apenas perceptible = "dos cositas".

## Por qué en ESTABLE suena "más cositas"?

Con R > 0.65 se van destrabando, en cascada, todas las capas que antes estaban mudas:

- Hat en todas las corcheas (no solo las pares)
- Open hat en los contratiempos
- Stab (acorde cortante) en el último beat de cada compás
- Acid (línea de bajo tipo 303) sonando con alta probabilidad en cada corchea
- Encima, acid extra en semicorcheas — corridas rápidas de notas
- Y por encima de R > 0.72, un swoosh de ruido (playBuildNoise) cada 32 semicorcheas, como un "riser"

Todo eso se va sumando en capas simultáneas, y como además suben en volumen (todas las funciones tienen + R * algo en su fuerza), no solo hay más elementos sino que suenan más fuerte y más presentes.


<img width="1460" height="808" alt="image" src="https://github.com/user-attachments/assets/93ef7ad6-3f7e-4162-bab3-de8bc0b4671e" />}

https://github.com/user-attachments/assets/8c86bac9-5bc3-4208-8a1e-6aeb61932dd8






