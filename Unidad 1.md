# Unidad 1: Aleatoriedad🫧🪼
## Actividad 03🫧🪼

En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.
*  La uniforme es que todos los numeros tienen la misma probabilidad de salir, la no uniforme significa que la probabilidad de salir de un numero tiende a una media.

Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha

```js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();

}

class Walker {
  constructor() {
    this.x1 = width / 2;
    this.y1 = height / 2;
     this.x2 = width / 3;
    this.y2= height / 3;
    this.x3 = width / 6;
    this.y3= height / 6;
  }
  show() {
    stroke(random(0,256),random(0,256),random(0,256));
    triangle(this.x1, this.y1, this.x2, this.y2, this.x3, this.y3)
  }

 step() {
  let r = randomGaussian()

  if (r < 0.5) {          
    this.x1++;
    this.x2++;
    this.x3++;
  } else if (r < 0.7) {   
    this.x1--;
    this.x2--;
    this.x3--;
  } else if (r < 0.85) {  
    this.y1--;
    this.y2--;
    this.y3--;
  } else {               
    this.y1++;
    this.y2++;
    this.y3++;
  }
}
  }



```


## Actividad 04🫧🪼

```
function setup() {
  createCanvas(400, 400);
}

function draw() {
 
  let x = randomGaussian(200, 60);
  let y = randomGaussian(200, 60);
  noStroke();
  fill(random(255), random(255),random(255));
  circle(x, y, 16);
}
```

<img width="546" height="537" alt="image" src="https://github.com/user-attachments/assets/e62a2a9a-e9b8-4990-bfd9-4852b87f9a4d" />

## Actividad 05🫧🪼

```
let walker;
function setup() {
  createCanvas(400, 400);
    walker = new Walker();
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
      this.x = width / 2;
  this.y = height / 2;
  }
 show()  
 {
noStroke();
fill(0,10);
circle(this.x, this.y, random(100));
    
  }
  
step() {
let r = random(1);
if (r < 0.2) {
  this.x = random(-400, 400);
  this.y = random(-400, 400);
} else {
  this.x += random(-1, 1);
  this.y += random(-1, 1);
}
}}
```

<img width="437" height="417" alt="image" src="https://github.com/user-attachments/assets/7040d0ea-2e90-475a-9807-4180804600dd" />

- Explica por qué usaste esta técnica y qué resultados esperabas obtener.

    Genuinamente me puse a improvisar haciendo esto, planeaba adaptar la actividad anterior a esta distribución levy pero pues no son distribuciones parecidas entonces como que no habia captado bien que hacer. Ahora despúes lo que hice fue que agarre el primer ejercicio y use la logica del walker y la adapte al de la actividad 3 pero modificando el step con las proobabilidades del levy.

  ## Actividad 06🫧🪼
```js
let t = 0;
let walker;
function setup() {
  createCanvas(400, 400);
    walker = new Walker();
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
     this.x = width / 2;
    this.y = height / 2;
  }
 show()  
 {
noStroke();
fill(0,10);
circle(this.x, this.y, random(20));
    
  }
  
step() {
   this.x = map(noise(t), 0, 1, 0, width);
    this.y = map(noise(t+100), 0, 1, 0, height);

    t += 0.01;
}}


```
  <img width="478" height="410" alt="image" src="https://github.com/user-attachments/assets/997ad238-4da1-4718-a21d-60a4752ed714" />

- Explica por qué lo visualizaste de esa manera y qué resultados esperabas obtener.
  
    Queria hacer como la misma versión del codigo anterior y ver tal vez como se  visualizaría si le cambiaba el tipo de distribucíon que se usaba.  Elegí hacerlo de esta forma ya que podia ver como los saltos que se daban en la otra distribución transformados a un movimiento mas "natural".

## Actividad 07🫧🪼
### Reto de diseño: Navegar la incertidumbre

Como idea inicial quiero lograr mover diferentes figuras que puedan cambiar de forma con la interacción del usuario.

Planeo usar el codigo de la actividad 5 como base para trabajar en la experiencia completa.

Para iniciar primero tengo que lograr cambiar las figuras con la interacción del click. No estaba muy segura de como empezar a hacerlo entonces le pregunté a chatgpt como emcaminarme para hacerlo y entenderlo.

Primero tenia que modificar el walker para que este leyera el cambio de la figura al hacer la interacción del click. La forma es primero añadirle una variable de shape a este constructor. La idea es que el walker pueda leer cual figura se esta guardando.

  
* 0 = círculo
* 1 = cuadrado
* 2 = triángulo

```js
  
constructor() {
  this.x = width / 2;
  this.y = height / 2;

  this.shape = 0;

}

```

y para q eso funcione ahora hay que hacer que en el show este el if else para que lea que numero es y muestre esa figura cuando se interactue con el click y se le sume al contador.

```js
show() {
  noStroke();
  fill(0, 10);

  if (this.shape == 0) {
    circle(this.x, this.y, 40);

  } else if (this.shape == 1) {
    rectMode(CENTER);
    square(this.x, this.y, 40);

  } else if (this.shape == 2) {
    triangle(
      this.x, this.y - 20,
      this.x - 20, this.y + 20,
      this.x + 20, this.y + 20
    );
  }
}
```

Y para que funcione lo del click se crea una función que detecte el mouse y le sume el numero al contador, y cuando llega a un número mayor de 2 se reinicia.

```js
function mousePressed() {
  walker.shape++;

  if (walker.shape > 2) {
    walker.shape = 0;
  }
}
```
Y asi queda la primera parte que tenia en mente hacer.


<img width="510" height="502" alt="image" src="https://github.com/user-attachments/assets/58f90b28-9172-44ed-adcb-3bcff84a890f" />


