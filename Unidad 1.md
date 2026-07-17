# Unidad 1: Aleatoriedad🫧🪼
##Actividad 03##

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
    const choice = floor(random(5));
    if (choice == 0) {
      this.x1++;
      this.y1--;
    } else if (choice == 1) {
      this.x2++;
      this.y2--;
    } else if (choice == 2) {
      this.y1++;
      this.y2++;
    } else if (choice == 3) {
      this.y2--;
      
      } else if (choice == 4) {
      this.x3++;
      this.y3++;
      
    }
  }
}

```
