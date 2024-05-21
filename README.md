# js.xbolinha

let ball;

let leftPaddle, rightPaddle;

function setup() {

  createCanvas(800, 400);

  

  // Inicializa a bola no centro da tela

  ball = new Ball();

  

  // Inicializa as raquetes

  leftPaddle = new Paddle(true);

  rightPaddle = new Paddle(false);

}

function draw() {

  background(0);

  

  // Desenha e movimenta a bola

  ball.update();

  ball.show();

  

  // Desenha e movimenta as raquetes

  leftPaddle.show();

  rightPaddle.show();

  leftPaddle.update();

  rightPaddle.update();

  

  // Checa colisão com as raquetes

  ball.checkPaddleCollision(leftPaddle);

  ball.checkPaddleCollision(rightPaddle);

}

class Ball {

  constructor() {

    this.reset();

  }

  

  reset() {

    this.x = width / 2;

    this.y = height / 2;

    this.xSpeed = random(4, 6) * (random() > 0.5 ? 1 : -1);

    this.ySpeed = random(3, 5) * (random() > 0.5 ? 1 : -1);

    this.radius = 12;

  }

  

  update() {

    this.x += this.xSpeed;

    this.y += this.ySpeed;

    

    if (this.y < 0 || this.y > height) {

      this.ySpeed *= -1;

    }

    

    if (this.x < 0 || this.x > width) {

      this.reset();

    }

  }

  

  show() {

    fill(255);

    noStroke();

    ellipse(this.x, this.y, this.radius * 2);

  }

  

  checkPaddleCollision(paddle) {

    if (this.x - this.radius < paddle.x + paddle.w && this.x + this.radius > paddle.x &&

        this.y > paddle.y && this.y < paddle.y + paddle.h) {

      this.xSpeed *= -1.1;

      this.ySpeed *= 1.1;

    }

  }

}

class Paddle {

  constructor(isLeft) {

    this.w = 10;

    this.h = 100;

    this.x = isLeft ? 0 : width - this.w;

    this.y = height / 2 - this.h / 2;

    this.ySpeed = 0;

    this.isLeft = isLeft;

  }

  

  update() {

    this.y += this.ySpeed;

    this.y = constrain(this.y, 0, height - this.h);

    

    if (this.isLeft) {

      if (keyIsDown(87)) {

        this.ySpeed = -5;

      } else if (keyIsDown(83)) {

        this.ySpeed = 5;

      } else {

        this.ySpeed = 0;

      }

    } else {

      if (keyIsDown(UP_ARROW)) {

        this.ySpeed = -5;

      } else if (keyIsDown(DOWN_ARROW)) {

        this.ySpeed = 5;

      } else {

        this.ySpeed = 0;

      }

    }

  }

  

  show() {

    fill(255);

    noStroke();

    rect(this.x, this.y, this.w, this.h);

  }

}