```js
  let walker;
function setup() {
  createCanvas(400, 400);
    walker = new Walker();
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
     this.shape = 0;
      this.x = width / 2;
  this.y = height / 2;
  }
 show() {
  noStroke();
  fill(0, 10);

  if (this.shape == 0) {
    circle(this.x, this.y, random(50));

  } else if (this.shape == 1) {
    rectMode(CENTER);
    square(this.x, this.y,  random(50));

  } else if (this.shape == 2) {
    triangle(
      this.x, this.y - random(50),
      this.x - random(50), this.y + random(50),
      this.x + random(50), this.y + random(50)
    );
  }
} step() {
    let r = random(1);

    if (r < 0.2) {
      this.x = random(-400, 400);
      this.y = random(-400, 400);
    } else {
      this.x += random(-1, 1);
      this.y += random(-1, 1);
    }
  }
} 

function mousePressed() {
  walker.shape++;

  if (walker.shape > 2) {
    walker.shape = 0;
  }
}

```

Bueno, en este punto habia que darle un poquito de autonomia al codigo para que el solito ambiara de figura sin necesidad de interactuar. Entonces lo que voy a hacer es poner un temporizador que cambie el contador si no detecta una interacción del mouse por mas de 10 segundos.


Siguiendo la misma logica de lo ultimo que hice voy a añadir otro contador pero que sea el del tiempo y añadirlo en el setup para inicializarla. Desúes en la función draw para 

```js
function draw() {
  walker.step();
  walker.show();

  if (millis() - ultimoClick > 10000) {
    walker.shape++;

    if (walker.shape > 2) {
      walker.shape = 0;
    }

    ultimoClick = millis();
  }
}
```

Aca en esta parte me estrellé un poquito pq genuinamente me perdi en como hacer eso y pedi ayuda a chat. Me explicó que habia que usarlo en el draw para que cada fotograma se lea lo que esta ocurriendo y se leen los segundos que lleva ejecutando los dibujos por decirlo asi. Para saber si cambia de figura lo que hace es leer cuanto tiempo lleva corriendo el programa y lo resta con la ultima vez que se hizo una interacción con el. Y para que el programa tenga como continuidad en la interacción con el usuario se usa la misma logica pero en la función de mousepressed que va a estar basicamente pendiente de que hacer cuando se haga una interaccion.

```js
function mousePressed() {
  walker.shape++;

  if (walker.shape > 2) {
    walker.shape = 0;
  }

  ultimoClick = millis();
}
```

Y la versión de este programa quedaria de esta forma.

```js
let walker;
let ultimoClick = 0;

function setup() {
  createCanvas(400, 400);
    walker = new Walker();
}

function draw() {
  walker.step();
  walker.show();

  if (millis() - ultimoClick > 10000) {
    walker.shape++;

    if (walker.shape > 2) {
      walker.shape = 0;
    }

    ultimoClick = millis();
  }
}
class Walker {
  constructor() {
     this.shape = 0;
      this.x = width / 2;
  this.y = height / 2;
  }
 show() {
  noStroke();
  fill(0, 10);

  if (this.shape == 0) {
    circle(this.x, this.y, random(50));

  } else if (this.shape == 1) {
    rectMode(CENTER);
    square(this.x, this.y,  random(50));

  } else if (this.shape == 2) {
    triangle(
      this.x, this.y - random(50),
      this.x - random(50), this.y + random(50),
      this.x + random(50), this.y + random(50)
    );
  }
} step() {
    let r = random(1);

    if (r < 0.2) {
      this.x = random(-400, 400);
      this.y = random(-400, 400);
    } else {
      this.x += random(-1, 1);
      this.y += random(-1, 1);
    }
  }
} 

function mousePressed() {
  walker.shape++;

  if (walker.shape > 2) {
    walker.shape = 0;
  }
}
```
### No se ve mucho en la imagen la automatización del cambio de figura.
<img width="451" height="420" alt="image" src="https://github.com/user-attachments/assets/cfd168ba-df12-4434-b995-934b0c901900" />


Bueno, ahora que hice la interacción con usuario toca hacer el resto de cosas. Se me vino a la cabeza para la parte del evento improbable tal vez hacer que haya una probabilidad minima de que los colores de las figuras sean arcoiris, vayan como de forma mas frenetica y se deformen. Y que despúes de un tiempo se normalizara. 

Para lograr esto hay que hacer algo que llamaremos modo excepción que es como este modo que solo se va a activar cuando se cumpla esta probabilidad.

Primero, hay que crear una variable de modoexcepción y un contador que lea cuanto dura este modo excepcion para que se pueda temporizar.


```js
let walker;
let modoExcepcion = false;
let inicioExcepcion = 0;
```
 Ahora, para hacer la parte de la probabilidad en draw se pone 

```js
if (!modoExcepcion && random(1) < 0.001) {
  modoExcepcion = true;
  inicioExcepcion = millis();
}


if (modoExcepcion && millis() - inicioExcepcion > 5000) {
  modoExcepcion = false;
}
```

Este código lee si en ese momento se esta en modo excepción o no, si no se esta en modo excepción y se cumple la probabilidad se inicializa. Cuando se activa se empieza el contador que mira que la excepción dure  5 segundos.

 Y ahora para hacer todos lo cambios hay que llenar la función de show con puros ifs, que va a leer si se esta en modo excepcion o no.

 <img width="515" height="452" alt="image" src="https://github.com/user-attachments/assets/4a6ce7c8-ac8b-415b-8415-41dee9a1ae52" />

 
