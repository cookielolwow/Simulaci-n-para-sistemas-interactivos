
# Unidad 2: Movimiento 🍌

## Actividad 02: motion 10 🍌

x+1=xi+v*deltaT   -> The nature of code : deltaT = 1
                  -> The particle life: framerate
                  <img width="879" height="456" alt="image" src="https://github.com/user-attachments/assets/728ed612-f741-4122-91d1-b5ebc0b03d0f" />



# ACTIVIDAD 05: RETO DE DISEÑOOOOOOOO 🍌🎉🎉🎉🎉🎉🎉🎉🎉🎉🎉

Estoy super motivada con este reto de diseño porque el concepto que elegí es de mis temas favoritos ever.
LLegué a este concepto cuando me desperté un dia random y literalmente lo primero que se me vino a la cabeza fue que los **MINIONS** funcionan como un sistema de particulas y todo en mi mente fue haciendo click.


<p style="text-align: center"> <img src="https://github.com/user-attachments/assets/9e67a366-cc4c-4e73-9892-36d058dba5d8"></p>




**QUIERO EXPLORAR LA CONTRADICCIÓN DE LOS MINIONS Y SUS LIDERES.**



Me parece una contradicción interesante de explorar porque los minions siempre andan junticos y como grupo siempre estan siguiendo su único propósito biológico que es encontrar y ponerse al servicio del amo más grande, malvado y despreciable de cada época.
Y me parece bastante ironico que ellos siempre buscando cuidar y dar sus servicios a su lider terminan lastimandolo o incluso asesinandolo entonces me parece una contradicción bastante curiosa.

Entonces esto me llevo a la conclusión: **Quiero explorar la tensión entre la devoció de los minions y la destrucción involuntaria que ellos tienen con sus lideres por la torpeza que tienen.**

Espero que esto se manifieste como grandes enjambres muy organizados que migran hipnóticamente hacia los lideres. Sin embargo, al momento de alcanzar su meta, la cercanía extrema romperá el equilibrio del sistema: el exceso de "amor" creara la desaparición del líder obligando a los minions a reorganizarse y buscar  un nuevo propósito.


* Mi intencion es que las personas al ver el proyecto es que vean a los minions en el sistema. Lograr retratar su comportamiento siguiendo las reglas del mundo.

Pero siento que en el sistema de particulas tienen que haber mas categorias que simplemente los minions y villanos. 
Recorriendo como toda la historia de los minions pues encontramos que en algun punto de la historia existieron minions morados q practicamente estaban al servicio del macho peroo atacaban a los minions originales. Quiero explorar este comportamiento por medio de aleatoriedad.

Quiero que exista otra entidad en el sistema que sean estos minions morados. Se van a crear a partir de que una particula de un villano "El macho" tenga la probabilidad de infectarlos y volverlos morados. Y que estas particulas moradas busquen ahora a las amarillas que representan a los minions y las ataquen asi sea eliminandolas o infectandolas.

Pero para que el sistema no se quede totalmente morado despues de un tiempo y haya una tendencia la idea es que hayan unas particulas de mermelada en el espacio que les de la posibilidad de desinfectarse y volver a la normalidad. Pues lore accurate los minions odian esta mermelada Y pues aca se puede crear una regla de repulsión de la mermelada a los minions.

Además de estos conceptos quiero darle la vida en el sistema a villanos representativos de la saga usando como lo que representaban para los minions y con esto definiendo el comportamiento que van a tener.

- Scarlet: Habian 3 minions muy particulares que lograron estar al servicio de ella entonces para representar esto quiero crear a bob, kevin y stuart con una atracción especial a ella y pues una mediana atracción a los otros villanos pero tirando mas a una indiferencia. Con ellos quiero hacer perceptible la traición de scarlet a los minions por medio de la excepción y que genere una probabilidad de repulsión a ellos.

- Pie grande: Con esta particula quiero hacer perceptible que los minions son bien mortales y que pueden asesinar a sus lideres por accidente. Quiero que esta particula atraiga a los minions y tenga la probabilidad de ser asesinada por ellos.
  
