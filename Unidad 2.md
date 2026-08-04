
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
| **Scarlet (1)**| `0.0` / `0` | `+0.2` / `200` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **Pie Grande** | `+0.1` / `400` | `+0.1` / `400` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **El Macho** | `+0.2` / `500` | `+0.2` / `500` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |
| **Mermelada** | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` | `0.0` / `0` |

*(1) Scarlet alterna estocásticamente a un estado de traición donde su fuerza hacia Élite y Amarillos pasa a ser de `-1.5` con un radio de `250`.*							
### Distancias de interacción.

* **Infección por El Macho:** Colisión a < 15px. Probabilidad: 30% de convertir Amarillo a Morado.

* **Infección por Morados:** Colisión a < 10px. Probabilidad: 100% de convertir Amarillo/Élite a Morado.

* **Curación por Mermelada:** Colisión a < 25px. Probabilidad: 100% de convertir Morado a Amarillo.

* **Muerte de Pie Grande:** Si hay > 15 partículas Amarillas a < 30px de distancia simultáneamente, la partícula de Pie Grande se elimina del sistema.

Seleccioné distancias de interacción extremadamente cortas y eventos dependientes de la colisión física porque quiero hacer perceptible la ironía de que alcanzar su meta biológica y acercarse a lo que aman es exactamente lo que desencadena su propia mutación o la destrucción accidental de su líder. Espero que produzca momentos de clímax visual donde agrupaciones estables colapsan al darse el contacto.




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