```js
 let walker;
let ultimoClick = 0;


let modoExcepcion = false;
let inicioExcepcion = 0;

function setup() {
  createCanvas(400, 400);
  walker = new Walker();

  ultimoClick = millis();
}

function draw() {

  walker.step();
  walker.show();


  if (millis() - ultimoClick > 10000) {
    walker.shape++;

    if (walker.shape > 2) {
      walker.shape = 0;
    }

    ultimoClick = millis();
  }


  if (!modoExcepcion && random(1) < 0.001) {
    modoExcepcion = true;
    inicioExcepcion = millis();
  }

 
  if (modoExcepcion && millis() - inicioExcepcion > 2000) {
    modoExcepcion = false;
  }
}

class Walker {

  constructor() {
    this.shape = 0;
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {

    noStroke();

 
    if (modoExcepcion) {
      fill(random(255), random(255), random(255), 120);
    } else {
      fill(0, 10);
    }

    if (this.shape == 0) {

      if (modoExcepcion) {
        circle(this.x, this.y, random(30, 90));
      } else {
        circle(this.x, this.y, random(50));
      }

    } else if (this.shape == 1) {

      rectMode(CENTER);

      if (modoExcepcion) {
        square(this.x, this.y, random(30, 90));
      } else {
        square(this.x, this.y, random(50));
      }

    } else if (this.shape == 2) {

      if (modoExcepcion) {

        triangle(
          this.x,
          this.y - random(80),
          this.x - random(80),
          this.y + random(80),
          this.x + random(80),
          this.y + random(80)
        );

      } else {

        triangle(
          this.x,
          this.y - random(50),
          this.x - random(50),
          this.y + random(50),
          this.x + random(50),
          this.y + random(50)
        );

      }

    }

  }

  step() {

    let r = random(1);

    if (r < 0.2) {
      this.x = random(-400, 400);
      this.y = random(-400, 400);
    } else {

      if (modoExcepcion) {

        
        this.x += random(-8, 8);
        this.y += random(-8, 8);

      } else {

        this.x += random(-1, 1);
        this.y += random(-1, 1);

      }

    }

  }

}

function mousePressed() {

  walker.shape++;

  if (walker.shape > 2) {
    walker.shape = 0;
  }

 
  ultimoClick = millis();

}

```

Ahora hay que hacer uso de los conceptos que usamos a lo largo de la unidad. Me lo imaginaba como cada figura tuviera su propio tipo de distribución. Para aumentar además la interacción del usuario voy a hacer que cada vez que se haga click se aumente la probabilidad del modo excepción y que este tenga un tope para reiniciarse.


Voy a organizar el proyecto de la siguiente manera:


* Posibilidad → Círculo → caminata completamente aleatoria.
* Tendencia → Cuadrado → distribución no uniforme con preferencia hacia una dirección.
* Normalidad → Triángulo → distribución normal.
* Excepción → Modo especial → Lévy Flight + arcoíris + movimiento rapido.
* Influencia → El usuario cambia el comportamiento y modifica la probabilidad de que ocurra la excepción.

```js

let walker;
let ultimoClick = 0;


let modoExcepcion = false;
let inicioExcepcion = 0;

function setup() {
  createCanvas(400, 400);
  walker = new Walker();

  ultimoClick = millis();
}

function draw() {

  walker.step();
  walker.show();


  if (millis() - ultimoClick > 10000) {
    walker.shape++;

    if (walker.shape > 2) {
      walker.shape = 0;
    }

    ultimoClick = millis();
  }


  if (!modoExcepcion && random(1) < 0.001) {
    modoExcepcion = true;
    inicioExcepcion = millis();
  }

 
  if (modoExcepcion && millis() - inicioExcepcion > 2000) {
    modoExcepcion = false;
  }
}

class Walker {

  constructor() {
    this.shape = 0;
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {

    noStroke();

 
    if (modoExcepcion) {
      fill(random(255), random(255), random(255), 120);
    } else {
      fill(0, 10);
    }

    if (this.shape == 0) {

      if (modoExcepcion) {
        circle(this.x, this.y, random(30, 90));
      } else {
        circle(this.x, this.y, random(50));
      }

    } else if (this.shape == 1) {

      rectMode(CENTER);

      if (modoExcepcion) {
        square(this.x, this.y, random(30, 90));
      } else {
        square(this.x, this.y, random(50));
      }

    } else if (this.shape == 2) {

      if (modoExcepcion) {

        triangle(
          this.x,
          this.y - random(80),
          this.x - random(80),
          this.y + random(80),
          this.x + random(80),
          this.y + random(80)
        );

      } else {

        triangle(
          this.x,
          this.y - random(50),
          this.x - random(50),
          this.y + random(50),
          this.x + random(50),
          this.y + random(50)
        );

      }

    }

  }

step() {

  
  if (modoExcepcion) {

    this.x += random(-8, 8);
    this.y += random(-8, 8);

  } 
  

  else if (this.shape == 0) {

    this.x += random(-10, 10);
    this.y += random(-10, 10);

  } 
  
else if (this.shape == 1) {

  let r = random(1);

  if (r < 0.45) {

    
    this.x += random(0.5, 2);

  } else if (r < 0.65) {


    this.x -= random(0.5, 2);

  } else if (r < 0.825) {

   
    this.y += random(-1, 5);

  } else {

    
    this.y -= random(-1, 2);

  }

}
  
  
  else if (this.shape == 2) {

    this.x += randomGaussian() * 2;
    this.y += randomGaussian() * 2;

  }

}

}

function mousePressed() {

  walker.shape++;

  if (walker.shape > 2) {
    walker.shape = 0;
  }

  
  ultimoClick = millis();

}
```

La primera figura mantiene una caminata aleatoria, donde puede moverse en cualquier dirección sin tener una preferencia específica. La segunda figura tiene una pequeña tendencia hacia el movimiento horizontal, haciendo que sea más probable que avance hacia un lado, aunque todavía conserva la posibilidad de cambiar de dirección aunque no me esta funcionando bien, se ve super exagerado. Finalmente, la tercera figura utiliza una distribución normal con randomGaussian() pero realmente se ve super parecida a la anterior.

<img width="382" height="386" alt="image" src="https://github.com/user-attachments/assets/1fa12e2a-2475-4adf-906c-a75285c38f70" />

