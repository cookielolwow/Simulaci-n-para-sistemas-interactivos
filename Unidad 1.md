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
```
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

