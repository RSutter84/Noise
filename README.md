# Noise
For this assignment, we were required to use noise and some degree of mouse interactivity. I kept things relatively simple here (due to time contraints. 

So I used noise to generate circles of varying sizes, I then also used noise to animate their x and y positions to make them appear like they are floating. For mouse functionality, I implemented a cursor-hover, so that when you hover over a circle it changes it's Alpha (and returns to normal when not touched by the cursor. 
Very simple! But I only had so much time.

## Code:
```
let circles = [];
let numCircles = 100

function setup() {
  createCanvas(800, 800)
  noStroke()

  for (let i = 0; i < numCircles; i++) {
    let x = random(width);
    let y = random(height);
    let circleSize = noise(i * 0.1) * 100 + 20
    let noiseOffsetX = random(1000)
    let noiseOffsetY = random(1000)

    circles.push(new Circle(x, y, circleSize, noiseOffsetX, noiseOffsetY))
  }
}

function draw() {
  background(0)
  for (let circle of circles) {
    circle.update()
    circle.display()
  }
}

class Circle {
  constructor(x, y, circleSize, noiseOffsetX, noiseOffsetY) {
    this.x = x
    this.y = y
    this.size = circleSize
    this.baseAlpha = 255
    this.alpha = 255
    this.noiseOffsetX = noiseOffsetX
    this.noiseOffsetY = noiseOffsetY
  }

  update() {
    let t = frameCount * 0.005
    this.x += (noise(this.noiseOffsetX + t) - 0.5) * 2
    this.y += (noise(this.noiseOffsetY + t) - 0.5) * 2

    let d = dist(mouseX, mouseY, this.x, this.y)
    this.alpha = d < this.size / 2 ? 50 : this.baseAlpha
  }

  display() {
    fill(255, this.alpha)
    ellipse(this.x, this.y, this.size)
  }
}
```

## p5 Sketch Link:
[https://editor.p5js.org/rsutter/full/llwXjHgxG](https://editor.p5js.org/rsutter/full/S1lUH2hNO)
