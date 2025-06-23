# codigojardineiro
let jardineiro;
let plantas = [];
let temperatura = 10;
let totalArvores = 0;

                                              
function setup() {
  createCanvas(600, 400);
  jardineiro = new Jardineiro(width / 2, height - 50);
}


function draw() {
  
  
  let corFundo = lerpColor(color(217, 112, 26), color(219, 239, 208),
    map(totalArvores, 0, 100, 0, 1));

  background(corFundo);
  mostrarInformacoes();
  temperatura += 0.1;
  jardineiro.atualizar();
  jardineiro.mostrar();
  verificarFimDeJogo();
  plantas.map((arvore) => arvore.mostrar());
}

function mostrarInformacoes() {
  textSize(16);
  fill(0);
  text("Vamos plantar arvores para reproduzir a temperatura", 10, 30);
  textSize(14);
  fill('white');
  text("Temperatura:  " + temperatura.toFixed(2), 10, 390);
  text("Árvores plantadas:  " + totalArvores, 460, 390);
  text("Para movimentar o personagem use as setas do teclado.", 10, 60);
  text("Para plantar árvores use P ou espaço.", 10, 80);
}
function verificarFimDeJogo() {
  if (totalArvores > temperatura) {
    mostrarMensagemDeVitoria();
  } else if (temperatura > 50) {
    mostrarMensagemDeDerrota();
  }
}
function mostrarMensagemDeVitoria() {
  textSize(20);
  fill(0, 0, 0);
  text("Você venceu! Você plantou muitas árvores!", 100, 200);
  noLoop();
}

function mostrarMensagemDeDerrota() {
  textSize(20);
  fill(0, 0, 0);
  text("😒 Você perdeu! A temperatura está muito alta", 100, 200);
  noLoop();
}

class Jardineiro {
  constructor(x, y) {
  this.x = x;
  this.y = y;
  this.emoji = '🧑‍🌾';
  this.velocidade = 3
}
  atualizar() {
    if (keyIsDown(LEFT_ARROW)) {
      this.x -= this.velocidade;
    }
    if (keyIsDown(RIGHT_ARROW)) {
      this.x += this.velocidade;
    }
    if (keyIsDown(UP_ARROW)) {
      this.y -= this.velocidade;
    }
    if (keyIsDown(DOWN_ARROW)) {
      this.y += this.velocidade;
    }
  }
  mostrar() {
    textSize(32);
    text(this.emoji, this.x, this.y);
  }
}
function kayPressed() {
 if (key === ' '|| key === 'p') {
  let arvore = new Arvore(jardineiro.x, jardineiro.y);
  plantas.push(arvore);
  totalArvore++;
  temperatura -= 3;
  if (temperatura < 0) temperatura = 0;
 }
}
class Arvore {
  constructor(x,y) {
    this.x = x;
    this.y = y;
    this.emoji = '🌳';
  }
  mostrar (){
    textSize(32);
    text(this.emoji, this.x, this.y);
  }
}