- Gru: El es el gran lider de los minions y logro hacerse parte de ellos. Con esta particula quiero hacer perceptible que los minions son leales a una persona de forma indefinida y que pueden llegar a cuidarlo sin hacerle daño.


  Para que el sistema conserve una identidad tiene que estar muy marcado que los minions siempre andan juntos y que sienten atracción a las particulas villanas.


  

  


## Diseño del sistema


### Tipos de partículas.

* **MINIONS:** Entre ellos se atraen para formar sus tribus. Tendran la necesidad constante de buscar a cualquier particula tipo ""villano". Son el motor del sistema.

* **Bob, Kevin Y Stuart:** Comparten el comportamiento de los minions normales pero su prioridad sera Scarlet. Podran estar cerca de los demás minions pero apenas ella aparezca, romperan la formación para ir a buscarla a ella.
* **MINIONS MORADOS**: No existen al inicio del sistema. Tienen más velocidad y un movimiento mas alocado. Sentiran atracción asimetrica por los minions. Ignoran a los villanos para consumir a los minions.

* **Scarlet:** Representa la traición. Su estado interno cuenta como con un temporizador que hara que ella pase de ser un atractor a un reepulsor de alta intensidad.

* **Pie grande:** El representa la letalidad de los villanos. Ejerce una atracción normal, invita a los minions a rodearlo. Su peculiaridad es que si hay muchos minions cerca de el pie grande se elimina del sistema emulando un accidente donde el grupo lo aplasta.

* **El macho:** El macho es un lider normal, pero actua como un peligro para los minions. Cualquier minion amarillo que entre en su radio no lo va a destruir, si no que tiene la probabilidad de ser corrompido y transformado en un minion morado.

* **Mermelada:** Son particulas de movimiento casi nulo. Los minions amarillos sienten repulsión y trataran de bordearlas. Sin embargo si un minion morado ( q no siente asco por ellas) atraviesa la mermelada, pierde su mutación y se vuelve un minion amarillo.

* **Gru:** Su movimiento sera pesado y seguro. Genera un campo de atraciión a los minions bastante alto y seguro para los minions. 

### Cantidad de partículas de cada tipo.

* Para iniciar la prueba seleccioné 300 Minions Genéricos, 3 Élite, 1 de cada Villano, 0 Morados iniciales y 5 áreas de Mermelada porque quiero hacer perceptible el proposito de los minions en encontrar su lider adecuado.

  
### Matriz de atracción, repulsión o indiferencia.

<img width="1477" height="843" alt="image" src="https://github.com/user-attachments/assets/a0548c52-782f-4e75-8b51-d6ef07ef6334" />


### Intensidad y alcance de cada relación.



| Siente \ Hacia | Amarillos | Élite | Morados | Gru | Scarlet | Pie Grande | El Macho | Mermelada |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Amarillos** | `+0.3` / `100` | `+0.3` / `100` | `-0.9` / `150` | `+0.8` / `800` | `+0.3` / `400` | `+0.6` / `400` | `+0.6` / `400` | `-1.0` / `80` |
| **Élite** | `+0.3` / `100` | `+0.6` / `150` | `-0.9` / `150` | `+0.8` / `800` | `+1.0` / `800` | `+0.6` / `400` | `+0.6` / `400` | `-1.0` / `80` |
| **Morados** | `+0.9` / `300` | `+0.9` / `300` | `+0.4` / `150` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `+0.01` / `800` |
| **Gru** | `+0.1` / `800` | `+0.1` / `800` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **Scarlet (1)**| `0.5` / `0` | `0.5` / `200` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **Pie Grande** | `+0.1` / `400` | `+0.1` / `400` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **El Macho** | `+0.2` / `500` | `+0.2` / `500` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **Mermelada** | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |

*(1) Scarlet alterna estocásticamente a un estado de traición donde su fuerza hacia Élite y Amarillos pasa a ser de `-1.5` con un radio de `250`.*							
### Distancias de interacción.

* **Infección por El Macho:** Colisión a < 15px. Probabilidad: 30% de convertir Amarillo a Morado.

* **Infección por Morados:** Colisión a < 10px. Probabilidad: 100% de convertir Amarillo/Élite a Morado.