### simplemente se ve horrible

Para mejorarlo un poquito en este punto voy a estabilizar el tamaño de las figuras en el modo normal y en el modo excepción voy a hacer que ya sigan aleatorias. Y voy a fijar un color a el modo excepción  de cada color.


<img width="437" height="403" alt="image" src="https://github.com/user-attachments/assets/3d7877c8-ae97-4eca-946c-0b22b54329d3" />

```js
let walker;
let ultimoClick = 0;


let modoExcepcion = false;
let inicioExcepcion = 0;

function setup() {
  createCanvas(400, 400);
  walker = new Walker();

  ultimoClick = millis();
}

function draw() {

  walker.step();
  walker.show();


  if (millis() - ultimoClick > 10000) {
    walker.shape++;

    if (walker.shape > 2) {
      walker.shape = 0;
    }

    ultimoClick = millis();
  }


  if (!modoExcepcion && random(1) < 0.001) {
    modoExcepcion = true;
    inicioExcepcion = millis();
  }

 
  if (modoExcepcion && millis() - inicioExcepcion > 2000) {
    modoExcepcion = false;
  }
}

class Walker {

  constructor() {
    this.shape = 0;
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {

    noStroke();


    if (this.shape == 0) {

      if (modoExcepcion) {
        circle(this.x, this.y, random(30));
        fill(247, 0, 111, 50)
      } else {
        circle(this.x, this.y, 10);
        fill(0, 10);
      }

    } else if (this.shape == 1) {

      rectMode(CENTER);

      if (modoExcepcion) {
        square(this.x, this.y, random(30));
        fill(247, 218, 0, 50)
      } else {
        square(this.x, this.y, 10);
         fill(0, 10);
      }

    } else if (this.shape == 2) {

      if (modoExcepcion) {

        triangle(
          this.x,
          this.y - random(30),
          this.x - random(30),
          this.y + random(30),
          this.x + random(30),
          this.y + random(30)
        );
        fill(156, 247, 0, 50)

      } else {

        triangle(
          this.x,
          this.y - 10,
          this.x - 10,
          this.y + 10,
          this.x + 10,
          this.y + 10
        );
         fill(0, 10);

      }

    }

  }

step() {

  
  if (modoExcepcion) {

    this.x += random(-8, 8);
    this.y += random(-8, 8);

  } 
  

  else if (this.shape == 0) {

    this.x += random(-10, 10);
    this.y += random(-10, 10);

  } 
  
else if (this.shape == 1) {

  let r = random(1);

  if (r < 0.45) {

    
    this.x += random(0.5, 2);

  } else if (r < 0.65) {


    this.x -= random(0.5, 2);

  } else if (r < 0.825) {

   
    this.y += random(-1, 5);

  } else {

    
    this.y -= random(-1, 2);

  }

}
  
  
  else if (this.shape == 2) {

    this.x += randomGaussian() * 2;
    this.y += randomGaussian() * 2;

  }

}

}

function mousePressed() {

  walker.shape++;

  if (walker.shape > 2) {
    walker.shape = 0;
  }

  
  ultimoClick = millis();

}
```

