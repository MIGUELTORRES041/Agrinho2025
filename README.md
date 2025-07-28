# Agrinho2025
let arvores = [];
let gotas = [];
let energia = 0;

function setup() {
  createCanvas(800, 500);
  textFont('Georgia');
}

function draw() {
  background(180, 230, 255);
  
  // céu e sol
  drawSol();
  
  // Chão
  fill(100, 200, 100);
  rect(0, height - 100, width, 100);
  
  // Painel solar
  drawPainel();
  
  // Água da chuva
  drawAgua();
  
  // Árvores
  for (let arvore of arvores) {
    arvore.mostrar();
  }
  
  // Gotas de água caindo
  for (let gota of gotas) {
    gota.cair();
    gota.mostrar();
  }
  
  // Energia e dicas
  fill(0);
  textSize(16);
  text(`Energia gerada: ${energia} kWh`, 20, 30);
  text("Clique no chão para plantar. Pressione 'R' para regar.", 20, 50);
}

function mousePressed() {
  if (mouseY > height - 100) {
    arvores.push(new Arvore(mouseX, mouseY));
  }
}

function keyPressed() {
  if (key === 'R' || key === 'r') {
    for (let arvore of arvores) {
      gotas.push(new Gota(arvore.x, arvore.y - 50));
      arvore.crescer();
    }
    energia += 5;
  }
}

function drawSol() {
  fill(255, 204, 0);
  ellipse(700, 80, 80, 80);
}

function drawPainel() {
  fill(60);
  rect(600, height - 150, 80, 40);
  fill(0, 100, 255);
  for (let i = 0; i < 4; i++) {
    rect(605 + i * 18, height - 145, 15, 30);
  }
  fill(255);
  textSize(14);
  text("Painel Solar", 600, height - 160);
}

function drawAgua() {
  fill(0, 150, 255);
  rect(50, height - 70, 60, 40);
  fill(255);
  textSize(14);
  text("Água da chuva", 30, height - 80);
}

// Classe Árvor
class Arvore {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.altura = 30;
  }
  
  mostrar() {
    fill(139, 69, 19);
    rect(this.x - 5, this.y - this.altura, 10, this.altura);
    fill(34, 139, 34);
    ellipse(this.x, this.y - this.altura, 40, 40);
  }
  
  crescer() {
    if (this.altura < 100) {
      this.altura += 5;
    }
  }
}

// Classe Gota
class Gota {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  
  cair() {
    this.y += 5;
  }
  
  mostrar() {
    fill(0, 100, 255);
    ellipse(this.x, this.y, 5, 10);
  }
}