* **Curación por Mermelada:** Colisión a < 25px. Probabilidad: 100% de convertir Morado a Amarillo.

* **Muerte de Pie Grande:** Si hay > 15 partículas Amarillas a < 30px de distancia simultáneamente, la partícula de Pie Grande se elimina del sistema.

Seleccioné distancias eventos dependientes de la colisión física porque quiero hacer perceptible la ironía de que alcanzar su meta biológica y acercarse a lo que aman es exactamente lo que desencadena su propia mutación o la destrucción accidental de su líder. Espero que produzca momentos de clímax visual donde agrupaciones estables colapsan al darse el contacto.




### Fricción y velocidad máxima.

* **Morados:** Velocidad Máxima alta (5.0), Fricción baja (0.98) — Movimiento errático y resbaladizo.

* **Amarillos/Élite:** Velocidad Máxima media (3.0), Fricción media (0.90) — Movimiento ágil y controlable.

* **Villanos:** Velocidad Máxima baja (1.0), Fricción alta (0.80) — Movimiento pesado y constante.

  
### Distribución inicial.
* **Minions (Amarillos y Élite):** Inician fuertemente junticos en un radio muy pequeñito en el centro exacto del lienzo.

* **Líderes y Mermelada:** Se ubican de forma dispersa y aleatoria en los bordes del lienzo.

* **Morados:** No hay minions morados inicialmente.
* 
### Parámetros constantes y variables.

* **Constantes:** La atracción incondicional hacia Gru y las fuerzas de repulsión de la Mermelada operan siempre bajo las mismas reglas y no cambian en el tiempo.

* **Variables**: El estado de Scarlet. Cuenta con un temporizador interno que, al cumplirse, cambia temporalmente su matriz de atracción (+1.0) a un estallido de repulsión extrema (-1.5). También la infección de los minions y la creación de los morados es una variable.

Seleccioné la lealtad hacia Gru como un parámetro constante y la relación con Scarlet como una variable  en el tiempo porque quiero hacer perceptible la diferencia entre el amo que le da estabilidad a los minions y un líder traicionero o volátil. Espero que se vea el rechazo rechazo de scarlett, forzando a los minions de Scarlet a salir disparados y buscar otros líderes temporalmente.


### Apariencia e interacción, cuando existan.

* **Círculos simples**. Los Amarillos, Élite y Morados tienen un radio pequeño (ej. 3px a 5px). Los villanos y las zonas de mermelada tienen un radio mucho mayor (ej. 15px a 30px).

  Para la interacción me parecio bien darle la oportunidad al usuario de curar a los minions poniendo zonas de mermelada ya que no quieor que se cambie el sentido colectivo de los minions frente a la individualidad de ellos, evitando que el control total del usuario arruinen el ecosistema.


## Registro de pruebas con ajustes, hallazgos y descartes.

Genuinamente paso de todo para llegar al resultado, me demore como 4 horas intentando optimizar ese codigo pero casi muero 30403848239 veces:)

Las primeras versiones que hice eran primero para crear el sistema de particulas y hacer que la matriz fuera funcionando.

El codigo simplemente no respondia como uno esperaba del particle of life que vimos en clase.

Hice lo posible para no tener que mover el concepto original que tenia porque genuinamente me gustaba bastante y sentia que podia lograr algo chevre usandolo.

En el proceso fui descubriendo y entendiendo como lo sparametros que iba trayendo el particle of life que anets no habia captado, por ejemplo el radio de cada particula para que unas no estuvieran encimas de otras y se lograran diferenciar.

La peor parte de esto fue literalmente la optimización, no la logre como lo esperaba y me tocó dejarla sin optimizar. 

<img width="629" height="850" alt="Captura de pantalla 2026-08-04 183329" src="https://github.com/user-attachments/assets/83d2da57-b5f6-47ea-b34f-c9cb6cf11e03" />
<img width="478" height="770" alt="Captura de pantalla 2026-08-04 175110" src="https://github.com/user-attachments/assets/6f47d246-fcb4-42c1-9053-e5d3b9b3916d" />
<img width="821" height="843" alt="Captura de pantalla 2026-08-04 195122" src="https://github.com/user-attachments/assets/fc6b2b34-c672-49e7-aa49-03ab42af9316" />