Todo mal :(, creo que mi error en general fue no entender del todo bien el proposito de diseñar la experiencia desde un concepto.

Bueno, hay que retomar el diseño de concepto porque me desvie totalmente del proposito de la actividad y me fue accidentalmente por un camino mas de arte y improvisación que por el camino de diseñar.

Me puse a investigar sobre festivales de ciencia y arte que estuvieran ocurriendo aca en medellin y encontré "el Festival Buen Comienzo 2026: Un Viaje al Universo". Una de las actividades que se iban a realizar en este festival es "La Aventura Lunar, una recreación de la superficie de la Luna."

Me gustaria intentar recrear como la superficie de la luna por medio de una experiencia que fuera construyendola lenntamente o intentara simularla.

## CONCEPTO
En vez de pensar:

"voy a dibujar la Luna"

Vamos a pensar:

"voy a dejar que miles de impactos microscópicos construyan lentamente un terreno."


Usando de base el intento fallido anterior voy a empezar desde ahi para empezar a dibujar los trazos. Voy a borrar el cambio de figura y eliminar el resto de figuras. Solo deje el circulo que me gustó como se estaba comportando ya que me gustaba pensar en circulitos como particulas de polvo que van construyendo este lugar que se va pareciendo como al regolito. Además inverti los colores para q el fondo fuera negro y el circulo blanco.


```js
let walker;
let ultimoClick = 0;


let modoExcepcion = false;
let inicioExcepcion = 0;

function setup() {
  createCanvas(1920, 1080);
  walker = new Walker();
background(0);
  ultimoClick = millis();
}

function draw() {

  walker.step();
  walker.show();


  if (millis() - ultimoClick > 10000) {
    walker.shape++;

    if (walker.shape > 2) {
      walker.shape = 0;
    }

    ultimoClick = millis();
  }


  if (!modoExcepcion && random(1) < 0.001) {
    modoExcepcion = true;
    inicioExcepcion = millis();
  }

 
  if (modoExcepcion && millis() - inicioExcepcion > 2000) {
    modoExcepcion = false;
  }
}

class Walker {

  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {

    noStroke();


    

      if (modoExcepcion) {
        circle(this.x, this.y, random(30));
        fill(247, 0, 111, 10)
      } else {
        circle(this.x, this.y, 10);
        fill(255, 10);
      }

   

  }

 step() {

      this.x += random(-10, 10);
      this.y += random(-10, 10);
    
   
    }
  
} 

  

function mousePressed() {


}

```

Hay un problemita y es que cuando se inicia el programa el punto inicial queda como un circulo blanco super saturadO, la idea es que desde el inicio salgan parejito de opacidad. Le pregunte a chat que me explicara que estaba ocurriendo y me explicó que el fill tiene que ir primero que el circle. 

En la parte de la interacción con el usuario funcionara con el click del mouse nuevamente. Va a hacer que cada que se de click al mouse se cree un nuevo circulito por decirlo asi que funciona igual que el inicial. La verdad en este punto me tuve que apoyar mas de chatgpt porque ya si me perdí del todo.

Chat me recomendó que cada circulo tuviera su propio estado para que entren en modo excepción de forma independiente. Entonces para hacerlo hay que usar un arreglo de walkers para que sean varios.

primero en el set up se esta acomodando el primer circulo del arreglo para que inicie en el centro de la pantalla.

despues en draw se lee los walkers del arreglo y se corren los codigos de step, update y show. Se añadió el metodo de update como el nuevo que lee si entra en modo excepción o no.
```js
let walkers = [];
let ultimoClick = 0;


let modoExcepcion = false;
let inicioExcepcion = 0;

function setup() {
  createCanvas(1920, 1080);
  background(0);

  walkers.push(new Walker(width/2, height/2, color(255)));
}

function draw() {
  
for (let w of walkers) {
  w.step();
  w.update();
  w.show();
}
  
}

class Walker {

  constructor(x, y) {
    this.x = x;
    this.y = y;

   

    this.modoExcepcion = false;
    this.inicioExcepcion = 0;
  }

  update() {

  if (!this.modoExcepcion && random(1) < 0.001) {
    this.modoExcepcion = true;
    this.inicioExcepcion = millis();
  }

  if (this.modoExcepcion &&
      millis() - this.inicioExcepcion > 2000) {
    this.modoExcepcion = false;
  }
}


 show() {

  noStroke();

  if (this.modoExcepcion) {
   fill(255,10);

    circle(this.x, this.y, random(15,30));

  } else {
    fill(255,10);

    circle(this.x, this.y, 10);
  }
}
  

 step() {

      this.x += random(-10, 10);
      this.y += random(-10, 10);
    
   
    }

}
function mousePressed() {

  walkers.push(
    new Walker(
      mouseX,
      mouseY
     
    )
  );

}
  



```
<img width="946" height="717" alt="image" src="https://github.com/user-attachments/assets/c18357dc-8434-4e79-ab5c-dd0479ac580a" />


En este punto ya se estaba asemejando al relieve y textura de la luna en mi criterio. 
Tenia la idea de hacer como una galaxia y que se vieran las estrellas. Para eso demarque primero como un rango en donde el walker iba a andar nada mas y que este fuera el circulo que representa la luna.


 ```js

let walkers = [];
let ultimoClick = 0;


let modoExcepcion = false;
let inicioExcepcion = 0;
let radius = 800;

let t = 0
function setup() {
  createCanvas(1920, 1080);
  background(0
            );

  walkers.push(new Walker(width/2, height/2, color(255)));
}

function draw() {

  
for (let w of walkers) {
  w.step();
  w.update();
  w.show();
}

  
  
}

class Walker {

  constructor(x, y) {
    this.x = x;
    this.y = y;

   

    this.modoExcepcion = false;
    this.inicioExcepcion = 0;
  }

  update() {

  if (!this.modoExcepcion && random(1) < 0.001) {
    this.modoExcepcion = true;
    this.inicioExcepcion = millis();
  }

  if (this.modoExcepcion &&
      millis() - this.inicioExcepcion > 2000) {
    this.modoExcepcion = false;
  }
}


 show() {

  noStroke();

  if (this.modoExcepcion) {
   fill(255,10);

    circle(this.x, this.y, random(15,30));

  } else {
    fill(255,10);

    circle(this.x, this.y, 10);
  }
}
  

 step() {

      this.x += random(-10, 10);
      this.y += random(-10, 10);

      if(dist(this.x,this.y,width/2,height/2) > radius/2)
      {
        this.x = random(-100, 100);
        this.y = random(-100, 100);
      }
   
    }

}



function mousePressed() {

  walkers.push(
    new Walker(
      mouseX,
      mouseY
     
    )
  );

}
 ```
<img width="523" height="420" alt="image" src="https://github.com/user-attachments/assets/6216524f-d35c-4989-b8bf-b0d23cf62a76" />

  Para la estrellas luego hice esto con la ayuda de la inteligencia artifical. 
<img width="586" height="415" alt="image" src="https://github.com/user-attachments/assets/316c7ef4-9607-4839-8d1c-bdc5d3d3f3a4" />

Tenia el concepto de que cada que una de los walkers que estaban dentro de la luna chocaran con el limite del circulo se empezaran a generar estrellas en el fondo pero la verdad no me terminaba de convencer porque se terminaba saturando demasiado la pantalla y seguia sin haber una tendencia en el programa porque todas las direcciones seguian siendo igual de probables.

 ```js

let walkers = [];
let stars = []
let ultimoClick = 0;


let modoExcepcion = false;
let inicioExcepcion = 0;
let radius = 800;

let t = 0
let choice = 0
function setup() {
  createCanvas(1920, 1080);
  background(0
            );

  walkers.push(new Walker(width/2, height/2, color(255)));
}

function draw() {

  textSize(49)
text(t,50,50)
  
for (let w of walkers) {
  w.step();
  w.update();
  w.show();
}

  for (let s of stars) {
  s.show();
}


  
  
}

class Walker {

  constructor(x, y) {
    this.x = x;
    this.y = y;

   

    this.modoExcepcion = false;
    this.inicioExcepcion = 0;
  }

  update() {

  if (!this.modoExcepcion && random(1) < 0.001) {
    this.modoExcepcion = true;
    this.inicioExcepcion = millis();
  }

  if (this.modoExcepcion &&
      millis() - this.inicioExcepcion > 2000) {
    this.modoExcepcion = false;
  }
}


 show() {

  noStroke();

  if (this.modoExcepcion) {
   fill(255,10);

    circle(this.x, this.y, random(15,30));

  } else {
    fill(255,10);

    circle(this.x, this.y, 10);
  }
}
  

 step() {

      this.x += random(-10, 10);
      this.y += random(-10, 10);

      if(dist(this.x,this.y,width/2,height/2) > radius/2)
      {
        stars.push(new Star(random(0,width),random(0,height),t))
        this.x += random(-100, 100);
        this.y += random(-100, 100);

        t++
        if(t > 3) t = 0
      }
   
    }

}
class Star {
  constructor(x,y,choice)
  {
    this.x = x
    this.y = y
    this.choice = choice
  }

  show()
  {
    if(this.choice == 0){ fill(255,150,0)}
    if(this.choice == 1) {fill(170,170,255) }
    if(this.choice == 2) {fill(255,170,170 )}
    if(this.choice == 3) {fill(255,255,255 )}
    
    circle(this.x,this.y,randomGaussian(0.1,0.5))
  }
}


function mousePressed() {

  walkers.push(
    new Walker(
      mouseX,
      mouseY
     
    )
  );

}
  

 ```


* No hay una distribución normal (todo usa random() uniforme).


* La interacción con el visitante  (mousePressed) solo añade walkers; no cambia las probabilidades del sistema.

* La excepción ocurre constantemente cuando sale del círculo, no como un evento realmente improbable.



Una galaxia no es galaxia sin cometas , ni estrellas, etc. Conceptualice que esas estrellitas que estaban en el fondo tuvieran la posibilidad de explotar como las supernovas y sacudir un poquito sus alrededores.
 Tambien pensé como  desde lejos, el choque de grandes meteoritos en la luna parece como una lluvia de estrellas que solo se detecta como breves destellos de luz con telescopios especiales. Entonces estaria interesante lograr este efectoen las estrelas que ya estaban hechas. La forma de lograrlo fue aprovechar los Levy flights de los walkers. Cada vez que un walker realiza uno de esos saltos y abandona el límite del sistema, deja una estrella en el punto donde salió y cae a la luna. Estas estrellas nacen como un registro de ese evento poco frecuente y permanecen brillando lentamente hasta desvanecerse.


Me faltaba solucionar los temas del concepto de la unidad y los requisitos del reto.


Para lograrlo utilicé walkers, ya que permiten construir trayectorias a partir de pequeñas decisiones probabilísticas en lugar de seguir una ruta fija.

La mayor parte del tiempo el walker utiliza una distribución normal, por lo que da pasos cortos alrededor de su posición actual. Esto hace que el recorrido permanezca concentrado y que visualmente la luna parezca mantenerse en una órbita estable, representando la normalidad del sistema.

Sin embargo, no quería que el movimiento fuera siempre igual. Por eso incorporé una tendencia, donde algunos pasos tienen una ligera preferencia hacia una dirección determinada. Esa preferencia es pequeña, pero al repetirse muchas veces termina construyendo una trayectoria reconocible sin eliminar el componente aleatorio.

Finalmente, añadí una excepción mediante Levy Flights. En muy pocas ocasiones el walker realiza un salto mucho más largo que los demás, permitiéndole explorar zonas nuevas del espacio. Estos eventos representan sucesos improbables que rompen el comportamiento habitual y, además, dejan una estrella como evidencia de que ocurrió algo extraordinario.


 
 ```js 


let walkers = [];
let stars = []
let ultimoClick = 0;
let trail;
let influencia = 0;
let direccionMouse;
let modoExcepcion = false;
let inicioExcepcion = 0;
let radius = 800;

let t = 0
let choice = 0
function setup() {
  createCanvas(1080, 1920);
  trail = createGraphics(1080,1920);
trail.background(0);
  background(0
            );

  walkers.push(new Walker(width/2, height/2, color(255)));
}

function draw() {

  background(0);


  image(trail,0,0);


  for (let w of walkers) {
    w.step();
    w.update();
    w.show();
  }


  for(let s of stars){
    s.update();
    s.show();
  }


  stars = stars.filter(s => !s.dead);

}


  
  


class Walker {

  constructor(x, y) {
    this.x = x;
    this.y = y;

   

    this.modoExcepcion = false;
    this.inicioExcepcion = 0;
  }

  update() {

  if (!this.modoExcepcion && random(1) < 0.001) {
    this.modoExcepcion = true;
    this.inicioExcepcion = millis();
  }

  if (this.modoExcepcion &&
      millis() - this.inicioExcepcion > 2000) {
    this.modoExcepcion = false;
  }
}


show() {

  trail.noStroke();

  if (this.modoExcepcion) {

    trail.fill(255,7);
    trail.circle(this.x,this.y,random(15,30));

  } 
  
  else {

    trail.fill(255,5);
    trail.circle(this.x,this.y,10);

  }

}
  

step(){

  let r = random(1);

  let dx;
  let dy;


 
  let mouseInfluence = influencia;



  
  if(r < 0.85 - mouseInfluence*0.2){

    dx = randomGaussian(0,3);
    dy = randomGaussian(0,3);

  }


 
  
  else if(r < 0.98){

    let target = direccionMouse || 0;


    dx = cos(target)*randomGaussian(4,2);
    dy = sin(target)*randomGaussian(4,2);


  }



  else{


    let ang = random(TWO_PI);

    let salto = random(80,300);


    dx = cos(ang)*salto;
    dy = sin(ang)*salto;


  }



  this.x += dx;
  this.y += dy;



  

  if(dist(this.x,this.y,width/2,height/2)>radius/2){


    stars.push(
      new Star(
        this.x,
        this.y,
        t
      )
    );


    this.x = lerp(
      this.x,
      width/2,
      0.05
    );


    this.y = lerp(
      this.y,
      height/2,
      0.05
    );

  }


}

}
class Star {

  constructor(x, y, choice) {

    this.x = x;
    this.y = y;
    this.choice = choice;

    this.size = random(1,3);

this.alpha = 255;
this.fadeSpeed = random(0.5,1.5);
    this.dead = false;

    this.state = "normal";

    this.flash = 0;
    this.explosion = 0;

    this.particles = [];
  }


  update() {



this.alpha -= this.fadeSpeed;


if(this.alpha <= 0){
  this.dead = true;
}


// EVENTO RARO DE EXPLOSIÓN
if(this.state == "normal" && random(1) < 0.00002){

  this.state = "flash";
  this.flash = 0;

}


    
    if(this.state == "flash") {

      this.flash++;

      if(this.flash > 20){

        this.state = "supernova";


        // crear partículas
        for(let i=0;i<40;i++){

          let ang = random(TWO_PI);
          let speed = random(1,6);

          this.particles.push({

            x:this.x,
            y:this.y,

            vx:cos(ang)*speed,
            vy:sin(ang)*speed,

            alpha:255

          });

        }

      }

    }



 
    if(this.state == "supernova") {


      this.explosion += 3;
this.alpha -= 2;


      
      for(let s of stars){

        if(s !== this){

          let d = dist(
            this.x,
            this.y,
            s.x,
            s.y
          );


          if(d < this.explosion){


            let ang = atan2(
              s.y-this.y,
              s.x-this.x
            );


            let fuerza = map(
              d,
              0,
              this.explosion,
              5,
              0
            );


            s.x += cos(ang)*fuerza;
            s.y += sin(ang)*fuerza;

          }

        }

      }




   

      for(let p of this.particles){

        p.x += p.vx;
        p.y += p.vy;

        p.alpha -= 5;

      }


      this.particles =
      this.particles.filter(
        p=>p.alpha>0
      );



      if(this.explosion > 200 &&
         this.particles.length == 0){

        this.dead = true;

      }

    }

  }



  show(){


 

    if(this.state=="normal"){

      noStroke();

      fill(255,this.alpha);

      circle(
        this.x,
        this.y,
        this.size
      );

    }



   

    else if(this.state=="flash"){

      noStroke();


      fill(255,255,255,50);

      circle(
        this.x,
        this.y,
        10
      );


      fill(255,255,255,80);

      circle(
        this.x,
        this.y,
        30
      );


    }



 

    else if(this.state=="supernova"){


      noStroke();




     fill(255,255,255,this.alpha*0.2);

      circle(
        this.x,
        this.y,
        this.explosion
      );



      

      for(let p of this.particles){

fill(255,255,255,p.alpha*this.alpha/255);

        circle(
          p.x,
          p.y,
          3
        );

      }



    

   fill(255,this.alpha);

      circle(
        this.x,
        this.y,
        8
      );

    }


  }

}
function dibujarLuna(){

  noFill();
  stroke(255,30);
  strokeWeight(2);

  circle(width/2,height/2,radius);

}

function mousePressed(){

  direccionMouse = atan2(
    mouseY-height/2,
    mouseX-width/2
  );

  influencia = 1;


  walkers.push(
    new Walker(mouseX,mouseY)
  );

}
  
 ```


<img width="420" height="765" alt="image" src="https://github.com/user-attachments/assets/7272de31-80fd-4a4f-8cdd-aecfedd44d96" />


 Por ultimo faltaba terminar de implementar el tema de usabilidad del usuario.  HIce que el tema de la influencia y tendencia fuera al presionar el mouse en la antalla y que los walkers fueran hacia ese punto por decirlo asi.


```js

let walkers = [];
let stars = []
let ultimoClick = 0;
let trail;
let influencia = 0;
let direccionMouse;
let modoExcepcion = false;
let inicioExcepcion = 0;
let radius = 800;

let t = 0
let choice = 0
function setup() {
  createCanvas(1080, 1920);
  trail = createGraphics(1080,1920);
trail.background(0);
  background(0
            );

  walkers.push(new Walker(width/2, height/2, color(255)));
}

function draw() {

  background(0);


  image(trail,0,0);


  for (let w of walkers) {
    w.step();
    w.update();
    w.show();
  }


  for(let s of stars){
    s.update();
    s.show();
  }


  stars = stars.filter(s => !s.dead);

}


  
  


class Walker {

constructor(x, y) {
  this.x = x;
  this.y = y;

  this.modoExcepcion = false;
  this.inicioExcepcion = 0;

  this.creoEstrella = false;
}

  update() {

  if (!this.modoExcepcion && random(1) < 0.001) {
    this.modoExcepcion = true;
    this.inicioExcepcion = millis();
  }

  if (this.modoExcepcion &&
      millis() - this.inicioExcepcion > 2000) {
    this.modoExcepcion = false;
  }
}


show() {

  trail.noStroke();

  if (this.modoExcepcion) {

    trail.fill(255,7);
    trail.circle(this.x,this.y,random(15,30));

  } 
  
  else {

    trail.fill(255,5);
    trail.circle(this.x,this.y,10);

  }

}
  

step(){

  let r = random(1);

  let dx;
  let dy;


 
  let mouseInfluence = influencia;


  

  if(r < 0.85 - mouseInfluence*0.2){

    dx = randomGaussian(0,3);
    dy = randomGaussian(0,3);

  }

  else if(r < 0.98){

    let target = direccionMouse || 0;


    dx = cos(target)*randomGaussian(4,2);
    dy = sin(target)*randomGaussian(4,2);


  }




  else{


    let ang = random(TWO_PI);

    let salto = random(80,300);


    dx = cos(ang)*salto;
    dy = sin(ang)*salto;


  }




if (mouseIsPressed) {

  let ang = atan2(
    mouseY - this.y,
    mouseX - this.x
  );

  dx += cos(ang) * 2;
  dy += sin(ang) * 2;

}

this.x += dx;
this.y += dy;


 

  if(dist(this.x,this.y,width/2,height/2)>radius/2){


    stars.push(
      new Star(
        this.x,
        this.y,
        t
      )
    );


    this.x = lerp(
      this.x,
      width/2,
      0.05
    );


    this.y = lerp(
      this.y,
      height/2,
      0.05
    );

  }


}

}
class Star {

  constructor(x, y, choice) {

    this.x = x;
    this.y = y;
    this.choice = choice;

    this.size = random(1,3);

this.alpha = 255;
this.fadeSpeed = random(0.5,1.5);
    this.dead = false;

    this.state = "normal";

    this.flash = 0;
    this.explosion = 0;

    this.particles = [];
  }


  update() {



this.alpha -= this.fadeSpeed;


if(this.alpha <= 0){
  this.dead = true;
}



if(this.state == "normal" && random(1) < 0.00002){

  this.state = "flash";
  this.flash = 0;

}


   
    if(this.state == "flash") {

      this.flash++;

      if(this.flash > 20){

        this.state = "supernova";


      
        for(let i=0;i<40;i++){

          let ang = random(TWO_PI);
          let speed = random(1,6);

          this.particles.push({

            x:this.x,
            y:this.y,

            vx:cos(ang)*speed,
            vy:sin(ang)*speed,

            alpha:255

          });

        }

      }

    }



  
    if(this.state == "supernova") {


      this.explosion += 3;
this.alpha -= 2;


      // EMPUJE
      for(let s of stars){

        if(s !== this){

          let d = dist(
            this.x,
            this.y,
            s.x,
            s.y
          );


          if(d < this.explosion){


            let ang = atan2(
              s.y-this.y,
              s.x-this.x
            );


            let fuerza = map(
              d,
              0,
              this.explosion,
              5,
              0
            );


            s.x += cos(ang)*fuerza;
            s.y += sin(ang)*fuerza;

          }

        }

      }




      

      for(let p of this.particles){

        p.x += p.vx;
        p.y += p.vy;

        p.alpha -= 5;

      }


      this.particles =
      this.particles.filter(
        p=>p.alpha>0
      );



      if(this.explosion > 200 &&
         this.particles.length == 0){

        this.dead = true;

      }

    }

  }



  show(){


  

    if(this.state=="normal"){

      noStroke();

      fill(255,this.alpha);

      circle(
        this.x,
        this.y,
        this.size
      );

    }



 

    else if(this.state=="flash"){

      noStroke();


      fill(255,255,255,50);

      circle(
        this.x,
        this.y,
        10
      );


      fill(255,255,255,80);

      circle(
        this.x,
        this.y,
        30
      );


    }



  

    else if(this.state=="supernova"){


      noStroke();


     

     fill(255,255,255,this.alpha*0.2);

      circle(
        this.x,
        this.y,
        this.explosion
      );



    
      for(let p of this.particles){

fill(255,255,255,p.alpha*this.alpha/255);

        circle(
          p.x,
          p.y,
          3
        );

      }



 

   fill(255,this.alpha);

      circle(
        this.x,
        this.y,
        8
      );

    }


  }

}
function dibujarLuna(){

  noFill();
  stroke(255,30);
  strokeWeight(2);

  circle(width/2,height/2,radius);

}

function mousePressed(){

  direccionMouse = atan2(
    mouseY-height/2,
    mouseX-width/2
  );

  influencia = 1;


  walkers.push(
    new Walker(mouseX,mouseY)
  );

}
 ```
Para poder lograr todo esto me tuve que apoyar bastante de la inteligencia artificial a la hora de realizar el codigo.


<img width="474" height="544" alt="image" src="https://github.com/user-attachments/assets/42685ad9-f019-4bf3-a53f-ca6d56b30e15" />

| **Criterio**                                                                                                                                      | **Cumplo** | **No cumplo** | **Evidencia**                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | :--------: | :-----------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Encargo completo: interpreto los cinco momentos dentro de un mismo sistema visual.**                                                            |      ☑     |       ☐       | La galaxia representa los cinco momentos mediante el comportamiento de los walkers: la posibilidad está en las direcciones aleatorias, la tendencia en la preferencia hacia una dirección, la normalidad en los pasos cortos con distribución normal, la excepción en los Levy Flights y las supernovas, y la influencia en la modificación de las probabilidades cuando el usuario hace clic. Todo ocurre dentro del mismo sistema visual. |
| **Simulación con intención: utilizo al menos tres conceptos de la unidad para comunicar las ideas del encargo.**                                  |      ☑     |       ☐       | Se utilizaron caminatas aleatorias, distribución normal y Levy Flights para construir el comportamiento del sistema. Cada uno cumple una función conceptual diferente y contribuye a la representación de la galaxia.                                                                                                                                                                                                                       |
| **Interacción significativa: la interacción modifica el comportamiento o las probabilidades del sistema, que también funciona sin intervención.** |      ☑     |       ☐       | El clic del usuario cambia la probabilidad de movimiento al aumentar la influencia hacia una dirección y genera un nuevo walker. Sin interacción, el sistema continúa funcionando, creando estrellas y eventos excepcionales de manera autónoma.                                                                                                                                                                                            |
| **Prototipo funcional: la experiencia puede ejecutarse y recorrerse completa sin errores que impidan comprenderla.**                              |      ☑     |       ☐       | El prototipo funciona en tiempo real, mantiene el formato 9:16 y permite observar todos los comportamientos del sistema sin fallos que afecten su comprensión.                                                                                                                                                                                                                                                                              |
| **Proceso documentado: la bitácora evidencia avances, decisiones, dificultades, soluciones, uso de IA y enlace al prototipo.**                    |      ☑     |       ☐       | La bitácora incluye la intención conceptual, experimentos, versiones intermedias, decisiones de diseño, dificultades encontradas, soluciones implementadas, explicación del uso de IA generativa y el enlace al prototipo junto con evidencias visuales.                                                                                                                                                                                    |



