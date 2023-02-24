# PRIMEIRO-PROJETO-JOGO-PONG
NECESSITO DE MAIS APRENDIZADOS PARA MELHORAR A MECÂNICA DO JOGO, PORÉM ESTOU FELIZ POR CONSEGUIR CONCLUIR!
LINHA DE CODIGOS//

//CRIADO POR Rafael melo

//

//sons do jogo
let raquetada;
let sompontos;
let trilhasonora;

  function preload (){
    trilha = loadSound ('trilha.mp3');
    ponto = loadSound ("ponto.mp3");
  raquetada = loadSound ("raquetada.mp3");
    
  }

function setup() {
  createCanvas(600, 400);
trilha.loop();
}


//BUG
let bolinhaNaoFicaPresa;

    //variaveis da bolinha  

let yBolinha = 200;
let xBolinha = 300;
let Diametro = 30;
let velocidadeXBolinha = 6;
let velocidadeYBolinha = 6;
let raio = Diametro / 2;
 
 //VARIAVEIS DAS RAQUETES;
  
let xRaquete = 5;
let yRaquete = 175;
let raquetecomprimento = 8;
let raquetetamanho = 70;
let angulo = 10;
let colidiu = false;
// Raquete do oponete;
let XRaqueteOponente = 587;
let YRaqueteOponente = 175;
let velocidadeYOponente;
let chanceDeErrar = 0;

//PLACAR DO JOGO;

let meusPontos = 0;
let pontosOponente = 0;

function draw() {
  
  background (40);
  mostrarBolinha();
  movimentaBolinha();
  verificacolisaoBorda();
  mostraRaquete(xRaquete, yRaquete);
  movimentosMinhaRaquete();
  //verificaColisaoRaquete();
  verificacolisaoRaquete(xRaquete, yRaquete);
  mostraRaquete(XRaqueteOponente, YRaqueteOponente);
  movimentaRaqueteOponente();
  verificacolisaoRaquete(XRaqueteOponente, YRaqueteOponente);
  incluirPlacar();
  marcarPontos();

  

function bolinhaNaoFicaPresa(){
    if (XBolinha - raio < 0){
    XBolinha = 50
    }
}

  
  function mostrarBolinha(){
  circle (xBolinha, yBolinha, Diametro);
  }
  
  
  function movimentaBolinha(){
     xBolinha += velocidadeXBolinha;
  yBolinha += velocidadeYBolinha;
  }
  
  function verificacolisaoBorda(){
     if (xBolinha + raio > width || xBolinha - raio < 0) {
        velocidadeXBolinha *= -1;
    }
    if (yBolinha + raio > height || yBolinha - raio < 0) {
        velocidadeYBolinha *= -1;
      
    }
  }
  //Mostrar minha raquete//
  function mostraRaquete(X,Y) {  rect (X,Y, raquetecomprimento, raquetetamanho, angulo);
   }                        
}


  // movimentos de raquete;
  
  function movimentosMinhaRaquete() {
    if (keyIsDown (UP_ARROW)){
      
      yRaquete -= 10;
    }
   
    if (keyIsDown (DOWN_ARROW)) {
      yRaquete += 10;
    }
  }
function verificaColisaoRaquete() {
  if (xBolinha - raio < xRaquete + raquetecomprimento
     && yBolinha - raio < yRaquete + raquetetamanho
     && yBolinha + raio > yRaquete){
    velocidadeXBolinha *= -1
    raquetada.play();
  }
}
  
 function verificacolisaoRaquete(X, Y) {
   colidiu = collideRectCircle(X,Y, raquetecomprimento, raquetetamanho, xBolinha, yBolinha, raio); 
   if (colidiu){
      velocidadeXBolinha *= -1
     raquetada.play();
   }
  
}




//TESTE;


function calculaChanceDeErrar() {
  if (pontosOponente >= meusPontos) {
    chanceDeErrar += 1
    if (chanceDeErrar >= 35){
    chanceDeErrar = 44
    }
  } else {
    chanceDeErrar -= 1
    if (chanceDeErrar <= 39){
    chanceDeErrar = 35
    }
  }
}




 function movimentaRaqueteOponente() {
   velocidadeYOponente = yBolinha - YRaqueteOponente - raquetecomprimento /2 - 30
   YRaqueteOponente += velocidadeYOponente + chanceDeErrar
   calculaChanceDeErrar();

  
 }
function incluirPlacar() {
  textAlign(CENTER)
  fill (color (255, 140, 0));
  rect (195 , 10, 40, 20, 10);
   fill (255);
  text (meusPontos, 215, 26);
  fill (color (255, 140, 0));
   rect (350 , 10, 40, 20, 10);
  fill (255);
  text (pontosOponente, 370, 26);
   
}

function marcarPontos() {
  if (xBolinha > 585) {
    meusPontos += 1
    ponto.play();
}
if (xBolinha < 15) {
  pontosOponente += 1
  ponto.play();                
}
}