<img width="954" height="890" alt="Captura de pantalla 2026-08-04 174110" src="https://github.com/user-attachments/assets/e1756087-a2d3-4750-b444-965abcb328a8" />

<img width="535" height="929" alt="Captura de pantalla 2026-08-04 212921" src="https://github.com/user-attachments/assets/b8c0c158-2b5e-4656-943a-aaec5aac127a" />



Lo que mas mejodio la verdad fue el uso de la inteligencia artificial y mis nulas habilidades de programación. Siento que si genuinamente supiera del tema hubiera logrado algo mas interesante. 
Sientoq ue el tema de la inteligencia artificial fue como sabotaje , simplemente nunca pude lograr un resultado chevre porque se me acababan los tokens,los chats, etc. Y tener que estar variando entre 28393 ias para lograr algo me daño mucho el flujo de trabajo y no logre como tener una homogeneanidad hasta full adherirme a chatgpt. Por mas q lo intenté no logré optimizar las particulas ni darles vida adecuadamente como el particle of life. 

De optimización solo logre añadir una cuadricula que hiciera que fuera mas facil buscarse entre ellos.

Decidi ponerles el trail y los caminitos para asi al menos lograr un poquito de dibujo en el proceso ya que como no pude optimizar a poder usar muchas particulas no pude lograr el efecto que estaba planeado del ejercicio.

Al final para que los minions no se aglomeraran de una en el centro decidi que empezaran repartidos por el canva para que asi crearan sus propias tribus. 


<img width="346" height="551" alt="image" src="https://github.com/user-attachments/assets/57f8b070-586e-43cc-961a-ed2cb8a9b246" />


<img width="460" height="411" alt="image" src="https://github.com/user-attachments/assets/424aec64-f7f5-44ef-9708-a1aac8477514" />



<img width="845" height="584" alt="image" src="https://github.com/user-attachments/assets/e01513fb-4c74-439a-8666-bc18b765eaf1" />


* Mejore el trail para que no se viera tan saturado y fluyera mejor.

## RESULTADOOOOS
**CODIGO:** https://editor.p5js.org/cookielolwow/sketches/hYZTU8Baj

| Tipo                     | Cantidad | Función                                                                | Justificación de los parámetros
| ------------------------ | -------- | ---------------------------------------------------------------------- |---------------------------------------
| Minions                  | 300     | Población principal. Se agrupan y siguen fuerzas de otras especies.    |Los minions amarillos son el grupo mas numeroso , por lo que para crear grupos y tribus se atrae entre ellos. Además como su proposito es buscar un lider siente gran atracción hacia ellos. Y repudian totalmente la mermelada.
| Elite (Bob/Kevin/Stuart) | 100      | Variante de minions con identidad visual propia.                       |La Élite mantiene una lógica similar a la de los minions, pero con una atracción mucho mayor hacia Scarlet, pues ambos representan figuras de autoridad y liderazgo dentro del universo. También son atraídos por Gru, ya que siguen a quien consideran el villano principal
| Morados                  | Variable | Especie invasora que puede transformar minions.                        |Los Morados fueron configurados para perseguir principalmente a los minions y a la Élite. En la película estos personajes son minions alterados que buscan atacar a los demás,
| Gru                      | 1        | Figura central con interacción limitada.                               |Gru posee un radio de influencia muy amplio y una atracción baja. Esto hace que actúe como un punto de reunión que organiza el sistema sin absorber inmediatamente a todas las partículas
| Scarlet                  | 5       | Agentes con comportamiento especial de rechazo/traición.               |Scarlet tiene una influencia más fuerte sobre la Élite (bob,stuart y kevin). Ella representa un lider volatil, por lo cual genera rechazo y atracción a los minions representando una traición.
| Pie Grande               | 20       | Población con condición de eliminación por exceso de minions cercanos. |Atrae a los minions a distancias medias. Su papel es representar la letalidad de los minions. Cuando tenga cirta de cantidad de minions alrededor va a desaparecer.
| El Macho                 | 3        | Infecta y transforma partículas amarillas.                             |Su presencia es más notoria y logra atraer minions desde una mayor distancia que pie grande. Su función es competir parcialmente con Gru por la atención de los minions, generando desplazamientos y reorganizaciones constantes dentro de la simulación, pero sin llegar a convertirse en el centro dominante del sistema.
| Mermelada                | 5        | Cura partículas moradas devolviéndolas al estado amarillo.             |Su función consiste únicamente en ser rechazado por los minions y la Élite, provocando que estos huyan de él y generando zonas de conflicto dentro de la simulación. Pero cura a los infectados morados, esstos sienten un poquito de atracción a ellas para que puedan curarse si poerden el rumbo.

Los parametros que decidí para cada particula representan el comportamiento de cada personaje dentro de la pelicula.

<img width="1477" height="843" alt="image" src="https://github.com/user-attachments/assets/a0548c52-782f-4e75-8b51-d6ef07ef6334" />

| Siente \ Hacia | Amarillos | Élite | Morados | Gru | Scarlet | Pie Grande | El Macho | Mermelada |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Amarillos** | `+0.3` / `100` | `+0.3` / `100` | `-0.9` / `150` | `+0.8` / `800` | `+0.3` / `400` | `+0.6` / `400` | `+0.6` / `400` | `-1.0` / `80` |
| **Élite** | `+0.3` / `100` | `+0.6` / `150` | `-0.9` / `150` | `+0.8` / `800` | `+1.0` / `800` | `+0.6` / `400` | `+0.6` / `400` | `-1.0` / `80` |
| **Morados** | `+0.9` / `300` | `+0.9` / `300` | `+0.4` / `150` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `+0.01` / `800` |
| **Gru** | `+0.1` / `800` | `+0.1` / `800` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **Scarlet (1)**| `0.5` / `0` | `0.5` / `200` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **Pie Grande** | `+0.1` / `400` | `+0.1` / `400` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **El Macho** | `+0.2` / `500` | `+0.2` / `500` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **Mermelada** | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |




  
<img width="302" height="197" alt="image" src="https://github.com/user-attachments/assets/427dcdbb-c370-4639-9918-0e9064bec59d" />
<img width="152" height="116" alt="image" src="https://github.com/user-attachments/assets/85052a9f-f154-413d-ad4d-99741134f1de" />
<img width="243" height="152" alt="image" src="https://github.com/user-attachments/assets/1a3f104d-16b9-4b09-b04a-ece06c7f4ff4" />


### Variaciones del sistema

**Invariantes:** reglas de interacción entre especies, matriz de fuerzas y radios, cantidad de tipos de partículas, comportamiento base de cada personaje y lógica de actualización del sistema.

**Variables:** posición inicial de las partículas, cantidad de individuos por especie, probabilidad de infección, estado inicial de Scarlet y los patrones emergentes generados en cada ejecución.

Cada ejecución produce una colonia diferente aunque conserve la misma identidad.

| Criterio                    | Evidencia                                  | Cumplimiento |
| --------------------------- | ------------------------------------------ | ------------ |
| Movimiento basado en física | logré que cada particula lograra tener una posición, velocidad y fuerzas              | 5           |
| Varias poblaciones          | hice 8 tipos de partículas  con diferentes propositos                    | 5           |
| Interacciones por distancia | Planteé una Matriz y sus respectivos rangos                            | 5            |
| Relaciones asimétricas      | Los minions morados solo seguian a los amarillos y estos corrian de ellos, Scarlet rexhazaba a veces a los minions amarillos, la mermelada generaba repulsión en los minions                  | 5            |
| Variabilidad                | posición inicial de las partículas, cantidad de individuos por especie, probabilidad de infección, estado inicial de Scarlet y los patrones emergentes generados en cada ejecución.                            | 5            |
| Emergencia                  | Se creaban grupos diferentes y buscaban objetivos distintos en el proceso, siempre estaban buscando lideres nuevos. Y hubieron comportamientos inesperados como que a veces ellos eran perseguidos por los villanos | 5           |
| Identidad visual            | Imágenes, colores y trails. Las poblaciones lograron ser reconocibles                 | 5           |

### nota: 5

